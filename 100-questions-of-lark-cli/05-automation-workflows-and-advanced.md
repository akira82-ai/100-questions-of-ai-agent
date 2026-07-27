# Chapter 5 · Automation Workflows and Advanced Practice

## 81. How to make Feishu CLI automation tasks run on a schedule

Wiring the CLI to a scheduled dispatcher is the watershed from "occasional use" to "continuous auto-run."

The lightest solution is the system's built-in scheduler. Linux and macOS use cron, Windows uses Task Scheduler. Write a shell script wrapping the CLI commands you want to run, then let cron trigger it on time. Push today's schedule at 8 every morning, send the weekly report at 5 every Friday; fixed-frequency tasks like these are fully covered by cron.

Cron condition examples:

```bash
# push today's schedule at 8:00 every morning
0 8 * * * /usr/local/bin/lark-cli calendar +agenda --as user >> /var/log/lark-daily.log 2>&1

# send weekly report at 17:00 every Friday
0 17 * * 5 /home/user/scripts/weekly-report.sh
```

The advanced solution is a dedicated task scheduler. If you already use n8n, Airflow, or GitHub Actions, wrap the CLI command into a step and plug it in, getting more complete retry, monitoring, and alerting capabilities.

The containerized solution suits scenarios needing stable residency. Put the CLI into a Docker image and manage scheduling with container orchestration (Kubernetes CronJob, Docker Compose), suited for enterprise automation.

Several engineering details to note. First, do not hardcode personal paths or credentials in CLI commands; pass them via environment variables. Second, give each task an independent log, so when something breaks you can quickly locate which step hung. Third, make side-effecting commands (send message, write doc) idempotent, avoiding sending twice when the timer triggers repeatedly. Fourth, token expiration makes tasks fail silently; add a `lark-cli auth status` pre-check in the scheduling script, and alert if the token is bad rather than hard-running.

## 82. How to wire the Feishu CLI into a CI/CD pipeline

Putting the CLI into a CI/CD pipeline, automatically pushing build results, deploy status, and test reports to a Feishu group, is one of the highest-frequency automation scenarios for R&D teams.

Integration has two layers. The first is the Runner layer: the CI/CD execution machine must have the CLI installed and auth login done. GitHub Actions, GitLab CI, Jenkins, these mainstream tools all support custom Runners; adding a line `npx @larksuite/cli@latest install` in the Runner init script installs it. The second is the Pipeline config layer: call the CLI command at some stage of the pipeline.

GitHub Actions integration example:

```yaml
- name: Notify Feishu on deploy success
  run: |
    lark-cli im +messages-send \
      --as bot \
      --chat-id ${{ secrets.FEISHU_DEPLOY_CHAT_ID }} \
      --text "✅ ${{ github.repository }} deployed successfully, commit: ${{ github.sha }}"
```

Credential management uses the CI/CD platform's secrets mechanism; do not write app_secret or token into the code repository. GitHub Actions uses secrets, GitLab CI uses variables, Jenkins uses credentials.

Identity choice in the CI/CD scenario has its particulars. Using the bot identity for push messages is more stable; the token is tenant_access_token, no manual re-authorization needed. If you need to see personal-related data (like someone's PR list), use the user identity but accept the cost of periodic re-login; relogin is troublesome in CI environments, so best to fix on the bot.

On notification content design, do not stuff the entire build log into the message. A build-result summary plus a detail link (pointing to the CI platform's build page) lets people click the link if they want details, keeping the Feishu group message volume lean.

Failure alerts should be tiered. Build failure pushes a red message to the R&D group, deploy failure pushes an urgent message to the owner's private chat, test-coverage drop pushes a warning to the quality group. Different severities go through different channels, avoiding alert fatigue.

## 83. How event subscription lets AI respond to Feishu messages in real time

Scheduled tasks are the CLI actively querying; event subscription is Feishu actively pushing to you. To have AI reply instantly when someone @s the bot, auto-welcome when someone joins the group, or trigger a notification when a doc is modified, all rely on event subscription.

The Feishu CLI provides a dedicated `lark-event` skill for event subscription. It receives Feishu's real-time events through a WebSocket long connection, supporting regex routing and agent-friendly output formats.

Basic usage:

```bash
# listen to IM message events
lark-cli event consume im.message.receive_v1

# listen to multiple events and filter with regex
lark-cli event consume --filter 'im.message.receive_v1' --regex '@bot\s+help'
```

The working mechanism of event subscription: you subscribe to certain events on the Feishu Open Platform (like `im.message.receive_v1`), and Feishu pushes to you via webhook or WebSocket when the event occurs. The CLI's event consume command maintains the WebSocket connection, and after receiving an event routes it to different processing logic per your filter rules.

Compared with the webhook approach, WebSocket's advantage is no public IP or domain needed. The webhook requires Feishu to be able to access your server, unfriendly to intranet deployment; WebSocket is your client actively connecting to Feishu, firewall-friendly. This is also why the CLI defaults to WebSocket.

To make AI truly "respond" to events, you need to chain event consume with the AI Agent. One pattern is event consume writes events to a queue, and another Agent process reads from the queue and processes. Another pattern is consume directly calls the Agent's interface after receiving an event (like Claude Code's prompt interface).

Engineering notes: event consumption must be idempotent. Feishu re-pushes when unsure whether you received it, and the same event may be consumed multiple times; the processing logic must recognize duplicates. Do not block the consume main loop with time-consuming operations; use an async queue to absorb them. The WebSocket disconnect needs a reconnect mechanism; the CLI has auto-reconnect built in, but your own consumption logic hanging will not auto-recover.

## 84. How to write a custom Skill to wrap repeated operations

After using the CLI for a while you will find certain operations recur: every weekly report is the same command combination, every task sync is the same flow. This is when you should write a custom Skill to wrap them.

The Feishu CLI provides `lark-skill-maker`, a skill specifically to help you create custom skills. It is at heart a framework letting you write a SKILL.md per the spec, defining the skill's trigger conditions, parameters, and execution logic, and the CLI loads it like a built-in skill.

Basic steps to write a custom skill.

Step one, clarify what this skill does. Like "every Friday afternoon automatically pull this week's completed items from Base, organize into a weekly-report markdown, send to the specified group." Break it into atomic actions: query Base, organize data, generate markdown, send message.

Step two, write SKILL.md. The file structure includes skill name, description, trigger words, parameter definitions, execution steps. In the execution steps write clearly which CLI command each atomic action calls, what parameters, how to handle the return.

Step three, test. Run the execution steps with dry-run, confirm each step's input/output matches expectations.

Step four, deploy. Put the SKILL.md into the skills directory, and the CLI auto-loads it.

A few suggestions when actually writing skills. Parameter design should be Agent-friendly, with clear names and descriptions so the Agent can correctly extract parameters from the user's natural language. Error handling should be robust: when a step fails, give clear next-step advice (retry, degrade, human intervention). Break complex logic into multiple small skills combined; do not write one skill as a hundreds-of-lines monster.

Someone in the community hoped for "selective install" skill capability, installing only the few domains you need, avoiding all 26 skills injecting and occupying context. The official is still evaluating this need; for now you can manually manage the locally installed skill list, deleting the ones you do not use.

## 85. How to handle Base cross-table relations with the Feishu CLI

The power of Base lies in cross-table relations: an orders table relates to a customers table, a tasks table relates to a members table. But this structure hits some special problems when operated with the CLI.

The field type for cross-table relations is called a lookup field; its value is not direct data but a reference to a record in another table. When the CLI reads such a field it gets a record_id, not the actual content in the related table. To see the customer name instead of a string of recXXXXXX, you need to call the API again to query the related table's corresponding record.

This is a high-frequency operation when writing automation scripts. The pragmatic approach is to write a helper function: input record_id and field definition, automatically resolve the lookup field and return the related table's actual value. This function has very high reuse rate; recommend putting it in your tool library.

The reverse operation (writing the relation field) also needs care. When writing a lookup field the value passed must be an existing record_id in the related table; passing wrong either errors or creates an empty relation. Before writing, first query the related table to confirm the record_id exists; this is a safe habit.

Cross-table query performance. If you want to batch-process 500 records of an orders table, each relating to the customers table, the naive approach is 500 queries to the customers table. The optimization is to first batch-query all the customer record_ids involved in this batch, fetch the customers table data in one go, and do the join in memory. This drops from 500 requests to 2.

Base also supports formula fields for cross-table calculation and rollup fields for aggregation. These fields are read-only; the CLI can read but not write, so avoid them in write operations.

Practical advice for complex business scenarios: treat Base as structured data storage plus simple relations, and put complex business logic into external code. Base's relation capability suits lightweight scenarios; heavy relations are more reliably handled by a proper database.

## 86. How to batch-manage Feishu task lists with the CLI

Feishu's task system is more capable than imagined, and paired with the CLI can do fairly deep batch management.

Basic operation chain. `lark-cli task +get-my-tasks` lists tasks, `lark-cli task +create` creates tasks, `lark-cli task +complete` completes tasks, `lark-cli task +update` updates task details. These atomic commands combined cover the vast majority of batch scenarios.

Typical scenario one: batch create. At project kickoff, create three tasks each for five members, fifteen total. Use a script reading a CSV or JSON config, looping `task +create`. Each task's title, due time, owner, and owning list all come from the config.

Typical scenario two: batch complete. A milestone ends, mark all incomplete tasks under it complete at once. First `task +get-my-tasks --list-id xxx --status incomplete` to pull the incomplete list, then loop `task +complete`.

Typical scenario three: batch reassign. An employee leaves, transfer all tasks under their name to the successor. First filter and pull the list by owner, then loop update to change assignee.

Typical scenario four: overdue-task reminder. Scan all incomplete tasks daily, push a message to the owner when overdue is found. Paired with cron, this is an automated overdue-urge system.

Several engineering points. Batch operations use `--page-all` for auto-pagination, do not flip manually. The task ID field is called task_guid or task_id, and parameter names differ slightly across commands; `--help` before writing the script to confirm. Subtask handling is similar to main tasks, but the parameter must carry parent_id.

Task linkage with other Feishu business domains. Tasks can be auto-extracted from meeting notes (using the minutes to-do field), synced from a Base row, or hooked to the calendar for reminders. These linkages need your own glue code; the CLI provides atomic capability, and the combination is up to your business.

## 87. How to package and distribute a custom Skill to the team

After writing a custom skill, if other team members also need it, distribution is a practical problem.

The simplest way is a Git repository. Commit the skill file to a repo, team members clone it and copy to their own skills directory. The advantage is version control, updates via git pull. The downside is more manual operations; members may not know when the skill updates.

The advanced way is to make it an npm package. The skill file is at heart markdown plus possible scripts; after packaging as an npm package, team members install with `npm install`, paired with `npx skills add` to register to the CLI. This suits cross-team, cross-company distribution, and also facilitates version management and dependency declaration.

Enterprises can use internal package management. Push the skill package to the enterprise private npm registry, or package as a tar file on the intranet share. Team members install from the internal source, not depending on the public network.

Details to handle when distributing. First, hardcoded paths and credentials in the skill must be parameterized; different people's environment paths differ, and hardcoding makes the skill not run. Second, the skill's dependencies must be explicitly declared (which CLI version it depends on, which scopes), so installers know the prerequisites. Third, write a simple README explaining what the skill does, how to install, how to use.

On version management, give the skill a semantic version. Breaking changes bump the major, new features bump the minor, bug fixes bump the patch. Team members can judge from the version number whether an upgrade will break things.

The ideal form of skill distribution is an official marketplace, like the VS Code extension store with one-click install. The Feishu CLI has not reached this yet, but the community's issues already discuss this direction. For now Git and npm packages are enough, just the process is less automated.

## 88. Can one Feishu CLI authorization be shared by a team?

This is a question unavoidable when promoting to a team. Short answer: technically yes, practically not recommended.

Technical feasibility. One Feishu app has a set of app_id and app_secret; multiple people auth login with the same set of credentials, and each person gets their own user token (user identity) or a shared tenant token (bot identity). The bot identity is natively shared; the user identity is independent per person.

Reasons not to recommend sharing.

First, blurred permission boundaries. Sharing the app means sharing the permission scope; A needs doc write permission, B does not, but B's token also carries doc write permission. The least-privilege principle is broken.

Second, difficult auditing. All operations are under the same app name; when something goes wrong you cannot trace which person executed it. Feishu's backend audit log can only see the app dimension, not the user dimension.

Third, stability risk. Sharing the app means one person resetting the app_secret invalidates everyone's credentials. One person changing the permission config affects everyone.

Fourth, the token mutual-kick problem. When multiple Agents use the same bot identity, the later login kicks the earlier; see Q55 in Chapter 3 for details.

The recommended multi-user approach. Each user config init's their own independent app, auth login with their own credentials. The apps are completely isolated; permission, auditing, and stability do not affect each other. If enterprise management is strict, the IT department uniformly creates apps and assigns to employees, and each person still gets independent credentials.

Whether the bot identity is shared depends on the scenario. CI/CD notifications and other scenarios with no personal ownership are fine with a shared bot. Scenarios involving personal-data operations, the bot identity is less compliant than the user identity.

At the enterprise-admin level, you can control who can create apps and who can authorize the CLI through the Feishu backend's app management, controlling the shared risk at the source.

## 89. How can an enterprise admin control who can create CLI apps?

Promoting the CLI in an enterprise, the admin's biggest worry is losing control. Employees casually create apps and authorize, permissions fly everywhere, auditing is difficult. Fortunately the Feishu Open Platform provides several control levers.

The first lever is app-creation approval. Feishu Enterprise Edition can set "creating apps requires admin approval" in the backend. When an employee wants to config init a new app, it must be approved by an admin before creation. This is the key to controlling app count at the source.

The second lever is app-permission approval. For each app, which scopes to enable, the admin can set high-risk permissions to require approval. An employee opens doc-delete permission for the CLI app, the admin receives an approval request, and can reject if inappropriate.

The third lever is app-visibility control. The admin can restrict the app to only visible within the enterprise, forbidding publishing to the app market. CLI-type internal-tool apps should default to internal visibility.

The fourth lever is the audit log. The Feishu backend provides a complete operation log: which app called which interface, when, what it returned, all queryable. When something goes wrong it can be traced to the specific app, then combined with the app's user list to locate the person.

The fifth lever is the app-disable mechanism. When an employee leaves or transfers, the admin disables their created CLI app, immediately cutting access. This is faster than waiting for the token to naturally expire.

Implementation advice. Pilot in a small scope first, let IT or the efficiency team use it first, get a management flow running, then open to all. Supporting docs must keep up, writing clearly "how employees apply for CLI apps," "how admins approve," "who to find when something goes wrong."

For the enterprise, the CLI control focus is on letting employees use it controllably, not banning it outright. Banning it makes employees go around to less-controllable tools. Open the front door and block the back door; that is the correct posture of governance.

## 90. How to choose between event subscription and polling without wasting quota

There are two ways to get Feishu data changes: event subscription (Feishu pushes to you) and polling (you actively query). Each has its cost; choosing wrong either misses real-time or wastes API quota.

Event subscription suits: message arrival, group-member changes, approval-status changes, new doc comments. These events occur at unpredictable times; polling would need high-frequency queries to respond timely, consuming large quota. Event subscription is Feishu actively pushing, best real-time, and you only process when the event arrives, zero consumption otherwise.

Polling suits: periodic statistics (compute a data summary once a day), batch sync (pull incremental data hourly), status confirmation (wait for some async task to complete). These scenarios have low real-time requirement; querying once on schedule is enough, and event subscription would be over-engineering.

The hybrid model is the pragmatic choice. Core business uses event subscription for real-time; non-core data uses low-frequency polling (like every 15 minutes) balancing cost. For example customer-service messages go through event subscription for second-level response, data reports poll every 15 minutes.

Quota-consumption considerations. The Feishu Open Platform has API call-frequency limits per app; polling too frequently triggers rate-limiting. Event subscription does not consume API quota (event push is Feishu-side active behavior), but WebSocket connection count has an upper limit. Before large-scale polling, calculate clearly: how many objects to query, how big each, how often, estimate the total request volume and compare with quota.

Tips to reduce polling consumption. Use incremental query instead of full query, each time only pulling changes since the last sync. Use webhook instead of polling if Feishu supports the corresponding event. Use caching to reduce duplicate queries; data queried recently is not queried a second time shortly after.

Selection criterion: high real-time requirement + unpredictable events = event subscription; low real-time requirement + stable data = polling; mixed needs = core event subscription + edge polling.

## 91. How to monitor whether an automation script is actually running

Finishing the script development is only the start; stable running after launch is the real challenge. An automation script with no monitoring hangs and you do not know; only when users feedback "hey why no notification" do you find it stopped a week ago.

The first layer of monitoring is process liveness. Scheduled tasks (cron, Kubernetes CronJob) record execution status after finishing; several consecutive non-executions mean the scheduler broke. Resident services (WebSocket consumption, polling services) use process-monitoring tools (systemd, supervisor, PM2) to guard, auto-restart and alert on hang.

The second layer is execution results. Each script run records key metrics: execution duration, success/failure, how many records processed, any exceptions. These metrics push to a monitoring system (Prometheus, CloudWatch) or simply write to a log file, checked periodically.

The third layer is business effect. The script "ran successfully" does not mean "business is normal." For example your task is to push schedule daily; the script returns success but actually did not send (token expired, network jitter), and the business failed. This kind requires monitoring the terminal effect: did the message actually send (see the message_id Feishu returned), did the doc actually update (fetch to confirm).

The alerting mechanism should be tiered. One script failure may be occasional; alert only after three consecutive failures. Important business (deploy notification, customer messages) alerts immediately on failure; secondary business (weekly report, statistics) tolerates delay. The alert channel should not be only Feishu messages; if Feishu itself is the fault source, the alert cannot be sent either, so have SMS or email as fallback.

Log management. Each script gets an independent log file, rotated by date and kept 30 days. The log records key steps' input/output, so you can trace back when something breaks. Do not only record "executed successfully"; record "what command executed, what parameters passed, what returned."

Health-check endpoint. If it is a resident service, expose an HTTP health-check interface for external monitoring (uptime robot, Prometheus blackbox) to probe liveness periodically. Service returns 200 normally, non-200 on anomaly.

The CLI's built-in `lark-cli doctor` can be integrated into the monitoring script, periodically checking credential status and network connectivity, warning before problems actually occur, rather than waiting for the task to truly fail.

## 92. How to isolate identities across multiple Feishu apps

One person managing multiple Feishu apps is a common scenario: company-main app, personal test app, client-delegated management app. These apps' identities must be strictly isolated; mixing them causes big trouble.

The Feishu CLI's profile mechanism is designed for multi-app isolation. Each profile corresponds to an independent config directory, storing its own app_id, app_secret, token, and scope. Switching profiles equals switching app identity, with the two not interfering.

Basic profile operations:

```bash
# create new profile
lark-cli config init --profile client-a

# switch to specified profile
lark-cli config use client-a

# view current profile
lark-cli config show

# list all profiles
lark-cli config list
```

Each profile auth login's independently; tokens are stored in their respective config directories or keychain entries. Profile A's operations do not affect Profile B's credentials.

Isolation engineering practice. First, each project uses an independent profile, and the project code specifies the profile name via environment variable, avoiding misusing the default profile. Second, name profiles clearly, using project or client names, not vague names like test1, test2. Third, periodically clean unused profiles, reducing misoperation risk.

CI/CD multi-app isolation uses environment variables. Each pipeline configures its own app_id, app_secret, and the script reads them via environment variables, not depending on the profile file. This way different pipelines are naturally isolated.

Containerized deployment isolation is more thorough. Each app runs an independent container, with independent CLI config and credentials inside, physically isolated. One container breaking does not pollute another.

The typical accident of identity mixing: using app A's token to call app B's data, getting `open_id cross app` or `invalid param`. Such error messages are not obvious, easily mistaken for parameter assembly errors. When hitting this kind of bizarre auth error, step one is to confirm whether the profile is correct and which app's token it is.

The community reported low-signal errors caused by profile mismatch; the CLI's diagnostic info is improving, and new versions will more clearly distinguish bot and user identity status in doctor and auth status.

## 93. How to run the Feishu CLI as a resident service on a cloud server

Running the CLI locally suits development and testing; production-environment automation needs to run resident on a cloud server.

Several forms of resident service.

The first is scheduled-task type. The CLI itself is not resident, awakened by cron or systemd timer on schedule, exits after execution. Suited for fixed-frequency tasks (push schedule daily, send weekly report weekly). This is simplest; configure cron and done.

The second is event-consumption type. The CLI's event consume command maintains a WebSocket long connection and needs to run resident. Use systemd or supervisor to manage it as a service, auto-restart on hang. Suited for real-time response scenarios (message auto-reply, event-triggered notification).

The third is API-service type. Wrap a layer of HTTP interface over the CLI, providing a RESTful API outward, other systems call your interface and you relay to the CLI. Suited for enterprise internal middle-platform architecture, multiple business systems sharing one Feishu integration.

Key config on the cloud server.

Credential management. Do not write app_secret into code or config files committed to git. Use environment variables or the cloud platform's secrets management (AWS Secrets Manager, Kubernetes Secrets).

Network config. The cloud server must be able to reach Feishu's API domains. Domestic cloud servers accessing feishu.cn usually have no problem; overseas servers accessing larksuite.com must confirm network connectivity. Enterprise-intranet servers need IT to whitelist related domains.

Resource planning. The CLI itself is a lightweight tool; one resident event-consume process occupying tens of MB of memory is enough. But if your service also runs an Agent (like Claude Code), leave enough resources for the Agent.

Logs and monitoring. Resident services must have logs; systemd comes with journald, or write your own log file. Pair with the cloud platform's monitoring (CloudWatch, Aliyun monitoring) to watch process status.

High availability. Single-point services always have hang risk; important business goes on dual-machine hot standby or Kubernetes multi-replica. But the CLI's WebSocket event subscription does not support multiple replicas consuming the same event simultaneously; multi-replica needs deduplication or partitioning.

## 94. Feishu message history is capped at 14 days, how to archive long-term

Feishu group messages by default can only be scrolled back 14 days (enterprise edition may be longer, but has a cap). For compliance audit, knowledge accumulation, and dispute tracing, this period is not enough; you need to do long-term archiving yourself.

The basic idea of archiving is to periodically pull messages and store them in your own storage. Use `lark-cli im +chat-messages-list` or `im +messages-search` to batch-pull historical messages by time range, store into a database or object storage.

Several implementation patterns of archiving.

Pattern one: scheduled incremental pull. Run once every hour or day, pulling incremental messages over the past period. Paired with cron or a scheduler, continuously append to the archive. The advantage is simple implementation; the disadvantage is near-real-time not real-time, and if one pull fails data may be missed.

Pattern two: event-subscription real-time archive. Subscribe to the `im.message.receive_v1` event; each message is stored immediately upon arrival. The advantage is strong real-time and no missed data; the disadvantage is needing a resident service and depending on event-subscription stability.

Pattern three: hybrid. Event subscription does real-time archiving; scheduled tasks do reconciliation (compare the archive and Feishu's actual message count hourly, fill gaps if missing).

Completeness of archived content. Messages are not just text, but also images, files, replies, emoji reactions, and rich-text posts. Complete archiving must download these attachments too. Images and files use `im +messages-image-download` or `drive +download` to pull locally; attachments and the message body are associated with message_id.

Retrievability of the archive. After raw JSON is stored, an index must be built for efficient query. Elasticsearch suits full-text search; relational databases suit structured query. Multi-dimensional retrieval by group, by person, by time, by keyword is the basic capability of an archive system.

Extra requirements for compliance scenarios. Finance and legal industries have regulatory requirements for message archiving; the archive system must be tamper-proof (append-only or blockchain notarization), auditable (every access leaves a trace), and have a retention-period policy (keep 7 years or permanent). These exceed the CLI's capability range and need a dedicated compliance archive system; the CLI only handles the data-collection link.

Archiving is best done early for peace of mind. When you really need a message from three months ago and find it was not stored, remediation is too late. Wire up archiving as soon as a new group is created; that is the safe approach.
