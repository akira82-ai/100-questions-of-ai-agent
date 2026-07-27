# Chapter 1 · Foundations and Positioning

## 1. Why do so many people now say prompt engineering is outdated?

A couple of years ago, most people using large models were still doing single-turn Q&A, one-off generation, rewriting, and polishing. Back then prompts really mattered: rephrase a sentence and the result could shift noticeably. It was natural to conclude that the core skill of building AI applications was writing prompts.

But what people build has changed over the last couple of years. More and more are building agents, multi-step tasks, systems that call tools, read files, check their own work, and keep running. Once you reach that stage, prompts still matter, but they are no longer the thing that decides the outcome.

What actually decides success becomes something else: is the task broken down clearly, is the context fed in correctly, can the tools be used, will state get lost, is the result checked, and can it be pulled back when it is wrong. You can write the most beautiful prompt, but if these fall apart, the system still veers off course.

So when people say prompt engineering is outdated, they do not mean it is useless. They mean it is no longer enough. Before, it was the lead actor; now it is closer to the foundation. You still need to know how to write it, but if you can only write prompts and cannot build flows, do verification, or manage context, you will struggle to build an AI system that actually runs.

References:
- [OpenAI Prompt Engineering Guide](https://developers.openai.com/api/docs/guides/prompt-engineering)
- [Anthropic: Effective context engineering for AI agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)
- [Reddit: Is "Prompt Engineer" about to become the next "Growth Hacker"?](https://www.reddit.com/r/PromptEngineering/comments/1t29qlf/discussion_is_prompt_engineer_about_to_become_the/)

## 2. What does loop engineering actually add beyond prompt engineering?

If you strip it to the core, what loop engineering adds is the whole mechanism that lets a model keep working and keep correcting itself.

Prompt engineering is more like stating your request clearly and waiting for the model to answer once. The focus is on how the input is written. Loop engineering takes a big step further: it cares about what the model does after it receives that instruction. How does it break the task down, call tools, read the environment, check results, redo things when they are wrong, and decide when to stop?

So what it adds is not a little prompt trickery, but a complete running chain. Usually several things show up that were not there before: state, tools, steps, verification, memory, and exit conditions. Without these, however articulate the model is, it tends to look smart in round one, drift in round two, and flap around aimlessly by round three.

You can think of it this way: prompt engineering solves how to answer this turn; loop engineering solves how to finish this job.

References:
- [Anthropic: Building Effective AI Agents](https://www.anthropic.com/research/building-effective-agents)
- [OpenAI: A practical guide to building AI agents](https://openai.com/business/guides-and-resources/a-practical-guide-to-building-ai-agents/)
- [Anthropic: Effective context engineering for AI agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)

## 3. Where exactly do loop engineering and harness engineering differ?

The two words look similar, so people keep mixing them up. If you really have to separate them, loop engineering is about how a task cycles, while harness engineering is about what you use to hold that cycle up.

The loop is the rhythm: spot a problem, take an action, check the result, move to the next round. The harness is the scaffold: how tools connect, how state is stored, how permissions are controlled, how logs are kept, how failures retry, and where verification plugs in. The former is closer to method; the latter is closer to the engineering carrier.

That is why you often see a loop fail to run, and on the surface it looks like a prompt problem, but dig down and the real issue is a weak harness. The loop itself is not wrong, but if the base cannot hold it, it scatters further with every round.

References:
- [OpenAI: Harness engineering: leveraging Codex in an agent-first world](https://openai.com/index/harness-engineering/)
- [Anthropic: Demystifying evals for AI agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents)
- [OpenAI: Unrolling the Codex agent loop](https://openai.com/index/unrolling-the-codex-agent-loop/)

## 4. Why is loop engineering about building a system, not writing a prompt?

Because once you actually run a loop, you find that the prompt is only the entry point. Most of the work lives after that one sentence.

You have to decide how the task breaks down, what information to supply, when to call tools, who verifies the result, how to recover after failure, and where to stop. A lot of this does not even live in the prompt; it lives in state management, tool design, verification rules, and workflow orchestration.

So a lot of people start out thinking they are optimizing a model, and only later realize they are actually designing a small system. The model is just one component. What truly stabilizes the result is the system arrangement.

References:
- [OpenAI: Harness engineering: leveraging Codex in an agent-first world](https://openai.com/index/harness-engineering/)
- [Anthropic: Harness design for long-running application development](https://www.anthropic.com/engineering/harness-design-long-running-apps)
- [OpenAI: New tools for building agents](https://openai.com/index/new-tools-for-building-agents/)

## 5. Is loop engineering a genuinely new paradigm, or just old engineering under a new name?

It is a bit of both. It did not appear out of nowhere, but it is not simply a renamed scam either.

The old part is that the engineering world has always talked about automation, feedback loops, state machines, monitoring, testing, and retries. When you say "loop" today, much of its flavor connects to those older concepts. The new part is that the executor in the middle has changed. Before, you hardcoded the flow; today you hand part of the judgment to the model, so both controllability and uncertainty go up at the same time.

That is exactly why loop engineering feels both familiar and strange. The underlying logic is not mysterious, but applied to the model era, many old engineering problems grow back again.

References:
- [Anthropic: Building Effective AI Agents](https://www.anthropic.com/research/building-effective-agents)
- [OpenAI: New tools for building agents](https://openai.com/index/new-tools-for-building-agents/)
- [Hacker News: The Coming Loop](https://news.ycombinator.com/item?id=48643180)

## 6. Why do some people only chat with an agent while others are already running loops?

Because "having an agent" does not by itself mean you have entered agent engineering.

A lot of people say they are using an agent, but they have only renamed the chat window. It is still you asking one thing and it answering one thing. The model has no long-term goal, no intermediate state, no verification, no ability to keep executing. At its core that is still an advanced conversation, not a real loop.

Others are already running loops because they have started putting the agent inside a task: search, act, verify, fix, act again, until a condition is met. The difference is not whether the model can talk, but whether you have placed it inside a self-sustaining closed loop.

References:
- [Anthropic: Scaling Managed Agents: Decoupling the brain from the hands](https://www.anthropic.com/engineering/managed-agents)
- [OpenAI: An open-source spec for Codex orchestration: Symphony](https://openai.com/index/open-source-codex-orchestration-symphony/)
- [OpenAI: A practical guide to building AI agents](https://openai.com/business/guides-and-resources/a-practical-guide-to-building-ai-agents/)

## 7. When do you need a loop instead of a longer prompt?

When the task is not "answered in one shot" but "you only learn the next step as you go," that is usually when you should consider a loop.

Fixing a bug, reading a repository, doing research, revising a document, running an investigation: these all share one trait. New information keeps surfacing midway. You do not know the full answer at the start; you have to find it, judge it, then continue. If you expect one oversized prompt to cover every case up front, it usually ends up long and fragile.

A long prompt suits single-shot tasks with clear boundaries. A loop suits tasks that branch, backtrack, and reveal information step by step. The former is like sitting an exam; the latter is more like working a case.

References:
- [Anthropic: Effective context engineering for AI agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)
- [OpenAI Cookbook: Build an Agent Improvement Loop with Traces, Evals, and Codex](https://developers.openai.com/cookbook/examples/agents_sdk/agent_improvement_loop)
- [Anthropic: Effective harnesses for long-running agents](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents)

## 8. Why does the more loop engineering is discussed, the easier its definition gets muddled?

Because the term is currently at the stage where everyone feels they understand a bit of it, but each person is talking about something different.

Some use it to mean multi-agent. Some use it to mean automated workflows. Some use it to mean the execution loop of a coding agent. Others just call any "repeatedly calling the model" a loop. All of these touch the edges, but the granularity is completely different, so the more you talk, the easier it is to clash.

This is not because everyone is wrong. It is because the word is still an umbrella. Too much has been stuffed under it, and once the discussion heats up, the boundaries naturally blur.

References:
- [Reddit: So is "loop engineering" the next AI dev buzzword?](https://www.reddit.com/r/myclaw/comments/1u047p8/so_is_loop_engineering_the_next_ai_dev_buzzword/)
- [Reddit: Is loop engineering actually real, or just another AI buzzword?](https://www.reddit.com/r/PromptEngineering/comments/1u2zpln/is_loop_engineering_actually_real_or_just_another/)
- [Hacker News: The Coming Loop](https://news.ycombinator.com/item?id=48643180)

## 9. Is loop engineering better suited to solo developers or to teams?

It suits both; they just extract different value.

For an individual, the biggest value of a loop is amplifying time. You can hand repetitive mental work to a system that keeps watch and runs, moving yourself from constantly supervising execution to only judging at key nodes. For a team, the value is larger, because a loop can crystallize process, standards, knowledge, and checking methods into something shared, so more people operate on the same structure.

But teams are also harder. A personal loop works because you have the whole picture in your head. A team loop works only if others can also pick it up. So individuals taste the payoff sooner, while teams are more likely to amplify the problems.

References:
- [OpenAI: A practical guide to building AI agents](https://openai.com/business/guides-and-resources/a-practical-guide-to-building-ai-agents/)
- [Anthropic: Building Effective AI Agents](https://www.anthropic.com/research/building-effective-agents)
- [Anthropic: Scaling Managed Agents: Decoupling the brain from the hands](https://www.anthropic.com/engineering/managed-agents)

## 10. Why do many people who learned agents still cannot design loops?

Because learning agents easily becomes "knowing how to use tools," but designing a loop requires a different layer of ability.

You have to judge whether a task can be broken down, which step is most likely to fail, where checks must be added, what information should persist, and when to stop. Much of this is not model knowledge; it is engineering judgment, task understanding, and failure foresight.

So many people can tune models, write prompts, and connect tools, yet cannot build a closed loop when faced with a real task. In the end, they learned to drive one component, but still cannot design the whole machine.

References:
- [Anthropic: Harness design for long-running application development](https://www.anthropic.com/engineering/harness-design-long-running-apps)
- [OpenAI: Harness engineering: leveraging Codex in an agent-first world](https://openai.com/index/harness-engineering/)
- [Anthropic: Effective harnesses for long-running agents](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents)

## 11. What is the difference between you using an agent and the agent running a loop for you?

The difference is who holds the initiative.

If every step is you watching and asking, you watching and choosing, you watching and pushing, then at its core you are still using the agent; it is just an enhanced assistant. It saves you some operations, but the rhythm stays in your hands.

If the goal, the steps, the checks, and the trigger for the next round are all designed in advance, and the agent can push forward most of the time on its own, coming back to you only when it hits a real problem, then it is closer to the agent running a loop for you. The former is a person working with a tool; the latter is a person designing a system and then letting the system run it.

References:
- [OpenAI: Unrolling the Codex agent loop](https://openai.com/index/unrolling-the-codex-agent-loop/)
- [Anthropic: Scaling Managed Agents: Decoupling the brain from the hands](https://www.anthropic.com/engineering/managed-agents)
- [OpenAI: A practical guide to building AI agents](https://openai.com/business/guides-and-resources/a-practical-guide-to-building-ai-agents/)

## 12. Why is the threshold of loop engineering in engineering judgment, not in the model?

Because today's model capability is often already enough. What really blocks people is usually not "it is not smart," but "you did not set up the system properly."

The same model placed in different task structures can perform wildly differently. Goals written too broadly, state not saved, tools too messy, verification too loose, exit conditions unclear: none of these are automatically solved by switching to a stronger model. The stronger the model, the more it can sometimes make wrong things look right.

So the truly hard part of loop engineering is not chasing the newest model, but judging where to let it run free and where guardrails must go up. That is engineering judgment, not parameter superstition.

References:
- [OpenAI: Harness engineering: leveraging Codex in an agent-first world](https://openai.com/index/harness-engineering/)
- [Anthropic: Demystifying evals for AI agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents)
- [Anthropic: Harness design for long-running application development](https://www.anthropic.com/engineering/harness-design-long-running-apps)

## 13. Is loop engineering the same thing as workflow automation?

They overlap, but they are not the same.

Workflow automation is more like automating a fixed process. You know it goes A, then B, then C, so you string that line together. The core is saving manual operation. Loop engineering, by contrast, usually leaves the model some room to judge, letting it find information on its own during execution, decide the next step on its own, and go back and revise based on results on its own.

So automation leans deterministic; a loop leans a little autonomous. Many loops certainly contain automation, but if the entire chain is hardcoded with no exploration, no judgment, and no feedback loop, then it is closer to automation and not really a loop.

References:
- [Anthropic: Building Effective AI Agents](https://www.anthropic.com/research/building-effective-agents)
- [OpenAI Agents SDK: Orchestration](https://developers.openai.com/api/docs/guides/agents/orchestration)
- [OpenAI: New tools for building agents](https://openai.com/index/new-tools-for-building-agents/)

## 14. Why does the same loop idea still hold up across different tools?

Because what is truly stable is not some product button, but that underlying structure.

Switch the agent platform, switch the IDE, switch the orchestration framework, and the surface operations change, but some things do not: the goal must be clear, state must be saved, tools must be usable, results must be verified, failures must be rollbackable, and there must be a condition to end. As long as that skeleton remains, the loop idea migrates.

This is also why many people later realize they did not learn the tricks of a particular tool, but a way of organizing intelligent execution. Tools change; the skeleton does not.

References:
- [Anthropic: Effective context engineering for AI agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)
- [OpenAI: New tools for building agents](https://openai.com/index/new-tools-for-building-agents/)
- [OpenAI Agents SDK: Sandbox agents](https://developers.openai.com/api/docs/guides/agents/sandboxes)

## 15. Does loop engineering actually replace manual prompting, or manual decision-making?

In the short term, it replaces more manual prompting. In the long term, what it most wants to eat is a slice of low-value decision-making.

Before, many people had to keep watching the model, patching and correcting round after round. Once a loop runs, that mechanical watchkeeping drops sharply, because the system keeps running, checks itself, and comes back to fix things on its own. That substitution is the most direct.

But it also gradually reaches the decision layer. Which information is worth looking at, which plan to try first, when to stop: judgments that originally required constant human participation will partly be taken over by the system. Still, high-value judgment is hard to remove entirely in the short term. People mostly step back from execution and turn to setting rules and making the final call.

References:
- [OpenAI Cookbook: Build an Agent Improvement Loop with Traces, Evals, and Codex](https://developers.openai.com/cookbook/examples/agents_sdk/agent_improvement_loop)
- [Anthropic: How we built our multi-agent research system](https://www.anthropic.com/engineering/multi-agent-research-system)
- [OpenAI: Harness engineering: leveraging Codex in an agent-first world](https://openai.com/index/harness-engineering/)

## 16. Why is buzzword the first reaction many people have when this term gets hot?

Because this industry has indeed been far too fond of coining new terms in recent years, and people have been trained into vigilance.

And "loop engineering" does sound a bit dangerous: it looks like repackaging old things like automation, agent, workflow, harness, and eval, and selling them again. If you have not seen real cases and only watch the spread, it is easy to feel this is another round of vocabulary theater.

But on the other side, you have to admit it did not get popular for no reason. People really are migrating from "how to ask" to "how to keep a system completing tasks." The word may change, the hype may fade, but the underlying problem will not disappear.

References:
- [Reddit: Is loop engineering actually real, or just another AI buzzword?](https://www.reddit.com/r/PromptEngineering/comments/1u2zpln/is_loop_engineering_actually_real_or_just_another/)
- [Hacker News: The Coming Loop](https://news.ycombinator.com/item?id=48643180)
- [OpenAI: Harness engineering: leveraging Codex in an agent-first world](https://openai.com/index/harness-engineering/)
