# Chapter 6 - Engineering for Production

A demo that runs and a system that does not fail in production are separated by an engineering layer. This chapter covers context, loops, guardrails, observability, cost, and release checks.

## 73. Can a product really ship with zero lines of code written by humans?

OpenAI has demonstrated a version of it: in five months, three engineers used agents to produce roughly one million lines of code and 1,500 pull requests without hand-writing the product code.

That does not remove engineering. It moves engineering into the environment, rules, feedback loops, and verification. Their `AGENTS.md` acts as a map rather than an encyclopedia. Golden principles, background scans, custom checkers, and agent-readable error messages make the repository enforce its own architecture.

Anthropic's experience adds the other half: the most successful agent systems use simple, composable patterns, visible planning, and carefully designed tools. They spent more time improving tool interfaces than prompts because one good guard against a common mistake can remove an entire class of failures.

1) OpenAI harness engineering https://openai.com/index/harness-engineering/

2) Anthropic Building Effective Agents https://www.anthropic.com/engineering/building-effective-agents

## 74. How should I handle context explosion?

Evaluate every compaction design on three points: when it triggers, what it retains, and whether the recovered conversation remains coherent. The goal is not the shortest context; it is the smallest set of high-signal tokens.

Codex uses a threshold-based compaction mechanism that preserves latent continuity rather than merely turning a conversation into a dry bullet list. That mechanism is not automatically portable to DSH. Use DSH's compaction subsystem and test recovery with your own important facts.

1) DSH compaction https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/subsystems/compaction.md

2) Codex agent loop https://openai.com/index/unrolling-the-codex-agent-loop/

3) Anthropic context engineering https://www.anthropic.com/engineering/effective-context-engineering

## 75. The Agent chooses the wrong tool and goes wild. How do I constrain it?

Use hard and soft controls together. Hard controls are an allowlist and schema validation. Soft controls are precise tool descriptions and compact, structured results. A tool description is part of prompt engineering: vague descriptions produce unreliable selection.

Anthropic calls the tool interface an Agent-Computer Interface, or ACI. Design it as carefully as a human interface: make names unambiguous, make common mistakes difficult, and test many inputs to see how the model actually uses the tool. More tools are not automatically better; one comparison found that the harness with the most calls passed no more tasks than the harness with the fewest.

1) Anthropic ACI guidance https://www.anthropic.com/engineering/building-effective-agents

2) Permission presets https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/subsystems/permission-presets.md

## 76. How do I break an Agent's infinite loop?

Use loop detection, timeouts, and reasoning budgets together. A step limit is a last-resort safety net, not the full solution.

LangChain's public comparison describes a doom-loop detector for repeated terminal behavior. It also shows why maximum reasoning is not always best: an all-high-budget group timed out and scored 53.9%. Use the strongest reasoning for planning and verification, and a cheaper level for routine execution.

At minimum, configure repeated-behavior detection, a per-task timeout, and task-specific reasoning budgets.

1) LangChain harness comparison https://www.langchain.com/blog/improving-deep-agents-with-harness-engineering

## 77. If state is lost, the session is useless. How should I persist it?

Use an append-only event log as the base. State can then be reconstructed from the event stream rather than depending on a fragile snapshot. DSH's session log supports this model for resume and fork.

Without persistence, every new session is an unbriefed shift worker. The runtime invariant "everything visible to the model is recorded" closes that gap. Also keep important deliverables as files: logs preserve process, files preserve results.

1) DSH session subsystem https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/subsystems/session.md

2) Anthropic long-running agents https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents

## 78. Errors cannot be traced. What should I do?

Use end-to-end logs and a trace ID. DSH's trajectory gives session-level traceability. For aggregation across sessions and agents, use a tracing system such as Langfuse.

The smallest implementation does not need a platform: assign one unique ID per task, attach it to every tool call, and retrieve the complete run by that ID. DSH already records tool arguments and file diffs in its session events, so start with the built-in audit trail before inventing another logging service.

1) Langfuse https://github.com/langfuse/langfuse

2) DSH session subsystem https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/subsystems/session.md

## 79. Can an Agent recover from errors by itself?

It depends on how the harness translates the error. A structured error with type, cause, and next action can help the model correct itself. A raw stack trace often makes it repeat the same mistake.

Error recovery needs three constraints: actionable messages, bounded retries with backoff, and a human escalation path. A small tool-layer error translator that standardizes failures into those three fields is often more valuable than another prompt rewrite. Use the session trajectory to see whether the model understood the error.

1) Composio's six factors https://composio.dev/content/best-ai-agent-harnesses

2) DSH session subsystem https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/subsystems/session.md

## 80. How do I verify that the Agent actually followed the rules?

Build an external verification layer. An agent saying "done" is not proof; Anthropic has documented agents that mark work complete without enough testing.

Use three levels. Assertions check files, formats, and ranges. Scripts turn rules into executable checks. Task-level evaluation measures pass rate. A strong pattern is a machine-readable feature list initialized as not passing, with later agents allowed only to mark items passing and forbidden to delete tests.

```text
# Completion rule
Agent says complete -> run the verification script -> passing means complete.
```

1) Anthropic long-running agents https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents

2) tau-bench paper https://arxiv.org/abs/2406.12045

## 81. How can multiple Agents avoid fighting each other?

Give each agent one responsibility and define messages as contracts. State should be explicit in files or a state machine, not hidden in a shared conversation that every agent can reinterpret.

Draw a contract table for each agent: inputs, outputs, and the authority it yields to during conflicts. Anthropic's patterns range from prompt chaining and routing to parallel work, orchestrator-workers, and evaluator-optimizer loops. Start with one agent plus a workflow; add multiple agents only when the simple design cannot express the job.

1) AutoGen https://github.com/microsoft/autogen

2) LangGraph https://github.com/langchain-ai/langgraph

3) Anthropic workflow patterns https://www.anthropic.com/engineering/building-effective-agents

## 82. What should guardrails block?

Block unauthorized access, sensitive actions, and dangerous commands. The policy should block first and request approval, not silently permit a dangerous operation or block every useful operation forever.

DSH's read-only, workspace-write, and full-access presets provide a practical product pattern. Guardrails AI provides a validation-oriented framework pattern. A good guardrail also makes errors hard to create: accepting absolute paths instead of ambiguous relative paths can eliminate a recurring class of mistakes.

```text
# Guardrail setup
1. Write an allow-never-automatically list of no more than 10 items.
2. Give each item an enforcement point.
3. Trigger each enforcement point once and verify that it blocks.
```

1) Guardrails AI https://github.com/guardrails-ai/guardrails

2) DSH permission documentation https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/subsystems/permission-presets.md

3) Anthropic tool design https://www.anthropic.com/engineering/building-effective-agents

## 83. Which observability metrics matter?

Track four: token flow and cache hits, latency, tool success rate, and failure distribution. Use median and P95 rather than average latency. Tool-call count is a process measure, not an outcome measure.

Cache hits connect directly to cost. Cost per successful task is the most honest headline: total cost divided by successful tasks exposes the money spent on failed work.

| Metric | Question | Common trap |
|---|---|---|
| Token flow | Which step burns tokens? | Re-sending long context |
| Latency | What are median and P95? | Average hides the tail |
| Tool success | Which tool fails independently? | More calls do not mean better output |
| Cost per success | What does each successful task cost? | Total spend alone overstates efficiency |

1) Langfuse https://github.com/langfuse/langfuse

2) Token meter https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/subsystems/token-meter.md

## 84. Costs will not come down. What should I cut first?

Follow this order: inspect token flow, remove redundancy, schedule batch work off-peak, and keep stable prefixes cache-friendly. Only then consider a cheaper model.

The usual offenders are long context resent every turn, large raw results injected back into context, and the full tool list included in every request. A model price reduction cannot compensate for a context design that multiplies tokens.

1) Token meter https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/subsystems/token-meter.md

2) Official pricing notice https://api-docs.deepseek.com/zh-cn/news/news260813/

## 85. Which checklist must pass before production?

Four gates: sandbox, guardrails, replay, and monitoring. Add an upgrade-and-rollback rehearsal during the release-candidate period.

```text
# Production gates
Sandbox    [ ] Write allowlist  [ ] Dangerous paths blocked  [ ] Real task verified
Guardrails [ ] Every rule has a gate  [ ] Every gate triggered once
Replay     [ ] Log grows normally  [ ] A historical run replays end to end
Monitoring [ ] Four metrics tracked  [ ] Someone sees alerts
Drill      [ ] Upgrade and rollback rehearsed
```

1) Sandbox subsystem https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/subsystems/sandbox.md

2) Langfuse https://github.com/langfuse/langfuse

## 86. Which failures appear only in production?

Three are especially dangerous: parallel tasks overwriting the same directory, permission drift, and breaking upgrades. Demos often hide all three because they have one task, one operator, and one version.

Use separate directories for concurrent work. Put permission configuration in version control and review changes. Rehearse an upgrade and rollback. DSH's public postmortems show why snapshot tests can miss a configuration that is syntactically accepted but semantically wrong.

1) Postmortem index https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/postmortem/README.md

2) Sandbox escalation discussion https://github.com/deepseek-ai/deepseek-harness/discussions/201
