# 第三章 · 把 AI 接进 Obsidian：最小路径，别被配置劝退

接 AI 这一步最容易卡在配置和隐私上。这一章给你一条最小路径：能本地就本地，要连云也带护栏。配置只是手段，让 AI 读得动你的笔记才是目的，它读的是你自己的积累，答得靠不靠谱，根就扎在你这堆笔记上。

## 31. 第一次给 Obsidian 接 AI，只装一个插件行不行？装哪个？

行，一个就够，装 Copilot。它在 Obsidian 里直接开聊，能基于你的笔记问答，选中一段文字也能让它当场改。今天三步就能跑通：设置 → 第三方插件 → 浏览 → 搜 Copilot → 安装并启用，然后打开任意一篇笔记，选中一段文字问它一句，能从你笔记里答出内容就算通了。

嫌装插件麻烦还有条零插件路：把笔记文件的完整路径贴给桌面端 AI，它能定位到那个文件并直接改写，一样先摸到 AI 读笔记的手感。

库还没过百页之前，别急着上 Dataview、Templater 这类，工具链的复杂度会在你养成习惯前先把动力耗光。装之前顺手去 Obsidian Stats 看一眼下载量和最近更新时间，半年没动静的插件直接跳过；国内访问官方市场慢，挑法和加速装法见第 90 题。

可复制模板（直接复制使用）：

```
1. 设置 → 第三方插件 → 浏览 → 搜 Copilot → 安装并启用
2. 设置 → 第三方插件 → Copilot → 设置 → Add Custom Model，填三项：
   - Base URL：本地 Ollama 固定填 http://localhost:11434/v1
     走云端就填服务商的官方端点，结尾同样带 /v1
   - Model：模型名一字不差复制，例如 qwen2.5:7b
   - API Key：本地留空；云端的 key 只显示一次，
     立刻存进密码管理器，绝不写进笔记、绝不进 Git
3. 打开任意笔记，选中一段问它，能答出你笔记里的内容就算跑通
```

依赖：Copilot 插件

资源：Copilot https://community.obsidian.md/plugins/copilot · Dataview https://community.obsidian.md/plugins/dataview · Templater https://community.obsidian.md/plugins/templater-obsidian · Obsidian Stats https://www.obsidianstats.com

## 32. 没有 API key 能不能玩？本地模型怎么零成本起步？

能玩，而且零成本。本地跑开源模型不用注册任何平台、不用填 key，数据全程留在你自己的电脑里，隐私这块最稳。装完 Ollama 敲两行命令就有结果，代价是吃你自己的硬件、答得比云端慢；对个人笔记问答这种短问答，慢几秒无所谓。桌面端几分钟跑起来，先走本地这条路摸清 AI 读笔记的手感，觉得不够快再考虑掏钱走云端。

内存吃紧的机器，先确认可用内存再挑模型档位，别硬上大的，具体看第 37 题。手机端用 Termux 也能跑通小模型，代价是 CPU-only 约 10 tok/s，慢但能出字，具体法子看第 45 题。

可复制模板（直接复制使用）：

```bash
# 不申请任何 key，本地直接跑（数据不出本机）
ollama pull qwen2.5:7b
ollama run qwen2.5:7b "用一句话介绍 Obsidian"

# 设置 → 第三方插件 → Copilot → 设置里填这两行，Key 留空
# Base URL: http://localhost:11434/v1
# Model: qwen2.5:7b
```

依赖：Ollama 与 Copilot 插件

资源：Ollama https://ollama.com/

## 33. Copilot、Smart Connections 到底怎么选不纠结？

按你最想要的那一件事选，三十秒就能定。想在 Obsidian 里直接聊、选中文字就改、基于笔记问答，装 Copilot。想让 AI 自动认得你的 vault、写东西时把相关旧笔记浮上来，装 Smart Connections，它把笔记做成 embedding，你写着写着旧笔记自己就冒出来了。想要完全本地的 RAG 问答、连对话界面都不依赖，直接开 Copilot 的 Vault QA 配上本地 Ollama，效果同一档。

还有一条不用装插件的路：把 vault 目录的读取权限给桌面端 AI，它自己建索引，能读也能改；只想改一篇的话，把那个文件的完整路径贴给它就够了。

三个一起装是卡住的开始。先装最合当下需求的那一个，连着用满两周，再决定要不要加第二个。

资源：Copilot https://community.obsidian.md/plugins/copilot · Smart Connections https://github.com/brianpetro/obsidian-smart-connections · ChatGPT https://chat.openai.com · Gemini https://gemini.google.com

## 34. 申请 API key 怕泄露，账号怎么开最安全？

这担心是对的，先立一条死规矩：key 绝不写进笔记正文，也绝不进 Git，私有仓库也不行，提交历史里删不干净。开账号当天做三件事：用专用邮箱开子账号拿 key，别绑主邮箱；key 一生成立刻存进密码管理器；在服务商后台给这个 key 设上用量上限和到期时间。

轮换按固定顺序走，先建新的再废旧的，中间不断服务。先去服务商后台生成一个新 key，复制后只粘进密码管理器；再回 Obsidian，设置 → 第三方插件 → Copilot → 设置 → API Key，把旧值手动清空再粘上新的，保存后随便问一句确认还能答；最后回服务商后台把旧 key 点 Revoke 作废。满 90 天、换过电脑、截图录屏里露过 key、账单里出现你没发起的调用，命中任意一条就立刻走这三步。

可复制模板（直接复制使用）：

```gitignore
# vault 根目录的 .gitignore
# 插件配置文件里存着明文 key，整个目录排除掉
.obsidian/plugins/
.obsidian/workspace.json
.obsidian/**/data.json

# 如果之前已经提交过，先停掉追踪，再去后台换 key
# git rm -r --cached .obsidian/plugins/
```

存好之后在 vault 里全文搜一次 `sk-`，搜不出任何结果才算干净。

资源：1Password https://1password.com/ · Bitwarden https://bitwarden.com/

## 35. 本地模型怎么装（Ollama），半小时跑通的最小步骤？

半小时够了，拢共四步：官网下 Ollama 装上，命令行 `ollama pull qwen2.5:7b` 拉一个中文轻量模型，去 设置 → 第三方插件 → Copilot → 设置 里把 Base URL 填 `http://localhost:11434/v1`、Model 填 `qwen2.5:7b`，最后打开今天的日记问它「这篇里我提到了哪几个待办」。装完用 `curl http://localhost:11434/v1/models` 能返回模型列表，就说明服务通了。

模型名一字不差地复制，冒号后面的 tag 漏一个字符就连不上，这是新手最常卡住的地方。16GB 的 Mac 实测下来系统加浏览器一吃只剩七八个 G，舒服跑的只有 7B 到 8B 这档，16G 能跑 13B 的说法别信。中文 vault 装完先别急着用，embedding 得换，看下一题。

可复制模板（直接复制使用）：

```bash
# 1. 装完 Ollama 后，拉一个中文轻量模型
ollama pull qwen2.5:7b

# 2. 确认服务活着（能返回模型列表就说明通了）
curl http://localhost:11434/v1/models

# 3. 设置 → 第三方插件 → Copilot → 设置 → Add Custom Model
#    Base URL: http://localhost:11434/v1   本地 Ollama 固定就是这个地址
#    Model: qwen2.5:7b
#    API Key: 留空

# 走云端时把 Base URL 换成服务商的官方端点，结尾同样带 /v1，Key 才需要填
```

依赖：Ollama 与 Copilot 插件

资源：Ollama https://ollama.com/ · Copilot https://community.obsidian.md/plugins/copilot

## 36. 中文 vault 用默认模型翻车，embedding 和对话模型怎么换？

默认那套按英文训练的 embedding 抓不住中文语义，搜「复盘」跟「回顾」两篇会根本对不上号。换两处就好：对话模型换 qwen 系列，embedding 换专为中文做的 bge-m3，1024 维，质量和索引体积的平衡点就在这儿。bge-m3 是中文 embedding 里用得最广的一档，Ollama 和 SiliconFlow 都能拉到。中文 vault 卡在索引 0% 多半也是这处没换。

换 embedding 会触发全库重建索引，几百篇的库几分钟，上千篇留出半小时，别挑赶稿的时候换。换完拿一对同义词各搜一次，能互相召回就算成了。

可复制模板（直接复制使用）：

```bash
# 1. 对话模型换中文友好的
ollama pull qwen2.5:7b

# 2. embedding 换专为中文的 bge-m3
ollama pull bge-m3

# 3. 设置 → 第三方插件 → Copilot → 设置 → Embedding Model
#    （Smart Connections 在 设置 → 第三方插件 → Smart Connections → 设置）
#    Provider: Custom OpenAI
#    Base URL: http://localhost:11434/v1
#    Embedding Model: bge-m3

# 4. 验收：搜一对同义词（复盘 / 回顾），两篇能互相召回就算换成了
```

依赖：Ollama 与 Copilot 或 Smart Connections 插件

资源：bge-m3 https://huggingface.co/BAAI/bge-m3 · Ollama https://ollama.com/ · Smart Connections https://github.com/brianpetro/obsidian-smart-connections

## 37. 老旧电脑显存不够，能跑哪些小模型？说清代价？

先说代价，省得你白折腾：本地模型吃的是自己的硬件，GPU 8GB 以上或者 Mac 16GB 以上才谈得上舒服。16GB 的 Mac 实际只跑得动 7B 到 8B，再往上就开始卡；手机 CPU-only 大约 10 tok/s，字出得来，等得人心焦。

机器确实老，就往下压一档：`ollama pull qwen2.5:1.5b` 或者 `qwen2.5:3b`，摘要、改写、从日记里挑待办这类活儿它扛得住，长文推理别指望。压到最小还是卡，就换个思路，AI 那部分交给云端，本地只留不吃算力的辅助，比如 Various Complements 这类基于你自己 vault 词库的补全，零模型、零联网，老机器也飞快。

说老旧机也能跑大模型的免费教程，多半没告诉你它跑一次要等多久。先量一把速度再挑档位，比硬上强。

可复制模板（直接复制使用）：

```bash
# 按可用内存挑档位（看可用内存，总内存不算数）
# 8GB 以下  → qwen2.5:1.5b   摘要 / 改写 / 提取待办
# 8-16GB    → qwen2.5:3b     上面全部 + 简单问答
# 16GB      → qwen2.5:7b     日常问答的上限，别再往上
# 24GB 以上 → qwen2.5:14b    有余量再考虑

# 先量一把速度，低于 5 tok/s 就降一档
ollama run qwen2.5:3b --verbose "用三句话总结什么是双链笔记"
```

依赖：Ollama

资源：Ollama https://ollama.com/ · Various Complements https://community.obsidian.md/plugins/various-complements

## 38. 怎么让 AI 只读"我的笔记"回答，不乱编？

把「基于 vault」那个开关打开，这是唯一关键的一步。Copilot 聊天面板顶部有个模式下拉，问之前先切到 Vault QA，它会先检索你的笔记再组织答案，训练知识只当补充。提问时再补一句硬要求：只根据我的笔记回答，每条结论后面标出处文件名，库里没有就直说没有。

能引回具体文件名、能翻出三月前的旧笔记跟当下对照，这种答案才站得住。验收就看一条：整段回答里一个文件名都没有，就当它编的，把要求重申一遍再问一次。

可复制模板（直接复制使用）：

```
只根据我 vault 里的笔记回答，遵守三条：
1. 每条结论后面用 [[文件名]] 标出处，标不出来的就别写
2. 我的笔记里没写的，直接回「库里没有」，不要拿常识补
3. 先列出你检索到的笔记标题，再开始回答

问题：<把你的问题写在这里>
```

依赖：Copilot 插件（Vault QA 模式）

资源：Copilot https://community.obsidian.md/plugins/copilot

## 39. 接上 AI 第一次该问什么，才能感受到"懂我的 AI"？

第一问别问百科能答的，问只有你的库能答的。最稳的开场：打开今天的日记，问「这篇里我提到了哪几个待办，按紧急程度排」。它从你自己的文字里捞出答案的那一下，手感就来了。日记还没成习惯的，先装 Periodic Notes 加 Calendar，点一下日历就有当天那篇，AI 也才有东西可读。

第一次连上，照下面这五句挨个问一遍，十分钟就知道这套值不值得留。

可复制模板（直接复制使用）：

```
# 接上 AI 的第一个十分钟，按顺序问这五句
1. 这篇日记里我提到了哪几个待办，按紧急程度排
2. 我这个月的日记里，反复出现的三个关键词是什么
3. 我上周在纠结什么，引用我自己写的原文两句
4. 我库里关于「<某个主题>」的笔记有哪几篇，各自讲了什么
5. 我三个月前对「<某个主题>」的看法，跟这周有什么不一样

# 五问里有三问它能引到具体文件名，这套就算真连上了
```

依赖：Copilot 插件（Vault QA 模式）

资源：Periodic Notes https://community.obsidian.md/plugins/periodic-notes · Calendar https://community.obsidian.md/plugins/calendar · Smart Connections https://github.com/brianpetro/obsidian-smart-connections

## 40. 断网也能用的私有 AI 知识库，最小配置是什么？

三样东西：本地模型、本地 vault、一个云端 key 都不填。Ollama 跑开源模型，笔记就躺在你自己的硬盘上，全程不连任何外部服务，拔了网线照用。代价是答得慢、模型小，隐私这块彻底稳。

配好之后做一次真断网验收：关掉 Wi-Fi，打开 Obsidian 问一句，能答就是真私有；答不出来，说明还有一环在偷偷连云，回 设置 → 第三方插件 → Copilot → 设置 查 Base URL 是不是填了云端地址，本地应当是 `http://localhost:11434/v1`。目录也一并立好规矩，原始资料只进不改，AI 只在它自己那块地里写。

可复制模板（直接复制使用）：

```
my-brain/
├── raw/          # 原始资料，只进不改
├── wiki/         # AI 的地盘
│   ├── index.md  # 总目录，每次操作后更新
│   └── log.md    # 操作日志
└── AGENTS.md     # 给 AI 的规则

# AGENTS.md 里写清：raw/ 永远不修改；wiki/ 由 AI 生成维护；index.md 每次更新

# 断网验收：关 Wi-Fi → 打开 vault → 问一句 → 能答就算真私有
```

资源：Ollama https://ollama.com/

## 41. 云端强、本地稳但弱，我该怎么分场景选？

别二选一，两边都配上，按内容敏感度切。切换成本极低，设置 → 第三方插件 → Copilot → 设置 里把 Model 换一个选项，五秒钟的事。

| 维度 | 本地模型（Ollama + 7B） | 云端 API |
|---|---|---|
| 隐私 | 数据不出本机，断网可用 | 内容要发到服务商服务器 |
| 速度 | 桌面端每秒几十字，手机 CPU 约 10 tok/s | 几乎即时，长文也快 |
| 中文能力 | 换 qwen 加 bge-m3 后日常够用，长文推理明显弱 | 摘要、改写、翻译准确率高一档 |
| 成本 | 零订阅，一次性吃硬件，Mac 16GB 起步 | 按 token 付费，重度使用每月几十元起 |
| 上手难度 | 装 Ollama、拉模型、填端点，半小时 | 申请 key 粘进去就能用，五分钟 |
| 适合场景 | 日记、客户资料、未公开草稿、财务与凭证 | 公开学习笔记、技术文档、长文改写与翻译 |

这段内容泄漏出去会让你难受，走本地；不会难受，走云端换质量和速度。拿不准就走本地，后悔的成本比慢几秒高得多。发去云端之前，手动删掉真名、公司名、金额和联系方式。会议纪要这类居中的，涉及人事、薪酬、未公开决策的走本地，其余走云端。

资源：Ollama https://ollama.com/ · Copilot https://community.obsidian.md/plugins/copilot

## 42. 把和 AI 的对话沉淀进 vault，哪个插件最省事？

Copilot 最省事，它就长在 Obsidian 里，聊完选中那段直接存成笔记，不用来回切窗口。Smart Connections 补另一半，它本来就读你的 vault，对话里牵扯到的旧笔记会自动浮出来，你顺手连回去就行。

插件只省了搬运那一步，真正让对话变成资产的是存的时候多写三行：当时什么背景、结论是什么、下一步做什么。少了这三行，三个月后你翻到只会看见一堆不知道从哪来的字。给每篇对话笔记打上统一属性，再用一段 Dataview 自动汇总，永远不会漏。

可复制模板（直接复制使用）：

```markdown
---
type: ai-chat
date: 2026-01-05
topic: 
model: 
---

## 背景
（我当时在解决什么问题）

## 结论
（一句话写完，别整段复制对话）

## 下一步
- [ ] 

## 原文摘录
（只留真正有用的那几句）
```

可复制模板（直接复制使用）：

````markdown
```dataview
TABLE date AS 日期, topic AS 主题, model AS 模型
FROM ""
WHERE type = "ai-chat"
SORT date DESC
LIMIT 30
```
````

依赖：Dataview 插件

资源：Copilot https://community.obsidian.md/plugins/copilot · Smart Connections https://github.com/brianpetro/obsidian-smart-connections · Dataview https://community.obsidian.md/plugins/dataview

## 43. 插件装太多 vault 变卡，怎么控制在 2 个就够用？

先有具体痛点，再去找插件，不提前囤。接 AI 这个阶段两个足够，一个负责聊，Copilot；一个负责让 AI 认得你的库，Smart Connections。库没过百页之前，Dataview、Templater 这些都可以再等等，等你真被某件事卡住了再装，那时候你也知道自己要它干什么。

拖得最狠的往往是你早忘了装过的那几个插件。每季度清一次，方法在下面，五分钟能砍掉一半。插件少了 vault 轻、启动快，反而更容易坚持写下去。

可复制模板（直接复制使用）：

```
# 季度插件清理，五分钟
1. 设置 → 第三方插件，把已安装列表从上到下过一遍
2. 每个插件问自己一句：最近 30 天用过吗？
   - 想不起来用在哪 → 直接禁用（先禁用别卸载，留一周反悔期）
   - 说得出具体场景 → 留着
3. 禁用完重启 Obsidian，记一下启动秒数，前后对比
4. 一周内没觉得少了什么 → 卸载
5. 以后新装任何插件前，先写一行：我要它解决的具体问题是 ___
   写不出来就别装
```

资源：Copilot https://community.obsidian.md/plugins/copilot · Smart Connections https://github.com/brianpetro/obsidian-smart-connections · Dataview https://community.obsidian.md/plugins/dataview · Templater https://community.obsidian.md/plugins/templater-obsidian

## 44. 我担心数据外泄，接 AI 前必做的三道护栏是什么？

先立护栏再接 AI，顺序反了就来不及。第一道，私密内容先隔离，日记和客户资料要么只走本地模型，要么用 Cryptomator 加密后再存，别让它出现在 AI 能索引到的目录里。第二道，外来内容人工过一眼，AI 生成的、网上抓的，进库前你自己看一遍，别开自动灌。第三道，外传通道收到最小，key 只给需要它的那个工具、定期换，插件只装最少的那几个。

风险可以拆成两件事叠加：内容不可信，加上有一条往外传的通道，两件同时成立才真出事，断掉任意一条就安全得多。文件夹按三档分权限是最省心的断法，抄下面这张目录结构。

可复制模板（直接复制使用）：

```
vault/
├── 00-private/     # 日记、客户资料、财务：AI 完全不可见
│                   # 做法：放在 vault 外，或者用 Cryptomator 加密卷
├── 10-readonly/    # 读书摘抄、剪藏：AI 只读，不许改
├── 20-workspace/   # 草稿、项目笔记：AI 可读可写
└── 90-ai-output/   # AI 生成的先落这儿，你审过再搬进 20-

# 接 AI 前的三条自检
- [ ] 00-private 里的东西，AI 检索确实搜不到
      （拿一个只有那里才出现的词搜一次验证）
- [ ] AI 生成的内容一律先进 90-，没有直接写进 10- 和 20- 的权限
- [ ] key 存在密码管理器里，vault 全文搜 "sk-" 搜不出任何结果
```

资源：Cryptomator https://cryptomator.org/

## 45. 手机上能跑本地 AI 吗，还是只能当同步端？

能跑，但先想清楚值不值。Android 上用 Termux 装 Ollama 能跑通小模型，CPU-only 约 10 tok/s，Obsidian 移动版把 Base URL 填 `http://localhost:11434/v1` 就能连上。代价是后台一被系统杀就断，得靠 termux-wake-lock 保活，Android 版本和网络配置还决定了 localhost 通不通。

更省事的分工是：电脑跑本地模型，手机只当同步端和输入端，出门想问就问家里那台。真要手机离线可用，接受慢和折腾，按下面的顺序试，卡在哪一步就停在哪一步，别硬撑。

可复制模板（直接复制使用）：

```bash
# 手机跑本地模型，按顺序验，卡住就退回同步端方案
# 1. 装 Termux，先执行
termux-wake-lock
# 2. 装 Ollama，拉最小的模型（手机别拉更大的）
ollama pull qwen2.5:1.5b
# 3. 起服务
ollama serve
# 4. 手机浏览器开 http://localhost:11434 ，看到 Ollama is running 才算通
# 5. Obsidian 移动版 → 设置 → 第三方插件 → Copilot → 设置
#    Base URL: http://localhost:11434/v1
#    Model: qwen2.5:1.5b
# 6. 切后台三分钟再回来，还能答就算稳；断了就是保活没做住

# 退回方案（推荐大多数人）：手机只负责同步和记录，AI 的活留给电脑
```

依赖：Termux、Ollama 与 Copilot 插件

资源：Ollama https://ollama.com/

## 46. 模型更新快，今天配的明天会不会废？怎么不被版本拖死？

会废掉一部分，所以别把配置写死。AI 插件比普通插件更容易被版本拖死：embedding 被重置要重跑几个小时，key 格式变了要重配，模型 API 弃用要回滚，而截至 2026 还没有内置的一键降级，护栏只能自己搭。

三招够用：一次只更一个插件，更完用一圈再更下一个；更新前把 `.obsidian/plugins/<插件名>` 整个复制一份，文件夹名后面缀上日期，出事直接盖回去；更新前扫一眼 changelog 里的 breaking change，AI 插件尤其要看。

写笔记的时候也留点余地，别把命令名、菜单路径、参数写死进模板，加一句「以插件最新 README 为准」，等它改了你不至于全库白配。

可复制模板（直接复制使用）：

```bash
# 更新任何 AI 插件之前，三步
# 1. 备份整个插件目录，文件夹名缀上日期
cp -r .obsidian/plugins/copilot .obsidian/plugins/copilot.bak-20260105

# 2. 读 changelog：只找 breaking / removed / renamed 这三个词
# 3. 更新后立刻验三件事：
#    - 模型还连得上吗（随便问一句，看有没有答案）
#    - 索引还在吗（搜一个老词，看还召不召得回）
#    - 设置 → 第三方插件 → Copilot → 设置 里的
#      Base URL / Model / API Key 有没有被清空

# 出事回滚：关 Obsidian → 删掉新目录 → 把 .bak- 那份改回原名 → 重开
```

依赖：Copilot 插件

资源：Copilot https://community.obsidian.md/plugins/copilot · Smart Connections https://github.com/brianpetro/obsidian-smart-connections
