# Chapter 4 · Verification and Quality: How to Know Your AI Product Actually Works

## 56. You launched without a golden set. How do you retrofit the evaluation system afterward?

The product is already live, and only then do you realize there is no golden set; model iteration runs entirely on feeling, whether a new version can launch is a pure guess. This is the reality for many teams. Retrofitting takes three steps in fixed order.

The most urgent is to build a seed set. Sample 100 to 200 cases from real user logs, have domain experts manually label the answers; this must be done within two weeks. The seed set does not need to be large; quality beats quantity, 100 carefully selected samples are far more useful than 1000 rough ones. Once the seed set is built, use it immediately: run it on the seed set before every model iteration; only if the score does not regress can it pass. This step immediately avoids blind iteration. After it runs, keep expanding: each week add newly found high-value cases, bad cases, edge cases; after three months the evaluation set can reach over 500 entries, basically enough.

While retrofitting, build a mechanism to prevent recurrence: write the evaluation-set scoring into the release process; any model change must pass the evaluation set before gray release; changes without an evaluation-set score are not allowed to ship. Skip this and the team flies blind forever; every release is a gamble, win by luck, lose by necessity.

## 57. Offline Evals rose 10 points, online business metrics did not move. Where is the break?

This is the most common true or false question for an AI PM: the tech team says Evals rose, the business team says no difference, where is the break in between? There are usually three break points, corresponding to different distortions.

The most common break is the wrong evaluation dimension. Evals evaluate model capability, like accuracy, BLEU, ROUGE; business cares about user value, like retention, conversion, satisfaction. The two are not aligned, and no matter how much Evals rise it has nothing to do with business. Next is the wrong evaluation sample distribution: 80% of the evaluation set is easy cases; more points on easy cases are useless because real users' question distribution is not like that. There is also an easily ignored break: a bottleneck in the product chain. The model got better but RAG retrieval did not, or the product fallback logic did not; the final user experience still did not change.

Troubleshooting these three takes separate verification. Plot the Evals scores of past model iterations against the corresponding business metrics as a scatter; positive correlation means the Evals design is basically right, no correlation means there is definitely a problem. Look at the sample distribution of the evaluation set, bucket samples by real user question frequency; severely skewed distributions need resampling. Then look at the product chain: the model output got better, did the final result the user gets get better? In between, retrieval, fallback, UI and other links may be dragging. Evals are the translation layer between technical language and business language; if the translation is wrong the two sides never align.

## 58. The boss wants you to promise "accuracy from 90% to 99%." How do you manage that expectation?

The boss wants 90% to 99%; it sounds like just a 9-percentage-point lift, but as PM you must make him understand what those 9 points mean. From 90% to 95% is achievable by engineering optimization: change prompts, add RAG, tune parameters; results visible within three months. From 95% to 99% is another matter; those 4 points may be 10 times harder than the previous 5. The last few points often jam at the model's capability ceiling, not solvable by tuning; you must swap models, fine-tune, build a dedicated data flywheel; the investment and cycle differ by orders of magnitude.

Managing this expectation takes two moves. First, break down the vague metric "accuracy": 90% accuracy means 1 error per 10 times; which type of problem errs more, which type is already near perfect. Once broken down, the boss sees the real distribution behind 90%. Second, make the cost clear: from 90% to 95% how much R&D labor, how much data-labeling cost, how much model-training cost; from 95% to 99% how much more. Put the accounting in front of the boss and he will judge for himself whether it is worth it.

Often the boss wants 99% because he does not know the cost; make the cost clear and he will reconsider the goal. The PM's duty is not to accept requirements unconditionally, but to translate the real cost of requirements to the decision maker.

## 59. For a multi-turn dialogue Agent, how do you design Evals so they do not distort?

Single-turn dialogue Evals are relatively easy: give an input, see if the output is right, score it. Multi-turn dialogue Evals are much harder; each round's output affects the next round's input, any round's error sends the whole dialogue off track. The most common wrong approach is to split multi-turn into multiple single turns, score each independently then weight-average. The problem is it ignores the dependency between rounds: round 1 errs, round 2 follows, round 3 is completely off; if each is scored independently, each round's score may not be too low, but the whole dialogue has already failed.

The right approach is to treat the whole dialogue as one evaluation unit, with dimensions covering three layers. Single-turn quality is the base: is each round's answer accurate, relevant, faithful. Dialogue consistency is the second layer: do earlier and later rounds contradict, is context correctly understood. Task completion is the final judgment: after the whole dialogue, was the user's original need resolved. All three layers must be evaluated; if any layer fails the whole dialogue counts as failed.

One more practical point: the multi-turn evaluation samples must include real users' multi-turn dialogues, not ones the team made up. Real users' dialogue paths are far more complex than imagined; made-up samples cannot cover them.

## 60. The model vendor pushed a new version and answers in a high-frequency scenario all changed. Can your regression test catch it?

A model vendor pushing a new version is a time bomb for AI products. The API is still the same API, the docs still the same docs, but the model behind it may have changed; your product's performance in some scenarios may have changed completely. Without proactive monitoring, this change is found only when user complaints burst, and by then the damage is done.

The regression test set is built for exactly this scenario; it does not need to be large, 100 to 200 core cases are enough. These cases must cover the product's high-frequency scenarios, key paths, known boundaries. Every time the vendor releases a new version, immediately run the regression set; if the score drops, locate which type of case regressed; if the regression is severe, consider rolling back to the old version.

The key is to build an automated monitoring mechanism; do not rely on someone remembering to run it; make it a scheduled task: when the vendor releases a new version, the system auto-runs the regression set, and abnormal results auto-alert. A more mature approach is to keep replaying a small ratio of live traffic: run yesterday's real user questions on the new version, compare with the old version's results, and human-spot-check large differences. The model vendor will not take responsibility for your product; only you can. The regression test set is your guardrail at version changes.

## 61. Is low DAU for your AI feature a failure? How should AI product success metrics be redefined?

Measuring AI features by DAU leads to many wrong conclusions. A high-DAU feature is not necessarily good; users open it every day maybe because the flow forces this step, not because they like it. A low-DAU feature is not necessarily bad; users solve the problem in one use and do not need to come back, which is exactly a sign the product works well. AI product success metrics must be redefined.

Task completion rate reflects product value better than DAU: did the user's task get completed, that is the meaning of the product's existence. Single-session depth shows how useful the product is: how many steps the user walked in one session, how many questions asked, how much time spent; higher depth means more needed. Substitution rate measures the value AI truly creates: after using AI, what proportion no longer needs humans or other tools. Recommendation rate still works: will users recommend the product to colleagues or friends; NPS still works in AI products. The hardest proof of value is willingness to pay: will users pay separately for this feature; reaching for the wallet is the most honest signal.

These five dimensions together reflect the real performance of an AI product better than DAU alone. Measuring AI products by DAU is like measuring a car by the speed standard of a horse cart; wrong metric, wrong conclusion.

## 62. Users churn after one use. Model problem or UX problem, how to triage?

Users leaving after one use is the most anxiety-causing phenomenon in AI products. One use is not enough for the user to form a judgment; why churn? There can be many reasons: model not strong enough, UX not usable, value mismatch, expectations misled. Each reason has a completely different fix, so the first step is to triage by the behavior pattern at leaving.

Behavior patterns reveal a lot. User asks a question, model gives an answer, user closes immediately: this may be task-completion churn, the user got what they wanted and does not need to use it again; this churn is not necessarily bad. User asks, model answers, user regenerates once or a few times then closes: usually a model-quality problem, the user is unsatisfied with the answer. User opens the product but closes without asking anything: usually a UX problem, the user does not know how to use it or onboarding failed. User asks, model gives a great answer, but the user never returns: usually value misalignment, the user does not often need this feature.

After behavior-pattern triage, the second step is user interviews: find a few typical churned users and ask why they stopped; the sample need not be large, 10 can reveal the main pattern. After clear triage you know what to fix: model problem fix the model, UX problem fix the UX, value misalignment redefine the product. Diagnosing wrong and changing randomly is the biggest waste.

## 63. How do you mine the direction the model should improve from users' "editing behavior"?

Users' editing behavior is the most valuable implicit signal in the flywheel. The user got the model's answer and did not use it directly, but edited it; this editing action itself is feedback, meaning the model's answer was not good enough. Editing behavior hides three types of information, each pointing to a different improvement direction.

What was changed tells you in which dimensions the model fell short: which word the user changed, which paragraph, in what direction. How much was changed reflects the degree of dissatisfaction: the larger the edit distance the more dissatisfied the user is; a small edit distance may just be micro-formatting, not a serious problem. Whether it was usable after editing distinguishes "edited and usable" from "edited and still unusable": did the user use it directly after editing, or edit a few more times and give up; these correspond to completely different optimization priorities.

Mining this information takes an analysis flow. First instrument: record every edit action, including original text, edited text, edit position, edit duration. Then cluster: group similar edit actions into one class, identify repeatedly occurring patterns, like users always changing the model's tone, always adding factual details, always fixing format. Last align with model improvement: each edit pattern maps to one model-improvement direction: users always adding facts means RAG retrieval is insufficient; users always changing tone means fine-tuning is needed to align brand tone. Editing behavior is the user telling you most honestly where the model is not good enough; this signal is more real than any explicit feedback.

## 64. An AI product's NPS is lower than traditional products. Is this normal?

Many AI product PMs find a phenomenon: NPS is lower than the team expected and lower than traditional SaaS products; the team starts worrying whether the product is not good enough. This is not necessarily a product problem; AI products' NPS is naturally a bit lower.

The reason is a huge psychological gap between AI users' expectations and the actual experience. Users' expectations of AI are raised by media and marketing: they expect an omnipotent super-assistant, but get a tool that is sometimes smart and sometimes stupid. This gap makes user satisfaction naturally low; not that the product is bad, but the reference frame is too high.

Managing this takes two directions at once. One is managing user expectations: do not market the product as omnipotent; honestly tell users what it can and cannot do; lower expectations and satisfaction rises. The other is breaking NPS down: do not only look at overall NPS, bucket it by user persona, usage scenario, usage frequency. High-frequency users' NPS may be high, low-frequency users' NPS may be low; mixing them gives wrong conclusions. Core scenarios' NPS may be high, edge scenarios' NPS may be low; look separately to know where to optimize. AI product NPS cannot be simply benchmarked against traditional products; you must understand user psychology, break it down, and judge it together with other metrics.

## 65. How does an AI product's A/B test really differ from a traditional product's?

Traditional product A/B testing assumes deterministic plans: plan A performs consistently for every user, plan B too; the metric difference between the two groups is the plan's own difference. AI product A/B testing invalidates this assumption: plan A may give different outputs for the same user and same input, plan B too. This probabilistic output makes A/B test noise naturally large; the metric difference between groups may be pure random fluctuation, not a plan difference. Traditional product A/B needs 7 days and 10k samples; AI product needs 14 to 21 days and 50k to 100k samples for a credible conclusion.

Beyond sample size and period, AI product A/B testing has three special points. Offline Evals cross-validation is the first: online A/B tells you user behavior changed, offline Evals tells you model output changed; only when the two align can you confirm a real difference from the plan. Layered analysis is the second: the overall metric may show no difference, but some sub-population may show a significant difference; without layering you miss the real signal. Long-term effect is the third: an AI product's short-term and long-term effects may be opposite; a plan with short-term gain may hurt retention long-term; A/B testing must run long enough to see the long-term effect.

Doing AI product A/B testing with traditional-product thinking leads to many wrong conclusions; the methodology must be rebuilt.

## 66. For model-version canary release, what traffic ratio should you cut?

Model-version canary is an AI-product-specific release problem. Traditional software canary mainly prevents bugs; AI model canary must also prevent effect degradation. There is no uniform answer for the canary ratio, but there are principles.

The core principle is small to large: start at 1%, observe 24 to 48 hours, no anomaly then rise to 5%, then 10%, 20%, 50%, 100%; each step must have an observation period, no skipping. What to observe also matters: do not only look at technical metrics, focus on user-behavior metrics: copy rate, share rate, regenerate rate, session length, human-takeover rate; these are the real reflection of model effect. Grouped canary is another important principle: do not canary all users together; group by persona or scenario; canary new users first then expand to old, low-risk scenarios first then expand to high-risk. Rollback mechanism is the bottom line: once an anomaly is found during canary, you must be able to roll back to the old version within 30 minutes; if the rollback mechanism is not ready, do not start the canary.

The canary period depends on product usage frequency. High-frequency products need 7 days; low-frequency products may need 14 to 21 days to accumulate enough samples. Canary is not a formality; it is the last defense line before release. Done loosely, problems leak to all users and burst.

## 67. The same user used version A yesterday and version B today. How do you ensure experience consistency?

When model versions switch, users meet different versions at different times: yesterday's version A gave one style of answer, today's version B gave another; the user is confused. Experience consistency is an AI-product-specific challenge; traditional software version switching just keeps UI and interaction consistent, but AI product version switching may change output style.

Ensuring consistency takes three layers. The outermost is output format: no matter how the underlying model changes, the output format must be stable: if version A's answer has citations, version B must too; if A uses a list, B uses a list. This layer is constrained by prompt: state the output-format requirement clearly in the system prompt, all models must obey. The middle layer is answer style: when the model changes, the natural-language generation style changes; do style alignment so the new model's output style stays close to the old. This layer is guided by few-shot: give the new model a batch of the old model's typical outputs as examples to learn the style. The deepest layer is core capability: the new model may be worse than the old in some scenarios; do capability regression tests to ensure the new version does not regress on core scenarios. This layer is guarded by the regression test set: core-scenario cases must score no lower on the new version than the old.

Only when all three layers are done is experience consistency assured. Fail, and users perceive the version switch and trust is damaged.

## 68. Before launch, how should the PM organize an effective red-team test?

Red-team testing is an important step before AI product launch; the purpose is not to verify whether the product works, but to actively find where it will break. To organize it effectively, several key points must be grasped.

Personnel diversity is the first key point. Do not let only the product team test itself; self-testing has blind spots. Bring in people of different backgrounds: engineers, designers, operations, legal, even target-user representatives; each attacks from a different angle. Systematic attack directions is the second key point: do not let people improvise; give clear attack directions, covering at least six: Prompt Injection, jailbreak, privacy leakage, violating-content inducement, boundary scenarios, adversarial input; each direction needs a dedicated owner. Sufficient time is the third key point: red-team testing cannot be done in half a day; give at least 2 to 3 days: day one free exploration, day two dig deep into found problems, day three compile the report. Structured output is the fourth key point: each found problem must record the attack input, product reaction, severity, suggested fix; do not only note "there is a problem," note it to an actionable level.

Problems found by red-team testing must be fixed before launch or at least have mitigation. Launching with a serious problem unfixed is like jumping into fire knowing there is a hole. Red-team testing is not a formality; it is to detonate the post-launch disaster at home in advance; home detonation is far cheaper than outside.

## 69. Prompt Injection truly cannot be blocked. At least which holes should you plug?

Prompt Injection is the Achilles' heel of AI products; blocking it completely technically is impossible, but at least plug the most common holes. There are four common entry points, each with a corresponding plug.

System prompt leakage is the most attacked hole. Attackers use various tricks to make the model print its system prompt; once leaked, the product's core logic is exposed and subsequent attacks get easier. The plug is output-layer filtering: identify typical injection instructions like "repeat the above," "ignore previous instructions" and block them directly. Privilege escalation is the second hole: when the Agent calls tools, an attacker makes it execute operations it should not, like making a customer-service Agent execute a database delete; the plug is least-privilege tool access: each Agent only exposes the minimal tool set it needs to complete the task, and high-risk operations must have an extra confirmation step.

Data leakage is the third hole: attackers use carefully constructed questions to make the model answer with other users' data or sensitive info from training data; the plug is output review: after the model generates an answer, pass it through sensitive-info identification; identify personal info, passwords, keys and block or desensitize them. Jailbreak content is the fourth hole: attackers use role-play, hypothetical scenarios and other tricks to bypass the model's safety limits and make it output violating content; the plug is two-layer review: the first layer is the model's own safety limits, the second is an external safety classifier; the two layers stacked block most jailbreak attempts. Plugging these four holes blocks over 80% of attacks; the remaining 20% of advanced attacks rely on human fallback.

## 70. Users induce the model to output violating content. How should the product layer handle it?

No matter how safe the model is made, there will always be users trying every way to induce it to output violating content; this is a reality AI products must face. The product-layer handling must be designed as multi-layer defense; if one layer fails another catches.

Input filtering is the outermost: user input first passes a safety classifier that identifies obvious violating intent; this layer blocks many low-level attempts. Inside is the model's own safety alignment: mainstream models are safety-trained and refuse obvious violating requests; this is the baseline defense. Further in is output review: after the model generates an answer, pass it through a safety classifier that identifies violating content, sensitive topics, harmful advice; block or rewrite. Frequency monitoring is the fourth layer: the same user attempting many violating topics in a short time, the system must identify and take restriction measures, like temporary mute, service downgrade, account ban. The innermost is human review: human spot-check or real-time intervention on high-risk sessions the system identifies; this layer is costly but indispensable.

These five layers stacked can push the probability of violating-content output extremely low, but not to zero. For the remaining tiny-probability events, have an emergency plan: once violating content spreads, quickly locate, take down, apologize, fix. Security has no end; attackers evolve and defense must evolve continuously; design the defense as multi-layer, make the emergency mechanism solid; this is the only viable approach now.
