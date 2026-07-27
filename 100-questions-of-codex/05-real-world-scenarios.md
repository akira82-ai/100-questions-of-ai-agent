# Chapter 5 · Real-World Scenarios

## 72. What task should I use to practice for the first time

Do not practice on an important project, do not practice on a complex need. Start with a small thing where "done is nice, wasted is no loss."

What specifically to practice. Recommended: let Codex make a simple Hello web page. Black background, large text in the center, white font, horizontally and vertically centered, only HTML and CSS. This task fits practice especially well. It is clear, simple, verifiable, and when Codex finishes you see at a glance whether it is right. It involves few files, no messy dependency problems. If wrong, no cost, just edit and redo.

Be clear on one point: the core goal of first practice is to run through the whole flow "create project, give task, watch Codex execute, read diff, accept," not to actually make something useful. What you want to feel is how Codex works, how you interact with it, where results show. These flow experiences run through with the simplest task, no need for a complex task to add cognitive load.

A few small rules for the first time. First use normal chat to ask a simple question, confirm Codex replies normally and the whole environment is set up. Then build a clean project folder, do not use your existing important project. Turn on plan mode, let Codex produce a plan for you to glance at. After running, seriously read the diff, see the actual artifact, build the acceptance habit from the first time. Throughout, do not open full access, keep the "request approval" tier.

One view worth remembering: many Codex task failures are not because Codex cannot write code, but because it is asked to act before understanding the project. So first practice is about familiarizing yourself with "how to collaborate with Codex," not testing its ability. Once you run this flow smoothly, go to real work.

## 73. How to state needs when letting Codex build a web page

Building web pages is Codex's most classic scenario, and the one that most shows "how you state needs decides result quality."

The mistake beginners most often make is too vague needs. One sentence "help me build a website," and Codex gives you something entirely from its own imagination. Tech stack, style, structure all decided by Codex, far from what you want. You look at this thing unsatisfied, do not know how to change it, and get stuck.

The right way is to make the need concrete enough for Codex to follow. You can use a structure. Background: one paragraph, who you are, why build this page. Goal: one paragraph, describe the final state, like "a portfolio page showing my personal work, single-page app, responsive." Constraints: a list, hard rules, like "only HTML and CSS, no framework," "dark color scheme," "font use Source Han Sans." Done standard: how to count done, like "open in browser and see content, also displays normally on mobile."

A few techniques directly lift result quality. First state purpose and audience. "A portfolio for myself," "a showcase page for clients," "a prototype for demo." Different audiences, Codex gives very different structure and style, state early to avoid rework. More key: first let Codex use the image function to generate concept art. Before writing UI code, let Codex use gpt-image to generate one or two images simulating the page look, save to the project, then write code looking at the images. The final visual effect is far better than letting Codex design from text description. Another point worth mentioning: after done, open in the in-app browser to see the effect. Let Codex open it in the sidebar's built-in browser, you see the effect directly, circle what is wrong and let Codex change, far more efficient than repeatedly typing to describe the problem.

After done, the standard acceptance flow: read diff to confirm changes, see actual effect in built-in browser, check layout at mobile size, click each link to see if it works. Only when all these pass is the web page truly done.

## 74. How to play with letting Codex make PPTs

Making PPTs is one of the scenarios where non-programmers benefit most directly.

Before starting, install the PPT plugin. Codex may not have PPT ability by default, needs the Presentations plugin. After install, Codex can generate editable PPT files, real presentation files you can open and edit, not images or PDF.

With the plugin installed, the most important next is give Codex enough material. For PPTs, material quality directly decides result quality. For a mid-year report PPT, throw all related files, data, screenshots, PDFs to Codex, it understands all this content and integrates into a PPT. The richer and more specific your material, the closer the result to your need.

Material alone is not enough, needs must be clear, same as web pages. Vague needs only get vague results. State the theme, audience, style, what sections to include, roughly how many pages, especially the style. Business formal, lively simple, strong tech feel, these style words directly affect Codex's design.

Also keep in mind: an AI-made PPT in one shot will definitely not be 100% to your requirement. After Codex finishes, you just edit it directly. If the change is large, keep giving Codex requirements to let it change, faster than doing it from scratch yourself.

If you make PPTs frequently, you can also use a Skill to freeze the style. There are PPT Skills others made online, send the Skill address to Codex, let it install for you, then PPTs follow that Skill's style. If you have your own fixed PPT style, also make it your own Skill, each time follows your style, no re-explaining.

Installing the plugin is only the most basic path. The community now also has two more advanced routes, often better looking than plugin-generated PPTs. One is image-based PPT: first let Codex use image ability to generate 16:9 visual images one by one, then lay images into the PPT, each page a complete image. This route has good visual effect, but each page is an image, poor editability. The other is HTML-based PPT: not using traditional PPT software, directly write slides with HTML, CSS, JS, previewable in browser, can animate, can interact, can control layout with code, especially fits Codex as a code-execution tool. There are many open-source HTML PPT Skills online, search and let Codex install to use.

Beyond "writing a Skill," there is a newer, more labor-saving Skill creation method called Record & Replay. You demo a set of operations yourself on Mac, Codex watches once, automatically organizes the flow into a reusable Skill. Say you record an "article multi-platform distribution" flow: open article, change title, organize tags, check cover, switch platform, process again. After Codex observes it generates a Skill, next time you just say "use my article-distribution Skill, original is this, platforms are Xiaohongshu and official account," and Codex processes by your recorded rules.

This route fits especially those repetitive flows "with fixed steps but you cannot write them clearly, demonstrating once is clearer": content distribution, e-commerce selection, report organizing, backend entry. A few limits to know first: mainly macOS supports it now, Windows still waiting. Needs Computer Use permission on. High-risk operations (payment, transfer, dropping database) not recommended to record. Sites that change often record unstably. Best fit are flows with stable steps, stable pages, clear success standard, controllable risk.

The easiest pit in making PPTs is expecting Codex perfect in one shot. Codex's value is giving you an 80% done draft, you then process it. Expecting it to give a directly usable finished product in one shot will mostly disappoint. Expecting it to give a draft much faster to edit than doing from scratch yourself, that expectation is reliable.

## 75. Is letting Codex make videos reliable

Can do, and the effect can be stunning, but install the right plugin and give the right material.

Codex itself does not directly cut videos, Codex's video ability relies on plugins. Two paths: one is the HyperFrames by HeyGen plugin, specialized in motion videos. The other is Remotion Studio, generating video with code. Both paths' logic is "describe video with code," then the corresponding engine renders into a real video file.

One vivid e-commerce case. An e-commerce person used Codex to build an "e-commerce editing workflow": break down hit products, identify and select material, auto-dub with BGM, auto-align subtitles. After making this a Skill, each time just input a slash command, Codex runs by the pre-designed flow, and after running you see the edited video in the Jianying draft. Relying on this one workflow, he said e-commerce material output efficiency quintupled, daily orders up 60%.

The lesson of this case: video is not "drop one sentence to Codex and done." Video is a flow. Break down hits, select material, dub, subtitles, each step an independent task, combined is the complete video workflow. Freeze this workflow into a Skill, next time one-click call, far more efficient than re-explaining the flow each time.

To make video output stably, a few points to hold. Material must be complete, video quality largely depends on your material quality. The flow must be split fine, do not just say "help me make a video," split into "first break down hit structure," "then select these materials," "dub at this rhythm," "align subtitles in this format." Most critical is verify the result. You must watch the video Codex made, find wrong places and let Codex change, do not accept by default. Once this flow runs through once, freeze it as a Skill for next call.

Video is a scenario with high ceiling for Codex ability, but higher threshold than web pages and PPTs. Beginners do not touch video right away, first run the basic flow smoothly, then extend to complex scenarios like video.

## 76. How to use Codex to process PDFs and documents

This is one of the highest-frequency scenarios for non-programmers using Codex.

What can Codex do. Analyze medical checkups, convert PDF to markdown, extract key info from PDF, organize content of a pile of documents, compare similarities and differences of several documents. Someone directly throws family medical checkup PDFs to Codex, lets it analyze then organize suggestions onto a Feishu doc, never reading those medical data themselves. Others often need to convert PDF to MD files, also hand to Codex for batch processing.

Why does Codex do this especially well. Document processing is typical "clear input, verifiable output" task. Input is one or several documents, output is structured organized result, whether right you see at a glance. This task best uses Codex's execution ability, and involves no high-risk operation.

The key to stating needs is make the "output format" clear. Do not just say "help me analyze this report," say "help me analyze this report, output in this structure: 1. overall health status, 2. abnormal indicator list, 3. explanation and suggestion for each abnormal indicator, 4. follow-up items to watch." The clearer the output format, the more useful what Codex gives you.

Processing multiple documents, put all documents in the same project folder, let Codex read all at once, then integrate. Like comparing three contracts' clause differences, organizing five meeting notes into one summary, screening candidates meeting some condition from ten resumes. These tasks by hand take hours, handed to Codex finish in minutes.

Document processing has one especially fit scenario: batch format conversion and cleanup. Convert a pile of PDFs to markdown, extract plain text from a pile of Word docs, rename and categorize a pile of messy files by some rule. This repetitive, clearly-ruled work, Codex does fast and accurate, you by hand easily err.

The only caution is privacy. If documents have sensitive info (ID number, bank card number, company secrets), think clearly before letting Codex process. Content Codex processes goes through Codex's model. Although OpenAI has a privacy policy, truly confidential content still needs caution.

## 77. How to let Codex analyze data and do reconciliation

Data analysis and reconciliation is another scenario where ordinary people benefit frequently.

One typical reconciliation scenario. A business person every morning checks yesterday's collections data, sees if several tables' data match. Previously done by hand, easy to forget, easy to miss. This person made this flow a Skill: tell Codex which account to reconcile, how, what counts as anomaly. Then set a scheduled task, auto-runs once daily, alerts on anomaly. This flow moved from his head to the system, never forgets, never misses.

This case reveals the key of reconciliation tasks: what you do is write the reconciliation rules in your head into steps Codex can execute, not expect it to judge for you what counts as anomaly. If you do not say, Codex does not know what to reconcile, how to count anomaly, naturally cannot help.

Stating such needs, a few elements to clarify. First tell Codex where data is, Feishu multi-dimensional table, Excel file, database, or some SaaS tool, let Codex know where to read. Then state rules: which fields to match, by what key, what difference range is normal, how much over counts as anomaly. Then clearly say what to do on anomaly, email you, push to Feishu, write into report, or just flag for you to see. Last do not forget to agree what to output in normal cases, daily report, weekly report, summary table, what format.

Involving external data sources may need MCP. Say data is in Feishu multi-dimensional table, install Feishu CLI or Feishu MCP for Codex, Codex can directly read Feishu data. Data in Notion, install Notion MCP. Data in local Excel, just put in project folder, no MCP needed.

Reconciliation tasks especially fit Skill plus automation. Skill freezes the reconciliation rules, automation lets Codex run on schedule. Combined, it is an "AI on-duty accountant," checks itself daily, compares itself, proactively reports on anomaly. With this, the most time-consuming "gather background material" work is often done before you return, you only make the final call.

## 78. Is letting Codex clean my computer reliable

Reliable, and the effect is surprisingly good, but with caution.

Someone used Codex to check whether recently installed apps were fully uninstalled. Uninstalling software, many meet this: clearly uninstalled, but the system still has a pile of config files, caches, dependencies left, slowly filling the disk. Let Codex check whether some app uninstalled cleanly, Codex finds files and dependencies related to this app, sees if any left. If so, directly let Codex clean. This person said on macOS this method freed 20G space.

Why Codex fits this. "Find leftover files" is clear rules (find files of specific name, specific path, specific suffix), verifiable (found is found, not found is not), and involves no dangerous operation (show you the list before deleting, you confirm before delete). This task Codex completes steadily, easy for you to accept.

But there is a safety boundary to state clearly. First, always use project read-write tier, do not open full access, limit Codex to what it can handle, do not let it scan the whole disk. Second, must see the list before deleting, let Codex list what to delete, you confirm before it acts. Also, back up important files first, in case Codex judges wrong what to delete, you have backup to recover. Most critical, on uncertain files, do not blindly trust Codex saying it is "useless," ask one more "what is this file, what impact if deleted," decide after it explains.

Cleaning the computer involves deleting-data operations, best not let Codex auto-execute, you must confirm. Codex is especially good at "finding candidate deletions," but the "delete or not" decision is yours.

This "Codex finds, you decide, Codex executes" collaboration mode is the standard for risky tasks. Codex does the most time-consuming "find," you do the most critical "judge," Codex executes the operation you confirmed. This keeps Codex's efficiency while holding your control.

## 79. How to use Codex to write articles and make content

Content creation is one of Codex's strengths.

One content creator's example is typical. This person's current content output basically relies on Codex. A few days ago an official-account article, new account ran 1000 views, a small hit. This article from outline to draft, to cover, to illustrations, all done by Codex. This person only did some detail adjustments after.

This person also has an automated content production flow. Daily Codex prepares an AI industry daily for this person, noteworthy info across the web seen first. Then an automated topic Brief task: Codex reads the daily each day, finds writable topics, turns into a requirement Brief in this person's knowledge base. That hit article's topic was made by Codex for this person.

This usage reveals the key of content creation: the truly labor-saving approach is let Codex carry the time-consuming manual work of "find topics, do research, draft, illustrate," and you only make the judgment of "which topic, what to change, publish or not." That author's approach is this, only some detail adjustments after done, effect not bad.

To make content output stably, a few points. Most critical is give Codex a style guide, your writing style, target reader, content tone, written into AGENTS.md or made a Skill, Codex follows your style each time. There are also writing Skills others made online, directly usable. Style alone is not enough, input must be sufficient. How well Codex writes largely depends on the material and background you give. Prepare topic, research, material first (these can also be done by Codex), then let Codex write the body. One more mindset to set right: AI output in one shot will not be 100% to your requirement. Expect it to give you an 80% draft, you then refine, not expect one-shot perfect.

Content creation also has a point fit for automation: periodic monitoring and topic finding. Daily let Codex scan your watched info sources, find writable content, organize into a topic list in your knowledge base. When you sit to write, the topic is there, research half done, you directly enter the "write and edit" stage, far more efficient.

## 80. How to use Codex most cost-effectively for a full side project

A side project is Codex's sweet spot.

Why side projects fit especially. A side project is usually one person, controllable scale, self-defined needs, low cost if wrong. In this scenario Codex's ceiling is fully enough, allowance consumption within control, you feel the "AI did most of the work for me" thrill.

The most cost-effective usage advances by a "six-step method." The full flow: requirement breakdown, make plan, small-step implement, test, code review, commit and review. Each step has a corresponding prompt template, advance step by step, far more reliable than dropping one big need.

Step one requirement breakdown. Write clearly what you want, seven elements: background, what to solve, related files, what not to touch, done standard, what tests needed, what risks. Step two make plan. Use plan mode to let Codex produce a plan, you review and confirm. Step three small-step implement. Do not let Codex finish the whole project in one breath, split by module, by feature, step by step, verify immediately each step. Step four test. Let Codex write test cases, pass to count this step done. Step five code review. Recommended two rounds: first round Codex self-reviews, exposes obvious problems first. Second round you manually review, focus on boundary conditions, safety, whether wrongly deleted, business logic. Step six commit and review. After editing commit to git, record problems met this time, summarize useful Prompts, update AGENTS.md.

Side projects also fit a work mode: ChatGPT plus Codex combo. First use ChatGPT to think clear, then Codex enters project to execute. ChatGPT is consultant, helps clarify thinking, do tech selection, discuss plans. Codex is intern, enters project to land the work. The two together beat either alone.

To save allowance, a few habits worth building. Complex tasks start with plan mode, planning phase consumes little, right planning means no waste in execution. Small tasks use low reasoning intensity, only complex tasks use high. Do not let Codex scan the whole project at once, specify files when you can. Also do not repeatedly refactor broadly, that operation burns allowance most. One more experience: when unsure, first let Codex explain thinking, you confirm then let it execute, more cost-effective than diving in and hitting a wall.

A side project is the best "practice field" for using Codex. You run the whole flow smoothly on a side project, familiarize with Codex's working way, then go to real production projects, you have confidence. To let Codex semi-auto run long projects, Q87 specifically covers that "semi-automatic workflow."

## 81. How to hand bug fixes to Codex most effectively

Bug fixing is one of the scenarios where Codex shows most value, but how you state needs decides success.

The most effective way: give Codex the complete error message, plus steps to reproduce this bug, plus related code files. The standard is send the error message directly to Codex, let it analyze itself. Codex can read the complete error stack, reproduce in your project, edit then run to verify. This "Codex really runs through in its own environment" ability is where Codex beats normal chat far more in bug fixing.

The mistake beginners most often make is only describe the bug without giving info. One sentence "my login page errors," Codex can only guess. Codex does not know what error, what your code looks like, how to reproduce, advice is generic, cannot solve your real problem.

The right way assembles these things. First give it the complete error, console output, error message, error stack copied directly, or screenshot (Codex supports image input). Then state reproduction steps: how you triggered this bug, where clicked, what entered, what operation. Also point to related files, tell Codex roughly which files, which functions the bug is in, narrow its search. Last do not miss environment info, what OS, what browser, what version, sometimes critical.

Bug fixing also fits a mode: let Codex reproduce first, then fix. Let Codex run once in your project, trigger that bug, confirm Codex can reproduce. Then let Codex fix. After fixing run again, confirm bug gone. This "reproduce first, then fix, then verify" loop is far more reliable than "Codex gives you a block of code you try" because Codex already verified in its own environment.

For hard bugs, recommended Goal mode. Give a clear finish line: "until this bug no longer reproduces, the fix counts done." Codex keeps striving toward this goal, tries various methods, verifies each, until the bug truly disappears.

The easiest pit in bug fixing is "fix one, introduce two." Codex finishes the bug, you may not notice Codex edited other things on the way, result bug fixed but new problem introduced. Defense is still that line: after each run read the diff, find Codex edited files unrelated to the bug, ask immediately, roll back immediately.

## 82. How to split new features for Codex

Adding new features is the most common need in side projects, the standard is "small-step implement."

The mistake beginners most often make is drop a big feature in one sentence. "Add a user system to my site," Codex hearing this builds a set from its own understanding, login, register, permission, database, session management, all done. Result most likely mismatches your existing project structure, introduces a bunch of new dependencies, may also touch places you do not want touched.

The right split is by "user-perceivable feature unit," not by "technical module." Say the big feature "add user system" should split into: step one add register page (user can fill form and submit), step two add login page (user can log in and out), step three add permission control (logged-in user sees specific content), step four add user profile page (user can view and edit own info). Each step a "user-perceivable feature unit," each independently acceptable.

How to execute each step. First use plan mode to let Codex produce a plan, you review and confirm. Then clearly tell it "this time only implement this step, do not do the next step on the way," frame it in the current feature unit. After done accept immediately, confirm this step truly done, then enter next step. Commit git once per step, leave a version node, convenient to roll back later.

One anti-pattern to watch: let Codex refactor unrelated code on the way. When adding features, Codex may feel existing code "not elegant enough," refactor on the way, introducing various surprises. Defense sentence written into task description: "this time only implement the current feature point, do not refactor unrelated code on the way, do not modify naming, directory structure, dependency versions, or global config."

Adding features also note one point: regression testing. Changing the homepage button may also affect other pages reusing the same component. After adding the new feature, not only test the new feature itself, also test whether original functions are affected. This "regression testing" is most easily ignored. You stare at the new feature, forget to confirm whether Codex broke something else on the way. Let Codex run the full test suite, or you manually click the core flow, confirm no new problem introduced.

## 83. Dare I hand an old project to Codex for refactoring

Dare, but with extreme caution, and definitely use Worktree mode.

Old project refactoring is a high-ceiling scenario for Codex, also the easiest to crash. Old projects usually have much code, heavy historical baggage, complex coupling, maybe a pile of legacy issues. Letting Codex make big changes on top, risk is naturally high.

Old projects have a few specific pits to know early. First, old projects themselves may have lint or type issues, do not let Codex refactor on the way. It sees these "problems" and wants to "fix," one fix drags a bunch of changes, breaks a runnable project. Second, respect the old project's historical baggage. Some code looks "bad" but was written for a special reason then, changing may introduce hidden bugs. Most critical, old project coupling is more complex than you think, change one place, may affect somewhere you never imagined.

The right approach is a set. Definitely use Worktree mode, give Codex an independent working copy to edit, your main project untouched. It finishes, you review, after review merge back to main, if broken just discard the worktree, zero risk. Each time only let Codex change a small block, not "refactor the whole module," but "only clarify this one function," "only extract this one component," smaller change scope, lower introduction risk. Each step must run full tests, the premise old projects can be changed is having tests. Old projects without tests, each step you must manually verify the core flow. Also watch the diff, every line Codex changes you read, find it refactored unrelated code on the way, roll back immediately.

Old project refactoring also fits a Goal mode scenario: code migration. Migrate an internal tool from Python to Rust. Build the new directory, set the goal: "until all unit tests pass, this new version's development counts done." Codex keeps striving toward this goal, runs tests each change, until all pass.

The most important mindset shift in old project refactoring: slow is fast. Do not rush Codex to refactor a big block at once, rather slower, steadier, verify each step. One sentence worth remembering: delivery is not the end, review is where next efficiency gain starts. After refactoring a block, review: where crashed, where Codex did well, how to split more reasonably next time. This review makes later refactoring smoother.

## 84. How to hand test writing to Codex

Writing tests is Codex's strength, recommended as a key technique for stable output.

Why test writing especially fits Codex. Tests feature "clear input, clear expectation, verify output." This clearly-ruled, auto-verifiable task is exactly what agents do best. Codex can read your code, infer boundary conditions, generate various test cases, then run itself to verify which pass which fail.

The most effective way: first let Codex read the code to test, then let it generate tests. Do not directly say "write tests for this function," but say "read this function's implementation, find all boundary conditions, write a test case for each, run to confirm all pass." This way lets Codex truly understand the code, find all boundaries, not mechanically generate a few routine cases.

There is also a reverse usage: write tests first, then let Codex implement. This thinking fits new features especially. You first tell Codex "this feature must satisfy these test cases," let Codex implement looking at the tests. Tests are clear, verifiable, the code Codex implements just needs to make all tests pass, counts done. This "test-driven" way is far steadier than "implement then patch tests." The Superpowers Skill is this thinking: clarify needs first, write spec, make plan, advance with TDD.

Test writing has a few pits to avoid. Do not let Codex only write "happy path" tests. It tends to write "normal case runs" tests, but truly valuable are boundary tests, like empty input, over-long input, illegal input, concurrency. Explicitly tell Codex "focus on boundary conditions," otherwise your tests do not cover real scenarios. Another hidden pit: tests and implementation may drift together. Sometimes Codex writes tests by one understanding, writes implementation by another, result tests pass but function is wrong. Defense: first confirm the test cases themselves are right, then let Codex implement. Also, tests need diff reading too. Accept without looking, may introduce meaningless tests, miss key tests. Glance at the tests it wrote, confirm covering the scenarios you want.

Test writing is "front investment, long-term benefit." First time letting Codex write tests may be slower than directly implementing, but with tests, each later change can run tests to verify, regression problems drop sharply. Writing tests is listed as a key stable-output technique for this reason.

## 85. Is letting Codex do code review reliable

Reliable, and in some aspects more detailed than human review, but must be used well.

Codex doing code review is let Codex read a set of code changes, find problems. Recommended two-round review. First round Codex self-reviews, outputs a problem list, exposes obvious bugs, boundary issues, safety risks first. This step is "let the Codex that wrote the code pick its own errors," often blocks low-level problems. Second round human review, you look at Codex's list and the diff, focus on judging whether the problems Codex found are real, whether anything missed.

This "one writes, one picks errors" mode is especially recommended for high-risk scenarios: changes involving login, payment, permission, database, auth, suggest a second model do cross-review. First model writes code, second model reviews, two models from different angles, far more reliable than one model writing and reviewing itself.

What is Codex good at in code review. Boundary conditions, it can think of various boundary inputs, remind where unhandled. Safety issues, like common injection, privilege escalation, sensitive info leak, it can identify. Obvious bugs, like null pointer, array out of bounds, logic error, these it also finds. Also style and consistency, inconsistent naming, not following project conventions, it can point out.

Codex's limits in code review also clear. Business logic it cannot see. Whether your code meets business needs, it cannot judge, because it does not know your business, this part you review. Architecture reasonableness its judgment also limited, can see local problems, but whether overall architecture is reasonable, what it says may not be reliable. Also, it may false-positive, say "problem here," but actually you intentionally wrote it that way, it does not know context. So its report you must judge, not fully trust.

Codex review also fits a scenario: review once before merge. Let Codex read the diff, list problems, you judge each. This is more efficient than reading diff line by line yourself, because human attention is limited, staring at diff long you miss problems, while Codex keeps consistent detail from start to end.

But always remember that hard rule: do not let AI auto-merge PRs. Codex can review, can find problems, but the "change or not, merge or not" decision is always yours. Codex's review is auxiliary, not a replacement for your judgment.

## 86. Can a team collaborate with multiple people

Can, but different from single-person usage, with some special notes.

First, project folder collaboration. Codex works in a local folder. If a team multiple people all use it on the same project, the steadiest way is Git. Each person runs Codex on their own computer, commits to Git after editing, collaborates via Git. Never let multiple people simultaneously use Codex to edit the same folder, file state conflicts, changes overwrite each other.

More critical is AGENTS.md's value in teams. In team scenarios, write the team's code norms, tech stack conventions, untouchable files, commit norms into AGENTS.md, place at project root. Then no matter who in the team opens this project with Codex, Codex follows the same rules, output style unified. AGENTS.md itself also commits to Git, all team members share the same rules.

Skills can also be team-reused. A team member makes some workflow a Skill, share to others. A Skill is just a markdown file in the folder, commit to the Git repo and everyone can use. Say the team unifies a "code review Skill," everyone reviews code by this Skill, review quality naturally unified.

Two more points to keep in mind. Allowance is per account, team multiple people using Codex, each uses their own ChatGPT account, allowance independent. To unify manage allowance, consider Team or Business plans. Business plan has team management, but specific plans and allowance change, refer to official page. Also be careful with sensitive data. In team scenarios data Codex processes may involve customer data, trade secrets, internal systems. Before processing think clearly data goes through Codex's model, complies with company data security policy. Truly confidential content, handle cautiously or simply not use Codex.

The core principle of team collaboration: Codex is a personal tool, team collaboration relies on Git and shared config files. Each person uses their own Codex for their own work, merges results via Git, keeps consistency via shared AGENTS.md and Skills. Do not try to treat Codex as a "team-shared tool," Codex's design is not for multiple people operating the same folder at once.

## 87. How to set up Codex to semi-auto run long projects

Many hearing automation stories think "full automation" is drop one prompt to Codex then go sleep. Community members who really did it tell you: this play is extremely risky, true "semi-auto" is another thing.

The semi-auto workflow verified by many is held up by three things: a task list, a watchdog mechanism, frequent version snapshots.

The task list is you use ChatGPT to first split needs into a structured list, write into a file (like `task-list.md`), as Codex's "progress ledger." Codex knows globally what to do, how far, advances by the list.

The watchdog mechanism (community slang watchdog, understand as "supervisor") periodically checks list progress, pulls wandering Codex back on track. Codex long tasks most easily veer, a list alone is not enough, something must watch it not zone out.

Version snapshot is after each step commit a version snapshot of your project (with Git commit once, without Git copy a backup). In case some step crashes, you roll back to the last known-good state, not lose everything.

How far can this loop run. Community measured: hours of unattended, multi-file implement-while-testing loop, is achievable, someone ran an 8-hour long task with this. But the realistic boundary also clear. High consumption, one several-hour autonomous run may eat over a tenth of the weekly allowance. Will veer, so needs the watchdog. High risk, unsupervised Codex is most dangerous.

So "full auto" must be understood right: the true goal is build a "task list plus watchdog plus frequent version snapshot" semi-auto loop, letting you keep advancing without watching full-time, while keeping the ability to intervene and roll back anytime, not "one prompt then sleep." Than the "hand all to AI" fantasy, this semi-auto loop is far more honest and far more practical.

This set leans advanced. If you just started, first run the basic scenarios Q72 to Q86 smoothly, then consider semi-auto. Ordinary users do not have to touch it, knowing this direction exists is enough.
