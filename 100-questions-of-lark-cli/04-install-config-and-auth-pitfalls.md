# Chapter 4 · Install, Configure, and Auth Pitfalls

## 58. Is it actually safe to let AI operate your Feishu?

This is the question everyone asks the first time they touch the Feishu CLI, and the psychological threshold blocking many from taking the first step.

Short answer: security can be guaranteed, but on the premise that you understand the mechanism and operate by the rules.

The Feishu CLI's security model has three lines of defense. The first is OAuth authorization: the CLI can only do what you have explicitly authorized, and cannot touch any business domain you have not authorized. The second is dry-run preview: side-effecting operations can be seen before sent, and if something looks wrong, not executed. The third is Feishu's own permission system: docs, group chats, and calendars all have independent permission controls, and the CLI's operations are constrained by these permissions.

What truly needs vigilance is what permissions you granted; the CLI itself is fine. `lark-cli auth login --recommend` opens a large bunch of read-write permissions at once, convenient yes, but if you only intend to read docs and not write, opening a pile of write permissions digs your own pit. Someone in the community noted that `--recommend` by default enables read-write permissions for almost all features, with no small over-permission risk, and recommended at least providing a read-only global recommendation config.

A pragmatic security strategy has three steps. In the starting phase only use the user identity to operate your own data; open the bot identity later when doing multi-person sharing. Grant permissions on demand: read-only if you can, do not open read-write; use a single business-domain permission if you can, do not open the full set. In production use the least-privilege principle, periodically run `lark-cli auth status` to review the authorized scope, and turn off unneeded scopes.

Will AI send messages or delete docs recklessly? As long as you tell the Agent in the prompt "dry-run confirm before side-effecting operations" and build that habit, the vast majority of accidents can be avoided. The CLI's design philosophy is that humans are responsible for installing and authorizing; the controllability of the execution link is stronger than you think.

## 59. Why 403 is the most common error Feishu CLI users hit

Anyone who has used the Feishu CLI is familiar with the `Permission denied [230027]` error. It is not a CLI bug; it is Feishu Open Platform's permission interception.

The causes of 403 are just three types: the app did not open the corresponding permission, the permission was opened but not re-authorized to refresh, or the wrong identity was used.

The first type is most common. You created an app in the developer console, by default only basic permissions are opened; you want to send a message and hit 403, you want to read a doc and hit 403. The solution goes straight to the Feishu Open Platform: app → permission management, open the scopes you need, then re-run `lark-cli auth login` to refresh authorization.

The second type is easy to overlook. The permission was changed in the console, but the token cached locally by the CLI still carries the old permissions; you must re-log-in for it to take effect. Someone re-ran `lark-cli auth login` countless times and it still did not work, because they did not open the permission in the console first, only repeatedly logged in on the CLI side, reversing the direction.

The third type is using the wrong identity. Querying a personal calendar with the bot identity, or doing CI/CD notifications with the user identity, both cause permission problems. The first step on hitting 403 is to confirm whether you used `--as user` or `--as bot`, then look at the identity field in the error message.

The standard flow for troubleshooting 403: first run `lark-cli doctor` to see network and credential status, then run `lark-cli auth status` to see the authorized scope, compare with what scope your executed command needs, open what is missing, and re-log-in after the change.

## 60. Bot installed but no reply in the group, how to troubleshoot

This is one of the most crushing moments for newcomers: the CLI is installed, the app is created, the bot is configured, but @ing it in the group gets no response at all.

The troubleshooting path goes from near to far.

Step one, check whether the bot is in the group. Open group settings → group bots, confirm your bot is in the member list. If the bot is not in the group, messages cannot be received and events cannot be received, so naturally no reply.

Step two, check whether event subscription is enabled. Go to Open Platform → app → event subscription, confirm the `im.message.receive_v1` event is enabled. Without this event, the bot has no idea someone @ed it.

Step three, check the mention strategy. Some frameworks (like OpenClaw) have a mention-strategy option in the channel config; confirm it is not configured as "only respond to @ messages." If configured to respond to no messages at all, the bot goes completely silent.

Step four, check whether the gateway is running. If you use a runtime framework like OpenClaw or Hermes, confirm the Gateway process is alive and the listening port is normal. If the Gateway is down, events pushed over get no one to process them.

Step five, check the logs. Run `lark-cli doctor` to check Feishu key-domain connectivity, and see whether the Gateway logs received events and whether there were processing errors. Logs are the most honest; they tell you which layer the problem is stuck at.

Most "bot no reply" problems are located after walking these five steps.

## 61. Why skipping config init makes everything collapse later

`lark-cli config init` is the foundation of all subsequent commands; skipping it is like building a building without laying the foundation.

What config init does: create an app on the Feishu Open Platform (or bind an existing app), generate app_id and app_secret, and store these credentials in the local config file. All subsequent command auth depends on this set of credentials.

If you skip this step and run other commands directly, you hit all kinds of mysterious errors. "Auth failed," "cannot find app," "cannot connect to Feishu service" all have config init not done as the root cause.

One common crash scenario: you config init'd on computer A, copied the config file to computer B, but B's CLI version differs or the config path differs, causing the CLI to not read the correct config. The solution is to re-config init on computer B.

Another pitfall is that the account used for config init differs from the account used for subsequent auth login. Init created the app with account A, login scanned authorization with account B, and you get "current account has no Feishu CLI usage permission." The reason is your logged-in account has no management permission for this app. The solution is to ensure init and login use the same Feishu account.

## 62. Why your chat-id is always filled in wrong

The chat-id is the unique identifier of a Feishu group chat, shaped like `oc_7f363f14d647ead384b55749ea581fcf`. Fill it wrong and the message goes somewhere else or errors out directly.

The most common mistake is guessing the chat-id from the group chat name, or copying a string that looks like an ID from some screenshot. These are unreliable; the chat-id can only be obtained from a reliable source.

Three reliable sources. First, the `lark-cli im +chat-list` command lists all groups you joined and their chat-ids, the most direct method. Second, extract it from the Feishu group link. The token contained in the group link is the chat-id, formatted as a long string starting with `oc_`. Third, get it from the message event. If you configured event subscription, every message event carries the chat-id of the group it is in.

The consequences of filling the chat-id wrong range from minor to major. Lightly, an error and it will not send; heavily, the message goes to another similarly-named group. Someone once wanted to send the weekly report to the R&D group, mistyped one character in the chat-id, and the weekly report went to the client group. Dry-run can save your life in this scenario: preview the target group and content before sending.

## 63. How to correctly extract the chat-id from a Feishu URL

Extracting the chat-id from a Feishu group link has its particulars, because the link mixes in other parameters.

The Feishu group link format is usually `https://feishu.cn/chat/thread_id=oc_xxx` or a URL obtained through "copy group link" in group settings. The real chat-id is the `oc_`-starting string, fixed length.

Common wrong extraction: passing the entire URL as the chat-id, also copying the thread_id parameter name from the URL, or carrying extra spaces and newlines when copying. These all cause the CLI to report invalid param.

The correct extraction: locate the `oc_`-starting string in the URL, cut off at the next `&` or URL end, with no spaces in between. If unsure, use `lark-cli im +chat-list` to check and compare.

Some groups' URLs have the chat-id in the path part, some in the query parameter; the format is not fully unified. The safest approach is to query the group list with the CLI command, get the accurate chat-id, then use it.

## 64. config init refused by the system, how to troubleshoot

Someone on Windows ran `lark-cli config init` and got `dial tcp ... actively refused it`, but curl to the same domain could connect.

The root cause is proxy configuration differences. On Windows curl defaults to the system proxy settings, but the Feishu CLI is written in Go, and Go only reads the `HTTP_PROXY` and `HTTPS_PROXY` environment variables. The system proxy is on but the environment variables are not set, so the CLI connects directly to the Feishu domain and gets refused by the network environment.

Troubleshooting: in CMD run `netsh winhttp show proxy` to see the system proxy status. If a proxy is configured, set the environment variables:

```cmd
set HTTPS_PROXY=http://your-proxy-host:port
lark-cli config init
```

Linux and macOS are the same; check whether `echo $HTTPS_PROXY` has a value.

Another common cause is the corporate firewall blocking. Some enterprise security policies block the two key domains `accounts.feishu.cn` and `open.feishu.cn`. The solution is to have IT whitelist these two domains. Running `lark-cli doctor` quickly judges whether the key domains are reachable.

There is also a case of endpoint security software blocking. On Windows, endpoint security like Cylance may block PowerShell from running lark-cli; IT needs to whitelist lark-cli.

## 65. What if `--recommend` permissions are not enough

`lark-cli auth login --recommend` is designed to open enough common permissions at once, avoiding frequent supplementary authorization later. But there are two situations where it feels insufficient.

The first is when you need a specific business-domain permission that `--recommend` does not include. For example if you want to operate the Wiki knowledge base, by default only read-only is opened, and add/delete/modify are not allowed. At this point manually open scopes like `wiki:wiki` on the Open Platform, then re-auth login to refresh authorization.

The second is when you only want to open part of the permissions, but `--recommend` opens too many. Someone reported it enables read-write for almost all features by default, with high over-permission risk; enterprise admins may even forbid certain high-risk permissions (like deleting cloud docs). In this case use the `--scope` parameter to precisely specify the permissions you want:

```bash
lark-cli auth login --scope "docs:document.content:read docx:document calendar:calendar:read"
```

Someone in the community suggested the official should provide a `--recommend-readonly` option, opening only read-only by default, with write permissions added on demand. This suggestion was marked high-priority but as of the current version is not yet landed.

The best practice for permission management is precise authorization by business domain. Only do calendar automation, only open calendar permission; only do doc read-write, only open doc permission. Do not open the full set for convenience; when something goes wrong it is too late to shrink the attack surface.

## 66. How to initialize if your company is not on the feishu.cn domain

Feishu domestic and the international Lark are two independent systems, with completely different domains and API endpoints. Domestic uses `feishu.cn` and `open.feishu.cn`; international uses `larksuite.com` and `open.larksuite.com`.

If your company uses the international Lark, you need to tell the CLI to use the international domain at config init. The specific approach is to specify the brand as lark instead of feishu at initialization, and the CLI automatically switches to the international endpoint.

Someone connected the Feishu CLI with Claude Code, authorized but could not read Base; troubleshooting found the data was in the Lark environment (larkoffice.com) while the CLI defaulted to the Feishu API (open.feishu.cn), and the two domains could not reach each other so it could not read. The solution is to confirm the CLI-configured brand matches your Feishu version.

If your company uses a privatized Feishu deployment, the domain is the enterprise's own, and config init needs to specify the self-built domain. The specific parameter is in the CLI help `lark-cli config init --help`, generally through a custom endpoint parameter.

Mixed scenarios are also common: the company entity is on domestic Feishu, but some cross-border collaboration teams use international Lark. The two sides' tokens, apps, and data are completely non-interchangeable. Cross-version operation requires initializing two sets of CLI configs separately.

## 67. What strange errors a wrong Node.js version causes

The Feishu CLI has requirements on the Node.js version; a wrong version causes all kinds of bizarre errors, and the error message often does not directly point to the version problem.

Below the required version you get: syntax errors at install, `SyntaxError: Unexpected token` at runtime, some commands silently exit with no output, and abnormally slow performance. These are all because new JavaScript syntax (like optional chaining `?.`, nullish coalescing `??`) is not supported on older Node.js.

Recommend using nvm to manage the Node.js version, convenient to switch. Before installing the CLI confirm the version:

```bash
node --version
```

If the version is too low, upgrade with nvm:

```bash
nvm install 22
nvm use 22
```

After installing nvm but running `nvm` prompts command not found is another high-frequency pitfall. The reason is nvm is not loaded into the current shell. Solution:

```bash
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
```

Write these two lines into `~/.zshrc` (macOS) or `~/.bashrc` (Linux) to make them permanent.

The CLI install error on an intranet is usually an npm registry problem. Switch to a domestic mirror:

```bash
npm config set registry https://registry.npmmirror.com
```

## 68. Why PowerShell JSON parameters error out on Windows

This is the most common platform-compatibility problem Windows users hit.

Passing a JSON string to `--params` or `--data` in PowerShell, the CLI reports `invalid JSON format`, but the same command works perfectly fine on macOS or Linux.

The root cause is PowerShell's quote-handling mechanism. PowerShell interprets single and double quotes differently from Bash; the double quotes inside JSON get variously escaped and reassembled by PowerShell, and by the time it reaches the CLI it is unrecognizable.

This problem has wide reach. Not just `--params`, but also `--data`, `--markdown`, and `reply_elements` with complex JSON bodies are hit. Someone tested that multi-line `--markdown` parameters on Windows only write the first line.

Several workarounds. First, store the JSON in a file and pass it with `--params @file.json`. Second, assign to a variable in PowerShell then pass, `$json = '{"key":"value"}'` then `--params $json`, but someone reported this still fails. Third, do not run in PowerShell; switch to CMD or WSL. Fourth, write a Node.js script that calls the CLI through a child process, bypassing the shell's quote handling.

The essence of this problem is the compatibility gap between the Windows shell ecosystem and Unix-style CLI tools; not only the Feishu CLI hits it, all command-line tools running on Windows have similar problems to a greater or lesser extent.

## 69. Authorization link expired or rejected, what to do

The authorization flow reaches half and the link expires; there are usually several reasons.

The most common is the time window expiring. The OAuth authorization link has a validity period; beyond a certain time (usually a few minutes to tens of minutes) it expires. You run `lark-cli auth login` in the terminal, the CLI prints an authorization URL, you copy it to the browser, get a coffee in between, come back and click authorize, and the link has expired. The solution is to re-run auth login for a new link.

The second is the app secret was modified. You reset the app secret on the Open Platform, and all previously issued authorization requests become invalid, including the in-progress authorization flow. Error `device authorization failed: The client secret is invalid`. The solution is to re-auth login, go through it once with the new secret.

The third is the account has no permission. The authorization page shows "current account has no Feishu CLI usage permission"; the reason is your Feishu account has no management permission for this app. The app was created by someone else; you are neither admin nor collaborator. The solution is to have the app creator add you as a collaborator, or config init a new app yourself.

The fourth is the authorization page opens but clicking "authorize" errors. Possibly the app version in the developer console is not published, or the permission config is incomplete. Go to the Open Platform to confirm the app status is "published" and the permission config is correct.

## 70. Bot not in the group, message send errors, how to fix

Sending a message to a group with the bot identity, getting `Permission denied` or `Bot not in chat`, the root cause is simply that the bot is not in the target group.

Feishu's security policy is that the bot can only send messages to groups it has joined. You take a chat-id and send to a group that does not have the bot added, and it is directly intercepted.

The solution is to add the bot to the group. Open group settings → group bots → add bot, select your app's bot and add it in. After adding, sending messages works.

If it still errors after adding the bot, check a few points. First, confirm the chat-id corresponds to the group you just added the bot to; do not mix them up. Second, confirm the app has the `im:message:send_as_bot` permission; without it the bot cannot send messages. Third, if it is an enterprise group or a group with special security policy, adding the bot may require group-admin approval.

The bot-add-group action itself can also be done with the CLI; `lark-cli im +chat-list` related commands can manage group members. But for the first operation recommend manual add, confirm the flow works, then consider automation.

## 71. How to clean up stale cache when switching accounts

Switching Feishu accounts to log in is the scenario most likely to step on the cache pit. You think you switched accounts, but the CLI is actually still using the old account's credentials.

Sources of stale cache: the config file under `~/.lark-cli/` stores app credentials and tokens, the keychain (macOS) or credential manager (Windows) stores encrypted credentials, and environment variables may have set old tokens.

Steps for a thorough cleanup:

```bash
# clear config directory
rm -rf ~/.lark-cli/

# macOS clear keychain (delete lark-cli entries in the "Keychain Access" app)
# or via command line
security delete-generic-password -s "lark-cli" 2>/dev/null

# clear environment variables (if credentials were set via env vars before, clear them all)
unset LARK_CLI_NO_PROXY
unset HTTPS_PROXY
unset HTTP_PROXY

# re-initialize
lark-cli config init
lark-cli auth login
```

If you use multiple profiles (multiple workspaces), each profile has an independent config directory; when clearing confirm you are clearing the right one.

Multiple people sharing one machine makes stale problems more likely. A used it without cleaning, B took over and still uses A's credentials, and the docs and messages operated out are all attributed to A. For production recommend each person an independent account, or uniformly use the bot identity with file-storage credentials, not depending on a personal keychain.

## 72. CLI-created document asks you to request permission, why?

You created a doc with the CLI, open it and find you must "request edit permission"; this absurdity is a typical side effect of the bot identity.

The reason, covered in Chapter 3: a doc created by the bot identity has the bot app as owner, not you personally. The app is the app, you are you; to the Feishu permission system these are two independent subjects.

Three solutions.

The most direct: create the doc with the user identity. Add `--as user` in the command, and the created doc's owner is directly you personally, no permission-request problem. Suited for personal-use scenarios.

The second: actively authorize after creation. After the bot creates the doc, immediately call the permission interface to add permission to yourself. The CLI has related commands to manage doc permission members. Suited for scenarios where the bot must create but you need management rights.

The third: upgrade to the latest CLI. The new version, when detecting both user and bot identities present, automatically handles permission granting; after the bot creates a doc it auto-adds permission to the current user. If you are still stuck on this problem, try upgrading first.

Multi-person collaboration is more complex. A doc created by the bot by default only the bot has permission; others who want to edit must be separately authorized. The solution is to put the doc under a shared folder or knowledge-base node, inheriting that location's permission policy. Or after creation batch-call the permission interface to add team members.

On permissions, the core principle is to first think clearly "who needs what permission," then decide whether to create with the bot and authorize afterward, or create with the user and share afterward.

## 73. Base attachment download returns 403, what went wrong

The Base attachment field stores files; you want to bulk-download with the CLI, but get HTTP 403.

The key condition triggering this problem is that Base has advanced permissions enabled. Under advanced permissions, even if you have the table's edit permission, the file download of the attachment field may still be blocked.

There are multiple paths for attachment download, with different permission requirements. `lark-cli base +record-download-attachment` is the command designed specifically for Base attachments, theoretically the most on-target. But in advanced-permission mode it may still 403, because the underlying API needs an `extra` parameter declaring the bitable permission context, and the CLI in some versions does not pass this parameter correctly.

Someone tried `lark-cli drive +download` and `lark-cli docs +media-download`; these two paths return 400 instead of 403 for the same file_token, because the underlying endpoints they call simply do not support the `extra` parameter needed by Base attachments.

The current pragmatic approach has several steps. Step one, confirm your scope includes `base:record:read` and `drive:file:download`, add if missing. Step two, upgrade to the latest CLI; the official is continuously fixing such issues, and the new version prints a log_id for easy locating. Step three, if the CLI still cannot handle it, bypass it and directly call Feishu's native OpenAPI Base attachment download endpoint, manually carrying the `extra` parameter. Step four, file an issue with the log_id for official troubleshooting.

## 74. AI created select options on its own in a Base field, how to stop it

Letting AI write data into Base via the CLI, a select-type field (single/multi-select) got a bunch of options created on its own by the AI, polluting the original option system.

This is a side effect of AI's flexible understanding. When writing to a Feishu Base select field, if a non-existent option value is passed, the API by default creates that option. The AI sees the field is select, is unsure what options exist, and simply writes one casually, resulting in more and more options.

The root cure is to explicitly constrain the AI in the prompt. Tell it the select field can only use existing options; when unsure what options exist, query first (`lark-cli base +fields-list` lists field definitions and optional values), do not create new ones on its own.

The engineering-level fallback is to validate before writing data. Your script first queries the field definition, gets the valid option list, and filters out illegal values when writing. The CLI's dry-run lets you see the request parameters and intercept wrong option names first.

A select field's options are at heart a controlled vocabulary and should not be arbitrarily extended by the writer. If you are building a multi-person collaborative Base, recommend defining the option system at the table-structure design stage, and doing validation on the write side; do not rely on the AI's "intelligence" to guess.

## 75. What Wiki knowledge base gaps to work around right now

Wiki is one of the least completely covered business domains by the Feishu CLI; some capability gaps need to be known in advance, so your plan design does not hit a dead end halfway.

Early CLI versions only opened read-only permission for Wiki; add/delete/modify were impossible. After manually opening `wiki:wiki` on the developer platform, basic add/delete/modify become usable. This is a permission-level pitfall, not a capability gap.

Capability-level gaps include: creating new nodes was once missing, later added; deleting nodes is still unstable in some versions; directly uploading files to Wiki is not supported, upload can only go to Drive then manually move to the knowledge base; Wiki and Drive auto-integration is weak, uploaded files do not auto-classify into the Wiki directory; batch operation capability is insufficient, batch move and create node commands are not fully covered.

There is also a hidden gap: Wiki node metadata is incomplete. `lark-cli wiki +node-list` returns node data without `created_time` and `modified_time` fields, so you cannot sort or filter by time or recently-modified docs.

Wiki's native `sub-page-list` block also has read/write inconsistency. `docs +fetch` can read it, but `docs +update` writing discards it as an unsupported tag. If you want to maintain the Wiki knowledge base's hub page with the CLI, after writing you find the hub page became empty.

The way to work around these gaps is divide and conquer. Use the CLI for the parts it covers, fill the missing parts with native OpenAPI, and accept manual operation for the parts that truly cannot. Do not expect the CLI to cover Wiki all at once; it is still evolving.

## 76. Created document cannot be moved into the knowledge base, why?

You created a doc with the CLI, want to move it into a directory of the knowledge base, and find it cannot be moved in or errors out.

The most common reason is identity mismatch. The doc was created with the user identity, but moving into the knowledge base requires the app to have write permission to the knowledge base. Or the doc was created by the bot, and the bot has no management permission to the knowledge base node.

The second reason is the knowledge base's permission policy. The knowledge base can configure "who can add content to it"; if the policy restricts only admins can add, ordinary users or bots cannot move in. The solution is to have the knowledge base admin adjust the policy, or operate with admin identity.

The third reason is doc ownership. When the doc is in "my space," moving is relatively free, but when the doc is already under some shared folder, moving is constrained by the source folder's permission policy.

In practice, the CLI command to move a doc into the knowledge base is `lark-cli wiki +node-create`, passing obj_token (doc token) and obj_type (doc type), specifying parent_node_token for which directory to hang under. When it cannot be moved in, first confirm these parameters are correct, then confirm whether the operating identity has write permission to the knowledge base.

Workaround: first create a knowledge base node (empty doc), then use docs +update to write content into it. This way the doc is in the knowledge base from the start, avoiding the later-move permission problem.

## 77. Markdown import into Feishu docs adds a bunch of blank lines

Using the CLI to write Markdown into a Feishu doc, open it and find extra blank lines between paragraphs, and the originally compact layout becomes sparse.

The root cause is in the Markdown-to-Feishu-doc block-structure conversion logic. Feishu doc's bottom layer is a block array, where each paragraph, heading, and list item is an independent block. Blank lines in Markdown may be treated as block separators during conversion, causing extra empty blocks to be inserted.

Several mitigations. First, clean the Markdown source before writing, removing redundant consecutive blank lines, keeping only the necessary single-line spacing. Second, use `docs +update`'s incremental mode, writing block by block rather than full overwrite, reducing side effects from structure reassembly. Third, after writing use `docs +fetch` to pull back and check the actual block structure; if extra empty blocks are found, delete them with the update command.

A deeper problem is that Markdown and Feishu docs are not structurally equivalent. Markdown is linear text; Feishu docs are nested blocks; the conversion between them is inherently lossy. Complex structures like list-nested-quote-blocks, quote-blocks-nested-in-lists, and multi-level nested lists are especially error-prone during conversion.

Practical advice: simple docs written with Markdown are fine; docs with complex structures (deeply nested lists, mixed quotes) are best operated directly with the block API, not going through the Markdown conversion layer.

## 78. Ordered list numbers become plain text in CLI-written docs

You wrote a doc in Markdown with standard ordered-list format (`1. 2. 3.`), and after writing to Feishu with the CLI, open it and the numbers became plain text "1.," not Feishu's native ordered-list block.

This is also loss from the Markdown conversion layer. Feishu's ordered list is a dedicated block type with native capabilities like auto-numbering and indent control. During conversion, if the Markdown ordered-list syntax is not correctly recognized by the parser, it is treated as ordinary paragraph text, and the leading "1." becomes part of the content.

Common triggers for this problem: blank lines between list items, list nesting other blocks, or Markdown using non-standard indentation. These may all make the parser misjudge.

Avoidance: when writing Markdown, do not leave blank lines between list items, keep it compact; use standard 4-space or 2-space indentation for nested lists, do not mix; uniformly use `1.` for ordered lists (Feishu auto-computes the number), do not write `1. 2. 3.` and expect it to keep.

After writing, check: `docs +fetch` pulls back the doc's block structure, see whether the list block's type is `ordered_list` or similar. If it became `text` type, the conversion had a problem; manually adjust the source Markdown or use the block API to write the list block directly.

## 79. Why callout highlight blocks and mermaid diagrams won't read out

Markdown has callout highlight blocks and mermaid flowcharts; after writing to Feishu with the CLI, these special syntaxes are all lost or become garbled.

The reason is direct: Feishu doc's block system and Markdown extended syntax do not fully correspond. Callout is an extension of certain Markdown dialects (like Obsidian); mermaid is a special language marker for code blocks; Feishu doc's native block types have no direct corresponding implementation.

Callout in Feishu has a similar highlight-block, but the CLI's Markdown parser may not recognize this syntax and discards it on write. Mermaid is more thorough: Feishu docs have no native mermaid rendering capability, and the written code block only displays as plain-text code.

Two solutions. First, do not use Markdown for these special contents; use the block API to operate directly. Feishu's highlight block (callout block) has a dedicated block type, creatable via API to render correctly. If you want to display a mermaid diagram, you can only screenshot it as an image block, or guide the user to manually draw it in Feishu's canvas. Second, accept the loss of these syntaxes, change callout to a plain quote block `>` in the Markdown source, and replace the mermaid diagram with a text description or screenshot link.

This reflects a general rule: Markdown and Feishu docs are not one-to-one; some Markdown extended syntaxes have no landing point in the Feishu system. When doing doc automation with the CLI, first clarify the target doc's structure; use native blocks where possible with the block API, and only pure text content is suited to the Markdown layer.

## 80. Things I wish I had known earlier after a month of Feishu CLI

First, understand the user vs bot identity pitfall on day one. Many people step on this; created docs you have no permission for, messages with messy ownership, tokens kicking each other, all rooted in not distinguishing identities. Spend ten minutes on day one understanding the difference between these two identities, and you save days of troubleshooting later.

Second, dry-run is muscle memory, not an optional operation. Any side-effecting command, dry-run the first run. Changed parameters, changed target, changed data source, dry-run again. This is not conservative, it is professional. Accidents like wrong group, wrong table, wrong doc deletion, dry-run intercepts the vast majority.

Third, grant permissions on demand, do not open the full set for convenience. `--recommend` is convenient but high-risk; enterprise admins may directly forbid some high-risk permissions. Authorize precisely by business domain, review the scope periodically, turn off what is unneeded.

Fourth, Windows users prepare to go around. The PowerShell JSON-parameter problem is system-level, not a CLI bug. Either get used to file-parameter passing, or use WSL; do not wrestle with the shell.

Fifth, do not treat the keychain as the only storage. macOS upgrade, account switch, system reinstall may all break the keychain. Important environments use file storage or keep an extra credential backup; do not wait until the keychain breaks to find there is no plan B.

Sixth, know the Wiki and doc-format-conversion pitfalls in advance. Wiki coverage is incomplete, Markdown-to-Feishu-block conversion is lossy, and complex structures should not go through Markdown. Write these limitations into the plan-design phase, so you do not find it impossible halfway through development.

Seventh, upgrade the CLI version diligently. The Feishu CLI iterates fast; in the 9 days before July it released 6 versions. Many pitfalls you step on may already be fixed in the new version; upgrading is the cheapest troubleshooting method. Running `lark-cli update` is easier than running `lark-cli doctor`.

Eighth, community and issues are a treasure. The pit you step on is most likely stepped on by others; searching GitHub issues often finds an answer or workaround. If not found, file an issue; the official response speed is decent.

Using the CLI has a learning curve early on; after stepping on pitfalls for a week or two you enter the smooth phase. The key is not to give up during the pitfall phase; once you have walked through the high-frequency pitfalls, the efficiency dividend follows.
