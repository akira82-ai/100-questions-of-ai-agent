# Chapter 3 · Three-Layer Architecture and Security

## 43. Why mixing user and bot identities is the biggest pitfall of the Feishu CLI

The Feishu CLI has two execution identities, user and bot. User is a specific person logged in via OAuth; bot is the Feishu app itself. The two identities have completely different permission scopes, accessible data, and operation ownership.

The biggest pitfall is that using the wrong identity gives completely unexpected results, and the error is often not intuitive.

Creating a doc with the bot identity, the doc owner is the bot not you, and you have to request permission yourself to edit it. Querying the calendar with the bot identity, you can only see schedules the app itself created, not your personal meetings. Sending a message in a group with the user identity, the message shows your name, but after you leave the company the ownership of that message gets messy.

The principle for choosing an identity: operations touching personal data (calendar, tasks, email, private docs) use user; operations that are system behavior (CI/CD notifications, batch creation, service accounts) use bot. Switch with `--as user` or `--as bot` in the command.

For first CLI configuration, recommend getting it working with the user identity first, because most high-frequency scenarios (checking schedule, reading docs, sending messages) are covered by the user identity. The bot identity suits background services and multi-person shared scenarios better.

## 44. Why dry-run is the "regret medicine" for AI operating Feishu

The biggest risk when an AI Agent calls the CLI to execute side-effecting operations is that it misunderstands you and really sends. For example you say "send the weekly report to the R&D group," it understands it as the product group, and the message is sent and cannot be recalled.

Dry-run is the mechanism against this layer of risk. Add `--dry-run` to side-effecting commands like sending messages, creating docs, modifying records. The CLI prints the full request to be executed, including target chat-id, message content, and API parameters, but does not really send. After you confirm it is correct, remove the parameter and rerun to truly execute.

Recommended rhythm: always dry-run the first time you run any side-effecting command. After changing the data source, changing the template, or changing the target group, dry-run again. Building this habit avoids the vast majority of "wrong group," "wrong person," "data written to wrong place" accidents.

The Agent itself can call dry-run. You tell the Agent in the prompt "dry-run before sending messages, let me confirm," and it automatically adds this parameter on the first execution.

## 45. How the preview-before-send mechanism for AI messages is built

The preview mechanism is dry-run at the bottom, but the application layer has several layers of wrapping.

The most basic layer: add the `--dry-run` parameter on the command line, output a JSON-format request preview containing endpoint, params, and body. This layer suits technical users reading directly.

The second layer: the Agent parses the dry-run JSON result into plain language. "I am about to send a text message to group oc_xxx with content 'this week's report is done,' confirm execution?" This layer suits non-technical users.

The third layer: interactive card preview. For complex content like sending card messages, the Agent can first generate the card JSON, preview the structure with dry-run, and really send after confirmation. The visual preview of the card is not supported by the command-line side of the Feishu client; to see the effect you can only really send to a test group.

The highest-level preview is "send to a test group, confirm, then forward." Swap the target group to a test group with only yourself, really send once to see the effect, and after satisfaction change the chat-id to the official group. This is the safest but also slowest, suited for important messages.

## 46. What configuration problems can `lark-cli doctor` diagnose?

`lark-cli doctor` is the CLI's built-in one-click diagnostic tool; running it scans out most common configuration problems.

Core items it checks: network connectivity, whether your machine can reach Feishu's key domains (accounts.feishu.cn, open.feishu.cn, these few). If these domains are blocked by a firewall or hijacked by a proxy, the CLI throws all kinds of mysterious errors, and doctor can locate it immediately.

Credential status, whether your user token and bot token have expired, whether the credentials in the keychain are stored correctly. macOS's sandbox mechanism occasionally causes keychain problems, and doctor can identify such anomalies.

Permission coverage, whether your currently authorized scope is enough to support the command you want to run. For example if you want to read doc comments but have not enabled `docs:document.comment`, doctor will prompt which scope is missing.

Version status, whether your installed CLI version is the latest, whether important security patches are missing.

For any CLI error, step one is to run doctor. Many seemingly complex problems are located by doctor at a glance.

## 47. What can the user identity do that the bot identity cannot?

The core advantage of the user identity is access to personal-dimension data.

Checking the personal calendar: only the user identity can see your own meetings and schedule. The bot identity querying the calendar can only see schedules the bot itself created, and knows nothing about your meetings.

Reading personal email: email is strongly personal-attribute data, completely inaccessible to the bot identity. `lark-cli mail +list` must use the user identity.

Checking the personal task list: `lark-cli task +get-my-tasks` returns the currently logged-in user's tasks; running this command with the bot identity is meaningless.

Accessing private docs: docs shared with you alone, your personal drafts, only your user identity can read. The bot must be separately authorized to read these docs.

Sending messages showing your name: messages sent with the user identity show your avatar and name in the group. This matters for some scenarios, like replying to a client in your personal capacity or doing a work report.

Simple principle: any operation starting with "my" (my calendar, my email, my tasks, my docs) uses the user identity.

## 48. What can the bot identity do that the user identity cannot?

The bot identity's advantage is in system-level operations and multi-person shared scenarios.

24/7 uninterrupted running. The user token has expiration issues; if not refreshed for a long time it becomes invalid, and scheduled tasks running at midnight easily hang due to token expiration. The bot uses tenant_access_token, whose refresh mechanism is more stable, suited for resident services.

Multiple people sharing one identity. A team shares one bot, and everyone operates Feishu through this bot, with unified permission management. If using the user identity, each person's operations must be authorized separately, with high management cost.

CI/CD and automation pipelines. Pushing Feishu notifications after CI/CD finishes is most reasonable with the bot identity, because this is system behavior not someone's personal behavior. Pushing notifications with the user identity shows the message as a specific person, semantically wrong.

Avoiding personal-data lock-in. Docs created by the bot, messages sent by the bot, are owned by the app not the individual. When an employee leaves, bot-created resources need no migration. Resources created by the user identity become a headache for permissions and ownership after the employee leaves.

Cross-user scenarios. If you build a customer-service bot serving multiple users, the bot identity is the unified entry; each user's request goes through the same bot, and the backend logic is simple.

## 49. How to choose among the CLI's three command tiers without getting it wrong

The three command tiers from coarse to fine: shortcut, API command, Raw API. The criterion for choosing a tier is "how far the CLI has wrapped what you want to do."

The shortcut tier, commands prefixed with a plus, like `lark-cli im +messages-send`. This tier does the most abstraction: smart defaults, table output, dry-run preview, and common parameter combinations are all built in. Ninety percent of daily operations are covered by this tier. The tell is "what I want is a high-frequency operation."

The API command tier, organized by business domain and resource, like `lark-cli calendar events list`. This tier maps one-to-one with the Feishu Open Platform APIs, with parameters fully exposed and no extra wrapping. Suited for operations the shortcut does not cover but are still standard APIs. The tell is "the shortcut has no such command but the API docs do."

The Raw API tier, calling any Feishu API directly with `lark-cli api GET/POST`. This tier has no wrapping at all; it just handles auth and error formatting for you. Suited for edge APIs the CLI does not cover at all, or scenarios needing extremely customized parameters. The tell is "this tier is the only choice."

Degradation order: first check if the shortcut has it, if not check the API command, if still not use the Raw API. Do not start at the bottom, because that equals rebuilding the wheel the CLI already built.

## 50. How to handle token expiration without logging in manually every time

User-identity token expiration is the highest-frequency operations pain point. The user_access_token is valid for about 2 hours, and the refresh_token for about 30 days, but under default security policy it may be only 7 days.

To make it persistent, the key is to enable the `offline_access` scope at login. After enabling, as long as the refresh_token is used once within its validity, it auto-renews, theoretically no need to re-scan to log in within a year. `lark-cli auth login --recommend` automatically brings this scope.

If you are already logged in but the token keeps expiring, two troubleshooting directions. First, see if multi-environment multi-profile caused the token not to persist. You logged in locally, but the script runs in a container using another config, and the two sides each refresh their own token, overwriting each other. Second, macOS's keychain occasionally fails to store credentials; running `lark-cli config keychain-downgrade` to switch to file storage can bypass it.

The bot identity has no such problem. The tenant_access_token is signed on the fly with app_id and app_secret, automatically refreshed internally by the CLI, imperceptible to you.

## 51. How much context quota does global Skills injection eat?

The Feishu CLI's Skills package has 26 skills; each skill is a markdown document telling the Agent which commands this business domain has, how to fill parameters, and what scenario uses what command.

Global injection means all skill documents are stuffed into the Agent's system prompt or context. The benefit is the Agent understands the full picture of Feishu and can call commands in any business domain. The downside is these documents add up to a sizable volume, occupying the model's context window.

Actual occupation depends on the skill package version and the Agent's context window size. Early skill documents were written in detail; full injection could occupy tens of thousands of tokens. The new version has been streamlined, but it is still a non-negligible context burden.

Several optimization strategies. First, only install the few skills you commonly use. Feishu supports selective installation; for example if you only do calendar and doc automation, install only lark-calendar and lark-doc, not lark-base and lark-sheets. Second, use the Agent framework's skill-loading mechanism to let the Agent read skills on demand rather than full injection. Third, do not write the documents too long; the more concise the skill document, the less context occupied.

Someone in the community has raised this pain point. If your Agent frequently hits the context limit, first see if it is the skill full-injection problem.

## 52. How to recover when the keychain master key is lost

On macOS the CLI stores credentials in the system keychain, which is encrypted by a master key. If the master key is lost, all credentials stored in the keychain cannot be decrypted, and the CLI keeps reporting auth failure.

The scenarios most likely to trigger this: macOS upgrade, reinstalling the system, switching the login account, or keychain database corruption. Any of these may make the master key unrecoverable.

Recovery steps: first try `lark-cli config keychain-downgrade`, which switches to file-storage mode, bypassing the keychain and storing credentials directly in the local config file. The premise is you can still run the CLI, even with sudo or a new account.

If keychain-downgrade also cannot run, you can only reset: delete the `~/.lark-cli/` config directory, re-run `lark-cli config init` and `lark-cli auth login`, configure from scratch. The cost is all historical credentials gone, but CLI credentials should be rebuildable at any time anyway.

Prevention: important environments should not rely only on the keychain. Production servers use Linux, credentials in files; macOS dev machines periodically confirm the keychain reads normally; multi-person shared environments uniformly use the bot identity plus file storage, not depending on someone's personal keychain.

## 53. What is the difference between the Feishu CLI's Skills and MCP tools?

The two are not on the same layer; one is a concrete tool, the other a standard protocol.

The Feishu CLI's Skills are a set of markdown documents telling the Agent what commands the Feishu CLI has, how to call them, and what scenario uses what. Its carrier is the CLI itself, and the Agent uses it by executing terminal commands. Skills solve the problem of "how does the Agent understand the CLI's command structure."

MCP (Model Context Protocol) is a standard protocol proposed by Anthropic, defining the unified interface spec for Agents calling external tools. Any tool that implements the MCP interface can be called by any MCP-supporting Agent. MCP solves the problem of "what protocol does the Agent and the tool communicate with."

The relationship between the two: the CLI can be wrapped as an MCP server, letting MCP-supporting Agents call it through the standard protocol. In fact the community is already doing this.

Which to pick depends on your Agent. Agents like Claude Code and Codex that can directly call terminals use the CLI most directly. If your Agent framework only supports MCP, then wrapping the CLI as an MCP server is a necessary step.

For production, recommend prioritizing the CLI itself, because it is officially maintained by Feishu, with guaranteed updates and coverage. The MCP wrapper is community-driven, and its coverage and timeliness depend on contributors.

## 54. How to check which permissions your CLI is currently authorized for

Permission transparency is the foundation of security. The Feishu CLI provides several ways to check authorization status.

`lark-cli auth status` shows the current login state and the list of authorized scopes. Running it shows what identity you logged in with, whether the token expired, and which permission domains are authorized.

`lark-cli auth scopes` lists all scopes the current app supports, including authorized and unauthorized. Comparing with the status output shows which scopes you could apply for but have not.

`lark-cli auth check --scope "calendar:calendar:read"` checks whether a specific scope is authorized. Returns exit code 0 if yes, 1 if no. Suited for pre-checks in scripts: before the command runs, confirm the permission is enough.

Regularly reviewing the authorized scope is a good habit. You may have temporarily opened a high-risk permission early to get a scenario running and forgot to close it. Run auth status every month or two, turn off unneeded scopes, shrink the attack surface. The principle of least privilege applies equally in the CLI scenario.

## 55. Why multiple Agents sharing one bot identity kick each other offline

This is a real stepped-on pitfall. Two Agents share one Feishu app's bot identity, and while running one suddenly errors with 401 and hangs.

The root cause is in the tenant_access_token management mechanism. Feishu's tenant_access_token has a validity period; when multiple independent clients each maintain their own token cache and each refreshes, one refresh may invalidate another's cache, manifesting as the first-logged-in being "kicked offline" by the later-logged-in.

Two Agents each maintaining their own token cache will kick each other. Agent A takes token T1 and caches it; Agent B triggers a refresh and takes token T2; T1 may soon become invalid, and Agent A's next request is 401.

Several solutions. First, the two Agents share one token cache, for example both reading the token from one file or Redis, and whoever refreshes updates the shared store. Second, stagger the refresh timing so refreshes do not happen simultaneously. Third, simply build a separate Feishu app for each Agent, each with an independent bot identity, avoiding conflict at the root.

If you are building a production-grade multi-Agent system, recommend one app per Agent. The convenience of sharing is superficial; stepping on the token mutual-kick pit is not worth it.

## 56. What each of the three layers (OpenAPI → CLI → Skills) solves

Feishu's capability is layered from bottom to top, each layer solving a different problem.

The bottom layer is OpenAPI, Feishu Open Platform's 2,500-plus APIs. This is the source of all capability, covering all business domains of messaging, docs, calendar, tasks, approvals, and more. It solves the most basic "what is Feishu's capability," but using it directly you must handle auth, errors, pagination, and parameter assembly yourself, with high development cost.

The middle layer is the CLI, wrapping OpenAPI into 200-plus command-line tools. It solves "how to make calling more effortless." OAuth built in, tokens auto-refresh, unified error format, automatic pagination, dry-run backing up safety, structured output for easy Agent parsing. Developers no longer repeat boilerplate.

The top layer is Skills, a set of markdown documents telling the Agent how to use the CLI. It solves "how to let the Agent know what commands exist and what scenario calls which." Each skill corresponds to a business domain, telling the Agent what shortcuts that domain has, how to fill parameters, and how to avoid common errors.

The effect of stacking three layers: the Agent goes from "facing 2,500 APIs at a loss" to "reading the skill doc and directly calling commands." Each layer up lowers the usage threshold by an order of magnitude.

## 57. How a Skill internally interacts with the Feishu API

A Skill itself is just a document; it executes no code directly. Its job is to tell the Agent "when you hit this kind of need, which CLI command should you call."

The full chain goes like this. The Agent receives your natural-language instruction, like "help me check today's schedule." The Agent reads the lark-calendar skill doc, understands that checking schedule uses the `lark-cli calendar +agenda` command. The Agent executes this command in the terminal.

After the CLI receives the command, internally it goes: first check auth status, confirm the current identity has calendar read permission; construct the OpenAPI request with the OAuth token and necessary parameters; send the request to the Feishu server; after getting the JSON response, format per the CLI's output contract, success results to stdout, errors to stderr, exit code distinguishes success/failure.

The Agent gets the CLI's stdout output, parses the JSON, understands today's meeting list, and returns it to you in natural language.

The whole chain: your words → Agent understands → skill doc points the way → CLI executes → OpenAPI call → Feishu server returns → CLI formats → Agent parses → natural language back to you. The Skill is navigation, the CLI is the execution body, OpenAPI is the underlying channel.
