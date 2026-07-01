# 《Loop Engineering · 100 问》

## 一、基础认知与定位

1. 为什么现在很多人说 prompt engineering 已经过时了
2. loop engineering 到底比 prompt engineering 多了什么
3. loop engineering 和 harness engineering 到底差在哪
4. 为什么说 loop engineering 不是写提示词而是写系统
5. loop engineering 真的是新范式还是旧工程换了个名字
6. 为什么同样是 agent，有人只会聊天有人已经在跑 loop
7. 什么情况下你需要的是 loop 而不是更长的 prompt
8. 为什么 loop engineering 讨论越热，定义反而越容易混乱
9. loop engineering 到底适合个人开发者还是更适合团队
10. 为什么很多人学了 agent 以后还是不会设计 loop
11. 什么叫你在用 agent，什么叫 agent 在替你跑 loop
12. 为什么 loop engineering 的门槛不在模型而在工程判断
13. loop engineering 和 workflow automation 到底是不是一回事
14. 为什么同样的 loop 思路放到不同工具里还能成立
15. loop engineering 真正替代的是人工 prompting 还是人工决策
16. 为什么这个词一火，很多人第一反应就是 buzzword

## 二、Loop 的组成与运行机制

17. 一个最小可用的 loop 到底要包含哪几个环节
18. 为什么 discover、plan、execute、verify 少一个都容易翻车
19. loop 的 stop condition 为什么比开头目标更重要
20. 为什么 loop 一旦没有明确退出条件就会越跑越贵
21. generator 和 verifier 在 loop 里到底分别负责什么
22. 为什么模型输出再强，也顶不上一个靠谱 verifier
23. open loop 和 closed loop 到底该怎么区分
24. 什么情况下 open loop 会比 closed loop 更值得冒险
25. 为什么 closed loop 更稳，却未必更有惊喜
26. loop 里的 state 为什么必须外置，不能只靠上下文记忆
27. 为什么 artifacts、contracts、logs 会成为 loop 的底座
28. 一个 loop 真正开始复利，靠的到底是什么共享结构
29. 为什么 worktree 在 loop 场景里不是可选项而是底线
30. loop 里为什么必须把 maker 和 checker 拆开
31. 为什么让同一个 agent 自己写自己验几乎一定会高估结果
32. loop 的 heartbeat 为什么往往比 prompt 本身更决定效果
33. 为什么 automation、skills、sub-agents 组合起来才像完整 loop
34. loop 一旦接入 cron、webhook 和 trigger，工程难度为什么突变

## 三、踩坑与反模式

35. 为什么你以为自己在做 loop，结果只是在放大错误
36. loop 跑得很勤，为什么结果却没有任何真实进展
37. 为什么很多 loop 看起来在工作，其实只是在空转烧 token
38. 目标写得太宽，为什么 loop 很快就会变成 slop machine
39. verifier 写得太软，为什么垃圾结果也能被判成通过
40. 为什么 loop 最危险的失败不是报错而是假成功
41. 看起来都通过了，为什么最后交付还是完全不能用
42. loop 一旦没人复核，为什么最容易滑向认知投降
43. 为什么把所有判断都交给 agent，最后只会更难排查
44. loop 一开始很顺，为什么跑久了反而越来越不可信
45. 为什么 prompt 写得再精细，也救不了一个烂 stop condition
46. loop 一接到真实仓库，为什么文件隔离立刻变成头号问题
47. 为什么没有 logs 的 loop 出了事几乎没法回溯
48. 为什么没有外部 state 的 loop 每轮都像失忆后重来
49. loop 的 verifier 为什么最容易变成形式主义打勾器
50. 为什么“先跑起来再说”是 loop 场景里最贵的乐观
51. 哪些 loop 看起来很聪明，其实只是把返工推迟到后面
52. 为什么越自动的 loop，越容易让人误以为自己可以不懂细节

## 四、验证、质量与成本控制

53. 为什么 loop engineering 的真正瓶颈已经从生成转向验证
54. verifier 到底该检查结果、过程还是中间状态
55. 什么样的 verifier 才能真正拦住假完成
56. 为什么“done”写不清，整个 loop 就没有可控性
57. loop 的质量标准到底该先写在 prompt 里还是系统里
58. 为什么 hard checks 才是 loop 收敛的地板
59. 什么情况下要用 rubric，什么情况下要用确定性检查
60. 为什么“模型给自己打分”在 loop 里几乎总会偏乐观
61. loop 要跑得稳，哪些指标必须持续被记录
62. 为什么 latency 变长，往往说明 verifier 开始变复杂了
63. cost、quality、novelty 三者在 loop 里到底怎么取舍
64. 什么情况下你该为更强 verifier 付出更高成本
65. loop 预算到底该按轮次管，还是按结果管
66. 为什么很多人知道 token 贵，却还是管不住 loop 成本
67. 怎么判断一个 loop 是在收敛，还是在优雅地浪费钱
68. 遇到高成本 loop，第一步该砍模型还是先砍无效循环
69. 为什么“惊喜很多”的 loop，往往也是最难控成本的 loop
70. loop 的上限为什么常常不是模型，而是你的评估体系

## 五、工程落地与真实工作流

71. 什么任务最适合先从单次 prompting 升级成 loop
72. 什么任务看起来适合 loop，其实根本不值得自动化
73. 为什么 bug 修复、文档维护和 triage 特别适合做 loop
74. loop 接入真实业务前，第一步该先锁哪几个风险点
75. 为什么 support loop、SEO loop、product loop 最容易做出复利
76. 一个 loop 真正接入团队流程，最先撞上的墙是什么
77. 为什么个人能跑通的 loop，一进团队就突然失灵
78. loop 想长期跑下去，哪些知识必须沉淀成 skill
79. 为什么 loop 不是替你省掉工程，而是逼你补齐工程
80. 让 loop 写 PR、开 ticket、改文档时，哪些动作必须留人工闸门
81. 什么情况下 loop 应该只提建议，不能直接执行
82. 为什么“让它后台一直跑”听起来方便，实际上最容易出事
83. loop 和 GitHub Actions、cron、webhook 结合后会新增哪些坑
84. 想让多个 loop 彼此协作，最先要统一什么结构
85. loop 跑得越多，为什么共享 artifacts 越容易变成新瓶颈
86. 什么样的团队文化，才真的吃得下 loop engineering

## 六、边界、争议与未来判断

87. 为什么很多人觉得 loop engineering 只是 prompt engineering 的营销升级
88. loop engineering 的 hype 过去以后，真正会留下什么能力
89. 什么人现在最应该学 loop，什么人最好先别跟风
90. 为什么 loop engineering 不是让工程师消失而是更难被替代
91. loop 越强，为什么越要求你保留人类判断
92. 为什么“我不写 prompt 了”听起来先进却也可能很危险
93. loop engineering 真正改变的是工具，还是工程师的工作重心
94. 什么情况下 loop 会让理解力债务越滚越大
95. 为什么 loop 做得越顺，越要警惕自己停止思考
96. loop engineering 最终拼的是模型能力还是系统设计能力
97. 为什么小团队也能受益于 loop，但不能照搬大公司的做法
98. loop engineering 会不会像 prompt engineering 一样很快被下一波词替代
99. 如果 verifier 才是核心，未来最值钱的能力会变成什么
100. loop engineering 真正值得留下来的，不只是“自动跑”而是什么
