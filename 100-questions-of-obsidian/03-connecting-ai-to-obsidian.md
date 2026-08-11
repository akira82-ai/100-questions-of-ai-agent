# Chapter 3 · Connecting AI to Obsidian: the minimum path, don't quit over config

The step that trips people up most is config and privacy. This chapter hands you one minimum path: local when you can, guardrails when you go cloud. Config is only the means; getting AI to actually read your notes is the point. It reads your own accumulation, and how reliable the answers are comes down to how solid that pile of notes is.

## 31. First time connecting AI to Obsidian, is installing just one plugin enough? Which one?

Yes, one is enough. Install Copilot. It chats inside Obsidian, answers from your notes, and rewrites whatever text you select. Three steps today get it running: Settings → Community plugins → Browse → search Copilot → install and enable, then open any note, select a passage and ask it something. If the answer comes out of your own note, it works.

If installing plugins feels like too much, there is a zero-plugin path: paste the full file path of a note to a desktop AI, and it locates that file and rewrites it directly. Same feel of AI reading your notes, nothing installed.

Before your vault passes a hundred pages, hold off on Dataview, Templater and that crowd. Toolchain complexity drains your motivation before the habit forms. Before installing anything, glance at Obsidian Stats for download counts and last update date, and skip anything untouched for six months.

Copy-paste template (use directly):

```
1. Settings → Community plugins → Browse → search Copilot → install and enable
2. Settings → Community plugins → Copilot → Options → Add Custom Model, fill three fields:
   - Base URL: for local Ollama, always http://localhost:11434/v1
     for cloud, your provider's official endpoint, also ending in /v1
   - Model: copy the model name exactly, e.g. qwen2.5:7b
   - API Key: leave empty for local; a cloud key is shown only once,
     store it in a password manager immediately, never in notes, never into Git
3. Open any note, select a passage, ask it. An answer from your own note means it works
```

Requires: the Copilot plugin

Resource: Copilot https://community.obsidian.md/plugins/copilot · Dataview https://community.obsidian.md/plugins/dataview · Templater https://community.obsidian.md/plugins/templater-obsidian · Obsidian Stats https://www.obsidianstats.com

## 32. Can I play without an API key? How to start local models at zero cost?

You can, and it costs nothing. Running an open-source model locally needs no platform registration and no key, and the data never leaves your computer, so privacy is settled. Install Ollama, type two lines, you have output. The cost is your own hardware and slower answers; for short note Q&A that gap is a few seconds, no big deal. On desktop the whole thing runs in a few minutes, so take the local path first to learn what AI-reading-notes feels like, then pay for cloud once speed starts bothering you.

For memory-tight machines, confirm available memory before picking a model tier, do not force a big one (see Q37). On Android, Termux plus Ollama also runs small models at about 10 tok/s, slow but usable; the phone setup is in Q45.

Copy-paste template (use directly):

```bash
# No key at all, run locally (data never leaves the machine)
ollama pull qwen2.5:7b
ollama run qwen2.5:7b "introduce Obsidian in one sentence"

# Settings → Community plugins → Copilot → Options, fill these two, leave Key empty
# Base URL: http://localhost:11434/v1
# Model: qwen2.5:7b
```

Requires: Ollama and the Copilot plugin

Resource: Ollama https://ollama.com/

## 33. Copilot, Smart Connections, how to choose without agonizing?

Choose by the one thing you want most and you can decide in thirty seconds. Want to chat inside Obsidian, rewrite selected text, ask questions against your notes: Copilot. Want AI to recognize your vault on its own and surface related old notes while you write: Smart Connections, which embeds your notes so older ones float up mid-sentence. Want fully local RAG Q&A with no dependence on a chat interface: turn on Copilot's Vault QA mode against local Ollama, same tier of result.

There is also a path with no plugin at all: give a desktop AI read access to the vault folder, it builds its own index and can read and edit. To change a single note, pasting that file's full path is enough.

Installing all three at once is where the stuck begins. Install the one that fits today, use it for two solid weeks, then decide about a second.

Resource: Copilot https://community.obsidian.md/plugins/copilot · Smart Connections https://github.com/brianpetro/obsidian-smart-connections · ChatGPT https://chat.openai.com · Gemini https://gemini.google.com

## 34. Afraid of API key leakage, how to open an account most safely?

The worry is right, so set one hard rule first: a key never goes into the body of a note, and never into Git, private repos included, because commit history keeps it around. Do three things the day you open the account. Use a dedicated email to open a sub-account for the key, never your main mailbox. The moment the key is generated, store it in a password manager. Set a spend cap and an expiry date on that key in the provider console.

Rotation follows a fixed order, new key first, old key last, so service never drops. First generate a new key in the provider console and paste it only into your password manager. Then back in Obsidian, Settings → Community plugins → Copilot → Options → API Key, clear the old value by hand, paste the new one, save, and ask any question to confirm it still answers. Finally return to the provider console and hit Revoke on the old key. Run these three steps immediately when any of these hits: the key is 90 days old, you changed machines, the key appeared in a screenshot or recording, or your bill shows calls you did not make.

Copy-paste template (use directly):

```gitignore
# .gitignore at the vault root
# Plugin config files hold the key in plain text, so exclude the whole directory
.obsidian/plugins/
.obsidian/workspace.json
.obsidian/**/data.json

# Already committed before? Stop tracking first, then rotate the key
# git rm -r --cached .obsidian/plugins/
```

After that, run a full-text search for `sk-` across the vault. Zero results means it is clean.

Resource: 1Password https://1password.com/ · Bitwarden https://bitwarden.com/

## 35. How to install a local model (Ollama), minimum steps to run in half an hour?

Half an hour is plenty, four steps total: install Ollama from the site, pull a lightweight model with `ollama pull qwen2.5:7b`, go to Settings → Community plugins → Copilot → Options and fill Base URL `http://localhost:11434/v1` and Model `qwen2.5:7b`, then open today's diary and ask "which to-dos did I mention in this note". Once `curl http://localhost:11434/v1/models` returns a model list, the service is up.

Copy the model name character for character; one missing character in the tag after the colon breaks the connection, and that is where beginners stall most. On a 16GB Mac the system plus a browser leaves seven or eight GB, so 7B to 8B is what actually runs comfortably, and claims that 16G handles 13B are not worth believing. For a Chinese vault, swap the embedding before you start using it, see the next question.

Copy-paste template (use directly):

```bash
# 1. After installing Ollama, pull a lightweight model
ollama pull qwen2.5:7b

# 2. Confirm the service is alive (a model list means it works)
curl http://localhost:11434/v1/models

# 3. Settings → Community plugins → Copilot → Options → Add Custom Model
#    Base URL: http://localhost:11434/v1   local Ollama always uses this address
#    Model: qwen2.5:7b
#    API Key: leave empty

# Going cloud: swap Base URL for the provider's official endpoint, also ending in /v1, and fill the Key
```

Requires: Ollama and the Copilot plugin

Resource: Ollama https://ollama.com/ · Copilot https://community.obsidian.md/plugins/copilot

## 36. Chinese vault with default model fails, how to swap embedding and chat model?

The default embedding is trained on English and cannot hold Chinese semantics; two notes that clearly mean the same thing never match each other. Two swaps fix it: chat model to the qwen series, embedding to bge-m3, built for Chinese, 1024 dimensions, the balance point between quality and index size. bge-m3 is the most widely used Chinese embedding, available from both Ollama and SiliconFlow. A Chinese vault stuck at 0% indexing is usually this swap not done.

Swapping the embedding triggers a full re-index: a few minutes for a few hundred notes, half an hour for a thousand. Do not do it on deadline day. When it finishes, search a synonym pair once each; if they recall each other, the swap worked.

Copy-paste template (use directly):

```bash
# 1. Chat model to a Chinese-friendly one
ollama pull qwen2.5:7b

# 2. Embedding to Chinese-specialized bge-m3
ollama pull bge-m3

# 3. Settings → Community plugins → Copilot → Options → Embedding Model
#    (for Smart Connections: Settings → Community plugins → Smart Connections → Options)
#    Provider: Custom OpenAI
#    Base URL: http://localhost:11434/v1
#    Embedding Model: bge-m3

# 4. Verify: search a synonym pair; mutual recall means the swap took
```

Requires: Ollama and either the Copilot or Smart Connections plugin

Resource: bge-m3 https://huggingface.co/BAAI/bge-m3 · Ollama https://ollama.com/ · Smart Connections https://github.com/brianpetro/obsidian-smart-connections

## 37. Old computer with insufficient VRAM, which small models can run? State the cost?

The cost first, so you do not waste an afternoon: local models eat your own hardware, and comfort starts at GPU 8GB or Mac 16GB. A 16GB Mac realistically handles 7B to 8B and lags above that; a phone on CPU only produces about 10 tok/s, which does output text, slowly enough to test your patience.

If the machine really is old, drop a tier: `ollama pull qwen2.5:1.5b` or `qwen2.5:3b` handles summarizing, rewriting, and pulling to-dos out of a diary. Long-form reasoning is out of reach. If the smallest tier still stalls, change the approach: send the AI work to the cloud and keep only zero-compute helpers locally, like Various Complements, which completes from your own vault vocabulary with no model and no network, fast even on old machines.

Free tutorials claiming old machines run large models usually skip how long one answer takes. Measure speed first, then pick a tier. Beats forcing it.

Copy-paste template (use directly):

```bash
# Pick a tier by available memory (available, not total)
# under 8GB → qwen2.5:1.5b   summarize / rewrite / extract to-dos
# 8-16GB    → qwen2.5:3b     all the above + simple Q&A
# 16GB      → qwen2.5:7b     ceiling for daily Q&A, stop here
# 24GB+     → qwen2.5:14b    only with headroom to spare

# Measure once; below 5 tok/s, drop a tier
ollama run qwen2.5:3b --verbose "summarize what a linked note is in three sentences"
```

Requires: Ollama

Resource: Ollama https://ollama.com/ · Various Complements https://community.obsidian.md/plugins/various-complements

## 38. How to make AI answer only from "my notes", not make things up?

Turn on the vault-based switch; that is the one step that matters. There is a mode dropdown at the top of the Copilot chat pane, so set it to Vault QA before asking. It retrieves your notes first and organizes the answer around them, with training knowledge as backup only. Then add a hard requirement in the prompt: answer only from my notes, tag every conclusion with its source filename, and say so plainly when the vault has nothing.

An answer that can cite a real filename and pull up a three-month-old note against today's thinking holds up. Acceptance comes down to one check: an answer with zero filenames in it is made up, so restate the requirement and ask again.

Copy-paste template (use directly):

```
Answer only from the notes in my vault, following three rules:
1. Tag every conclusion with [[filename]]; if you cannot tag it, do not write it
2. If my notes do not cover it, reply "not in the vault", do not fill in with general knowledge
3. List the note titles you retrieved first, then start answering

Question: <write your question here>
```

Requires: the Copilot plugin, in Vault QA mode

Resource: Copilot https://community.obsidian.md/plugins/copilot

## 39. First time connecting AI, what should I ask to feel "an AI that gets me"?

Do not open with something an encyclopedia could answer. Ask what only your vault can answer. The most reliable opener: open today's diary and ask "which to-dos did I mention in this note, ordered by urgency". The moment it pulls the answer out of your own words, the feel arrives. If the diary habit has not formed yet, install Periodic Notes plus Calendar so one click on the date gives you that day's note, and AI has something to read.

On your first connection, run the five questions below in order; ten minutes tells you whether the setup is worth keeping.

Copy-paste template (use directly):

```
# The first ten minutes after connecting AI, ask these five in order
1. Which to-dos did I mention in this diary entry, ordered by urgency
2. Which three keywords repeat across my diary entries this month
3. What was I wrestling with last week, quote two lines of my own text
4. Which notes in my vault cover "<some topic>", and what does each one say
5. How does my view of "<some topic>" three months ago differ from this week

# If three of the five come back with real filenames, the setup is genuinely connected
```

Requires: the Copilot plugin, in Vault QA mode

Resource: Periodic Notes https://community.obsidian.md/plugins/periodic-notes · Calendar https://community.obsidian.md/plugins/calendar · Smart Connections https://github.com/brianpetro/obsidian-smart-connections

## 40. A private AI knowledge base usable offline, what is the minimum config?

Three things: a local model, a local vault, and not one cloud key filled in. Ollama runs the open-source model, the notes sit on your own disk, nothing external gets contacted, and it works with the cable pulled. The cost is slower answers and smaller models, and privacy is completely settled.

Once configured, run a real offline acceptance test: turn off Wi-Fi, open Obsidian, ask one question. An answer means genuinely private; no answer means something is still quietly reaching the cloud, so go to Settings → Community plugins → Copilot → Options and check whether Base URL points at a provider address when it should read `http://localhost:11434/v1`. Set folder rules at the same time: raw material only comes in and never gets edited, and AI writes only on its own patch.

Copy-paste template (use directly):

```
my-brain/
├── raw/          # raw material, only in, never edited
├── wiki/         # AI's territory
│   ├── index.md  # master index, updated after each operation
│   └── log.md    # operation log
└── AGENTS.md     # rules for AI

# In AGENTS.md write clearly: raw/ never modified; wiki/ generated and maintained by AI; index.md updated each time

# Offline acceptance: turn off Wi-Fi → open the vault → ask one question → an answer means truly private
```

Resource: Ollama https://ollama.com/

## 41. Cloud is strong, local is stable but weak, how to choose by scenario?

Skip the either-or, configure both sides, and cut by content sensitivity. Switching is nearly free: Settings → Community plugins → Copilot → Options, change the Model dropdown, five seconds.

| Dimension | Local model (Ollama + 7B) | Cloud API |
|---|---|---|
| Privacy | Data never leaves the machine, works offline | Content is sent to the provider's servers |
| Speed | Dozens of tokens per second on desktop, about 10 tok/s on phone CPU | Near instant, fast even on long text |
| Chinese capability | Fine for daily use after swapping to qwen plus bge-m3, clearly weaker at long reasoning | A tier more accurate at summary, rewriting, translation |
| Cost | No subscription, one-off hardware cost, 16GB Mac as the floor | Pay per token, tens of dollars a month for heavy use |
| Ease of setup | Install Ollama, pull a model, fill the endpoint, half an hour | Get a key, paste it, five minutes |
| Best for | Diary, client materials, unpublished drafts, finances and credentials | Public study notes, technical docs, long-form rewriting and translation |

If this content leaking would hurt, keep it local; if it would not, send it to the cloud and take the quality and speed. When unsure, go local, because regret costs far more than a few slow seconds. Before sending anything to the cloud, strip real names, company names, amounts, and contact details by hand. For borderline cases like meeting notes, anything touching personnel, compensation, or unannounced decisions goes local, the rest goes cloud.

Resource: Ollama https://ollama.com/ · Copilot https://community.obsidian.md/plugins/copilot

## 42. Which plugin is most hassle-free for sinking AI conversations into the vault?

Copilot is the most hassle-free; it lives inside Obsidian, so after chatting you select the passage and save it as a note without switching windows. Smart Connections covers the other half: it already reads your vault, so old notes touched by the conversation surface on their own and you link back casually.

The plugin only saves the hauling step. What turns a conversation into an asset is three extra lines when you save: the background you were in, the conclusion, the next action. Without those three lines, in three months you find a pile of text with no idea where it came from. Tag every conversation note with one shared property and let a Dataview block roll them up, and nothing slips.

Copy-paste template (use directly):

```markdown
---
type: ai-chat
date: 2026-01-05
topic: 
model: 
---

## Background
(what problem I was solving at the time)

## Conclusion
(one sentence, do not paste whole transcripts)

## Next step
- [ ] 

## Excerpts
(keep only the few lines that are actually useful)
```

Copy-paste template (use directly):

````markdown
```dataview
TABLE date AS Date, topic AS Topic, model AS Model
FROM ""
WHERE type = "ai-chat"
SORT date DESC
LIMIT 30
```
````

Requires: the Dataview plugin

Resource: Copilot https://community.obsidian.md/plugins/copilot · Smart Connections https://github.com/brianpetro/obsidian-smart-connections · Dataview https://community.obsidian.md/plugins/dataview

## 43. Too many plugins make the vault slow, how to control to just 2 being enough?

One rule: a specific pain point first, a plugin second, no stocking up in advance. At the AI-connecting stage two are enough, one for chatting, Copilot, and one to make AI recognize your vault, Smart Connections. Before the vault passes a hundred pages, Dataview and Templater can wait; install them when something actually blocks you, because by then you also know what you want from them.

The worst offenders are usually the plugins you forgot you installed. Clean house once a quarter with the routine below; five minutes usually cuts the list in half. Fewer plugins means a lighter vault and faster startup, which makes writing easier to keep up.

Copy-paste template (use directly):

```
# Quarterly plugin cleanup, five minutes
1. Settings → Community plugins, read the installed list top to bottom
2. For each one, ask yourself: have I used this in the last 30 days?
   - Cannot recall where → disable it (disable, do not uninstall, keep a week to change your mind)
   - Can name the exact case → keep it
3. Restart Obsidian after disabling, note the startup seconds and compare
4. Nothing missed within a week → uninstall
5. Before installing anything new, write one line: the specific problem I want it to solve is ___
   Cannot write it, do not install it
```

Resource: Copilot https://community.obsidian.md/plugins/copilot · Smart Connections https://github.com/brianpetro/obsidian-smart-connections · Dataview https://community.obsidian.md/plugins/dataview · Templater https://community.obsidian.md/plugins/templater-obsidian

## 44. I worry about data leakage, what are the three guardrails to set before connecting AI?

Set the guardrails before connecting AI; the other order comes too late. First, isolate private content: diary and client materials either go through a local model only, or get encrypted with Cryptomator before storage, and never sit in a folder AI can index. Second, review incoming content by hand: whatever AI generates or the web hands you gets one look from you before it enters the vault, with auto-import off. Third, shrink the outbound channel: keys only to the tool that needs them and rotated on schedule, plugins kept to the smallest set.

The risk splits into two conditions stacking: untrusted content plus an outbound channel, and real damage needs both at once, so cutting either one buys you a lot of safety. Three tiers of folder permission is the least effortful cut; copy the structure below.

Copy-paste template (use directly):

```
vault/
├── 00-private/     # diary, client materials, finances: fully invisible to AI
│                   # how: keep it outside the vault, or in a Cryptomator volume
├── 10-readonly/    # book excerpts, clippings: AI reads, never edits
├── 20-workspace/   # drafts, project notes: AI reads and writes
└── 90-ai-output/   # AI output lands here first, you review before moving into 20-

# Three self-checks before connecting AI
- [ ] Content in 00-private truly does not come back in AI retrieval
      (verify by searching a word that appears only there)
- [ ] AI output always lands in 90- first, with no permission to write straight into 10- or 20-
- [ ] Keys live in a password manager, and a full-text vault search on "sk-" returns nothing
```

Resource: Cryptomator https://cryptomator.org/

## 45. Can I run local AI on my phone, or is it only a sync endpoint?

It can run, but decide whether it is worth it first. On Android, Termux plus Ollama runs small models, CPU only at about 10 tok/s, and Obsidian mobile connects once Base URL is set to `http://localhost:11434/v1`. The cost is that the system killing the background kills the connection, so termux-wake-lock has to hold it, and your Android version and network config decide whether localhost is even reachable.

The easier division of labor: the computer runs the local model, the phone stays a sync and capture endpoint, and questions on the go go to the machine at home. If you genuinely need offline AI on the phone, accept the slowness and the fiddling, run the sequence below, and stop at whichever step blocks you.

Copy-paste template (use directly):

```bash
# Local model on a phone, verify in order, fall back to sync-only if it blocks
# 1. Install Termux, run this first
termux-wake-lock
# 2. Install Ollama, pull the smallest model (nothing larger on a phone)
ollama pull qwen2.5:1.5b
# 3. Start the service
ollama serve
# 4. Open http://localhost:11434 in the phone browser; "Ollama is running" means it works
# 5. Obsidian mobile → Settings → Community plugins → Copilot → Options
#    Base URL: http://localhost:11434/v1
#    Model: qwen2.5:1.5b
# 6. Background it for three minutes and come back; still answering means stable

# Fallback (recommended for most people): phone syncs and captures, the computer does the AI work
```

Requires: Termux, Ollama and the Copilot plugin

Resource: Ollama https://ollama.com/

## 46. Models update fast, will today's config be useless tomorrow? How not to be dragged by versions?

Part of it will break, so do not hard-code the config. AI plugins get dragged by versions harder than ordinary ones: embeddings reset and need hours of re-running, key formats change and need reconfiguring, model APIs get deprecated and need rollbacks, and as of 2026 there is still no built-in one-click downgrade, so guardrails are yours to build.

Three moves cover it: update one plugin at a time and use it for a round before the next; before updating, copy the whole `.obsidian/plugins/<plugin>` folder with a date suffix so you can paste it back; scan the changelog for breaking changes before you click update, especially on AI plugins.

Leave slack in your notes too. Do not hard-code command names, menu paths, and parameters into templates; add a line saying "follow the plugin's latest README", so a change on their side does not send you reconfiguring the whole vault.

Copy-paste template (use directly):

```bash
# Before updating any AI plugin, three steps
# 1. Back up the whole plugin folder with a date suffix
cp -r .obsidian/plugins/copilot .obsidian/plugins/copilot.bak-20260105

# 2. Read the changelog: search only for breaking / removed / renamed
# 3. Right after updating, verify three things:
#    - Is the model still reachable (ask anything, see if an answer comes)
#    - Is the index still there (search an old term, see if it recalls)
#    - In Settings → Community plugins → Copilot → Options,
#      are Base URL / Model / API Key still filled in

# Rollback: quit Obsidian → delete the new folder → rename the .bak- copy back → reopen
```

Requires: the Copilot plugin

Resource: Copilot https://community.obsidian.md/plugins/copilot · Smart Connections https://github.com/brianpetro/obsidian-smart-connections
