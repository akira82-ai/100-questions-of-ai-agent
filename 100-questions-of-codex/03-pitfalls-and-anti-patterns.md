# Chapter 3 · Pitfalls and Anti-Patterns

## 36. Why did Codex suddenly start spinning its wheels

This is the most complained-about crash in the community. Almost everyone has met it.

The phenomenon: you give Codex a task, Codex starts working, errors out after a while, Codex edits a version and runs again, errors again, edits again, runs again. This loops several rounds, each round's error message roughly the same, but it just will not pass. You watch Codex spin, wait ten-plus minutes and it is still in place, allowance dropping fast.

Why does this happen. When an agent meets failure, Codex's strategy is "try a different approach." But sometimes the "new approach" Codex switches to is actually similar to the last one, or Codex simply does not realize it is repeating. Codex lacks the human metacognition of "I already tried this, this path is clearly blocked." The result is Codex stuck in the same dead end, hitting the wall over and over.

The community calls this "infinite random trying" or endless loop. On Reddit someone even opened a thread complaining that Codex suddenly became "almost unusable," with tasks turning into "endless loops, missed instructions, half-finished fixes."

What to do. Stop in time. When Codex spins, send this line directly:

> Stop for a moment. Summarize the current failure reason, do not keep editing files.

Let Codex stop and review. This helps far more than letting Codex keep trying hard. After the review, either switch to a completely different approach and restart, or narrow the task scope, or step in yourself to judge where the problem is. Letting Codex try endlessly will most likely still fail, but the allowance will definitely burn out.

Build a habit: watch Codex's action log. If you see two or three rounds in a row doing roughly the same thing and reporting roughly the same error, stop immediately. Do not wait.

## 37. The task ran for half an hour and gave me a half-finished product

This crash is more hidden and more annoying than spinning in place.

The phenomenon: the task runs smoothly, no errors, no spinning, looks like it keeps advancing. After twenty minutes, half an hour, you accept with full expectation, and the thing Codex gives you is only half done. Either the feature is not fully implemented, or some places are clearly not finished, or there is a half-written comment in the code, like Codex was unplugged midway.

Why. The most common is over-long context. In long tasks Codex reads many files and edits many places, and the conversation history piles longer and longer. Past a certain length Codex's attention scatters, and later details start leaking. Another reason is unclear task boundaries. What Codex understands as "done" differs from what you want. Codex feels "core feature done counts as done," but you feel "still need to handle edge cases, write tests, add docs."

The most insidious is another kind: Codex secretly "thinks it is done" midway. This is a known issue. Sometimes while a background task is still running, Codex drops you a "final answer" and ends the task early. You think Codex ran for half an hour, but it may have "decided" it was done at minute 15, and spent the rest doing something else.

How to avoid. Write the acceptance criteria into the task description, clearly stating "the standard for done is X, missing any one does not count," so Codex cannot clock out early. Long tasks must be split into small segments, accepted after each segment, do not let Codex run half an hour in one breath. Also, after finishing, do not only look at the line "completed" in Codex's text summary. Open the diff, look at the actual artifact, confirm how far it really got yourself.

## 38. I wrote it clearly, so why does Codex still miss instructions

This is the most crushing crash: you list the requirements clearly one by one, and Codex still misses a few.

You write "1. change A, 2. change B, 3. change C, 4. add tests, 5. do not touch D." Codex finishes, A and B changed, C missed, tests not added, and D got edited along the way. You go back to your description, clearly written, but Codex just does not do it all.

Why. When an agent processes long instructions, attention is not evenly distributed. The first few and last few Codex remembers firmly, the middle ones leak easily. Piled together, Codex tends to grab the few it "thinks most important" and do those first, ignoring the rest. The community feedback that Codex suddenly became "endless loops, missed instructions, half-finished fixes" points exactly at this missed-instructions part.

Another reason: the more instructions, the more Codex tends to "finish the quickly-doable ones first to show you," planning to come back for the rest, then forgets. Codex does not miss on purpose. Its working memory is only so big, and the middle few of a long list naturally get squeezed out.

How to cure this. There is some art to the arrangement: put important instructions at the start and end, secondary ones in the middle, do not pile them into one blob. Also restrain the instruction count. Four or five requirements per task is the ceiling, more than that split into two tasks. The most useful is plan mode, let Codex list the steps first, and you can see at a glance whether anything is missing, then confirm before executing. After finishing, do not forget to check your original requirements line by line, and have Codex fill any miss, do not accept by default.

The most effective is still plan mode. Let Codex produce a plan first. If the plan misses one of your requirements, you spot and add it immediately, ten times better than discovering the miss after Codex finishes.

## 39. Codex keeps editing and breaks good code too

This crash is called "drive-by refactoring," the number one anti-pattern.

The phenomenon: you ask Codex to change feature A. Codex finishes A, and on the way feels section B's code is "not elegant enough," so it refactors it for you. After refactoring B, it feels C's naming is not standard, so it changes the naming. After changing the naming, every place referencing C must change too, and D, E, F all move in a chain. You thought you asked Codex to change one place, look back and Codex changed over twenty files, half of which have nothing to do with your task.

Why Codex does this. An agent has an "optimization tendency." When Codex sees code, it instinctively feels "this could be better" and goes to change it. Codex does not distinguish "what you asked me to change" from "what I felt like changing on the way." In Codex's eyes both are edits. Many old projects have lint or type issues. When Codex feels some code is "not elegant enough" it refactors on the way, which may bring renaming causing reference errors, changing global styles affecting other pages, upgrading dependencies causing compatibility problems, even deleting code Codex thinks useless but is actually business logic.

The consequences are severe. Rename one component and every place referencing it must change, one wrong edit and it errors. Change global style and other pages' layout may break. The most insidious is deleting code. Codex feels "this is unused," but it is your business logic, and you will not know what broke.

How to defend. Write this fixed script into the task description or AGENTS.md:

> Only implement the current feature point this time.
> Do not refactor unrelated code on the way.
> Do not modify naming, directory structure, dependency versions, or global config.
> If you find code that could be optimized, record it as a suggestion first, do not modify directly.

This script blocks most drive-by refactoring. Add a harsher iron rule aimed specifically at deletion:

> Do not delete files you did not create. When you meet erroring code, fix it, do not delete it.

This one is especially important. When Codex meets an error it has a dangerous tendency: delete the erroring thing to remove the error, even if that thing has nothing to do with the current task. The community reported Codex deleting an unrelated module entirely during a small change, on the grounds that "it was erroring." Writing "forbid deleting files you did not create" into AGENTS.md blocks this most insidious crash.

Last line of defense: after each run look at the diff. If you find Codex edited files unrelated to the task, immediately have Codex roll back that part, do not accept by default.

## 40. Why does Codex take a huge detour for a simple need

You tell Codex "add a button on this page," sounds simple, and Codex finishes having changed over a dozen files, built three new modules, introduced two new dependencies, and fiddled for fifteen minutes. You look at the diff confused: I asked you to add a button, what are you doing.

This is another common agent ailment: over-engineering. On Reddit you often see feedback that Codex "over-complicates simple tasks," and even with detailed requirement docs Codex still twists simple classification and organization work into circles.

Why. The root is Codex has seen too many "good practices." The training data is full of design patterns, best practices, architecture thinking, so on any requirement Codex instinctively wants "to do it more professionally." Add a button. Codex feels it should be wrapped into a reusable component. Make a simple data display. Codex feels it should introduce state management. Codex is not deliberately messing up, it genuinely feels this is "better."

More troublesome: Codex will not proactively ask you "want it simpler." It defaults to you wanting a production-ready solution and builds to production standard. But often you only want a quick prototype, or a small change, with no need for that much fuss.

What to do. State your expectation clearly in the task description. Common script:

> Implement in the simplest way. Do not introduce new dependencies, do not add modules, do not do encapsulation beyond this requirement's scope.

Or:

> This is a prototype or demo, no production-grade architecture needed, just needs to run.

Saying "simple" explicitly cures most over-engineering. Also, when you see Codex finished with a bunch of file changes you did not expect, do not rush to accept. Ask Codex "why are these changes needed, can they be simplified." In most cases Codex can converge to a smaller change scope.

## 41. Are background tasks secretly burning my allowance

Very likely. This is the number one reason Plus users burn out early.

The phenomenon: you open a task, run it a while, feel bored or need to do something else, close the browser or switch to another app. You think you are "not using it," but the task is still running in the background, consuming allowance every round. When you come back two hours later, you find a big chunk of allowance gone, and the task may still hang halfway.

This "invisible consumption" phenomenon does exist. There were reports that Codex's background process made users "hit the limit faster than expected." OpenAI's engineering lead acknowledged it was a problem at the time and was fixing it. But as of now, the fact that background tasks consume allowance has not changed, only the interface prompts became a bit more obvious.

More insidious is another case: you open a thread, run a task, the task finishes, and you think this thread "stopped." But if you turned on automation or some continuously running task, it may keep consuming where you cannot see.

How to avoid. Build a few habits. The most critical: fully quit Codex when not using it. Note really quit, not minimize. On Windows go to the tray icon and right-click to quit. On Mac quit from the menu bar. Codex minimized to the background is still running and still dropping allowance. Also, glance at the allowance before a long task and estimate whether it can last to the end. Check allowance regularly, and if it drops faster than expected, investigate whether a background task is sneaking.

One mindset to correct: Codex has no "open costs money, closed is free" deal. As long as Codex is alive and a task is running, it is spending. Closing it completely when not using is the simplest and most effective way to save.

## 42. Why does allowance still drop after I close the window

This is another pain of Q34 "does the task keep running after I close Codex": you think you closed it, but you did not.

Codex's default behavior is to minimize to the system tray (Windows) or menu bar (Mac), not truly quit. You click the X at the top-right, the window disappears, you think Codex is closed, but Codex is still alive in the background. Background-alive Codex, if you left a task unfinished, that task keeps running and consuming allowance.

Many burn money this way: open a task, get impatient waiting, X the window to do something else, thinking "I closed it so it should not burn." Next day find the allowance gone and the task ran into a mess hanging halfway. One such loss is enough to hurt.

The way to tell "close window" from "quit Codex." On Windows, clicking X only closes the window. You must find the Codex icon in the bottom-right system tray, right-click and select Quit, that is the real quit. On Mac, clicking the red dot closes the window, but you must select "Quit Codex" in the menu bar or press Command+Q for the real quit. Build a judging habit: every time you want to close, ask yourself "did I close the window or quit the program." The difference between these two actions is huge.

If you truly want a long task to keep running in the background, go back to Q34 for the difference between local and cloud modes. Only cloud mode achieves "task continues after computer off," local mode cannot.

## 43. Why did my opened task vanish with no result

This crash is especially infuriating: you open a task, run it a while, look back, the task is gone, no result, no error, as if it never existed.

A few possibilities. The most common is the task got terminated unexpectedly, that known issue where Codex drops a "final answer" while the background task is still running, ending itself. You think Codex is still running, but it "decided" long ago it was done and quietly exited.

It could also be Codex crashed or got killed by the system. Local tasks depend on the Codex process, and when Codex goes down the task goes with it. If your computer is memory-tight, the system is cleaning processes, or Codex itself bug-crashed, the running task disappears together, too fast to save even intermediate results.

Another type is the environment dropping: login expired, network disconnected, cannot reach the server, the task may cut off directly with no recovery mechanism. Last is allowance running out, hitting insufficient halfway and stopping directly. This usually prompts, but sometimes the prompt is not obvious, and you think the task "vanished."

How to reduce this. Run important long tasks in cloud mode, not depending on the local Codex process, so Codex crashing does not affect it. After a task finishes, accept immediately and save the result to the project folder, do not let Codex stay in the "only in conversation" state. Keep login and network stable, reconnect immediately on drop. Also build the habit of watching the task list. If a task mysteriously vanishes, go through the action log and system notifications to see if there was an error.

## 44. Running the same task again gives a completely different result

This is an agent "feature," not a bug, but you must know it exists or you will be hurt.

Today you tell Codex "build a login page," Codex gives you version A. Tomorrow you send the exact same task again, Codex gives you completely different B. Both A and B run, but the style, structure, libraries used, even tech stack differ. You are confused: same task, why so different.

The reason is randomness in agent output. Each time Codex generates, there is some internal "sampling" component, and the same input can walk to different generation paths. Plus the model version may update, the context may differ slightly, Codex's "judgment" that round may differ, and the result is each run of the same task is not exactly the same.

The trouble this feature brings is concrete. Say you see a great result and want "run once more to see if there is a better one," but version two is much worse, and you cannot get back to version one (unless you saved early). Another is collaboration: you and a colleague run the same task separately and get results that do not match at all, and you cannot even discuss "which version to use."

The response is direct. Save good results immediately, do not think "run once more might be better." Copy the result to the project folder, commit to git, freeze it. To compare multiple plans, use the multi-plan preview feature and let Codex give you several plans to compare at once, far more reliable than running three times separately. For tasks with high reproducibility needs, write the task description extremely detailed, because the vaguer the description, the larger each run's difference. The more precise, the smaller.

Remember one line: agent output is "one-time." What runs out is gone if not saved. Do not expect Codex to "do it exactly again."

## 45. Why does Codex's plan not match my project

This crash often happens in the "paste code" scenario: you paste a piece of code to Codex to change, Codex gives you a version, you happily paste it back into the project, run it and get errors everywhere.

Why. Because Codex cannot see your project's full picture. What you paste is only that piece of code. Codex does not know what surrounds it, what it depends on, what it calls. When editing, Codex can only change by its understanding of "general code," which does not match the actual context of this code in your project. The result is Codex's changes fight with elsewhere in your project, reference errors, type errors, missing dependencies, all such problems.

If you do not use project mode and only paste code for Codex to change, the environment Codex verifies is one layer away from your real project, and the result's credibility discounts. This is why project mode is stressed: let Codex enter your project directory and read all your files, so when Codex edits it knows what surrounds it.

How to avoid this crash. Use project mode when you can, let Codex read your project's full picture, do not let Codex see only the piece you pasted. If you must paste code (the project is inconvenient to share), paste the related dependencies, imports, and context together, do not give a lonely isolated piece. After Codex edits, remember to actually run it in your project. Codex can give you code that "looks right," but whether it runs in your project, Codex itself does not know (because it never ran in your project).

The most fundamental is still project mode. Many Codex task failures are not because Codex cannot write code, but because Codex is asked to act before understanding the project. Let Codex read the project first, then act, and the crash rate drops sharply.

## 46. Codex says it fixed it, so why do I get errors everywhere on run

The root of this crash is: the environment Codex ran through is not the same environment you run in.

Codex ran through in the sandbox. That sandbox has dependencies Codex installed itself, Codex's own runtime, Codex's own assumed project structure. Codex "ran through" in that environment. You take Codex's code and put it in your real project, where your environment may differ: different dependency versions, different OS, different config, conflicts between other code and Codex's changes. The result is Codex says "ran through," but you get errors everywhere on run.

There is a real complaint: someone asked Codex to do a simple job, and Codex did not even identify what language the codebase uses, a simple task failed directly. This is typical "Codex started working before really entering your environment."

More troublesome: sometimes Codex did not really run at all, just "feels" it ran through. Codex finishes the code, looks at it and feels "this should be fine," then tells you "completed." You did not verify, took it to run, found it never ran.

How to cure. The key line: let Codex run in your project, do not let Codex talk to itself in its own sandbox. Use project mode, let Codex really enter your project directory, so what Codex runs through is your project's environment. After finishing, run it yourself again, do not fully trust Codex's "ran through." If there is an error, send the real error message straight back to Codex and let Codex see the scene, do not let Codex imagine. Also, if Codex keeps failing on the same kind of error, it is mostly the task description not clear enough, or the task beyond its ability, then consider splitting smaller or switching approach.

## 47. What signals say this task should be manually stopped

Stopping in time is the core skill for saving allowance and preventing crashes, more important than knowing how to start tasks.

A few clear signals, stop at any one. The most typical is spinning in place, several rounds of similar errors and similar attempts with no real progress. Waiting longer is useless, stop immediately.

File count also reveals problems. You ask Codex to change one feature, it changed over twenty files, clearly drive-by refactoring or wandering off. When you see the diff file count spike, pause and see what it is actually doing. More dangerous is Codex starting to delete large amounts of code. Unless you explicitly asked Codex to refactor or clean up, any code deletion warrants vigilance. Codex's "unused" code is often your business logic.

A few more signals matter equally. Codex introduced a new dependency, changed package.json, touched config files, you must ask "why is this needed." The task ran long with no completion and no clear progress, something that should finish in minutes dragging past ten minutes, is mostly a loop or stuck. Last is an especially fatal one: Codex's text summary does not match the actual diff. It says "modified the login logic" but the diff did not touch any login-related file. This say-one-thing-do-another case must be stopped immediately and clarified.

At any unease you can send this line:

> Stop for a moment. Summarize what you have done and what problem you met, do not keep editing files.

Let Codex stop and report. This saves more time and allowance than letting Codex keep trying. Remember one principle: rather stop and restart a few more times, do not let Codex run a wandering task for half an hour. The former wastes minutes, the latter wastes ten-plus minutes and a big chunk of allowance.

## 48. After a task fails, should I retry or change the requirement

These two responses differ greatly. Pick wrong and it gets worse.

First, when to retry. If the failure is sporadic, like network dropped, Codex crashed, some temporary error, just retry, no need to change the original task. This is environment or luck, and one more time will most likely succeed.

When to change the requirement. If the failure is "Codex tried several times and still cannot do it," then do not treat it as luck. The root is the task itself: maybe too big, description too vague, or beyond Codex's ability. In this case direct retry will most likely still fail, wasting allowance. The right move is stop, analyze why it failed, then adjust the task.

Adjusting the task commonly goes a few directions. The most used is split smaller, break a big task into a few small steps, one by one, each with high success rate. Then state the need clearly, make the vague parts concrete, make the acceptance criteria explicit. Also tighten the scope, do not let Codex "refactor the whole module," let Codex "only change this one function." If Codex keeps failing on the same approach, maybe that approach itself does not fit, then switch to a completely different direction.

One especially important habit: when failing, have Codex summarize the reason first, instead of continuing to try. Send "stop for a moment, summarize the current failure reason, do not keep editing files," and let Codex give you a failure analysis. This analysis helps you judge retry or change. If Codex says "network issue" or "temporary error," retry. If Codex says "the module this requirement involves is too complex" or "the depended API does not exist," then you must change the requirement.

The most taboo is "mindless retry." See failure and click rerun directly, changing nothing, most likely still fails, and a few consecutive failures burn out the allowance. Every failure, stop and think why first, then decide the next step.

## 49. Why does splitting a big task make it more likely to fail

This counterintuitive phenomenon has tricked many. You "reasonably" split a big task into a few small ones, thinking it is the steady approach, but each small task runs poorly, and connecting them is messier, worse than letting Codex do it whole at the start.

Why splitting makes it fail. The most common is wrong boundaries. You think A, B, C are three independent small tasks, but actually they couple. A's edit affects what B depends on, and B runs still based on A's pre-edit state, so B's change conflicts with A. This "split but not cleanly" is worse than not splitting.

Another trap is context loss. A big task run at once, Codex stays in the same context from start to end, remembering what it did before. Split into small tasks run separately, each is a "new start," Codex does not know what was done before, may repeat edits, may contradict before. Plus splitting too fine, Codex only stares at this small block doing each small task, cannot see the whole, so each block alone looks okay, but pieced together the style is inconsistent, the structure misaligned, even logic conflicts.

How to split right. The key principle is split by coupling degree, not by "feature module." Tightly coupled parts go in one task, do not force-split. After splitting, also give Codex the whole context: before each small task tell it "what was done before, what to do now, what still to do," so Codex has a whole sense. A steadier approach is use plan mode to plan the whole first, let Codex propose how to split, you see if its split is reasonable, more reliable than you force-splitting. Last, accept each segment after it finishes, adjust immediately if wrong, do not wait until all three small tasks finish to find the whole is messy.

Splitting itself is not wrong, what is wrong is "mechanical splitting." Those who can split make complex tasks simple, those who cannot make tasks that could work become undoable.

## 50. How to stop one task from dragging down the whole week's allowance

This is self-protection Plus users must learn, or one wandering task can leave you unable to use it for a week.

How the danger happens. You open a task that looks not too big, Codex runs and falls into a loop, each extra round burning allowance. You forget to watch Codex, go do something else, come back half an hour later and find a big chunk of allowance gone. You want to stop loss but are not willing, let Codex try once more, burn another wave. In the end the task failed, allowance nearly gone, and the remaining days you can only stare.

The avoidance method, the core is to set a stop-loss line for the task. Before opening, estimate cost first, look at task complexity, estimate roughly how many rounds and how much each consumes, have a number in mind. Then set a time cap for the task, like force-stop if no result after 10 minutes, do not wait mindlessly. Watching the action log is also key. If Codex is spinning, trial-erroring, failing repeatedly, stop immediately, do not count on it figuring out itself.

The other end is "split and save." Big tasks must split small, run in multiple times, glance at remaining allowance after each segment, continue if enough, wait if not. Small tasks use low reasoning intensity to save allowance. Before acting use plan mode to plan first, the planning phase consumes little, and if planning is right the execution phase is not wasted.

The third end is "monitor." Check allowance often, investigate immediately if it drops fast. Fully quit Codex when not using, do not let background tasks sneak. Run only one heavy task in the background at a time, multiple stack and consumption doubles.

The most fundamental mindset shift: do not treat Codex as a "drop in and wait for result" tool, treat it as a "needs you watching" tool. When Codex runs a task, you better watch nearby, intervene immediately if something is wrong. Tasks completely let go are either cloud mode (you are not afraid of Codex wandering) or routine tasks you already verified Codex can complete steadily. New tasks, complex tasks, must be watched.

## 51. Which basics do the people who crash most with Codex fail to do

After reading all these pitfalls, you will find the truly life-saving moves are just a few. The people who crash most in the community basically failed to hold these few bottom lines. Organized into a minimum-standard checklist, doing them blocks over eighty percent of disasters.

The most important line: before letting Codex act each time, save a version of your project first. If you use Git, commit once before letting Codex work. If you do not use Git, at least copy the whole project folder as a backup. If Codex edits it broken you can still reset, still checkout back. If Codex deletes key code you can still pull it from backup. Without this "undo key," letting Codex edit the project is like driving on the highway without a seat belt.

Another line: for any slightly larger change, run in Worktree mode. Worktree is like an independent scratch notebook for Codex, letting it boldly edit on the copy while your main project stays untouched. If it breaks, just throw away the copy, zero risk. Refactoring, adding features, uncertain-result attempts, all should use Worktree.

Another line: write in AGENTS.md the hard rule "forbid deleting files you did not create." When Codex meets erroring code, it tends to delete the erroring thing to remove the error, even if that thing has nothing to do with the current task. This iron rule blocks this most insidious behavior.

Then: do not let Codex run unsupervised big actions. Renaming, cleaning, large-scale refactoring, migration, these tasks are highest risk, most easily led astray by Codex's "optimization tendency," and must be watched throughout.

Last: small steps fast, check diff each step. Split big tasks into small, clearly bounded changes, and look at the diff immediately after each step finishes. This habit blocks most crashes before merge.

None of these is a deep technique, all are bottom-line operations. The people in the community who use Codex with great success did not master any secret weapon. They just did these few lines into their bones. Conversely, the most miserable crash cases in the community can almost all be traced to violating one of these lines.
