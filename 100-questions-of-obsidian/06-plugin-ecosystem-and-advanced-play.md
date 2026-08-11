# Chapter 6 · Plugin Ecosystem and Advanced Play: broaden horizons, don't get lost

Too many plugins make the vault slow and easier to quit. This chapter is not about filling your vault with plugins. It is about which ones to install, which ones to skip, and a few plays worth knowing exist. For the advanced stuff, knowing the road is there is enough; do not rush down it on day one. However flashy a plugin is, it serves what you accumulate. The root is still your vault.

## 83. Does Obsidian have official AI? If not, how to pick community plugins?

Obsidian ships no built-in AI, and every AI capability comes from community plugins, so waiting for an official feature is waiting forever and judging plugins is a skill you have to build yourself. In May 2026 the official Obsidian Community catalog went live and gives every plugin a safety scorecard, so for the first time you have an official safety grade to weigh instead of guessing from download counts.

Use three hard checks before installing anything, and put it back unless you get three yeses. First, update frequency: open the GitHub repo and confirm the latest commit is within six months, which tells you the author is still around. Second, issue response: sort issues by newest and read the last ten; if the author replied to more than half, you have a maintainer to ask when things break. Third, scope: the top of the README should explain the plugin in one sentence. A plugin bundling seven unrelated features brings a maintenance risk and a performance cost together. Plugins that fail the new automated review are eventually phased out, which is a new thing to factor in. What matters more is that a community plugin can read any file in your vault, so every extra supply chain hop is extra risk.

The install path is Settings → Community plugins → turn off Restricted mode → Browse → search by name → Install, then go back to the list and flip the toggle on. That last step is the one people skip, and an installed plugin that is never enabled does nothing.

```
# Three questions before installing (write the answers down; fewer than 3 yeses, skip it)
1 Update frequency: GitHub → Commits. Is the latest commit within 6 months?
2 Issue response: Issues sorted by newest. How many of the last 10 got an author reply?
  Fewer than 5 counts as a no
3 Scope: does the top of the README explain it in one sentence?
  More than 3 unrelated features counts as a no
Extra: check download count in the market. For niche plugins under 10k downloads,
install only when all three answers are yes.
After installing, write one line: I installed this to fix ______.
If you cannot fill the blank, uninstall it.
```

Resource: Obsidian Stats https://www.obsidianstats.com · Official plugin directory https://obsidian.md/plugins

## 84. In 2026, which 2-3 plugins are worth keeping, and which should I skip?

Keep your always-on plugin count under three, and for every extra one you should be able to name the step it removes from your day. A programmer rewrote Homepage and Nldates down to a few dozen lines and replaced Obsidian Git with a cronjob, all for one reason: a plugin can read every note in your vault, so install none you can do without. That is the same posture as the official "less is safer" stance.

On the personal vault plus AI track, only three capabilities earn a permanent slot: asking questions against your notes, surfacing old notes while you write, and running a model locally. The concrete mapping: Copilot handles note-based Q&A and acting on selected text. Smart Connections pushes related old notes into the sidebar as you type. Ollama pulls the model onto your machine, and once Copilot points at that local address, your chats stop leaving the laptop. Install all three, use them for two weeks, and disable whichever one you never opened on purpose.

The category to skip is anything that only changes how things look: flashy themes, animations, decorative dashboards. They load on every start and pay off only on day one.

```
# 1 After installing Ollama, pull a small model that is good enough
ollama pull qwen2.5:7b
# 2 Let Obsidian reach the local service, then restart Ollama
launchctl setenv OLLAMA_ORIGINS "app://obsidian.md*"    # macOS
setx OLLAMA_ORIGINS "app://obsidian.md*"                # Windows
# 3 Copilot settings → Model → Add Custom Model
#   Provider: ollama   Base URL: http://localhost:11434   Model: qwen2.5:7b
# 4 Verify: disconnect from the network and ask a question.
#   An answer means you are on the local model.
```

Resource: Copilot https://community.obsidian.md/plugins/copilot · Smart Connections https://community.obsidian.md/plugins/smart-connections · Ollama https://ollama.com

## 85. Where to find templates and ready-made vaults? Besides building your own, anything you can copy directly?

Do not build a system from a blank page, and do not worship another user's finished vault. A five-year forum user warned that starting from an empty vault and skipping other people's starter kits is the better path, because another user's structure grew around their own head and you will only keep reading their vault instead of writing your own. A live counterexample is Ideaverse Zero, which ships with thirty community plugins enabled by default and on an older laptop makes characters appear seconds after you type. The culprit is exactly that pile of preinstalled plugins.

If you want to copy, pick the skeleton closest to what you actually do this month, then replace its sample content with three real notes of your own the same day. If your material will not fit, that structure is wrong for you. Delete it and try the next one. For an MOC-style opening with Chinese-language docs, LYT Kit has a Mandarin repo you can clone and edit. Once you have it, clear the stage first: move every sample note outside the template folder and keep only the folder skeleton and the template files. Leave the samples in and you will keep reading another person's vault.

```
# Grab an MOC skeleton and turn it into your own vault
git clone https://github.com/nickmilo/LYT-Kit-in-Mandarin.git my-vault
cd my-vault && rm -rf .git
# List the sample notes first and eyeball them before running the next line
find . -name "*.md" -not -path "./Templates/*"
# Move samples into a holding folder, delete it tomorrow
mkdir -p _to-delete
find . -name "*.md" -not -path "./Templates/*" -not -path "./_to-delete/*" -exec mv {} _to-delete/ \;
# In Obsidian: Open folder as vault → pick my-vault → start with three real notes
```

Resource: LYT Kit in Mandarin https://github.com/nickmilo/LYT-Kit-in-Mandarin · Obsidian forum https://forum.obsidian.md

## 86. Are bidirectional links = GraphRAG hype or really useful, how do ordinary users benefit?

Really useful, on one condition: your links are few and deliberate. The payoff of graph retrieval comes from the relationship each link carries. Let autocomplete wire up every matching phrase and every node points at everything, which carries no information at retrieval time.

The benefit for an ordinary user is concrete. You ask about a concept, and beyond the notes whose titles match, the model pulls in the pages linked to them, even when those pages never contain the word you asked about. Keyword search cannot produce that recall.

The action you can take today is to measure your own link quality. A developer hit "vault rot" at four hundred notes and said the rot is not about individual notes being badly written, it is a graph problem. First list notes with more than 20 outgoing links; most of them are junction pages polluted by autocomplete, so cut each down to five links you can explain out loud. Then list long notes with zero outgoing links and give each one real parent link. After those two passes, graph retrieval gets visibly sharper.

```dataview
TABLE length(file.outlinks) AS "Outlinks", file.folder AS "Folder"
FROM ""
WHERE length(file.outlinks) > 20
SORT length(file.outlinks) DESC
```

```dataview
LIST
FROM ""
WHERE length(file.outlinks) = 0 AND file.size > 500
SORT file.mtime DESC
LIMIT 30
```

Resource: Graph Analysis https://community.obsidian.md/plugins/graph-analysis · Dataview example vault https://github.com/s-blu/obsidian_dataview_example_vault

## 87. What is Agentic+MCP, and why is it "for those who want to go further"?

Hold off on this road for now. There is one test: does your vault already contain an operation you repeat three or more times a week with fixed steps, such as rolling scattered to-dos out of daily notes into one page, or backfilling frontmatter on new notes? With work like that, handing it to an agent pays. Without it, you will just watch the thing idle.

Separate the two terms first. Agentic means the model decides how many steps to take and which tool to call to finish a job, without you feeding instructions one line at a time. MCP is a standard interface that lets a model read and write your local files and apps. On the Obsidian side, the Local REST API plugin opens a port on your machine for the client to connect to. A trusted long-time writer actually wired a filesystem MCP server into her own vault and concluded it was unusually reliable compared with most AI tools she had tried, because the interface the model gets is constrained, explicit, and verifiable, which shrinks the room for hallucination.

Roll it out in three steps: split your folders into three visibility tiers, put a rules file at the vault root, then run it read-only for a week. Check whether it ever reached into private. If it never did, grant write access.

```
# Put this at the vault root as CLAUDE.md or AGENTS.md; the agent reads it first every session
## Folder permissions (three tiers; crossing a line stops the run)
- 00-private/   Never read. Journals, medical records, contracts, account hints live here
- 10-inbox/     Read only. You may cite it, you may not edit it
- 20-notes/     Read and write. New notes go here and nowhere else
## Write rules
1 Print a diff for any write and wait for me to reply "approved" before applying it
2 Never delete a file; move it to 99-trash/ instead
3 Every new note carries frontmatter: title / created / tags
4 Preserve existing links when editing; never flatten [[a link]] into plain text
5 End each turn with the list of files you read and the files you changed
```

Resource: MCP docs https://modelcontextprotocol.io · Local REST API https://community.obsidian.md/plugins/obsidian-local-rest-api

## 88. Let Claude / ChatGPT also read my vault, minimum viable connection?

There are two tiers, chosen by how often you use it. If you ask a few questions a week and each one touches a handful of notes, dragging those folders into the chat window is enough, with zero setup. Only when you want it reading and writing the whole vault across sessions does MCP earn its keep.

Either way, put a manual at the vault root first. An outside model has none of your context. It does not know that inbox holds fragments while notes holds finished writing. The manual is where you stop repeating that. Spell out what each folder means, your naming rules, your link syntax, and which folders are off limits. Write it once and it outlives any single model.

The minimum setup for tier two: install the Local REST API plugin, copy the API key out of it, paste it into your client's MCP config, restart. Then ask it to list the top-level folders in your vault. Once that comes back correct, go on.

```
# README-for-AI.md at the vault root; the model reads this before anything else
This vault is plain local Markdown. Folder meanings:
- 00-private/  Never read. Do not cite anything inside under any circumstance
- 10-inbox/    Unsorted fragments. Citable, never treat as a conclusion
- 20-notes/    Finished notes. Prefer these when answering
- 30-refs/     Excerpts and sources. Always name the source file when citing
Rules:
1 Every answer cites its source in [[filename]] form
2 If the vault does not cover it, say "not covered in the vault" instead of
  filling the gap with general knowledge
3 To create a note, print the full Markdown and let me save it myself
```

```json
// Add this to the Claude Desktop config file and restart the client
// macOS: ~/Library/Application Support/Claude/claude_desktop_config.json
{
  "mcpServers": {
    "obsidian": {
      "command": "uvx",
      "args": ["mcp-obsidian"],
      "env": {
        "OBSIDIAN_API_KEY": "paste the key from the Local REST API plugin",
        "OBSIDIAN_HOST": "127.0.0.1"
      }
    }
  }
}
```

Resource: mcp-obsidian https://github.com/MarkusPfundstein/mcp-obsidian · Local REST API https://community.obsidian.md/plugins/obsidian-local-rest-api

## 89. Where to follow news, tutorials, community? How not to drown in the tutorial sea?

Subscribe to a dozen sources and copy every new trick the day you see it, and you end up with a vault full of half-finished configs. The tutorial sea drowns people because it updates faster than you practice, so you stay busy chasing while your vault stays empty. Collecting a pile of setups feels like producing, but it only mimics productivity. That is the "information collector's fallacy," so admit this up front: collecting by itself makes nothing.

Three types are worth keeping. A community weekly that rounds up new plugins and known pitfalls, ten minutes a week. A live Q&A floor where searching your exact error message beats watching a tutorial. One index list that sorts plugins, themes, and templates by category, so you check it before you go hunting. Keep your source list under five, favor weekly digests, skip anything that publishes daily.

The guardrail is a rule about action, not about reading. Anything you find goes into the inbox first, with a line naming the specific problem it solves for you. Look again a week later and only build it if you can still state the problem. Most entries do not survive that week, which is exactly the point.

```
# New file in 10-inbox/, named: idea-YYYYMMDD-keyword
---
type: idea
source: original link
created: 2026-08-10
review: 2026-08-17
---
Which specific problem of mine does this solve:
(if you cannot answer, delete this note instead of saving it)
First step I would take:
(one sentence, doable in 20 minutes)
Verdict after one week: adopt / drop
```

Resource: Obsidian forum https://forum.obsidian.md · awesome-obsidian https://github.com/kmaasrud/awesome-obsidian

## 90. Besides the official market, where else to hunt plugins and themes? How to install smoothly in China? How to pick without getting burned?

Third-party directories are for research only, where you compare downloads, update activity, and betas that have not reached the official market yet. The actual download goes through the official market or the author's GitHub Releases page. A plugin is code that can read every file in your vault, and every extra hop in its supply chain is extra risk. When the market will not load, work through it in order. Check whether the network is the problem: if the browser opens GitHub while the in-app market does not, the client's channel is blocked. Next, install by hand, pulling three files from the author's Releases page into your plugins folder, which depends on no acceleration service at all. If you do need a mirror service, pick one whose version numbers match the official repo.

Three red lines when picking: no update in six months, network permission with no explanation of what gets sent, and an archived repo. Any one of them, walk away. Whiteboard mind-map plugins deserve extra care: one user reported a plugin that wiped the original file content clean on reopen. That "dynamic layout" need clashes with the static nature of a whiteboard, so for large mind maps a dedicated tool stays the safer bet.

```
# Manual install (for when the in-app market will not load; dataview as the example)
# 1 Download three files from the author's Releases page: main.js  manifest.json  styles.css
# 2 The folder name must be the id from manifest.json, not a name you invent
mkdir -p "<your-vault>/.obsidian/plugins/dataview"
mv ~/Downloads/main.js ~/Downloads/manifest.json ~/Downloads/styles.css \
   "<your-vault>/.obsidian/plugins/dataview/"
# 3 In Obsidian: Settings → Community plugins → Reload plugins → flip the toggle on
# 4 Cross-check: version in manifest.json must match the Releases tag. If not, redo it.
```

Resource: PKMer https://pkmer.cn · Official plugin directory https://obsidian.md/plugins

## 91. My vault gets slower with use, how to health-check and slim down?

Slowness is not about note count. The CEO himself runs forty thousand markdown files just fine. A developer hit "vault rot" at four hundred notes and nailed it: the rot is not about individual notes being badly written, it is a graph problem. The two real sources of slowness are the number of always-on plugins and the size of your attachments. Work through them in that order and most vaults stop choking.

Step one, count plugins. Check the enabled count in settings and disable in batches, restarting after each batch and writing down the startup time. Obsidian ships a near-unknown stopwatch tool at Settings → General → Advanced → click the stopwatch icon, and it lists each plugin's startup cost so you can copy it to the clipboard. One user used it to trace Templater dragging startup from ten seconds to one or two minutes, and replacing it dropped right back to under ten. Step two, audit attachments. Run a command at the vault root to find files over 5 MB, then move big PDFs and screen recordings outside the vault and reference them by absolute path. Step three is the content check, with the three Dataview queries below.

Here is what healthy looks like. An orphan note with zero backlinks may have great content but is functionally invisible, so the more of them you have the more the vault rots. Notes missing frontmatter are invisible to every query you will ever write, so drive that number toward zero. Handle whatever the queries return the same day rather than saving it for a later round.

```dataview
TABLE length(file.inlinks) AS "Inlinks", length(file.outlinks) AS "Outlinks", file.mtime AS "Modified"
FROM ""
WHERE length(file.inlinks) = 0 AND length(file.outlinks) = 0
SORT file.mtime ASC
```

```dataview
TABLE file.folder AS "Folder", file.mtime AS "Modified"
FROM ""
WHERE length(values(file.frontmatter)) = 0
SORT file.mtime DESC
LIMIT 50
```

```dataview
TABLE file.size AS "Bytes", file.folder AS "Folder"
FROM ""
WHERE file.size < 200
SORT file.size ASC
```

```
# Attachment audit (run at the vault root)
find . -type f -size +5M -not -path "./.obsidian/*" -exec du -h {} + | sort -rh | head -20
find . -name "*.md" -not -path "./.obsidian/*" | wc -l    # total notes
du -sh .                                                   # total vault size
```

Resource: Vault Physician https://github.com/tejnaren07/vault-physician · Obsidian forum https://forum.obsidian.md

## 92. Want to migrate away from Obsidian, can local Markdown really leave anytime?

You can leave anytime, as long as your body text has not been captured by plugin syntax. A direct self-test: disable every community plugin, restart, and open ten notes at random. If the screen fills with code blocks and fields that no longer render, that content is now tied to a plugin.

Count before you move. Dataview blocks, tasks markers, and excalidraw files all degrade into raw text in another editor. If there are only a few, rewrite them as static content by hand. If there are many, gather them into one folder and deal with them separately at migration time so they stay out of your body text. A vault of forty thousand files migrated by copying the folder to a new machine, which shows local Markdown portability holds at that scale.

The move itself is two things: copy the whole folder, and copy the attachment folder with it. Wiki-style links work as-is in any editor that supports them, and for editors that do not, one command converts them to standard Markdown links. Run that conversion on the backup copy first.

````
# 1 Pre-migration audit (run at the vault root)
grep -rl '```dataview' --include=*.md . | wc -l      # notes that need Dataview to render
grep -rl '```tasks'    --include=*.md . | wc -l
find . -name "*.excalidraw.md" | wc -l
# 2 Back up before touching anything
cp -R "<your-vault>" "<your-vault>-backup-$(date +%Y%m%d)"
# 3 Convert [[wiki links]] to [title](title.md), on the backup copy only
grep -rl '\[\[' --include=*.md . | xargs sed -i '' -E 's/\[\[([^]|]+)\]\]/[\1](\1.md)/g'
# macOS uses sed -i '', Linux uses sed -i
# 4 Check: open 10 random notes in a plain text editor; links and image paths still resolve
````

Resource: Obsidian Help https://help.obsidian.md
