# Chapter 5 · Engineering in Practice and Real Workflows

## 71. What tasks are most worth upgrading first from single-shot prompting to a loop?

The most worth upgrading are usually those that recur, have similar steps, and still need a回头 check on the result.

A more practical judgment method is the four-step staircase. Layer one: first smooth out single-shot prompting. Layer two: make it a turn-based loop, letting it read code, act, run checks on its own. Layer three: if done is clear, add a goal-based loop. Layer four: only when the task is high-frequency and stable, consider time-based or proactive. Do not skip the order.

So the tasks most worth upgrading first are those you have manually run many times, to the point you can almost recite what to remind it to do next. Those jobs show effect fastest and make the loop steadiest most easily.

References:
- [OpenAI: A practical guide to building AI agents](https://openai.com/business/guides-and-resources/a-practical-guide-to-building-ai-agents/)
- [Addy Osmani: Loop Engineering](https://addyosmani.com/blog/loop-engineering/)
- [GitHub: loop-engineering daily triage example](https://github.com/cobusgreyling/loop-engineering/blob/main/examples/grok/daily-triage.md)

## 72. What tasks look loop-worthy but are actually not worth automating?

High frequency does not mean worth a loop. What is truly not worth it is often tasks with extremely high judgment cost, environments that change too fast, or consequences of failure that are very heavy.

Some things look repetitive on the surface, like complex negotiation, sensitive approval, fuzzy strategic judgment, but each time the truly hard part is different. If you force a loop, you likely only automate the surface actions, not the truly valuable layer of judgment.

So the "worth it" question looks not just at how often the task appears, but more at how much structure inside it can be stably reused. If the structure is unstable, the faster you put it on a loop, the harder it is to收 later.

References:
- [Anthropic: Building Effective AI Agents](https://www.anthropic.com/research/building-effective-agents)
- [Developers Digest: Managed Agents vs LangGraph vs Rolling Your Own](https://www.developersdigest.tech/blog/managed-agents-vs-langgraph-vs-diy-2026)
- [Stack Overflow Blog: What the AI hype gets wrong](https://stackoverflow.blog/2026/05/18/what-the-ai-hype-gets-wrong/)

## 73. Why are bug fixing, doc maintenance, and triage especially suited to loops?

Because all three kinds of tasks are alike: information must be gathered first, actions done step by step, results still checked回头.

Fixing a bug: first reproduce, then locate, then change, then run tests. Doc maintenance: first find the change, then align facts, then update, then verify. Triage: first aggregate information, then classify, then judge priority, then output a handling suggestion. None of these flows can be cleanly done in one prompt, but they are structured enough to suit closed-loop推进.

So once these three kinds of tasks become loops, the payoff is often especially obvious. Because what you save is not just one prompt sentence, but more of the entire repeated judgment chain.

References:
- [MindStudio: Production Error Sweep Loop That Runs Every Night](https://www.mindstudio.ai/blog/production-error-sweep-loop-nightly-agent)
- [Jescalada: Auto-triage GitHub issues with an AI agent and Actions](https://jescalada.com/blog/2026-04-12-auto-triage-github-issues-ai-agent-actions/)
- [Cursor Automation: Triage failed GitHub Actions](https://cursor.com/marketplace/automations/triage-github-workflow-failures)

## 74. Before connecting a loop to real business, which risk points should be locked down first?

First lock down these five points: permissions, data boundaries, false triggers, false success, human backstop. And preferably write them into real files, not just keep them in your head.

Many teams only care about getting the loop running at first, and only later realize the real danger is it running too smoothly. Permissions should be written into config like `settings.json`; project boundaries and no-go zones into resident docs like `CLAUDE.md`; verification steps into places that can run repeatedly like hooks, skills, evaluation scripts. Only this way is risk control not just a verbal reminder.

Before connecting to business, ask first: if it goes wrong, how will it break, down to which layer, who takes over. If you cannot answer this clearly, do not rush to automate.

References:
- [OpenAI Agents SDK: Guardrails](https://developers.openai.com/api/docs/guides/agents/guardrails-approvals)
- [Martin Fowler: Harness Engineering for Coding Agent Users](https://martinfowler.com/articles/harness-engineering.html)
- [Ryan Lopopolo / OpenAI: Harness engineering](https://openai.com/index/harness-engineering/)
- [Sherlocks AI: Why AI Agents Fail in Production](https://www.sherlocks.ai/blog/why-ai-agents-fail-in-production)

## 75. Why do support loops, SEO loops, and product loops most easily compound?

Because all three kinds of tasks persist long-term, and each round leaves assets for the next.

A support loop leaves problem classifications, handling templates, escalation rules. An SEO loop leaves keyword judgments, page update rules, content structure experience. A product loop leaves user feedback patterns, priority judgment frameworks, post-mortem structures. None are one-off tasks; they instead accumulate shared structure the more they run.

This is the most fascinating part of compounding. Today you did not just complete one round of actions; you also paved the way for the next dozens of rounds. The more reusable structure there is, the lower the loop's marginal cost.

References:
- [MindStudio: Production Error Sweep Loop That Runs Every Night](https://www.mindstudio.ai/blog/production-error-sweep-loop-nightly-agent)
- [GitHub: durable-support-triage](https://github.com/gunnargrosch/durable-support-triage)
- [OpenAI: An open-source spec for Codex orchestration: Symphony](https://openai.com/index/open-source-codex-orchestration-symphony/)

## 76. What wall does a loop hit first when truly entering team flow?

Usually not model capability; the first wall is often organizational friction.

Who trusts the result, who receives the failure, who defines done, who bears the permission responsibility, who maintains the rules: once no one makes the call, the loop can only stay at the demo level. When an individual uses it, a person's mental tacit understanding can still turn it; in a team, all that tacit understanding must be made explicit.

So truly connecting a loop into team flow, the first wall is often the collaboration structure, not the technical detail. If the system wants to run long, someone must first be willing to work together by the same set of rules.

References:
- [OpenAI: Harness engineering: leveraging Codex in an agent-first world](https://openai.com/index/harness-engineering/)
- [Anthropic: Scaling Managed Agents](https://www.anthropic.com/engineering/managed-agents)
- [Stack Overflow Blog: What the AI hype gets wrong](https://stackoverflow.blog/2026/05/18/what-the-ai-hype-gets-wrong/)

## 77. Why does a loop that works for an individual suddenly fail in a team?

Because much of the "invisible context" in a personal loop evaporates instantly in a team.

When you run it yourself, much judgment is simply not written down. You know which directory is dangerous, which files not to touch, how to patch if this round fails. But in a team, if these are not externalized, others taking over are like entering an unfamiliar scene, and the system also starts distorting due to lack of shared context.

So an individual being able to run it only means you yourself can carry it. A team being able to run it means this structure can stand even脱离 you.

References:
- [OpenAI: Harness engineering: leveraging Codex in an agent-first world](https://openai.com/index/harness-engineering/)
- [Anthropic: Effective context engineering for AI agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)
- [Anthropic: Scaling Managed Agents](https://www.anthropic.com/engineering/managed-agents)

## 78. Which knowledge must be sedimented into skills for a loop to run long-term?

Any knowledge that recurs and is not worth re-explaining each time should be sedimented into skills.

The six types most worth sedimenting are usually: task decomposition playbooks, directory maps, available commands, verification checklists, common pitfalls, human escalation conditions. Look at many projects that run long-term, and a structure very much like `CLAUDE.md + skills/ + hooks/ + MEMORY.md` eventually appears. They all do the same thing: turn scattered experience into work assets that can be directly called next time.

What makes skills truly valuable is letting the loop take fewer detours. You move experience into the system, and the next round does not need a person to patch holes on the spot.

References:
- [OpenAI: Skills](https://developers.openai.com/api/docs/guides/tools-skills)
- [Ryan Lopopolo / OpenAI: Harness engineering](https://openai.com/index/harness-engineering/)
- [Addy Osmani: Loop Engineering](https://addyosmani.com/blog/loop-engineering/)

## 79. Why does a loop often force you to fill in the engineering?

Because the engineering debts that single-shot prompting could paper over all get exposed the moment a loop starts.

Unclear directories, unsaved state, no logs, weak verification, messy permissions, vague task definitions: these might be barely held together by human experience normally. But once you want the system to run continuously, they all become explicit failures. A loop does not cover engineering problems for you; it amplifies them until you must deal with them seriously.

So many people just starting with loops mistakenly think it is a laziness tool. Only after really doing it do they find it is more like an engineering health check. Wherever it is weak, it immediately sees the light.

References:
- [OpenAI: Harness engineering: leveraging Codex in an agent-first world](https://openai.com/index/harness-engineering/)
- [Anthropic: Effective harnesses for long-running agents](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents)
- [Medium: Top Skills Every Developer Needs in 2026](https://medium.com/devs-community/top-skills-every-developer-needs-in-2026-beyond-prompt-engineering-233178d3ceec)

## 80. When a loop writes PRs, opens tickets, edits docs, which actions must keep a human gate?

Any action that directly changes external facts, affects team collaboration rhythm, or may create irreversible consequences should keep a human gate.

For example, sending a formal PR, merging changes, closing an issue, editing shared docs, touching external notifications, writing external user messages: once these go wrong, the impact has already spread beyond the system internals. You can of course let the loop prepare content first, draft suggestions first, run pre-checks first, but whether that final step takes effect is best left for a person to decide.

The human gate is there not because people are slower, but because it is the responsibility switch point. The closer the action is to the real world, the more worth keeping this door.

References:
- [OpenAI Agents SDK: Guardrails](https://developers.openai.com/api/docs/guides/agents/guardrails-approvals)
- [GitHub issue triage example](https://github.com/cobusgreyling/loop-engineering/blob/main/examples/grok/daily-triage.md)
- [Jescalada: Auto-triage GitHub issues with an AI agent and Actions](https://jescalada.com/blog/2026-04-12-auto-triage-github-issues-ai-agent-actions/)

## 81. When should a loop only suggest, not execute directly?

When risk is high, reversibility is low, and responsibility attribution is sensitive, it should only suggest.

For example, security-related changes, production data actions, user communication, pricing strategy, permission changes, legal or compliance content: even if the model's judgment is eighty percent reliable, it is not worth letting it make the final call. Because the missed twenty percent is likely the most expensive twenty percent.

A loop is well suited as a high-quality front-end analyzer, organizing information, listing plans, clarifying risk points. But in some scenarios, its best position is to stop there, and not take that step toward execution.

References:
- [OpenAI Agents SDK: Guardrails](https://developers.openai.com/api/docs/guides/agents/guardrails-approvals)
- [OpenAI: A practical guide to building AI agents](https://openai.com/business/guides-and-resources/a-practical-guide-to-building-ai-agents/)
- [Sherlocks AI: Why AI Agents Fail in Production](https://www.sherlocks.ai/blog/why-ai-agents-fail-in-production)

## 82. Why does letting it run in the background sound convenient but is actually most prone to incidents?

Because once you cannot see it, many slowly-deforming problems get more time to ferment.

Background loops most easily fail around the tenth round, the thirtieth round. Input changed, dependency hung, permission drifted, state file got dirty, scheduled triggers stacked: each alone is not scary, but stacked they get annoying. So do not rush to pursue proactive. The steadier approach is to first run turn-based and goal-based solidly, then fill in monitoring, pause, alerting, human takeover, and only then put it in the background as a resident.

Plainly, background running is not "more worry-free," it just moves the problem from in front of your eyes into the system. If you have no monitoring ability, best not go to this level first.

References:
- [Anthropic: Effective harnesses for long-running agents](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents)
- [OpenAI Agents SDK: Background mode](https://developers.openai.com/api/docs/guides/background)
- [Firecrawl: Loop Engineering](https://firecrawl.dev/blog/loop-engineering)

## 83. What new pitfalls appear when a loop combines with GitHub Actions, cron, webhook?

The most common are duplicate triggers, concurrency clashes, dirty state, external dependency jitter, and auto-retry after failure amplifying the problem.

When you run manually, many of these do not show. Once connected to scheduling and event systems, timing truly gets complex. An event may be received duplicated; a workflow may continue running on old state; a webhook may trigger when you are not ready. Without well-designed deduplication, locks, idempotency, and pause mechanisms, the loop creates accidents for itself at the automation layer.

So GitHub Actions, cron, webhook are not simply "triggers"; they conveniently bring in the troubles of distributed systems too.

References:
- [OpenAI Agents SDK: Webhooks](https://developers.openai.com/api/docs/guides/webhooks)
- [GitHub Community: Actions stuck in Expected](https://github.com/orgs/community/discussions/26698)
- [Stack Overflow: How do I re-run Github Actions?](https://stackoverflow.com/questions/56435547/how-do-i-re-run-github-actions)

## 84. To make multiple loops cooperate, what structure must be unified first?

What must be unified first is usually state, artifact format, task boundaries, and handoff protocol.

The biggest fear in multi-loop cooperation is not who is not smart enough, but who cannot understand whom. One loop records progress in files, another in chat summaries; one writes done as "about ready," another requires test numbers and screenshots. In this situation, opening a few more agents only amplifies the chaos. First define clearly how state is recorded, how artifacts are written, how risk is marked, how the next step is handed over.

So multi-loop cooperation is more like building a pipeline than hiring a few more people to help. Unify the structure first, then information can flow.

References:
- [OpenAI: An open-source spec for Codex orchestration: Symphony](https://openai.com/index/open-source-codex-orchestration-symphony/)
- [Anthropic: How we built our multi-agent research system](https://www.anthropic.com/engineering/multi-agent-research-system)
- [Firecrawl: Multi-Agent Orchestration With Codex](https://www.firecrawl.dev/blog/codex-multi-agent-orchestration)

## 85. Why does shared artifacts more easily become a new bottleneck the more a loop runs?

Because a shared artifact starts as an asset, but at scale becomes a transit hub.

Everyone writes into it, everyone reads from it; once versions multiply, quality varies, naming gets messy, the artifact itself starts creating friction. Which copy to trust, which is latest, who can overwrite, which are expired: these questions gradually replace "is there an artifact at all" and become the new bottleneck.

So shared artifacts bring reuse, but also governance cost. The more it runs, the earlier this problem surfaces.

References:
- [OpenAI: Harness engineering: leveraging Codex in an agent-first world](https://openai.com/index/harness-engineering/)
- [Anthropic: Effective context engineering for AI agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)
- [OpenAI: Skills](https://developers.openai.com/api/docs/guides/tools-skills)

## 86. What team culture can actually digest loop engineering?

It must be a culture willing to write judgments down, externalize processes, and fix failures as system problems.

If the team culture relies on word of mouth, on hero figures putting out fires on the spot, on everyone figuring it out themselves, then loops struggle to grow. Because what it most needs is explicit rules, reusable structures, traceable traces. Plainly, loops like institutionalized environments, and do not like environments where "everyone has it in their head."

So whether a team can digest loops is not just about the tech stack, but also about whether it is willing to sediment experience into public assets.

References:
- [OpenAI: Harness engineering: leveraging Codex in an agent-first world](https://openai.com/index/harness-engineering/)
- [Anthropic: Scaling Managed Agents](https://www.anthropic.com/engineering/managed-agents)
- [Medium: Top Skills Every Developer Needs in 2026](https://medium.com/devs-community/top-skills-every-developer-needs-in-2026-beyond-prompt-engineering-233178d3ceec)
