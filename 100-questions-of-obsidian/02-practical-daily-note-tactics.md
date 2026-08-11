# Chapter 2 · Practical Daily-Note Tactics

This chapter is not about AI. Get the act of note-taking right first, and AI will have something worth reading later.

Eight hundred notes and you cannot pull one out when you need it. The count is rarely the problem. Most of what you stored was the kind of thing that loses value the moment it is written down, links were added densely and without reason, the same concept carries three different tag spellings, and attachments are scattered all over the vault. None of these is fatal on its own. Pile them up and the vault starts to rot, and the rot is not located in any single badly written note, it sits in the shape of the whole graph.

The sixteen questions ahead run from how to capture, how to link, how to tag, how to name, all the way to how to pull a scattered old library back into one place. Every one of them is something you can act on.

## 15. I took 800 notes and never use them. What counts as "usable"?

You never use them because most of what you stored depreciates the moment you write it. Tool commands, concept explanations, software tutorials: AI can produce a more complete list of those in three seconds, so eight hundred of them are worth close to nothing. What survives is judgment, knowing when to act, when not to, and what signal means it is time to switch routes. That layer cannot be copied out of you, and it gets more valuable the more times you practice.

So change what you write. Once a week pick one thing and answer a single question: which call did I make this week that AI could not have made. Length does not matter, three hundred words is plenty, but it has to be a real decision, spelling out why you took A and not B at that moment. Fifty of those in a year is your moat.

There is a cheaper habit too. Do not count on scheduled review. Sitting down to reread on a timetable rarely lands, because you are not in the state that made the note relevant, and when you actually are in that state the note never comes to mind. What works is topping up: every time you open an old note for real use, add one new thing to it. Recording facts and information is mostly hoarding. The payoff comes from writing a note and from revisiting it, and nothing in between.

Resource: Obsidian Help https://help.obsidian.md/

## 16. Others link like crazy, but when I link it gets messier. Where is the problem?

It gets messier because there was no relationship there in the first place. The autocomplete popped up and you hit Tab. Trying to thematically tag every note and cross-link every note to every other note is the classic first impulse in Obsidian, and it is the single biggest mistake.

Check that the relationship exists before you link. Source, extension, belongs to the same project, supports the other, contradicts the other: those are worth a link. A link added so the graph looks fuller just guarantees that jumping out of any node lands you somewhere irrelevant. Do not take the graph view too seriously either. Past a few thousand notes it delivers awe more than navigation, and what you use daily is search plus backlinks.

The autocomplete plugin is fine, its default settings are not. Set the match strategy to prefix and the minimum trigger length to two or three characters so it stops firing on every keystroke. It only gets genuinely good past a hundred notes, when you want to link a concept but cannot recall the exact title. Also put aliases to work: list every way you say the same concept in the aliases field, and typing two brackets will surface the synonyms as well. That beats bolting on a pile of links.

Resource: Various Complements https://community.obsidian.md/plugins/various-complements

## 17. What is an MOC, and why is it better suited to the AI era than folders?

An MOC is a Map of Content, a note that does nothing but index. It carries almost no body text, it just lists the other notes on a topic in some structure and becomes the entrance to that topic. Add a Home note listing every MOC and you have a map of maps.

Folders are strictly hierarchical, a note lives in exactly one of them, and once the nesting gets deep it builds walls between ideas. An MOC moves no files, it only exposes relationships, so the same note can hang under three maps at once. Vault size stops mattering: from any topic MOC you can locate what you want, and a new note belongs somewhere as soon as one map references it. In the graph an MOC is a dense node, a natural hub, and AI walking through it beats digging down folder by folder.

To make it actually run you need one rule: every new note links back to at least one MOC. Leave an empty MoC property in your new-note template and fill it as you create. Do not hand-copy the list inside the map either. One Dataview query pulls in every note that links back to the map without linking out itself.

Copy-paste template (use directly):

```
# Python Learning Map
## Basics
- [[Variables and Data Types]]
- [[Functions]]
## Web Frameworks
- [[Getting Started with FastAPI]]
```

Drop this query into the MOC note to auto-collect backlinks:

```dataview
list from [[]] and !outgoing([[]])
sort file.name asc
```

Resource: Dataview https://community.obsidian.md/plugins/dataview

## 18. How do I tag without abusing it? Three counter-examples

Three counter-examples, straight up. First, one concept spelled three ways: advml, AdvML, advanced-machine-learning each stored separately, aggregating to nothing at search time. Second, the tag used exactly once, never picked up by a second note, pure noise. Third, five or six tags per note, tag count explodes, and one topic ends up smeared across a dozen words.

Tags that hold up mark categories. Person, paper, talk, concept, tool, project: things you can classify at a glance. Keep fields of study and specific subjects out of tags, that is the job of notes. Dates do not belong in tags either, filenames handle those. You can also push tags down to the bare minimum, reserving them for a few specific Dataview queries and using nothing elsewhere, which stays remarkably clean.

Sprawl is fixable. Merge the near-duplicates first, normalize the casing and hyphenation to one spelling, delete anything used only once. Few and accurate tags mean you and AI search with the same vocabulary, so pulling up every reading note takes one line and nothing gets missed over a spelling mismatch.

Resource: Dataview https://community.obsidian.md/plugins/dataview

## 19. Should I learn templates (Templater)? Just copy these 3 and you are set

Yes, but stop at the point where you can copy one. You never need the engine internals. Templater beats the core template plugin because it auto-fills the current date, the note title, the weekday, and can even pop up a picker.

Do the config once. After installing, open settings, fill Template folder location in Templater with a folder name such as Templates, and put every template file in there. From then on, create a note, hit Ctrl/Cmd+P, search Templater: Insert template, pick one, and the content drops in with the date replaced by today.

Three templates cover you. A diary template that carries today's date and weekday plus three sections for what happened, what I learned, what to do tomorrow. A reading-note template with frontmatter on top and a fixed body of one-sentence summary, core viewpoint, inspiration and action, golden quotes. A meeting template splitting attendees, topics, discussion and conclusion, action items. Add the rest when you need them. Build a template once a note type keeps recurring, reach for a plugin once a manual action keeps recurring, and do not take on maintenance for a habit that has not formed yet.

Copy-paste template (use directly):

```
# <% tp.date.now("YYYY-MM-DD") %> Diary

> Today is <% tp.date.now("dddd") %>.

## What happened today

## What I learned today

## What to do tomorrow

- [ ]
```

Resource: Templater https://community.obsidian.md/plugins/templater-obsidian

## 20. How long should one note be? Too long and AI cannot read it either?

There is no target length, it depends on whether the note covers one thing or several. In practice most notes stay very short, a few sentences and one figure, and their main job is to be indexed into the vault so other notes can link in. Only the handful that touch your current work deserve length, and those can run several pages.

One idea per note is the safest default. Write a concept card in three moves: explain it in plain language, give one example, list a few related concepts and link out. If you can explain it simply you understood it, and if you cannot, go learn it again. Restate everything in your own words, because a note that copies the original verbatim is worth zero.

Do not swing to the other extreme either. Spinning up a mini note for every obscure corner concept is just as pointless. When in doubt do not agonize, wait until a note is visibly bloated and then split it. Once your vault has structure, merging and splitting are quick, you walk the backlinks and fix a few links. Fine granularity pays off because AI can quote precisely instead of losing the thread inside a five-thousand-word grab bag.

Resource: Obsidian Help https://help.obsidian.md/

## 21. How do I turn links into an AI-usable "knowledge graph" instead of noise?

Type your links, and only then is it a graph. A plain wikilink says two notes are related but not how. Write fields like hasTopic, isA, subset, author, project into frontmatter and the link carries semantics, so AI following it knows what it is walking.

Hierarchy rides on the same mechanism. Chain topic notes with subset into a directed graph and one topic can sit under two parents at once. Folders cannot do that, and hierarchical tags cannot either, they only grow into trees. Papers and talks hang off topics with hasTopic, they show up automatically in the topic note's backlinks, and the navigator lets you drill down level by level.

Link density has to be high enough. Every concept you want to mention gets wrapped in brackets, even if that note does not exist yet. A note with zero backlinks may be brilliantly written and is still functionally invisible. Vault rot is rarely about one badly written note, it is a graph problem, and once orphan notes, dead links, and single-use tags accumulate, retrieval starts failing. One aside: suggesting related notes for linking does not require semantic understanding, keyword matching is enough, not everything needs an embedding model.

Copy-paste template (use directly):

```
---
aliases: [synonym 1, synonym 2]
hasTopic: "[[Topic Note]]"
isA: "[[Parent Concept]]"
project: "[[Related Project]]"
---
```

Topic notes build hierarchy with subset:

```
---
subset: "[[Parent Topic]]"
---
```

Resource: Obsidian Help https://help.obsidian.md/

## 22. Daily stream-of-consciousness logging, how to avoid turning into a junk pile?

Give the daily note a job and let it be a hub. Name the file after the date, make it your starting page every day, and dump the day's output there first: questions you ask yourself, snippets you looked up, half-formed ideas. Whichever one grows up later gets pulled out into its own note.

The move that turns it into a hub is writing dates as links. Process steps, appointments, call logs, whoever you met, wherever you went: bracket any date and it links back to that day's note. The daily note then aggregates everything tied to that day on its own, and the backlink list gives you the thread. Add an alias too. Besides the 2026-05-21 style number, write one phrase capturing the day's theme, and that phrase is how you find it again later.

For anything you genuinely cannot place, keep a separate scratch pad for material with no home and no guarantee you will finish it. Push capture friction to the floor as well: set up a capture plugin so a hotkey opens an input box and typing plus Enter appends to a chosen note in under three seconds. Stream logging is not the flaw. Writing it and never touching it again is.

Resource: QuickAdd https://community.obsidian.md/plugins/quickadd

## 23. How to take reading/article notes so it is not "copy-paste then gather dust"?

Copying a passage verbatim is worth zero, accept that first. An excerpt pasted in has only changed location, and later you will remember neither what it said nor why you kept it.

A note you can reuse needs four blocks at minimum. What this is, summarized in your own words. My call, why it is worth keeping. Next step, what you intend to do with it. Related, which projects or topics it links to. Do not skip the fourth: put a wikilink to the topic page under Related, and afterwards you can click through from here to the topic page and find this note again in that page's backlinks.

For books, fill one fixed structure every time. Frontmatter on top with title, author, rating, date finished, then a body split into one-sentence summary, core viewpoint, inspiration and action, golden quotes. The real function of that structure is forcing out the sentence that is yours, and failing to produce it means you have not understood the material. Same for loose article clippings: append one line on why it is worth reading, because a clipping saved without a reason never gets opened again.

Copy-paste template (use directly):

```
---
tags: reading-note
book:
author:
rating:
date-finished:
---
## One-sentence summary
## Core viewpoint
## Inspiration and action
## Golden quotes
```

Resource: Templater https://community.obsidian.md/plugins/templater-obsidian

## 24. What is frontmatter (YAML header) for, and why does AI especially like it?

Frontmatter is the block of fields wrapped in three dashes at the very top of a note, and its job is to make the note filterable by machines. You open a note and see date, status, source, summary up front. Search, plugins, and any AI you granted access see a uniform set of key-value pairs they can filter on exactly, with no guessing from full text.

Fields should be few and good. Lock in four you will really use: updated for last modified, status for state, summary for one line on what the note solves, source for the original link. Adding tags and created is fine too. Too many fields and nobody maintains them, half your notes end up with empty shells, which is worse than having none.

With that layer in place Dataview has something to query. Give reading notes a consistent title, author, rating, date finished, then write one query anywhere and a table sorted by finish date builds itself and updates as you add books. In the other direction, mismatched field names, types flipping between string and number, some notes having the header and some not, are all signals the vault is starting to rot, and running a linter early beats patching later.

Copy-paste template (use directly):

```
---
updated: 2026-05-21
status: active
summary: what problem this note solves
source: original source or link
tags: reading-note
book:
author:
rating:
date-finished:
---
```

Companion query, drop it in any note:

```dataview
TABLE author, rating, date-finished
FROM #reading-note
SORT date-finished DESC
```

Resource: Dataview https://community.obsidian.md/plugins/dataview

## 25. Using AI to help me write notes, will it make me stop thinking?

It will, so do not hand it the body text. The entire point of taking notes is writing them in your own words and later looking back at how well you actually understood the thing. Outsource that step and the note was pointless.

From a learning standpoint, what pays off is the external action that forces internal processing, and hooking new information onto what you already know is the textbook case. The risk was never how strong the model is, it is using the model as a shortcut around that processing, the same mechanism by which students who let AI write their essays end up writing worse.

Draw one line. Q&A, looking things up, writing code, polishing prose: use it freely. The notes in your vault that represent your understanding: write those yourself. Treat anything AI gives you as a draft, rewrite it in your own words, link one related old note, and only then has it really entered your vault. What it is good at is searching, organizing, and continuing the work across the material once you authorize it. Let it write for you, do not let it think for you.

Resource: Copilot https://community.obsidian.md/plugins/copilot

## 26. How to store meeting/interview records so AI can find them later?

Do not rush to store all of it. Meeting records are highly perishable, most stay relevant for a few weeks, and their biggest value is being shared with others. Obsidian is single-user and passing markdown around is awkward. Transcribe whole sessions into the vault and a few months later they only dilute it.

What deserves to stay is conclusions and action items. Title the note with the date plus the meeting subject, say 2026-05-21 Product Requirements Review, and split the body into attendees, topics, discussion and conclusion, action items. Record decisions and who owes what, not every utterance. Write action items as task lines with a due date, and then one query block in another note can pull every unfinished task across the vault that is due before tomorrow. Keep a task overview note holding a few queries with different conditions and open that one page daily.

If the meeting is tightly bound to a project, just hang the action items inside the project note and skip the separate file. One more guardrail: company matters stay in company tools, and only your own reviews, calls, and takes go into Obsidian, so changing employers does not hand your accumulation over with it.

Copy-paste template (use directly):

```
## Attendees
## Topics
## Discussion and conclusion
## Action items
- [ ] who does what 📅 2026-05-22
- [ ] who does what ⏳ 2026-05-25
```

Put this query in the task overview note:

~~~
```tasks
not done
due before tomorrow
```
~~~

Resource: Tasks https://community.obsidian.md/plugins/obsidian-tasks-plugin

## 27. How do images, screenshots, PDFs enter the vault without becoming disconnected?

Nail the attachment path first. Under Files and links in settings, point the default attachment folder at one directory so every pasted or dragged image and PDF lands in the same place, otherwise they end up scattered across the vault. For finer control, let attachments follow the note: set the new attachment location to ./assets/${noteFileName}, generate attachment filenames from a timestamp, and turn on renaming sync so the attachment folder tracks note renames and references never break.

Drag a PDF into the editor and it is in the vault with a link generated. Double-click it in the file list to read and page through, or embed it in the body with an exclamation mark and double brackets around the filename. Audio and video work the same way: drop in mp3, wav, m4a, mp4, webm and reading mode renders a player. Be sparing with video, big files bloat the vault and slow sync, so keep the small ones and park large ones in cloud storage with only a link in the note. If you paste screenshots a lot, install an image toolkit plugin for fullscreen preview, scroll zoom, arrow-key switching, Esc to close, no configuration needed.

The thing that prevents disconnection is still one sentence. Next to every image and every PDF, write what it says and which note it belongs to, then link back with a wikilink. Dumping it into the attachment folder is not storing it. For bulk material coming out of Word, Notion, or EverNote, run Importer and the original structure and links survive.

Resource: Importer https://community.obsidian.md/plugins/importer · Image Toolkit https://community.obsidian.md/plugins/image-toolkit

## 28. What is a dumb-but-stable method for naming and directories?

Numeric prefixes and a two-level ceiling, that is the whole method. Prefixes lock the ordering, 00 Inbox, 01 Diary, 03 Projects, so the system sorts by number and you never memorize the order or get shuffled by first letters. Cap folders at one or two levels and use MOCs and links to connect anything deeper instead of building a nest.

Do not copy anyone else's top-level directories. Create a small number based on the material you genuinely handle. Writers may need topics and published, project workers may need in-progress and done. Directories grow out of real work rather than being cloned from a knowledge-management system and stuffed afterwards. Anything you cannot place goes to the inbox and gets cleared periodically.

For the folders you live in, put a 00 Index at the top spelling out what is here, where the important material enters, and which notes you open most right now. Add a 00 Rules covering what belongs here, how files are named, whether the sort is by date or importance, and where things go once finished. If the folder is simple, write the rules straight into the Index rather than creating two empty files for form's sake. Use exactly one sort logic per folder, all by date or all by importance, because mixing them makes everything unfindable.

Copy-paste template (use directly):

```
my-vault/
├── 00-Inbox/        # temporary material, to be sorted
├── 01-Diary/        # auto-named by YYYY-MM-DD
├── 02-Weekly/       # YYYY-Www
├── 03-Projects/     # PARA Projects
├── 04-Areas/        # PARA Areas
├── 05-Resources/    # PARA Resources
│   ├── reading-notes/
│   ├── knowledge-cards/
│   └── learning/
├── 06-Archive/      # PARA Archives
├── 99-Attachments/  # images, PDFs, etc.
└── Templates/       # note templates of all kinds
```

Resource: Obsidian Help https://help.obsidian.md/

## 29. What exactly should a diary record to become AI's future "context"?

Three sections plus one judgment. What I did today, what I learned today, what to do tomorrow forms the skeleton, and the fourth item is what makes the diary useful later: the call you made that day and why you made it that way. AI reads facts out of the first three, the fourth is the part it cannot copy.

Let tooling carry the rhythm. Enable the core daily notes plugin and pin a calendar panel to the right sidebar so you can see at a glance which days are written and which are blank, and click a date to jump there or create it. One level up, a periodic notes plugin fills in weekly, monthly, quarterly, and yearly notes. Set the weekly format to YYYY-[W]ww, point it at a template and folder, and clicking a week number on the calendar creates that week's note.

Reserve one review per week. Sunday, fifteen to twenty minutes, four blocks: what I finished this week, my biggest takeaway, where I did badly, the three most important things next week. The last two carry the weight, the first two write themselves, and the hard part is admitting what went wrong and narrowing next week down to three. Keep it up for a month and looking back you will find you did far more than memory suggests. Those honest records accumulate, and when AI reads your vault later it can reassemble you along a timeline.

Copy-paste template (use directly):

```
## What I did today
## What I learned today
## What to do tomorrow
- [ ]
## Today's judgment call
- what I decided / why I decided it that way
```

Weekly review template:

```
## What I finished this week
## Biggest takeaway
## Where I did badly
## Three most important things next week
1.
2.
3.
```

Resource: Periodic Notes https://community.obsidian.md/plugins/periodic-notes · Calendar https://community.obsidian.md/plugins/calendar

## 30. My notes are too scattered, AI answers by piecing things together randomly. What to do?

Set up a single point of entry first. Details can stay where they are, but the vault needs an index note pointing at them so all the connections are visible from one place. Bring bulk material in from Word, Notion, and EverNote with Importer, and for tools like Lark Docs export to Markdown and drag the files in. Dump everything into archive right after the import, which clears the desk instantly without losing a single item of history.

Then resist rebuilding the whole thing. Backfilling properties and tags across every old note is the kind of job you abandon after a few days. Only touch what you have actually used recently: keep what you will keep using and add a one-line summary, merge duplicates into one main note, move expired but archival material to the archive, and leave alone anything you cannot decide on. Once several notes pile up under one topic, build an index to string them together.

Own the tradeoff mentally: eighty percent success is a win. Settle on a structure you can live with long term, route every new note through it, digest the old library a bit at a time, and spend energy where you actually benefit. Give old notes a status field and bump it one level each time you touch one, from raw to usable to mature, which turns cleanup from a grand project into a casual motion. Once entry, fields, and maps are all standing, AI answers by walking a map.

Copy-paste template (use directly):

```
During migration, give every old note a status field:

---
status: seed        # seed -> sapling -> evergreen
source: original source
updated: 2026-05-21
---

Archive strategy:

06-Archive/   # the old library lands here in bulk, history intact
00-Inbox/     # fish items out when needed, move to a real home once processed
```

Resource: Importer https://community.obsidian.md/plugins/importer · Dataview https://community.obsidian.md/plugins/dataview
