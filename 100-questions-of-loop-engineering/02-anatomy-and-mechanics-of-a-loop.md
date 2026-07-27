# Chapter 2 · Anatomy and Mechanics of a Loop

## 17. What are the minimum steps a usable loop must contain?

A minimally usable loop usually needs at least four steps: first see what the current situation is, then decide the next move, then actually do it, and finally check whether it was done right.

Many people start by imagining a loop as something complex, as if it only counts with multi-agent, multi-tool, and multi-layer state. It does not. The minimal version is plain: get the context, make a judgment, execute an action, then decide based on the result whether to continue or stop. As long as those four steps close the loop, it is a loop.

The problem is many people only do the middle "execute" step, with nothing before or after. Without the front-end recognition, they act blindly. Without the back-end check, they fake completion. So the minimal unit of a loop looks like one model call, but is actually one complete closed loop.

References:
- [Anthropic: Building Effective AI Agents](https://www.anthropic.com/research/building-effective-agents)
- [OpenAI: A practical guide to building AI agents](https://openai.com/business/guides-and-resources/a-practical-guide-to-building-ai-agents/)
- [Hacker News: The unreasonable effectiveness of an LLM agent loop with tool use](https://news.ycombinator.com/item?id=43998472)

## 18. Why does a loop break easily if any of discover, plan, execute, verify is missing?

These four steps each guard against a different type of error. Drop any one and the system leaks somewhere.

No discover: you have no idea what is actually happening in front of you, easy to grab the wrong context. No plan: actions become improvisation, one step at a time. No execute: nothing happens, of course. No verify: the most dangerous, because the system confidently treats wrong things as done.

Many loops fail not because the model suddenly got dumb, but because one of these four steps was quietly dropped. Especially verify, the one people most easily skip, and the one with the most expensive consequences. Because once that final gate is missing, the faster you did the front work, the bigger the rework later.

References:
- [OpenAI Cookbook: Build an Agent Improvement Loop with Traces, Evals, and Codex](https://developers.openai.com/cookbook/examples/agents_sdk/agent_improvement_loop)
- [Anthropic: Demystifying evals for AI agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents)
- [Reddit: After going through 15 agentic-loop papers, the thing that predicts success is the verifier, not the model](https://www.reddit.com/r/AI_Agents/comments/1uh0gfa/after_going_through_15_agenticloop_papers_the/)

## 19. Why is a loop's stop condition more important than its opening goal?

The goal only gives direction; the stop condition gives the brakes. The place that really costs money is often not "where to go" but "when to stop."

Look at turn-based loops, goal-based loops, time-based loops: they look very different on the surface, but at the runtime layer they all circle back to this. Turn-based is a human calling stop; goal-based is the result calling stop; time-based is the time window calling stop. As long as that stop line is unclear, the system will keep feeling it can do one more round, try once more, optimize a bit more.

So when writing a loop, the goal can be a little broad, but the stop condition must be written concretely. Tests passing, the page opening, the format being compliant, the key metric crossing the line: these are where the loop truly closes.

References:
- [Ryan Lopopolo / OpenAI: Harness engineering](https://openai.com/index/harness-engineering/)
- [Oracle Developers: What Is the AI Agent Loop?](https://blogs.oracle.com/developers/what-is-the-ai-agent-loop-the-core-architecture-behind-autonomous-ai-systems)
- [Firecrawl: Loop Engineering](https://www.firecrawl.dev/blog/loop-engineering)

## 20. Why does a loop with no clear exit condition keep getting more expensive?

Because systems are naturally bad at "good enough," and better at "can we do another round?"

If you do not give an exit condition, the model usually will not stop gracefully on its own. It keeps finding problems, keeps adding details, keeps retrying, even when the later returns are already very low. That way, tokens, time, tool calls, and human attention all keep piling up.

The worse part is this expense does not blow up at once; it disguises itself as "each round still looks reasonable," so people easily lose vigilance. In the end you look back and realize the problem is not that the model produced nothing, but that it kept consuming resources in a boundless space. The exit condition, at the end of the day, exists to protect cost.

References:
- [Anthropic: Effective context engineering for AI agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)
- [OpenAI Agents SDK: Results and state](https://developers.openai.com/api/docs/guides/agents/results)
- [Addy Osmani: Long-running Agents](https://addyosmani.com/blog/long-running-agents/)

## 21. What do generator and verifier each own in a loop?

The generator pushes forward; the verifier hits the brakes.

The generator's job is simple: produce as much as possible. It writes code, revises docs, looks up information, calls tools. The core is outputting actions. The verifier is different: it is not there to help; it is there to doubt. It checks whether the result meets the bar, whether the process drifted, whether a surface pass is a fake pass.

Once these two roles are separated, the system gets much steadier. One focuses on pushing, the other on finding faults; different goals naturally create tension. A truly reliable loop does not let one agent be both athlete and referee; you need different roles to check each other.

References:
- [Anthropic: Harness design for long-running application development](https://www.anthropic.com/engineering/harness-design-long-running-apps)
- [Anthropic Workshop: Build Agents That Run for Hours](https://www.youtube.com/watch?v=mR-WAvEPRwE)
- [Reddit: Are AI "loops" just agents grading their own homework?](https://www.reddit.com/r/codex/comments/1ucbi24/are_ai_loops_just_agents_grading_their_own/)

## 22. Why can no model output beat a reliable verifier?

Because generation capability answers "can it be produced," while verification answers "is what was produced correct?" The latter is scarcer in engineering.

However strong the model, at best it writes better, thinks better, fills in better. But once a loop reaches a real environment, what is truly expensive is misjudgment. A result that looks decent but is actually wrong is often more troublesome than a direct error, because an error makes you stop, while a fake success makes you keep stacking on top.

So a strong generator raises the ceiling; a strong verifier holds the floor. Often whether a system is usable is not about how brilliant it looks at its smartest, but whether it can steadily block the obviously wrong.

References:
- [Anthropic: Demystifying evals for AI agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents)
- [OpenAI Cookbook: Build an Agent Improvement Loop with Traces, Evals, and Codex](https://developers.openai.com/cookbook/examples/agents_sdk/agent_improvement_loop)
- [Reddit: After going through 15 agentic-loop papers, the thing that predicts success is the verifier, not the model](https://www.reddit.com/r/AI_Agents/comments/1uh0gfa/after_going_through_15_agenticloop_papers_the/)

## 23. How to tell open loop from closed loop?

The simplest view: after the action is done, does the system come back to read the result and decide the next step?

An open loop is more like a straight line. You give a task, it executes, the flow pushes forward. A closed loop circles back to re-examine the scene round after round; the previous round's tests, logs, page state, and user feedback all become the next round's input. The difference is not the number of steps, but whether feedback flows back.

One more easily confused point: many people lump harness and loop together. Actually the harness is more like the kitchen, deciding where tools, permissions, files, and state live; the loop is the recipe, deciding what to do this round, what to verify, when to continue. No matter how good the kitchen, if after acting it does not come back to look at the result, it is still just an open loop.

References:
- [Anthropic: Building Effective AI Agents](https://www.anthropic.com/research/building-effective-agents)
- [OpenAI: Unrolling the Codex agent loop](https://openai.com/index/unrolling-the-codex-agent-loop/)
- [Martin Fowler: Harness Engineering for Coding Agent Users](https://martinfowler.com/articles/harness-engineering.html)
- [Firecrawl: Loop Engineering](https://www.firecrawl.dev/blog/loop-engineering)

## 24. When is an open loop worth the risk over a closed loop?

When the task is cheap enough, reversible enough, and the cost of failure is low, an open loop is actually more cost-effective.

Batch rewriting, low-risk information organizing, one-off asset generation: even if these drift a bit, they will not cause disaster. If you force a lot of verification and loops here, the system gets heavy, and the payoff may not be worth it.

The value of a closed loop is most obvious in high-risk and high-uncertainty tasks. But if the task itself is light and you forcibly apply a full closed loop, you often get an absurd situation: the checking cost is more expensive than the task itself. So not every task should be locked down tight; in some scenarios, open is actually more agile.

References:
- [Anthropic: Building Effective AI Agents](https://www.anthropic.com/research/building-effective-agents)
- [OpenAI: New tools for building agents](https://openai.com/index/new-tools-for-building-agents/)
- [Developers Digest: Managed Agents vs LangGraph vs Rolling Your Own](https://www.developersdigest.tech/blog/managed-agents-vs-langgraph-vs-diy-2026)

## 25. Why is a closed loop steadier, yet not necessarily more surprising?

Because the core of a closed loop is convergence, while surprises often come from divergence.

Tighten the checks, pull the feedback close, pin the goal fine, and the system is of course steadier. It is less likely to run away or let bad results through. But the cost is that its space to explore strange directions also shrinks. Many closed-loop systems end up more and more like a competent employee, rather than a quirky genius who occasionally gives you inspiration.

So a closed loop is strong at delivery, not necessarily at unexpected discovery. If your goal is stable production, it is great; if your goal is non-standard answers, you need to leave it some room to err and detour.

References:
- [Anthropic: Harness design for long-running application development](https://www.anthropic.com/engineering/harness-design-long-running-apps)
- [OpenAI: Harness engineering: leveraging Codex in an agent-first world](https://openai.com/index/harness-engineering/)
- [Hacker News: The unreasonable effectiveness of an LLM agent loop with tool use](https://news.ycombinator.com/item?id=43998472)

## 26. Why must a loop's state be externalized, not just held in context memory?

Because context is more like a temporary workbench; relying on it as a reliable store will eventually go wrong.

The model can of course remember a bit of the prior text, but that memory is both expensive and unstable. As rounds lengthen and the window fills, it compresses, forgets, misreads, or simply understands old information wrong. If you push key progress, task state, to-dos, and failure records all into context, the system will eventually restart like amnesia.

So a loop that truly runs long writes state out to the outside. Files, databases, task lists, logs, memory services: these are the long-term state. Context handles the current round; external state handles cross-round continuity.

References:
- [Anthropic: Effective context engineering for AI agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)
- [OpenAI Agents SDK: Results and state](https://developers.openai.com/api/docs/guides/agents/results)
- [LangChain: Context Engineering for Agents](https://www.langchain.com/blog/context-engineering-for-agents)

## 27. Why do artifacts, contracts, and logs become the base of a loop?

Because once a loop crosses two or three rounds, you can no longer bet on "it should remember what just happened."

Artifacts keep the scene: the produced files, page screenshots, evaluation results. Contracts set the criteria: what counts as pass, what counts as fail, what counts as needing human takeover. Logs keep the trail: letting you know why it reached this step. Without these three, a loop looks like a construction site that only charges forward but has no medical records or construction logs.

Many long-running agents, later on, are not competing on whether the prompt is pretty, but on whether these bases are planted steady. Whether you can check the last round, pick up the next, and do post-mortems after incidents depends on these external structures.

References:
- [OpenAI: Harness engineering: leveraging Codex in an agent-first world](https://openai.com/index/harness-engineering/)
- [Anthropic: Harness design for long-running application development](https://www.anthropic.com/engineering/harness-design-long-running-apps)
- [Mem0: Loop Engineering for AI Agents](https://mem0.ai/blog/loop-engineering-for-ai-agents-memory-first-design)

## 28. What shared structure actually compounds a loop?

The key is not running more rounds, but that each round leaves what it learned for the next round to reuse.

This shared structure might be skills, a playbook, templates, evaluation rules, task decomposition methods, a common error list. The point is not the form, but whether it can be reused across tasks. If every problem is solved by human improvisation on the spot, you only get one-time gains, no compounding.

So a loop truly entering the compounding stage usually means the system starts accumulating structured experience. It does not get a little smarter from scratch each time; it hardens effective paths, and later directly applies them to similar problems.

References:
- [OpenAI: Harness engineering: leveraging Codex in an agent-first world](https://openai.com/index/harness-engineering/)
- [OpenAI: Skills](https://developers.openai.com/api/docs/guides/tools-skills)
- [Anthropic: Scaling Managed Agents: Decoupling the brain from the hands](https://www.anthropic.com/engineering/managed-agents)

## 29. Why does worktree go from a nice-to-have to a baseline in loop scenarios?

Because as long as you let multiple tasks run in parallel, iterate repeatedly, and keep modifying code, not isolating the workspace will eventually cause trouble.

Without worktree, multiple loops easily step on each other's files, pollute the environment, overwrite each other's intermediate results. Before you judge whether a change is worth keeping, another task has already washed away the scene. That way, verification becomes fake, rollback becomes hard, and investigation is a disaster.

The point of worktree is not just convenient branching; it is more like giving each loop an independent scene. Only when the scene is isolated are results trustworthy, does verification mean something, and does parallelism avoid mutual pollution.

References:
- [OpenAI: Harness engineering: leveraging Codex in an agent-first world](https://openai.com/index/harness-engineering/)
- [Mike McQuaid: Sandboxes and Worktrees: My secure Agentic AI Setup](https://mikemcquaid.com/sandboxed-agent-worktrees-my-coding-and-ai-setup-in-2026/)
- [Firecrawl: Multi-Agent Orchestration With Codex](https://www.firecrawl.dev/blog/codex-multi-agent-orchestration)

## 30. Why must maker and checker be separated in a loop?

Because the same system being responsible for both "producing the thing" and "judging whether it works" will naturally be biased.

The maker's mental model is pushing the task; it tends to explain, embellish, rationalize its own result. The checker's mental model should be the exact opposite: default to disbelief, default to finding holes, default to doubting boundary conditions. If you cram these two roles into one agent, it will swing between the urge to push and the urge to doubt, and usually the push urge wins.

So separating maker and checker is not just clearer organization; it is to create real opposition inside the system. Without this opposition, a loop easily becomes self-congratulation.

References:
- [Anthropic: Harness design for long-running application development](https://www.anthropic.com/engineering/harness-design-long-running-apps)
- [Anthropic Workshop: Build Agents That Run for Hours](https://www.youtube.com/watch?v=mR-WAvEPRwE)
- [Reddit: Are AI "loops" just agents grading their own homework?](https://www.reddit.com/r/codex/comments/1ucbi24/are_ai_loops_just_agents_grading_their_own/)

## 31. Why does letting the same agent write and verify almost surely overestimate results?

Because it inherits the thinking it just used, rather than standing outside and looking again.

Even people go soft when checking their own writing; models are the same. Just to make some plan cohere and work, the model has already formed an explanatory path in its head. Then asking it to verify, the easiest thing is not to overturn itself, but usually to keep justifying along the original logic.

This is why many loops clearly have a "check" step but still end in fake passes. The problem is not that it did not check, but that the checker and the doer come from the same set of biases. If you do not cut the perspective apart, the check can rarely get hard.

References:
- [Anthropic: Harness design for long-running application development](https://www.anthropic.com/engineering/harness-design-long-running-apps)
- [Reddit: Are AI "loops" just agents grading their own homework?](https://www.reddit.com/r/codex/comments/1ucbi24/are_ai_loops_just_agents_grading_their_own/)
- [Anthropic: Demystifying evals for AI agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents)

## 32. Why does a loop's heartbeat often decide the effect more than the prompt itself?

Heartbeat, plainly, is how the system advances, reports, and continues to the next beat each round. Often this sense of rhythm affects the result more than the wording in the prompt.

Because a loop is not a one-shot deal; it relies on continuous execution. What you let it look at, report, record, and judge each round changes the direction of the next dozens of rounds. A prompt written perfectly, if the heartbeat is messy, the system will still slowly lose control.

So many mature loops, in the end, do not compete on some magic prompt, but on that stable rhythm. Like people at work, excellent teams are often not the best at meetings, but the best at pushing forward on rhythm.

References:
- [OpenAI: Unrolling the Codex agent loop](https://openai.com/index/unrolling-the-codex-agent-loop/)
- [Anthropic: Effective harnesses for long-running agents](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents)
- [OpenAI Agents SDK: Running agents](https://developers.openai.com/api/docs/guides/agents/running-agents)

## 33. Why do automation, skills, and sub-agents combine to look like a complete loop?

Because these three exactly land on three layers. Automation handles triggering, skills handle experience, sub-agents handle division of labor. Take any single one out and it only solves one slice.

Think of a real workbench. Automation is like timers and triggers, deciding when to start. Skills are like the team's operation manual, deciding how to handle this type of task. Sub-agents are like people in different roles, running generation, verification, organizing, and reporting separately. Only this way can the loop push forward while reusing and keeping complexity down.

Many people feel what they lack is some magic agent, and only later realize what they lacked was usually the combination structure. A loop that runs long usually has this layering; it does not rely on one big model to hard-carry everything.

References:
- [Addy Osmani: Loop Engineering](https://addyosmani.com/blog/loop-engineering/)
- [OpenAI: Skills](https://developers.openai.com/api/docs/guides/tools-skills)
- [Anthropic: How we built our multi-agent research system](https://www.anthropic.com/engineering/multi-agent-research-system)

## 34. Why does the engineering difficulty jump once a loop connects to cron, webhook, and trigger?

Because once it no longer relies on a human manually clicking start, the whole system shifts from "tool" to "infrastructure."

When triggered manually, many problems are caught by human instinct. A person checks whether the environment is right, whether the context is fresh, whether the result looks decent. But once connected to cron, webhook, trigger, the system must handle timing, concurrency, retries, duplicate triggers, permissions, and external dependency failures on its own. Places that a person could patch on the fly become formal engineering problems.

So many loops look smooth in the manual phase and suddenly crash once auto-triggered. The problem is often not the idea itself, but that you switched from single-use to continuous running. The threshold jumps up at once.

References:
- [OpenAI: Harness engineering: leveraging Codex in an agent-first world](https://openai.com/index/harness-engineering/)
- [OpenAI Agents SDK: Background mode](https://developers.openai.com/api/docs/guides/background)
- [OpenAI Agents SDK: Webhooks](https://developers.openai.com/api/docs/guides/webhooks)
