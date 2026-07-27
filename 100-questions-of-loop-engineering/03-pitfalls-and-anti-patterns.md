# Chapter 3 · Pitfalls and Anti-Patterns

## 35. Why do you think you are running a loop, but are only amplifying errors?

Many people jump in feeling they are already running a loop, because the system keeps executing on its own, calling tools, iterating a few rounds. It looks like a closed loop, but often it is just repeatedly amplifying the same error.

The problem usually lies in uncalibrated premises. The goal was written crooked to begin with, the input was not clean, the tool returns were already noisy, and the system keeps pushing round after round. You see it busy, diligent, persistent, but the direction it is busy in was wrong from the start. That way, the loop did not help you fix errors; it just let the error travel farther, cost more, and leave more traces.

So the truly scary part of a loop is not that it makes mistakes, but that it packages a small mistake as a sense of continuous progress. If you have no midway calibration point, it is easy to watch it run all the way and only realize at the end that it just kept widening the deviation.

References:
- [Arize AI: Why AI Agents Break: A Field Analysis of Production Failures](https://arize.com/blog/common-ai-agent-failures/)
- [NimbleBrain: AI Agent Failure Modes](https://nimblebrain.ai/why-ai-fails/agent-governance/agent-failure-modes/)
- [Hacker News: The unreasonable effectiveness of an LLM agent loop with tool use](https://news.ycombinator.com/item?id=43998472)

## 36. The loop runs diligently, so why is there no real progress?

Because "many actions" and "much progress" were never the same thing.

Many loops give you a strong illusion of progress. It keeps producing logs, keeps calling tools, keeps writing something, looking like it is pushing forward all the time. But if you actually look at the delivery surface, tests did not pass, the problem did not shrink, risk did not drop, and the user got no new value. It just made the "sense of busyness" especially full.

The most common cause of this is the system not binding to a real progress metric. It only knows it completed a few steps, not whether those steps brought the goal closer. If you only watch activity volume and not the result surface, however diligent the loop, it may just be high-frequency spinning its wheels.

References:
- [Latitude: Detecting AI Agent Failure Modes in Production](https://latitude.so/blog/ai-agent-failure-detection-guide)
- [Braintrust: how to trace and debug AI agents in production](https://www.braintrust.dev/articles/agent-tracing-debug-ai-agents-production)
- [Reddit: Agents that "succeed" are scarier than agents that crash](https://www.reddit.com/r/AI_Agents/comments/1sd9y1l/agents_that_succeed_are_scarier_than_agents_that/)

## 37. Why does a loop that looks like it is working just burn tokens spinning empty?

Because it satisfies the condition "continue to the next round," but not the condition "this round was worth continuing."

The most typical look of an empty-spinning loop is finding a seemingly reasonable next step each time: try again, switch a parameter, read it again, add a prompt sentence. Each step alone can justify itself, but put together there is no obvious convergence. In the end tokens keep burning, time keeps moving, but the result does not push forward much.

Where many teams lose is not whether the model is strong enough, but often that they did not set the loop a threshold of "prove this round was worth continuing before continuing." Without that threshold, the system naturally leans toward running a few more rounds. The model is good at continuing; the system is responsible for the brakes.

References:
- [Latitude: Detecting AI Agent Failure Modes in Production](https://latitude.so/blog/ai-agent-failure-detection-guide)
- [Reddit: Reinventing Control Theory one feature at a time](https://www.reddit.com/r/softwarearchitecture/comments/1u5tjy8/reinventing_control_theory_one_feature_at_a_time/)
- [Addy Osmani: Long-running Agents](https://addyosmani.com/blog/long-running-agents/)

## 38. Why does a too-broad goal quickly turn a loop into a slop machine?

Once the goal is written too broad, the system starts filling the space with actions that only "look kind of relevant." Over time, slop naturally emerges.

"Make this product good," "optimize this code a bit," "complete this research": to a person these might still be inferable, but to a loop they are an infinite playground. It patches everywhere, changes everywhere, expands everywhere, touches a bit of everything, and in the end every part looks done, yet no part is truly done deep.

The biggest problem with this kind of slop is not just poor quality, but that it dilutes judgment. You find it harder and harder to tell which actions are critical and which just grew out randomly. The broader the goal, the more easily the loop mistakes "relevant" for "necessary."

References:
- [Sherlocks AI: Why AI Agents Fail in Production](https://www.sherlocks.ai/blog/why-ai-agents-fail-in-production)
- [Galileo: 7 AI Agent Failure Modes and How to Prevent Them](https://galileo.ai/blog/agent-failure-modes-guide)
- [YouTube: Most enterprise AI agents are Slop - here's why they fail](https://www.youtube.com/watch?v=7i7A-Y4EMgQ)

## 39. Why does a too-soft verifier let garbage results pass?

Because once a verifier only says nice things, it is no longer a verifier, just a polite narrator.

Many systems clearly have a check step, but the check standard is too loose and the questioning too soft, so what they get is all "overall not bad," "can be further optimized," "basically done." This feedback sounds gentle, but has no interception power at all. The result is garbage results keep getting released, and the system keeps thinking it is successful.

What a verifier should really do is block the things that "should not pass." It must dare to clearly say failure, dare to point out which item did not meet the bar, dare to send the system back to redo. The moment it starts showing favor, the quality floor of the entire loop is gone.

References:
- [Anthropic: Demystifying evals for AI agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents)
- [OpenAI Cookbook: Build an Agent Improvement Loop with Traces, Evals, and Codex](https://developers.openai.com/cookbook/examples/agents_sdk/agent_improvement_loop)
- [Reddit: After going through 15 agentic-loop papers, the thing that predicts success is the verifier, not the model](https://www.reddit.com/r/AI_Agents/comments/1uh0gfa/after_going_through_15_agenticloop_papers_the/)

## 40. Why is the most dangerous loop failure not an error report but a false success?

An error report at least stops you; a false success tricks you into continuing.

Many engineering systems are already familiar with explicit errors: exceptions, failures, timeouts, wrong exit codes, everyone sees the problem at a glance. But the trouble with loops is they especially easily produce a result that "looks like success." Logs normal, steps done, output present, even the verifier nodded. Only when you actually use the result do you find the core was never solved.

The reason this kind of failure is dangerous is it contaminates all later judgments. You take a wrong result as a new starting point and stack more actions on top. Once a false success enters the chain, every later round is built on a false foundation.

References:
- [Reddit: Agents that "succeed" are scarier than agents that crash](https://www.reddit.com/r/AI_Agents/comments/1sd9y1l/agents_that_succeed_are_scarier_than_agents_that/)
- [Hackernoon: Tracing an AI Agent's Reasoning](https://hackernoon.com/tracing-an-ai-agents-reasoning-building-observability-into-your-pipeline)
- [Anthropic: Demystifying evals for AI agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents)

## 41. Everything passed, so why is the final delivery completely unusable?

Because "passing" often only means it passed the few checks you defined, not that it can truly survive real use.

Many loops narrow verification too much. The page opens, the interface responds, the format is right, so the system judges completion. But in a real environment, users click paths you did not test, data is dirtier than the samples, tools deform under boundary conditions. All your earlier checks passed, yet the final delivery is still a mess.

This kind of problem shows not that the model is utterly useless, but that verification coverage is fake. You tested a carefully arranged stage, but what it delivers faces the wild.

References:
- [Anthropic: Harness design for long-running application development](https://www.anthropic.com/engineering/harness-design-long-running-apps)
- [LangChain: How to Debug & Evaluate AI Agents with Observability](https://www.langchain.com/blog/agent-observability-powers-agent-evaluation)
- [Comet: Agent Tracing and Observability](https://www.comet.com/site/blog/ai-agent-tracing/)

## 42. Why does a loop with no one reviewing most easily slide into cognitive surrender?

Because once the system looks fine for several rounds in a row, people get lazier and lazier about doubting it.

This is not a model problem; it is a human problem. You see it keeps producing, keeps pushing, and easily start handing over the judgment bit by bit. Especially in high-frequency loop scenarios, people instinctively want to save brainpower, so they start defaulting to "since it has run this long, probably fine." This is the most common entry point to cognitive surrender.

Once at this stage, the loop is no longer just an automation tool; it starts shaping your judgment in return. You are no longer managing the system; you are more like being hypnotized by the system's continuity.

References:
- [Reddit: The last human in the coding-agent loop is a bottleneck pretending to be a safeguard](https://www.reddit.com/r/AI_Agents/comments/1suuz4b/the_last_human_in_the_codingagent_loop_is_a/)
- [Hacker News: The Coming Loop](https://news.ycombinator.com/item?id=48643180)
- [Anthropic Workshop: Build Agents That Run for Hours](https://www.youtube.com/watch?v=mR-WAvEPRwE)

## 43. Why does handing all judgment to the agent make things harder to debug later?

Because when all judgment is done inside a black box, when something breaks you have no idea which layer went wrong.

Why did it choose this tool, why did it ignore that clue, why did it feel this result was good enough: if these judgments were not broken out, recorded, left with traces, in the end you only see a bad result. You know it was wrong, but not from which step it started being wrong.

So the more complex the loop, the less you should greedily stuff all judgment into the agent. The agent can do the judging, but the judgment process must be made as traceable as possible. Otherwise what you save is the operation of the moment, and what you trade for is a debugging disaster later.

References:
- [Braintrust: how to trace and debug AI agents in production](https://www.braintrust.dev/articles/agent-tracing-debug-ai-agents-production)
- [Sentry: AI agent observability](https://blog.sentry.io/ai-agent-observability-developers-guide-to-agent-monitoring/)
- [LangFuse: Why Agent Tracing Matters](https://pub.towardsai.net/langfuse-why-agent-tracing-matters-you-cant-debug-what-you-can-t-see-0b63b92c0495)

## 44. Why does a loop that starts smooth become less trustworthy the longer it runs?

Because short-term smoothness does not equal long-term stability; many problems only slowly surface after rounds accumulate.

Context gets polluted, state drifts, temporary patches stack up, tool side effects accumulate, verification starts going through the motions. None of this is obvious at first, so the system often gives a "wow, it actually runs" surprise. But after running long, noise comes in and trustworthiness drops instead.

So a loop's maturity is not about how smooth the first ten rounds were, but whether there is still order after a hundred rounds. Good sprint performance only means a good start. Only if it does not scatter over the long run does the system truly stand.

References:
- [Anthropic: Effective harnesses for long-running agents](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents)
- [Anthropic: Effective context engineering for AI agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)
- [Addy Osmani: Long-running Agents](https://addyosmani.com/blog/long-running-agents/)

## 45. Why can no matter how refined the prompt, it cannot save a bad stop condition?

Because the prompt affects how to do it; the stop condition decides when to stop doing it.

However finely you write the prompt, at best it makes each round a bit more decent. But if the stop condition itself is mushy, the system will still overrun, over-supplement, or keep纠缠 in low-value details. This problem cannot be fixed by wording.

Many people, when a loop diverges, instinctively patch the prompt, and it gets longer and messier. But the place that really needs fixing is often not the opening prompt, but the closing gate. If the gate is rotten, no matter how elegantly you phrased the front, it is wasted.

References:
- [OpenAI: Harness engineering: leveraging Codex in an agent-first world](https://openai.com/index/harness-engineering/)
- [Anthropic: Effective harnesses for long-running agents](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents)
- [Reddit: The "deterministic agent loop" problem](https://www.reddit.com/r/AI_Agents/comments/1sshc8b/the_deterministic_agent_loop_problem_has_anyone/)

## 46. Why does file isolation instantly become the number-one problem once a loop touches a real repo?

Because a real repo is not a toy sandbox; every file, every branch, every temporary change affects each other.

You run a loop in a pure demo environment, and many problems never show up. But once connected to a real code repo, the system faces concurrency changes, dirty workspaces, test side effects, cache pollution, leftover temp files, these real problems. If isolation is not done well, verification results become untrustworthy, and even "what exactly did this change change" may be unclear.

So file isolation is not a nice-to-have; it is the most basic hygiene condition. Without it, talking about verification, rollback, parallelism, and review later basically cannot stand.

References:
- [OpenAI: Harness engineering: leveraging Codex in an agent-first world](https://openai.com/index/harness-engineering/)
- [Mike McQuaid: Sandboxes and Worktrees: My secure Agentic AI Setup](https://mikemcquaid.com/sandboxed-agent-worktrees-my-coding-and-ai-setup-in-2026/)
- [Firecrawl: Multi-Agent Orchestration With Codex](https://www.firecrawl.dev/blog/codex-multi-agent-orchestration)

## 47. Why is a loop with no logs almost impossible to trace back after an incident?

Because a loop's failure often does not live in the final output, but hides in the intermediate process.

Which tools it called, what results it got, at which step it started drifting, why that round decided to continue: without logs, you can only guess afterward. You see a bad result, but not how it gradually grew into this.

So logs in a loop are not something "added during debugging"; they should be present from the start. Without logs, once the system enters multi-step execution, you almost lose the ability to do post-mortems.

References:
- [Braintrust: how to trace and debug AI agents in production](https://www.braintrust.dev/articles/agent-tracing-debug-ai-agents-production)
- [Comet: Agent Tracing and Observability](https://www.comet.com/site/blog/ai-agent-tracing/)
- [Sentry: AI agent observability](https://blog.sentry.io/ai-agent-observability-developers-guide-to-agent-monitoring/)

## 48. Why does a loop with no external state feel like amnesia restarting every round?

Because no matter how long the context, it cannot bear the continuity demands of a long-term task.

If you do not give the system external state, each round can only lean on the bit of information in the current window. As rounds multiply, old decisions get lost, failure records get lost, to-dos get lost, even "why did we choose this before" gets lost. The result is the system each time takes over the scene in a half-amnesiac state.

The meaning of external state is to steadily store "what the last round truly left behind." Without it, a loop does not last long; if it does last, it more and more resembles starting over each time.

References:
- [Anthropic: Effective context engineering for AI agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)
- [LangChain: Context Engineering for Agents](https://www.langchain.com/blog/context-engineering-for-agents)
- [Building AI Coding Agents for the Terminal](https://arxiv.org/html/2603.05344v1)

## 49. Why does a loop's verifier most easily degenerate into a formalism checkbox?

Because the verifier is the thing that most looks "present," but is actually most easily just a decoration.

Many teams add a check step to the system, and psychologically feel reassured. But if you really look, it may only be checking the easiest-to-quantify surface signals: did the file get generated, did the interface return, can the page open. The truly hard judgments, it does not touch, and dare not touch.

That way, the verifier slowly degenerates into a formalism checkbox. It makes you feel the process is complete, but actually raises the interception power very little. The worst verifier is often the one that makes you mistakenly think you already checked.

References:
- [Anthropic: Demystifying evals for AI agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents)
- [LangChain: How to Debug & Evaluate AI Agents with Observability](https://www.langchain.com/blog/agent-observability-powers-agent-evaluation)
- [Reddit: After going through 15 agentic-loop papers, the thing that predicts success is the verifier, not the model](https://www.reddit.com/r/AI_Agents/comments/1uh0gfa/after_going_through_15_agenticloop_papers_the/)

## 50. Why is "run it first, talk later" the most expensive optimism in loop scenarios?

Because once a loop can run continuously, errors also compound continuously.

In ordinary prototyping, "run it first, talk later" is sometimes acceptable. But in loop scenarios, this optimism gets amplified by the system. You run first something with unclear boundaries, unwritten verification, un-designed state, and it will not just make a small error; it will keep copying, spreading, and settling those errors into bigger rework across rounds.

So early optimism in loops is often the most expensive bill later. What you save is today's bit of design time; what you spend is multiplied investigation and patch costs later.

References:
- [Anthropic: Effective harnesses for long-running agents](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents)
- [OpenAI: Harness engineering: leveraging Codex in an agent-first world](https://openai.com/index/harness-engineering/)
- [Sherlocks AI: Why AI Agents Fail in Production](https://www.sherlocks.ai/blog/why-ai-agents-fail-in-production)

## 51. Which loops look smart but are just deferring rework to later?

The most typical kind fronts the problem with rhetoric and leaves the human to clean up afterward.

For example, it can quickly produce a decent report, a seemingly coherent piece of code, a set of seemingly complete operation records. At first glance you feel it is smart and efficient. But once you actually check, you find the core judgment was not made solid, boundary conditions were not handled, key evidence was not examined. It just deferred the seriousness that should have been paid upfront to later human rework.

The most deceptive thing about this kind of loop is it is very good at "first-impression engineering." What is truly valuable is not how much it looks like a finished product at first glance, but whether you have to take it apart and redo it later.

References:
- [DEV: AI Agent Failure Modes Beyond Hallucination](https://dev.to/maximsaplin/ai-agent-failure-modes-beyond-hallucination-208g)
- [Medium: The Tool Execution Gap](https://medium.com/@nraman.n6/the-tool-execution-gap-why-your-agents-make-perfect-decisions-but-nothing-gets-done-d44fecc623a4)
- [Arize AI: Why AI Agents Break: A Field Analysis of Production Failures](https://arize.com/blog/common-ai-agent-failures/)

## 52. Why does the more automated a loop is, the more it makes people think they can skip the details?

Because automation most easily creates an illusion: since the process can run itself, can the person stop caring about the底层?

Reality is often the opposite. The more automated the loop, the more it demands the person designing it understand the details. Because details do not disappear; they just get pressed into the system. If you do not understand tool side effects, state drift, verification blind spots, cost structure, once the system automates, these pitfalls only get buried deeper.

So what automation truly saves you from is repetitive operation, not the responsibility of understanding. The more automated the system, the more easily a layperson overestimates how much they already control it.

References:
- [OpenAI: Harness engineering: leveraging Codex in an agent-first world](https://openai.com/index/harness-engineering/)
- [Reddit: Are we really doing this again](https://www.reddit.com/r/theprimeagen/comments/1ue0vrs/are_we_really_doing_this_again/)
- [Sentry: AI agent observability](https://blog.sentry.io/ai-agent-observability-developers-guide-to-agent-monitoring/)
