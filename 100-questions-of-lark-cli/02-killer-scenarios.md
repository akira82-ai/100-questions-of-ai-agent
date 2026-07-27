# Chapter 2 · Killer Scenarios

## 17. The 5 killer scenarios most worth trying first with the Feishu CLI

After installing the Feishu CLI, the worst thing is not knowing what to do with it. Here are 5 scenarios proven to perform and get you started fastest, in recommended order.

First, daily and weekly report automation. Have the Agent pull this week's meetings from the calendar, pull progress from the task list, summarize into a doc, and send it to the group. What used to take 90 minutes now takes 5. This is the rigid need of the layer-2 efficiency white-collar, and the easiest scene to get that first "wow."

Second, automatic meeting-note organization. After a meeting, the Agent reads the Minute transcript, extracts to-dos, marks owners, generates a notes doc, and sends it to attendees. The to-dos can also auto-sync to the Feishu task list.

Third, push schedule and to-dos every morning. Configure a scheduled task: every morning at 8 the Agent pulls your calendar and incomplete tasks, organizes a brief, and sends it to a private chat or group.

Fourth, CI/CD result notification. After code merges or deploys finish, automatically push results to the R&D group, success to one group, failure to another.

Fifth, Base batch operations. Pour CSV into Base, query table data with natural language, monitor table changes to trigger notifications.

The common thread of these 5 scenarios: they are all high-repeatability, clearly-ruled, but time-consuming when done by hand each time. They are your starting point for the first efficiency burst from the CLI. Get one working first, then expand to the second and third.

## 18. How to tell AI in one sentence to send your weekly report to the group

The core idea is to break the weekly report into three steps: pull data, generate content, send message. Each step has a ready CLI command.

Pull data: the Agent calls `lark-cli calendar +agenda` for this week's meetings, `lark-cli task +get-my-tasks` for task progress, and if the data is in Base, `lark-cli base +records-list` to read it.

Generate content: after getting the raw data, the Agent generates markdown body per your weekly-report template, then calls `lark-cli docs +create` to create a Feishu doc.

Send message: finally call `lark-cli im +messages-send --chat-id "oc_xxx" --msg-type interactive` to send the doc link to the target group.

What you say to the Agent is: "Help me organize this week's meetings and tasks into a weekly report and send it to the R&D group." It completes these three steps itself.

The key point is identity choice. Pulling calendar and tasks needs the user identity, because it touches your personal data. Sending the message can be user or bot, depending on whether you want the group to see who sent it. For the first run, add `--dry-run`, preview without sending, confirm the content is right, then really send.

## 19. How to avoid sending the weekly report to the wrong person or group

The biggest fear in auto-sending to a group is sending it wrong. To prevent this, rely on three layers of fallback.

Layer one, hardcode the chat-id. Do not let the Agent find the group itself each time; it will find the wrong one. Store the target group's chat-id as a variable or hardcode it in the script in advance. The chat-id is a string starting with `oc_`, obtainable from the Feishu group link.

Layer two, dry-run preview. The first run, after changing the data source, or after changing the template, always run with `--dry-run` first. The Agent prints what it is about to send without really sending. Confirm it is correct, then remove the parameter and rerun.

Layer three, small-scale test. Before sending to a big group, first send to a test group with only yourself, get the whole chain working, then switch to the real group.

One common pitfall: the bot is not in the group, so sending fails with an error. Before sending, confirm the target group has your bot, otherwise the message will not go out and the Agent will get stuck retrying.

## 20. How to have AI auto-organize meeting notes and @ the relevant people

Feishu's meeting-notes chain is fairly complete, and the CLI covers the key nodes.

After the meeting, first get the Minute's minute_token. Then the Agent calls `lark-cli vc +notes --minute-tokens <token>` to pull the four structured data types: transcript, summary, to-dos, and chapters. After getting the to-do list, the Agent identifies the owner of each to-do and creates tasks with `lark-cli task +create --name "xxx" --assignee "ou_xxx"`.

The notes doc can be generated with `lark-cli docs +create`, containing basic meeting info, key discussion points, and the to-do list. Finally use `lark-cli im +messages-send` to send the doc link to the attendees' group, with `<at user_id="ou_xxx">` tags in the body to @ the relevant people.

One detail: the quality of to-do recognition depends on the clarity of the transcript. In multi-person meetings, heavy accents, or free-ranging discussions, the Agent's to-do extraction accuracy drops. For important meetings, recommend a human pass over the Agent-generated to-dos before sending.

## 21. How to auto-sync to-dos from meeting notes into a task list

After the notes are generated, the to-dos only close the loop if they land in Feishu tasks. Otherwise the notes doc sits there unread and the to-dos sink without a trace.

The practice is for the Agent to extract to-do items from the notes data and call `lark-cli task +create` for each. Each task carries a title, assignee, due date, and the linked notes doc. If you manage tasks in Base instead of Feishu tasks, switch to `lark-cli base +record-create` to write into the table.

One real pitfall: for a Base select field, if the option name the Agent writes does not match an existing option, the API silently creates a new option instead of erroring. The result is a bunch of duplicate options in the table. To prevent this, either explicitly tell the Agent in the prompt "only use existing options, do not create new ones," or do a field-get before record-upsert to confirm the option list.

## 22. How to have AI check your calendar for free slots and create a meeting

The most annoying part of scheduling is finding a time everyone is free. The Feishu CLI has a dedicated command for free-busy lookup.

The Agent first calls `lark-cli calendar +freebusy --user-ids "ou_a,ou_b,ou_c" --start-time xxx --end-time xxx` to check several attendees' busy/free status over a period, getting the slots where everyone is free. Then call `lark-cli calendar +time-suggestions` to let Feishu recommend suitable slots.

After confirming the time, use `lark-cli calendar +event-create` to create the event, with attendees, meeting title, and conference room. Find an available room with `lark-cli calendar +room-find`.

Note that checking free-busy needs the user identity; the bot identity cannot read personal calendars. If your Agent is shared by multiple people, each user's free-busy must be queried with their own token.

## 23. How to batch-manage Feishu calendar events with the CLI

Three common batch scenarios: batch create, batch update, batch delete.

Batch create: organize a batch of event data into JSON or CSV, write a loop calling `lark-cli calendar +event-create`. Suited for one-time batch creation like quarterly scheduling or project milestones.

Batch update: first `lark-cli calendar events list` to pull all events in a period, filter the ones to change, then call `lark-cli calendar events patch` for each. Suited for shifting all meeting times or bulk-changing rooms.

Batch delete: list first, then delete one by one. Deletion is irreversible, so always dry-run to preview the delete list, confirm, then really delete.

The biggest risk in batch operations is concurrency. Do not fire too many requests at once; Feishu APIs have QPS limits. The safe approach is a serial loop with a small delay between each.

## 24. How to have AI push your day's schedule and to-dos every morning

This is a typical scheduled-automation scenario, needing a timer paired with the CLI.

For the timer, cron or launchd both work. On macOS launchd is more native; on a Linux server cron is more universal. The scheduled task calls a script in which the Agent executes: pull today's schedule, pull incomplete tasks, summarize into a brief, send to the specified chat.

Recommend a fixed brief format, like: "Today you have 3 meetings, 2 overdue to-dos, 1 due today." Have the Agent output strictly in this format, not varying each time.

The push target depends on your habit. Sending to a private chat is most private; sending to a work group syncs the team. For first configuration, recommend sending to a test group with only yourself, get it running for a few days, then switch to the real group.

Watch the token expiration issue. If the scheduled task suddenly reports auth failure after running a while, it is most likely the user token expired and needs `lark-cli auth login` again.

## 25. How to auto-push CI/CD results into a Feishu group

A high-frequency need for R&D teams. After CI/CD finishes, automatically push results to a Feishu group, with different notification strategies for success and failure.

The approach is to add a webhook or script step in the CI/CD pipeline config, calling `lark-cli im +messages-send --chat-id "oc_xxx" --msg-type interactive --card '{...}'`. The card structure carries build status, commit info, changed files, and log links.

The practice of splitting success and failure groups: the pipeline judges build status, success goes to one chat-id, failure to another. Or send different-colored cards in the same group, green for success, red for failure, visually distinguishable at a glance.

The bot identity is appropriate for sending messages, because CI/CD is system behavior and need not bind to a specific user. But the bot must be in the target group, otherwise it will not go out.

Some teams go further: the failure message @s the owner with the `<at user_id="ou_xxx">` tag, forcing the owner to respond immediately.

## 26. How to have AI read an email and auto-fill a Base table

Email processing is a high-frequency pain point for white-collar workers. Receive a pile of emails every day, pick out the important info and fill it into a table, pure manual operation.

The CLI chain: `lark-cli mail +list` pulls the inbox, filters the emails to process (by sender, subject keyword, unread status), then `lark-cli mail +get --message-id xxx` reads the email body. After getting the body, the Agent extracts info per your defined field structure (like client name, order number, requirement description), and finally calls `lark-cli base +record-create` to write to the corresponding Base fields.

Extraction quality depends on the stability of the email format. Business emails with fixed formats (system notifications, form submissions, order confirmations) get high Agent extraction accuracy. Free-form personal emails drop in accuracy; recommend human review.

One practical trick: add an "original email link" field in Base, and the Agent writes the email link in when filling data. Later verification jumps back to the original with one click.

## 27. How to bulk-load CSV data into a Feishu Base

Two approaches.

Small data (dozens to hundreds of rows): write a loop, call `lark-cli base +record-create` row by row. Simple and direct, but slow; a few hundred rows may take minutes.

Large data (thousands of rows): use the Base batch-create interface. Call `lark-cli base records batch_create --params '{"table_id":"xxx"}' --data '{"records":[...]}'`, submitting a batch at once, much faster.

Either way, confirm the table structure first. Field types must match, select-field options must be built in advance, date-field formats must be unified. The safest approach is to first `lark-cli base +fields-list` to pull the field definitions, then prepare data per that definition.

Cross-table relations are another pitfall. If the imported data needs to relate to records in another table, first query the related table's record IDs, and write the relation field as record_id, not the display name.

## 28. How to query Base data with natural language

You do not need to memorize Base field names and filter syntax; just speak plain language to the Agent.

"Help me check which clients haven't paid back this month." The Agent first `lark-cli base +fields-list` to see the table structure, understands which fields "client," "payment," and "this month" map to, then constructs filter conditions and calls `lark-cli base +records-search` or `+records-list` to pull data, finally formatting and returning it to you.

The premise of this interaction is that the Agent can see the table structure. The first time querying a table, have it pull fields and the first few records for schema understanding; afterward queries are fast.

The presentation of query results needs design. Have the Agent return a table rather than long text, or directly generate a new Feishu doc listing the results, convenient for sharing and archiving.

## 29. How to auto-archive valuable group chat info into a knowledge base

The group chat is where valuable info is most easily produced and most easily lost. One important conclusion buried in hundreds of casual messages is unfindable three days later.

The archiving approach: use event subscription to listen to group messages, and for each message have the Agent judge "is this worth archiving." The criteria are yours: contains a keyword, @s a tag, gets multiple replies, contains a link or file. For those worth archiving, the Agent extracts key info and calls `lark-cli wiki +node-create` or `lark-cli docs +create` to write into the knowledge base.

The judgment step is the hard part. Too strict a rule misses things; too loose archives the chit-chat too. Recommend running with loose rules for a while, see the archived content quality, then gradually tighten.

Event subscription requires the bot to be in the group, and you must configure the `im.message.receive_v1` event subscription on the Open Platform. After configuration, every group message is pushed to your Agent for processing.

## 30. How to have AI monitor a document for changes and auto-notify

Monitoring document changes is a common need. For example, notify dev when the requirements doc changes, notify everyone when the schedule table changes.

The approach is to periodically pull the document content and diff it. The Agent periodically calls `lark-cli docs +fetch --doc-id xxx` to read the doc, compares it with the last read content, and if there is a change, `lark-cli im +messages-send` pushes a notification.

A finer approach: only notify the changed part, not "the document changed." After the Agent diffs, extract the added or modified paragraphs, and the notification body carries the change content directly, saving people from clicking in to look.

Do not monitor too frequently. Pulling once per minute wastes API; every 15 minutes or hourly is enough for most scenarios. Document changes usually do not need second-level response.

If it is Base change monitoring, using Base's built-in automation is more efficient than CLI monitoring, because it has native change-event triggering.

## 31. How to do two-way data sync between Feishu and external systems

Two-way sync is one of the most complex scenarios, with high error cost, so proceed with caution.

One-way sync is relatively simple: external system to Feishu, or Feishu to external system, both are periodic pull from one side and push to the other. The difficulty of two-way sync is conflict handling: when the same data is changed on both sides, which one wins.

If you must do two-way, recommend making Feishu the primary data source. The external system reads Feishu data for display or computation, and all writes uniformly go back to Feishu. This way there is only one write direction, avoiding conflicts.

Technically, Feishu side uses CLI read/write, external side uses its own APIs. The sync logic is coordinated by a middle script that periodically pulls both sides, compares differences, and pushes updates.

Monitoring is essential. It is common for sync to run and then data mismatch, either because the field mapping is wrong or because one side's data format changed. The sync script must have logs, recording how many records synced and how many failed each run, for troubleshooting.

## 32. How to build a cross-app message bridge with the Feishu CLI

Scenario: you want to receive messages from WeCom, DingTalk, or Slack inside Feishu, or the reverse.

The bridge logic: on one side listen to app A's message events and forward to app B for sending. Feishu side, use event subscription to listen to IM messages, and after receiving, call the other platform's API to send out. Reverse is the same.

The Feishu CLI's role here is the Feishu-side send/receive layer. Listen with `lark-cli event consume im.message.receive_v1`, send with `lark-cli im +messages-send`. Other platforms use their own SDKs.

In practice, most teams do not build their own bridge but use ready-made tools, like some Agent frameworks with built-in multi-platform message routing. The CLI suits highly customized scenarios, like when you want to do content filtering, translation, or format conversion during forwarding; pairing the Agent with the CLI is more flexible.

## 33. How to build a fully automated daily-report bot with Python plus the CLI

The daily-report bot is a classic combination of CLI plus script, suited for people with some technical foundation.

Overall architecture: a Python script responsible for pulling data, calling the Agent to generate content, and calling the CLI to send messages. Paired with a scheduled task that triggers the script at a fixed time daily.

In the data-pull step, the script uses subprocess to call `lark-cli calendar +agenda` and `lark-cli task +get-my-tasks`, parsing the JSON output. In the content-generation step, the script feeds the data to a large-model API (like OpenAI, Anthropic), having it generate markdown body per the daily-report template. In the send step, the script calls `lark-cli docs +create` to build the doc, then `lark-cli im +messages-send` to send to the group.

The benefit of this architecture is that every step is replaceable. The data source can add email, add Base; the generation model can be swapped; the send target can be changed. The downside is more things to maintain; any break in script, token, or scheduled task cuts the daily report.

Recommend a simple health check: after the script runs, send a "daily report sent" message to a monitoring group; if not received, something broke.

## 34. How to build a Feishu Q&A customer service bot that auto-replies in groups

Someone asks in the group, AI auto-answers. This is a scenario many teams want.

Core components: a Feishu self-built app (bot) responsible for sending and receiving messages in the group, a bridge layer forwarding Feishu messages to a local AI Agent for processing, and the Agent calling the CLI or knowledge base to generate a reply and send it back to the group.

Configuration steps: first create an app on the Open Platform, enable the `im:message` permission and the `im.message.receive_v1` event subscription. Then build the bridge layer; in the community someone uses lark-channel-bridge, or you can write your own. The bridge layer forwards group messages to your Agent (Claude Code, Codex, or any Agent that can call the CLI), and after processing the Agent sends the reply back to the group.

The knowledge base is key to answer quality. The Agent's knowledge sources are layered: system prompts set behavior rules, Skills provide Feishu API operation capability, long-term memory stores historical interactions, and the external knowledge base holds business docs. A customer-service bot without a knowledge base can only answer generic questions; connecting a knowledge base lets it answer specific business.

On security, recommend the bot only respond to @ messages, not all messages in the group, to avoid noise and permission abuse.

## 35. What to do when a Minute transcript export stalls halfway

This is a real high-frequency pitfall. Using the CLI to export a Minute transcript, it stops at some timestamp and the rest is not retrieved.

Three troubleshooting directions.

First, pagination. The Minute transcript interface by default returns only the first page; long meetings (over 30 minutes, say) may span multiple pages. Add the `--page-all` parameter to let it auto-paginate and pull all content.

Second, wrong interface. `lark-cli minutes minutes get` only returns meta info like title and duration, not the transcript. The transcript goes through `lark-cli vc +notes --minute-tokens xxx`, the correctly-routed skill-layer wrapper.

Third, points used up. The Minute transcription service has a point limit; once used up, subsequent content cannot be retrieved. In this case the CLI error may not be obvious; you must check the Minute backend for the point balance.

After confirming which cause, treat accordingly. Pagination adds a parameter, wrong interface switches the command, points used up need recharge.

## 36. How to upload a local video via the CLI and convert it to a Feishu Minute

Local video to Minute is a two-step operation, not one-shot.

Step one, upload to the cloud drive. Call `lark-cli drive +upload --file ./your-video.mp4`, get the returned file_token.

Step two, generate the Minute with the file_token. Call `lark-cli minutes +upload --file-token xxx`, Feishu starts the transcription flow, and after finishing returns the minute_token.

After getting the minute_token, you can use `lark-cli vc +notes --minute-tokens xxx` to pull the transcript, summary, and to-dos.

Confirm the limits first. Minute transcription supports videos up to 6 hours long and 6GB in size, covering common formats like mp4, mp3, wav, mov. Videos longer than that must be split first.

Transcription is not real-time; the longer the video, the longer the wait. Recommend a polling loop in the script, checking transcription status at intervals, and pulling data after completion.

## 37. How to have AI read Feishu meeting notes and extract to-dos

After the meeting, notes generated, the to-dos must auto-land in the task system to close the loop.

The Agent approach: call `lark-cli vc +notes --minute-tokens xxx` to get the notes' structured data, which contains summary, to-do list, chapters, and transcript. The to-do list is usually structured, each item with owner, content, and sometimes a due time.

After getting the to-do list, the Agent calls `lark-cli task +create --name "xxx" --assignee "ou_xxx" --due "2026-07-15"` for each. If the owner is not accurately recognized (the transcript only has a name, no user_id), you must first call `lark-cli contact +search-user` to resolve the name into an open_id.

One practical approach: all tasks generated from notes automatically carry the notes doc link and meeting name in the description. This lets you jump back to context with one click when working on the task later.

## 38. Does a PDF exported via the Feishu CLI add an AI-generated watermark?

This has been asked many times in groups. The answer: it depends on Feishu platform's watermark policy; the CLI itself cannot control it.

For AI-generated or AI-edited docs, Feishu may mark "content generated by AI" or a similar watermark when exporting PDF. This is a platform-level compliance requirement. The CLI calls Feishu's API, and however the API marks it, it marks; there is no switch for the CLI to bypass.

If you really need a watermark-free PDF, a few ideas: manually edit the doc after generation (even changing one character), so the platform judges it "human-modified"; or use the CLI to export markdown and convert to PDF with another tool, bypassing Feishu's export chain.

But the labeling of AI-generated content's source is an industry trend, and fighting it is not a long-term plan. Accept the mark, put your energy into making the AI-generated content high-quality enough that people do not mind seeing the mark.

## 39. How to let Claude Code operate your Feishu directly

This is the top concern of the layer-4 AI Agent developers. Claude Code natively supports calling terminal commands, so connecting the Feishu CLI is smooth.

Steps: first install the Feishu CLI on the machine, `npx @larksuite/cli@latest install`. Then configure app credentials, `lark-cli config init`. Then log in and authorize, `lark-cli auth login --recommend`. Finally install the Skills package, `npx skills add larksuite/cli -y -g`, so Claude Code understands the Feishu CLI command structure.

After installation, you say directly in Claude Code "help me check today's schedule," and it calls `lark-cli calendar +agenda --as user` itself, gets the result, and shows you.

The advantage of Claude Code calling the CLI is that it is multi-turn conversational and can dynamically decide the next step based on the return. If the first call fails, it reads the error and corrects the parameters to retry. This adaptive ability is something fixed scripts cannot do.

On security, recommend adding `--dry-run` to any side-effecting operation on the first run. Claude Code is powerful, but it also makes mistakes; preview then confirm is the safe approach.

## 40. How much time can Feishu CLI automation actually save?

Take the weekly-report scenario for a quantified comparison.

Manual flow: open Feishu, switch to the calendar to flip through this week's daily meetings, switch to the task list to see everyone's progress, switch to Base to pull project data, create a doc to paste and format the data, switch to the group chat to send the link. Full flow 60 to 90 minutes.

CLI automation: say one sentence to the Agent, it pulls calendar, tasks, and Base data itself, generates the doc, sends to the group. Your involvement is only the final dry-run preview confirmation. Full flow 5 to 10 minutes, of which your actual time spent is 2 to 3 minutes.

The efficiency gain is not simply "90 minutes becomes 5 minutes." More importantly, most of those 90 minutes is low-value repetitive operation (window switching, copy-paste, formatting); after automation your time goes to confirming content quality, which is high-value judgment. The saved time can be spent on things that truly need human thinking.

Different scenarios save different amounts. Batch operations, scheduled tasks, and data-aggregation scenarios save the most, usually 10x or more. Scenarios needing judgment and creativity save less, but still over half.

## 41. How to let AI perceive Base data changes in real time

Two approaches.

First, Base's built-in automation. Base has a native "automation" feature where you can configure "trigger when a record is modified," and the trigger action can be sending a message or calling a webhook. This is the lightest approach, no code needed.

Second, periodic polling. The Agent periodically calls `lark-cli base +records-list --filter "LastModifiedTime > xxx"` to pull recently changed records, diffs, and processes. Suited for complex trigger logic that the automation feature does not cover.

For high real-time requirement, use the first; native automation is almost real-time. For low real-time requirement (like syncing once an hour), use the second, which is more flexible because you can add any judgment in the polling logic.

One limitation: Base dashboards are currently not readable by the CLI. If you want "notify me when dashboard data changes," it cannot be done now; you can only monitor the underlying data table.

## 42. Which office scenarios are best to automate with the CLI first?

The criterion for picking scenarios has three rules: high repeatability, clear rules, time-consuming when done by hand each time. All three satisfied is a good scenario.

Best to start with: reporting (daily, weekly, monthly reports with fixed data and format), notification (CI/CD results, document changes, task due), aggregation (pulling multi-source data together into a doc or table), and batch (batch create, batch update, batch export).

Not recommended to touch first: those needing creative output (writing copy, designing), those needing interpersonal judgment (replying to customer complaints, coordinating conflicts), and those with unstable or free-form data sources (processing free-form emails, organizing group discussions). These scenarios the Agent can help partially, but the automation degree is low and the return on investment is not high.

Newcomers are advised to start with "repetitive things done every day." If you spend over 20 minutes a day on the same thing, it is probably worth automating. Get one working first, build confidence and methodology, then expand to complex scenarios.
