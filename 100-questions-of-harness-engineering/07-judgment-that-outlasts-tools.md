# Chapter 7 - Judgment That Outlasts Tools

The final chapter is about judgment: when to stay simple, when to build, how to learn from incidents, how to evaluate a project that may disappear, and how to learn harness engineering without a teacher. Tools expire. Good judgment transfers.

## 87. What does the best harness look like?

It provides exactly the control the task needs - no less and no more. A useful rule is that the diversity of your controls should be at least as rich as the diversity of the task. Too little control causes failures; too much creates cost and friction.

|  | Guides | Sensors |
|---|---|---|
| Deterministic, fast, cheap | Code modifications and fixed transforms | Tests, linters, structural checks |
| Semantic, uncertain, expensive | `AGENTS.md` and skill instructions | AI review and LLM judges |

Guidance without feedback repeats mistakes. Feedback without guidance leaves the system without a way to avoid them. Start with the control the task requires, then add one layer after a measured failure.

1) Martin Fowler on harness engineering https://martinfowler.com/articles/harness-engineering.html

## 88. Should I build a component myself or use an existing one?

Use an existing component when you can adapt it; build only when you have reached a core requirement. OpenAI's agent-first work offers a useful bias toward boring technology: stable interfaces, composability, and familiar tools are easier for agents to use.

They still wrote a small concurrency component instead of using a general library because it had to integrate with their monitoring, have complete test coverage, and behave deterministically. All three conditions mattered. Ask: can I adapt the existing component, is this a core differentiator, and can I fully test it? Build only when all three answers justify it.

1) OpenAI harness engineering https://openai.com/index/harness-engineering/

## 89. How do I read the design philosophy of a harness?

Use four passes: definition, loop, tool boundary, and state record.

First ask whether the author uses a broad or narrow definition of harness. Then trace input assembly, model calls, tool-result injection, and the stop decision. Next inspect the tools, descriptions, and permissions. Finally inspect the state granularity and replay model. DSH's session log is a useful reference because it makes "model-visible means recorded" an explicit invariant.

Practice on DSH and Codex CLI this week. Fill in the same four-field table for both. After that, new harnesses become comparative reading rather than a new vocabulary problem.

1) OpenAI loop anatomy https://openai.com/index/unrolling-the-codex-agent-loop/

2) LangChain Anatomy https://www.langchain.com/blog/the-anatomy-of-an-agent-harness

## 90. Where should I start contributing to open source?

Start with documentation and reproducible bugs. They have the lowest barrier, fastest feedback, and clearest way to build credibility. DSH routes feedback through Discussions, so that is where to look.

Take three steps: correct stale documentation, add minimal reproduction steps to a simple bug, and only then move into core code. Adding the `dsh-plugin` topic to a useful plugin repository is also an ecosystem contribution.

1) Contribution guide https://github.com/deepseek-ai/deepseek-harness/blob/master/CONTRIBUTING.md

2) Discussions https://github.com/deepseek-ai/deepseek-harness/discussions

## 91. What is the most valuable lesson from real incidents?

Learn the method for finding root causes, not the final fix. DSH's public postmortems show why.

One incident disabled filesystem tools because a JavaScript expression marker was interpreted in one configuration field but became a truthy object in another. Snapshot tests reproduced the wrong behavior instead of testing correctness. Another incident misclassified a partial sandbox execution notice as a child-process failure. The general lesson is to test each translation layer explicitly.

Copy the postmortem structure: executive summary, summary, timeline, root cause, guardrails, and lessons. Writing those six sections after your own failure often reveals that the first symptom was not the root cause.

1) Postmortem 0002 https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/postmortem/0002-js-expression-disabled-filesystem-tools.md

2) Postmortem 0004 https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/postmortem/0004-landlock-partial-notice-misclassified-child-failures.md

3) Postmortem index https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/postmortem/README.md

## 92. Why is my colleague better with the same model?

Turn "they tuned it better" into an experiment. Keep the task, model, parameters, and reasoning level fixed; change only the harness or one configuration; compare pass rate, cost, time, and full trajectories.

Use five to ten real tasks as a fixed set. DSH's `fork` is useful here because it creates two branches from the same starting point. The trajectory usually shows differences in tool descriptions or context strategy. Disclose the setup when reporting the result: agent comparisons without harness details are incomplete.

1) Harness-disclosure paper https://arxiv.org/abs/2605.23950

2) DSH session documentation https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/subsystems/session.md

## 93. What happens if I depend on the harness too much?

You outsource judgment and later cannot explain either failure or success. The degradation is quiet: the smoother the tool feels, the less you practice verifying it.

One Hacker News example produced more than 140 pages of rules and zero lines of code. The process was immaculate, but the output was zero. A harness can execute for you; it cannot remove your responsibility to understand and evaluate the result.

Once a month, inspect one complete trajectory and explain why each major decision happened. If you cannot, your dependence has exceeded your understanding.

1) Hacker News example https://news.ycombinator.com/item?id=49285244

## 94. Will harnesses replace programmers?

The evidence supports a shift in work, not a simple replacement story. People who only translate requirements into routine code are under more pressure. People who design environments, define acceptance, build feedback loops, and verify results are moving up the control stack.

OpenAI's team and the appearance of harness engineering roles support that reading. The idea of an outer harness also matters: users can build a control layer around the tool itself. That skill is becoming more valuable, not less.

1) OpenAI harness engineering https://openai.com/index/harness-engineering/

2) Martin Fowler on outer harnesses https://martinfowler.com/articles/harness-engineering.html

## 95. How do I build my own harness judgment?

Record one reusable lesson every time you hit a failure. Judgment grows from the quality of your postmortems, not the number of evaluations you have read.

Use four fields: symptom, root cause, guardrail, and reuse condition. "DSH has a bug" is not reusable. "On Windows, native PowerShell avoids the MSYS2 exit-127 launch failure" is reusable. After about thirty entries, new failures start looking like variations of old ones.

```text
# Four-field failure log
Symptom:        What happened, without emotion
Root cause:     Which harness factor failed
Guardrail:      An executable prevention step
Reuse condition: When this lesson applies
```

1) DSH postmortem index https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/postmortem/README.md

## 96. There is a harness job, but nobody can teach me. How do I self-study?

Practice across seven capability layers: execution and sandboxing, tool interfaces, context and memory, lifecycle orchestration, observability, evaluation, and governance.

| Layer | Practice project | Acceptance test |
|---|---|---|
| Execution and sandbox | Configure three DSH permission levels | A real task proves the sandbox works |
| Tool interface | Write one plugin | It appears in Settings and unloads cleanly |
| Context and memory | Run compaction and add memory | Three facts survive compaction |
| Lifecycle orchestration | Build a worker-plus-reviewer flow | The contract is explicit |
| Observability | Connect Langfuse and inspect a trace | Four metrics are tracked |
| Evaluation | Build a ten-task private benchmark | Before-and-after results exist |
| Governance | Write permissions and rehearse an upgrade | The four production gates pass |

Spend one or two weeks per layer and start with the weakest layer rather than following the table mechanically.

1) Agent Harness Engineering survey https://picrew.github.io/LLM-Harness/main.pdf

2) Langfuse https://github.com/langfuse/langfuse

3) DSH documentation https://github.com/deepseek-ai/deepseek-harness

## 97. A popular open-source harness can still shut down. How do I judge whether to follow it?

Stars measure attention, not lifespan. Roo Code was a visible example: after substantial popularity, it announced a shutdown. Evaluate maintenance continuity and your exit route instead.

Every six months, check recent commits, issue response, license permissions for a rescue fork, maintainer concentration, and whether your data and configuration can be exported. Repository moves are not automatically bad, but every move is a reason to re-check trust.

```text
# Five checks for project continuity
1. Recent commits
2. Issue response time
3. License and ability to fork
4. Number of maintainers
5. Export path for data and configuration
```

1) Roo Code repository https://github.com/RooCodeInc/Roo-Code

2) OpenCode https://github.com/anomalyco/opencode

3) Goose https://github.com/aaif-goose/goose

## 98. What if DSH is abandoned after two months?

You still keep the durable part if you learned the ideas rather than memorized the commands. Agent loops, layered configuration, event history, and permission tiers also appear in Codex, Fowler's writing, and the academic capability map.

The transferable list is short: input-reasoning-tool-result loops, profile-bundle-patch layering, replayable traces, and graduated permissions. Keep commands in a versioned cheat sheet and discard them when they expire. Keep the design principles in your notes.

1) OpenAI loop anatomy https://openai.com/index/unrolling-the-codex-agent-loop/

2) DSH architecture https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/architecture.md

## 99. What is the shortest path for an ordinary user who wants to use it?

Three steps: choose a small task you can verify, run the default preset, and change one variable at a time when the result is poor. Avoid YAML during the first month; it is a guardrail for learning, not a permanent ban.

When something fails, check the known categories first: Windows shell environment, key or provider configuration, and long tasks with no completion notification. Read the session log before assuming the product is unusable.

1) Official quick start https://deepseek.com/harness/en/

2) Community FAQ https://www.aixq.cc/62316.html

## 100. Is it too late to enter harness engineering?

The field is real and active: roles are being posted, official documentation is expanding, plugin ecosystems are growing, and surveys are being published. Nobody can honestly promise how long the current window will last.

The durable asset is engineering judgment. A failure log, a seven-layer capability map, and a private benchmark remain useful after a product changes owners or disappears.

The best entry point is not a forecast. Pick one real task and run it today. The answer to the book's first question still holds: when AI talks nonsense, the problem is not always the model. Build judgment about everything around it.

1) LangChain Anatomy https://www.langchain.com/blog/the-anatomy-of-an-agent-harness

2) DSH repository https://github.com/deepseek-ai/deepseek-harness
