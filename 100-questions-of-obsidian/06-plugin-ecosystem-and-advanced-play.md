# Chapter 6 · Plugin Ecosystem and Advanced Play: broaden horizons, don't get lost

Too many plugins make the vault slow, which makes it easier to quit. This chapter is not about filling plugins, but which to install, which not, and a few plays that broaden horizons. For advanced things, knowing the path exists is enough, do not rush in. However flashy the plugins, they serve your own accumulation; the root is still your vault.

## 83. Does Obsidian have official AI? If not, how to pick community plugins?

Obsidian itself does not do AI features; AI capability all comes from community plugins. Someone talking about the plugin ecosystem's future said the official prefers to be the base, leaving imagination to the community. Someone reviewed themselves, spent months tuning plugins, swapping themes, looked back to find not a single line written in the vault, all time spent on config. Plugins serve your accumulation, not reverse.

The order of picking plugins is problem first, plugin later, not reverse. You hit a specific stuck point, like wanting AI to Q&A based on notes, then search the corresponding plugin, not install whichever is hot. The common path is in settings turn off restricted mode, enter community plugin market search by name, remember to click enable after installing, many miss this enable step. The official does not choose for you; the mainstream few in the community (note-based Q&A, auto-link related notes) are validated by many people, start with one that best fits current need.

## 84. Which to install, which not: the 2-3 plugins most worth keeping in 2026

Someone compiled a big post of most underrated plugins; the highly upvoted are often those solving specific small pain points, not the fanciest. For personal vault plus AI in 2026, two or three are worth keeping.

Want to chat AI based on notes, process selected text: keep Copilot. Want AI to understand your accumulation, auto-surface related old notes while writing: keep Smart Connections. Want to run models locally not depending on cloud: Ollama plus Copilot with local address is enough. Someone uses an emerging whiteboard mind-map plugin for file-tree preview, but that is non-essential. Add others when you truly hit a pain point; fewer plugins in the vault the more stable, a consensus after years for many. Install a bunch and the vault only gets slow, you stop using it.

Copy-paste template (use directly):

```
# The 2-3 plugins most worth keeping in 2026
- Copilot: chat AI based on notes, process selected text
- Smart Connections: auto-surface related old notes while writing
- Ollama + Copilot local address: run models locally not depending on cloud
Add others when you truly hit a pain point; fewer plugins the more stable the vault.
```

## 85. Where to find templates and ready-made vaults? Besides building your own, anything you can copy directly?

Someone opening Obsidian for the first time stared at the blank page for two hours, not knowing what the first note should look like. You do not have to build the system from blank; many in the community have packaged their working flows into starter vaults and templates, fork one and tweak.

A few reliable entries: Vaultorial collects a bunch of free MIT-licensed starter vaults, daily notes, tasks, students, Zettelkasten, TTRPG all there, downloaded as zip no sign-up; Obsidian Garden Gallery's Vault Templates section curates productivity systems, academic flows, PARA/Zettelkasten frameworks, and you can also peek at others' digital gardens for inspiration; Vault Hub sorts templates, CSS snippets and dashboards by twenty-plus scenarios like student, developer, writer; the Templates section of the awesome-obsidian list names classic starts like LYT Kit, PARA Starter Kit, Obsidian Starter Templates. Chinese readers also have PKMer's vault market, with ready examples like a math knowledge base and a novel-writing vault.

Do not be greedy, pick one closest to how you think now, swap the example content for your own and you are on the road. Copying a working system is far faster than grinding from a blank page, and you also learn the folder and tag conventions others have iterated on.

## 86. Are bidirectional links = GraphRAG hype or really useful, how do ordinary users benefit?

Someone doing GraphRAG retrieval found impulsively linked links lower accuracy, needing to down-weight impulsive links. This shows links used by AI have a real mechanism, not pure hype, but the premise is linking accurately.

The benefit for ordinary users is concrete: the links you carefully made, AI along graph retrieval can find related notes keyword search cannot. Like you ask a concept, AI not only finds title-hit ones, but also pulls out the several linked via links, even if those notes never contained the word you asked. Few but accurate links, AI clearly understands you more. Random linking creates noise, that is where hype crashes. The premise of links being useful to you is always you first think clearly about the relationship between the two notes. Someone who wove their notes into an interconnected network found AI surfaced hidden associations they had not seen; this kind of serendipitous discovery from graph retrieval is exactly the most real benefit of links for ordinary users.

Copy-paste template (use directly):

```
# Mechanism of links used by AI (GraphRAG approach)
- Links you carefully made → AI promotes along graph retrieval, finds related notes keyword search cannot
- Links from auto-complete plugin → down-weighted, otherwise lowers accuracy
- Benefit: ask a concept, AI pulls out the several linked too, even if those notes never contained the word you asked
```

## 87. What is Agentic+MCP, and why is it "for those who want to go further"?

Someone used Claude plus Obsidian to build an automated loop, others used Hermes plus Claude Code to form a Trinity system, letting AI read the vault, write pages, maintain the index itself. This kind of play is called Agentic, paired with MCP letting AI directly operate your file system.

It is strong, but the threshold is high, needing to know how to set rules for AI, how to gate, otherwise AI messes up your vault itself. Someone used this framework for enterprise knowledge base, but that is an advanced need. For personal users, first get note-based Q&A, surfacing while writing smooth; Agentic is icing on the cake not snow in winter. Know the path exists, touch it when you want to play deeper later, do not let the cool demo lead your pace now. The picture of this play is a vault that becomes a personal wiki shared by human and agent, where the agent can read, search, build, and link, built once and reused forever. But the guardrail is here too: give the agent three tiers of folder permissions, private holds diary and trade secrets completely invisible to the agent, and only let it touch the part you want it to touch.

## 88. Let Claude / ChatGPT also read my vault, minimum viable connection?

Someone used Codex to push Obsidian to the extreme, others used Hermes plus Claude Code to let external AI read the vault directly. The minimum viable connection is write a user manual for the vault, let external AI read by it.

The method is put a CLAUDE.md at the vault root, explaining the vault's structure and rules, external AI reads this and understands your accumulation, no need to explain each time. Someone used the LLM Wiki approach, splitting raw and wiki layers, external AI first reads wiki/index.md to understand the whole then answers. This connection does not depend on a specific plugin; Claude, ChatGPT can read your vault by this manual. You write the manual once, later whichever AI reads is universal, more flexible than binding to one plugin. Harder-core still is the official CLI, letting an agent send commands straight to the running Obsidian, moving files while auto-maintaining links and querying all tags for minimal tokens without scanning the whole vault. This is another path of local-first plus cost-down.

Copy-paste template (use directly):

```
1. Put a CLAUDE.md at vault root, write clear structure and rules (see folder structure in Q40)
2. Drag the vault folder directly to Claude / ChatGPT, or configure filesystem MCP
3. First conversation let it read CLAUDE.md and wiki/index.md to understand the whole
4. After that ask "answer based on my notes", it reads your vault by this manual
```

## 89. Where to follow news, tutorials, community? How not to drown in the tutorial sea?

Someone installed plugins for months, swapped several themes, looked back to find not a single line written, all time spent on config. Obsidian's tutorials and shares are enough to drown you; follow the wrong sources and you burn a whole week watching how others play while your notes stay untouched.

Pick a few high-quality sources: Obsidian Roundup is a community-maintained weekly digest, new plugins, new plays, pitfalls all summed up; the official forum and the Chinese forum have real Q&A and example-vault shares; Reddit's r/ObsidianMD and the official Discord are the front line of seeing how others use it; Chinese readers follow SSPAI and AllinBon, plus PKMer's tutorials and Chinese plugin docs. The awesome-obsidian and awesome-obsidian-zh lists gather plugins, themes, templates, converters in one place, check them first when searching.

One guardrail: subscribe to three or five curated sources, scan periodically, do not follow every tutorial. What you see is someone else's system, not your pass line. Stash the inspiration you catch into the inbox, go back when you actually use it, far easier than copying on the spot.

## 90. Besides the official market, where else to hunt plugins and themes? How to install smoothly in China? How to pick without getting burned?

Someone following a tutorial to install a plugin, clicked browse and got a load failure, stuck at the door for half a day. The official community plugin market is the most direct entry, but direct connection from China often hiccups, the most common hurdle for Chinese readers.

Where to hunt: the official new Obsidian Community is a unified directory of plugins plus themes, filter by category, each project with screenshots and a safety scorecard; Obsidian Stats ranks by downloads, stars and update activity, and shows Beta plugins not yet in the official market; Obsidian Mate browses themes, plugins, vaults in one place; the awesome-obsidian list gathers classic projects by category. Smooth install in China: use PKMer's Market plugin, one-click accelerated download of official-market plugins and themes, with Chinese docs, a free monthly quota after sign-up, basically saying goodbye to network anxiety. Pick without getting burned: first see downloads and stars, mass-market plugins with tens of thousands of downloads are usually stable; then see recent updates, half a year idle may mean abandoned; plugins with network permission or file reading deserve an extra look at reviews, install only those you trust.

Remember, before installing think clearly which specific stuck point to solve, do not install whichever is hot.

## 91. My vault gets slower with use, how to health-check and slim down?

Someone timed with a stopwatch, listed which plugins especially slow performance, the conclusion consistent: more installed, slower. The first step of health check is look at plugin count, turn off unused ones. Others stuffed the vault with thousands of images and large PDFs, global search and startup noticeably slower, especially on mobile, because large attachments eat the most memory and sync quota.

Someone specifically health-checks the vault, finding which pages are sourceless islands, which concepts repeatedly mentioned but not independent pages, which connections are noise. The hard truth of slimming is less is more, cut plugins to two or three, subtract notes, the vault naturally fast. Someone switched from pursuing perfect structure to dropping real ideas into the inbox every day, and the vault got lighter. You do a round of health check periodically, delete islands, merge duplicates, turn off idle plugins, the vault's health is kept, do not wait until too slow to use to clean up. There is also a handy hard metric: use one command to list all tags by count, checking island notes costs only about a hundred tokens while scanning the whole vault takes millions, and the agent understands structure and heals broken links, far more efficient than flipping through the vault by hand.

Copy-paste template (use directly):

```
# Find orphan pages (no inlinks, no one can link to)
LIST FROM "" WHERE length(file.inlinks) = 0
SORT file.mtime DESC

# Or install Vault-Physician plugin, one-click health check: orphan pages / duplicates / broken links
```

## 92. Want to migrate away from Obsidian, can local Markdown really leave anytime?

Someone managing a library of forty thousand files, when migrating relied on this confidence of local Markdown. Your notes are plain-text files, not locked in some private format, this is Obsidian's hardest trump card.

When switching tools, drag folders and md files away directly, links still work in tools supporting Markdown. Someone migrating from another tool made confirming the target is pure local Markdown their first move, so they can leave anytime in the future. Cloud note software dies and your material hangs; local Markdown not afraid of this. The premise of leaving anytime is you always use plain text, never stuff content into some plugin's proprietary private format. Hold this line, Obsidian is just one of your many exits, not a cage.
