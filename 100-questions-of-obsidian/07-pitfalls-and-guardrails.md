# Chapter 7 · Pitfalls and Guardrails

Chapters one through six taught you how to drop the conversation into your own vault so AI actually works for you. This chapter flips the camera and walks the crash sites. Almost everyone steps into these pits, the only difference being early or late. Treat the eight below as cautionary tales, cheaper than waiting to hit them yourself.

## 93. The 5 pits beginners most easily step on

Beginners crash on the same handful of moves, so set three hard lines up front: no more than two always-on plugins, no folder deeper than two levels, and week one is for writing notes only, no system building.

The five pits are always the same: a dozen plugins in week one, folders nested four or five levels, a dozen forced links per note, importing a stranger's perfect structure, and thousands of notes never opened again. The self-check is easy to read. You reshuffled your folder structure five times this week and wrote no new notes. The vault takes several seconds to open. One graph node has a dozen lines hanging off it and you cannot say which one matters. You have thousands of notes and have not opened a single old one this month. Hit any two and stop adding anything, measure the three numbers below first.

Recovery goes subtract first, add later. Over the plugin limit, disable by the question "did I use this in the past week", do not delete yet, and uninstall only if you have not missed it in two weeks. Folders too deep, do not move files one layer at a time, create an MOC note at level two and hang the deep material off it as links, keeping the physical structure flat. Keep links few and deliberate, if you cannot say why two notes connect, do not connect them. Somebody else's vault belongs to them, and copying it means you spend day one organizing instead of writing.

```bash
# Run in the vault root. Whichever number is over the line, fix that one first.
ls .obsidian/plugins | wc -l
# Installed plugin count. Over 2 means disable a batch.

find . -type d -not -path "./.obsidian*" | awk -F/ '{print NF-1}' | sort -rn | head -1
# Deepest folder level. Over 2 means flatten with an MOC.

find . -name "*.md" -mtime -7 | wc -l
# Notes touched in the last 7 days. Zero means you are organizing, not writing.
```

```
# Beginner 5-pit checklist (if it hits, do the right column)
1 Installed a pile of plugins     -> keep 2, add more once those run smoothly
2 Folders nested 4 or 5 levels    -> max 2 levels, hang deeper stuff off an MOC
3 A dozen forced links per note   -> few and accurate, no reason means no link
4 Imported a stranger's structure -> write one or two real notes, let structure grow
5 Thousands of notes, never read  -> review monthly, do not farm a dead archive
```

Resource: Official getting started guide https://help.obsidian.md/Getting+started/Create+your+first+note · Official forum help category https://forum.obsidian.md/c/get-help/19

## 94. What happens to those who treat AI as "thinking for you"?

Treat AI as the thing that thinks for you, and what atrophies is your own judgment, and the process has no pain to it. The smoother it feels, the faster you atrophy, and by the time you notice, six months are gone. The position is simple: AI lays out the possibilities, and the judgment call stays with you.

Three signals say you are already in it. Scroll through your last ten notes, more than half the text came out of a model and you cannot point to a single sentence of your own judgment. That long article you had it summarize yesterday, you cannot restate the conclusion today, only that "it said the piece was good". Your first reaction to a blank page is to open a chat box, when you used to scribble three messy lines yourself.

The fix is to run it backwards. Stop asking for conclusions, start asking for problems. Write 200 words of your own first, then hand those 200 words over to be torn apart. Judge every hole it names, and whether you accept or reject it, add one line of reasoning. That line of reasoning is the part that belongs to you. Cut any AI-written passage in half before it enters the vault. The act of cutting forces you to decide which sentence earns its place, and the half that survives is a half you definitely read. AI is great at the grunt work of organizing and sorting, but it cannot do the thinking-for-you part, and it is no stronger there than a plain chat. Do not quietly hand over the judgment call.

```
# Reverse prompt: make the AI push my thinking instead of replacing it
You are my interrogator. No conclusions. No recommendations.

My rough thinking on <topic>:
<paste 200 words you wrote yourself, no ghostwriting>

Do only three things:
1 List every claim in my text that has no evidence behind it
2 Give three counter-scenarios I did not consider, one line each
3 Restate my core argument in one sentence so I can check you read it right

Then ask me one question and stop. Wait for my answer.
```

Depends on: any chat model; inside the vault, pair it with the Copilot plugin

Resource: Official forum knowledge management category https://forum.obsidian.md/c/knowledge-management/6 · Copilot https://community.obsidian.md/plugins/copilot

## 95. Connected AI but notes messier? How to avoid "AI junkyard"

Connect AI and the notes get messier because AI output and your own writing share one pool with no exit. Once the pool is dirty, searching your own stuff returns other people's machine text instead of your own words.

The self-check takes a minute. Search a keyword you know well, if three of the top five results are AI text you never read, the pool is already dirty. Then pick a note and ask whether you or the model wrote that paragraph. If you cannot tell, the problem is worse, because your vault has started lying to you. Two rules fix it: every AI artifact lands in `10-AI-drafts/` first, and anything you have not rewritten within a week gets deleted.

The action has two layers. Layer one tags every AI artifact with properties for origin and review state, since fixed fields are the only thing you can query later. Layer two runs the query below every Friday. Items on that list have exactly two fates: you rewrite them, set `reviewed` to true, and move them out of the draft folder, or you delete them. The rewrite standard is cut half, then add one sentence of your own judgment. Link only to what you have read. Auto-generated links look impressive, but every click lands on a sentence you have never seen, and the graph gets prettier and less useful at the same time.

```yaml
---
source: ai          # ai or me; every AI artifact is tagged ai
reviewed: false     # only true after you rewrote it
created: 2026-08-10
---
```

```
TABLE created AS Generated, file.folder AS Location
FROM "10-AI-drafts"
WHERE source = "ai" AND reviewed != true
  AND date(today) - created > dur(7 days)
SORT created ASC
```

Depends on: Dataview plugin, code block language set to dataview

Resource: Dataview https://community.obsidian.md/plugins/dataview · File Cleaner https://community.obsidian.md/plugins/obsidian-file-cleaner

## 96. Privacy three-piece set: private data, untrusted content, outbound channel

Local files are not the same as safe files. Obsidian stays open all day, the vault sits in plaintext most of that time, and any other program on the machine can read it. Work out who you are actually afraid of before deciding which layer to block. Encrypting everything on day one only makes your own workflow miserable.

Block the three things separately. Private data gets encryption, with sensitive directories wrapped before they sync. Untrusted content gets a human read, because models do make things up and you should glance at it before it lands. The outbound channel gets a judgment call, made before you paste a paragraph into a cloud model rather than after. Give an agent three tiers of folder permission: `private` is unreadable, `readonly` can be read but never modified, and only `work` allows it to create and edit. It touches the part you meant it to touch and nothing else. Never write a key into an md config that gets synced. Keep it in an environment variable or the system keychain, so even if the vault leaks, the thief only gets a placeholder they cannot read.

Two signals mean it already went wrong, and one command surfaces both: a key or password written in plaintext somewhere in the vault, and your API key sitting inside a plugin's `data.json`. Run the scan below. On a hit, move the content out of the vault immediately and rotate that key in the provider console. Deleting the note alone does nothing, since the key already passed through your sync history.

```bash
# Scan the vault root for plaintext secrets; act on any hit
grep -rnE "sk-[A-Za-z0-9]{20,}|api[_-]?key[[:space:]]*[:=]|password[[:space:]]*[:=]" . --include="*.md"

# Also confirm plugin configs are not holding a key in the clear
grep -rn "apiKey" .obsidian/plugins/*/data.json

# After a hit: move it out -> rotate the key in the console -> store it in the
# system keychain or an environment variable instead
```

```
# Three permission tiers for an agent (put this at the vault root)
private/    journal, medical, contracts, client lists   completely unreadable
readonly/   reading excerpts, meeting records           read only, no edits, no deletes
work/       drafts, project notes                       read and write, must be revertible

Before anything leaves: could I live with this paragraph sitting in a cloud
model's logs? If no, it stays in private/.
```

Resource: Cryptomator https://cryptomator.org/ · Meld Encrypt https://community.obsidian.md/plugins/meld-encrypt

## 97. Local models are not zero-cost, how to self-check and stop-loss on performance

Local models are not zero-cost. With lag, isolate the layer before you change anything, do not dive in swapping models, quantization, and backends at random.

Three steps isolate it, usually inside 30 minutes. Step one, enter safe mode with every plugin disabled and time a cold start. Still slow means plugins are innocent, so go look at the file count and oversized attachments in the vault itself. Step two, if the vault is fine, bisect the plugins: enable half, restart, and keep halving the slow side, which pins the culprit in four rounds at most. Step three, once plugins and vault are both clean, run the model on its own in a terminal and read the eval rate. Only that number describes the model. Run it outside Obsidian, and on a 16GB machine running a 7B model the measured rate sits in the double digits, so if the number falls well outside that range the problem is the model layer and has nothing to do with plugins.

Some signals mean stop pushing: a single answer takes over 30 seconds, other apps visibly stutter while the model runs, or you have already sunk three hours into making it work. Two of those and it is time to quit. The fallback plan, copy it as is: keep only short jobs like summarizing and rewriting on local hardware, move question answering to a pay-as-you-go cloud model, and if that still drags, turn every AI plugin off and get the vault itself running smoothly first. A usable vault matters more than a model that happens to run locally.

```bash
# Step 1, isolate: Settings -> About -> Restart and disable all plugins, time a cold start
find . -name "*.md" | wc -l
# Note count in one vault. Past the tens of thousands, consider splitting the vault.

find . -type f -size +50M -not -path "./.obsidian*" | head -20
# Oversized attachments. Move them outside the vault and reference by link.

# Step 2, bisect plugins: enable half -> restart -> keep halving the slow side, 4 rounds max

# Step 3, measure the model alone, outside Obsidian
ollama run <the model you use> --verbose "Explain backlinks in one sentence"
# Read eval rate. Well below the range for your hardware is a model-layer problem.
```

```
# Stop-loss lines (hit any two and stop pushing)
1 One answer takes over 30 seconds and you already dropped a tier
2 Other software visibly stutters while the model runs, fans pinned high
3 You have already spent 3+ hours just getting it to work
4 Memory pressure stays yellow or red (Activity Monitor / Task Manager)

Downgrade in three steps: local does summaries and rewrites only ->
question answering moves to pay-as-you-go cloud -> still rough, disable all AI plugins
```

Resource: Official help on debugging https://help.obsidian.md/Advanced+topics/Debugging · Ollama https://ollama.com/

## 98. Don't let conversations go to waste, but "full automation" is the bigger pit

Full automation is the bigger pit. Automation may move and file things, every trade-off and every deletion needs your nod. Earlier chapters taught you to capture conversations so they leave a trace. This one adds the other half: keep a hand on the wheel.

Three signals say you let go too far. You cannot name the three files the agent touched yesterday. Auto-generated digests older than a week are piling up unread. The agent's permissions include delete. The dangerous part of automation is handing over the trade-offs too. Letting it sort and file is fine, but the moment it also decides what stays and what goes, the vault drifts crooked with nobody noticing. Two guardrails, both installable today. The first is Git, which turns the vault into something revertible so you can pull work back after a bad edit, and before every AI plugin update back up its plugins subfolder so a bad one rolls back in seconds. The second is a whitelist that spells out what is automatic, what needs confirmation, and what never happens without you. Anything off the table waits for a human.

Spend two minutes a week on `git log` and scan what it touched. The more hands you keep on the work, the better grounded its future answers will be in what you actually accumulated.

```bash
# Give the vault an undo key
cd /path/to/vault && git init && git add -A && git commit -m "baseline"
printf ".obsidian/workspace.json\n.obsidian/cache\n.trash/\n" >> .gitignore

# Commit once at the end of each day
git add -A && git commit -m "daily $(date +%F)"

# It broke something: see what moved, confirm, then revert one file
git log --oneline -10
git diff HEAD~1 --stat
git checkout HEAD~1 -- "path/to/broken-note.md"
```

Depends on: Git command line, or the auto-backup option in the Obsidian Git plugin

```
# Automation whitelist (anything off this table waits for a human)
Automatic:      capture, file to inbox, add timestamps, move by tag, draft generation
Needs approval: rewriting body text, merging notes, renaming, bulk find and replace
Never:          delete files, empty folders, overwrite existing text, push to a public repo

Weekly: git log --oneline --since="7 days ago"
```

Resource: Obsidian Git https://community.obsidian.md/plugins/obsidian-git · Official help on file recovery https://help.obsidian.md/plugins/file-recovery

## 99. The second brain is mythologized, which promises you must never believe

The second brain is mythologized. Any promise containing "automatic", "once and for all", or "you never have to remember anything again" should be heard at half volume. The vault is your external drive and you are the CPU. Get that ordering right and it will not disappoint you. Using it as an external drive is genuinely convenient, but the moment you expect it to produce insight for you, disappointment is guaranteed. It cannot do the thinking, and what gets outsourced is only your reflection, at the cost of your own mind. Do not buy the sweet talk about "automatic".

Four signals say the myth got you. You have not pulled anything out of the vault on purpose this month. Asked what you have been thinking about, you can only open the vault and look. The vault keeps getting prettier while your output sits at zero. The graph looks magnificent, and clicking any node leaves you unable to say what it has to do with the work in front of you.

Run the five-question checkup once a month, five minutes, answers written into that month's note. You can also estimate a retrieval rate from the command line: if notes touched in the last 30 days are clearly a small share of the total, your vault is turning into a dead archive. It is strong at instant retrieval and at not losing things across years, and weak at producing insight on its own. Accept that boundary and you stop expecting it to grow a brain for you, and you also stop abandoning the whole vault when it fails to.

```
# Monthly second-brain checkup (1st of the month, 5 minutes, answers into that month's note)
1 How many times did I pull something out on purpose? Name the moments.
  Under 3 means storage without use.
2 How many times did this month's output cite a note older than six months?
  Zero means dead archive.
3 Among new notes, how many carry my own judgment rather than pasted text?
4 Is there a note I have still never read once? Read it before adding more.
5 If I switched tools, which 10 notes would I refuse to lose? Tag them. That is your core.
```

```bash
# Rough retrieval rate: notes touched in 30 days / total notes
find . -name "*.md" -mtime -30 | wc -l
find . -name "*.md" | wc -l
# Clearly a small share means the vault is going dead. Start with the five questions above.
```

Resource: Official forum knowledge management category https://forum.obsidian.md/c/knowledge-management/6 · Official help on graph view https://help.obsidian.md/plugins/graph

## 100. 3 things understood only after a year of use

Three lessons, each with something you can do today: less is more, AI drafts and you decide, the notes are yours.

First, less is more. The Obsidian team keeps cutting dependencies and shipping a security scorecard, and old plugins that fail the review will eventually disappear from the catalog, yet you keep stacking third-party plugins into the same vault. Run a plugin audit: delete the directories of plugins installed but never enabled, then open the repo of each enabled one and check the latest commit. Anything idle for well over a year means find a replacement. An abandoned plugin is the mine that blows up your vault for no obvious reason months later.

Second, AI drafts, you decide. Outlines and source material are fine work for a model. Which sentence gets cut, which stays, and how the piece concludes have to be yours. Ask three questions of every AI draft before it enters the vault: do I stand behind this judgment, is there one sentence here in my own voice, and what survives if I delete half. No answer means it does not get filed.

Third, the notes are yours. Verify that claim with a drill instead of holding it as a belief. Twice a year, close Obsidian, open five notes in a plain text editor, and see whether they still make sense. If they do, they really belong to you. If they do not, plugins have locked you in, and it is time to move the important content back into the body text.

```bash
# Plugin audit: compare what is installed against what is enabled
ls .obsidian/plugins
python3 -c "import json;print(json.load(open('.obsidian/community-plugins.json')))"
# Installed but not enabled: confirm the directory name, then delete it
# Enabled: open each repo, check the latest commit, replace anything idle for ages
```

```
# Exit drill (twice a year, 30 minutes)
1 Close Obsidian and open the vault folder in your system file manager
2 Pick 5 notes at random, open them in a plain text editor, see if they still read
3 Any of these means plugins have locked you in:
   the body is mostly dataview query blocks and goes blank without the plugin
   attachment paths are plugin-managed and every image breaks outside Obsidian
   key information lives only in a plugin's data.json and never reached the markdown
4 The fix: export your regular query views to a static list on a schedule,
   and keep body text in plain standard Markdown
```

Resource: Obsidian Stats https://www.obsidianstats.com · Official help on plugin security https://help.obsidian.md/plugin-security · Official help on file formats https://help.obsidian.md/file-formats
