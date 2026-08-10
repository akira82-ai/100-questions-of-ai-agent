# Chapter 3 · Connecting AI to Obsidian: the minimum path, don't quit over config

Many get stuck at the step of connecting AI, afraid of installing plugins, configuring models, privacy issues. This chapter specifically breaks these stuck points, giving you a minimum viable path: local if possible, with guardrails if you must go cloud. Config is not the goal; getting AI to read your notes is. It reads your own accumulation, not made up from nothing; the more solid that root, the more reliable the answers.

## 31. First time connecting AI to Obsidian, is installing just one plugin enough? Which one?

Some agonize over installing a bunch of plugins to connect AI, but actually one is enough for the first time. Install Copilot, the one in Obsidian that chats with AI directly and can answer based on your notes, and can process selected text directly.

Resource: Copilot https://community.obsidian.md/plugins/copilot

Resource: Copilot https://community.obsidian.md/plugins/copilot

Someone building a knowledge base explicitly said before the vault passes a hundred pages, do not install Dataview, Templater and those; the complexity of the toolchain kills motivation before you build the habit. Same for connecting AI: first install just one Copilot, get the feel of "AI reads my notes" working, add others when you truly need them. Too many plugins and the vault gets slow, which makes it even easier to quit. One is enough, get moving first. For those who dread installing plugins, there is an even lighter path: paste the note-file path to a desktop AI and it locates and rewrites the matching file, so you run AI reading your notes with zero plugins. Before installing, you can also glance at the community ranking site Obsidian Stats for download counts and ratings, avoiding plugins no one maintains; for readers in China where the official market is slow to reach, the picking method and accelerated install are in Question 90.

Resource: Dataview https://community.obsidian.md/plugins (search "Dataview") · Templater https://community.obsidian.md/plugins (search "Templater") · Obsidian Stats https://www.obsidianstats.com

Copy-paste template (use directly):

```
1. Settings → Community plugins → Browse → search Copilot → install and enable
2. Settings → Copilot → Add Custom Model → fill three fields:
   - Base URL: must end with /v1
   - Model: copy model name exactly
   - API Key: shown only once, store in password manager, never into git
3. Open any note, select text and ask it, verify it works
```

## 32. Can I play without an API key? How to start local models at zero cost

Afraid of the trouble of applying for a key, afraid of leakage, so dare not connect AI. Actually you can play without a key; local models start at zero cost.

Running an open-source model locally, data never leaves your computer, no platform registration, no key. The cost is your own hardware, answers slower than cloud, but plenty for personal note Q&A. Someone ran Ollama on a phone, CPU only, and got it working at about 10 tok/s. Don't be scared off by the cost; this local-model path, zero key, zero fee, lets you feel AI reading notes. For how to install, see the next question.

Resource: Ollama https://ollama.com/

Resource: Ollama https://ollama.com/

Copy-paste template (use directly):

```
# No key application, run locally directly (data never leaves machine)
ollama pull qwen2.5:7b
ollama run qwen2.5:7b "introduce Obsidian in one sentence"

# In Copilot point Base URL to local, no key needed
Base URL: http://localhost:11434/v1
```

## 33. Copilot, Smart Connections, ObsidianRAG, how to choose without agonizing?

Three mainstream plugins in front of you and you agonize. Actually choose by what you want most, no agonizing.

Want to chat with AI directly in Obsidian, process selected text, answer based on notes: choose Copilot, it is most like a chat box plus note retrieval. Want AI to automatically understand your vault, auto-surface related old notes while writing: choose Smart Connections, it embeds your notes so AI recognizes your accumulation. Want local RAG Q&A, no dependency on a chat interface: choose ObsidianRAG. Someone migrating from another tool made dropping the pursuit of perfection their first move; same for plugins, install one that best fits current need, get it smooth before considering others. Don't do all three at once; that is where the stuck begins. Some also just hand a desktop AI read access to the vault; it builds the index itself and can read and rewrite your notes without any plugin, and pasting a note-file path to a desktop-side assistant like ChatGPT or Gemini also lets it locate and edit the file directly.

Resource: Copilot https://community.obsidian.md/plugins/copilot

Resource: Copilot https://community.obsidian.md/plugins/copilot · Smart Connections https://github.com/brianpetro/obsidian-smart-connections · ObsidianRAG https://community.obsidian.md/plugins (search "ObsidianRAG")

Resource: ChatGPT https://chat.openai.com · Gemini https://gemini.google.com

## 34. Afraid of API key leakage, how to open an account most safely?

Afraid of key leakage, this worry is reasonable, the vulnerable part is exactly those credentials shown only once. There is a security practice specifically about key rotation, a few core things.

Open a sub-account with a dedicated email for the key, not your main account. Key shown only once, immediately store in a password manager, never write into code, never into git. Rotate regularly, do not use one key for a year. Someone took apart an attack surface, saying the vulnerability is not just the content itself, but untrusted content stacked with the outbound channel. So for the key gate: dedicated email, password manager, regular rotation, do these three and leakage risk drops.

## 35. How to install a local model (Ollama), minimum steps to run in half an hour

Local models sound scary, but with Ollama you can actually get it running in half an hour. The minimum steps are just a few lines.

Resource: Ollama https://ollama.com/

Resource: Ollama https://ollama.com/

First install Ollama, then pull a lightweight Chinese model with one command, like qwen2.5:7b. Then in Copilot fill Base URL http://localhost:11434/v1, copy the model name exactly. For a Chinese vault remember to configure Chinese embedding, see next question. Someone tested on a 16GB Mac, system plus browser eats only seven or eight GB left, so realistically only 7B to 8B runs comfortably; do not believe the claim that 16G can run 13B. After installing, open your diary and ask which to-dos I mentioned in this note, and it pulls the answer from your words.

Resource: Copilot https://community.obsidian.md/plugins/copilot

Copy-paste template (use directly):

```
# 1. After installing Ollama, pull a lightweight Chinese model
ollama pull qwen2.5:7b

# 2. Fill in Copilot settings
Base URL: http://localhost:11434/v1
Model: qwen2.5:7b
```

## 36. Chinese vault with default model fails, how to swap embedding and chat model?

A Chinese vault with the default English embedding often fails retrieval; someone tested that Chinese retrieval often does not match.

The root cause is the default model is trained on English and cannot catch Chinese semantics. Two places to swap: the chat model to a Chinese-friendly one, like the qwen series; the embedding model to one specialized for Chinese, bge-m3. Someone tested bge-m3 is the balance point of quality and storage, 1024 dimensions, Ollama can run ollama pull bge-m3, also has a hosted version. In Smart Connections set Provider to Custom OpenAI and fill in bge-m3's address. After swapping, search again and Chinese notes finally match, and AI reading your vault truly understands.

Resource: Smart Connections https://github.com/brianpetro/obsidian-smart-connections

Resource: bge-m3 https://huggingface.co/BAAI/bge-m3 · Ollama https://ollama.com/ · Smart Connections https://github.com/brianpetro/obsidian-smart-connections

Copy-paste template (use directly):

```
# 1. Swap chat model to Chinese-friendly, e.g. qwen series
ollama pull qwen2.5:7b

# 2. Swap embedding to Chinese-specialized bge-m3
ollama pull bge-m3

# Copilot / Smart Connections: Provider set to Custom OpenAI, fill bge-m3 address
# After swapping, search again and Chinese notes finally match
```

## 37. Old computer with insufficient VRAM, which small models can run? State the cost

An old computer with insufficient VRAM, hearing local models are zero-cost, rushes in, only to find it cannot run. The cost must be stated.

Local models eat your own hardware; only comfortable with GPU 8GB+ or Mac 16GB+, a 16GB Mac realistically runs only 7B to 8B, bigger and it lags. On phone with Ollama, CPU only about 10 tok/s, can run but slow. So pick the 0.8B to 7B tier, like qwen's small-parameter version; the cost is answer quality below cloud large models and slow speed. Do not believe free tutorials saying old machines can run large models; that is cheating your hardware. Know the cost, pick the tier that fits you, better than forcing it.

Resource: Ollama https://ollama.com/

Resource: Ollama https://ollama.com/

## 38. How to make AI answer only from "my notes", not make things up?

The most feared is AI confidently making up things your vault does not have. The key to making AI answer only from your notes is turning on the switch based on notes.

Plugins like Copilot, when asking, select vault-based or similar mode, and it retrieves your notes before answering, instead of spitting training knowledge directly. Someone migrating from another tool valued most that notes always belong to you and are precisely retrievable. Others found AI's answer is stable only when it cites your note sources; what is made up from nothing deserves most vigilance. When you ask, explicitly tell it to answer only based on my notes, the probability of it making things up drops, and cases of answering not what you recorded also decrease. Some also have AI precisely search the vault and cite their earlier viewpoints, like reminding them of a similar conclusion they wrote three months ago, so the answer actually holds up.

Resource: Copilot https://community.obsidian.md/plugins/copilot

Resource: Copilot https://community.obsidian.md/plugins/copilot

## 39. First time connecting AI, what should I ask to feel "an AI that gets me"?

Connected AI but do not know what to ask, chat casually and feel no different from the web version. The first thing to ask is a question only your notes can answer.

Open the diary you wrote today and ask it which to-dos I mentioned in this note. When it actually pulls the answer from your words, you feel the hand of an AI that gets me. Others use Smart Connections, and while writing it auto-surfaces related old notes; that moment it actually remembers what I noted three months ago is the most touching. First time do not ask what an encyclopedia can answer; ask what only your vault can answer, then you see AI connected with your accumulation. Some first feed AI a whole stretch of life background, then ask what they were wrestling with last week, and when it pulls the answer from the diary, that is the moment they truly feel it gets them.

Resource: Smart Connections https://github.com/brianpetro/obsidian-smart-connections

Resource: Smart Connections https://github.com/brianpetro/obsidian-smart-connections

## 40. A private AI knowledge base usable offline, what is the minimum config?

Afraid of data leaving the cloud, want offline use, the minimum config is local model plus local vault.

Install Ollama to run open-source models, the vault is on your disk, never connecting any external service throughout, usable offline. Someone ran Ollama on a phone, Obsidian mobile fills localhost:11434/v1 to connect, data never leaves the machine. The cost is slow answers and small models, but privacy is fully stable. Others compared cloud and local, saying local is stable but weak, cloud is strong but has outbound risk. The minimum private config: local model, local vault, no cloud key filled; do these three and your knowledge base is in your own hands, alive even offline.

Resource: Ollama https://ollama.com/

Resource: Ollama https://ollama.com/

Copy-paste template (use directly):

```
my-brain/
├── raw/          # raw material, only in, never edit
├── wiki/         # AI's territory
│   ├── index.md  # master index, updated after each operation
│   └── log.md    # operation log
└── CLAUDE.md     # rules for AI

# In CLAUDE.md write clearly: raw/ never modified; wiki/ generated and maintained by AI; index.md updated each time
```

## 41. Cloud is strong, local is stable but weak, how to choose by scenario?

Cloud models are strong, fast, high quality, but data leaves the machine; local is stable, private, but weak and slow. Someone specifically built a cloud-local hybrid decision framework.

Choose by scenario and it is clear: sensitive content, diary, client materials, go local, data never leaves computer; daily non-sensitive note Q&A, wanting quality and speed, go cloud. Someone else took apart an attack surface, saying the vulnerable part is untrusted content stacked with outbound channel, so sensitive always local. You do not have to choose one; cut by content sensitivity, private what should be private, fast what should be fast, have both ready, and it is most worry-free.

## 42. Which plugin is most hassle-free for sinking AI conversations into the vault?

Chatting with AI produces something useful, but close the window and it evaporates; which plugin is hassle-free for sinking it into the vault. The most hassle-free is Copilot, it is right in Obsidian, after chatting select that passage and save it as a note directly, no switching back and forth.

Resource: Copilot https://community.obsidian.md/plugins/copilot

Resource: Copilot https://community.obsidian.md/plugins/copilot

Others use Smart Connections, which already reads your vault, and related notes it mentions in the chat auto-surface, you link back casually. The key is do not let the conversation go to waste; spend thirty seconds after chatting dropping background, conclusion, next step into the inbox, the template from chapter one. The plugin just saves you one step; what truly sinks the conversation is the three lines you store each time. Some also use an in-vault chat plugin with a few added skills, no local subscription fee, and the notes AI writes automatically carry links and properties, even one-click mind-maps, auto-summarized databases, and noise-stripped web pages saved as notes.

Resource: Smart Connections https://github.com/brianpetro/obsidian-smart-connections

## 43. Too many plugins make the vault slow, how to control to just 2 being enough?

Someone specifically timed with a stopwatch which plugins especially slow performance; too many makes the vault visibly slow. Others reviewing three years of notes said the easiest trap in the plugin craze is installing a bunch you never use.

The control method is simple: problem first, plugin later. You hit a specific pain point, then find a plugin that solves it, do not stock up in advance. Someone building a knowledge base explicitly said before the vault passes a hundred pages, do not even install Dataview or Templater. For most people, at the AI-connecting stage two are enough: one to chat with AI, Copilot; one to let AI understand your vault, Smart Connections. Add others when you are truly stuck. Fewer plugins, lighter vault, faster startup, easier to stick with.

Resource: Copilot https://community.obsidian.md/plugins/copilot

Resource: Dataview https://community.obsidian.md/plugins (search "Dataview") · Templater https://community.obsidian.md/plugins (search "Templater") · Copilot https://community.obsidian.md/plugins/copilot · Smart Connections https://github.com/brianpetro/obsidian-smart-connections

## 44. I worry about data leakage, what are the three guardrails to set before connecting AI?

Someone specifically took apart an attack surface, saying the vulnerability is not just the content itself, but untrusted content stacked with the outbound channel, called the fatal three-piece set. Set three guardrails before connecting AI.

First, protect private data first: diary, client materials, either go local model not leaving the machine, or encrypt with Cryptomator before storing. Second, manually review untrusted content: what AI gives, what is scraped from the web, you glance at it before it enters the vault, do not auto-pour. Third, minimize permissions on the outbound channel: keys only to what is needed, rotate regularly, install fewest plugins. Do all three and leakage risk drops to minimum. One bottom line: protect private content first, then talk about intelligence. It is also worth learning to give an agent three tiers of folder permissions: private holds diary and trade secrets, completely invisible to the agent; readonly is read-only, like reading excerpts; read+write lets it create and edit. Only let it touch the part you want it to touch.

Resource: Cryptomator https://cryptomator.org/

Resource: Cryptomator https://cryptomator.org/

## 45. Can I run local AI on my phone, or is it only a sync endpoint?

Many think the phone can only be a sync endpoint, with AI all in the cloud. Actually the phone can run local AI too, just troublesome.

Someone ran Ollama on a phone, CPU only about 10 tok/s, got small models working, Obsidian mobile fills localhost:11434/v1 to connect. The cost is background keep-alive is a long-term pain; Android version and config decide whether localhost interworks, may need termux-wake-lock to keep background. So the phone can run, but the experience is not as smooth as desktop. Daily you use phone as sync endpoint, computer runs local model, most stable; wanting pure phone offline, accept the trouble and slowness. Clear positioning, do not expect the phone to replace the desktop.

Resource: Ollama https://ollama.com/

Resource: Ollama https://ollama.com/

## 46. Models update fast, will today's config be useless tomorrow? How not to be dragged by versions

AI plugins update fast; someone stepped on the pit where embedding was reset and had to re-run for hours, API key format changed and had to reconfigure, model API deprecated and had to roll back. More easily version-dragged than ordinary plugins.

A few tricks to not be dragged: small-step updates, do not update five at once, do them one by one and test each; before updating, copy the plugin directory with a version number as backup; read the changelog once, especially breaking changes of AI plugins. Others pointed out that as of 2026 there is still no built-in one-click downgrade, guardrails must be self-built. So when writing notes do not hard-code command names and paths into templates, note "follow the plugin's latest README", so when it changes you do not have to reconfigure everything.
