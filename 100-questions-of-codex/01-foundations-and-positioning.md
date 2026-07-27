# Chapter 1 · Foundations and Positioning

## 1. What exactly is Codex

Many people hear "Codex" for the first time and assume it is just ChatGPT with a new name, built specifically for writing code. That understanding misses the mark by a wide margin.

Codex is an AI agent made by OpenAI. Its core ability is to walk into a project, take a clearly defined task from start to finish, and hand back a result you can actually accept and verify. You give Codex a task. Codex reads your files on its own, edits them, runs them, watches the errors, and goes back for another round. When it passes, it shows you the result. The whole process feels like watching a remote colleague operate inside your project. It thinks, it experiments, it backtracks and corrects.

The biggest difference from ordinary chat is whether it touches anything. In ordinary chat you say one thing and it returns a block of code. You copy it, run it, fix it yourself. The AI only talks. Codex actually executes. What Codex gives you is a result that has been run and verified, a piece of output you can use directly.

This point matters, because every later question about why it is slow, why it burns your allowance, or why it sometimes wanders off traces back to one fact. Codex is really working, not guessing. Once you grasp those two words, "it works," what Codex is becomes clear. Codex is an AI assistant that enters your project site and does the actual work of getting things done.

## 2. What forms does Codex come in, and which should an ordinary person use

This is where beginners get most confused, because Codex now exists in four forms at once, each with a completely different purpose.

The desktop app is OpenAI's official graphical client. At first there was only a macOS version. The Windows version shipped on March 4, 2026, and now both platforms can install it. You open a full application window, with a task list on the left, the conversation in the middle, and results on the right. Codex can read local files on your computer, control your desktop apps, and has a built-in browser. It is the most complete form and the friendliest to ordinary users.

The CLI version runs in the terminal with no graphical interface. Wherever you type `codex`, that is where Codex works. People who know the command line like it because it is light, fast, and pairs cleanly with git and shell.

The IDE extension installs into editors like VS Code and Cursor, for programmers to use while they write code.

Codex Web / Cloud runs in the cloud, focused on GitHub projects, and opens a PR for you when it is done. Codex runs on OpenAI's servers, so it keeps working even after you shut your computer down.

Among the four forms, ordinary users, beginners, and non-coders should pick the desktop app. It has a graphical interface, needs no commands, and is the most complete. Unless this book mentions another form specifically, everything from here on refers to the desktop Codex by default.

## 3. How is Codex different from asking ChatGPT for code

The difference is not intelligence. It is whether it touches anything.

In a normal chat box you ask why a piece of code errors out. The model reads the context and returns an analysis plus a revised block. Whether it is right and whether it runs is entirely on you to verify. The model itself does not know what the code would do when executed, because it never executed anything.

Codex takes a different path. After receiving a task, it first translates your request into a sequence of actions: which files to read, where to edit, what dependencies to install, what tests to run. Then it executes step by step, checks the result at each step, and sees whether it actually worked. If it worked, it moves on. If not, it goes back and edits again. This loop may run several rounds.

The concrete difference shows up fast. In normal chat you often meet the moment where the code looked right but errored the instant you pasted it. What Codex gives you has at least passed inside Codex's own environment. Codex also edits the other files involved along the way, something normal chat cannot do with that kind of coherence.

There is a cost too. Normal chat replies in seconds. Codex has to set up an environment and experiment, so a task taking anywhere from a few minutes to tens of minutes is normal. What you trade waiting time for is the credibility of the result.

## 4. What is the difference between desktop Codex and CLI Codex

They share the same underlying capability, but usage and the barrier to entry differ a lot.

The CLI has no interface. You open a terminal and type commands to interact with Codex. The upside is that it is light, fast, and pairs smoothly with git, shell scripts, and automation flows. Programmers who know the command line use it like a fish in water. The downside is the high barrier. You must know how to open a terminal, type commands, and read the logs it spits out. People who never touch the command line will suffer.

The desktop app is a graphical interface. You open a complete application window. On the left you see all tasks, in the middle you type to talk, on the right you directly see the files, web pages, and code changes Codex produces. Codex can read local folders, control your desktop apps, and the built-in browser lets you see the effect directly. Almost every command you would type in the CLI can be clicked or spoken in the desktop app.

For ordinary people and beginners, the desktop app is friendlier on nearly every dimension. You do not memorize commands, you see what is happening, and the result sits right in front of you. The desktop app is far easier to pick up than the CLI, and fits ordinary usage habits.

So the conclusion is simple. If you know the command line and like the terminal feel, the CLI suits you. If you are not a programmer, or simply do not want to mess with the command line, use the desktop app directly.

## 5. Can I use Codex without a code repository

Yes, and this is one of Codex's biggest advantages over the cloud version.

The most natural use of cloud Codex is to connect a GitHub repository. After authorization, Codex pulls the code, makes changes, and opens a PR. Without a GitHub project, the cloud version feels awkward, because the cloud version is built around repositories.

Codex does not depend on GitHub at all. Codex's concept of a "project" is just an ordinary folder on your computer. When you create a project, you let Codex pick a folder. After that, every file in that folder, Codex can read, write, and edit. Whether the folder contains code, whether it is a git repository, whether it gets pushed to GitHub, none of that affects Codex's work.

This means you can use Codex for all kinds of things that have nothing to do with a "code repository." Hand Codex a folder of medical checkup PDFs and let it analyze them. Hand Codex a folder of raw footage and let it help cut a video. Hand Codex an empty folder and let it build you a web page from scratch. None of this needs GitHub.

The one thing to watch is which folder you pick. Never pick messy places like the desktop, downloads, or system directories, and avoid Chinese paths or paths with spaces. Make a clean working folder specifically, and treat it as your dedicated workspace.

## 6. Do I need to buy a subscription before using Codex

It depends on how deep you want to go. Free allowance lets you try, but doing real work basically requires a subscription.

A free account gets a fairly restrained allowance, roughly enough to feel "oh, so this is what an agent is," and it runs dry after one or two decent tasks. If you want Codex as a daily tool, you cannot avoid the ChatGPT Plus tier, twenty dollars a month.

Plus gives you an allowance inside a rolling five-hour window, enough for work equivalent to tens of minutes of reasoning. Small tasks are fine, but a few large ones hit the ceiling. On top of the five-hour window there is also a weekly limit, and hammering it for several days straight will hit the cap. The Pro tier is more expensive but far more generous, and only heavy users need to consider it.

There is also a very practical option for China-based users. Codex does not have to use OpenAI's official allowance. Codex supports connecting domestic models. Through a tool called CC Switch, you can plug in Zhipu GLM, Kimi, DeepSeek, and other domestic vendors. The price is much lower, and you do not need a VPN. Many people run domestic models day to day.

So the threshold looks like this. Just want to test the waters, a free account is enough for a spin. Want to use it seriously, either buy Plus or route through a domestic model. The path of spending nothing at all while still working continuously basically does not work.

## 7. Can Codex touch other files on my computer

It can, but there is a boundary, and you set it.

Codex has a permission system called Sandbox, with three tiers. The first tier is read-only. Codex can only look at files in your project, not change anything. The second tier is project read-write. Codex can edit files in your current project folder, but cannot leave that folder. The third tier is fully open, and Codex can touch the entire computer. For daily use the second tier is recommended. Beginners should not touch the third.

What does this mean? As long as you keep your project inside a dedicated working folder, what Codex can edit is only the stuff in that folder. Files elsewhere on your computer are off limits to Codex. Your WeChat, email, system config, and other projects' code are, by default, outside Codex's boundary.

But Codex has one ability that breaks this boundary, called Computer Use. With this feature on, Codex can look at your screen like a person, click buttons, and operate desktop apps you have authorized. This ability is powerful and needs more caution. For operations involving payments, accounts, or deleting data, it is best not to let Codex touch them. Close sensitive apps you are not using.

So the answer is: by default Codex is locked inside the project folder you gave it. For Codex to reach beyond its hands into other apps, you have to actively turn on the permission and actively authorize it. The switch is always in your hands.

## 8. Is Codex a chat tool or a programming tool

Strictly it is an agent, sitting between a tool and a tool-person. In form Codex wears a chat shell, but what it does is real work.

A chat tool's trait is that it ends when the conversation ends. You say one thing, Codex replies one thing, done. A programming tool's trait is that you give Codex a task and Codex gives you an artifact. Codex touches both, and is fully neither.

Codex has a chat shell. You talk to Codex in a dialog box, describe tasks, give feedback, tell it to change. But the work Codex does is more like a tool. Codex really edits files, runs code, controls apps, and delivers a verifiable result. In between, Codex thinks, decides, and experiments on its own, which feels like collaborating with a colleague.

OpenAI's own positioning is getting clearer: ChatGPT is the entry point, Codex is the execution layer. You hand the task in through conversation, but the task truly lands in the Codex execution layer. Inside OpenAI, Codex has largely already replaced ChatGPT for engineering work.

The practical impact on you: do not use Codex with chat expectations. In chat you can ask anything, stop anytime, no pressure. With Codex you need task awareness. Every conversation burns allowance, and every task needs an acceptance standard, or you are just burning money.

## 9. Why do some people praise Codex and others complain it is hard to use

There is no standard answer, but one variable is critical: what the user treats Codex as.

The loudest complainers are often people who use Codex as a beefed-up ChatGPT. They drop in a vague requirement and wait for Codex to snap back a perfect result like a conversation would. After waiting a few minutes they get something half-done, missing requirements or edited off track, and naturally feel it is hard to use. The gap between this kind of user's expectation and how Codex actually works is an entire "how to use an agent" awareness.

The loudest praise usually comes from people who can write requirements, break tasks down, and watch the process. They know an agent needs clear input, know big tasks must be split, and know to stop and restart when it wanders. The same Codex in their hands produces stable usable results, so naturally they like it.

Beyond usage, Codex itself does have version fluctuations. The community frequently sees feedback like "it got harder to use lately" or "last week it was fine, this week it won't run." Behind this is the impact of model versions and system updates. After GPT-5.5 shipped, quite a few people reported long tasks degrading and wandering more easily. This fluctuation is real.

Half is a usage problem, half is the product still tuning itself. Those who know how to use it treat it as a treasure, those who do not treat it as a trap, and neither side is entirely wrong.

## 10. Is Codex better at writing from scratch or editing existing code

Editing existing code is far steadier than writing from scratch.

This conclusion may be counterintuitive, because many people feel "writing from scratch is more free, the AI can play however it wants." But the way Codex works means Codex needs context, not more freedom.

When editing existing code, Codex can read the project structure, naming conventions, dependencies, existing tests, and config files. When editing, Codex has a frame of reference. It knows where to change and how to change so it matches the existing code style, and after editing it can run the existing tests to verify. In this scenario Codex's output quality is high, often making you feel "I would have written this change about the same way myself."

Writing from scratch is a completely different situation. You give only a requirement description, with no existing code as an anchor. Codex has to decide the project structure, tech stack, and file organization on its own. Every decision may differ from what you had in mind, and Codex cannot read your mind. The result is often a complete version of code where the tech stack, directory structure, and style are all Codex's own choices, far from your expectation.

So if you want Codex to start a project from zero, the best method is to manually build a minimal skeleton first, even just an empty directory structure plus a README, and let Codex continue writing on that skeleton. Give Codex an anchor and Codex is steady. Let Codex play from nothing and Codex drifts.

## 11. What do ordinary users most overestimate about Codex

What they most overestimate is Codex's "autonomy."

Many people open Codex with an expectation: I drop the requirement, Codex finishes it start to finish on its own, and hands me something usable. This expectation usually comes from demo videos and marketing copy, which show the pretty result after the task passes, with all the repeated adjustments, stop-and-restart, and supplemental explanations cut out.

The real experience is this. Codex can indeed complete many actions autonomously, but how well it completes them depends extremely on how clear the input you gave is. Drop in a vague requirement and Codex runs forward on its own understanding. What comes out is often a step away from what you wanted. You think Codex is "autonomous," but actually Codex is being autonomous on its own guesses, and those guesses are often off your wavelength.

People who truly use it smoothly never treat Codex as a black box they "drop and forget." They break tasks fine, state acceptance standards clearly, interrupt and restart when it wanders, and review the result carefully when done. They trust Codex's execution, but do not let Codex roam free.

The direct cost of overestimating autonomy is allowance. You drop a vague big requirement, and while Codex guesses on its own it runs many rounds and tries many directions, each extra round real money. In the end you get something still not quite right, and you have lost allowance and still need rework.

## 12. What kind of work should not be handed to Codex

A few kinds of work, handed over, are basically a waste of time or money.

If you cannot even state the requirement clearly yourself, do not drop it on Codex. If what you want is still a fog in your head, just a general feeling, Codex cannot think the requirement clear for you. Codex will only run forward on its own foggy understanding, the result is probably wrong, and you will spend several more rounds correcting it. Better to think it through yourself first.

Work whose right-or-wrong cannot be verified also cannot use Codex's strength. Codex is strong because it can execute and verify. If after something is done there is no objective standard to judge "did it work or not," then Codex's execution ability is useless. Things like "help me think of a few product directions" or "help me evaluate whether this design is good" are subjective judgment tasks where ordinary chat is enough.

Work that strongly depends on your local sensitive environment or real accounts, especially anything involving money, carries too much risk. Letting Codex operate payments, log into bank accounts, or change production databases, if something goes wrong there is no way to recover. Operations involving payments, account settings, and deleting data are best kept away from Codex.

Work you cannot understand or verify at all, Codex can give you a result, but if you cannot even judge whether the result is right, that result is useless to you. Either accept it wholesale, which is risky, or check it line by line, which is more tiring than doing it yourself.

## 13. Can someone who does not know programming use Codex

Yes, and this is exactly one of the biggest points of Codex over the CLI.

The CLI Codex assumes you can use the terminal, read logs, and handle errors. For people who never touch code the barrier is high. Codex wraps all that into a graphical interface. You type a description of the need, Codex executes, and the result shows directly in the right-hand window. The whole interaction is more like talking to a tech-savvy colleague than operating a development tool.

Plenty of real non-programmer scenarios with Codex already work. E-commerce sellers use Codex to cut videos and break down hit products. Content people use Codex to write articles, make covers, and build PPTs. Ordinary employees use Codex to analyze medical checkups, clean disks, and reconcile accounts. None of this needs programming knowledge, as long as you state clearly what you want Codex to do.

But "non-programmers can use it" does not mean "you need to understand nothing." You still need to know a few things: how to give Codex a clear task, how to accept Codex's result, when to call a stop, and which operations are risky. These belong to common sense about using an agent, and have nothing to do with programming knowledge.

One sentence summary: Codex drops the programming barrier to zero, but leaves the "knowing how to use an agent" barrier right there. Codex solved the former for you, but you still have to cross the latter yourself.

## 14. What is the one thing to get clear before using Codex

First get clear on whether, once your task is done, you can verify "good or not" yourself.

This sounds simple, but it is the watershed of whether using Codex goes smoothly. Many people use it poorly because the root is here: they throw the task out, wait for the result, and when it comes back they do not know if it is good. They can only say vaguely "seems okay." Under this usage, whether Codex's result is good is pure luck.

Why this matters so much. Codex's entire working mode is to run the "edit, run, see result, edit again" loop for you, and finally hand you a version that passed inside Codex's environment. What Codex can guarantee is "it ran through inside Codex's environment," but not "this thing actually solves your problem." The gap between the two can only be filled by you.

If after getting the result you can clearly judge "this is right" or "this is still wrong," using Codex is smooth. Right, use it directly. Wrong, tell Codex where and let it edit again. If you cannot judge, you can only accept it wholesale or check line by line, and both are tiring.

So before using it, ask yourself first: when this is done, how will I know it worked? Having tests to run, clear expected behavior, references to compare against, all of these help you verify. If you yourself do not know what "done" looks like, do not rush to start. Think the acceptance standard clear first.

## 15. Will Codex replace my manual work

Short answer: it changes how you work, it does not let you do nothing.

Codex is good at executing one clear, verifiable task to completion. You give clear input, Codex gives a passing result. This part of the labor, the repetitive, patterned, trial-and-error kind, does get taken over by Codex. After using it, many things you no longer want to do by hand.

But what Codex cannot replace is judgment. Which task to hand to Codex, whether the task description is clear, whether the result is right, whether to accept it, where to go next, all these judgments sit on you. The more capable Codex is, the heavier your judgment weight becomes, because every execution of Codex burns allowance and every edit affects the project.

Another thing Codex cannot replace is your understanding of the work itself. If you completely do not understand a thing and drop it to Codex, Codex gives you a result you cannot accept, then that work is still not truly done for you. The most comfortable use of Codex is when you understand the thing well enough to let Codex carry the execution part, while you focus on judgment and decision.

So a more realistic expectation is: Codex will slowly turn you from a "person who does the work by hand" into a "person who states needs, accepts results, and makes decisions." In this process you do less work, but you think more. Whether that counts as replacement depends on the angle you look from.
