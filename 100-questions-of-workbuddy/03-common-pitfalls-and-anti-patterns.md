# Chapter 3 · Common Pitfalls and Anti-Patterns

## 34. Why does a Workspace not cleaned up at the start almost certainly cause trouble later?

Because what the Workspace decides was never about looks; it really decides what materials this task can touch by default and where the result will land. If you start without cleaning it up, you hand it a mix of context, history files, old results, and irrelevant materials. It looks like a small problem at first, but once the task starts reading directories, referencing old files, and generating multiple versions, it amplifies step by step. Many failures are not one step suddenly wrong; the problem is often that the site was dirty from the start. The more WorkBuddy acts like a real executor, the more it depends on a clear site. An uncleaned Workspace, even if the result looks right, leaves you unable to truly relax.

## 35. When Ask is taking stock of the site, which abnormal signals should you watch most?

The three types of signals to watch most. The first is vague scope, such as these files, that directory, recent data; the speaker thinks it is clear, but the system is not. The second is excessive permission, such as allowing batch organizing, overwriting, and archiving before the task is even clear. The third is goal swing, now wanting a report, then wanting spreadsheets and PPT, with no priority set. The most valuable part of the Ask stage is digging out these fuzzy points in advance. If you see such signals and keep going, the later problem is not just speed; it will execute very seriously on a wrong premise.

## 36. Why should you brake immediately once Plan shows "overwrite the original file"?

Because it means the task has moved from generating new results to modifying original assets. The risk levels are not the same at all. A new file, if unsatisfying, can just be deleted and redone; overwriting the original means the old version may vanish directly, and much context goes with it. The more troublesome part is that users often assume by default it will handle it carefully, but the system sees an allowed action. Once such wording appears in Plan, you should at least clarify backup, version naming, target files, and the allowed edit range first. Solve with a new copy when you can; avoid direct overwrite. Braking is not being conservative; it leaves you a way back.

## 37. Why does letting it fill missing data on its own often plants a mine in advance?

Because filling sounds like helping, but actually it makes key assumptions for you. Whenever there is a hole in the data, it must guess: should this value carry over from last period, fill by average, estimate by common sense, or simply drop it. If you are not clear, it picks the way that looks most able to continue. The problem is, once this choice enters later charts, conclusions, and judgments, the whole chain is dragged off. Many end up feeling the report reads smoothly but some numbers are weird; the root is here. The most stable way with missing data was never default fill; it should be marked first, then decide how to handle. Seeing the blank is safer than confidently filling it wrong.

## 38. When the result looks very much like the real thing, what danger signal do you most easily miss?

What you most easily miss is that it has formed a complete surface, so you stop chasing the underlying basis. Neat layout, decent titles, charts present, people easily assume it is reliable. But the truly dangerous signals hide inside, such as unexplained caliber, unclear citation relations, charts not matching the text conclusion, and some key numbers with no source. The more mature the appearance, the more it fools the first review. The thing a tool like WorkBuddy most needs to guard against was never obvious nonsense; the trouble is it makes something ninety percent like real, making you skip that last ten percent. What newcomers should practice is not picking writing style; they should first practice finding basis, source, and formula.

## 39. Why does making a weekly report and PPT not equal a reliable conclusion?

Because weekly reports and PPT lean toward display, not verification. They are good at compressing information into something more like a conclusion, but this step also most easily smooths away the hesitation and exceptions in the raw data. What you see is page after page of neat narrative; what it often sees is just organizing existing material into a more finished form. But being showable is not the same as withstanding questioning. Especially for consolidation tasks, as long as the source data caliber differs, the time range is inaccurate, or the sample is incomplete, the final weekly report and PPT may be just well-packaged half-finished products. The truly stable order should be reviewing the underlying data first, then the display logic. Trusting the layout first easily backfires.

## 40. Why are empty values in spreadsheets the easiest to be handled wrong?

Because an empty value in a spreadsheet never means just one thing. It could be truly none, not yet filled, field not applicable, missed by the system, or just format lost. But when the model sees a blank, it naturally tends to treat it as a gap needing further processing, not a signal to be judged. So sometimes it skips, sometimes fills zero, sometimes guesses the most likely explanation by context. The error is right here: the most inconspicuous blank in a spreadsheet often hides a business definition problem behind it. If you do not state it clearly first, later sorting, consolidation, proportion, and trend may all drift. Empty values are not a small issue; they are the most underestimated bomb in spreadsheet tasks.

## 41. Once month-over-month, year-over-year, and statistical caliber get messy, which judgments get dragged off first?

Usually trend judgment and priority judgment get dragged off first. Month-over-month looks at short-term change, year-over-year looks at cycle position, and statistical caliber decides whether what you compare is even the same kind of thing. If any one of these three is messy, later words like growth, decline, anomaly, and recovery may not hold. The more troublesome part is that such errors disguise well, because the numbers themselves need not be fake; only the comparison relation is wrong. Once you continue to do resource allocation, problem attribution, and action suggestions on a wrong caliber, the whole judgment chain feels smooth but the direction may be completely wrong. For an Agent, calculating is not hard; confirming what you are actually comparing is the real difficulty.

## 42. Why does saying "redo it" more often make the result worse and worse?

Because such words sound like a reset but actually easily re-blur the original fuzzy points. It does not know whether you want to completely overturn the structure or are just dissatisfied with a few sections; it does not know which content can be kept and which must be dropped. So each redo, it may re-assemble a version among old understanding, new guesses, and existing results. After a few rounds, drift appears. A better phrasing usually should not be "redo it"; it should clearly state what is wrong, which part to keep, which part to recalculate, and whether the output format stays. Fix local problems locally; full restarts again and again make it harder to hold quality.

## 43. How do you phrase a local edit without destroying the parts done right before?

The key is to state both what to change and what not to touch at the same time. Many only say "change this" but omit the second half, so the system must judge the edit range itself, and often rewrites adjacent structure, layout, even conclusions. A more stable phrasing usually includes four things at once: which page or paragraph to change, what to change to, which content stays unchanged, and where the output is still saved. You are drawing a local construction zone for it. Then it is more like repairing the product than re-understanding the whole task. For a result that already runs smoothly, the real fear is not that it cannot be changed, but that the change boundary is not drawn.

## 44. Why, once Connector permission is granted too wide, is it hard to trust it to act later?

Because once you do not know theoretically how much it can see and touch, every later execution carries a mental burden. The Connector was meant to reduce moving and switching, but if the permission scope is far larger than the task needs, what it brings is not just convenience but uncertainty. Especially for systems like email, knowledge base, and online docs, much content does not belong to the current task site. If you grant too wide, even if it makes no mistake this time, you will find it hard to fully relax next time it processes automatically. The best state is permission roughly aligned with the scenario: what it can read, write, and search, you know in your own mind. Being able to trust it to act is itself part of efficiency.

## 45. When giving instructions remotely from the phone, which confirmation gate do you most easily miss?

What you most easily miss is what action this sentence actually becomes once it lands on the computer side. Sending a message on the phone is light, easily creating the illusion of just casually handing it off. But what the Remote Assistant catches is not a chat vibe; it catches an executable task. Away from the computer, it is harder to see in time which directory it read, which Connector it used, where the result was written. Many giving remote instructions only confirm the goal, not the site and boundary. The gate to add is asking one more question in your head: if it starts right now, what would it touch? Ask that, and many over-broad instructions automatically rein in.

## 46. Why does the first successful automation run not mean the scheduled run will be stable?

Because the first successful run often happens while you are still watching it. Whether the directory is right, data is updated, the Connector is valid, the output format has small issues, you can see on the spot. But once it runs on schedule, the environment changes. Data may not have arrived, external service permission may have expired, file names may collide, even old files in the same directory may affect the result. The difficulty of automation was never whether it can run; the hard part is whether it can run stably unattended. First success only means the process has hope, not that it already meets long-run conditions.

## 47. Which batch file-organizing tasks most easily cause misclassification and mis-movement?

The most problematic are tasks whose rules look simple but are actually ambiguous in judgment. Such as dividing by theme, by purpose, by whether important; these words may be clear in your head, but when applied to file names, content, and directories, the boundary is not hard. Another high-risk scenario is many same-named files, many old versions, mixed formats; you think it will understand version relations, but it can only judge by visible clues. Once the criterion of a batch task is not hard, a few misjudgments amplify into whole-batch chaos. The most stable classification rules can usually be written as clear text, not relying on feeling.

## 48. Why does generating many versions without clear naming only make it messier?

Because once versions multiply, what is truly scarce is no longer the file itself; scarce is your grasp of the file relations. Which is the draft, which is the edited one, which is just a temporary export, which can be sent out, if this info does not enter the file name, after a few rounds you can only guess by memory. WorkBuddy is very good at generating results and easily leaves multiple products during iteration, so naming matters more than in the manual era. Unclear naming makes later editing, archiving, sharing, and automation relay harder. Version management looks like a small thing but actually protects your sense of control over the result chain. The more files, the less you can be lazy.

## 49. Why, once task steps get messy, is the result hard to trust for reuse even if produced?

Because reuse relies not on the vague thing of accidentally getting it right once; you need to know why it is right. When steps are messy, the result may happen to be usable, but you find it hard to judge whether next time with a different batch of materials, a different day's data, or a different colleague taking over, it will fail immediately. A truly reusable process has a relatively stable order, clear input, and explainable intermediate steps behind it. One of WorkBuddy's strengths is pushing tasks forward, but if the pushing process itself is chaotic, what you reuse is not a method but luck. Producing the result is only the first gate; whether it can be rerun with confidence decides whether it is a process.

## 50. When does an Expert Team turn from a helper into a source of more chaos?

When the task main line is already single but you force multiple roles in, the Expert Team easily turns from accelerator to noise source. Because its value is built on division of labor; if the task needs no division, the extra roles only bring more perspectives, more speech styles, more integration cost. Another common problem is the user also did not state the core goal clearly, yet expects the Expert Team to think together, so the lead splits enthusiastically but what comes back is more scattered. The Expert Team is most afraid of the scenario I do not know what I want either, but you think more. The more roles, the clearer the main line must be.

## 51. Why does installing too many messy Skills instead easier drag the task off?

Because with more Skills, the system has more paths to take during execution, and these paths need not all suit the current task. You think you are enhancing capability, but actually adding forks. Especially when several Skills touch writing documents, organizing materials, generating content, it more easily sways among closely bordered capabilities. The docs suggest enabling only the Skills the current task needs; this is not just for tidiness, but more practically to lower mis-call probability. For newcomers, narrowing the Skill pool first matters more than blind expansion. Only when you clearly know why you open this one and not another have you truly entered the stage of knowing how to use it.

## 52. When automation clearly has a target space but you cannot select it, where should you check first?

The first step usually should neither doubt the model nor rush to rebuild the task; you should first go back to the Workspace and data state itself. Automation demands a more stable directory than manual tasks; it needs a clearly visible, writable, persistently existing location. If the target space cannot be selected, common reasons are often that the Workspace was not saved correctly, the directory state changed, the current entry does not see the project you thought, or the system default-assigned a new automation Workspace. First check whether the space truly exists, whether it is in the current list, whether it is still in the right place; this beats blind retry. Many so-called cannot select are actually the site not aligned.

## 53. Why must the last pass of externally sending emails and publishing documents be done by a human?

Because once such actions are sent out, the cost of error is no longer just an internal rework. Email may go to the wrong recipient, documents may expose uncleaned content, small wording issues may become external risks. WorkBuddy is very suitable for helping you prepare these, even finishing most mechanical steps in advance, but the last move is still better done by a human. It may not be wrong, but the responsibility boundary of external actions is completely different from internal organizing. Leaving the last gate to a human separates high-consequence actions from the high-efficiency process. Let it run the front, do not skip the last move.
