# Chapter 4 · Advanced: Skills, MCP, Plugins, Automation, Computer Use

## 52. What is the difference between Skill, MCP, and plugin

These three words are a hurdle every beginner must pass, and mixing them up makes it impossible to tell who is who. Let me put it in plain words.

A plugin is a capability install package. You install a plugin and Codex gains a new ability. Install the Presentations plugin and Codex makes PPTs. Install the Spreadsheets plugin and Codex handles tables. Install the Chrome plugin and Codex operates your logged-in browser. Plugins solve the "can it do this kind of thing" question.

A Skill is a workflow instruction manual. A Skill's job is not to add new ability to Codex. A Skill freezes "how to do something" into a method. Say you have a standard process for organizing data. Write it as a Skill, and next time one sentence makes Codex follow your process, no need to explain again each time. Skills solve the "how to do similar tasks" question.

MCP is a channel connecting external tools. MCP lets Codex read outside data and tools, your GitHub, your Feishu, your Notion, your database. MCP solves the "connect what external resource" question.

One-line memory: use Skill for "how to do," use MCP for "what to connect," use plugin for "packaged ability."

The ordinary person's onboarding order should be: first master the built-in abilities and plugins (this step alone is enough for most things), then touch Skills once you have a repetitive workflow to freeze, then study MCP once you need Codex to read external data. The standard is simple: ordinary coding does not necessarily need MCP. Consider MCP only when you need Codex to access external tools or external data.

## 53. How to find and install a good plugin

More plugins is not better. Install on demand.

Codex has a plugin page. Open it and you see all available plugins, clearly categorized. Installation is simple: find what you want, click Add to Codex or Install, follow the prompts to finish authorization. Common plugins fall into a few categories: browser (Chrome, built-in browser), office (Documents, Presentations, Spreadsheets), development (GitHub, Computer Use), content creation (HyperFrames, Remotion).

The mistake beginners most easily make is "install on sight." Start with only the plugins OpenAI already built in, do not rush to install a bunch, add slowly once skilled. Installing too many plugins you will not use only clutters the interface, increases context consumption (each plugin takes a bit), and may introduce compatibility problems.

The right approach is install on demand. You clearly know "I want Codex to make PPTs," then install Presentations. You clearly know "I want Codex to read my GitHub," then install GitHub. When there is no clear need, do not install "in case I need it later."

Another standard: think clearly what you want to do first, then find the corresponding plugin. Not the reverse, staring at a pile of plugins not knowing which to install. Once you clearly know "I want Codex to connect some tool," go to the plugin page to find it. This "demand-driven" installation makes every plugin you install actually useful.

After installing a plugin, the call method is the `@` command in the dialog. For example `@Chrome` calls the Chrome plugin, `@Computer` calls computer control. Type one `@` and you see all installed plugins, pick the one you want.

## 54. How do I create a Skill myself

Creating a Skill needs no technical knowledge. Speaking natural language is enough.

The simplest creation method: first let Codex run the process you want to freeze end to end, the result satisfies you, then tell Codex "turn this process into a Skill." Codex automatically organizes your just-run process into a SKILL.md file and saves it, next time you can call it quickly.

A more direct method is skill-creator. Type `$skill-creator` in the dialog, then like talking to a colleague, describe your process in natural language: what to do in step one, what in step two, what to output at the end. Codex helps organize this description into a structured Skill file. This method needs no technical details, just speak your process out, no need to be airtight, Codex understands, and for what it does not understand you interact a few more rounds.

Many feel the word Skill sounds advanced and complex, and dare not touch it. Actually a Skill is just a markdown file, clearly writing "what scenario to use, what the goal is, what steps to follow, what output format." The value of a Skill is turning experience that only lives "in your head" into a standard process "Codex can repeat."

The order of doing things matters. Do A then B, or B then A, the result differs a lot. When cooking, wiping the stove right after stir-frying while the oil has not set is far easier than cleaning up after the meal. During cooking, washing the utensils you will not use later in the gaps lightens the after-meal cleanup. A Skill freezes your "process" of doing things, letting Codex follow your efficient process rather than play freely.

When to make a Skill. The standard is clear: use a prompt for a task done only once, use a Skill for a task done repeatedly. If you do a monthly report every month and re-explain the process each time, make the process a Skill. If it is just a one-off temporary thing, just say it, no need for a dedicated Skill.

## 55. How to write a Skill so it auto-triggers

Many make a Skill and find it never auto-called, having to manually `$skill-name` each time, feeling the Skill is useless. The problem is in the Skill's description.

Whether a Skill auto-triggers hinges on the Skill's description field. Codex decides whether to use a Skill by matching your task description against the Skill's description. A vague description never matches. A clear description lets Codex automatically judge "this task should use that Skill" when you speak.

One-line summary: Codex matches your task only by the description text, for implicit invocation. Put key use cases and trigger words up front. A vague description never triggers.

What is a good description. A contrast. Bad: "This is a data analysis Skill." Too vague, Codex does not know what scenario to use it. Good: "Read the collections data from Feishu's multi-dimensional table, summarize by product and channel, flag anomalies, output an Excel weekly report with charts. Trigger whenever I ask for 'collections reconciliation' or 'weekly report'." Scenario, action, output, and trigger words are all clear.

A few points for writing the description. Put the most common trigger scenario at the start so Codex sees at a glance what this Skill does. Write the trigger words clearly, explicitly saying "trigger whenever I say X or Y." What input, what output must also be stated so Codex knows what to read and what to give. One easily missed point: avoid generic words. "Data analysis" or "content creation" is too broad. Be specific to narrow scenarios like "Feishu collections reconciliation" or "official account article generation."

Beyond auto-matching, two fallback methods. One is explicit call, type `$skill-name` in the conversation to summon the Skill directly, not depending on auto-matching. The other is `@` mention, same syntax as referencing a file. These two ensure you can manually call even if auto-matching fails. But the premise is still a clear description, otherwise you would not even know which Skill to summon.

## 56. When do I actually need to touch MCP

Most ordinary scenarios do not need MCP. But a few specific scenarios make MCP unavoidable.

First, when not needed. If you only let Codex handle local files, make web pages, make PPTs, cut videos, analyze PDFs, built-in abilities and plugins are enough, no MCP. MCP is not "more advanced when used." It is a tool "only needed in specific scenarios."

When needed. When you want Codex to read outside data or use outside tools. The most common are a few kinds of work. You want Codex to read your GitHub repo, create branches, open PRs, comment on issues, use GitHub MCP and Codex operates directly, no manual carrying. You want Codex to read docs and tasks in Notion, Feishu, Linear, connect the corresponding MCP and Codex reads directly, saving you copy-paste. Another kind is letting Codex read some database, internal API, or some SaaS tool's data. As long as the corresponding service has an MCP, connect and use.

What MCP does is "give Codex a socket to connect external tools." A life analogy: Codex is a person who can work, MCP is the socket connecting tools for Codex, the MCP Server is the toolbox, the Tool is the specific tool. If the work you want Codex to do lives only in Codex's own head and local files, no socket needed. If the work involves outside data and tools, you must connect the socket.

If you judge you truly need MCP, configuration is not hard. Codex has an MCP management interface, add the MCP Server per prompts, fill in the start command and credentials. Common MCP Servers are ready-made, like GitHub, Notion, Feishu, various databases. After install, Codex can directly call these external tools in conversation.

Remember one line: MCP is something "enabled on demand," not something "installed to look professional." Do not touch without need, study when there is need.

## 57. Should I write AGENTS.md or not

Yes, and this is one of the key configs for using Codex steadily.

AGENTS.md is a project rule manual written for Codex. Every time you open a new conversation in this project, Codex reads this file first, knowing who you are, what the project is, what the rules are, what must not be touched. AGENTS.md is the most underrated file in Codex.

What if you do not write AGENTS.md. Every new conversation, Codex "re-learns" your project, each answer differs, each time you must re-explain the background. "No AGENTS.md" is the top bad habit that lets Codex use only 3% of its potential.

Writing AGENTS.md is not hard, and no need to write from scratch. The smart move: tell Codex your project goal in simple words and let Codex draft an AGENTS.md for you. You get a well-structured file, then modify per your needs. This is far faster, more complete, and less likely to miss things than writing from scratch.

What should a good AGENTS.md contain. Roughly four blocks. Start with background, one paragraph on who you are and why this project. Then the goal, one paragraph describing your final state. Then constraints, listed as a checklist of hard rules, like what tech stack, what not to use, safety boundaries, output format. Last is working habits, also a checklist, like "confirm the plan before editing code," "do not refactor on the way," "record failure experience."

Where to put it. One AGENTS.md at the project root, applies to the whole project. A sub-directory AGENTS.md holds that sub-module's specific rules. A user-level one (`~/.codex/AGENTS.md`) holds your personal rules across all projects, like globally forbidding certain dangerous commands. These layers stack and take effect.

For ordinary people, the minimal AGENTS.md only needs three things clear: what this project does, what language or style to answer you in, and what absolutely must not be touched. Write once, every later conversation saves effort. Further advanced patterns go to Q68 on high-value AGENTS.md patterns.

## 58. How to use task steering and task queuing

These two functions keep your control during a running task, called the "human-machine merged sense of control."

Task steering is interrupting Codex mid-way. When you find Codex wandering or about to hit a wall, no need to wait for Codex to finish, just interrupt and give Codex a new direction. Say Codex is reviewing a web page, you watch the sidebar and find some element spacing is off, directly say "the spacing between these two elements looks off, make it smaller." Codex receives your instruction immediately and adjusts the current work.

Task queuing is lining up later work for Codex. Codex is doing A, you want Codex to do B after A, no need to wait for A to finish, tell Codex now "after this is done, send the preview link to Slack." Codex queues B after A, and B auto-starts the moment A completes.

The difference is clear: steering changes what Codex is doing right now, queuing arranges what Codex will do next.

Why these two functions matter. Without them, your way of using Codex is "drop task, wait, see result, drop another," each step must wait for Codex to finish before the next, very low efficiency. With them, you can keep intervening and commanding during Codex's run, like a real collaborating colleague, not a black box you throw tasks at and forget.

When to use steering. The moment you see Codex's direction is wrong, use it, do not wait. When to use queuing. You already thought of the next step in your head, but the current step is not done, use queuing to line up the next step.

One small trick: by default, when you send a new instruction while Codex runs, the new instruction is queued (executed in order). If you want to jump the queue, have Codex handle the new instruction immediately instead of waiting for the current task, explicitly use the "steer" function and tell Codex "this is priority."

## 59. What is automation good for

Automation hands "things that need doing on a schedule" to Codex to run itself, like hiring an AI on-duty engineer for the project.

Good for automation are things with a fixed rhythm, a clear process, no need for you to rethink each time. The most typical is periodic summarization. Every morning let Codex organize project status, generate a weekly report each week, pull data from some source daily for a summary. Someone has Codex prepare an AI industry daily for them each day, so noteworthy info across the web reaches them first. There is also periodic checking, like checking the repo for problems weekly, checking collections data for anomalies daily, monitoring some web page or mailbox for updates regularly. Another useful kind is continuation. Resume the current thread after half an hour, return to the same conversation daily to push work forward on schedule. Conversation-flow automation returns to the same conversation on a set schedule to keep working, even adjusting the check-in frequency by situation.

Setting automation is not hard. After running a complex task through, directly tell Codex "run automatically at 9am every day" or "check once every Monday," and Codex automatically creates the automation task.

But one especially important reminder: the automation task's model selector does not inherit your active conversation's settings. A newly created automation uses the panel's default value, which may be slower and cheaper than the model you actually want. If you do not specify the model manually, a task that took 7 minutes may suddenly run 40. So when creating automation, always explicitly specify what model and what reasoning intensity.

Automation is a double-edged sword. Used well, automation works while you sleep. Used poorly, automation wanders, burns allowance, and produces garbage where you cannot see. When setting it, write the process clearly, specify the model right, and check Codex's output regularly, then it truly saves worry.

## 60. What is Computer Use, and is it safe

Computer Use is Codex's strongest and most caution-needed feature. It is the most praised ability, but also demands great care.

What can Computer Use do. Open apps on your computer, click buttons, read pages, fill forms, like a person sitting at your computer helping you operate. Codex can operate Xcode, Feishu, Figma, system settings, iOS simulator, any desktop app you installed and authorized, Codex can touch. Someone used Computer Use to write a legal research report from scratch, only doing the login to a few sites themselves, while search, exploring site structure, clicking, and organizing materials were all done by Codex in one pass.

Why so strong. Because Codex "sees" your screen. Computer Use works like: see screen, decide where to click, click, wait for app response, see again. Each step is based on the picture Codex sees, so Codex can operate any app with a graphical interface, no API from that app needed.

But a safety issue must be clear. Turning on Computer Use is handing part of your computer keys to Codex. Codex can touch all authorized desktop apps, including WeChat, email, browser, paid software, company tools, private data. Operations involving payment, account settings, deleting data, best not let Codex touch. Close unused sensitive apps, do not let Codex reach unrelated things. Give Codex only one clearly described task each time.

The minimum safety standard for beginners using Computer Use: first time, only let Codex operate risk-free apps, and especially remember not to let Codex operate social media accounts and WeChat. Once you have confidence in Codex's behavior pattern, loosen gradually.

There is also a difference among three "control" methods, most easily confused by ordinary people. Computer Use has the largest permission, can touch all authorized apps on the desktop, but is slowest. The Chrome extension has medium permission, enters your logged-in browser with your account and cookies, and sites treat Codex's actions as your own. The in-app browser has the smallest permission, fully isolated, carries none of your account info, best for local dev debugging.

Selection principle: desktop-app-related things use Computer Use, web tasks needing your login state use the Chrome extension, local dev and public page debugging use the in-app browser. Operations involving payment, publish, submit, delete, no matter which method, must be confirmed by you, do not let Codex auto-execute.

## 61. Which of the three browser methods to use

The three methods overlap, and beginners especially confuse them. Here is the selection logic.

The in-app browser is the most isolated and safest. It is a brand-new browser living inside Codex, with none of your cookies, accounts, extensions, or history, completely clean. Fits: opening a local dev server (localhost), debugging front-end styles, checking layouts at different screen sizes, annotating feedback directly on the page. The in-app browser cannot do pages needing login, but fits local dev and public page debugging best.

The Chrome extension carries your login state. It does not open a new browser, it enters your already-logged-in Chrome with your account, cookies, and open tabs. Fits: tasks needing your login state, operating multiple tabs, reading and comparing info across different pages. Typical: you already logged Vercel in the browser, let Codex go to Vercel Dashboard to see deploy status. You logged Feishu docs, let Codex read some doc. Sites treat Codex's actions as your own, so operations involving send, submit, payment, must be confirmed by you.

Computer Use operating the browser is the heaviest, slowest, broadest. When Codex uses Computer Use on the browser, it sees pixels and coordinates, like blind-clicking on screen, not understanding web structure. Fits: must operate desktop apps, need to switch among multiple apps, complete some "last step" (like uploading a file, confirming a popup). The contrast is clear: the whole task is in the browser, use the Chrome extension, do not use Computer Use. Need to operate desktop apps, only Computer Use works.

Simple memory: permission from small to large, isolation from strong to weak: in-app browser, then Chrome extension, then Computer Use. Use the smallest permission that completes the job. Local debugging uses the in-app browser, logged-in web tasks use the Chrome extension, desktop-app-related things use Computer Use.

There is another tool called Appshots. Appshots is not a fourth method, it is your way of "pointing" for Codex to see. On Mac quickly press the Command key twice (left CMD + right CMD) to capture the frontmost window, and Codex receives the screenshot and page text. Then you say "what does this error mean" or "I want to move this button to the right, how to change it." Appshots is your finger to point for Codex, while Computer Use, Chrome, browser are Codex's tools to "act."

But the three above are all "see screen and operate." One class of sites is especially hard: Pinduoduo backend, e-commerce admin backends, SaaS systems with anti-crawl detection. You operate with Computer Use and the site identifies it as automation and rejects access directly. Then switch to a fourth path: Playwright. Playwright can be understood as "let code directly control the browser kernel." It does not rely on seeing the screen or simulating keyboard-mouse, but directly finds buttons, fills forms, clicks pages through Chrome's underlying protocol, behavior closer to a real person. Combined with "reuse your already-logged-in browser," it bypasses most login-state detection. The division is clear: open sites (Google search, doc editing, X posting, Vercel-like), Computer Use or Chrome extension is enough. Backend systems with anti-crawl protection (e-commerce backend, pages with captcha, sites detecting WebDriver), Playwright is steadier. This leans advanced, beginners use the three basic methods first, study Playwright only when hitting the anti-crawl wall. Same warning: Playwright is also a risky operation, steps involving payment, submit, delete must be confirmed by you before letting Codex execute.

## 62. When should I use Worktree mode

Worktree opens an extra independent working copy for the same project, like a scratch notebook for Codex, letting it boldly edit without affecting your main project.

Why need Worktree. In Local mode, Codex edits directly in your current project directory, each change affects the real working files. Small fixes are fine, but if Codex wants to boldly try, refactor, or test an uncertain plan, editing on the main project is too risky, a break ruins your main project.

Worktree solves this. Worktree isolates changes in a Git worktree (an independent working directory bound to the same repo), Codex works in a separate branch, not affecting your main branch. If it runs wrong, just delete the worktree, zero risk, your main project untouched.

The rule of thumb: use Worktree for important work, Local for small fixes, Cloud for long-running automation. Three trust levels, choose by task.

When to use Worktree. Any work with wide impact and uncertain result should turn it on. Like letting Codex make a larger change, test an uncertain plan, or refactor and add a feature. Another: you want to do multiple tasks at once, compare multiple plans, each plan gets its own worktree without interference. In the end, whenever you want Codex to "boldly try, worst case just throw away," use Worktree.

When is Local enough. Changing copy, adjusting a color, fixing a small bug, changes small, controllable, completable while you watch, Local is fastest and most direct, no need for a dedicated worktree.

Worktree has a hidden benefit: comparing plans. You can open two worktrees for the same task, let Codex run two different approaches, compare which is better after, keep the good, discard the bad. This "parallel trial" is impossible in Local mode, because two changes would overwrite each other.

Ordinary people just starting Codex may feel Worktree sounds advanced and complex. Actually Worktree is just a "scratch notebook" concept, natural for Git users. Even if you do not use Git, understand Worktree as "give Codex an independent copy to edit, merge back to main after done." Any slightly larger change should use Worktree, the lowest-cost safety guarantee.

## 63. Which one to pick in multi-plan preview

This is a quite useful Codex feature: let Codex give you several different implementation plans for the same task, and you pick one.

The new Codex introduced a preview system that generates 2 to 4 different implementation options per task. Each plan may use different tech choices, different structures, different tradeoffs. You can compare and pick the most suitable, rather than accepting whatever Codex gives.

Which to look at. A few dimensions to judge. First see which fits your project's existing style. If your project uses tech stack A, and Codex gives one plan with A, one with B, pick the A one, integrates smoothest. Then look at change scope. Same feature, one changes 5 files, one changes 15, prefer the smaller change, lower introduction risk. Fewer dependencies is better. One introduces no new dependency, one needs a new library, pick the former, cleaner project. The most critical line: pick one you understand. A plan you cannot understand cannot be maintained later.

But multi-plan preview has traps. One is do not fall into choice paralysis. Codex gives 4 plans, you compare back and forth for half an hour unable to choose, more wasteful than just using the first. In most cases the first or second plan is enough, obsessing has little marginal benefit.

Another point, do not try them all. Someone thinks "I will run all 4 plans to see which is good," sounds reasonable, actually very allowance-costly. The point of multi-plan preview is to compare thinking before execution, not to actually execute each.

The right usage: look at the thinking descriptions and key differences of a few plans, pick the one you think most suitable, execute. If the result is unsatisfying, switch to another. This "look at thinking first, pick one, switch if not" way is far more efficient than "run each once."

## 64. What is the difference between Goal mode and a normal task

Goal mode draws a clear finish line for a task, letting Codex sprint toward it over a period.

A normal task: you state a need, Codex finishes and ends, whether it succeeded and to what degree decided by Codex's judgment. Goal mode differs. Besides the need you give a clear "success criterion," and Codex keeps striving toward that criterion until met or clearly unmet.

The contrast is clear. A bad Goal: "implement the plan in this Markdown file." No finish line, when Codex counts done is up to Codex itself, most likely "feels" done halfway.

A good Goal: "this new version's development is done only when all unit tests pass." Clear finish line, Codex knows what state to reach to count done, before that state it is not success.

What Goal mode does is combine "continuous execution" with a "verifier." You define the desired result, the stop condition, and the signal of whether Codex is getting closer to the finish. Useful verifiers include: a complete test suite, a benchmark performance test, a reliably reproducible bug, a verification matrix, a must-always-pass end-to-end workflow.

Fits Goal mode: code migration (from one language to another, goal all tests pass), bug fix (goal some bug no longer reproduces), performance optimization (goal some benchmark runs faster), refactor (goal function unchanged but structure better, all tests still pass).

Does not fit Goal mode: vague-need things, things with no objective acceptance standard, pure creative things. These have no clear "finish line," Goal mode cannot be used.

One sentence worth remembering: ambition matters, but ambition without a verification mechanism is just wishful thinking. The premise of Goal mode is you can give a verifiable finish line. If you can, Goal mode pushes complex tasks into place. If you cannot, normal task mode fits better.

## 65. How to use durable threads and pinning

Durable threads are an underrated Codex feature.

A normal conversation is "burn after chat": you open one, finish the task, close it, next time open new and re-explain background. Durable threads differ, they can run long and keep working context across multiple uses. Codex remembers your past decisions, your preferences, current progress, and next time you return to this conversation Codex is still in that state.

Why use durable threads. Much work is continuously pushed, not one-off. You build a product, may last weeks. You do content, may add new ideas daily. You monitor some data, may need continuous follow-up. In these scenarios re-explaining background each new conversation is tiring, durable threads let you "continue from last time."

The recommended usage is "pinning." Pin those durable threads needing continuous push, they are on call. Like a dedicated "chief of staff" thread handling daily chores, a thread for product release, a thread for reviewing docs, a thread for monitoring external data. These differ from the burn-after-chat small-talk box, they are persistent work spaces.

After pinning you can use shortcuts. Press Command-1 to Command-9 and you instantly jump back to these saved dedicated threads to continue work. This "one-key return to some work context" experience is far faster than flipping history each time to find the conversation.

Durable threads with shared memory are more powerful. Anchor these persistent conversations in a knowledge base, plainly a folder of plain-text files. Put an AGENTS.md at the outermost layer, setting rules for Codex: when Codex learns new situations, how to update this knowledge base. Then important context is not locked in one chat, but written down, placed where the next conversation flow can immediately pick up.

The ordinary person's starting usage: for the few types of things you do most, each open a durable thread and pin it. Like one "daily chores," one "my projects," one "study notes." Next time something comes up, go directly to the corresponding thread, no need to re-explain who you are and what you are doing each time.

## 66. How to build shared memory most steadily

Shared memory is the mechanism letting Codex keep context across conversations, and there is one steadiest way to build it.

Why build shared memory. Codex by default only has short-term memory. What Codex learns in this conversation, forgotten tomorrow. Each new conversation, Codex "re-learns" you and your project. If you repeatedly do similar things, re-explaining each time is low efficiency. Shared memory stores this repeatedly-needed context outside the conversation, letting future work continue on this info.

The steadiest build is a plain-text folder as the knowledge base. Plainly build a folder with markdown files inside. Example structure: under a vault folder, sub-directories TODO, people, projects, agent, notes. Put an AGENTS.md at the outermost layer, setting rules for Codex: when Codex learns new info about people, projects, decisions, todos, how to update this knowledge base.

Why a plain-text folder. It is simple and direct, convenient for you to view, modify, move anytime, can be kept long. A team can put this folder in any cloud drive, Git, Dropbox, Google Drive all work.

One especially important point: do not rigidly copy some one knowledge-base structure. What you need is to "teach" Codex: where persistent context should go, which context needs keeping, when not to recklessly edit files. Everyone works differently, the knowledge base structure should fit your reality, not copy a "standard template."

A practical AGENTS.md guide can write: treat this folder as long-term work memory. Organize notes tidily, do not scatter fragment records everywhere. Accurately categorize todos, people, projects, daily summaries. Save decisions made, blockers met, owners, dates, useful links. If no substantial new progress, do not casually modify files.

Codex itself provides an official memory feature, in Settings, Personalization, Memory. This feature is like a system-built local notepad, remembering your personal preferences, common workflows, frequent pitfalls. But this feature assists the context you clearly wrote down, not replaces it.

When you go deeper and want a smarter memory system, you can upgrade toward "indexing and semantic retrieval." Advanced players in the community use Obsidian as the memory base shell, add a layer of local database for keyword search, add a layer of semantic retrieval (find by meaning, not just original word match), with Git for version traces, a closeout script for auto wrap-up, an audit script for periodic health checks. This architecture upgrades the memory base from "a pile of text files" to "a searchable, auditable, self-running system." But this leans geek, high build cost. For ordinary users, first use the basic plain-text knowledge base well, upgrade this direction only when your rules grow too many to manage.

Ordinary starting point: build a folder, put an AGENTS.md, write clearly the few things you most need Codex to remember. Then use it, fill what is missing, slowly grow your own knowledge base. No need for a perfect structure at the start.

## 67. Why voice input is worth using

Voice input sounds like a small feature, but it solves a real problem: capturing the most raw, rough thought in your head first.

What is the problem with typing. You have a vague idea not fully formed. To type it, you instinctively "weigh every word," organizing language while thinking, filtering while trimming. This organizing process loses much info, the originally rich context compressed into a few dry sentences, and the AI gets less info.

Voice input bypasses this filter. You "mutter" to Codex for two or three minutes, pouring the idea out, the effect is surprisingly good. Example: "I remember someone called Ben mentioned this on Slack, forgot the details, go help me find it." For an agent that searches, gathers context, and reports to you on its own, such vague words are enough for Codex to work.

Transcribing recordings is the same logic. An unpolished meeting note, or a spoken plan draft, is often more valuable than a short summary. Those rough notes keep your hesitant tone, emphasized points, unfinished sparks. These details get "trimmed" when typing, but are exactly the key signals for AI to understand your real intent.

Voice input with task steering is more powerful. A task is running, you watch the sidebar and find some element wrong, no need to stop and type, just say "make this smaller" or "this copy is wrong." This "watch and talk" interaction is far smoother than "type to describe the problem."

When to use voice. When the idea is still vague and not fully formed, most should use it, pour it out then organize. When the need is complex and typing would be long, also worth it. When you want to interject anytime during a running task, speaking is far faster than typing. Also when you are walking and inconvenient to type.

Codex's voice input can be set as a global key, after on not only inside Codex but callable in any dialog box on the computer. If you are used to another voice input (like Doubao), no need to switch, the point is build the "speak with mouth" habit, not type everything.

## 68. What high-value advanced AGENTS.md patterns are there

Q57 covered the basic AGENTS.md writing. Writing more you find a few rule types especially useful, community-verified "efficient patterns." These four patterns each target a pain point, pick by need, no need to use all.

The first pattern is Confidence Gate, curing "half-finished products." Codex often declares done when the task is not truly done. Write a "definition of done" in AGENTS.md, making Codex self-score before declaring done, continue if the score is low. Template:

> Before declaring any task done, score yourself on three dimensions (each 0-10): 1. Test evidence, did you run tests, paste the output. 2. Behavior equivalence, did you verify public interfaces and behavior unchanged. 3. Cleanup, did you delete dead code, leave no commented-out blocks. All three reaching 8+ counts as done. Any below 8, keep working, do not ask me.

This pattern is especially effective against half-finished. To hit the score, Codex actively runs tests, actively verifies, actively cleans up, instead of stopping after the core feature.

The second pattern cures "frequent interruptions." In long tasks Codex stops now and then to ask "continue?" "what next?", breaking rhythm. Write clearly in AGENTS.md:

> Keep executing until the task is done, do not stop midway to ask me "continue?". For things needing confirmation, do the most reasonable thing first, record the decision, let me review together when I return.

This turns long tasks from "stop three times an hour" to "run continuously for hours," far more worry-free.

The third pattern cures "context explosion." Running long tasks, Codex stuffs the whole-page log of command output back into context, eating allowance. Constrain command output handling in AGENTS.md:

> For command output over 50 lines, keep only the tail and key error lines, do not stuff the whole-page log back into context. For heavy work like reading large files, open a new sub-conversation to read, the main conversation only takes the conclusion.

Someone measured this rule cut allowance consumption by about half.

The fourth pattern is a bit counterintuitive: do not let AGENTS.md be too long. A community cross-agent study found overly long AGENTS.md instead lowers performance. Codex spends more attention obeying all rules, instead missing the point. The right move is treat AGENTS.md as an "entry," only put the most core rules and guidance. Architecture details, implementation conventions, repo structure, split into separate markdown files referenced from AGENTS.md. Keep AGENTS.md to a length you can scan in one glance, Codex obeys better.

The fifth pattern is advanced: split habits into multiple files, route by scenario. When one AGENTS.md cannot hold all rules, do not force in, split by scenario into a few files, let Codex read the corresponding one before working.

Example split. One holds global usage habits: what system (like Windows defaults to PowerShell), file operations use `-LiteralPath`, do not mix Bash `&&`, confirm project directory before executing commands. These look fragmentary but decide whether Codex's commands run directly on your computer. Often Codex is not unable, but does not know your local environment. Another holds writing and communication preferences: Chinese direct, no filler, no forced elevation, untested tools must be marked "untested," so Codex does not write that standard AI tone. Another holds safety boundaries: do not delete user files, do not auto commit or push, check tokens and keys before publish, do not send private code to public search tools.

The benefit of "multi-file routing": each file short, focused, easy to maintain. Codex reads the corresponding one on demand, not disturbed by irrelevant rules. The downside is higher build cost than a single AGENTS.md, fits when you have used it a while and rules keep growing. Beginners first write the basic AGENTS.md from Q57, upgrade to this only when rules overflow.

## 69. How to make Codex explain its thinking before editing code

This is a specially practical anti-crash trick, lighter than plan mode, fits "do not want the full plan flow, but not comfortable letting Codex just do it" scenarios.

Normally you give a task and Codex starts directly. Codex works fast, by the time you want to intervene it has finished more than half. If you could hear Codex's thinking before it acts, many crashes are blocked early.

How to make Codex explain first. Simplest is directly say: "first tell me how you plan to do it, start editing after I confirm." Codex returns a thinking description, which files to change, what method, in how many steps. You read, if fine say "start executing," if wrong raise it in the thinking phase.

Complex tasks can use plan mode, type `/plan`, Codex returns a structured plan doc, more complete than just explaining thinking.

A more labor-saving approach is write it into AGENTS.md as Codex's default behavior. Like "for any multi-file change, tell me the thinking first, execute after I confirm." Then no need to remind each time, Codex defaults to explaining first.

Skipping the planning phase is the biggest cause of project errors. A one-sentence misunderstanding can make Codex edit forty files. Let Codex explain thinking, you correct in one sentence, ten times easier than changing after code is written.

When to use this trick. Any task involving multi-file changes, multiple approach choices where you want to join the decision, or high cost if wrong, must explain thinking first.

When not to. Renaming a variable, tweaking style, asking a simple question, things with strong certainty and easy rollback, just let Codex do it, explaining first is verbose.

Remember one principle: the higher the complexity and the stronger the irreversibility, the more let Codex explain thinking first. Simple reversible things can be let go, complex or wide-impact things must align thinking first. This habit blocks most crashes.

## 70. How to make Codex remember my project's conventions

The steadiest way to make Codex remember conventions is to write them down, not expect Codex to "remember" on its own.

Codex by default only has short-term memory, what it learns in this conversation, forgotten in the new one. Many complain "I told Codex several times not to touch that file, Codex still touches it," the root is Codex truly "forgot," what you said last time lives in last conversation, new conversation Codex does not know.

To truly remember conventions, rely on several "write down" mechanisms.

The most common is project-level AGENTS.md, write the project's hard rules inside, Codex reads each new conversation. Like "do not modify any file under the config directory," "all new components go in the components directory," "use our project's own code style." Write once, long-term effective.

One level up is user-level AGENTS.md (at `~/.codex/AGENTS.md`), write your personal general preferences here, effective for all your projects. Like "I prefer concise code," "explain impact before editing," "remind me first for privacy-related files."

If you have a fixed way of working, like "write docs in this structure," "do code review by this checklist," make this way a Skill. A Skill is explicit, callable, more reliable than pure memory.

Codex also has a built-in memory feature (Settings, Personalization, Memory), a system-level local notepad for your personal preferences, common workflows, pitfalls stepped on. But this feature is auxiliary, cannot replace the context you clearly wrote down.

One especially good suggestion: when meeting experience worth recording, tell Codex to update AGENTS.md or project memory. Say Codex tried a method and failed, you tell Codex "record this failure reason into AGENTS.md, do not try this method next time." The system gets smarter with use, because Codex wrote these lessons down.

One-line summary: do not expect Codex to "remember," make Codex "read." Things in AGENTS.md, Skill, knowledge base, Codex reads each time. Things only in conversation, gone next time. Important conventions must be written down.

## 71. Which small habits double result stability

Many small habits, each unremarkable alone, stack to astonishing effect. Here are a few most effective.

Most worth building: all complex tasks start with plan mode. The planning phase consumes little and blocks most wandering. Build the habit of "anything slightly complex gets `/plan`," crash rate drops sharply.

After each run do not only read Codex's text summary, go to the diff to see what Codex actually touched. See a wrong change, ask immediately, roll back immediately. This habit blocks "drive-by refactoring" and "over-engineering" before merge.

Clarify task boundaries. One clear task one thread, do not cram multiple things into one conversation. The more independent the task and the cleaner the context, the steadier Codex.

On failure stop then think. Send "stop, summarize the failure reason," far more useful than mindless retry. Let Codex give you a failure analysis, then decide the next step.

A few more easy ones: save good results immediately, agent output is one-time, what runs out is gone if not saved, satisfied results copied to the project folder and committed to git right away. Task description with acceptance criteria, clearly "the standard for done is X, missing any one does not count," half-finished probability drops sharply. Task description also with constraints, "do not touch X," "do not introduce new dependencies," "do not refactor on the way," the clearer the constraints, the more Codex converges.

Last two rules about allowance and cost. Check allowance often, investigate immediately if it drops fast, fully quit Codex when not using so background tasks do not sneak. Match reasoning intensity to task, small tasks use low to save allowance, only complex tasks use high, spend two seconds judging the tier before opening.

One more critical: when meeting experience worth recording, immediately write it into AGENTS.md, so Codex does not repeat the same mistake next time. The system gets smarter with use.

None of these habits is a deep technique, all are daily-operation small rules. Those who use Codex especially well rely not on secrets, but on doing these small habits every day. Stacked, their result stability is simply much higher than ordinary people.
