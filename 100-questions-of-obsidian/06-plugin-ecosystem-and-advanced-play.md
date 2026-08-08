# Chapter 6 · Plugin Ecosystem and Advanced Play: broaden horizons, don't get lost

Too many plugins make the vault slow, which makes it easier to quit. This chapter is not about filling plugins, but which to install, which not, and a few plays that broaden horizons. For advanced things, knowing the path exists is enough, do not rush in.

## 83. Does Obsidian have official AI? If not, how to pick community plugins?

Obsidian itself does not do AI features; AI capability all comes from community plugins. Someone talking about the plugin ecosystem's future said the official prefers to be the base, leaving imagination to the community.

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

## 85. Little-known but useful small plugins (tags / graph / review types)?

Someone specifically compiled underrated plugins, several solving small but real pain points. The one that smartly auto-completes links by vault title while typing, links the right note on impulse, reducing manual search. The file-tree plugin with preview cards, hover to see note content without opening.

There are also review types, pulling old notes by your set frequency, used with periodic notes. The highly upvoted in the most-underrated-plugin post are mostly this kind of silent nourishing, not the eye-catching large-model type. When picking, see which specific inconvenience it solves, not the download ranking. One or two small plugins enough; too many and the vault gets slow too, this line you must hold yourself.

## 86. Are bidirectional links = GraphRAG hype or really useful, how do ordinary users benefit?

Someone doing GraphRAG retrieval found impulsively linked links lower accuracy, needing to down-weight impulsive links. This shows links used by AI have a real mechanism, not pure hype, but the premise is linking accurately.

The benefit for ordinary users is concrete: the links you carefully made, AI along graph retrieval can find related notes keyword search cannot. Like you ask a concept, AI not only finds title-hit ones, but also pulls out the several linked via links, even if those notes never contained the word you asked. Few but accurate links, AI clearly understands you more. Random linking creates noise, that is where hype crashes. The premise of links being useful to you is always you first think clearly about the relationship between the two notes.

Copy-paste template (use directly):

```
# Mechanism of links used by AI (GraphRAG approach)
- Links you carefully made → AI promotes along graph retrieval, finds related notes keyword search cannot
- Links from auto-complete plugin → down-weighted, otherwise lowers accuracy
- Benefit: ask a concept, AI pulls out the several linked too, even if those notes never contained the word you asked
```

## 87. What is Agentic+MCP, and why is it "for those who want to go further"?

Someone used Claude plus Obsidian to build an automated loop, others used Hermes plus Claude Code to form a Trinity system, letting AI read the vault, write pages, maintain the index itself. This kind of play is called Agentic, paired with MCP letting AI directly operate your file system.

It is strong, but the threshold is high, needing to know how to set rules for AI, how to gate, otherwise AI messes up your vault itself. Someone used this framework for enterprise knowledge base, but that is an advanced need. For personal users, first get note-based Q&A, surfacing while writing smooth; Agentic is icing on the cake not snow in winter. Know the path exists, touch it when you want to play deeper later, do not let the cool demo lead your pace now.

## 88. Let Claude / ChatGPT also read my vault, minimum viable connection?

Someone used Codex to push Obsidian to the extreme, others used Hermes plus Claude Code to let external AI read the vault directly. The minimum viable connection is write a user manual for the vault, let external AI read by it.

The method is put a CLAUDE.md at the vault root, explaining the vault's structure and rules, external AI reads this and understands your accumulation, no need to explain each time. Someone used the LLM Wiki approach, splitting raw and wiki layers, external AI first reads wiki/index.md to understand the whole then answers. This connection does not depend on a specific plugin; Claude, ChatGPT can read your vault by this manual. You write the manual once, later whichever AI reads is universal, more flexible than binding to one plugin.

Copy-paste template (use directly):

```
1. Put a CLAUDE.md at vault root, write clear structure and rules (see folder structure in Q40)
2. Drag the vault folder directly to Claude / ChatGPT, or configure filesystem MCP
3. First conversation let it read CLAUDE.md and wiki/index.md to understand the whole
4. After that ask "answer based on my notes", it reads your vault by this manual
```

## 89. Multi-agent debate looks cool, why avoid it daily?

Someone showed multi-agent debating play, looks impressive, but daily personal vault does not need it. Its value is in enterprise-level knowledge base complex scenarios, not you taking notes answering your own questions.

Daily AI use, note-based Q&A, surfacing while writing, producing draft, these three cover most needs. Multi-agent debate needs gating, managing multiple models' outputs, complexity kills your motivation first. Someone used this for enterprise retainer, but that is an external paid service, not personal note flow. What you want daily is peace of mind, not watching AIs hold a meeting. Master the basic few, more real than chasing cool architecture, do not let config performance take your note time.

## 90. Plugin command names keep changing, how to write notes not dragged by versions?

Community plugin command names and shortcuts change with versions; someone specifically reminded that when citing specific commands note "follow the plugin's latest docs". Then writing notes will not be dragged by versions.

The method is for key operations do not only record command names, record what problem it solves and roughly where to set. Like sync, you record "use Git plugin for private repo backup", specific command name changed you can also find in settings. Someone wrote sync solutions, listed eleven, but the core idea unchanged, only the entry position changes. You record intent and path, not a precise button name of some version, next plugin update you re-click by the idea, no rewrite the whole note.

## 91. My vault gets slower with use, how to health-check and slim down?

Someone timed with a stopwatch, listed which plugins especially slow performance, the conclusion consistent: more installed, slower. The first step of health check is look at plugin count, turn off unused ones.

Someone specifically health-checks the vault, finding which pages are sourceless islands, which concepts repeatedly mentioned but not independent pages, which connections are noise. The hard truth of slimming is less is more, cut plugins to two or three, subtract notes, the vault naturally fast. Someone switched from pursuing perfect structure to dropping real ideas into the inbox every day, and the vault got lighter. You do a round of health check periodically, delete islands, merge duplicates, turn off idle plugins, the vault's health is kept, do not wait until too slow to use to clean up.

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
