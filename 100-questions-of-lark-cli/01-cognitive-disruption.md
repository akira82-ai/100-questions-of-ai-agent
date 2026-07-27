# Chapter 1 · Cognitive Disruption

## 1. Is the Feishu CLI made for humans or for AI?

Short answer: both can use it, but its true target user is the AI Agent, not the human.

You can certainly type `lark-cli calendar +agenda` in your terminal to see today's schedule. But that is no different from opening the Feishu app and clicking the calendar, only more troublesome. The CLI's value is not in replacing the human at the interface. Its value is in giving AI a ready-made set of commands to operate Feishu. You install the CLI, finish authorization, and hand the rest to Claude Code, Codex, or any Agent that can call a terminal. You say "organize this week's meetings into a table and send it to the R&D group," and the Agent pulls the calendar, aggregates the data, generates the document, and sends the message. You never touch Feishu once.

That is the real reason the CLI was designed. Every command has been tested against real Agent calls. Parameters are kept minimal, output is structured, defaults are smart, all so the model gets it right on the first try. If it were only for humans, none of this degree would be necessary.

So before deciding whether to use the Feishu CLI, ask yourself one question: do you have an AI Agent that can call a terminal? If yes, this is your new Feishu entry point. If no, you will probably drop it after a few days.

## 2. Why did DingTalk, Feishu, and WeCom all open-source their CLIs within three days?

In the last week of March 2026, DingTalk, Feishu, and WeCom open-sourced their respective CLI tools within three days. DingTalk on March 27, Feishu on the 28th, WeCom on the 29th. Three top collaboration-software companies made the same decision almost simultaneously: wrap their most core APIs into command-line tools and give them away free to everyone.

This cannot be a coincidence. Behind it is one shared judgment: AI Agents are entering the enterprise, and the first threshold for that is not how smart the model is, but whether the Agent can operate the office system. The traditional Open Platform API is for developers writing code. You register an app, request permissions, read docs, write SDK calls, handle auth and error retries. That flow is far too heavy for an Agent. What an Agent needs is one command it can execute directly, one structured return, one unified error format.

The CLI fills exactly that gap. It compresses hundreds of APIs into a few dozen commands with smart defaults, ready for the Agent to use with zero extra development. The three companies betting on the CLI at the same time shows the industry has reached consensus: the next entry point to office software is the human conversation, and the execution layer of that conversation is the Agent calling commands, not the human clicking the interface.

Moving within three days, the three companies are racing for the infrastructure position of the Agent era. Whoever lets Agents operate their system smoothly first keeps the users in the next-generation office paradigm.

## 3. Feishu built AI its own keyboard, are you still clicking the interface by hand?

Every Friday afternoon you open Feishu, switch to the calendar to see which meetings happened this week, open Base to pull everyone's task progress, create a doc to write the weekly report, copy data and paste it in, then switch to the group chat to send the link. Four windows back and forth, forty minutes gone just on organizing data.

You have done this flow for years and maybe think it is normal. It feels normal only because there was no other choice before. Now Feishu officially built AI its own keyboard, and that keyboard is the CLI. Install it, authorize once, then say one sentence to Claude Code or any Agent: help me summarize this week's meetings and tasks into a weekly report and send it to the R&D group. The Agent pulls the calendar, reads the tasks, generates the doc, and sends the message. The whole thing might take five minutes.

You went from operator to commander. The difference is that before you told Feishu every step of how to do it; now you only tell the AI what result you want.

This is not a few-times efficiency gain. It is a wholesale switch in how work gets done. The gap in efficiency, half a year later, between people still clicking the interface and people who let AI operate Feishu for them will be too large to close.

## 4. What does the shift from humans clicking the interface to AI calling the API mean?

For the past twenty years, every office tool's design assumption was: the person sitting in front of the screen is a human who completes tasks through clicking, dragging, and filling. The Word toolbar, the Excel cell, the Feishu document editor, all were designed for the human hand and eye.

That assumption is being broken. When AI Agents start executing office tasks for people, they need no toolbar, no cells, no visual interface at all. What they need is a set of interfaces callable through natural language or structured commands. That is exactly what the Feishu CLI does: it translates Feishu, which only humans could use, into a set of commands AI can operate directly.

The deeper impact is that the users of office software are no longer only humans, but also AI. And AI calling interfaces is far more efficient than humans clicking, because it can run concurrently, in batches, and around the clock. When your competitor lets AI manage calendars, write weekly reports, archive the knowledge base, and monitor document changes while you still operate by hand, your productivity gap will be measured in orders of magnitude.

Office software shifting from humans clicking the interface to AI calling the API is not a feature upgrade. It is a paradigm switch. Whoever's tools adapt to this switch first gets the ticket to the next round.

## 5. Why does the Feishu CLI say humans only need to install and authorize?

There is a core design in the Feishu CLI's security model: every operation executes bound to some authenticated identity, either a specific user's OAuth identity or the app's bot identity. No matter who asks the Agent for something, the identity used at execution time is the pre-authenticated one.

This means the human's job is very limited: install the CLI, complete OAuth authorization, tell the Agent what you want. Hand everything else to the Agent. You do not need to watch every step. The CLI's built-in dry-run shows you a preview before any side-effecting action executes, and it only truly sends after you confirm.

The logic behind this division is: humans are good at judgment and decision-making, not at repetitive execution. Let AI do the repetitive work, let humans only confirm at the key nodes, and overall efficiency and safety are both higher than a human doing it all by hand. The CLI wraps the repeatable parts into commands and leaves the parts needing human judgment to dry-run and authorization, cutting right at the reasonable boundary.

Of course this design has a premise: you must trust the Agent you use and the scope you authorized. The smaller the authorization scope, the more limited what AI can do, but also the safer. The Feishu CLI's default recommended scope is a curated common combination, and most people are fine starting from that baseline.

## 6. If Feishu bots already exist, why do we still need the CLI?

What a Feishu bot can do is actually quite limited: receive messages, reply to messages, passively respond to events. If you want it to proactively check next week's schedule, batch-download group files, or export Base data to Excel, it cannot, because the bot only has the IM message channel and lacks coverage of business domains like docs, calendar, tasks, and Base.

The CLI fills that gap. It covers 18 of Feishu's business domains and over 200 commands, from sending messages to creating docs, from checking schedules to managing tasks, from reading Base to writing email. Almost any Feishu operation you can think of has a corresponding command. The bot handles the conversation channel, the CLI handles execution capability. The two together form the complete Agent office solution.

More importantly, the bot is passive, the CLI is active. The bot waits for the user to send a message before responding; the CLI can be called by the Agent proactively at any time. Scheduled automation, background batch jobs, event-triggered real-time response, all rely on the CLI. With only a bot, you can make a customer-service bot. Add the CLI, and you can make an office Agent that truly works for you.

## 7. How to explain the Feishu CLI to a non-technical person in one sentence

"The Feishu CLI is the keyboard Feishu built for AI."

This sentence works because it does three things at once. First, it uses "keyboard," an object everyone knows, as an analogy, so the other person immediately knows this is an operating tool. Second, "built for AI" points out its difference from the traditional Feishu client: the target user is not the human. Third, it implies value: since AI now has its own keyboard, the one humans used can be set down.

Do not explain concepts like command line, API, or OAuth. The moment the other person starts asking "what is a command line," you have already lost. Build the cognitive anchor with one sentence. If they are interested, expand downward: you install it, authorize once, then say one sentence to the AI, and the AI can operate your entire Feishu for you.

This script lands almost every time when explaining the Feishu CLI to non-technical colleagues, superiors, or clients. The core is to let the other person first form the intuition "oh, this is a tool for AI," rather than falling into technical details.

## 8. What exactly is the relationship between the Feishu CLI and the Open Platform API?

The Feishu Open Platform has over 2,500 APIs covering almost every business from messaging, docs, calendar, tasks, and approvals. This is the underlying foundation of Feishu's capability, and all third-party integrations are built on these APIs.

The Feishu CLI is not starting from scratch. It is a command-line wrapper over the same set of APIs. The underlying calls are still these APIs, but the CLI does three things. First, it combines high-frequency APIs into shortcut commands with smart defaults, ready for the Agent to use. Second, it structures the API parameters and returns so the model understands and calls them more easily. Third, it builds in the infrastructure every API needs but you would rewrite each time: auth, error handling, pagination, and dry-run.

In other words, the API is the raw material, the CLI is the processed semi-finished product. You can certainly call the API directly, handling OAuth yourself, assembling parameters yourself, parsing returns yourself. But if your goal is to get the Agent running fast, the CLI saves you about 80% of the boilerplate.

For developers, the CLI and API are not either-or. They are used in layers: quick validation with the CLI, deep customization with the API. Both share the same underlying capability.

## 9. When should you use the Feishu CLI and when should you call the API directly?

The criterion is simple: does the CLI have a ready-made command for what you want to do?

If a shortcut or API command covers it directly, use the CLI. Its smart defaults, structured output, and error handling are already done, so the Agent's call success rate is higher. Especially for high-frequency operations like sending messages, checking schedules, and reading docs, the CLI commands are tested against real Agents, and the parameter design is optimized specifically for model friendliness.

If the CLI does not cover it, or you need extremely customized behavior, call the API directly. The CLI's Raw API layer supports calling all 2,500-plus Feishu APIs; you can send any request with `lark-cli api GET /open-apis/xxx`. At that point the CLI acts as an HTTP client that handles auth and error formatting for you, more convenient than bare API calls but keeping full flexibility.

In real projects the two are often mixed. High-frequency operations go through shortcuts, edge cases go through the Raw API. That is the most effort-saving combination. Do not use only one form for the sake of "purity." Use whichever fits.

## 10. Are the Feishu CLI and the MCP protocol competitors or complements?

MCP is a standard protocol proposed by Anthropic, aimed at letting AI Agents call various external tools in a unified way. The Feishu CLI is a concrete command-line tool that wraps Feishu's APIs.

They are not on the same layer, so there is no real competition. MCP is a protocol, the CLI is a tool. In fact, someone in the Feishu ecosystem has already wrapped the CLI as an MCP server, letting MCP-supporting Agents call Feishu capability through the standard protocol.

For the user, which to pick depends on what your Agent supports. If your Agent natively supports calling terminal commands (like Claude Code, Codex), using the CLI directly is simplest, no extra MCP server needed. If you use an MCP-native Agent framework, wrapping the CLI as an MCP server is a natural extension.

The real difference is the ecosystem. The CLI is officially maintained by Feishu, with guaranteed command coverage and update speed. The MCP server is community-driven, and its coverage depends on contributors. For production, prefer the CLI, which has official backing and continuous iteration.

## 11. If you already use n8n, is the Feishu CLI still necessary?

Depends on what you use n8n for.

If you only do simple data shuttling between Feishu and external systems, like a webhook in triggers a Feishu message, n8n is enough and there is no need to fuss with the CLI. n8n's visual orchestration is friendly to non-technical users and cheap to build.

But if you want an AI Agent to truly operate Feishu for you, dynamically, intelligently, deciding what to do based on context, n8n falls short. n8n's flow is pre-orchestrated; what each node does is decided by a human, and it does not change on its own while running. The core value of an AI Agent is that it dynamically decides which operations to call based on your natural-language instruction. That flexibility n8n cannot give.

The Feishu CLI fills the slot of "letting AI dynamically operate Feishu." You give the Agent one sentence, and it decides which CLI commands to call, in what order, how to combine them. That is something fixed-flow automation tools cannot do.

The two are not in conflict either. n8n handles stable, repetitive, clearly-ruled workflows. The CLI with the Agent handles flexible, one-off, judgment-requiring tasks. A mature automation system usually has both.

## 12. Who is each of the CLI's three command tiers suited for?

The Feishu CLI's commands come in three tiers, from coarse to fine, each with its own use.

The first tier is the shortcut, commands prefixed with a plus, like `lark-cli im +messages-send`. This tier does the most abstraction: smart defaults, table output, and dry-run preview are all built in, and it is the friendliest to both humans and AI. Ninety percent of daily operations are covered by this tier.

The second tier is the API command, organized by business domain and resource, like `lark-cli calendar events list`. This tier maps one-to-one with the Feishu Open Platform APIs, with parameters fully exposed, suited for scenarios needing precise control but not wanting to write HTTP requests.

The third tier is the Raw API, calling any Feishu API directly with `lark-cli api`. This tier has no wrapping at all; it just handles auth and error formatting for you, suited for edge APIs the CLI does not cover, or scenarios needing extremely customized parameters.

The criterion for picking a tier: use the shortcut if you can, do not go down. If the shortcut cannot handle it, fall back to the API command; if that still does not work, use the Raw API. Step down tier by tier from the top. Do not start at the bottom, because that equals rebuilding the wheel the CLI already built.

## 13. What is the real difference between the Feishu CLI and Feishu AILY?

AILY is Feishu's built-in AI assistant. Open the Feishu client and you can talk to it directly, out of the box, backed by Feishu's own models. You install nothing, configure no permissions, and use it inside Feishu.

The CLI is a completely different species. It has no model of its own; it just wraps Feishu's APIs into command-line tools. Its value only emerges when paired with an external Agent: you install the CLI in Claude Code, Codex, or any Agent that can call a terminal, and the Agent can use these commands to operate your Feishu.

The difference is in control and depth. AILY is built for you by Feishu: you use its model, its prompts, its capability boundaries, and the ceiling is set by Feishu. The CLI with an external Agent lets you decide which model, how to write the prompt, what to make it do. AILY's ceiling is what Feishu gives; the CLI's ceiling is your own engineering ability.

Daily lightweight needs are covered by AILY. For deep automation, connecting a custom knowledge base, or running a 24/7 office Agent, the CLI is the only choice.

## 14. Why is the Feishu CLI the lowest-cost entry point for Agents into the enterprise?

For an enterprise to make an AI Agent truly work, the hardest part is not the model, but letting the Agent operate the enterprise's internal systems. The traditional approach is to connect the Agent to the enterprise's own APIs, and each system integration goes through: read docs, write auth, handle errors, do retries, maintain token refresh. That takes anywhere from a few days to a few weeks per system.

The Feishu CLI has done all of that. The APIs of 18 business domains are wrapped into ready commands, OAuth is built in, tokens auto-refresh, error formats are unified, and dry-run backs up safety. One Agent that can call a terminal, after installing the CLI and authorizing once, can immediately operate Feishu's calendar, docs, messages, tasks, Base, and approvals, covering over 80% of the enterprise's high-frequency office scenarios.

Compare the cost. Connecting Feishu's API yourself, a skilled developer needs about a week to get the first complete flow running. With the CLI, from install to the first command running, the official time is 3 minutes. This order-of-magnitude gap makes the CLI the lowest-cost solution for Agents to access domestic office systems, bar none.

For an enterprise wanting AI office automation, starting with the Feishu CLI is the highest return-on-investment entry point.

## 15. What trend does 15k stars in three months signal?

Open-source for three months, 15.4k stars on GitHub, while DingTalk CLI sits at 1.8k and WeCom CLI at 2.5k over the same period. Feishu's lead is 8x DingTalk and 6x WeCom.

Star count does not fully represent technical strength, but it does signal one thing: the developer community's recognition of and willingness to participate in this. 15k stars means enough developers are really using it, filing issues, and contributing skills, forming a positive-cycle ecosystem flywheel. Once that flywheel spins, latecomers find it hard to catch up.

Behind that number is another signal: Agent-native office work is not a concept, it is a fact happening now. If only Feishu were hyping itself, stars would not climb this fast. Three companies open-sourcing in the same period with Feishu far ahead shows the market has real and urgent demand for "letting AI operate office systems." The curve of 15k stars in three months is the validation of this track.

For content creators and early evangelists, this number means a window of opportunity. There is no systematic Feishu CLI book or course on the market yet. Whoever produces deep content first occupies the head position of this niche track.

## 16. How is Agent-native office work different from old RPA automation?

RPA's logic is record the flow, set the rules, repeat execution. You record every step of a business process, telling the RPA tool "step one click here, step two fill this, step three submit," and then it runs that script repeatedly. When the flow changes, you re-record.

Agent-native office work is completely different logic. You do not tell the Agent how to do it; you tell it what you want. The Agent itself decides, based on current context, which tools to call, in what order, how to combine them. The same "help me organize the weekly report and send it to the group" may call completely different commands this week versus next, because the meetings, tasks, and groups involved are different.

The root of the difference is that RPA is rule-driven, the Agent is semantic-driven. A rule-driven system breaks when the flow changes, because every step is hardcoded. A semantic-driven system adapts to change, because it understands intent, not steps.

RPA suits repetitive flows where the rules never change, like exporting a certain table and archiving it at a fixed time every day. The Agent suits tasks needing judgment and flexible combination, like organizing meeting notes, coordinating cross-department schedules, or updating a project board based on email content. The two paradigms will coexist long-term, but the incremental, valuable work will increasingly be handed to the Agent.
