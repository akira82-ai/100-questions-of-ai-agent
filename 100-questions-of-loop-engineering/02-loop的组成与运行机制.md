# 二、Loop 的组成与运行机制

## 17. 一个最小可用的 loop 到底要包含哪几个环节

一个最小可用的 loop，通常至少得有四步：先看清现在是什么情况，再决定下一步做什么，然后真的去做，最后检查做得对不对。

很多人一开始会把 loop 想得很复杂，好像非得多 agent、多工具、多层状态才算。其实不用。最小版本反而很朴素：先拿到上下文，做一个判断，执行一个动作，再根据结果决定是继续还是停。只要这四步能闭起来，它就是一个 loop。

问题在于，很多人只做了中间那步“执行”，前后都没有。没有前面的识别，就会瞎做；没有后面的检查，就会假完成。所以 loop 的最小单位，看起来是一次调用模型，实际上是一次完整闭环。

参考资料：
- [Anthropic: Building Effective AI Agents](https://www.anthropic.com/research/building-effective-agents)
- [OpenAI: A practical guide to building AI agents](https://openai.com/business/guides-and-resources/a-practical-guide-to-building-ai-agents/)
- [Hacker News: The unreasonable effectiveness of an LLM agent loop with tool use](https://news.ycombinator.com/item?id=43998472)

## 18. 为什么 discover、plan、execute、verify 少一个都容易翻车

因为这四步各自防的是不同类型的错，少任何一个，系统都会在某个地方漏风。

没有 discover，你根本不知道眼前到底发生了什么，很容易拿错上下文。没有 plan，动作会变成临场乱撞，做一步看一步。没有 execute，那当然什么都不会发生。没有 verify，最危险，因为系统会很自信地把错事当成做完。

很多 loop 出问题，往往不是模型突然变笨，更多是这四步里有一步被偷掉了。尤其是 verify，大家最容易省，结果也是最贵的。因为一旦没有最后那道关，前面做得越快，后面返工越大。

参考资料：
- [OpenAI Cookbook: Build an Agent Improvement Loop with Traces, Evals, and Codex](https://developers.openai.com/cookbook/examples/agents_sdk/agent_improvement_loop)
- [Anthropic: Demystifying evals for AI agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents)
- [Reddit: After going through 15 agentic-loop papers, the thing that predicts success is the verifier, not the model](https://www.reddit.com/r/AI_Agents/comments/1uh0gfa/after_going_through_15_agenticloop_papers_the/)

## 19. loop 的 stop condition 为什么比开头目标更重要

因为目标只负责给方向，stop condition 负责给刹车。真正花钱的地方，常常不在“要去哪里”，而在“什么时候该停”。

你看 turn-based loop、goal-based loop、time-based loop，表面差别很大，落到运行层都绕不开这件事。回合制是人来喊停，目标制是评估结果来喊停，定时制是时间窗来喊停。只要这条停机线不清楚，系统就会一直觉得自己还能再补一轮、再试一次、再优化一下。

所以写 loop 时，目标可以稍微宽一点，停机条件一定要写实。测试通过、页面打开、格式合规、关键指标过线，这些才是 loop 真正收口的地方。

参考资料：
- [Ryan Lopopolo / OpenAI: Harness engineering](https://openai.com/index/harness-engineering/)
- [Oracle Developers: What Is the AI Agent Loop?](https://blogs.oracle.com/developers/what-is-the-ai-agent-loop-the-core-architecture-behind-autonomous-ai-systems)
- [Firecrawl: Loop Engineering](https://www.firecrawl.dev/blog/loop-engineering)

## 20. 为什么 loop 一旦没有明确退出条件就会越跑越贵

因为系统天生不擅长“差不多就行”，它更擅长“还能不能再来一轮”。

你不给退出条件，模型通常不会自己优雅收手。它会继续找问题、继续补细节、继续重试，哪怕后面的收益已经很低了。这样一来，token、时间、工具调用、人工注意力都会一路往上堆。

更麻烦的是，这种贵不会一下子爆炸，它会伪装成“每一轮都还挺合理”，所以人很容易失去警惕。最后你回头看，会发现问题不在于模型没产出，而在于它在没有边界的空间里一直消耗资源。退出条件说到底，是拿来保护成本的。

参考资料：
- [Anthropic: Effective context engineering for AI agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)
- [OpenAI Agents SDK: Results and state](https://developers.openai.com/api/docs/guides/agents/results)
- [Addy Osmani: Long-running Agents](https://addyosmani.com/blog/long-running-agents/)

## 21. generator 和 verifier 在 loop 里到底分别负责什么

generator 负责往前推，verifier 负责踩刹车。

generator 的任务很简单，就是尽可能把东西做出来。它写代码、改文档、查资料、调工具，核心是产出动作。verifier 则不一样，它不是来帮忙的，它是来怀疑的。它要看结果有没有达标，过程有没有跑偏，表面通过是不是假通过。

这两个角色分开以后，系统会稳很多。因为一个专注推进，一个专注挑错，目标不一样，天然就形成张力。真正靠谱的 loop，不会让一个 agent 又当运动员又当裁判，还是得让不同角色互相掐住。

参考资料：
- [Anthropic: Harness design for long-running application development](https://www.anthropic.com/engineering/harness-design-long-running-apps)
- [Anthropic Workshop: Build Agents That Run for Hours](https://www.youtube.com/watch?v=mR-WAvEPRwE)
- [Reddit: Are AI “loops” just agents grading their own homework?](https://www.reddit.com/r/codex/comments/1ucbi24/are_ai_loops_just_agents_grading_their_own/)

## 22. 为什么模型输出再强，也顶不上一个靠谱 verifier

因为生成能力解决的是“能不能做出来”，验证能力解决的是“做出来的是不是对的”。后者在工程里更稀缺。

模型再强，最多也只是更会写、更会想、更会补全。但 loop 一旦跑到真实环境，真正贵的是误判。一个看起来像样但其实错了的结果，往往比直接报错更麻烦。因为报错你会停，假成功你会继续往下堆。

所以强生成器能提高上限，强 verifier 才能守住下限。很多时候，系统好不好用，不看它最聪明的时候有多亮眼，得看它能不能把明显不对的东西稳稳拦下来。

参考资料：
- [Anthropic: Demystifying evals for AI agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents)
- [OpenAI Cookbook: Build an Agent Improvement Loop with Traces, Evals, and Codex](https://developers.openai.com/cookbook/examples/agents_sdk/agent_improvement_loop)
- [Reddit: After going through 15 agentic-loop papers, the thing that predicts success is the verifier, not the model](https://www.reddit.com/r/AI_Agents/comments/1uh0gfa/after_going_through_15_agenticloop_papers_the/)

## 23. open loop 和 closed loop 到底该怎么区分

最简单的看法就是：动作做完以后，系统有没有回来读结果，再决定下一步。

open loop 更像一条直线。你给任务，它执行，流程继续往前推。closed loop 则像一圈一圈地回看现场，上一轮的测试、日志、页面状态、用户反馈，都会变成下一轮输入。两者差别不在步骤多少，在有没有反馈回流。

还有一个容易混的点。很多人把 harness 和 loop 混成一团。其实 harness 更像厨房，决定工具、权限、文件、状态放哪；loop 是菜谱，决定这一轮做什么、验什么、何时继续。厨房搭得再好，如果动作做完不回来看结果，那照样只是 open loop。

参考资料：
- [Anthropic: Building Effective AI Agents](https://www.anthropic.com/research/building-effective-agents)
- [OpenAI: Unrolling the Codex agent loop](https://openai.com/index/unrolling-the-codex-agent-loop/)
- [Martin Fowler: Harness Engineering for Coding Agent Users](https://martinfowler.com/articles/harness-engineering.html)
- [Firecrawl: Loop Engineering](https://www.firecrawl.dev/blog/loop-engineering)

## 24. 什么情况下 open loop 会比 closed loop 更值得冒险

当任务足够便宜、足够可逆、失败代价也低的时候，open loop 反而更划算。

比如批量改写、低风险信息整理、一次性素材生成，这些事即使有点偏，也不会酿成大祸。这时如果还强行加很多验证和回路，系统会变得很重，收益不一定划算。

closed loop 的价值在高风险和高不确定性任务里最明显。可如果任务本身很轻，你硬上全套闭环，常常会出现一种很滑稽的情况：检查成本比任务本身还贵。所以不是所有任务都该闭得死死的，有些场景，open 反而更敏捷。

参考资料：
- [Anthropic: Building Effective AI Agents](https://www.anthropic.com/research/building-effective-agents)
- [OpenAI: New tools for building agents](https://openai.com/index/new-tools-for-building-agents/)
- [Developers Digest: Managed Agents vs LangGraph vs Rolling Your Own](https://www.developersdigest.tech/blog/managed-agents-vs-langgraph-vs-diy-2026)

## 25. 为什么 closed loop 更稳，却未必更有惊喜

因为 closed loop 的核心就是收敛，而惊喜很多时候来自发散。

你把检查做严、把反馈拉紧、把目标卡细，系统当然更稳。它不容易跑飞，也不容易把烂结果放过去。但代价就是，它探索奇怪方向的空间也会变小。很多闭环系统最后都会变得越来越像一个合格员工，而不是一个偶尔能给你灵感的怪才。

所以 closed loop 强在交付，不一定强在意外发现。如果你的目标是稳定生产，它很好；如果你的目标是找非标准答案，你就得给它留一点犯错和绕路的空间。

参考资料：
- [Anthropic: Harness design for long-running application development](https://www.anthropic.com/engineering/harness-design-long-running-apps)
- [OpenAI: Harness engineering: leveraging Codex in an agent-first world](https://openai.com/index/harness-engineering/)
- [Hacker News: The unreasonable effectiveness of an LLM agent loop with tool use](https://news.ycombinator.com/item?id=43998472)

## 26. loop 里的 state 为什么必须外置，不能只靠上下文记忆

因为上下文更像临时工作台，靠它充当可靠仓库，迟早会出问题。

模型当然能记一点前文，但这个记忆既贵，又不稳。轮次一长，窗口一满，它就会压缩、遗忘、误读，或者干脆把旧信息理解歪掉。你如果把关键进度、任务状态、待办、失败记录全压在上下文里，系统迟早会像失忆一样重来。

所以真正能跑久的 loop，都会把状态写到外面去。文件、数据库、任务列表、日志、记忆服务，这些东西才是长期状态。上下文负责当前一轮，外置状态负责跨轮次连续性。

参考资料：
- [Anthropic: Effective context engineering for AI agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)
- [OpenAI Agents SDK: Results and state](https://developers.openai.com/api/docs/guides/agents/results)
- [LangChain: Context Engineering for Agents](https://www.langchain.com/blog/context-engineering-for-agents)

## 27. 为什么 artifacts、contracts、logs 会成为 loop 的底座

因为 loop 一旦跨过两三轮，你就不能再赌“它应该记得刚才发生了什么”。

artifacts 负责留现场，比如产出的文件、页面截图、评估结果。contracts 负责定口径，比如什么叫通过、什么叫失败、什么叫需要人工接管。logs 负责留轨迹，让你知道它为什么走到这一步。少了这三样，loop 就很像一个只会往前冲、却没有病历和施工记录的工地。

很多长时运行的 agent，到后面拼的已经不是 prompt 漂不漂亮，拼的是这些底座有没有放稳。你能不能查上一轮、能不能接下一轮、能不能出事后复盘，靠的都是这些外置结构。

参考资料：
- [OpenAI: Harness engineering: leveraging Codex in an agent-first world](https://openai.com/index/harness-engineering/)
- [Anthropic: Harness design for long-running application development](https://www.anthropic.com/engineering/harness-design-long-running-apps)
- [Mem0: Loop Engineering for AI Agents](https://mem0.ai/blog/loop-engineering-for-ai-agents-memory-first-design)

## 28. 一个 loop 真正开始复利，靠的到底是什么共享结构

关键不在多跑几轮，而在每跑一轮，系统都能把学到的东西留下来给下一轮复用。

这个共享结构可能是 skills，可能是 playbook，可能是模板、评估规则、任务分解方式、常见错误清单。重点不在形式，在于它能不能跨任务复用。只要每次遇到问题都重新靠人临场发挥，那就只有单次收益，没有复利。

所以 loop 真正进入复利阶段，往往意味着系统开始积累结构化经验。它不会每次都从头变聪明一点，而是把有效路径固化下来，后面遇到类似问题直接套上去。

参考资料：
- [OpenAI: Harness engineering: leveraging Codex in an agent-first world](https://openai.com/index/harness-engineering/)
- [OpenAI: Skills](https://developers.openai.com/api/docs/guides/tools-skills)
- [Anthropic: Scaling Managed Agents: Decoupling the brain from the hands](https://www.anthropic.com/engineering/managed-agents)

## 29. 为什么 worktree 在 loop 场景里会从加分项变成底线

因为只要你让多个任务并行、反复迭代、持续改代码，不隔离工作区迟早出事。

没有 worktree，多个 loop 很容易互相踩文件、污染环境、覆盖彼此中间结果。你还没判断清楚一个改动值不值得保留，另一个任务已经把现场冲掉了。这样一来，验证会变假，回滚会变难，排查更是灾难。

worktree 的意义不只是在方便开分支，它更像是在给每个 loop 一块独立现场。只有现场隔离了，结果才可信，验证才有意义，并行才不会变成互相污染。

参考资料：
- [OpenAI: Harness engineering: leveraging Codex in an agent-first world](https://openai.com/index/harness-engineering/)
- [Mike McQuaid: Sandboxes and Worktrees: My secure Agentic AI Setup](https://mikemcquaid.com/sandboxed-agent-worktrees-my-coding-and-ai-setup-in-2026/)
- [Firecrawl: Multi-Agent Orchestration With Codex](https://www.firecrawl.dev/blog/codex-multi-agent-orchestration)

## 30. loop 里为什么必须把 maker 和 checker 拆开

因为同一个系统同时负责“把东西做出来”和“判断这东西行不行”，天然会偏心。

maker 的心理模型是推进任务，它会倾向于解释、修饰、合理化自己的结果。checker 的心理模型应该完全相反，它要默认不信，默认找洞，默认怀疑边界条件。你把这两个角色塞给同一个 agent，它就会在推进欲和怀疑欲之间摇摆，最后通常推进欲赢。

所以 maker 和 checker 分开，不只是组织形式更清楚，而是为了让系统内部形成真正的对抗。没有这层对抗，loop 很容易变成自我感动。

参考资料：
- [Anthropic: Harness design for long-running application development](https://www.anthropic.com/engineering/harness-design-long-running-apps)
- [Anthropic Workshop: Build Agents That Run for Hours](https://www.youtube.com/watch?v=mR-WAvEPRwE)
- [Reddit: Are AI “loops” just agents grading their own homework?](https://www.reddit.com/r/codex/comments/1ucbi24/are_ai_loops_just_agents_grading_their_own/)

## 31. 为什么让同一个 agent 自己写自己验几乎一定会高估结果

因为它会继承自己刚才那套思路，而不是站到外面重新看一遍。

人写完东西自己检查都会手软，模型也一样。它刚刚为了把某个方案讲通、做通，脑子里已经形成了一条解释路径。接着再让它来验，它最容易做的不是推翻自己，通常会顺着原来的逻辑继续给自己打圆场。

这就是为什么很多 loop 明明也有“检查”步骤，最后还是假通过。问题不在于它没检查，而在于检查的人和动手的人其实是同一套偏见。你不把视角切开，检查就很难真的硬起来。

参考资料：
- [Anthropic: Harness design for long-running application development](https://www.anthropic.com/engineering/harness-design-long-running-apps)
- [Reddit: Are AI “loops” just agents grading their own homework?](https://www.reddit.com/r/codex/comments/1ucbi24/are_ai_loops_just_agents_grading_their_own/)
- [Anthropic: Demystifying evals for AI agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents)

## 32. loop 的 heartbeat 为什么往往比 prompt 本身更决定效果

heartbeat 说白了，就是系统每一轮怎么推进、怎么汇报、怎么继续下一拍。很多时候，这个节奏感比 prompt 里的措辞更影响结果。

因为 loop 不是一锤子买卖，它靠的是连续执行。你每轮让它先看什么、汇报什么、记录什么、判断什么，都会改变后面几十轮的走向。一个 prompt 写得再好，如果 heartbeat 乱，系统照样会慢慢失控。

所以很多成熟 loop 到最后，拼的不是某句 magic prompt，拼的是那套稳定节奏。就像人工作一样，优秀团队往往不是最会开会，往往是最会按节奏推进。

参考资料：
- [OpenAI: Unrolling the Codex agent loop](https://openai.com/index/unrolling-the-codex-agent-loop/)
- [Anthropic: Effective harnesses for long-running agents](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents)
- [OpenAI Agents SDK: Running agents](https://developers.openai.com/api/docs/guides/agents/running-agents)

## 33. 为什么 automation、skills、sub-agents 组合起来才像完整 loop

因为这三样东西刚好落在三层。automation 管触发，skills 管经验，sub-agents 管分工。单拿一个出来，都只能解决一截问题。

你可以把它想成真实工作台。automation 像定时器和触发器，决定什么时候开工；skills 像团队里的操作手册，决定遇到这类任务该怎么做；sub-agents 像不同岗位的人，把生成、验证、整理、汇报拆开跑。这样 loop 才能一边推进，一边复用，一边把复杂度压住。

很多人觉得自己缺的是某个神奇 agent，后面才发现缺的往往是组合结构。能长期跑的 loop，通常都有这套分层，不会只靠一个大模型硬扛所有事情。

参考资料：
- [Addy Osmani: Loop Engineering](https://addyosmani.com/blog/loop-engineering/)
- [OpenAI: Skills](https://developers.openai.com/api/docs/guides/tools-skills)
- [Anthropic: How we built our multi-agent research system](https://www.anthropic.com/engineering/multi-agent-research-system)

## 34. loop 一旦接入 cron、webhook 和 trigger，工程难度为什么突变

因为一旦不再靠人手动点开始，整个系统就从“工具”变成了“基础设施”。

手动触发的时候，很多问题会被人类本能兜住。人会看环境对不对、上下文新不新、结果像不像样。可一旦接进 cron、webhook、trigger，系统就得自己处理时序、并发、重试、重复触发、权限、外部依赖失败这些问题。原来能靠人顺手补的地方，都会变成正式工程问题。

所以很多 loop 在手动阶段看着很顺，一接自动触发就突然翻车。问题往往不在思路本身，而在于你从单次使用切到了持续运行。门槛一下子就抬高了。

参考资料：
- [OpenAI: Harness engineering: leveraging Codex in an agent-first world](https://openai.com/index/harness-engineering/)
- [OpenAI Agents SDK: Background mode](https://developers.openai.com/api/docs/guides/background)
- [OpenAI Agents SDK: Webhooks](https://developers.openai.com/api/docs/guides/webhooks)
