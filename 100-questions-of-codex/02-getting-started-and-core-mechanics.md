# Chapter 2 · Getting Started and Core Mechanics

## 16. What should be the first step when using Codex for the first time

Do not rush to assign work. Do two things first: install and health-check.

There is only one download channel, the official OpenAI entry. Mac users go to the site for the dmg, and must tell Apple Silicon (M-series chips) from Intel versions. Pick wrong and it will not install. Windows users search Codex in the Microsoft Store and confirm the publisher is OpenAI. The Windows version shipped in March 2026 and works best on Windows 11, though Windows 10 is supported. Do not download from odd third-party sites, where quality varies wildly.

On first launch after install, you go through a login flow. Three options: ChatGPT account login, API Key login, or a third-party relay. Ordinary users pick the first, log in with your ChatGPT account, and use the subscription allowance. This is the most worry-free. The API Key is for developers and automation, beginners should not touch it.

After login Codex asks your professional identity (Engineer, PM, HR, and so on). Pick any, it is only for OpenAI statistics and does not affect function. Then it asks whether to turn on Sandbox mode. Always click Set up to enable it, so Codex will not mess with anything outside your project directory when running commands.

After all this, do not drop a task yet. Send a casual "hello" to confirm Codex replies normally, which means the whole setup works. Then start real project work.

The minimum goal for first contact is one line: confirm "installed right, logged in right, can run." Whether it can do the work can wait. Get this step smooth and you avoid buried mines later.

## 17. Which login method to choose, ChatGPT account or API Key

Ordinary users pick ChatGPT account login. Do not touch the API Key. This is the fork beginners most easily get wrong.

ChatGPT account login uses your subscription allowance. Plus, Pro, and these tiers give you a certain amount of usage each month, which recovers next cycle when used up. You do not worry about how many tokens or how much money, OpenAI calculates it for you. This mode is transparent and predictable for ordinary people, the most worry-free.

API Key login uses OpenAI Platform's pay-as-you-go billing. However many tokens you use, that much gets deducted, like prepaid phone credit. The upside is no fixed monthly fee, pay for what you use. The downside is you must watch consumption, and a task that wanders can burn a chunk of money in an instant. This mode suits developers, automation scenarios, and CI/CD pipelines, not ordinary daily use.

One standard: if you have to pause and think about what "token" or "pay-as-you-go" means, then honestly use ChatGPT account login. Once you are familiar and want fine cost control, study the API Key path.

There is a third route, connecting domestic models through a tool like CC Switch. This route also uses an API Key, but spends the domestic vendor's allowance. It is cheaper for China-based users, but is unofficial, detailed in Chapter 6.

## 18. What exactly is a project, and why must you create one first

A project is a folder on your computer.

Codex is not a simple chat tool. Codex needs to enter a concrete "project directory" to work. When you create a project, you let Codex pick a folder. After that, every file in that folder, Codex can read, write, and edit. The folder is Codex's working boundary and also its trust boundary.

Why this step is mandatory. Codex's core ability is "to act," and acting needs a place to act. You tell Codex "help me fix this web page," and Codex needs to know which folder the page is in, what files exist, where dependencies are installed. Without a clear project directory, Codex is like a person blindfolded and dropped into a strange office, not knowing where to start.

Many people skip creating a project and tell Codex to work directly in a normal chat box, then hit a pile of weird things. Codex says it cannot find the file. Codex edited something and you do not know where it saved. Codex ran a command and reported a baffling error. The root of all these problems is "no project created."

Creating a project has another benefit: the result is traceable. In project mode, all files Codex generates live in one folder. You open the folder and see every artifact, instead of having things scattered everywhere like in chat mode, unfindable. Daily use is basically all project mode, unless you ask a quick temporary question in normal chat.

So the correct opening is: first build a dedicated folder as your workspace, then treat each specific task as a project inside that folder.

## 19. Which project folder to pick, and what are the traps

This choice matters far more than you think. Pick wrong and everything after is trouble.

First, what to pick. Create a clean folder specifically for Codex, with subfolders per project inside it. For example `D:\AI-Codex-Projects\my-web-project`, or on Mac `~/AI-Codex-Projects/my-web-project`. English paths are safest. Chinese paths and spaces cause particular trouble on Windows.

Then, what never to pick. C drive root, desktop, downloads, system directories, important data folders, Chinese paths, paths with spaces, none of these work.

C drive root and system directories are permission-sensitive, and Codex's commands easily hit a wall. Desktop and downloads are too messy, full of everything, and Codex cannot tell which are the files you want processed and which are your private files. The risk with important data folders is that if Codex misunderstands the task and edits or deletes your important files, recovery is painful. Chinese paths and spaces are technical-level traps. Many command-line tools handle these two path types poorly and throw baffling errors.

One hidden trap: do not pick a folder currently occupied by another program. If you are editing this project in VS Code while also telling Codex to edit it, the two may conflict and the file state gets messy. Either close the editor, or use worktree mode for Codex (covered later).

Remember one iron rule: build a clean, dedicated, English-path working folder, treat it as the shared workspace between you and Codex, and let all projects happen inside it.

## 20. How to choose among the three Sandbox tiers

Sandbox is Codex's safety fence, with three tiers. Pick wrong and either your hands are tied or the risk runs out of control.

The first tier is read-only. Codex can only look at files in your project, not change anything. It fits scenarios where you only want Codex to analyze, explain, or advise, but not touch files. For example "help me see if this project's architecture is reasonable" is safest on read-only.

The second tier is project read-write. Codex can edit files in your current project folder, but cannot leave that folder. This is the daily recommended tier, used for the vast majority of work. Codex can read, write, run commands, and install dependencies, but all actions are confined to your project directory. Files elsewhere on your computer are unreachable.

The third tier is full access. Codex can touch the entire computer. Beginners should not touch this tier. Only consider it when you are very clear about what you are doing and fully trust the current task. Turning this on is like handing the computer keys entirely to Codex. If Codex misunderstands the task, it can cause big trouble.

These three tiers map to three options in Codex: "request approval / auto-review / full access." Beginners should keep "request approval," meaning any command asks you before executing, and only runs after you confirm. This is slower but safe. The middle "auto-review" tier lets the system decide for you whether certain safe operations should pass. It is more worry-free than "request approval" but not as lax as "full access."

How much permission to grant is ultimately a tradeoff between trust and efficiency. Small permission is safe but tedious. Large permission is smooth but risky. Start small, and loosen gradually once you are familiar and trust is built. Opening maximum permission right away is the easiest way to crash.

## 21. What is the difference between the reasoning intensity tiers

Reasoning intensity controls how long Codex thinks before answering you. Higher tiers mean Codex thinks deeper, but slower and more allowance-burning.

Usually there are four tiers. Low fits light work like editing copy, changing colors, answering small questions, done in seconds. Medium fits ordinary web pages, simple bugs, daily development. This is the most used tier. High fits multi-file edits, complex bugs, refactoring, work that needs deep thought. The highest tier fits very hard problems, architecture analysis, bugs that will not fix. Codex thinks a long time, but often reaches solutions you would not expect.

The mistake many make is turning the highest reasoning on for every task, feeling "higher is smarter." This is a double waste. Small tasks need no such deep thought. High and low give the same result on something like renaming a variable, and you waited for nothing. High consumes far more allowance than low, and you burned allowance for nothing.

The correct usage is to match the task. Editing text or tweaking style, use low. Building a normal feature or fixing a routine bug, use medium. Only when you hit something truly complex that needs Codex's deep analysis do you go high. The core principle for saving allowance is this one line: do not turn on highest reasoning for small tasks.

If you are unsure which tier, start at medium. Medium is the sweet spot of "enough and not wasteful." Run it, see the result, then go up or down. After a few times you learn the pattern.

By the way, the current main model. As of mid-2026, Codex's flagship model is GPT-5.5, shipped in late April 2026. Plus, Pro, Business, and Enterprise accounts can all use it, and Edu and Go are within the official available range. Compared to the previously programming-specialized GPT-5.3-Codex, GPT-5.5 is more like an engineering lead that can plan, execute, and check, strong in reasoning and long-chain tasks. Two key numbers are worth noting for Codex users: the context window expanded to 400K tokens (fits larger projects and longer conversations), and there is a Fast mode (about 1.5x faster, but about 2.5x token consumption, for time-pressed tasks). Models and tiers keep updating, so what your account can actually select is the final word.

## 22. What is plan mode, and when should you turn it on

Plan mode is the most underrated feature of Codex, and the most important gate against crashing.

In normal mode, you give a task and Codex starts working directly. In plan mode, Codex does not act immediately. It stops first and lays out a work plan: how it intends to do it, in how many steps, which files it will touch, what the risks are. Then it waits for your confirmation before starting.

Why this mode matters so much. An agent works fast, fast enough that you cannot react. You drop one sentence and Codex may have edited a dozen files. By the time you find the direction is wrong, it has finished more than half, and rolling back is a pain. Plan mode gives you a chance to brake. Before Codex really acts, first see whether Codex's thinking is right.

Skipping plan mode is the biggest cause of project errors. A one-sentence misunderstanding can make Codex edit forty files, while if you saw the plan first, one sentence could correct it.

When to turn it on. Turn on plan mode first for any moderately complex task. Renaming a variable or tweaking a color needs no plan, but anything involving multiple files, new features, refactoring, or complex bugs, turn on plan mode and let Codex produce a plan. You review it, then let Codex execute.

The usage is simple. Type `/plan` in the dialog, or say "give me a plan first" when describing the task. Codex returns a step-by-step plan. If it looks fine, say "start executing." If something is wrong, raise it in the plan phase. That is ten times easier than changing after the code is written.

## 23. What is the sidebar for, and why is it so important

The sidebar is Codex's "work inspection area," and the key that sets Codex apart from ordinary chat tools.

In normal chat, the AI gives you a block of text or code, and you are done after reading. Codex is different. While Codex works, the right-hand sidebar shows in real time what Codex is doing, what it generated, and where it edited. This sidebar is Codex's "work site."

The sidebar can show many things: files Codex generated, search sources, web previews, image previews, PDF previews, a built-in browser, and code change comparisons. The middle tells you "what Codex did," the right lets you see "what Codex produced."

Among the sidebar's most valuable uses, the one to watch closest is the code changes. After Codex edits a file, the sidebar shows a diff, green is added and red is removed, so you clearly see which lines Codex actually touched. Beyond that, if Codex made a web page, the sidebar opens it directly so you can see the effect without starting a server yourself. Better still, when previewing the web page you can circle a button on the page and say "make this color darker," and Codex receives your feedback precisely, editing only the spot you pointed at.

Many people, when first using Codex, keep their eyes only on the middle dialog box and use Codex like a chat tool, completely ignoring the sidebar. This is a huge waste. People who truly know how to use it keep their eyes on the sidebar, because that is where Codex does the work. The middle conversation is only your channel to command Codex. The right sidebar is where Codex hands in its homework.

## 24. What is a diff, and why check it every time

A diff is the comparison of code changes, green for added and red for removed. Every time Codex finishes a task, the first thing is to look at the diff.

Why stress the diff so much. Codex edits fast, fast enough that you do not know what it actually changed. If you only read the text summary Codex wrote, "I modified the login logic and optimized the style," you have no idea which specific places moved. A text summary can gloss over things. A diff never lies.

Looking at the diff helps you catch several kinds of problems. The most common: Codex edited somewhere it should not. You thought you asked Codex to fix the login page, but it also tweaked the homepage style along the way. This "editing by the way" is obvious in the diff at a glance. Another is deleting things it should not. Some code Codex thinks "useless" and deletes, but it is actually your business logic. Then there is a mysteriously extra dependency or new file, all very visible in the diff.

One hard rule worth repeating: after every Codex task completes, look at the diff first, then decide whether to accept. Do not relax just because you read the text summary. When you see a change you do not understand, stop and ask Codex "why did you change this," rather than accepting by default.

The diff can also be used to iterate. You leave a comment next to one diff line saying "this change is wrong, do it another way," and Codex receives your feedback and edits only that spot again. This is far more efficient than re-describing the whole task.

Building the habit of "look at the diff first" is the minimum bar for using Codex steadily. This habit blocks most crashes before they are merged.

## 25. What is a thread, and how many can one project have

A thread is one specific task conversation inside a project. One project can have many threads.

Why separate threads. A project usually has more than one thing to do. While building a web page, you may have Codex fix a homepage bug, add a new feature, and change the style, all at once. These are three independent tasks. Cramming them into one conversation gets messy. Codex cannot tell whether your new sentence continues the last task or starts a new one, and the context gets tangled.

The correct approach is one clear task per thread. Fixing a bug is one thread, adding a feature is another, changing style is yet another. Each thread focuses on one thing, the context stays clean, and the result is clear. The project is like a company, the thread like an employee in the company, each handling one pile of work.

Threads can run in parallel. After assigning one task, you need not wait for Codex to finish. You can open a new conversation and assign another directly. As long as multiple tasks are not editing the same file, they do not interfere. Each thread's progress is independent, and you can see separately which finished and which is still running.

Finished threads can be archived. Archiving is not deleting code, it is collapsing the task list to keep the interface clean. Archived threads can be retrieved. Unarchive in settings and it restores. If a thread ran poorly and you want to try a new approach, you can fork a copy to test the new plan while the original stays.

Remember one line: do not cram everything into the same thread. The clearer the task and the more independent the thread, the steadier Codex is.

## 26. How do I know how long a task will still run

There is no precise answer, but a few signals tell you.

While Codex runs a task, the status of that task in the left conversation list changes. If it is a spinning icon, Codex is still working, not done. If it becomes a static blue dot, the task has finished and you can accept it.

As for exactly how long, Codex gives you no countdown. A task can be done in tens of seconds fast, or tens of minutes slow, a huge gap. Factors: the task's own complexity, whether Codex needs to install dependencies, how many rounds of trial-and-error Codex runs, and the current model version's state. Renaming a variable finishes in seconds. Having Codex build a complete app from scratch running half an hour is not strange.

If you feel Codex is running too long, you can peek midway at what Codex is doing. Open that thread and you can see the action Codex is currently executing, reading a file, running a command, waiting for something. If Codex is stuck on one action for a long time with no movement, it may have hit a problem. If Codex is advancing step by step normally, then the task itself just needs that long.

One common phenomenon to watch: Codex can fall into a "spinning its wheels" state, repeating the same solution but always failing. Waiting longer is useless then. You should manually stop it and try a new approach. To judge whether Codex is spinning, look at the action log. If several rounds in a row are doing roughly the same thing, it is basically going in circles.

## 27. What if the task loses all movement while running

Do not panic. Handle it by case.

The most common case: Codex is really still running, just slow. Some tasks are inherently time-consuming, like installing a bunch of dependencies, running the full test suite, or processing large files. Open the thread and look at Codex's action log. If it is still advancing normally, it is a matter of waiting, do not interrupt.

Another case: Codex is waiting for you to approve something. In "request approval" mode, Codex stops at sensitive operations and waits for your confirmation, such as installing a new dependency, editing a certain file, or running a certain command. Here Codex is asking whether to let it continue, not stuck. Check whether the interface has a pending approval prompt. Handle it and Codex moves on.

Yet another case: Codex is truly stuck or spinning in place. The way to judge is the action log. If several rounds in a row repeat similar operations, keep reporting the same error, or simply have no action updates, then it is stuck. Waiting longer is useless then.

What if stuck. The most direct method is to manually stop, re-describe the task, or narrow its scope. You can also stop the thread directly, open a new one, reorganize the context, and give it to Codex again. If it is an environment problem (dependency will not install, network unreachable), pause the task first, clean up the environment, and let Codex continue after solving it.

When failures keep coming, stop. Do not let Codex try randomly forever. Codex sometimes falls into a death loop of "edit a version, run it, find it still wrong, edit another version," each extra round burning allowance, and most likely still failing in the end. Stopping in time beats waiting hard.

## 28. Where do I see the result after the task finishes

See the result in three places, each with its own use.

The middle dialog box is fastest. After Codex finishes it gives you a text summary of what it did, where it changed, and how it turned out. This is the quickest overview, but also the least trustworthy part. A text summary can gloss over things, and you must verify against other places.

What you really should look at is the right sidebar. If Codex edited code, the sidebar shows a diff where you can read line by line what Codex actually touched. If it generated a new file, the sidebar previews that file. If it made a web page, the sidebar opens it directly to see the effect. The sidebar is where Codex "hands in homework."

The most real is your project folder itself. All files Codex edited and all artifacts it generated ultimately land in the folder you picked when creating the project. Open Finder or File Explorer and go to that folder, everything is there. No matter how Codex writes the text summary, the real state of the folder cannot lie.

The standard acceptance flow is this: first scan the text summary to know the gist, then seriously read the diff to confirm the changes match expectations, then open the actual artifact (web page, file, image) to confirm the effect, and finally run your own test or verification flow. Only after these four steps can you say the task is truly done.

Never relax just from reading the text summary. After each completion, look at the diff first, then decide whether to accept. Text summary plus diff plus actual artifact plus your verification, none of the four checks can be omitted.

## 29. How exactly does the 5-hour rolling window work

This is the most confusing thing for Plus users. Get it wrong and you keep burning allowance for no reason.

First, the easiest point to misunderstand: the Plus 5-hour window is not about "how many messages you can send in 5 hours." It is about "how much reasoning compute you have in the 5-hour window." OpenAI's official docs say local messages and cloud tasks share one 5-hour window, and the allowance inside the window is counted by reasoning compute, not directly by message count.

Community measured data: Plus gets roughly 40 minutes of reasoning time per 5-hour window. The Pro 5x tier is about five times that number. Note this "40 minutes" means the task you run converted to reasoning compute, roughly equal to 40 minutes of reasoning consumption, unrelated to the wall-clock time you sit at the computer. A simple text edit may finish in seconds and consume almost nothing. A complex multi-file refactor may eat several minutes of reasoning allowance in one message.

This is why many feel "I sent few messages but the allowance is gone." The few you sent were heavy, each consuming a lot. Likewise, some feel "I sent quite a few and still have allowance" because they were all light.

There is also a "rolling" trap. The window does not "refresh on the hour every 5 hours." It is calculated rolling. The allowance you used 5 hours ago is only "released" back 5 hours later. So you will not feel a clear "refresh moment." The allowance recovers slowly.

On top of the 5-hour window there is also a weekly limit. Community members measured that reusing heavily for several days straight hits the ceiling. After hitting it you can only wait for next week to recover.

## 30. How do I check how much allowance is left

You can see it directly in Codex, no need to check the web.

Open Codex, find the allowance-view entry in settings, and you can see the current account's usage, how much is left, when it refreshes, and the rate-limit status. The entry is generally in the bottom-left settings, click to see the remaining usage. Once used up you can only wait for the next cycle to auto-refresh.

Why check often. Codex will not proactively remind you when you are about to run out. Codex only waits until you truly run out, then the next task you send errors out directly telling you the allowance is insufficient. This "sudden power cut" experience is terrible, especially when you are running a long task.

Build one habit: before opening a slightly larger task, glance at the allowance. If enough, run. If not, wait, or split the task smaller. This habit avoids more than half of "allowance anxiety."

If you use API Key billing (not the ordinary user's first choice), you check balance and consumption in the OpenAI Platform backend. If you connected a domestic model, check the balance in the corresponding vendor's backend. These non-subscription routes are more transparent in consumption, but also need you to watch actively, because pay-as-you-go that wanders really can blow up the bill.

One more detail: allowance recovery is not instant. Sometimes you see "1 hour to recover" and think it will be full at the mark, but recovery is gradual. Right after recovery the allowance is tiny, and heavy work still will not run. Leave some margin when scheduling tasks, do not use it right up to the edge.

## 31. Is the allowance gap between Plus and Pro large

Large, but most people do not need Pro.

Plus is twenty dollars a month and gives a reasoning allowance inside a 5-hour rolling window, enough for small tasks. Pro is much more expensive and gives several times Plus's allowance. Pro has a 5x tier (five times Plus) and even higher tiers. The numbers look scary, but the price is scary too. Pro 5x often has promotions where the allowance doubles again, but such promotions are temporary and revert after.

Who needs Pro. Only those who treat Codex as a productivity tool, use it heavily every day, and hit the Plus ceiling frequently. Ordinary people building web pages, editing files, running small tasks, Plus is completely enough. Going Pro is wasting money.

The simplest way to judge whether to upgrade Pro: first run Plus for a week or two and see if you hit the allowance wall frequently. If Plus's allowance is something you cannot finish even binding yourself to use it, then Pro is a waste. If every few days you have to rest because the allowance is insufficient, then Pro makes sense.

One hidden option: buy extra allowance. When Plus and Pro users run out, they can buy extra credits separately to keep using, without upgrading the plan. This fits people who "occasionally need a heavy burst once," more cost-effective than subscribing to Pro long term.

For China-based users there is a special money-saving route: connect domestic models. Through CC Switch connecting Zhipu, Kimi, DeepSeek, the monthly fee is far cheaper than Plus, and no VPN needed. This route is unofficial, with compatibility and stability risks, but for budget-sensitive people who want to keep using it, it is a real option.

## 32. Does the task stop immediately when the allowance burns out

It will not stop immediately, but it will stop.

Allowance checks usually happen at task start or certain key nodes. The task you are running will most likely finish its current round, then when you launch the next task, or when Codex is about to enter the next execution round, it errors telling you the allowance is insufficient.

This means two things. First, do not worry too much about a running task being cut in half. It will most likely finish the current stage. Second, you cannot count on "just using the last drop of allowance to finish the task," because the timing of allowance exhaustion is out of your control. It may jam right in the middle of your task.

More troublesome are background tasks. You open a task without watching, close the browser to do something else, and the task keeps running and consuming in the background. When you come back you find the allowance burned out long ago, and the task may hang half-done, neither finished nor without losing allowance. This "invisible consumption" is one of the main reasons Plus users burn out early.

How to avoid it. Before running a long task, check the allowance and estimate whether it is enough. If unsure, split it into small segments and glance at the remaining allowance after each segment. Do not open several background tasks at once, because consumption stacks and burns especially fast.

If a task really runs out of allowance halfway, do not force a restart. Let Codex stop there, wait for some allowance to recover, then decide whether to continue or restart. Forcing the tiny remaining allowance to continue a task needing heavy consumption often fails to finish and just wastes.

## 33. Can I use Codex on my phone

Codex itself is desktop-side. What you use on the phone is another thing, the Codex feature inside ChatGPT's mobile app.

The two have different abilities. Codex runs on your computer, can read local files, control your desktop apps, and use the local environment. The Codex inside the mobile app goes through the cloud, and what it can do is closer to Codex Web. It handles GitHub projects and runs cloud tasks, but cannot touch the local files on your computer.

The mobile side does have one especially practical scenario: continuing and remote control. In May 2026 OpenAI specifically updated so ChatGPT's mobile version can directly launch Codex tasks, including Codex tasks running on Windows. You open a long task on your computer, go out, and check progress on the road from your phone. When Codex has a question for you, you reply directly on the phone, approve Codex's next step, or assign a new direction. Your computer's local environment works quietly there, and you are free to move.

The experience is: the task runs on your computer, but your freedom is not limited. The mobile version and desktop side fully sync all past sessions, far more stable than ChatGPT's mobile version alone.

So the answer is: the phone cannot run Codex itself, but you can use the phone to keep participating in tasks launched on Codex. This is especially useful for long and background tasks. If you just want to ask small questions anytime, the phone-side Codex also works, only its ability is a notch weaker than the desktop version, after all it cannot touch your computer's things.

## 34. Does the task keep running after I close Codex

It depends on the case, on which kind of task you are running.

If you are running a local task (Local mode or Worktree mode), the task directly depends on the Codex process on your computer. You fully quit Codex (note fully quit, not minimized), and the task stops. This is the trait of local tasks: the task runs on your machine, and if the machine or Codex is off, the task is gone.

Here is a trap: many think closing the window is quitting Codex, but Codex defaults to minimizing to the system tray (Windows) or menu bar (Mac), and Codex is still running in the background. You think it is closed, but it is not. The task keeps going and the allowance keeps burning. To truly quit, right-click the tray icon and select Quit, or select exit in the menu bar.

If you are running a cloud task (Cloud mode), it is different. The cloud task runs on OpenAI's servers. Your computer shutting down or Codex quitting does not affect it, and the task keeps advancing in the cloud. This is the biggest value of cloud mode: it does not depend on your machine being online.

So to judge "does the task keep running after closing Codex," first see which mode you are running. Local mode, closing Codex equals stopping the task. Cloud mode, closing Codex the task continues. If unsure, the safest practice: use cloud mode for long tasks or when leaving the computer. Use local mode for daily short tasks, quit when done.

Build a habit: fully quit Codex when not using it, do not let Codex minimize and secretly consume in the background. Especially for Plus users, allowance is precious, and being silently burned by background tasks is the most losing.

## 35. Are Codex Credits worth buying

Depends on your usage. Two kinds of people.

One kind: normally Plus allowance is enough, only occasionally need a heavy burst for a few days. This kind is worth buying credits. Plus's monthly allowance is fixed, and overage can only wait for next month. If you have a big project to rush this month, buy some credits to tide over, far more cost-effective than upgrading to Pro for those few days. Stop when used up, return to Plus rhythm next month, flexible.

The other kind: almost every month uses up Plus allowance and often gets stuck by allowance. This kind should not buy credits, should upgrade Pro. If you supplement with credits every month, accumulated it may be more expensive than Pro, and the experience is intermittent. Once allowance cuts, the task stops, and after buying credits you must reconnect context, low efficiency. In this case go straight to Pro, the allowance pool is large, continuous work does not jam, more worry-free long term.

To judge which kind you are, running one or two months tells you. If you find yourself buying credits this month, then next month, then two or three months straight, that is the signal to upgrade Pro. If it is only occasional demand, credits are the most flexible supplement.

One hidden cost to calculate: after buying credits, psychologically you easily "let loose," and what should have been saved also gets spent freely, so credits burn fast too. Before buying, ask yourself whether there is really that much work, or just using more casually. The former is worth it, the latter is burning money for nothing.
