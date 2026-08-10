# Chapter 5 · Real-World Scenarios: exam prep, writing, research, workplace, ready to use

Everything before was underlying capability; this chapter goes straight into scenarios. Each scenario gives you a copyable workflow; the only point is: AI gives the draft, you make the trade-offs. Do not hand out the judgment step. And the draft AI can give you sticks to your own thread, on the premise that your notes themselves have accumulated, so it can pick up where you left off.

## 65. Grad school / civil service exam: how to let AI generate mock questions and test points based on my notes?

Worth doing, but do not reverse the order: read through your own notes once first, then let AI write questions. Ask an empty vault for questions and you get the same generic paper that circulates everywhere online, matched to nobody's weak points, least of all yours.

Feed one chapter at a time. Paste that chapter's body text in, require it to write questions using only that text, and require a gap table afterwards: which test points you covered at the definition level, which ones you can restate the derivation for, and which are just a heading you copied. That table is worth more than the questions. It tells you which section to fix tonight. Do not throw away the questions you answered. Fold the ones you got wrong back into the original note, and next round they become the new key points.

Someone preparing for a math exam linked formulas and derivations into a web, then had AI write cross-section questions along those links, which lands much closer to a real paper than grinding chapter by chapter. If you do not want to build a vault from scratch, the community has ready student-oriented example vaults; cloning and adapting one beats starting from blank.

```
# Generate mock questions from my notes (swap [[Chapter X notes]] for your filename)
Read only the body of [[Chapter X notes]]. Do not bring in knowledge from outside it.
Write three tiers:
- 10 multiple choice: only on concepts I marked "key" or "error-prone"
- 5 short answer: only on derivation steps or procedures I wrote down
- 2 essay: must string together the other notes this page links to
Then append a gap table with three columns:
test point | depth I reached (heading / definition / derivation) | what is missing
For any test point absent from my notes, write "not covered in this note".
Do not fill in the answer for me.
```

Resource: Obsidian Garden Gallery https://vaults.obsidian-community.com/ · LifeOS example vault https://github.com/quanru/obsidian-example-lifeos

## 66. Forgetting after memorizing, how to use AI to turn notes into flashcards (Anki-style)?

Pick the destination before you start. If you want to review across devices and see forgetting-curve statistics, go to Anki. If you want to stay inside your vault and refuse to open another app, install the Spaced Repetition plugin and mark cards inside the notes. Running both means maintaining two copies. Pick one.

Someone got stuck wanting to card an entire book and finished exactly zero cards. The correct opening is to cut only your weakest chapter, get the import working, then expand. Let AI read the note body, cut it into one question and one answer per card, review once and delete the strained ones, then batch import. For Anki, the thing that matters is a fixed field order of `Front,Back,Tags`. Get the order right and you stop remapping columns every time.

The cards come from what you actually wrote, so they test your actual weak points. Do not skip the review pass. A badly cut question stays in the deck and you keep memorizing it wrong.

```
# Prompt: turn this note into Q&A cards
Cut the note below into Q&A cards, one knowledge point per card. Output CSV with no
header row. Field order is fixed: Front,Back,Tags
Rules:
1. The front is a question that stands alone, with no "the above" or "the following"
2. The back is under 40 words, the answer only, no restating the question
3. Tags come from my top-level headings, spaces to underscores, multiple tags space-separated
4. If a field contains a comma, wrap that whole field in double quotes
5. Do not invent anything absent from the note; fewer cards is better
Note body:
<paste the note here>
```

```
# Save as cards.csv (UTF-8) and add these three lines at the very top by hand
#separator:comma
#html:true
#tags column:3
# The rows look like this (order: Front,Back,Tags)
What is Obsidian's core file format?,Local Markdown plain text .md,Obsidian_basics
What is the link syntax?,"Wrap it with [[note name]]",Obsidian_basics
# In Anki: File → Import → pick cards.csv
# Field separator "Comma"; field 1 → Front, field 2 → Back, field 3 → Tags
# Set duplicate handling to "Update existing notes" so re-imports do not spawn copies
```

Requires: Anki desktop; to review inside the vault instead, install the Spaced Repetition plugin

Resource: Anki https://apps.ankiweb.net/ · Spaced Repetition https://community.obsidian.md/plugins/obsidian-spaced-repetition

## 67. When writing gets stuck, how to let AI dig topics and material from my vault?

When you are stuck, make AI retrieve, never let it write the prose. The moment it writes a sentence you start sliding along its rhythm, and your own voice is gone from the page.

The concrete move is a three-column table: usable material, which note it came from, which paragraph of yours it attaches to. Dredge in three groups: settings and scenes you can reuse as is, similar passages you recorded six months ago and have since forgotten, and pairs of records that contradict each other. The third group is the valuable one, because a contradiction is already the seed of a conflict.

Someone writing long-form splits each scene into its own file and uses Longform to order and compile them, so getting stuck on one scene means dredging that scene only instead of the whole vault. Screen what comes up yourself. Using a third of it is usually enough to break the block; the rest stays in the pool.

```
# Material dredge when stuck (retrieve only, write nothing)
Search every note in my vault mentioning [character / theme] and output three columns:
usable material | which note it came from | which paragraph of mine it attaches to
Give it to me in three groups:
A settings, scenes, and dialogue I can reuse as is
B similar passages I recorded months ago and have forgotten
C pairs of records that contradict each other (these turn into conflict most easily)
Dredge and sort only. Do not write a single line of prose for me.
```

Requires: Longform plugin (scene-level splitting and compiling for long drafts)

Resource: Longform https://community.obsidian.md/plugins/longform

## 68. An article half-written, let AI continue writing, will it go off track? How to control?

It will, and you should assume it always will. It cannot see the conclusion in your head, so it just slides forward on the feel of your last sentence. There is one control that works: outline first, write second, and let out the rein one paragraph at a time.

Three steps. Step one forbids prose entirely: it lists an outline for the next three paragraphs, one line each, stating the problem each paragraph solves, and it moves only after you revise the outline. Step two writes paragraph one only, under a word cap, reusing the person, tense, and word choices already in your draft, with no new facts or data you never wrote. Step three has it place the new paragraph beside your original and point out where the tone breaks; you nod before it writes the next one.

Use your plugin's selection-rewrite mode so it replaces only the highlighted lines rather than overwriting the whole file. Turn on file recovery while you are at it, so a botched rewrite can be rolled back to the version from half an hour ago.

```
# Let AI continue without derailing (three steps, one paragraph of rein at a time)
Step one (no prose yet):
Read what I have written and list an outline for the next 3 paragraphs, one line each,
stating what problem each paragraph solves.
Step two (after I revise the outline):
Write paragraph 1 only, under 200 words, reusing the person, tense, and word choices
in my existing draft. Do not introduce facts, data, or examples I never wrote.
Step three:
Place that paragraph beside my original and list where the tone or diction breaks.
Wait for my confirmation before writing the next one.
```

Requires: Copilot plugin (use selection rewrite, never whole-file replacement)

Resource: Copilot for Obsidian https://community.obsidian.md/plugins/copilot · Obsidian file recovery https://help.obsidian.md/Plugins/File+recovery

## 69. Self-media daily posting runs out of material, how to let AI generate 30 topics from old notes?

A topic drought is usually a retrieval problem. Your vault holds three months of material already; it is just scattered. Frame the range with search first, then let AI cluster. Reverse that order and you get a pile of headlines you cannot actually write.

Frame with the built-in query syntax: `path:` limits the folder, `tag:` limits the theme, and a leading minus excludes. One query pulls three months of daily notes clean. Paste the results in and require every topic to merge at least two fragments, dropping anything a single fragment cannot carry. That one rule kills eighty percent of the filler.

Someone keeps the habit of picking five or six writable topics from the list and parking the rest in a topic pool to rescan next month. The selection criterion is material depth, not how good the headline sounds.

```
# Step one: frame the range in the Obsidian search bar (paste directly)
path:"daily/" -tag:#archive
```

```
# Step two: paste the results in and use this
Cluster these fragments by theme and output 30 topics, one per line, in this format:
topic title | one-line angle | which of my fragments it uses
Requirements:
1. Every topic merges at least 2 of my fragments; drop anything a single one cannot carry
2. Mark the 5 where my material is deepest and I could write tomorrow
3. No generic inspirational topics, nothing my vault has no material for
```

Requires: Obsidian built-in search (no plugin needed)

Resource: Obsidian search syntax https://help.obsidian.md/plugins/search

## 70. Reading papers / reports, how to let AI summarize and auto-link to my existing notes?

The summary itself is cheap. The valuable step is hanging the paper into your existing network. If a summary produces zero links, that paper is an island the moment you close it, and in three months you will not remember reading it.

Fix a literature-note template and make "relation to my existing notes" a required section with three buckets: supports, conflicts, fills a gap. Require at least three relations per paper, each labeled with its bucket and one line of reasoning. The step that matters is pasting in your list of note titles and telling it that links may only come from that list, and that anything without a match gets "no matching note yet". Now it cannot invent filenames that do not exist.

Generate the note from your reference manager so year, authors, and item link fill themselves in, leaving you only the judgment section to write.

```
---
type: literature
title:
authors:
year:
zotero:
read-on:
---
## One-sentence conclusion
## Problem / method / conclusion / limitation
## Relation to my existing notes
- Supports: [[ ]] because:
- Conflicts: [[ ]] because:
- Fills a gap: [[ ]] because:
## My own judgment
```

```
# Prompt: hang it into the network as soon as it is read
Read this paper and fill in the template above. Section three needs at least 3 relations,
each labeled supports / conflicts / fills a gap, each with one line of reasoning.
Here is my list of note titles. Links may only be chosen from this list:
<paste your list of note titles>
If nothing on the list matches, write "no matching note yet". Do not invent titles.
```

Requires: Zotero Integration plugin (generates notes with metadata straight from your reference library)

Resource: Zotero Integration https://community.obsidian.md/plugins/obsidian-zotero-desktop-connector

## 71. Researcher: how to use local AI to read literature closely without leakage?

Confidential or unpublished literature goes to a local model only. There is no middle option here. If the hardware cannot keep up, drop to a smaller model, not to the cloud. Slow still finishes; one leak never comes back.

Someone assumed that typing a localhost address into settings settled the matter, without ever checking whether traffic left the machine. After pulling the model and pointing the plugin at the local endpoint, run an offline test: turn off Wi-Fi and ask again. A normal answer proves the whole path is local. Keep the original confidential files on an encrypted volume, unmount it when done, and let the vault hold only de-identified notes.

A 7B-class model is enough for summarizing, extracting claims, and spotting contradictions. Move up only when you need reasoning across a long document, and expect the wait to grow noticeably.

```
# 1. Pull the model (terminal)
ollama pull qwen2.5:7b
ollama serve

# 2. Obsidian → Copilot settings → Model → Add Custom Model
#    Provider:   openai-format
#    Base URL:   http://localhost:11434/v1
#    Model Name: qwen2.5:7b
#    API Key:    any non-empty string (the local service does not check it)

# 3. Offline check: turn off Wi-Fi and ask again. An answer means fully local.

# 4. Keep original confidential files on an encrypted volume, unmount after use.
#    The vault holds de-identified notes only.
```

Requires: Ollama + Copilot plugin

Resource: Ollama https://ollama.com/ · Copilot for Obsidian https://community.obsidian.md/plugins/copilot

## 72. Workplace: how to let AI sink meeting records into retrievable action items?

However elegant the minutes look, if the action items cannot be queried the file is just archive. The rule is simple: action items must use one task format with an owner and a due date, so a query can pull them out. Everything else in the note is background.

During the meeting you just capture real points by hand. Do not record audio and expect AI to handle the rest. Afterwards paste your rough notes in and have it fill the four-section structure, where every action item carries three things: what, who, by when. Anything missing from your notes becomes "to confirm", never a guess. Then put a task query block on the project page so unfinished items from every meeting collect in one place, and a glance before the weekly sync tells you who owes what.

What actually saves time is format consistency, not which model you use. Freeze the date format and the tag naming first, or the query will keep missing rows.

```
## Attendees
## Topics
## Discussion and conclusion
## Action items
- [ ] Draft the proposal (@Zhang) #project/site-redesign 📅 2026-08-20
- [ ] Confirm the budget basis (@Li) #project/site-redesign 📅 2026-08-15
```

````
# Put this on the project page to collect every unfinished item across meetings
```tasks
not done
tag includes #project/site-redesign
sort by due
```
````

```
# Prompt: turn rough notes into minutes
Turn my rough meeting notes below into the four-section structure above.
Every action item needs three things: what, who, by when. Whichever is absent from my
notes becomes "to confirm". Do not guess.
Do not add conclusions that never appeared in my notes, and do not polish anything into
a quote that was never spoken.
Rough notes:
<paste the points you captured during the meeting>
```

Requires: Tasks plugin

Resource: Tasks https://community.obsidian.md/plugins/obsidian-tasks-plugin

## 73. Too much client / project material, how does AI surface the right one when I need it?

Past a certain client count, hunting through folders always loses. Switch to semantic surfacing: while you write a proposal for client A, the sidebar lists the A preferences you recorded, the pitfall from last time, and the playbook from a similar project.

Someone installed the plugin, found the surfacing inaccurate, and the cause was almost entirely in the notes. Vector retrieval eats text, and a client note containing one line saying "follow up next week" gives it nothing to work with. The fix is two or three plain sentences of summary at the top of each client note covering industry, need, and current stage; surfacing quality changes immediately. Manually linking one similar project for a new client gives it a starting point.

Do not skip the "their exact words" section in the template. Original phrasing is the best retrieval anchor, and paraphrasing strips out the very keywords that would have matched.

```
---
client: South China - Company A
stage: proposal
last_contact: 2026-08-05
---
> Summary: manufacturing, wants offline dealer data piped into their current system,
> stalled on budget approval.

## What they care about (copy their exact words, do not paraphrase)
## Pitfalls from the last conversation
## Pricing and walk-away point
## Similar projects
- [[ ]]
```

```
# Three moves that make surfacing accurate
1. Install Smart Connections and let the first run finish embedding the whole vault
2. Add 2-3 plain sentences of summary atop each client note; retrieval eats these
3. Manually link 1 [[similar project]] for each new client, and surfacing extends from there
```

Requires: Smart Connections plugin

Resource: Smart Connections https://github.com/brianpetro/obsidian-smart-connections

## 74. Writing proposals / reports, how to let AI draft based on my historical material without making up?

There is one move against fabrication: force a source on every paragraph and delete any paragraph without one. Prompting it to "not make things up" achieves nothing. You have to make fabrication visible on the page.

Concretely, hand it a closed list of material, state that only that list may be used, and require an inline field at the end of each paragraph, such as `[source:: [[March client meeting notes]]]`. Where material is missing it may not patch the hole with general knowledge; the whole paragraph becomes "[MISSING] need to add: ...". You scan the draft, delete every paragraph without a source marker, and what remains is the part you can defend.

Leave "why this direction" empty and write it yourself. That section is the only place in the proposal that genuinely carries your name. Structure, enumeration, and phrasing can all start as its work.

```
# Prompt: draft from historical material (no source means fabricated)
Here is the material list. You may use nothing outside it:
<paste project notes / meeting minutes / client preferences>
Draft the first version of [proposal name]. End every paragraph with
[source:: [[note name]]] marking its basis.
For any paragraph without supporting material, write the whole paragraph as
"[MISSING] need to add: ...". Do not fill gaps with general knowledge.
Leave the "why this direction" section empty. I write that one.
```

```
<%* /* Templater: generate the skeleton when creating a proposal */ %>
---
type: proposal
created: <% tp.date.now("YYYY-MM-DD") %>
sources: []
---
## Background (cite historical material)
## Current state and problems (every paragraph carries [source:: ])
## Proposal (every paragraph carries [source:: ])
## Why this direction (I write this, AI stays out)
## Risks and cost
```

Requires: Templater plugin

Resource: Templater https://community.obsidian.md/plugins/templater-obsidian

## 75. Legal / medical and other sensitive industries, how to use AI without stepping on compliance red lines?

Three hard lines: local model, encryption at rest, least privilege. Break any one of them and this material should not touch AI at all. The arithmetic in these fields differs from everywhere else. Ten minutes saved is worth nothing; one leak is an incident.

Enforcement comes from partitioning, since willpower does not hold. Split the vault into three zones. Red holds original confidential material on an encrypted volume, and you add that folder to your AI plugin's exclusion list. Amber holds de-identified working notes and goes to the local model only. Green holds statutes, published case law, and public industry material, and may go to the cloud. De-identify with a fixed substitution table so the same person carries the same code name across every note; otherwise cross-referencing reconstructs the identity anyway.

Run the four questions before any upload. A "no" on any of them stops you. Tedious, and far cheaper than explaining yourself afterwards.

```
# Zone layout (red never touches AI)
vault/
├─ red/     original confidential material, on an encrypted volume,
│           added to the AI plugin's exclusion list
├─ amber/   de-identified working notes, local model only
└─ green/   statutes, published case law, public industry material, cloud allowed

# Substitution table (one per matter, kept in red/, never enters an AI context)
real name        → code
XX Hospital      → Institution A
Jane Doe         → Party A
visit 2026-03-14 → day T0
```

```
# Four questions before uploading (any "no" stops you)
1. Does this text still contain names, record numbers, contract numbers, exact amounts?
2. Is this model running locally (does it still answer with the network off)?
3. Was this key issued to a dedicated sub-account, and rotated in the last 90 days?
4. If challenged, can I produce a record of what content this call used?
```

Requires: Cryptomator (encrypted volume) + Ollama (local model)

Resource: Cryptomator https://cryptomator.org/ · Ollama https://ollama.com/

## 76. Doing review: how to let AI synthesize "what I grew this year" from a year of notes?

Remembering the review in December is already too late. The quality of an annual review is set by how dense your weekly notes were all year. Without them, AI can only boil scattered diary entries into handsome nothing.

Get weekly notes running with the periodic notes plugin, on a fixed four-section template: what I finished, biggest gain, what went badly, top three for next week. Force the gain section to state why it counts as a gain, or a year later you will not decode what you meant. In December paste all 52 weekly notes in at once and require four things per quarter, each citing a specific date: what you actually finished (only with an artifact), the same problem you kept stalling on (listed only if it appears three or more times), how your focus migrated, and what you said you would do and never touched.

Someone dreads the fourth item most, which is exactly why it is the useful one. Explicitly forbid conclusions like "you grew". Facts and dates only; the conclusion is yours.

```
## What I finished this week
## Biggest gain this week (state why it counts as a gain)
## What went badly
## Top 3 things for next week
## Keywords: #area/ #project/
```

```
# Annual synthesis prompt (paste all 52 weekly notes at once)
Distill four things per quarter, each citing a specific weekly-note date:
1. What I actually finished (only counts with an artifact)
2. The same problem I kept stalling on (list only if it appears 3+ times)
3. How my focus migrated (what I wrote in Q1 versus Q4)
4. What I said I would do and never touched all year
Do not write conclusions like "you grew". Facts and dates only. I draw the conclusion.
```

Requires: Periodic Notes plugin

Resource: Periodic Notes https://community.obsidian.md/plugins/periodic-notes

## 77. Reading blogger: how to use AI to turn book excerpts into citable knowledge cards?

A whole-book reading note cannot be cited; one concept per card can. Do not skip the card-splitting step, because it decides whether the book is still retrievable to you six months from now.

The flow has two stages. After finishing, write one whole-book note on a fixed template, with frontmatter for title, author, rating, and finish date, and four sections: one-sentence summary, core viewpoints, takeaways and actions, quotes. Then have AI split that note into cards, one concept each, in a uniform format: concept name, one-line definition, plain-language explanation, one example from your own field, source down to the chapter. Any passage that yields no standalone concept gets dropped; fewer cards is better.

Once the cards accumulate, one query block lists every reading note as a shelf sorted by finish date, and when you write long pieces you flip through cards by tag and use them as bricks. To see the finished shape, a community example vault demonstrates the one-card-one-concept plus query-summary layout.

```
---
tags: reading-note
book:
author:
rating:
date-finished:
---
## One-sentence summary
## Core viewpoints
## Takeaways and actions
## Quotes
```

```
# Prompt: split a whole-book note into citable cards
Split the reading note above into cards, one concept per card, each in this format:
# Concept name (a noun phrase, not the book title)
One-line definition:
Plain-language explanation (under 80 words):
One example from my own field:
Source: <book>, chapter X
Drop any passage that yields no standalone concept. Fewer cards is better.
Do not treat table-of-contents entries as concepts.
```

````
# Auto-built shelf, placed in your "My bookshelf" note
```dataview
TABLE author, rating, date-finished
FROM #reading-note
SORT date-finished DESC
```
````

Requires: Dataview plugin

Resource: Blue Topaz example vault https://github.com/PKM-er/Blue-topaz-example · Dataview https://community.obsidian.md/plugins/dataview

## 78. Learning a foreign language: how to let AI do contextual practice based on my notes?

A generic question bank never reaches your weak points. Build the error log first, then talk about practice. Reverse that and you are just keeping a textbook company.

Fill the error log with the table below and drop none of the fields. The "what I wrote" column is the most useful one in the whole table, because it preserves the original shape of your mistake, and that is what lets AI write correction drills that actually land. Keep one file per week in one folder.

Cross-week review needs one caveat: query plugins cannot read cells inside a Markdown table, so write each entry a second time as a task line with inline fields, then let one query block pull everything unmastered into a single screen sorted by error count. That screen is your weekly review. For practice, paste the whole error log in and require questions built only from its entries, in three forms: a situational dialogue, correction drills, and a short essay prompt. Afterwards have it give feedback only on error causes already in the log, without quietly rewriting your other phrasing, which would scatter the feedback.

```
---
type: error-log
language: English
week: 2026-W33
updated: 2026-08-10
---

| Item | What I wrote | Correct form | Cause | Where | First error | Count | Mastered |
|---|---|---|---|---|---|---|---|
| effect / affect | affect the effect | the effect of the change | part of speech | work email | 2026-07-02 | 3 | no |
| bring / take | bring it there | take it there | direction reversed | speaking | 2026-07-18 | 2 | no |
| in / on time | I arrived on time barely | I barely arrived in time | fixed collocation | speaking | 2026-08-05 | 1 | no |
```

````
# Write each entry again as a task line so the query can reach it (below the table)
- [ ] effect / affect | cause:: part of speech | where:: work email | count:: 3
- [ ] bring / take | cause:: direction reversed | where:: speaking | count:: 2

# Put this in your "This week's review" note. Tick the box and the row disappears.
```dataview
TASK
FROM "language/errors"
WHERE !completed
SORT count DESC
```
````

```
# Prompt: build contextual practice from my error log
Here is my error log. Build questions only from its entries, with no outside vocabulary:
<paste the error log>
Give me three things:
1. An 8-turn dialogue set at [ordering food / emailing about leave / a status update],
   using at least one of my error items per turn
2. 5 correction drills that deliberately use the wrong forms from my "what I wrote" column
3. One 80-word writing prompt that must use the items whose cause is "part of speech"
After I write, give feedback only on causes already in the log.
Do not quietly rewrite my other phrasing.
```

Requires: Dataview plugin (cross-week aggregation); add the Spaced Repetition plugin for card-based review

Resource: Dataview https://community.obsidian.md/plugins/dataview · Spaced Repetition https://community.obsidian.md/plugins/obsidian-spaced-repetition

## 79. Startup / side hustle: how to use vault+AI to manage ideas, not lose inspiration?

Lost ideas are caused by friction at the entrance. There is one standard: if getting a thought from your head into the vault takes more than three seconds, you will skip it. So compress capture into a single keystroke and push sorting, linking, and judging entirely to later.

Build a "spark" capture action in your capture plugin, landing in `inbox/spark.md`, set to prepend, with source and timestamp in the format, then bind a global shortcut. Fill it in exactly as below and it works. While capturing, no self-censorship. Save the ones you think are stupid too; judgment happens on the weekend.

Spend ten minutes each Sunday clearing the box: paste the week's entries in, have it cluster into at most five groups, label each group with one action (test now, park and watch, drop for good) plus one line of reasoning, and separately flag any idea you recorded three or more times. The one that keeps reappearing is usually the one to actually do. Do not let it judge which idea makes money; it sorts and de-duplicates, nothing more.

```
# QuickAdd → Choices → new Capture, fill in these fields
Name:            Spark
Capture To:      inbox/spark.md
Prepend:         on (newest idea goes to the top)
Capture format:  on, template is this one line
- [ ] {{VALUE}} | source:: {{VALUE:source}} | logged:: {{DATE:YYYY-MM-DD HH:mm}}
Back in QuickAdd settings, click the ⚡ on "Spark" to add it to the command palette,
then go to Settings → Hotkeys, find "Spark", and bind Cmd/Ctrl + Shift + I
```

```
# Sunday 10-minute inbox clearing prompt
Here are all entries from my inbox/spark.md this week:
<paste entries>
1. Cluster into at most 5 groups and name each group in words I will understand
2. Label each group: test now / park and watch / drop for good, plus one line of reasoning
3. For each "test now" group, write one smallest test I can finish within a week
4. Separately list any idea I recorded 3 or more times
Do not judge which one makes money. Sort and de-duplicate only.
```

Requires: QuickAdd plugin

Resource: QuickAdd https://community.obsidian.md/plugins/quickadd

## 80. Content repeats itself? How to let AI hint "you wrote a similar view three years ago"?

Checking for repetition before you write beats having a reader point it out after you publish. Two minutes here saves a whole wasted draft.

Three moves. When you create the note, first write the core claim of this piece as one sentence, a claim rather than a headline, so semantic retrieval has something to bite. Open the plugin sidebar and look at the top five it surfaces. Ask one question of each: what does this piece have that the old one did not. If you cannot answer, do not write it.

Once they surface, do more than eyeball for overlap. Have AI produce a comparison table with a verdict limited to three options: repeat, upgrade, or reversal. An upgrade must state what is new; a reversal must state where your position moved. Each gets one self-citing line you can drop straight into the opening. Admitting you changed your mind persuades better than pretending the thought is brand new, and readers get to watch your thinking move.

```
# 2-minute repetition check before writing
1. Create the note and write this piece's core claim as one sentence (a claim, not a headline)
2. Open the Smart Connections sidebar and read the top 5 it surfaces
3. Ask of each: what does this piece have that it did not? No answer means do not write it
```

```
# Prompt: compare this piece against what I already wrote
Here is my claim this time: <one sentence>
Here are the 5 old notes the sidebar surfaced: <paste their text>
Output a table: old note | what I said then | what I say now | the difference | verdict
Verdict is one of three: repeat (drop the draft) | upgrade (state what is new) |
reversal (state where my position moved)
For upgrade or reversal, give one self-citing line I can put straight in the opening,
such as "Three years ago I argued X; I have changed my mind, because Y".
```

Requires: Smart Connections plugin

Resource: Smart Connections https://github.com/brianpetro/obsidian-smart-connections

## 81. Cross-department collaboration material scattered, can personal vault+AI fill in? Where is the boundary?

It fills the half you handled yourself and cannot fill the half sitting with other people. Try to make a personal vault replace the team's collaboration system and the first permissions dispute will send you back.

Draw the boundary at intake, and draw it in advance. Three lines. Meeting notes you wrote, process records from projects you handled, and reading notes on public material go in freely. Anything containing other people's personal information, client names, or unpublished financial figures gets redacted first. Original files held by others, system exports that require authorization, and other people's chat logs never go in at all. Hold those three and your vault contains only your own accumulation, so letting AI read it carries no compliance risk.

When a colleague needs information, give the conclusion and the source rather than forwarding the original file. For anything that genuinely needs joint maintenance, use the team tool or the official shared-vault feature, so permissions and audit trails stay somewhere that keeps records.

```
# Three intake boundaries for a personal vault
Goes in:      meeting notes I wrote, process records from projects I handled,
              reading notes on public material
Redact first: content with others' personal information, client names,
              unpublished financial figures
Never:        original files held by others, system exports requiring authorization,
              other people's chat logs

# Reply to use when a colleague asks (give conclusion and source, forward nothing)
"My record on this is X, from the meeting on <date>.
 The original file lives in <team system>; pull your own copy with your access.
 I do not forward it."
```

Resource: Obsidian shared vaults https://help.obsidian.md/sync/collaborate

## 82. A real workflow demo: from collecting to producing, where does AI work for me?

Across the whole flow AI should do four manual jobs only: sorting, marking sources, surfacing, and drafting. Judgment, direction, and the final pass stay with you. Settle that division and the rest is just building the folders.

Three layers. `raw/` holds pages clipped from the browser with their source links, unprocessed, not one word touched. `wiki/` holds processed concept pages, each noting its source at the top, with an `index.md` inside as the master index. `drafts/` holds finished pieces. Your daily job is one thing: clip anything useful into `raw/` with one click, with no attempt to digest it on the spot.

Run a compile once a week: AI reads what is new in `raw/`, generates a source-summary page per item, extracts concepts into existing or new concept pages, and updates the master index. When you want to write, it reads the index first, then drafts, marking each claim with the concept page behind it and writing "[TO ADD]" wherever there is none, leaving the conclusion empty. Your four jobs are dropping real thoughts in, reviewing the sorting, setting the conclusion, and revising the final. Everything else is handed over.

```
vault/
├─ raw/       pages clipped from the browser, source_url kept, unprocessed
├─ wiki/      processed concept pages, source noted at the top of each
│  └─ index.md   master index, AI reads this first every time
└─ drafts/    finished pieces
```

```
# Weekly: compile raw/ into wiki/
Read the files added to raw/ after <date>:
1. Generate one source-summary page per item, keeping source_url and clip date
2. Extract concepts, extend existing concept pages or create new ones in wiki/concepts/
3. Update wiki/index.md and mark which pages were added this week
Do not put claims into wiki/ that the source does not contain.
Leave a TODO wherever my judgment is needed.

# When it is time to write: draft
Read wiki/index.md first, then draft [topic] from wiki/.
Mark each claim with [source:: [[concept page]]]; write "[TO ADD]" where there is none.
Leave the conclusion section empty. I write that one.
```

Requires: Obsidian Web Clipper (browser extension, feeds raw/)

Resource: Obsidian Web Clipper https://obsidian.md/clipper
