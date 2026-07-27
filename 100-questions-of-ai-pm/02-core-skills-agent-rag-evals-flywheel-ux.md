# Chapter 2 · The Core Five: Agent / RAG / Evals / Flywheel / UX

## 14. Still designing AI features with a deterministic flowchart? What is your fallback when the model is only 80% sure?

The underlying assumption of traditional product design is determinism: the user clicks a button, the system must return a deterministic result. The underlying assumption of AI products is the reverse: model output is probabilistic, the same input may give different results at different times, and there is a certain probability of total failure. Many PMs fall at the first step because they are still designing AI features with traditional flowchart thinking: every step drawn beautifully, but each step assumed to succeed, with no fallback. This design looks stunning in an offline demo; once live, the moment a user asks a slightly edge question, the whole flow starts to avalanche.

Fallbacks should be thought of as three layers. At the bottom is the confidence threshold: the model's certainty about its own output can be quantified into a score; below a certain line, do not force an answer, go straight to the fallback logic. The middle layer is the human-takeover path: when the model cannot answer or is not confident enough, hand it off to a human smoothly; do not leave the user stuck on an error page. The top layer is the user-feedback loop: when it answers wrong, collect the user's negative feedback, and sink those cases to feed back into the evaluation set. None of these three layers is optional; missing any one, it comes back after launch as complaints, churn, or reputation damage.

Designing AI features with deterministic thinking is like building on sand; the faster you build, the harder it collapses.

## 15. How do you design trust calibration for an Agent product, so users know when to trust it and when to step in?

Agent products most easily fail on trust: either users do not trust it, or they trust it too much. Both extremes cause trouble. The typical over-trust scene is users throwing all tasks to the Agent, including high-risk operations like sending email, transferring money, deleting data; one mistake is enough to cause serious pain. Under-trust goes the other way: users doubt every action, the Agent's efficiency advantage is worn away, and in the end they feel doing it manually is better. The core of calibrating trust is to match the user's trust level to the Agent's actual capability. This does not happen on its own; it must be designed actively by the product.

A few design principles are unavoidable. Make capability transparent: from the start the user must know what the Agent can and cannot do; do not sell it as an all-powerful assistant, or the backlash after launch will be harsher when users find it cannot deliver. Visualize confidence: every output carries a confidence bar; 80% confidence and 50% confidence must look clearly different in the UI; low-confidence answers should visually alert the user. Manage error expectations actively: in high-risk scenarios you must clearly tell the user this is AI output, please verify; do not let the user mistake it for 100% reliable.

These principles land in the UI as: onboarding must be honest, output must carry signals, dangerous operations need second confirmation. Trust is not the more the better; it is the more accurate the better.

## 16. The boss wants multi-Agent collaboration. How do you talk him out of it with latency and cost data?

Multi-Agent collaboration got especially hot starting in 2025. The boss comes back from a few launch events and tells the team to build a multi-Agent system; this happens every week now. As PM, you are responsible for figuring out the real cost of this at the requirements stage. Discovering it halfway through development is too late.

The cost is really three layers, each quantifiable. Latency is the most direct: a single Agent may finish a task in 10 seconds; multi-Agent has to communicate and aggregate, latency often triples or more. Cost is the second layer: every Agent burns Token, and the communication between Agents also burns Token; three Agents collaborating often costs 5 to 10 times a single Agent. Reliability is the third layer: the more Agents, the higher the probability that a single point of failure collapses the whole flow; once the chain is long, one broken link cuts the whole line.

Put this data into a table and bring it to the boss; it works far better than reasoning. Single-Agent: latency 10 seconds, cost per call 0.05 yuan, task success rate 85%. Multi-Agent: latency 35 seconds, cost per call 0.4 yuan, task success rate 72%. For the same task, spending 8 times more money to get a success rate that moves backward; the boss will judge for himself. In the vast majority of scenarios, a single Agent plus good tool calls beats multi-Agent collaboration.

Multi-Agent is not unusable; it should be used where true parallelism and true division of different professional capabilities are needed. More for the sake of more is just burning money. Talking the boss out of it does not rely on words but on data; data speaks for you.

## 17. Agent autonomous planning triples latency. Which scenarios are worth it, and which are pure self-indulgence?

The core difference between an Agent and a traditional workflow lands on one question: who decides the path. A workflow is a path you design in advance; the model follows it. An Agent is the model deciding the path itself; every step is dynamically planned. The cost of autonomous planning is direct: latency doubles, cost doubles, reliability drops; all three are paid in real money.

Scenarios worth using autonomous planning share consistent traits. One type is tasks whose path cannot be predicted: changing a piece of code may touch several files depending on the code itself; writing a research report may check several directions depending on what is found. These tasks cannot be drawn as a flowchart in advance; you must let the model walk and see. The other type is exploratory tasks: creative divergence, open-ended research, multi-round iterative optimization. The value of this type lies precisely in the model discovering unexpected paths; welding it shut in advance kills its strength.

Pure self-indulgence scenarios also split into two types. Where the flow is already fixed: customer-service routing, order processing, report generation; the path is clear, a workflow is enough, adding an Agent just adds cost. Latency-sensitive scenarios cannot be touched either; where users cannot wait 30 seconds, autonomous planning equals suicide.

The criterion is one line: can this task's path be drawn in advance? If yes, use a workflow; only if not, consider an Agent. Autonomous planning is not "advanced"; it is expensive. Used in the right place it is leverage; in the wrong place it is a burden.

## 18. How is an Agent product's "reliability" actually measured? What does "less capability, more reliability" mean?

People building Agent products soon hit a counter-intuitive phenomenon: the more capable Agent often gets worse user feedback. The reason is that the mistakes it occasionally makes are more shocking, and users remember them longer. In reverse, a weaker Agent that stably makes the same small mistakes is actually accepted, because users figure out its boundary and know when to use it and when not to. This is the core meaning of "less capability, more reliability": an Agent's bottleneck was never the capability ceiling; it is the reliability floor.

What users truly fear is not that the Agent occasionally cannot do something, but that it occasionally can and occasionally acts stupid, and the way it acts stupid is completely unpredictable. This unpredictability destroys the user's judgment model; they cannot even build a sense of "when to trust it."

Measuring reliability looks at three things. The lower bound of task success rate matters far more than the average; an Agent averaging 90% but occasionally producing catastrophic errors is harder to use than one averaging 80% whose worst case is still acceptable. Error predictability is also key: can the user figure out in what scenarios this Agent errs, and thus avoid them proactively? Then there is error recoverability: after an error, can the user easily roll back, retry, or take over?

"Less capability, more reliability" does not mean building a weak Agent; it means moving engineering effort from "make it stronger" to "make it less stupid." Raising the floor by an inch is worth more than raising the ceiling by a meter.

## 19. When designing an Agent, how do you decide which steps must involve a human?

Human-in-the-loop is standard for Agent products; no Agent can run reliably fully unattended. The real question is not whether to have HITL, but which steps must involve a human and which can let the Agent run itself. Judging this looks at two dimensions: the reversibility of the operation and the cost of error. The two cross into a clear priority.

Irreversible high-cost operations must involve a human: sending email, transferring money, deleting data, posting announcements. Once executed these cannot be undone, and the cost is high, so a human must click confirm. Reversible high-cost operations can be reviewed by a human afterward: the Agent does it first, the human reviews, and if unsatisfied can send it back. Drafting an email or a first-version plan fits this mode. Irreversible low-cost operations can let the Agent run but must keep logs: changing a config, sending a reminder; the error impact is small and traceable afterward. Reversible low-cost operations are handed fully to the Agent: internal doc drafts, data preprocessing; errors there do not matter.

In product terms, HITL has four typical modes to pick from. Pre-execution approval fits high-risk operations: the Agent proposes, the user clicks confirm, then it executes. Plan-then-execute fits long-flow tasks: the Agent lists steps, the user modifies, the Agent executes. Real-time guidance fits exploratory tasks: the Agent asks as it works, the user can cut in anytime. Post-hoc review fits low-risk but quality-check-needed tasks: the Agent finishes, the user accepts or sends back. More modes is not better; one Agent product picking one main mode and doing it through beats doing all four halfway.

## 20. Why is chunking strategy not something the PM should worry about? What three things should the PM actually own in a RAG project?

Many PMs doing their first RAG project dive headfirst into technical details like chunking strategy, vector model selection, and retrieval-algorithm tuning. These are for the algorithm and engineering teams, not the PM. The PM touching them is grabbing the engineers' job, while their own job goes undone.

What the PM should actually own in a RAG project is three things. First, define "what counts as good": what accuracy, what recall, what latency, where the cost ceiling sits. No one else sets these business constraints; engineers can only give technical reference. Second, build the evaluation system. Whether RAG works needs a quantifiable evaluation set containing real user questions, covering common cases, edge cases, and adversarial cases. If the PM does not do this, no one will. Third, design the fallback and feedback loop: what if RAG cannot answer, how to collect negative feedback when it answers wrong. These are product decisions landing on the PM's side.

Chunking strategy certainly affects results, but that is the engineer's KPI. The PM's KPI is whether the whole product solves the user's problem, not whether one parameter is tuned to optimal. Spending energy on chunking strategy is like a general digging trenches at the front line; dig well and the battle is still lost.

## 21. When should you use RAG, and when should you let the model answer directly?

RAG is not a panacea. Some scenarios gain a lot from RAG; some are gilding the lily. Whether to use it mainly looks at three things.

Freshness of knowledge is the first signal. Model training data has a cutoff date; knowledge after it the model simply does not know. Once business touches frequently updated content, like product specs, policies, prices, you should use RAG to bring in the latest knowledge. Privateness of knowledge is the second signal: internal company docs, customer data, industry intelligence, none of which the model has ever seen; content like this also needs RAG. Query precision requirement is the third signal: the user asks "what is the company travel reimbursement standard," and wants an accurate answer, not one the model guesses from common sense; this must go through retrieval.

In reverse, scenarios where the model answers directly also fall into a few types. Open creative tasks, writing copy, brainstorming, code review, the model's general ability is enough; adding RAG actually limits it. General knowledge Q&A is the same: common-sense questions, historical events, scientific principles, the model is already trained on them, no need to retrieve. Very small data-volume scenarios: the knowledge base is only a few dozen entries; stuffing them directly into the prompt is more efficient than building a whole RAG system.

One often-ignored dimension is cost. RAG's maintenance cost is not low; document updates, index rebuilds, vector-DB ops are all ongoing investment. If the knowledge base updates less than once a month, think carefully. RAG is a tool, not a standard; use it when it fits, and forcing it when it does not only complicates a simple product.

## 22. RAG retrieval recall is low. How should the PM troubleshoot which link broke?

When RAG retrieval works poorly, the team's first reaction is often to swap the vector model or tune retrieval parameters. This is the most common misconception. Low recall may have its root cause buried in four links, each with a completely different fix.

The frontmost link is document parsing. A PDF table parse is lost, a Word comment is missed, a scan OCR is wrong; all of these make the knowledge incomplete from the source. If parsing breaks, no amount of retrieval tuning later can save it. Further back is chunking quality: too-large chunks stuff too much irrelevant info at retrieval; too-small chunks cut off key context; a wrong chunk position splits a sentence in the middle and the semantics break. Further back is query understanding: the user asks "how to do insurance," the model does not know whether the user means auto-insurance claims or health-insurance enrollment; if the query is not rewritten, the retrieval direction is wrong. Last is the retrieval algorithm itself: vector model selection, hybrid-retrieval weights, re-ranking model. These are technical links, but often the last that need touching.

The PM's correct order for troubleshooting is front to back. First sample a few failed-recall cases and see whether the corresponding source document was parsed correctly; if parsing is fine, check whether chunking is reasonable; if chunking is fine, check whether the query was rewritten correctly; only if the first three links are fine do you touch the retrieval algorithm. Tuning back to front is the team's most common waste: three weeks tuning retrieval parameters, only to find the PDF table was never parsed at all.

## 23. Building RAG on an enterprise knowledge base, how do you handle "documents contradicting each other"?

This is the most hidden and most headache-causing problem in enterprise RAG projects. Documents contradicting each other is usually not because someone deliberately messed up, but because enterprise knowledge itself keeps evolving: last year's policy changed this year, different departments have different rules for the same thing, what the boss said verbally differs from what is written. RAG retrieves all these contradictory documents together, and the model randomly picks one to answer. The user asks the return policy and may get last year's answer this time, this year's next time, and some department's internal rule the time after.

Governing this takes three steps. First, layer the documents: grade them by authority. The latest official policy has highest priority, department-internal rules next, historical versions lowest. Retrieve with the authority tag attached, and the model prefers high-authority sources when generating. Next, conflict detection: before launch, scan the knowledge base with a script to automatically identify documents on the same topic that contradict, and have a human decide which to keep. Skip this and the contradiction stays latent until a user complaint exposes it. Last is the answer strategy: when the model finds multiple sources disagree, do not force a pick; it should clearly tell the user "per doc A the policy is this, per doc B it is that, and here is which to prefer."

Honesty beats fake authority. Document contradiction is not a technical problem; it is a knowledge-governance problem. If the PM pushes it to the algorithm team, it will never be solved.

## 24. Why did the team build Evals but still fail at launch? What are the 5 most common failure modes?

Building Evals but still failing is especially common in AI teams. The reason is usually not that Evals are useless, but that Evals were done wrong, and the wrong ways repeat.

The most common pit is looking only at aggregate metrics. 85% accuracy sounds pretty, but which 15% erred and why, if you do not look at specific cases you cannot find the repeatedly-erring patterns. The next pit is an unchanged evaluation set: business changes, users change, models change, but the evaluation set has not moved in half a year; however high the score, it is self-deception. Evals disconnected from business is the third: technical metrics rose but business metrics did not, meaning you evaluated model capability, not user value.

Two more are subtler. No Bad Case library is one; failed cases are a gold mine that tells you in what scenarios the model fails. Most teams do not collect, attribute, or review them, pouring gold down the drain. The last is treating evaluation as QA's alone. Evals are a shared responsibility of PM plus algorithm plus business; the PM especially must lead the evaluation-system design. Handing evaluation to QA turns it into a formality.

Evals are not a test script run once before launch; they are a production system running through the product's whole lifecycle. If you built Evals but still failed, the Evals design itself is the problem. Fix Evals first, then talk about launch.

## 25. How do you build the Evals golden set? Are 500 samples enough?

The golden set is the core asset of Evals, the brake pad for model iteration. Before any new version launches, it must run once on the golden set; only if the score does not regress can it pass. Building the golden set, quantity is not the key, quality is; 500 carefully selected samples are far more useful than 5000 rough ones.

A few principles are unavoidable. Samples must come from real user input; building an evaluation set from synthetic data is self-deception. The distribution of real user questions is completely different from what the team dreams up. Samples must cover three layers: common cases, edge cases, adversarial cases. Common cases secure the base; edge cases probe capability limits; adversarial cases defend against misuse and attacks. Each sample must have a clear labeling standard: what counts as a good answer, what as a bad one, with example-led scoring rules. Without rules, inter-annotator agreement is poor. Samples must also be updated continuously: business changed, users changed, model upgraded, the golden set must expand with them. An evaluation set not updated in three months is basically already invalid.

Whether 500 is enough depends on business complexity. A vertical scenario with 500 selected samples is enough; complex business may need 1000 to 2000. The standard for "enough" is whether the evaluation set covers all the typical scenarios where you worry the model will err. If coverage is incomplete, keep adding. The golden set is a moat; whoever owns the best domain evaluation set can keep optimizing the best product.

## 26. Why does LLM-as-a-Judge give your Evals 90 points, yet you dare not trust it directly? In what 3 types of problems does it lie?

LLM-as-a-Judge became standard for Evals from 2025, using a large model as judge to score outputs: fast, cheap, runnable at scale. But trusting its score directly is dangerous; the LLM judge lies systematically on three types of problems.

Subjective-preference is the first type. Ask the LLM judge "which copy is better," and its judgment may completely disagree with your real users; it has its own preferences, like favoring long answers and confident phrasing. Self-evaluation is the second type: having GPT-4 evaluate GPT-4's output gives systematically high scores; the model has affinity for its own output, a bias repeatedly verified. Vague-evaluation-dimension is the third type: what is "answer quality," what is "user-friendly"; dimensions without a clear rubric, the LLM judge is basically scoring blind.

The correct usage is to treat LLM-as-a-Judge as a large-scale pre-screening tool, with human spot-checks for calibration. First have humans label a batch of gold-standard samples, then have the LLM judge score the same batch, and compute the agreement between the two. If agreement is insufficient, tune the rubric, add few-shot examples, until agreement meets the bar. Only after that can the LLM judge be used for large-scale scoring, but even then keep 10% to 20% human spot-checks for continuous calibration. LLM-as-a-Judge is not a silver bullet; it is a tool that lowers human-labeling cost from roughly 100 dollars per thousand to 10 dollars per thousand. That last 10% still needs a human to catch.

## 27. After model iteration the business metric did not rise. Is the Evals design wrong, or did the model not improve?

This is the most common true or false question for an AI PM: the tech team says Evals rose 10 points, the business team says conversion did not move; who is wrong? Both are possible; you must check separately.

Wrong Evals design is common. The evaluation dimension only looks at model capability, not user value; BLEU went up but users do not care; accuracy rose but on cases users never encounter. The model-not-improved case also exists: the new model performs well on the golden set only because a few cases in it happened to be covered by the new model; on a live set of the real distribution the effect may be unchanged.

Troubleshooting takes two steps. First verify the correlation between Evals and business metrics: plot the Evals scores of past model iterations against the corresponding business metrics as a scatter plot; positive correlation means the Evals design is basically right, no correlation means there is definitely a problem. Then look at the sample distribution of Evals: if 80% of the evaluation set is easy cases, more points on easy cases are useless, because real users' question distribution is not like that.

The direction to fix Evals is to lean the evaluation set toward business metrics: turn real users' high-value scenarios into evaluation samples, turn the dimensions business cares about into scoring rules. When the model team and business team are misaligned, the root cause is often a poorly designed Evals; it was meant to be the translation layer between technical language and business language.

## 28. Why do most teams' data flywheels get stuck at the first step (instrumentation)? Where exactly do they jam?

Everyone understands the data flywheel: user behavior produces data, data feeds the model, the model improves, user experience rises, producing more data. But most teams' flywheel jams at the first step, instrumentation, because nobody owns it. The PM thinks instrumentation is the developer's job; the developer thinks it is the data team's; the data team thinks the field definitions must be set by the PM. Three sides push it around, and at launch the instrumentation is either missing or incomplete. The deeper problem is that the PM did not write clearly in the PRD stage "which signals to collect."

For the flywheel to turn, at least three types of signals must be collected. Explicit signals are preferences the user actively tells you: likes, dislikes, ratings, regenerate; intent is clear but coverage is low, usually only 1% to 3% of users give feedback. Implicit signals are preferences the user does not say but tells through behavior: which part they copied, which words they edited, how many seconds before closing the page. This type of signal can reach over 80% coverage and is the real fuel of the flywheel, yet ignored by most teams. Result signals reflect model quality through downstream business metrics: whether the user completed a purchase, whether the ticket was closed, whether the code was merged; directly tied to business but with long delay and complex attribution.

If the PM does not write the event list of these three signal types clearly in the PRD stage, the developer will not instrument proactively; if the developer does not instrument, the flywheel dies from day one. The flywheel is not the algorithm team's job; it is the PM's core responsibility. Skip it and the product peaks at launch.

## 29. Building RAG on an enterprise knowledge base, where business docs contradict and core knowledge lives in employees' heads, how do you govern the data first?

This is the most underestimated pit in enterprise RAG projects: the tech team builds the RAG system, the PM eagerly pours in enterprise docs, and the result is a mess. The root cause is usually not that the RAG system is bad, but that the data itself is rotten.

The typical problems of enterprise docs are concentrated. Docs contradicting each other is one type: last year's policy differs from this year's, different departments have different rules for the same thing, what the boss said verbally differs from what is written. Severely outdated docs are another type: the system was long upgraded but the doc still describes the previous version; the process was long changed but the doc still describes the old one. The trickiest is that core knowledge is simply not in the docs at all; how things really work lives in veterans' heads, in WeChat groups, in the unspoken understandings never written down. This part is the main body of enterprise knowledge.

Governing this data takes three steps in fixed order. First, inventory the docs: archive all docs by topic, tagging version, time, source, authority; if same-topic docs conflict, identify it immediately. Next, conflict arbitration: bring in the business side to arbitrate, deciding which version to keep and which to discard. This step must involve the business side; the tech team cannot do it. Last is making tacit knowledge explicit: write down the veterans' processes, rules, and experience through interviews, retrospectives, and case organization. The workload is large, but without it RAG can only ever answer surface questions.

Data governance is the least sexy but most critical link in a RAG project. However flashy the tech, rotten data gives rotten results. Garbage in, garbage out, is repeatedly verified in enterprise RAG.

## 30. Building the data flywheel, should you fund labeling first, the evaluation system first, or the data pipeline first? How to prioritize with a limited budget?

This is the most common budgeting decision for a PM planning a flywheel: all three must be done, but the money only covers one; which first? The answer is fund the evaluation system first.

Why is the evaluation system top priority? Because without evaluation, you have no idea whether what you do later is useful. You label a pile of data; how do you judge whether the model got better or worse after this batch went into training? No evaluation set means flying blind. However pretty the data pipeline, data flows in and out; did it finally become a product-value lift? No evaluation set cannot answer. The evaluation system is the flywheel's brake pad; it lets you dare to iterate, dare to swap models, dare to adjust direction. A car without brake pads goes faster and more dangerously.

Second priority is the data pipeline. With the evaluation system in place, let data flow continuously; the pipeline of instrumentation collection, signal cleaning, and sample ingestion must run through. Third priority is labeling. With evaluation and pipeline in place, start large-scale labeling; now every piece of labeled data can be verified by the evaluation set for usefulness.

For budget-limited teams, the most common mistake is rushing to labeling first. They hire a batch of annotators to label tens of thousands of entries, only to find no evaluation set was built and no way to verify whether the data is useful. The data sits there, and the flywheel still will not turn. Evaluation first, pipeline second, labeling last; this order cannot be reversed.

## 31. When should you fine-tune, and when is RAG enough?

Fine-tuning and RAG are not a substitute relationship; they are tools for different problems. Choose wrong and you waste money with no result. The criterion is one line: does the problem lie in knowledge, or in style?

Knowledge problems use RAG. The model does not know internal company policy, does not know the latest product specs, does not know industry-specific information; these are all knowledge gaps. RAG retrieves external knowledge and injects it into the prompt to solve them. Style problems use fine-tuning: the model's answer is not professional enough, the tone does not match the brand, the output format is inconsistent, some vertical-task performance falls short; these need the model's behavior adjusted, which RAG cannot solve, only fine-tuning can.

More concretely, fine-tuning fits a few typical scenarios. When output format must be strictly uniform, like requiring the model to always output a specific JSON structure or always write a report by a certain template; RAG gives knowledge, it cannot change the model's output habit. When a vertical domain needs deep alignment, like law, medicine, finance; the model needs professional terms and to organize answers by industry convention; the general model used directly has the wrong tone and depth. When style and brand tone need fixing: customer service needs a customer-service tone, sales needs a sales tone; the general model cannot give this differentiation.

The most common misconception is treating fine-tuning as a panacea. The model does not know company policy, fine-tune; does not know the latest price, fine-tune; these are all knowledge problems. Fine-tuning is costly, long-cycle, and must be retrained whenever knowledge updates. The rule is plain: style problems fine-tune, knowledge problems RAG. Get this rule wrong and the budget burns for nothing.

## 32. How to choose the three tiers of HITL labeling: pure human, LLM-as-a-Judge, active learning, and what is each worth?

HITL labeling is a key gear of the flywheel; pure automatic labeling cannot succeed, human participation is mandatory. How humans participate splits into roughly three tiers; which to pick depends on what stage the flywheel is in.

When the flywheel just starts, pure human labeling fits. Annotators score each input-output pair from 1 to 5; high cost, high quality; the goal is to accumulate 500 to 2000 high-quality seed samples in the shortest time. This seed data calibrates the later LLM judge; without this human gold standard, the LLM judge cannot be used.

When the flywheel enters growth, switch to the LLM-as-a-Judge plus human spot-check tier. Use the large model as judge to score each output; humans only spot-check 10% to 20% of samples to calibrate whether the LLM judge has drifted. The key in this tier is giving the LLM judge clear scoring rules; without rules it scores randomly, with rules plus few-shot examples its agreement with humans can reach over 80%, and labeling efficiency rises 10 times.

When the flywheel matures, active learning plus human fallback can be used. The model actively picks the samples it is most uncertain about and sends them to humans; 90% of data is handled by the LLM judge, 10% uncertain sent to humans; the goal is to let humans only make the most valuable judgments, freeing them from repetitive labor. The three tiers are not either-or; a mature flywheel runs all three, switching flexibly by data type and importance.

## 33. Why is the moat of an AI product UX, not the model?

"The moat of an AI product is UX, not the model" was proposed in 2023 and still holds in 2026.

The model was never a moat, for a simple reason: everyone can call the same GPT, the same Claude, the same open-source model; what you can do, others can do. The most convincing example is ChatGPT itself. Before it exploded, a similar model, Davinci, had been open via API for nearly a year, and no team built a ChatGPT. The real moat was two UX innovations: one is streaming output, tokens displayed as they generate, simulating the experience of reading and listening, far friendlier than waiting for full generation then displaying; the other is abstracting away state management, the user no longer has to copy-paste past Q&A into a new prompt, the system maintains conversation state automatically. That is the real meaning of Chat. The model did not change; the UX changed; the product exploded.

Judging whether a UX change counts as a moat has a plain standard: does this improvement move work from the user to the product, and visibly? If yes, it is a moat; if it only looks prettier, it is just decoration. By this standard, the UX moat can be thought of in three layers. The shallowest is having AI present: a product with AI beats one without; this is the entry ticket, not the moat; most AI products are stuck here. The middle is making AI useful: the same target user gets results more easily with your product; this is experience differentiation. The deepest is making AI powerful: the product lets users discover uses the model itself never imagined; this is utility differentiation, the deepest moat.

AI overall still mainly sits at layer one with a bit of layer two; layer three is far from unfolded. The PM's energy should focus on layers two and three; in-fighting within layer one is the least efficient competition.

## 34. What is the fundamental difference between Agentic UX and traditional GUI?

Traditional GUI is a designer-predefined interface: where the button is, how the flow goes, how errors are handled, all fixed at design time. Agentic UX takes another path: the interface is dynamically generated by the Agent; the same entry, different tasks may render completely different interfaces. This difference is fundamental and directly dictates that the product-design methodology must switch.

Several differences are linked. On interface-generation method, traditional GUI is the designer drawing forms for the user to fill and buttons to click; Agentic UX is the Agent dynamically generating cards, components, canvas by task. User operation changes with it: from clicking buttons, filling forms, walking a fixed flow, to natural-language plus multimodal input; the user says one sentence and the Agent understands intent. Flow control also changes from a fixed flow tree to Agent autonomous planning; each step may be a new path. Error handling changes from defensive design to HITL plus self-healing; when the Agent errs, a human catches it. Trust building also differs: traditional GUI is usable once the function works; Agentic UX must explicitly calibrate, the user's trust in the Agent must match the Agent's actual capability.

These differences land in product design as a completely different way of working. The PM designing traditional GUI centers on drawing flowcharts, defining state machines, designing components; the PM designing Agentic UX centers on defining the Agent's capability boundary, designing the HITL control flow, calibrating user trust, designing the schema for generative UI. Still designing Agent products with traditional GUI thinking is like designing a car with carriage thinking; both are called vehicles, but driving them is a completely different matter.

## 35. How do you calibrate user trust in the Agent, avoiding over-trust or not daring to use it?

Trust calibration, seen from retention, is more piercing than seen from design principles, because it directly decides how long users stay before leaving.

Users' trust in the Agent naturally slides to two extremes; it will not spontaneously stop in the middle. This is an Agent-product-specific phenomenon. Over-trusting users throw all tasks to the Agent, including high-risk operations the Agent clearly does poorly; and when the Agent errs once, this type of user instantly flips to complete distrust, faster than gradual churn, almost leaving overnight. Under-trusting users take another path: they doubt every action, re-check every answer the Agent gives; the Agent's efficiency advantage is fully worn away, and in the end they feel manual is better. Both paths end in churn, just at different rhythms.

The difficulty of calibration is that it fights not the user's rational judgment, but the user's emotional inertia. Capability transparency is the first gate: at onboarding the user must know what the Agent can and cannot do; do not package it as an all-powerful assistant to sell, or the backlash after launch will be harsher. Confidence visualization is the second gate: every output carries a confidence indicator; 80% and 50% must look clearly different in the UI; low-confidence answers should visually alert the user. Error-expectation management is the third gate: in high-risk scenarios you must clearly tell the user this is AI output, please verify; do not let the user mistake it for 100% reliable.

These three gates land in the UI as: onboarding must be honest, output must carry signals, dangerous operations need second confirmation. The biggest UX dividend of an Agent product is not making the Agent look stronger, but letting the user accurately understand how strong the Agent is. Calibrate well and retention holds steady.
