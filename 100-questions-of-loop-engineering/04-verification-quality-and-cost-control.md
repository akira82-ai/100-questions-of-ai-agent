# Chapter 4 · Verification, Quality, and Cost Control

## 53. Why has the real bottleneck of loop engineering shifted from generation to verification?

Generation has not been so scarce in the last couple of years. Everyone has seen models write, fill, expand. What really blocks many teams now is the other end: how do you know it actually did it right this time.

Because once a loop can execute continuously, the system's output speed clearly outpaces human review speed. You encounter "could not write it" less and less, and "wrote it, but I dare not trust it" more and more. At this point the bottleneck naturally moves from generation to verification. If you do not strengthen verification, that big pile of efficient output just becomes a faster risk amplifier.

So what many teams lack most today is not a more generative agent, but truly a system that is better at blocking errors. The model is responsible for producing things; verification is responsible for deciding whether those things are worth keeping.

References:
- [Anthropic: Demystifying evals for AI agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents)
- [AI evals are becoming the new compute bottleneck](https://evalevalai.com/research/2026/04/29/eval-costs-bottleneck/)
- [Medium: The Agent Quality Problem](https://medium.com/@moradikor296/the-agent-quality-problem-why-observability-isnt-enough-9b45272b324a)

## 54. Should the verifier check results, process, or intermediate state?

The answer is usually all three, just with different weights.

Checking only results easily misses the "luckily correct" fake stability. Checking only process easily manages the system too rigidly, with every step acting by script. Intermediate state is also critical, because many problems are no longer visible in the final output; the deviation grew midway.

A more practical approach is to split these three layers. The result layer sees whether delivery meets the bar; the process layer sees whether there were违规 actions; the intermediate-state layer sees whether there was obvious drift. This way the system neither passes purely by luck nor loses flexibility by over-managing. Verification should never just stare at one layer; what matters more is knowing which layer is most prone to trouble.

References:
- [Anthropic: Demystifying evals for AI agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents)
- [OpenAI Cookbook: Build an Agent Improvement Loop with Traces, Evals, and Codex](https://developers.openai.com/cookbook/examples/agents_sdk/agent_improvement_loop)
- [Thinking Inc: AI Agent Evaluation in Production](https://thinking.inc/en/blue-ocean/agentic/ai-agent-evaluation-production/)

## 55. What kind of verifier can truly block false completion?

A verifier that blocks false completion usually has three traits: specific standards, clear failure, actionable feedback.

Specific standards means it does not just say "looks not bad," but can point out which condition failed. Clear failure means it truly dares to judge failure, not half-discover a problem yet still give pass. Actionable feedback means after stating the problem, the next round can truly fix according to it, not just leave a vague "suggest optimizing."

Many verifiers look present but actually lack these three, so in the end they just make a checking gesture. A truly useful verifier does not block errors by atmosphere; it relies on concrete thresholds that can be implemented one by one.

References:
- [Anthropic: Demystifying evals for AI agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents)
- [OpenAI Cookbook: Build an Agent Improvement Loop with Traces, Evals, and Codex](https://developers.openai.com/cookbook/examples/agents_sdk/agent_improvement_loop)
- [MorphLLM: AI Agent Evaluation](https://www.morphllm.com/ai-agent-evaluation)

## 56. Why, if done is unclear, the whole loop has no controllability?

Because as long as done is mushy, decisions like continue, stop, rework all get mushy too.

Many systems write goals enthusiastically but write done lazily. The result is the agent does not know when to stop, the verifier does not know what to judge by, and the human does not know whether this round counts as done. In the end the whole loop slides into a familiar state: everyone feels about done, but no one can say clearly where the gap is.

The value of writing done clearly is not just convenient acceptance; it is actually setting boundaries for the whole loop. Once the boundary is clear, things like cost, quality, and rhythm start to become truly controllable.

References:
- [OpenAI: Harness engineering: leveraging Codex in an agent-first world](https://openai.com/index/harness-engineering/)
- [Anthropic: Harness design for long-running application development](https://www.anthropic.com/engineering/harness-design-long-running-apps)
- [Anthropic: Demystifying evals for AI agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents)

## 57. Should quality standards be written in the prompt or in the system first?

What can go into the system, put into the system first. What stays in the prompt is better for the parts needing flexible judgment.

Because standards in the prompt easily drift. You switch a task, switch context, switch a few rounds of conversation, and the model's understanding of that sentence may deviate. System-layer standards are harder: structural validation, test thresholds, approval conditions, permission rules, these are more stable once written in, and easier to reuse.

So a steadier division is: the system guards the floor, the prompt supplements tone and inspiration. The floor must be hard; the play can be soft. Reverse it, and the loop tends to run more and more by feel.

References:
- [OpenAI Prompt Engineering Guide](https://developers.openai.com/api/docs/guides/prompt-engineering)
- [OpenAI Agents SDK: Guardrails](https://developers.openai.com/api/docs/guides/agents/guardrails-approvals)
- [Anthropic: Demystifying evals for AI agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents)

## 58. Why are hard checks the floor of loop convergence?

Because relying only on soft judgment, the system will eventually learn to make excuses for itself.

The value of hard checks is they leave no room for explanation. Test failed is failed, format wrong is wrong, critical path not reached is not reached. You can stack more complex subjective evaluation on top, but without that hard floor underneath, the loop easily lets bad results through while reasoning.

Many people initially find hard checks too dumb, feeling they limit creativity. Only in production do they realize this "dumb" layer is exactly the floor of convergence. Without a floor, you do not even know where you drifted.

References:
- [Anthropic: Demystifying evals for AI agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents)
- [Towards More Standardized AI Evaluation](https://arxiv.org/html/2602.18029v1)
- [Best AI Agent Evaluation Tools for Production Teams](https://www.augmentcode.com/tools/best-ai-agent-evaluation-tools)

## 59. When to use a rubric, when to use deterministic checks?

Anything that can be clearly computed, tested, judged: prefer deterministic checks. Anything with subjectivity, composite judgment, style trade-offs: then bring in a rubric.

Interface status, output format, key fields, test results: these suit deterministic checks. But when you ask the system to judge "is this answer persuasive," "does this page have quality," "is this triage suggestion steady enough," a rubric is more useful then, because it breaks fuzzy judgment into several comparable dimensions.

Plainly, deterministic checks are the iron gate, the rubric is the score sheet. Both matter; just do not put a score sheet where an iron gate is called for, nor force an obviously subjective question into a binary.

References:
- [Anthropic: Demystifying evals for AI agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents)
- [Thinking Inc: AI Agent Evaluation in Production](https://thinking.inc/en/blue-ocean/agentic/ai-agent-evaluation-production/)
- [MorphLLM: AI Agent Evaluation](https://www.morphllm.com/ai-agent-evaluation)

## 60. Why does a model grading itself in a loop almost always lean optimistic?

Because it just participated in generating, and naturally has path dependence on its own thinking.

It knows why it wrote this, why it chose that, so it especially easily mistakes "I can explain" for "I did it right." This is a lot like a person reviewing their own writing; the original intent is already in the head, and when looking at the problem it automatically fills in for itself.

So self-grading is not completely useless; it can serve as light pre-screening. But if you treat it as the main verification, you are basically inviting optimistic bias to the table. If you want it stricter, you still need to separate perspective and separate roles.

References:
- [Anthropic: Harness design for long-running application development](https://www.anthropic.com/engineering/harness-design-long-running-apps)
- [Anthropic Workshop: Build Agents That Run for Hours](https://www.youtube.com/watch?v=mR-WAvEPRwE)
- [Anthropic: Demystifying evals for AI agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents)

## 61. Which metrics must be continuously recorded for a loop to run steady?

At least these categories continuously: quality, cost, latency, rounds, failure type, human intervention point.

Quality tells you whether it truly got better; cost tells you whether it is worth it; latency tells you whether the system is getting heavier; rounds tell you whether it converged; failure type tells you whether problems are shrinking or changing form; the human intervention point exposes where the real bottleneck still lies, with the human or with the system.

Many teams only record tokens and success rate, and the numbers look fine but the real experience is a mess. Because whether a loop is steady was never a single-metric question. You have to see whether it stands together on quality, cost, and controllability.

References:
- [Braintrust: Best tools for tracking LLM costs in production](https://www.braintrust.dev/articles/best-tools-tracking-llm-costs-2026)
- [MorphLLM: AI Agent Evaluation](https://www.morphllm.com/ai-agent-evaluation)
- [Anthropic: Demystifying evals for AI agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents)

## 62. Why does rising latency often mean the verifier is getting more complex?

Because generation usually charges forward; verification usually has to come back and look repeatedly.

Writing something may be fast, but checking whether it meets conditions, whether tool returns are right, whether page paths work, whether intermediate state drifted: these actions are naturally slower. Once verification gets complex, latency usually rises first.

So rising latency is not necessarily bad; it sometimes reminds you the system is moving from "get it produced" to "confirm it carefully." The problem is not the delay itself, but whether you realize what that delay bought. If slower but not steadier, that is the real loss.

References:
- [Anthropic: Demystifying evals for AI agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents)
- [Anthropic: Introducing Claude Opus 4.7](https://www.anthropic.com/news/claude-opus-4-7)
- [Medium: The Agent Quality Problem](https://medium.com/@moradikor296/the-agent-quality-problem-why-observability-isnt-enough-9b45272b324a)

## 63. How to trade off cost, quality, and novelty in a loop?

These three rarely max out together. Want it cheaper, usually means fewer rounds, fewer branches, less verification. Want more novelty, often means allowing more exploration and more failure. Want quality steady, and cost and speed probably both yield a bit.

So the key to trade-off is not finding a "universal optimal line," but first admitting which item you most want to protect now. Production delivery usually protects quality first; creative exploration can give novelty more room; batch operations care more about cost.

The most feared situation is saying you want everything, yet the system does not write clear priorities. Then usually none of the three get served.

References:
- [MorphLLM: AI Agent Evaluation](https://www.morphllm.com/ai-agent-evaluation)
- [Anthropic: Demystifying evals for AI agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents)
- [Anthropic: Introducing Claude Opus 4.7](https://www.anthropic.com/news/claude-opus-4-7)

## 64. When should you pay higher cost for a stronger verifier?

When the cost of error is clearly higher than the cost of verification.

For example, modifying a real repo, batch-sending user messages, touching tickets, touching a knowledge base, touching production data: once you let a false completion through here, the later rework and loss are large. If you save verifier money here, it will mostly come back doubled from elsewhere.

Conversely, if the task itself is light, reversible, and easy to fix on failure, there is no need for overly heavy verification. Whether to spend is not about whether you like rigor, but about how expensive it would be once an error leaks through.

References:
- [Anthropic: Demystifying evals for AI agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents)
- [AI evals are becoming the new compute bottleneck](https://evalevalai.com/research/2026/04/29/eval-costs-bottleneck/)
- [Thinking Inc: AI Agent Evaluation in Production](https://thinking.inc/en/blue-ocean/agentic/ai-agent-evaluation-production/)

## 65. Should loop budget be managed by rounds or by results?

Managing only by rounds easily harms those slow but necessary tasks. Managing only by results easily lets the system inflate infinitely. The steadier way is to manage both layers.

Round budget suits the first-layer guardrail, preventing infinite retries. Result budget suits the second-layer judgment, seeing whether the quality improvement those rounds bought is worth it. Tie these two together, and the system will not be stingy on one side and produce nothing, nor produce a lot on one side and be ridiculously expensive.

In the end, loop budget should not only ask "how many rounds ran," nor only ask "is it done," it must answer "for this result, were these resources worth spending?"

References:
- [Braintrust: Best tools for tracking LLM costs in production](https://www.braintrust.dev/articles/best-tools-tracking-llm-costs-2026)
- [MorphLLM: AI Agent Evaluation](https://www.morphllm.com/ai-agent-evaluation)
- [OpenAI Agents SDK: Results and state](https://developers.openai.com/api/docs/guides/agents/results)

## 66. Why do many people know tokens are expensive, yet still cannot control loop cost?

Because people usually only know "a single call is expensive," but did not factor in "how the system will continuously amplify this expense."

The place loop cost most easily runs out of control is not in one round, but in accumulation. Try once more, open one more branch, run one more verifier, do one more review: each looks reasonable. But these small reasonables stack up, and the bill becomes very unreasonable.

So controlling loop cost is not about staring at token unit price every day; it is more about seeing which structures are automatically creating extra rounds, extra verification, extra context. Cost out of control is usually a system-habit problem, not an arithmetic problem.

References:
- [Braintrust: Best tools for tracking LLM costs in production](https://www.braintrust.dev/articles/best-tools-tracking-llm-costs-2026)
- [AI evals are becoming the new compute bottleneck](https://evalevalai.com/research/2026/04/29/eval-costs-bottleneck/)
- [Anthropic: Demystifying evals for AI agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents)

## 67. How to tell whether a loop is converging or elegantly wasting money?

Look at three things: are errors decreasing, are new rounds still bringing clear benefit, is the system getting closer to done.

If every few more rounds the problem type is still the same, cost keeps rising, done is still fuzzy, then it is probably elegantly wasting money. It gives you a very professional illusion: complete logs, detailed feedback, continuous actions. But peel open these appearances and there is no real convergence inside.

A converging loop gets shorter, more accurate, with fewer wasted actions. Spending money is not the problem; spending money yet not making the boundary clearer, that is the problem.

References:
- [MorphLLM: AI Agent Evaluation](https://www.morphllm.com/ai-agent-evaluation)
- [Medium: The Agent Quality Problem](https://medium.com/@moradikor296/the-agent-quality-problem-why-observability-isnt-enough-9b45272b324a)
- [Anthropic: Demystifying evals for AI agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents)

## 68. Facing a high-cost loop, should you cut the model first or cut the ineffective loops first?

Most of the time, cut the ineffective loops first.

Because many high-cost problems are not at all about the model being too expensive, but about the system doing too many low-value repetitive actions. You switch to a cheaper model, but the loop still spins empty, still repeats verification, still does meaningless retries, so you just waste money more cheaply with a cheaper model.

What you should really look at first is which rounds can be deleted, which checks are duplicated, which context should not have been stuffed in at all. Without changing structure, switching models only buys a breath; once structure changes, the cost curve truly comes down.

References:
- [Anthropic: Effective context engineering for AI agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)
- [Braintrust: Best tools for tracking LLM costs in production](https://www.braintrust.dev/articles/best-tools-tracking-llm-costs-2026)
- [OpenAI Agents SDK: Results and state](https://developers.openai.com/api/docs/guides/agents/results)

## 69. Why is a loop with many surprises also often the hardest to control cost?

Because surprises usually come from exploration, and exploration naturally means more branching, more trial and error, more coming up empty.

If you want the system to always take the steadiest path, you can control cost, but it also more easily becomes conservative. If you want it to occasionally break the routine, try new combinations, new tool paths, new expressions, cost is hard to pin down like an assembly line.

This does not mean surprise-type loops have no value; it only means you must first think clearly: are you buying stable output, or buying exploration space? Exploration space is inherently expensive; the key is not to mistakenly package it as cheap automation.

References:
- [Anthropic: Harness design for long-running application development](https://www.anthropic.com/engineering/harness-design-long-running-apps)
- [Anthropic: Building Effective AI Agents](https://www.anthropic.com/research/building-effective-agents)
- [Hacker News: The unreasonable effectiveness of an LLM agent loop with tool use](https://news.ycombinator.com/item?id=43998472)

## 70. Why does a loop's ceiling often get stuck at the evaluation system?

Because however strong the model, it can only optimize within the "good result" space you defined.

If the evaluation system is crude, the system learns to satisfy those crude standards; if the evaluation system has blind spots, the system grows problems in those blind spots. The ceiling you finally see is often not stuck at model capability, but more at whether you wrote, tested, and pinned clearly what "good" means.

So when a loop reaches later stages, the most valuable ability is often not continuing to swap models, but continuing to upgrade evaluation. Only when the evaluation system lifts does the system ceiling lift with it.

References:
- [Anthropic: Demystifying evals for AI agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents)
- [Towards More Standardized AI Evaluation](https://arxiv.org/html/2602.18029v1)
- [AI Agent Evaluation in Production (2026 Guide)](https://thinking.inc/en/blue-ocean/agentic/ai-agent-evaluation-production/)
