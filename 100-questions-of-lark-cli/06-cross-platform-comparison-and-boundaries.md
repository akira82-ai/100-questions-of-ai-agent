# Chapter 6 · Cross-Platform Comparison and Boundary Reflection

## 95. Feishu vs DingTalk vs WeCom CLIs, who actually performs best in practice?

In the last week of March 2026, DingTalk, Feishu, and WeCom open-sourced their CLI tools within three days. This is no coincidence; it is industry consensus: the CLI is the key entry point for Agents into the enterprise workflow. But the three started from different places, and what they built differs greatly.

A few hard numbers first. Feishu's lark-cli got 15.4k stars in three months open-source, DingTalk's dingtalk-cli 1.8k, WeCom's wecom-cli 2.5k. Feishu covers 18 business domains, DingTalk 11, WeCom 7. Feishu has 26 AI Agent Skills, DingTalk 19, WeCom about 12. Feishu is written in Go, DingTalk in Go plus Python, WeCom in Rust.

Star counts and business-domain coverage are only surface; the real gap is in the underlying design. Feishu CLI's three-tier command architecture (shortcuts → API commands → raw API) is built specifically for Agents; each tier considers parameter simplicity, smart defaults, and structured output when the Agent calls. DingTalk and WeCom's CLIs are more like "command-line-ifying the SDK," friendly to human ops but not deep enough in Agent optimization.

The Skill-system gap is more obvious. Feishu's 26 Skills are Agent-readable documents wrapped by business domain; after loading, the Agent directly understands Feishu's business concepts (what is chat_id, what is open_id, what message formats exist). DingTalk and WeCom have similar designs, but the coverage and documentation degree fall short.

Feishu also leads in internationalization and ecosystem openness. Lark (international) and Feishu (domestic) share the CLI codebase, so overseas developers can use it directly. DingTalk's overseas DingTalk has weak presence in the international market, and WeCom's WeCom basically only serves domestically.

The practical conclusion is direct: the Feishu CLI is currently in a league of its own in the Agent-native office track. Its underlying architecture is natively the operating-system base prepared for Agents. DingTalk is catching up but started late; WeCom currently looks more like making up lessons.

How long this gap lasts depends on each company's investment. Feishu's first-mover advantage in Skill ecosystem and community activity has obvious accumulation effects, and the probability of being caught up in the short term is small.

## 96. How long can Feishu CLI's lead hold?

After leading, the biggest fear is resting on laurels. Whether Feishu CLI's lead can sustain depends on several variables.

The first variable is iteration speed. lark-cli released 69 versions in three and a half months, averaging two to three updates per week. This pace far exceeds DingTalk and WeCom. High-frequency iteration means the team invests heavily, responds fast, and has sustained resource support. As long as this pace holds, the lead expands rather than shrinks.

The second variable is the community ecosystem. Behind 15.4k stars is a real developer community. The issue area has 159 open issues, very active. Community-contributed Skills, workarounds, and experience posts keep accumulating, forming a content moat. For DingTalk and WeCom to build this ecosystem from zero, the time and investment cost are not small.

The third variable is the depth of Agent-ecosystem integration. The Feishu CLI is already supported out of the box by mainstream Agent tools like Claude Code, Cursor, Cline, and WorkBuddy. This ecosystem integration is a snowball effect: the more people use it, the more Agent tools are willing to prioritize support, and the more support there is, the more people use it.

The fourth variable is the evolution of Feishu's product itself. The CLI is Feishu's interface layer; Feishu's product itself is iterating (continuous enhancement of Base, Minute, knowledge base). Product enhancement naturally drives CLI capability enhancement, which DingTalk and WeCom cannot easily replicate.

But risks exist too. If Feishu launches an official certification system or its own tutorial matrix, third-party content creators' authority will be diluted. If the CLI makes a major architecture change (like a Skills-system rebuild), early accumulated content will quickly become outdated. If DingTalk or WeCom finds a differentiated breakthrough point (like deeper vertical-industry integration), it may overtake in a niche.

From the trend judgment, Feishu CLI's lead will expand over the next 6 to 12 months. After that it depends on the three companies' strategic resolve on the Agent-native office track. For now Feishu invests most decisively and has the thickest ecosystem, and is hard to catch up with in the short term.

## 97. When should you bypass the Feishu CLI and call the API directly?

The CLI is not omnipotent; some scenarios are more appropriate bypassing it and calling the Feishu OpenAPI directly.

The first scenario is capabilities the CLI has not yet covered. The Feishu Open Platform has 2,500-plus APIs; the CLI's API-commands tier covers the high-frequency part, and the raw-API tier can theoretically call all, but parameter passing and error handling are less flexible than calling the API directly. A new API you need was just released and the CLI has not had time to wrap it; calling the API directly is the fastest way.

The second scenario is extreme performance optimization. The CLI itself has startup overhead, parameter parsing, JSON serialization costs. If your service needs to call Feishu APIs hundreds of times per second, forking a CLI process each time accumulates overhead. Using the Feishu SDK or an HTTP client to call the API directly saves the middle layer and performs better.

The third scenario is complex business logic. The CLI's commands are atomic; complex business combines multiple commands, with data transformation and state management in between. In this scenario using Python/Go to call the SDK directly to write business logic is clearer and more maintainable than shell scripts stitching CLI commands.

The fourth scenario is projects with existing SDK investment. Your team already built a system with the Feishu Python SDK or Go SDK; no need to rewrite just to use the CLI. The CLI and SDK are complementary, not a substitute.

The CLI's advantage is rapid prototyping, Agent-friendliness, and zero-code threshold. The SDK's advantage is performance, flexibility, and deep customization. Selection criterion: prototype phase and Agent integration use the CLI, production-grade deep integration uses the SDK, and mixing the two is also common.

Pragmatic judgment: first evaluate whether the CLI can do it; if it can, use the CLI (effortless); if it cannot or does not handle it smoothly, consider the SDK or direct API. Do not forcibly bypass the CLI for "looking professional"; that is complicating a simple problem.

## 98. Can the Feishu CLI access Lark (international) data?

Yes, but with prerequisites, and the domestic and international versions are two independent systems.

The Feishu CLI supports two brands by default: feishu (domestic) and lark (international). Choose the brand at config init, and the CLI connects to the corresponding API endpoint. Domestic connects to open.feishu.cn, international to open.larksuite.com.

The data isolation is strong isolation. Domestic Feishu data and international Lark data are completely non-interoperable: accounts not interoperable, apps not interoperable, tokens not interoperable. An app you created domestically cannot access international data, and vice versa.

Multinational companies often hit this pitfall. Headquarters domestic uses Feishu, overseas branches use Lark, and the two sides' data need to be connected; technically you must initialize two sets of CLI configs separately, authorize separately, then write glue code for data sync. The CLI itself provides no cross-version sync capability.

International version's functional coverage differs from domestic. Most core business domains (IM, docs, calendar, Base) are supported on both sides, but some new or domestic-specific features (like certain attendance, approval fields) may not exist in the international version, or the field names differ. Before using the CLI to operate the international version, first confirm the business domain you want is available in the Lark version.

Network access also needs attention. A domestic server accessing open.larksuite.com may be blocked by the firewall; an overseas server accessing open.feishu.cn may also have network problems. A hybrid architecture must plan which side runs which set of CLI.

The identity-auth system is also independent. Domestic uses Feishu-account OAuth, international uses Lark-account OAuth. Your Feishu account cannot log into Lark, and vice versa. Cross-border teams must prepare two separate account systems.

Data compliance is a deeper consideration. Some industries (finance, healthcare, government) have regulatory requirements on cross-border data flow; domestic data cannot leave the country, foreign data cannot enter. Before using the CLI for cross-border data sync, first confirm compliance; do not step on the regulatory red line.

## 99. Who is simply wasting time touching the Feishu CLI?

Tools are not omnipotent, and the Feishu CLI has people it does not suit. Forcing it on wastes time and energy.

The first type is people who do not use Feishu. Sounds like nonsense, but someone really saw "Feishu CLI is hot" and wanted to try, only to find their company uses DingTalk or WeCom. The CLI is part of the Feishu ecosystem; without a Feishu account, Feishu app, or Feishu data, the CLI is useless. Use DingTalk, go find dingtalk-cli; use WeCom, go look at wecom-cli.

The second type is people who do not code at all and do not intend to use an AI Agent. The CLI's value is letting the Agent or script call Feishu; if you insist on only clicking the interface, the CLI has no direct value for you. This type is better suited to Feishu's automation tools (like Base automation, approval flow engine), which are GUI-operable.

The third type is environments extremely sensitive to security and unacceptable to any automation risk. Some finance, military, healthcare scenarios forbid any external tool calling internal systems. The CLI needs OAuth authorization and calls external APIs, and simply cannot run in a strictly isolated intranet. This environment should honestly use the official secure-integration solution; do not think about the CLI.

The fourth type is people with extremely simple needs. You only occasionally send a message or create a doc; clicking twice by hand is done, and setting up a CLI environment, configuring OAuth, maintaining tokens, has a poor return on investment. The CLI's value is in batch, repetitive, automated scenarios; single-operation simple needs are faster with the interface.

The fifth type is people expecting "zero-code drag-and-drop." Although simpler than the SDK, the CLI is still at heart a command-line tool; you read parameters, look at JSON output, write shell scripts. People expecting integration like Zapier by dragging a few boxes will be frustrated with the CLI. This need is better served by visual automation platforms like n8n.

To judge whether you suit the CLI, ask three questions: do I use Feishu? Do I need batch or automated operations? Can I accept command-line or AI-Agent interaction? All three yes, the CLI is worth a try. Any no, consider another solution first.

## 100. What will Agent-native office work ultimately look like?

Finally a judgment-leaning topic. What will Agent-native office work look like in five or ten years.

First look at the current state. Tools like the Feishu CLI do "expose office-software capability as interfaces callable by Agents," letting AI read your calendar, send your messages, change your docs. This is the first step: open the interfaces.

The next evolution direction is "the Agent becomes the hub of office work." Now you tell the Agent what to do, and it calls the CLI to execute. In the future the Agent will be more proactive: it understands your work pattern, predicts what you need, prepares in advance. Monday morning you open the computer, and the Agent has already organized last week's progress, marked this week's priorities, arranged key meetings, waiting for you to review once and execute.

Further on is "the redesign of the interface itself." Now Feishu is GUI-first, and the CLI is a side door added for the Agent. But the end state of Agent-native office, the interface may reverse-design: the Agent is the main operator, and the GUI becomes "the display layer for humans to see" and "the confirmation layer for humans to approve." What you see is no longer the "how to operate" interface, but the status board of "what the Agent is doing" and the confirm button of "whether to let it continue."

The identity and permission model will also be reconstructed. Now user and bot are two identities; the future may evolve an "Agent representing user" proxy-identity system, where permissions are dynamically assigned by delegation relationship, rather than the either-user-or-bot binary. The security mechanism evolves from "pre-authorized scope" to "real-time risk assessment," where each Agent operation judges safety by context, and high-risk operations ask a human in real time.

Cross-app Agent collaboration is another direction. Now the Feishu CLI only manages Feishu; in the future the Agent may simultaneously operate Feishu, Salesforce, Notion, Jira, orchestrating workflows across apps. CLIs will standardize between each other (perhaps through protocols like MCP), letting the Agent operate different SaaS in a unified way.

The ultimate form may be "the invisibilization of office software." You no longer open the Feishu app; you open an Agent assistant, tell it or it judges itself what to do, and you do not care which tools it calls behind. Office software changes from "the interface you open every day" to "the service interface the Agent calls." This is the ultimate meaning of "office software shifting from humans operating the interface to AI operating the interface."

This end state will not arrive overnight; there are a large number of engineering problems, security-compliance problems, and user-acceptance problems to solve in between. But the direction is clear. Learning tools like the Feishu CLI today, what you really learn is the new paradigm of "Agent-native office," not memorizing specific commands. Commands will change, tools will evolve, but once the paradigm is established it will continue to deepen. Those who understand this paradigm early will have a first-mover advantage in the coming decade.
