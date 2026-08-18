# Chapter 1 - The Hidden Battlefield Beyond the Model

You have probably seen this: the same model feels fast and reliable for a colleague, but makes things up or loops forever for you. A newer model does not necessarily fix it. The problem is often not the horse but the harness. This chapter defines the word, explains why major labs are talking about it, and shows why changing the harness can matter more than changing the model.

## 1. Is confident nonsense really caused by a weak model?

Not always. A weak model can hallucinate, but more often it never received what it needed: no tool to look up the missing material, no background context, and no one checking the result. Those responsibilities sit outside the model, in the system around it.

The useful formula is `Agent = Model + Harness`. The model reasons; the harness gives it context and tools, keeps it inside the task boundary, and checks the result. Anthropic's own engineering writing describes agents that choose the first plausible solution and mark work complete without enough testing. A stronger model does not automatically cure either behavior. The surrounding system has to enforce decomposition, progress tracking, and verification.

LangChain puts the boundary even more sharply: out of the box, a model consumes text or images and emits text. It has no memory between calls, no loop, no code execution, and no live knowledge. The harness supplies those things. Even a chat box is a harness feature: a loop that retains history and appends new messages.

When an agent talks nonsense, inspect the run before replacing the model. Did it have the information it needed? Was the information correct? Did anything verify the result? Those three questions usually identify the missing layer.

1) LangChain's anatomy of an agent harness https://www.langchain.com/blog/the-anatomy-of-an-agent-harness

2) Anthropic's effective harnesses for long-running agents https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents

## 2. Everyone says agents are powerful. Why does mine fail immediately?

The gap is between a demo and a real task. A demo takes one or two short steps. A real task may take dozens: context grows, tools are called repeatedly, and intermediate state accumulates. Those are exactly the responsibilities a harness has to manage.

The failure reports are remarkably consistent: context overflow, wrong tool choice, infinite loops, lost state, and no way to reconstruct what happened. In one comparison, the same model connected to eight harnesses completed between 68% and 88% of the same 25 tasks. The model stayed fixed; the harness moved the result by twenty percentage points.

Do not blame the harness by reflex either. Record the latest failure in four layers: task conditions, visible context, tool calls, and the evidence used to declare completion. Once those are written down, the faulty layer usually stops being mysterious.

1) Hacker News discussion on the DeepSeek Harness launch https://news.ycombinator.com/item?id=49285244

2) Zhihu discussion on DeepSeek Harness https://www.zhihu.com/question/2071335529577239335

3) Hacker News discussion of OpenAI's harness article https://news.ycombinator.com/item?id=48416264

## 3. What exactly is a harness? Is it really the gear around the model?

Use this working definition: a harness is everything in an agent other than the model - context management, tools, permissions, state, execution loops, and verification. The model is the horse; the harness is the reins, saddle, and brake that let it pull a cart without running away.

Hugging Face draws a narrower distinction. A scaffold defines behavior through system instructions, tool descriptions, output parsing, and context management. The harness is the execution layer that calls the model, handles tools, and decides when to stop. Claude Code documentation is often cited as the broad version: Claude Code is the agentic harness around Claude.

The boundary varies by author. Martin Fowler's definition is broad; the Hugging Face glossary is narrower. Anthropic has used the term but has not issued a single formal definition, so do not attribute a definitive definition to Anthropic. The word came from physical horse gear, then moved through test harnesses and evaluation harnesses into agent systems.

When explaining it to a beginner, one sentence is enough: a large model is a powerful horse, and the harness is the equipment that helps it do useful work without crashing.

1) Martin Fowler on harness engineering https://martinfowler.com/articles/harness-engineering.html

2) Hugging Face agent glossary https://huggingface.co/blog/agent-glossary

## 4. Why are major companies hiring harness engineers? Is this an algorithm or systems role?

It is a systems role. The job is about system design, toolchains, sandbox permissions, observability, and evaluation, not primarily about training models. Public hiring and engineering posts from Tencent, DeepSeek, and OpenAI all point in that direction.

OpenAI's harness engineering article gives the clearest practical description: when agents write the code, human engineers spend their time designing the environment, specifying the work, and building feedback loops. The code is generated by the agent, but the conditions that make good code possible are built by engineers.

OpenAI also published a useful scale reference: three engineers used agents to produce roughly one million lines of code and 1,500 pull requests in five months, averaging 3.5 PRs per person per day. The line to remember is: "Humans steer. Agents execute." Engineers are not gone; the control surface has moved upward.

If you are considering a transition from backend engineering, ask whether you can design tool interfaces, control sandboxes and permissions, and build observability and evaluation. Those skills matter more here than model training.

1) 36Kr profile of DeepSeek's harness team https://m.36kr.com/p/3819926608204164

2) OpenAI harness engineering https://openai.com/index/harness-engineering/

## 5. Why do recent official materials use "harness" while OpenAI's Chinese translation says "engineering technology"?

Because OpenAI chose an official Chinese rendering in its localized article: *Engineering Technology: Leveraging Codex in an Agent-First World*. The translation is a fact, but it has not settled the community's terminology. Chinese readers also use phrases meaning horse-gear engineering, steering engineering, or simply keep `harness` in English.

The English term carries a useful image and the localized phrase does not. It also collides with the broader meaning of software engineering. A practical writing rule is to write `harness` the first time with a short explanation, then keep the English term afterward.

The timeline is more important than the translation dispute: Anthropic used the term in an engineering article in late 2025; OpenAI published agent-loop and harness articles in early 2026; LangChain proposed `Agent = Model + Harness`; Martin Fowler published a longer taxonomy; and research papers began arguing that agent comparisons should disclose their harnesses. A blog term became an engineering concern and then a job description within months.

1) OpenAI's Chinese translation https://openai.com/zh-Hans-CN/index/harness-engineering/

2) Anthropic's harness article https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents

## 6. I keep tuning the prompt and nothing improves. What layer is missing?

Prompt engineering, context engineering, and harness engineering are best understood as nested layers. Prompt engineering changes the input wording. Context engineering decides what information the model sees at each step. Harness engineering designs the complete control system around those choices: tools, orchestration, verification, and governance.

Anthropic describes context engineering as selecting and maintaining the optimal set of tokens at inference time. It includes retrieval, compression, memory, tools, MCP, and message history. Prompt writing is usually a one-time act; context engineering is repeated curation before every call.

Use a simple triage question: does the task need the model to know more, or to do more? The first is usually a context gap and may need retrieval. The second is a harness gap and may need tools or a better execution loop. Better wording cannot give a model a filesystem or reliable verification.

1) Anthropic on context engineering https://www.anthropic.com/engineering/effective-context-engineering

2) Martin Fowler's layered view https://martinfowler.com/articles/harness-engineering.html

## 7. How do harness, prompt, MCP, and RAG relate?

They are different layers. A harness is the whole execution system. A prompt is the input text. MCP is a protocol for connecting models to external tools. RAG retrieves external information and places it into context.

| Term | What it is | Layer | Plain-language analogy |
|---|---|---|---|
| harness | Execution system for loops, tools, permissions, memory, and verification | System | The house |
| prompt | Input text sent to the model | Input | Instructions to the tenant |
| MCP | Open protocol for connecting external tools | Interface | A standard outlet |
| RAG | Retrieval before generation | Knowledge supply | Delivery of the right books |

Installing an MCP server only solves the connection. The harness still decides whether the model can use the tool, how the tool is described, how results return, and what happens on failure. A standard outlet does not mean the house has working wiring or useful appliances.

1) DeepSeek Harness glossary https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/glossary.zh.md

2) Hugging Face agent glossary https://huggingface.co/blog/agent-glossary

## 8. Why did the same model jump from around rank 30 to the top five after changing the harness?

Because the experiment changed only the harness. LangChain kept the model fixed on Terminal-Bench 2.0 and improved the system prompt, tool setup, environment context, time budget, loop detection, and reasoning allocation. The score rose from 52.8% to 66.5%, moving from outside the top 30 to the top five.

The most useful detail is the "reasoning sandwich": spend the strongest reasoning budget on planning and verification, and use a cheaper level during routine execution. The model did not change; the surrounding decisions did.

| Change | Improvement | Result |
|---|---:|---|
| Harness only | +13.7 percentage points | 52.8% -> 66.5%, top 30 -> top 5 |
| Stronger model in the comparison | About +6.8 percentage points | A common smaller gain |

Keep the conditions attached when quoting these numbers: Terminal-Bench 2.0, fixed model, harness changes only. It is a single experiment, not a universal promise.

1) LangChain's write-up https://www.langchain.com/blog/improving-deep-agents-with-harness-engineering

2) Terminal-Bench 2.0 leaderboard https://www.tbench.ai/leaderboard/terminal-bench/2.0

## 9. Why can changing the harness matter more than changing the model?

Long tasks amplify small control differences. Every context decision, recovery path, state handoff, and completion check is repeated dozens of times. A small advantage per step becomes a large advantage across the whole run.

Research and practical comparisons point to the same mechanism: on long-horizon work, harness variance can exceed model variance and can even reverse model rankings. The main amplifiers are context selection, accumulated tool errors, cross-step state, and the stop decision.

LangChain also gives an important caveat: some harness patches are bandages for current model weaknesses and may become unnecessary as models improve. That does not erase their current value. It means the useful abstraction is to measure the improvement and revisit the patch later.

1) Research on disclosing harnesses https://arxiv.org/abs/2605.23950

2) LangChain's comparison https://www.langchain.com/blog/improving-deep-agents-with-harness-engineering

## 10. Why does the agent finish without notifying me?

In the current version, completion notification is simply not a finished feature. Long tasks may finish without a visible alert; image input may fail because DeepSeek models are text-only; and two tasks sharing one directory may overwrite each other's output.

DeepSeek Harness is still a developer preview aimed at people building agent harnesses. Core plugins and APIs are expected to change. The practical substitute for a notification is the session log: when you return to the browser, the trajectory shows what happened instead of making you guess.

```text
# Three rules before starting batch work
1. Give every task its own directory.
2. Write the acceptance checklist before the run.
3. Poll long-running work yourself; do not assume completion notifications exist.
```

1) DeepSeek Harness product page https://deepseek.com/harness/en/

2) GitHub Discussions https://github.com/deepseek-ai/deepseek-harness/discussions

## 11. Can the Chinese translation "engineering technology" become accepted terminology?

It may remain disputed. The official translation is real, but the community values the original metaphor and uses several alternatives. The phrase also overlaps with ordinary software engineering, which makes it less precise in conversation.

The precedent is `vibe coding`: several Chinese translations circulated for months without a single winner. The stable technical practice is simple: explain the term once, keep `harness` afterward, and do not pretend the community has reached a consensus it has not reached.

1) OpenAI's Chinese translation https://openai.com/zh-Hans-CN/index/harness-engineering/

2) Community terminology discussion https://m.okjike.com/topics/55fadac08cc2e30e00e2e42a

## 12. Why is the harness an invisible battlefield?

The interface shows the model's words, not the four control layers that determine whether the work succeeds: context management, tool boundaries, loop control, and verification with replay.

These controls work in pairs. Guidance without feedback becomes a rule nobody checks. Feedback without guidance means the same mistake repeats. Anthropic's long-running-agent work demonstrates a practical pattern: initialize a machine-readable feature list as not passing, then let later agents mark items as passing while forbidding them from deleting or weakening tests.

When evaluating an AI product, ask four questions instead of only asking which model it uses: How is context managed? How are tools restricted? How are long tasks controlled? How are results verified? Those questions expose the harness.

1) Martin Fowler's guides-and-sensors taxonomy https://martinfowler.com/articles/harness-engineering.html

2) Anthropic on long-running agents https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents

## 13. Why does the same model have a different fate in a different harness?

The harness inserts several decisions between you and the model. A useful six-factor checklist, drawn from the Composio comparison, is:

```text
# Six factors to verify one at a time
1. System instructions   What extra instructions does the harness add?
2. Tool descriptions      How are tools named, described, and exposed?
3. Context management    What is deleted, compressed, or persisted?
4. Planning              Does it plan first or improvise step by step?
5. Error recovery        Can the model understand and correct failures?
6. Verification          Who decides that the task is complete?
```

Test one factor at a time with the same task, model, and parameters. The comparison also carries a warning: its best-performing harness used a different reasoning level and official APIs for most tasks, so the comparison is not perfectly controlled. The six factors are both an analysis framework and a lens for reading benchmark claims.

1) Composio comparison https://composio.dev/content/best-ai-agent-harnesses

2) LangChain's industrial comparison https://www.langchain.com/blog/improving-deep-agents-with-harness-engineering

## 14. What responsibility does each kind of harness take on?

The phrase "everything outside the model" can be divided at different points. Some products deliver a finished house, some provide a foundation, and some focus on orchestration.

| Type | Examples | Responsibility |
|---|---|---|
| Vertically integrated product | Claude Code | Finished, opinionated, and tightly integrated |
| Open foundation | DeepSeek Harness, OpenCode, Goose | Extensible runtime and composition primitives |
| Orchestration layer | LangGraph, AutoGen | Workflow graphs or multi-agent coordination |
| CLI-oriented harness | Codex CLI | Open tooling with detailed sandbox controls |

Stars are not a lifespan guarantee. Roo Code had substantial popularity and still announced its shutdown. Check recent commits, issue responses, license terms, maintainer concentration, and your ability to export data before choosing a foundation.

```text
# Two questions before choosing
1. Do you want a finished product or a foundation?
2. Do you want managed credentials or BYOK control?
```

1) OpenAI Codex CLI https://github.com/openai/codex

2) OpenCode https://github.com/anomalyco/opencode

3) Goose https://github.com/aaif-goose/goose
