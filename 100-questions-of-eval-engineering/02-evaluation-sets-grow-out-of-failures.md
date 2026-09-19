# Chapter 2 Evaluation Sets Grow Out of Failures


## 13. Why should you hand-label the first 30 examples yourself when starting an evaluation set from scratch?

The opening move is error discovery: read traces and write down the ways the application fails. Start with a pool of roughly 100 diverse traces, hand-label at least the first 30, and only then look at the agent's suggestions. Write free-text notes on anything that looks wrong from the user's perspective—these 30 examples leave the agent a concrete record of your judgment criteria.

The first pass must stay manual. If the agent starts surfacing issues too early, its guesses will bias your judgment, and you may miss failures that only become visible through product context, or through your own definition of "a good user experience." After 30 examples, let the agent search the rest of the pool for similar cases: review every suggestion yourself, accept or reject each one, and correct the agent on the spot whenever it misreads your criteria.

Where do you stop? When new traces no longer reveal new failure modes and no longer reshape the existing ones, you have reached what qualitative researchers call theoretical saturation. The recommendation is to review at least 100 traces; if you are still learning something new, keep going. A pool of roughly 100 diverse traces is the working guardrail for this human-machine loop—the agent concentrates your attention on the most informative traces, so you no longer have to read all 100 in order.

Two common pitfalls: outsourcing labeling—never do it, labeling must be done by domain experts; and not looking at enough examples—30 at minimum, aim for at least 50, sometimes as many as 100.

```
Error analysis notes table (one row per trace):

trace_id │ input │ output │ failure notes (free text, any wording) │ failure category (backfilled after grouping)

Rule: notes only describe "what happened"; leave the category blank for now and backfill it when grouping in open coding
```


## 14. How do you run the full error analysis workflow, from open coding to prioritization?

The workflow starts with building a dataset: collect representative user-interaction traces; if you have no data, generate synthetic data to get started. Step two is open coding: a human—ideally that "benevolent dictator"—reviews traces one by one, writing open-ended notes on any problem, in a practice similar to journaling, adapted from qualitative research methods. Hand-label at least 30 traces to start; at first it is enough to record the first failure observed in each trace, since upstream errors drag along downstream cascades, though if you have the bandwidth you can also tag failures that are independent of one another. This step should be done by a domain expert.

Step three is axial coding: group the open-ended notes into a failure taxonomy—cluster similar failures into clear categories, then count how many failures fall into each category. Axial coding is the most important step in the entire workflow, and an LLM can help with it. Step four is iterative refinement: have the agent cluster the data and pick a diverse initial sample; once the first batch of 30 is labeled, have it search the remaining traces for suspected instances of the failures you described, accepting or rejecting each one until you reach theoretical saturation.

Nurture Boss walked this exact path: each spreadsheet row corresponded to one conversation, open-ended notes were written on any undesired behavior, an LLM then built a taxonomy of common failure modes, and each row was mapped to a specific failure label with frequencies counted—three problems accounted for over 60% of all problems.

Rerun cadence: rerun error analysis after new features, prompt updates, model changes, and major bug fixes; the heuristic target is at least 100 new traces per review cycle, with cycles commonly 2–4 weeks long. Between major analyses, review 10–20 traces per week, watching outliers: unusually long conversations, sessions with multiple retries, traces flagged by automated monitoring. For a new system, analyze weekly until the failure modes stabilize; for a mature system, once a month may suffice. Always analyze after incidents, spikes in complaints, or metric drift.

| Step | Action |
| --- | --- |
| 1 Open coding | Write open-ended notes on each trace, describing only what happened |
| 2 Grouping | Cluster the open-ended notes into a failure taxonomy (failure classification) |
| 3 Counting | Count the frequency of each failure category and prioritize by share |
| 4 Rerun | At least 100+ new traces per cycle; cycles of 2–4 weeks, plus 10–20 per week in between |


## 15. How many golden set examples are enough—50, 100, or 500?

DeepEval's advice: keep datasets high-quality and low-quantity—about 100 golden set examples (goldens), ideally with expected outputs. After serving dozens of enterprise customers, their recommendation is to start with 100 goldens and expand to at most 500; the worst mistake is auto-generating massive numbers of test cases, degrading the dataset into meaningless AI slop.

The practitioner course gives a five-layer dataset, each layer with its own size: a dev set of about 50–100 examples, looked at daily to guide day-to-day decisions; an eval set kept in reserve, about 200–500 examples, used only for major decisions (deployment gates, A/B test winners), separated from dev to prevent overfitting; a regression set that takes in every bug you fix, growing over time and rerun on every change; a canary set of about 20 examples, continuously sampled from production to watch for drift; and a production sample—a random sample of real queries plus periodic human review—which is the source of truth all the other layers are approximating. Of the four sources of data, the first 50 must be handwritten—sitting down to write 50 examples will surface more bugs to you than any other activity.

The statistical power perspective gives a third set of numbers: to detect a 3-point improvement from 82% to 85% at 5% significance and 80% power, a two-proportion z-test works out to roughly 2,400 examples per group; with 100 examples, the minimum detectable effect is close to 10–12 points, not 3 points. Paired analysis can cut the sample needed for 3-point detection roughly in half, to about 1,200—still not 100.

| Source | Recommendation | Note |
| --- | --- | --- |
| DeepEval | Start with about 100 golden set examples, expand to at most 500 | Vendor's framing |
| Practitioner course | Five layers: dev ~50–100 / eval ~200–500 / regression set one per bug / canary ~20 / production sampling; the first 50 must be handwritten | Practitioner's framing |
| Statistical power | ~2,400 per group to detect a 3-point gain; minimum detectable effect at 100 examples is 10–12 points; paired analysis halves it to ~1,200 | Single-source account |


## 16. How do you fill in the non-happy-path samples missing from your golden set?

LangWatch lists "testing only the happy path" among common mistakes: your experiment dataset has 500 examples of the agent doing its job correctly—great, but what about angry, rude users? Requests that are completely off-topic? Multi-turn conversations that fall apart? The edge cases in real production logs? Pull failure cases from production into your test set—that is where the real edge cases live.

In the first lesson of the Hamel & Shreya course, Shreya tackled the question of figuring out what "good" looks like in the context of a specific application. Rather than trying to define "good" directly, she recommended starting from users' latent dissatisfaction. Taking the course project recipe bot as an example, there are five unhappy paths: ingredients that are unusual or impossible to buy; ignoring dietary restrictions or allergens; unclear cooking instructions; complexity mismatched with the user's skill level; and the user asks for healthy and gets unhealthy.

This unhappy paths approach helps you first define what "good" is not—and its flip side lays the foundation for positive specifications.

Anthropic's counterpart practice is building a balanced set of questions: test both the cases where the behavior should appear and where it should not—one-sided evals create one-sided optimization; for instance, testing only "search when it should search" can end up cultivating an agent that searches on everything. Try to avoid class-imbalanced evals. They learned this firsthand while building web search evals for Claude.ai: the hard part was striking a balance between undertriggering and overtriggering, and it took many rounds of iterating on the prompt and the eval to get it tuned; as new examples emerged, they kept adding them to the eval to improve coverage.


## 17. How do you mix random sampling and targeted selection to pick traces?

Five common sampling methods, each with a main limitation: Random picks traces with equal probability, and small batches easily miss rare cases; Clustering groups by content similarity and picks examples per group, with results depending on feature and clustering choices; Data analysis reviews extremes such as latency and tool-call counts, and extremes may have nothing to do with quality; Classification uses an evaluator or another model to flag suspected failures, and it is biased toward problems the classifier already knows how to find; Feedback selects traces with negative feedback, and problems users never report slip through. The table runs from most exploratory to most targeted: explore the data first when starting out, and lean more on signals to select traces as you learn more; the mix depends on your goals—you have to experiment your way to it.

Keep a share of random traces in every batch—this gives you a chance to stumble upon failure modes your existing signals cannot describe. To test a rare failure mode, use targeted sampling: first find signals associated with that failure, such as specific tool-call sequences, unusually long traces, retries, or known input patterns; then review this targeted batch, collecting examples and sharpening your definition of the failure.

You can also borrow active learning from machine learning to choose the next trace to review: the system asks a human to label the data points most useful for its next round of updates. In Shreya Shankar's demo, Claude Code clusters traces and picks examples from each cluster for human review, while a monitor command watches for new labels in annotations.json—once new labels arrive, the agent updates the failure taxonomy, then goes looking for similar cases or different failures. Active learning is used in error analysis to find new cases, and it can also be used at any point in the workflow that requires labeled data.

| Sampling method | Approach | Bias |
| --- | --- | --- |
| Random | Pick traces with equal probability | Small batches easily miss rare cases |
| Clustering | Group by content similarity, pick examples per group | Results depend on feature and clustering choices |
| Data analysis | Pick extremes from metrics such as latency and error rates | Extremes are not necessarily related to quality |
| Classification | Use an evaluator or another model to flag suspected failures | Biased toward problems the classifier already knows how to find |
| Feedback | Select traces with negative feedback | Misses problems users do not report |


## 18. How do you generate synthetic evaluation data without fooling yourself?

Start by prioritizing data sources. The DeepEval documentation's order: first, reasonably curated datasets—human-reviewed examples take priority, especially covering important user journeys, failures, and edge cases; second, production traffic—if you have no ready-made dataset, sample real conversations or requests from production, then review and clean them before using them for evals; third, synthetic data—when the first two fall short, use it to lay down initial coverage and expose obvious regressions. Within synthetic data there are three further tiers of groundedness: generating from documents is the most solid default, since the generated goldens land in your own knowledge base; generating from existing goldens comes next, suited to cases where the seeds themselves have already been human-reviewed; generating from scratch is the least grounded and is not recommended unless the scenario is simple or you only need rough initial coverage.

Validation is another gate to clear. Arize's rule: a synthetic dataset used for evaluation and experimentation becomes your "ground truth," so take validation seriously—when benchmarking the synthetic dataset on top models, never use the same model for generation and validation, for example generating with GPT-4 and validating with Mistral Large 2; the validation process must also include human review, since humans catch nuances that automated methods miss. A small number of human-labeled examples can noticeably raise the quality of a synthetic dataset: add targeted examples by hand to fill gaps or under-covered scenarios, but don't drown out the synthetic portion.

Databricks' approach is to turn synthetic answers into facts: instead of a complete LLM-written answer, the API generates "a set of facts a correct answer must contain" (expected_facts), stored in a table alongside the request and the source document chunk; having an SME review a set of facts is far faster than reviewing a complete generated answer.

```
Synthetic data generation workflow (generation and validation must be separated):
1. Source ordering: curated data > production traffic > synthetic top-up (generating from scratch not recommended)
2. Use model A to generate candidate Q&A pairs from documents (e.g., GPT-4)
3. Use model B to validate quality (e.g., Mistral Large 2)—never self-validate with the same model
4. Human spot-check a small number of samples; fill in gap scenarios
5. Keep evaluation sets isolated from the generation process: the real eval set must never enter generation
```


## 19. Which labeling can be outsourced, and which must you do yourself?

Course notes list this among common pitfalls: outsourcing labeling—never do it; labeling must be done by domain experts.

The expanded judgment: outsourcing error analysis is usually a big mistake (with exceptions). The core of evaluation is building product intuition, and that intuition comes only from systematically analyzing your own system's failures—if this gets outsourced, be extremely wary. There are three risks: superficial labeling—even the clearest metrics require nuanced judgment an external team does not have; handing labeling to generalist developers or IT staff without domain knowledge often yields shallow or wrong labels; loss of tacit knowledge—your lead domain expert holds tacit knowledge that cannot be written into a rubric, and involving the expert in labeling is precisely how you excavate preferences and expectations they could not have articulated in advance; labeling conflicts—external annotators without shared context can create more disagreements than they resolve; aligning an internal team already takes effort, and external parties only take more time.

Three categories of exceptions where outside help is fine: purely mechanical tasks—highly objective, unambiguous work like recognizing phone numbers or validating email formats can be handed to external annotators after a rubric is strictly defined internally; tasks that carry no product context—translation is the classic case, requiring linguistic expertise but not knowledge of your product; hiring domain experts—bringing on an external SME to act as your internal domain expert is not outsourcing; it is importing necessary expertise into the evaluation process: AnkiHub hired fourth-year medical students to evaluate its medical-content RAG system rather than outsourcing to generalist annotators.

Ways to economize when expert time is scarce: use the Think-Aloud protocol from usability testing—ask the expert to look at a few traces while speaking their thoughts aloud; a single one-hour session can surface deep insights. Pair it with smart sampling—thoroughly analyzing 100 diverse traces to find patterns is more effective than superficially labeling thousands.


## 20. How do you use agreement statistics to adjudicate disagreements between annotators?

Start with a counterintuitive bit of arithmetic: Meta PM Daniel McKinnon had three annotators answer a binary question; two chose A and one chose B—on the surface, 66% agreement, which sounds fine. But you actually have to check pairwise: 1 and 2 both chose A, agree; 1 and 3 chose A and B, disagree; 2 and 3 chose A and B, disagree. Only one of the three pairs agreed, so the true agreement rate is 33%. And pure guessing yields a 50% random agreement rate—this 33% is worse than guessing blindly. McKinnon's conclusion: most people severely overestimate the reliability of human evaluation; to do human evaluation, the judgment criteria must be written with extreme precision to guarantee Inter-annotator Agreement—otherwise it amounts to wasted effort.

Why raw agreement alone is not enough: if humans put 88% of items in the same class, a judge with a 90% agreement rate may be only slightly better than a lucky guess. That is why this field measures agreement with chance-corrected statistics, such as Cohen's kappa, rather than raw accuracy.

The disagreement-handling workflow for multi-annotator labeling: first have each annotator independently label the same batch of examples before any discussion; measure agreement and collect cases where labels diverge; hold an alignment meeting, probing which rubric clause triggered the disagreement and what additional rule would make the next judgment clear; update the rubric with a definition, rule, or example that covers the disputed case, then relabel the affected examples; if the annotators still cannot converge, designate one domain expert to make the final decision, and record the reasoning.


## 21. How do you write scoring criteria so that two experts reach the same conclusion?

An Anthropic engineering post gives a gradable definition: a good task is one where two domain experts, each reviewing independently, arrive at the same pass/fail conclusion. Ambiguity in the task spec becomes noise in the metric; the same holds for a model-based grader's criteria—an ambiguous rubric produces inconsistent judgments. The accompanying probing question: could they pass the task themselves? If not, refine the task. Every task should also come with a reference solution—a known-good output that passes all graders, used to prove the task is solvable and the grader is configured correctly. The cost of ambiguity has concrete examples: while reviewing Terminal-Bench, it emerged that some tasks asked the agent to write a script without specifying a file path, while the tests assumed the script lived at a particular path—the agent would fail through no fault of its own. Everything a grader checks must be inferable from the task description.

The Claude platform documentation offers operational items: standardize the grading process with a rubric, especially when human grading is needed; set a baseline performance level for the eval—for example, "the model must answer 85% of test cases correctly"—so you know whether the current system is good enough and can measure improvement over time. For the mix of test cases: include tasks that reflect the real world, add edge cases and outliers, blend easy and hard problems, and fold in cases that specifically target known failure modes (cases where the model has stumbled before).

Alongside the rubric comes a principle of skepticism: stay suspicious of large jumps in performance—verify that the improvement does not come from test-set leakage, nor from overfitting to the eval itself.


## 22. Why should labeling verdicts rest with a "benevolent dictator" instead of a vote?

Minimum viable evaluation starts from this very role: begin with error analysis rather than infrastructure, spend 30 minutes manually reviewing 20–50 LLM outputs each time you make a significant change, and use one domain expert who understands your users as the quality decision-maker—the "benevolent dictator."

Why one person decides: for most small and mid-sized companies, appointing a domain expert as the "benevolent dictator" is the most effective approach—this person becomes the final voice on quality standards. Pair a mental health chatbot with a psychologist; pair legal document analysis with a lawyer. A single expert eliminates labeling conflicts and prevents "too many cooks in the kitchen" paralysis. The benevolent dictator can take in others' opinions and feedback, but the process is driven by them. If you feel that judging a single interaction requires five subject matter experts, that is itself a signal: your product scope may be spread too wide.

The escalation path and its boundaries: larger organizations or companies spanning multiple domains (say, multinationals operating in different cultural contexts) may need multiple annotators; once multiple people truly collaborate, you need luck-aware agreement measures such as Cohen's Kappa. But even in large companies, a single expert is often enough. Start with a benevolent dictator where feasible, and add complexity only when absolutely necessary.

Who alone can hold the position: the course notes line up with this—labeling cannot be outsourced; it must be done by domain experts.


## 23. How do you manage evaluation sets like code, with versioning and review?

Of the four properties Braintrust lists for EDD, the second is dataset and run lineage: each eval run is bound to a specific dataset version, prompt version, and model configuration, so the team can precisely reproduce any historical result and, weeks or even months after a change shipped, still go back and debug that regression. Correspondingly, dataset management shifts from "rarely-updated static test fixtures" to "versioned datasets that grow out of production traces."

The prerequisite for reproducible reruns is pinning the version of every component involved in evaluation: datasets, prompt templates, model identifiers, judge configurations, scoring rubrics. When a regression appears later, you can rerun the very evaluation that approved the change and find out exactly what changed. Two things come along with it—audit and permissions: every evaluation run, score update, and promotion decision is logged with a timestamp and reviewer identity; role-based access control defines who may modify evaluation criteria, approve promotions, and bypass regression gates.

Databricks shows what this looks like as a product: its managed evaluation dataset service manages the lifecycle of evaluation data in a version-controlled Delta Table, and developers and SMEs can trace the version history of each evaluation record—question, ground truth, and label-type metadata—specifically tracking three types of events: adding an evaluation record, modifying an evaluation record (question, ground truth, etc.), and deleting an evaluation record.


## 24. How many labeled failure cases does it take to sustain a judge?

The core budget number: label 100 to 200 samples per failure mode. Reuse traces labeled during the error analysis stage whenever they match that failure mode; if those fall short, keep collecting until you are inside this range. Labels should come from one trusted domain expert, and the samples must contain enough Pass examples and enough Fail examples—the judge has to be able to assess both classes.

Before committing to building a judge, run the cost hierarchy first: simple assertions and checks against reference answers are cheap to build and cheap to maintain; LLM-as-Judge requires 100+ labeled samples, ongoing weekly maintenance, and collaboration across three parties—developers, PMs, and domain experts. This cost gap should in turn shape evaluation strategy—build expensive evaluators only for problems you will iterate on repeatedly. LLM-as-Judge is expensive; reserve it for persistent, generalizing failures, and don't spend it on small glitches you can fix in passing. Start with the cheap stuff—regex patterns, structural checks, execution tests—and only reach for complex evaluation for subjective qualities that simple rules cannot capture.

There is also an upstream gate: many teams discover the model is failing preferences they never stated explicitly—they want shorter replies, specific formats, step-by-step reasoning. Close such gaps in the prompt before talking about evaluation infrastructure; errors a single assertion or regex can catch cost next to nothing and are very likely worth doing right away.


## 25. Why should 60 to 80 percent of development time go into error analysis?

The number itself: in projects we have done, 60–80% of development time went to error analysis and evaluation. Set the expectation: most of the effort will flow toward understanding failures—that is, looking at data—rather than building automated checks. Evaluation is part of the development process, not a separate budget line, just as debugging is part of software development.

Where the time goes: error analysis is the most important activity in evaluation—it decides which evals you write first and lets you identify the failure modes unique to your application and data. Skip it, and the evaluation metrics you develop lose their grounding in real application behavior and fall onto counterproductive generic metrics—which is exactly where most platforms push you. Many problems found in error analysis get fixed on the spot as ordinary development, with no need to build separate evaluation infrastructure for them; whether to build an automated evaluator for a given failure mode is a cost-benefit calculation: errors an assertion or regex can catch are worth doing directly, while calibrating an LLM-as-judge demands weighing whether the failure mode deserves it.

The payoff structure: Nurture Boss wanted to improve its AI assistant for the apartment industry. The team built a simple viewer to go through AI–user conversations one by one, with a space beside each for open-ended failure notes. After labeling a few dozen conversations, a pattern emerged—date handling failures: when users said things like "let's schedule a tour in about two weeks," it went wrong 66% of the time. Instead of reaching for a new tool, they looked at real conversation logs, categorized the types of date-handling failures, built targeted tests to catch these problems, and measured improvement on those metrics—date handling success rose from 33% to 95%. The same consultant's broader observation: teams with a well-designed data viewer iterate 10x faster than those without, and such tools can be built in a few hours with AI-assisted development (e.g., Cursor or Lovable).


## 26. Should you build a small 100-example set or a large 2,400-example set after all?

One camp argues for going small: DeepEval recommends high-quality, low-quantity datasets—start from about 100 golden set examples and expand to at most 500. The reasoning: every test run pays LLM API costs and waits for an LLM to evaluate an LLM, so you cannot afford to test everything; a small, sharp dataset is far more effective than thousands of low-quality auto-generated cases. They cite the LIMA paper: 1,000 carefully curated samples aligned a 65B model to be on par with GPT-4. The worst mistake is auto-generating massive numbers of cases, letting the dataset degrade into meaningless AI slop.

The other camp argues for going big: statistical power is the probability that your test detects an effect when the effect truly exists, with the standard target at 80%—accepting a one-in-five chance of missing a real effect at the 5% significance level. Required sample size grows with variance and shrinks with the square of the effect size: halve the effect you want to detect and the sample quadruples. To detect the true 3-point gain from 82% to 85%, a two-proportion z-test works out to roughly 2,400 examples per group; with 100 examples, the minimum detectable effect is close to 10–12 points. The same article's description of reality: the average internal eval suite—50 to 200 examples hand-picked early in development—is not even in the right order of magnitude. Paired analysis exploits the tendency of two models to make consistent difficulty judgments on the same items, using covariance as "free" variance reduction to cut the sample needed for 3-point detection to about 1,200. Still not 100.

Two real-world failure shapes: a team ships a prompt change on the strength of a 3-point eval improvement—pure noise—while having checked only 80 examples, they fail to see the 8-point regression.

| Position | Content | Note |
| --- | --- | --- |
| Go small | Start with ~100 golden set examples, at most 500; 1,000 curated samples once aligned a 65B model to GPT-4 level | Vendor's framing |
| Go big | ~2,400 per group to detect a 3-point gain; minimum detectable effect at 100 examples is 10–12 points; paired analysis halves it to ~1,200—still not 100 | Single-source account |


## 27. Why is a 100% pass rate on your evaluation set actually a bad sign?

To put it in the strongest terms: beware optimizing for high pass rates. If your evals all pass, at 100%, you are most likely not challenging your system hard enough. A 70% pass rate may instead signal a more meaningful evaluation, one genuinely stress-testing your application. Care about evals that help you catch real problems, not evals that make your metrics look good.

Anthropic characterizes 100% as saturation: an eval at 100% can only watch for regressions and provides no signal for improvement. Eval saturation refers to the state where the agent has passed every solvable task and has no room left to improve. Progress also slows as you approach saturation, because only the hardest items remain; results become deceptive then—large capability gains show up only as small score increases. The code review company Qodo was initially unimpressed by Opus 4.5 because their one-shot coding eval failed to capture the model's gains on longer, more complex tasks; only after building their own agentic eval framework did they see the actual progress.

Anthropic's internal rule: treat no eval score at face value until someone has dug into the eval's details and read some transcripts. Unfair grading, ambiguous tasks, correct solutions being penalized, a harness constraining the model—if even one of these holds, the eval should be revised.

Target values and retirement lines: the Claude platform documentation's example is setting a baseline for the eval—"the model must answer 85% of test cases correctly"—as the criterion for whether the system is good enough. The accompanying disposition: if everything keeps passing, the eval has become useless and should be retired, or run at a lower frequency.


## 28. Why do scoring criteria drift on their own, and how do you fix it?

The drift has a paper behind it: "Who Validates the Validators?" by Shreya Shankar et al. (arXiv:2404.12272) describes this phenomenon—to score outputs, a person must externalize and define the evaluation criteria; yet the very act of scoring outputs is what helps them define those criteria in the first place. A paradox follows: without having seen a large volume of outputs, you cannot fully specify the evaluation criteria; yet evaluating those outputs requires criteria up front—before human review of LLM outputs, fully determining the evaluation criteria is impossible.

The FAQ's practical advice: reviewing a batch of examples first and then writing a detailed rubric is often better. Once reviewers go down a checklist ticking boxes item by item, they miss problems outside the rubric. This change in your judgment of "good" is called criteria drift. Don't underestimate how much drift happens while reviewing examples—with a customer service agent that escalates refund requests to humans per policy, you might read several interactions before realizing the process itself annoys users. So use error analysis to review examples systematically and decide what belongs in the rubric, and rerun error analysis regularly to keep the rubric current.

From the front lines: when Honeycomb built its Query Assistant, expert Phillip Carter watched how the LLM broke down its reasoning and realized he was not consistent in judging certain edge cases—the process of reviewing AI outputs helped him articulate the evaluation criteria in his head more clearly. Teams that maintain trust in their evaluation accept rather than fight this reality: treat evaluation criteria as a living document that evolves together with your understanding of the problem space; different stakeholders' criteria may differ or even contradict each other—reconcile them rather than forcing a single standard.

Hugo Bowne lists criteria freshness as the fifth direction for harness evals: the act of scoring agent behavior changes the scorer's perception of "good," and a good harness eval process should expect the definition of quality to evolve.


## 29. How do you keep your evaluation set from being memorized into a model's training data?

Where the risk comes from: Arize warns to be careful when choosing public datasets as generation sources—many publicly available datasets have already been used to train existing models, and if the model you are evaluating was likely trained on that same data, the results will mislead.

Evidence of contamination: GSM1k was designed to create a new set of problems guaranteed to be absent from training data—commission Grade School Math 1000 (GSM1k), mirroring the style and complexity of the GSM8k benchmark and keeping the two benchmarks comparable on metrics such as human solve rate, number of solving steps, and answer magnitude. Evaluating on leading open- and closed-source LLMs, they observed accuracy drops of up to 8%, with several model families showing evidence of systematic overfitting across nearly all model sizes. Further analysis found a positive correlation (Spearman's r^2 = 0.36): the higher the probability of a model generating a given original GSM8k problem, the larger its performance gap between GSM8k and GSM1k—some models may have partially memorized GSM8k. At the same time, many models (especially frontier models) show little sign of overfitting, and all models generalize broadly to new math problems guaranteed absent from training data.

The defense on the leaderboard side: since 2023-12-16, CMMLU has verified two things first for API models not yet in open public beta—1. whether the model has basic instruction-following ability; 2. whether data contamination exists—and only models that pass verification get updated onto the leaderboard.


## 30. How do you turn production logs into an evaluation set that keeps growing?

OpenAI's flywheel in three sentences: log inputs, outputs, and outcomes; sample these logs on a schedule, automatically routing ambiguous or high-cost cases to experts for review; fold these expert judgments into your evals and error analysis, then use them to update prompts, tools, or models. Deployed at scale, this loop produces a large, differentiated, context-specific, and hard-to-replicate dataset—a valuable asset for the organization building the best product or process in its market.

Shreya Shankar's framework breaks the same loop into three segments: evaluation (define success metrics) → monitoring (implement the metrics so they keep pace with production data) → continuous improvement (close the loop). Monitoring actions: for each metric, sample and label from production data on a regular schedule; store the labeled examples in a database, ideally with timestamps so you can track the latest. Improvement actions: on a daily or weekly cadence, review and "fix" low-scoring outputs—find out where the original output went wrong, rewrite it into a correct version, and record the change and the rationale for the team to learn from; then layer on active learning-style continuous improvement: store production traces together with metric scores and human fixes, with low-scoring traces queued first for human review and repair.

The flywheel's foundation: a complete log recording outputs and their associated metric scores—many LLMOps tools (e.g., LangSmith) can help here. The metric set itself is not static: after launch you will learn new failure modes and may need to update the metric set; LLM APIs keep changing under the hood, and the ideal system behavior itself evolves over time.


## 31. How do you mine failure modes from logs the way Nurture Boss did?

The starting point: Nurture Boss founder Jacob wanted to improve the company's AI assistant for the apartment industry. The team built a simple viewer to inspect conversations between the AI and users, with a space beside each conversation for open-ended notes on failure modes.

After labeling a few dozen conversations, a clear pattern emerged: the AI struggled with date handling—when users said things like "let's schedule a tour in about two weeks," it failed 66% of the time. Their response was not to reach for a new tool, but to take four steps: look at real conversation logs; categorize the date-handling failures; build targeted tests to catch these problems; measure improvement on those metrics. The result: date handling success rose from 33% to 95%.

Methodologically this is the bottom-up route: error types can be identified top-down—starting from common metrics like "hallucination" and "toxicity" plus task-specific metrics, which is convenient but often misses domain-specific problems; the more effective bottom-up approach forces you to look at real data and let metrics emerge naturally. NurtureBoss's implementation: start with a spreadsheet, one row per conversation, writing open-ended notes on any undesired behavior; then use an LLM to build a taxonomy of common failure modes; finally map each row to a specific failure label and count the frequency of each problem.

The results were striking: just three problems accounted for over 60% of all problems—conversation flow problems (missing context, awkward replies); failure to escalate to a human (not recognizing when a handoff was due); and rescheduling problems (struggling with date handling). The actionable insights uncovered were so numerous that Jacob's team needed several weeks to finish fixing the problems they had found. An Excel pivot table is a simple tool, but it works.


## 32. Why should metrics grow out of failures instead of starting with generic metrics?

"Tools first" is the most common mistake: teams get swallowed by architecture diagrams, frameworks, and dashboards, skipping the process of figuring out what works and what doesn't. One client proudly showed off their evaluation dashboard—a dashboard that portended failure. This is the "tool trap": believing that picking the right tool or framework (here, generic metrics) will solve the AI problem. Generic metrics are worse than useless, dragging progress down in two ways. First, they create an illusion of measurement and progress: with a dashboard in hand you call yourself data-driven while staring at vanity metrics unrelated to real user problems—one team celebrated a 10% helpfulness score improvement while real users were still struggling with basic tasks, like optimizing load time while the checkout flow is broken. Second, too many metrics shred attention: you should be focusing on the few metrics that matter for your use case, yet you end up optimizing multiple dimensions at once—when everything matters, nothing does.

The FAQ puts it this way: using off-the-shelf generic evaluation metrics as quality measurements wastes time and manufactures false confidence. Evaluation libraries are full of scores like helpfulness, coherence, and quality that promise easy evaluation; they measure abstract qualities that may be irrelevant to your use case, and a good-looking score does not mean the system works. The misuse of generic metrics is endemic: many eval vendors push off-the-shelf metrics, entangling engineers in superfluous tasks.

The alternative order and the exception: do error analysis to understand failures; define binary failure modes based on real problems; create custom evaluators for those failures; then validate against human judgment. Experienced practitioners demote generic metrics to exploratory signals, using them to find traces worth human review. Similarity metrics (BERTScore, ROUGE, cosine similarity) cannot evaluate LLM outputs in most AI applications, but they are useful in search and recommendation—cosine similarity between embeddings can measure semantic closeness in retrieval systems.
