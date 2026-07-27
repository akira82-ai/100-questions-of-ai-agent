# Chapter 4 · Result Verification and Stability

## 54. How do you set a truly acceptable completion standard for WorkBuddy?

A truly acceptable standard states at least three things: what to generate, in what format, where to put it. For example, consolidate these three data sources this week into a weekly report, Word format, stored in the weekly report directory. The result area just gives you the reference: the artifact view shows whether the file was generated, the change view shows what it touched, the all-files view shows whether the result landed in the right directory. The more specific the standard, the less effort acceptance takes. A vague standard eventually becomes you opening the file and guessing again whether this counts as done.

## 55. Why, without an output path constraint, is it hard to confirm where it actually delivered?

Delivery must finally land as a concrete file. If you do not tell it where to store, it picks a place itself. When you turn back to accept, you do not know where that file is, and even seeing the artifact you find it hard to judge whether it landed right. The value of an output path constraint is giving you and it a shared expectation of where the result lives. Specifying a directory when issuing the task turns acceptance from hunting files into checking the path.

## 56. How do you ask it to report progress by stage, without chattering a bunch of nonsense while working?

Tie the report rhythm to the execution steps. Rather than let it report anytime, state clearly: do it in three steps: first inventory the data, then generate charts, then write the conclusion; after each step, tell me in one sentence before continuing. The conversation area already shows light hints like analyzing data, enough to see progress. What you really need to add is key checkpoints: after which step you want to stop and look at the intermediate result. The clearer the nodes, the more useful the report; a report with no nodes is mostly just noise.

## 57. How do you check that every conclusion in the generated report can trace back to the raw data?

The most direct way is to require it to carry the source when writing conclusions, such as annotate the corresponding data source, time range, or raw field after each key conclusion. Then when you get the report you can trace each conclusion back. The change view and all-files view in the result area also help you compare whether the raw data and processed result drifted. The docs specifically note that when data credibility is required, state in advance whether public sources and source links are needed. A report whose conclusions cannot trace back to raw data, however good-looking, is only a half-finished product.

## 58. Why is writing correlation as causation the most dangerous office illusion?

Correlation only says two things appear together; causation says one caused the other. The model is good at finding A rose and B also rose, but it does not naturally know whether the two have a causal chain. So the report may say because new users rose, conversion improved, which sounds reasonable but may just be the same external factor pushing both metrics up. The most dangerous part is that such a conclusion looks especially like it can guide action; you allocate resources by it and the direction may be wrong. When you meet causal phrasing, first ask back: is this proven by data, or just smoothed out by a sentence.

## 59. When a file cannot be read, should you check the material first or switch the model first?

By the order the docs give, switch the model first. The most common root cause of unreadable files is the current model not supporting this file type, not the file itself broken. To read images, scanned PDFs, complex Excel, you must switch to a model supporting image understanding or multimodal. If still fails after switching, then check whether the material is encrypted, damaged, or had its extension changed. Another easily missed point is not having the corresponding Skill installed; some document-processing capabilities come through the Skill market. The order is roughly: switch model first, then check plugins, then check material.

## 60. How do you use "to be confirmed" to keep risk on the table instead of hiding it in the product?

The practice is simple: clearly tell it that wherever it is unsure, cannot find basis, or can only guess, mark it out, do not fill in a seemingly real answer yourself. For example, require it to annotate with [to be confirmed] for data or judgments without clear source, and list what you still need me to provide. Then the risk points in the product are visible, not covered by a smooth paragraph. The permission system also provides similar protection: under default permission, sensitive operations and execution outside the Workspace both need your confirmation. At each layer you can set a to be confirmed gate.

## 61. Why must you check whether the file can be edited further, not just look at the preview?

The preview only proves this thing can be viewed, not that it can be edited. The result-area preview is handy; tables and documents can be glanced at for layout. But preview passing does not mean the file itself is an editable format. Sometimes it generates a screenshot, a web page, a locked PDF, all previewable, but hard for you to edit. A workflow that truly moves forward needs editable source files: Word where words can be changed, Excel where formulas can be changed, PPT where pages can be swapped. When accepting, besides the preview, best open the file itself to confirm the format is right and the content can keep moving.

## 62. How do you tell whether an automation task can basically be left to run on its own?

At least three conditions must be met. One, the process has run smoothly manually more than once, with stable input and output. Two, the result save path is clear; confirm first whether that default automation Workspace is the one you want. Three, external dependencies are stable: data arrives on time, Connector authorization has not expired, the model is available. The docs position automation on periodic, repetitive tasks, which itself shows it suits taking over verified things. Finally, see whether your computer is actually on when it should execute. First success only means the process has hope; running stably unattended is true hands-off.

## 63. Why, after switching a Skill, Connector, or model on the same task, should you re-accept?

These three all directly join the execution chain; change one and the result may change. Switch the model and comprehension and output style change; switch the Skill and the work flow changes; switch the Connector and the data it reads and the position it can write may change. The previous acceptance held under the old combination; after switching it is void. The most stable practice is a minimal verification after switching: take a small task whose correct answer you already know, and see whether the new combination still gives a consistent result. Re-accepting once is far cheaper than reworking later.

## 64. After an upgrade or restart, if the original Workspace looks gone, what should you check first?

Do not suspect the system broke, and do not rush to rebuild the task; first look in the local large directory. The Workspace is ultimately a local folder; after upgrade and restart it is not visible in the interface, usually because the entry did not match, not because files were deleted. On Windows go to C:/Users/your-username/Tencent WorkBuddy, on Mac go to /Users/your-username/Tencent WorkBuddy; the date-named folders are usually still there and can be found by reopening. Another case is the install directory was cleared and rewritten during update, which is also why the docs repeatedly remind to sync important files to an independent directory. Most disappearances are just not finding the right place.

## 65. After newly connecting a model, what should you compare first, instead of blindly switching wholesale?

Compare its specific performance on your fixed tasks first, not the capability list on its promo page. Capability markers like tool call, image input, reasoning mode only tell you what it can theoretically do; what truly decides usability is whether it is stable in your scenario. After connecting a new model, pick one or two tasks with verified results and let it run once, then compare with the old result. Focus on three things: did the output format change, did key conclusions drift, did tool calls fail. The docs also mention different models have different focuses; these differences only show in your real tasks. Compare on a small scope first, then decide whether to expand use.

## 66. How do you tell whether a failure should blame the model or rewrite the process?

Break it by error source. If an error code comes with it, first see which class it belongs to. The docs classify common error codes: ones like 14003, 11133, 1001 are mostly about model-side state, usually switch model and retry first; ones like 3002, 3003, 400, 401, 504 are mostly about network environment, first check whether you use company or home network. An error code pointing to the model means this time it is likely the model; if it keeps stuck at the same step and switching the model cannot save it, then the process likely has a flaw: task too heavy, directory not set right, or a fuzzy point in the need it cannot understand. First classify by error code, then see whether it repeatedly sticks at the same place, and you can basically tell whether to switch model or fix process.

## 67. Why are the artifacts in the result area often more trustworthy than "completed" in the chat box?

The words in the chat are what it says itself; the files in the result area are what it actually made. A completed can be very light; a landed file must truly be generated, written, saved, not in the same credibility league. The four views in the result area let you check delivery from different angles: the artifact view shows what was generated, the all-files view shows where it landed, the change view shows what it touched, the preview view lets you glance without downloading. Many failures are because only the chat was read, not the file: it said done, you open and see either wrong place, wrong format, or a missing section. Trust the artifact, not just the words.

## 68. How do you add a confirm before send layer to a Connector task, to avoid trouble?

The easiest place for a Connector to cause trouble is that it can directly act on external systems: send email, send messages, edit online docs, write to cloud drives, these actions are costly to undo. So for send-type tasks, best add a confirmation gate right in the instruction, such as after the email is ready, save it as draft first, wait for me to confirm content and recipient before sending. The docs also mention that after a Connector is authorized, you can disable or disconnect it anytime via a switch; when you do not want it to auto-send externally, turn off the corresponding Connector and let it only read and prepare. Downgrade it from auto-execute to prepared and waiting for your nod; this one extra confirmation saves much external-send trouble.

## 69. Why, when the client is offline, does even the best automation fail to run at all?

WorkBuddy's automation executes on your local computer, not in the cloud. Once the schedule triggers, the one actually reading files, calling the model, generating results is the client on your machine. If the computer is off, asleep, or the client is not running, this chain breaks, and no matter how precise the schedule, it is useless. The docs specifically mention an anti-sleep setting; once on, the system will not sleep, leaving continuous-run conditions for remote control and automation. The premise of building automation is not only that the process runs, but that at the time it should execute, your computer is awake, online, and running the client.

## 70. When you want more stable results, which three links should you prioritize strengthening?

The first is the input end, how to state needs. Write the three elements clearly: what to do, what materials, what result, plus a reference sample; this beats ten lines of abstract requirements. The second is the capability end, model, Skill, Connector. If a file cannot be read, switch to a model supporting that capability; once a fixed process runs smoothly, distill it into a Skill; if external data is enough, do not randomly connect Connectors. The third is the acceptance end, result area and version management. Check the four result-area views one by one, back up important files in advance, self-check the change view before accepting. The onboarding order the docs recommend also confirms this progression: first learn to state needs, then stepwise adjustment, then get familiar with Experts and samples, finally for real files back up first then try automation.
