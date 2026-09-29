# Chapter 5 Validate Calibration Before Production

## 65. Why can a model with higher F1 be less useful?

In the COMPSAC paper on predicting PR merges, the random forest scored an F1 of 0.958, and the majority-class baseline that always answers "merge" also scored 0.957; what actually separates a useful model from a useless one is ROC-AUC: the forest 0.676, the baseline 0.500. The paper states explicitly that these models "should not be treated as perfectly calibrated probabilistic models" and are fit only for triage, not for automated accept or reject decisions. The prediction uses only signals visible at submission time; post-submission comments, CI, and subsequent commits are all excluded from the input.

This is not a quirk of one dataset; it is the normal shape of production classifiers. On imbalanced problems most of the accuracy is free, accuracy saturates early, and the hard parts are ranking and confidence. Downstream logic wants probabilities, not labels: when a model reports 0.95 for something that is right seven times out of ten, every threshold you set is a lie. Miscalibration is invisible in F1, in accuracy, and even in AUC: ACC and F1 are threshold metrics and AUC is a ranking metric, and the problem only surfaces once the business rules built on top start causing damage.

First compute Brier and ECE on the classifier in hand: if they are bad, this is a problem Jev might solve; if they are good, what remains is probably just latency and cost.

## 66. How do you compute and read the two numbers, ECE and Brier?

Expected calibration error measures whether the stated probabilities can be trusted: bin the predictions by confidence, measure how far each bin's actual accuracy sits from the claimed confidence, and average with weights equal to the sample count in each bin. The Brier score measures overall prediction quality: the mean of the squared difference between the predicted probability and the actual outcome. One looks at the bins, the other at the global picture.

A Norwegian-language measurement checked 192 claim judgments: the 0 to 0.1 bin held 14 judgments with 0% agreement with the reference answers; the 0.1 to 0.3 bin held 56 at 4%; the 0.3 to 0.7 bin held 41 at 34%; the 0.7 to 0.9 bin held 38 at 97%; the 0.9 to 1.0 bin held 43 at 98%. The direction is right everywhere, with slight underconfidence at both ends.

Binned statistics are the standard engineering practice for measuring calibration: slice the model's probability or noul into intervals (for example 0.5 to 0.6, 0.6 to 0.7), tally each interval's actual correctness in real business traffic, and draw a reliability diagram for every model; a single ECE number hides where the model is overconfident and where it is underconfident. Accuracy and calibration are two different things: nine questions out of ten right while reporting 100% confidence on every question is accurate but not calibrated; reporting 50% on every question and being right half the time is well calibrated but useless; production automation needs both to pass at once.

The same 192 judgments were rerun with different phrasing: the short-sentence version scored ECE 0.040, and after switching to a phrasing with triple-hedged qualifiers it rose to 0.116. The complete binned data follows.

Table T16: Norwegian-language binned calibration

| Confidence bin | Count | Actual agreement rate |
| --- | --- | --- |
| 0 to 0.1 | 14 | 0% |
| 0.1 to 0.3 | 56 | 4% |
| 0.3 to 0.7 | 41 | 34% |
| 0.7 to 0.9 | 38 | 97% |
| 0.9 to 1.0 | 43 | 98% |

## 67. Why must the GBT baseline be run before any talk of switching models?

For many classification tasks the correct baseline is not an LLM but gradient-boosted trees on decent features, equally sub-millisecond, free, and interpretable. The meaningful comparison is three-way on the same task: a classical tabular model, an LLM used as a classifier, and Jev, compared on accuracy, ranking, calibration, latency, and cost. In one leak-proof PR acceptance pipeline, the baseline is a 400-tree random forest, plus the same forest with isotonic calibration fitted in-fold. The bench details are pinned: a fixed five-fold split; the only state inputs are the PR title, body, metadata at submission time, and diff statistics; comments, CI, and subsequent commits are excluded without exception; the leak-prevention rules are not relaxed when the model changes; and the question carries a single noul, will this PR be merged.

The comparison can get cheaper still. As long as the task is classifiable and training data is obtainable, word vectors plus logistic regression reach 95% accuracy on email classification with 50 to 100 training examples, in a model under 1MB with inference under 100 milliseconds; that under-1MB figure does not include the word-vector encoder itself.

The precondition for switching models is beating this baseline on your own data under your own leak-prevention rules.

## 68. How must shadow mode be run for the results to count?

Shadow mode wires Jev into the real production path while only silently logging decision outcomes in the background, triggering no business action, running in parallel with the existing system, fed by real production traffic to accumulate observational data.

Six validation steps come before shadow mode: define the Schema on historical samples and confirm that real situations are not forced into wrong options; record prediction, probability, ground-truth label, and human action field by field; compute accuracy, confidence binning, calibration error, false positives, and false negatives separately; set the thresholds for automatic execution, human review, and fallback; then run in shadow mode first, without directly changing production actions; then observe latency, tokens, retries, human takeovers, and long-run price.

The route to production has four steps. Controlled testing: run the same batch of real historical samples through the incumbent LLM and Jev once each, comparing accuracy, calibration stability, p95 latency, and cost. Shadow mode: connect to the real path and log silently in the background. Small-traffic trial: once the shadow data has validated the integration, open release within bounded low-risk limits and keep observing through the staged rollout. Continuous monitoring with the fallback pinned: a standby path for switching back to the traditional LLM in one click at any time must always be preserved, and any detected drift in probability calibration triggers an alert and intervention immediately. Prism, on the quantification side, currently defaults to shadow/advisory and does not drive trades directly.

## 69. What exactly do you validate when verifying calibration on your own data?

Calibration must be measured on your own dataset: probabilities that sum to 1 do not mean Jev or Jev-family models are calibrated. For a deep dive into calibration, ad click-through-rate models are a good starting point, because calibration is life-or-death there; such models survive by recalibrating repeatedly as the data drifts, not by calibrating once for a lifetime.

Three things to validate. Reliability diagram: plot actual frequency by confidence bin and check whether the curve hugs the diagonal. Expected calibration error: one number summarizing overall deviation. Noise at the threshold: rerun the samples sitting exactly on the business threshold many times and watch the flip rate; rules in the middle band wobble, cases at the two ends barely move, and the threshold sits precisely in the wobbling band.

Treat "calibration" as a hypothesis: on your distribution, before the business rules depend on it, test it away.

## 70. How do you judge whether the experimental result is capability or convenience?

The interpretation criteria were pinned in the experiment design. If Jev matches the random forest's AUC and beats the calibrated forest on Brier and ECE with no post-hoc fitting of any kind, the calibration claim holds on distributions TypeSafe has never seen, and migrating the company's classification-shaped LLM calls onto it can begin. Beating the uncalibrated forest while failing against the calibrated one is convenience, not capability. If AUC is clearly lower, speed is irrelevant no matter how fast it runs.

If "probabilities are honest out of the box" holds, what it removes from production ML systems is an entire layer of glue. That "if" is the whole question, and it is measurable; whatever the numbers turn out to be, the results will be published.

Table T17: Three conclusions for reading results

| Result | Conclusion |
| --- | --- |
| Matches the baseline and is better without post-hoc calibration | Capability |
| Slightly worse but saves the calibration post-processing | Convenience |
| Clearly lower ranking ability | Do not switch |

## 71. How many samples does a conclusion need to stand?

The Norwegian study used twenty-four documents and declared its own scope up front: twenty-four documents plus one early-access model is a first look, not a benchmark. With twenty-four documents, the 95% confidence interval on a stance number spans about 15 points on each side, and on the stance and claim rows the three model columns are the same result.

SEC annual report classification used sixty filings: the 0.9 confidence line split the sample exactly in half, with the confident 30 correct on 27 and the unconfident 30 correct on only 12; when the same batch of answers was rolled up one level to the parent category, correctness rose from 40% to 70%.

The two self-consistency studies varied the repeat count instead: each condition was repeated 15 times, with every run counted as an independent sample rather than a replay. The object of study was precisely that labels flip within a single condition, TypeSafe included, and disagree across conditions as well.

The sample floor follows the use case. For a rough probe, a few dozen suffice; for a review-grade conclusion, a few hundred is the entry point; for committing performance externally, give confidence intervals first, not point estimates.

## 72. What should the height of a threshold follow?

A confidence threshold is not one number; different actions within the same system sit at different tiers according to the consequences of getting them wrong: anything below 0.5 goes to a human, a floor that catches whatever the model itself reports as unsure; high-risk transfer approval is confirmed and executed only above 0.9, and between 0.5 and 0.9 the user confirms again first; read-only balance checks can execute once past 0.5. Start from conservative thresholds, test on your own data, and tune as you observe.

Other lines sit above thresholds. The guardrail Score question has its own threshold: a medical consultation was originally routed to human handoff, but a severity of 2.02 crossed the 2.0 ban line and the review was pushed into a ban. The AUTO_ACCEPT line for citation checking is 0.8, set high at the start and lowered as observation accumulates. In the code-review measurements, one mid-band rule rerun twelve times gave a judgment value of 0.587, standard deviation 0.037, range 0.53 to 0.65, with the two ends barely moving; the noisiest position is exactly where the threshold sits, which is why high thresholds are recommended.

The same batch of probabilities under different policies can produce different decisions: a jailbreak probability of 0.74 is a ban under a strict policy, and after relaxing the action line to 0.85 it becomes a review. When the consequences are asymmetric, the threshold follows the consequences: a ticket routed to the wrong department can be reassigned, so the bar can be looser; high-stakes operations such as automatic refund approval or account bans need tight thresholds and human review.

The tier numbers given by examples across the official documentation can be collected into one list; the sources differ and the scopes differ, but together they state one principle.

Table T18: Threshold source list

| Scenario | Threshold |
| --- | --- |
| Intent routing | 0.5 |
| Citation checking, starting point | 0.8 |
| Balance check | 0.6 |
| Transfer approval | 0.85 |
| High-risk actions | 0.9 |
| Global floor | 0.5 |

## 73. After launch, how do you roll back to the LLM fallback in one click?

What the continuous monitoring step pins is the fallback path: the production environment must always keep a standby path for switching back to the traditional LLM in one click at any time, and drift in probability calibration discovered through metrics triggers an alert and intervention immediately. The rollback design is built in three layers: a feature flag governs the one-click switch-back, fallback routing guarantees that switched-back traffic lands on the traditional LLM immediately, and staged rollout keeps the new integration on a small traffic share so the cost of pulling it back is low.

Shipped projects each carry a fallback layer of their own. The moon landing demo is a simplified cinematic simulation that drops to a deterministic fallback when the model is unavailable; the context compaction plugin throws Jev's failures, malformed answers, missing keys, and histories that will not fit straight out to the caller or a Claude Code hook, letting them decide what to fall back to, and the plugin itself reverts to built-in summarization on errors or insufficient compaction.

Production governance adds the version line: a system whose threshold tuning has been finalized should explicitly lock the model version ID and record the version number corresponding to every response in its logs, because the default jev-latest changes with each iteration.

## 74. Is it true that more rigorous wording makes calibration worse?

The same batch of judgments was run twice. The first-draft phrasing used short sentences; it was later rewritten into an aligned version per the annotation guidelines, carrying qualifiers about incidental remarks and citations, at a time when no labels existed yet, so the rewrite had nothing to fit against. Comparing the two versions: claim agreement fell from 0.89 to 0.86, expected calibration error rose from 0.040 to 0.116, and the judgments landing in the 0.3 to 0.7 bin rose from 24 to 41, as the longer instructions pushed probabilities toward the middle. Read the other way around, the 0.3 to 0.7 bin went from 41 judgments to 24; the 0.7 to 0.9 bin held 38 judgments with a 97% agreement rate.

The mechanism is in the literal reading: models read instructions literally, and indirect phrasing costs accuracy; the rewritten question is exactly one long sentence stuffed with three qualifiers. Write the question the way you would ask the colleague at the next desk, and leave the fine print in your own code.

## 75. Why do the official evaluation's reference answers keep drawing criticism?

The 193.6x and 444.6x figures come from the workflow evaluation: assume a "workflow" compute graph expressed in code, run every model through the same workflow, and measure the gap against the average of the smartest models' outputs; the reference answers are the average of GPT-6 Astra and Fable 5.1, and these numbers are expected to sit on the high end of real-world gains.

The same disclosure batch also includes: the workflows came from the model capabilities team, so bias may exist; the reference answers favor OpenAI and Anthropic and may underestimate their own models and DeepSeek; the comparison LLM was called through the System One wrapper, slower and more expensive than a direct call without probability attached. The criticism targets exactly this design: if a correct compute graph is assumed to exist, why compare against the average of the smartest models instead of against that graph? Under this comparison, the result reads "how similar I am to Fable" rather than "how correct I am". That passage ends with the words "I gave up".

The calibration conclusions all come from internal evaluations, and no independent third-party calibration audit report exists yet; the headline numbers are fit to serve as hypotheses for a project kickoff test, not to be copied verbatim into procurement ROI calculations.

## 76. How was a judge with variance 900x lower measured?

LangChain built a target agent with Deep Agents and captured the answers to five weather requests as a fixed LangSmith sample set; each judge scored the same batch of trajectories on a continuous quality score and a binary pass or fail, with human review labels as ground truth; Jev, Luna, Terra, and Claude Sonnet 4.6 each ran one hundred repeats, measuring agreement with human judgment and per-case variance.

On binary judgments Jev matched human judgment on all 500 runs, Terra 99.8%, Luna 96.4%, Claude 80.0%; on continuous scoring Jev had the lowest average per-case variance, 0.0000149, with Luna 433x higher, Terra 913x higher, and Claude 92x higher. Averaging 0.44 seconds and $0.00035 per call, the totals came to $0.34 against $28.17.

The reproduction notes laid it out: the LLM judges had no temperature, top-p, or seed set and ran on each vendor's defaults, and Jev's serving version was absent from the metadata. The conclusions laid it out too: lower variance does not automatically mean more accurate, since a judge can be stably wrong; why the variance is low is something the experiment cannot explain.

The results are explicitly characterized as observational: low variance does not mean the training objective caused the low variance. The four rows of the head-to-head collapse into one table, with Comparison A Terra, Comparison B Luna, and Comparison C Claude.

Table T19: Judge comparison

| Judge | 500-run agreement | Variance multiple | Cost |
| --- | --- | --- | --- |
| Jev | 500/500 | 1x | $0.34 |
| Comparison A | 99.8% | 913x | none |
| Comparison B | 96.4% | 433x | none |
| Comparison C | 80.0% | 92x | $28.17 |

## 77. Why can a constant that only ever says reject count as a good classifier?

Strictly speaking, out-of-the-box calibration does not stand: two projects can hold completely different standards for merging PRs, the probability of a random PR being accepted differs with each project's distribution, and what number could Jev return that would count as "calibrated" for both? The output mode does not even offer an "I don't know" option, and the schema cannot separate "conditioned on the state, the probability is confidently 50%" from "the state holds no usable information and the posterior should fall back to the prior".

A joke test deliberately fed irrelevant state, choosing sports match results, and failed all three questions: it gave neither a probability near the "no-information correct answer" nor, when the prior sat far from 0.5, an answer near 0.5.

The second half is the serious point. In one firsthand production scenario, the best classifier available was a constant that always output the same result, because that result accounted for the overwhelming majority; and it was a constant whose calibration had been measured, tested. There is no way to feed that information to Jev; it was tried, and writing the distribution explicitly into the state does not help much either, though it moves the output a little.

The story has three elements: rejects account for the overwhelming majority of the sample, the model always outputs reject, and the constant's calibration was measured in practice rather than guessed.

## 78. Why does answering the same every time not mean answering correctly?

The self-consistency experiment's comparison, laid side by side: 15 repeats per condition, TypeSafe's raw label agreement rate 90.8%; Haiku at temperature zero scored full agreement, with an average probability standard deviation of 0.0012, lower than TypeSafe's 0.0098. The flips happen at business boundaries: on the primary risk question, harassment came up 11 times out of 15 and violence 4 times, with the top probability pressed below 0.60 and the whole round displaying "uncertain".

Add one application-layer rule, returning "uncertain" and routing to a human whenever the top probability falls below 0.60, and TypeSafe's agreement rate rises to 99.2%, with automatic execution at 74.2%, corresponding to 25.8% of answers converted to uncertain. The 0.60 line is an illustrative application policy, not a calibration guarantee. But these percentages measure repeatability and the frequency of intervening, not whether the actions are right. Haiku's temperature-zero 100% carries an asterisk: repeatability does not mean correctness, and this experiment does not test accuracy.

## 79. Why is calibration a property of model plus data, not of the model?

A model can be well calibrated on its own training and benchmark distributions and drift badly on yours; calibration is a property of model plus dataset. A model trained to please does not necessarily mean 95 when it says 95; a model with calibration as its training objective makes good on 60 when it says 60.

State itself rewrites the judgment: for the same rule, with only the one referenced comment plus the code in the state, the judgment value is 0.32; with 14 unused groups mixed in, it becomes 0.75. Irrelevant details act as interference, and the larger the state, the harder errors are to locate; this is drift on the data side.

Calibration parameters can fail on their own. Laya's MLX port follows upstream v0.3.5 and clamps the fitted calibration temperature to 0.5 to 5.0 before use; the choice:11+ bucket shipped with the weights is 0.1006, which would sharpen the logits roughly tenfold, reporting a coin flip with even odds as near-certain, and warnings are raised bucket by bucket at load time.

Post-hoc fixes, Platt scaling, isotonic regression, and temperature scaling, all work, but each is one more fitted component that drifts the moment the data drifts, and they need quarterly routine recalibration rerun against the data. The only number worth trusting is the one measured on your own data.

## 80. Can asking multiple times and averaging serve as calibration?

The ask-several-times path was tried directly in the self-consistency experiment: 14 judgment questions, 15 repeats per condition, TypeSafe's per-question average probability standard deviation 0.0102, lower than all of the LLM probability conditions. But the "underwriting" question swung between 0.43 and 0.53, straddling the 0.5 decision line; and each call stuffed a fresh one-off uid into the state, so this setup cannot separate sensitivity to irrelevant fields from jitter inherent to the same request.

The handling is to make uncertainty an explicit outcome: below 0.30 answer no, 0.30 to 0.70 (boundaries included) returns "uncertain" and routes to a human, above 0.70 answer yes. The band's motivation lies at the 0.5 line: 0.49 and 0.51 express almost the same uncertainty yet trigger opposite actions on the two sides of the line. The review band absorbs the wobble around 0.5, but values near the band's edges still move, and the automatic decisions that break out of the band are not proven correct either.

The band itself is illustrative: neither a calibration guarantee nor an optimized threshold; production boundaries must be set from labeled samples and from the costs of misjudgment and review. Repetition and averaging measure repeatability, not correctness.
