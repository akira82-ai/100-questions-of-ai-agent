# Chapter 4 · AI Turns Your Notes Into Assets: From Storing to Using

Hundreds of notes piling up are still just dust if they are never used. The real value starts only after you connect AI: the more your accumulated notes can be answered from by AI, the more they become assets instead of a dump of digital garbage. This chapter is about making AI turn your accumulation into something usable, from an identity file that lets AI understand you, to a knowledge-base structure that keeps raw and wiki apart, and on to the daily loop of compile, query, and health-check.

## 47. How do I make AI truly "get me" without re-introducing myself every time?

Put a me.md at the root of your vault that states who you are, what you are doing, what you care about, and what not to do to you, and have AI read it at the start of every session. Think of it as your portable identity for AI. Any AI that reads it can use it, so you never repeat your self-introduction.

The practice breaks into three blocks: identity (one line on your role, field, current state), projects (main line, side line, and where you are stuck), and how to use your vault (directory rules, fewer but real links, answers must cite sources). Claude.md can even be just one line, "go immediately to me.md", and AI acting on that line finds your identity file. Retrieval, answers, and note surfacing all rest on AI understanding you first; without it, AI can only guess from the literal text.

Copy-paste template:

```
# me.md minimal skeleton (put at vault root, AI reads it first every session)
---
type: profile
updated: 2026-08-10
---

## Who I am
One line: role / field / current identity

## What I am doing
- Main line: [[ProjectA]] (what is the goal, where am I stuck)
- Side line: [[ProjectB]]
- Questions I care about long term:

## How my vault is organized
- inbox/ raw · notes/ processed · wiki/ concept pages
- Naming rule: YYYY-MM-DD-topic
- Only link things genuinely related, fewer is better

## What I want AI to do
- Answer from this vault, cite the source note for every claim
- Say so when the vault has nothing, do not make it up
- Leave conclusions and wording to me, you only gather, retrieve, draft
```

Resource: Smart Connections https://github.com/brianpetro/obsidian-smart-connections · YouTube "me.md" https://www.youtube.com/watch?v=rRa9td4oe7k

## 48. What is Vault QA, and how do I let AI answer from my accumulation instead of from scratch?

Vault QA means treating your notes as a knowledge base: before answering, AI reads the vault first, and the answer comes from your own accumulation. It only works if the notes are retrievable. The more tightly they are linked and the more they are processed, the more accurate the answer.

Two layers are enough: raw/ holds raw material, wiki/ holds processed concept pages, and wiki/ keeps a master index index.md. Before asking, have AI read index.md to grasp the whole picture, then require it to point to the specific source page after answering, and to say so honestly when the vault has nothing. That way when you ask "what was my conclusion about X last year", it opens your own notes, not generic web talk. Retrieval tends to pull only surface-relevant hits, so for judgments spanning several years, break the question down; do not expect one shot to cover it.

Copy-paste template:

```
First read wiki/index.md to understand the whole picture, then answer my question based on wiki/ content: [your question]
When answering, cite the specific source pages in wiki/; tell me when the knowledge base has no relevant information.

# Two-layer vault structure (build it like this)
raw/    raw material, keep source_url, do not process
wiki/   processed concept pages, note the source at the top of each page
wiki/index.md   master index, AI reads it first every time
```

Resource: Copilot for Obsidian https://community.obsidian.md/plugins/copilot

## 49. How do I write a "user manual" for my vault so AI behaves?

Put a CLAUDE.md at the vault root (write AGENTS.md if you use Codex) that lays out the directory structure, page format, naming rules, and the steps for the three operations: ingest, query, and lint. This file is the most important thing in the whole repo. Without it, AI compiles in a different format every time, pages that should merge do not merge, and a month later you get a pile of AI-flavored fragments.

The minimal content is three blocks: structure (raw/ is original material, add only, never edit; wiki/ is AI's turf), page rules (every page carries frontmatter, internal references use [[wikilink]], every claim traces back to a raw/ source), and iron laws (NEVER delete any file, NEVER edit raw/). There is also a heuristic for new page vs. edit: if other pages will link to it, create new; if it is just supplementary info to an existing page, update in place. Feed the first few items one by one, write the corrections back into CLAUDE.md, and only scale up after training your admin.

Copy-paste template:

```
# CLAUDE.md (put at vault root, AI reads it first)
## Structure
- raw/: original material, never modify any file here
- wiki/: Markdown pages you generate and maintain
- wiki/index.md: master index, update after every operation
- wiki/log.md: append-only operation log

## Page rules
Every wiki page must carry frontmatter:
  title: page title
  sources: [source file path under raw/]
  related: ["[[related page]]"]
- Internal references always use [[wikilink]]
- Every claim must trace back to a raw/ source; write no claim without a source

## Ingest flow
1. Read the specified new file in raw/
2. Write a summary page, update or create related concept pages
3. Update index.md, append to log.md

## Query flow
1. First read index.md to locate relevant pages, read 2-3 pages, then answer
2. Cite [[pages]] in the answer, give the raw/ path when tracing to source

## Lint flow
Check: contradictions between pages / old conclusions overturned by new material /
orphan pages with no inbound links / concepts mentioned but with no page.
Output a report, make no deletion without my consent.

## Iron laws
- NEVER delete any file
- NEVER edit raw/
- New page vs. edit: create new if other pages will link to it;
  update in place if it is just supplementary info
```

Resource: Obsidian Properties docs https://help.obsidian.md/properties

## 50. Is my second brain just a journal? How do I tell it really "thinks"?

A big vault is not the same as a thinking one. A journal only records without processing: one line today, one line tomorrow, nothing connects, and looking back it is just a stream. Real thinking means you made a judgment when you wrote: these two are related, that note overturned my earlier conclusion, and you go back and revise on a schedule.

Three self-checks are the most direct: do the notes connect, have you gone back and processed them, and can the old ones be used when you write something new. Treating collection as effort and a big vault as growth tends to stockpile things you never read. If all three are empty, it is just a journal. Whether your vault thinks decides whether what AI later answers from it has any root. Hoarding without review is only搬运, never real thinking.

Copy-paste template:

```
# Does your second brain "think" or is it a journal? Three self-checks
- Do the notes connect? (MOC / bidirectional links)
- Have you gone back and processed them? (periodic review, updated conclusions)
- Can the old ones be used when you write something new? (AI answers from your accumulation)
All three empty -> just a mover, add processing to truly think

# Quantify the first check: pull out the island notes
# Install and enable the Dataview plugin first, then put these three lines in a dataview code block
LIST
WHERE length(file.outlinks) = 0 AND length(file.inlinks) = 0
SORT file.mtime DESC
```

Resource: Dataview https://community.obsidian.md/plugins/dataview

## 51. What does the three-layer AI knowledge base look like, and why split raw and wiki?

A working AI knowledge base has three layers: raw/ holds original material, wiki/ holds the knowledge entries AI compiles, and the vault root holds a CLAUDE.md with maintenance rules. raw/ is like a warehouse, keeping original evidence without processing. wiki/ is like a bookshelf, where AI turns material into pages you can reread, link, and update, with a master index index.md and a maintenance log log.md. CLAUDE.md is like a manual telling AI that raw/ is immutable, every judgment points to a source, and index and log are updated after each cleanup.

Obsidian is not the AI itself here, only the knowledge-base IDE: you use it to view raw, browse wiki, and inspect link relations. The split keeps AI-generated wiki content from polluting your original material, and any claim can be traced back to the original file in raw/. Feed the first 10 items one by one, correct the format and write it back into CLAUDE.md while compiling, and only scale up after training your admin.

Copy-paste template:

```
AI knowledge base/
├── raw/                 # original material, add only, do not edit
│   ├── articles/        # external articles, blogs, tutorials
│   ├── papers/          # papers, research reports
│   └── clips/           # web clippings, excerpts
├── wiki/                # knowledge entries AI compiled
│   ├── index.md         # master index, quickly know what is in the vault
│   ├── log.md           # maintenance log, records each addition and compile
│   ├── concepts/        # concept pages, one file per important concept
│   ├── entities/        # entity pages: people, orgs, products, projects
│   ├── syntheses/       # synthesis pages, cross-source topic write-ups
│   └── sources/         # source summary pages, one per raw item
├── outputs/             # Q&A, reports, health checks
│   ├── qa/              # answers to complex questions
│   └── health/          # health-check reports
└── CLAUDE.md            # maintenance rules written for AI
```

Resource: Various Complements https://community.obsidian.md/plugins/various-complements

## 52. How do I let AI build the whole vault scaffold at once, so I do less?

Give AI a vault-building prompt that directly creates the directory structure, the master index, the maintenance log, and CLAUDE.md, and you get a usable empty scaffold in hand. This step is called init; after it, you start feeding material in.

The prompt must state four things clearly: which directories to create (raw subtypes, wiki's concepts/entities/syntheses/sources, outputs' qa/health), create wiki/index.md and wiki/log.md, create CLAUDE.md with maintenance rules (raw/ is stored only, never deleted or overwritten, every judgment cites a source, unsure info is marked for verification), and write a source-summary template under sources/ (with title/source/source_url/summary/key_points/related_concepts). Have AI tell you in one paragraph how to use the vault once built. Do not chase perfection on the first pass; get it running, then fix in later rounds.

Copy-paste template:

```
Goal:
I want to build a Markdown knowledge base ordinary people can use, following the LLM Wiki idea. No enterprise RAG, no complex database; first get the minimal loop running with folders and Markdown.

Please do the following:
1. Create this directory structure:
   - raw/articles/
   - raw/papers/
   - raw/clips/
   - wiki/concepts/
   - wiki/entities/
   - wiki/syntheses/
   - wiki/sources/
   - outputs/qa/
   - outputs/health/
2. Create wiki/index.md describing the current themes, material, and entry points of this knowledge base.
3. Create wiki/log.md recording each addition, compile, page update, and health check.
4. Create the project rule file: build CLAUDE.md if using Claude Code, or build both AGENTS.md and CLAUDE.md (same content) if unsure.
   - raw/ only stores original material, do not delete, do not overwrite.
   - Every important judgment should point to a source.
   - Mark uncertain info as needs-verification, do not make it up.
   - After each cleanup, tell me which files you changed.
5. In wiki/sources/README.md write a source-summary template: title / source / source_url / created / summary / key_points / related_concepts.
6. In outputs/health/README.md write a health-check note: pages missing sources, conflicting concepts, pages with no links, possibly stale judgments.

Create these directories and files directly. When done, tell me in one paragraph how to use this knowledge base now.
```

Resource: Copilot for Obsidian https://community.obsidian.md/plugins/copilot

## 53. When new material comes in, how do I let AI auto-compile it into the knowledge base?

Each time you drop a new item into raw/, give AI a compile prompt that generates a source-summary page, updates concept pages, and refreshes the index and log, and you get a skeleton with sources in hand. This action is called compile, and it is the key to the wiki's compounding value.

The prompt should make it do five things: generate a source-summary page for each item and keep source_url; extract key concepts, updating an existing concept page or creating a new one; update wiki/index.md so you quickly know what is in the vault; update wiki/log.md recording what this round processed; and never delete the original material in raw/. Do not chase perfection on the first compile; AI may miss key points and group things wrong, just get it running. After compiling, spend ten minutes in Obsidian: did the summary keep the original link, does the concept page logic hold, is index complete. Note the problems and let AI fix them next round.

Copy-paste template:

```
Read the new material in raw/ and compile it into wiki/.

Do these things:
1. Generate a source-summary page for each item, keep source_url.
2. Extract key concepts; if wiki/concepts/ already has a related page, update it; otherwise create new.
3. Update wiki/index.md so I quickly know what is in the vault now.
4. Update wiki/log.md recording which material this round processed.
5. Do not delete the original material in raw/.
```

Resource: Copilot for Obsidian https://community.obsidian.md/plugins/copilot

## 54. How do I let AI answer from wiki and cite a source for every claim?

Before asking, have it read wiki/index.md to grasp the whole picture, then answer based on wiki/ content, and require it to cite the specific source page, saying so when the vault has nothing. That way the answer comes from your own accumulation, not generic web talk.

The prompt has two core lines: first read index.md to understand the picture, then answer your question based on wiki/ content, citing the specific source pages in wiki/, and tell you when there is no relevant info. For complex questions, have it save the answer to outputs/qa/. Answers alone are not enough; run health checks on a schedule: read index.md, find pages missing sources, conflicting concepts, island pages with no links, and concepts mentioned often but without their own page, then save the report to outputs/health/ with the top 5 fixes. Checks can also be written as a standing Dataview query; the community has ready-made example vaults you can copy directly.

Copy-paste template:

```
# Ask (ask the vault first, do not search the web from scratch)
First read wiki/index.md to understand the current knowledge base, then answer my question based on wiki/ content: [your question]
When answering, cite the specific source pages in wiki/. If the knowledge base has no relevant info, tell me.

# Health check (run weekly)
First read wiki/index.md to understand the current knowledge base, then run a health check.
Focus on:
1. Which pages lack sources.
2. Which concept definitions conflict.
3. Which pages have almost no links, like islands.
4. Which important concepts are mentioned often but have no page yet.
5. Which pages may be stale and need re-verification.
Save the report to outputs/health/ and give the top 5 fixes to prioritize.
```

Resource: Copilot for Obsidian https://community.obsidian.md/plugins/copilot · Dataview example vault https://github.com/s-blu/obsidian_dataview_example_vault

## 55. Should I trust everything AI answers? How do I catch it making things up on the spot?

AI answering from your vault does not mean it cannot be wrong. RAG retrieval only takes the top 3-5; if the relevant note is not in the top few, AI can only fabricate. And it is semantic retrieval, not keyword retrieval, so short phrases like "1 on 1" get preprocessed as stopwords and dropped, so they are never even retrieved.

Three ways to catch it on the spot. First, watch whether its answer points to a specific note; vague talk with no source gets a question mark. Second, push back: "which exact sentence in which note did you just cite", a real reader points it out, a fabricator is exposed on the spot. Third, check against facts you know: if you remember writing the opposite conclusion and it says the vault has none, that is a hallucination. The final gate is always your own known judgment; do not treat ChatGPT as an infallible oracle, it is a predicted-text generator by design.

Copy-paste template:

```
# Spot AI hallucination: three push-back questions (copy and ask)
1. Which exact sentence in which note did you just cite?
2. Paste that sentence verbatim for me to see.
3. I check against known facts: I recorded the opposite conclusion, you said none exists, explain.
Cannot give a specific source -> probably making it up, do not adopt.
```

Resource: Smart Connections https://github.com/brianpetro/obsidian-smart-connections

## 56. How do I let AI run a "regular health check" on the vault so it does not get messier?

Handing cleanup entirely to AI most often leaves the vault no clearer, only adding a layer of source-less AI-generated pages on top of the pile. The fix is a regular Lint that reviews every round of output.

The Lint flow checks four things: contradictions between pages, old conclusions overturned by new material, orphan pages with no inbound links, and concepts mentioned but without their own page. Treat the report only as a checklist; you decide whether to delete or fill in, and without your consent AI must not delete anything. Such checks can also be written as standing queries; the community has ready-made example vaults you can copy directly, far more accurate than writing from scratch. AI cleanup is reviewed round by round, and only by clarifying sources and links each round does the vault stay clean.

Copy-paste template:

```
# Regular Lint: force it to have really read the vault (copy and ask AI)
Review the whole wiki/: find contradictory pages, conclusions overturned by new material,
source-less orphan pages, give a report and suggest blank concepts worth creating.
Make no deletion without my consent.

# Standing query: catch pages missing sources
# Install and enable the Dataview plugin first, then put these three lines in a dataview code block
TABLE file.mtime AS modified
FROM "wiki"
WHERE !source AND !source_url
```

Resource: Dataview https://community.obsidian.md/plugins/dataview · Dataview example vault https://github.com/s-blu/obsidian_dataview_example_vault

## 57. Using AI as a second brain, how do I prevent cognitive atrophy?

Cognitive atrophy hits people who use it well, because AI is so convenient you easily hand over the thinking part too. Three risks sit there: memory atrophy, storing everything in the vault and never memorizing yourself; absorption atrophy, only reading AI's summaries and never the original; competence illusion, assuming that having it in the vault means you understand it.

Hold three defensive lines: make the key judgments yourself, at least occasionally go back to the original when AI gives a summary, and keep a paragraph of your own writing in every note. To judge whether a note passes, check whether it contains one line only you could have written. The generative processing theory says learning happens when external tasks trigger internal cognitive processing, and linking a note to existing knowledge is exactly that kind of generative activity; storing without processing simply never triggers it. The second brain is an add-on; the thinking part stays yours.

Copy-paste template:

```
# Three risks + three defenses of cognitive atrophy
Risks: 1 Memory atrophy (store only, never memorize) 2 Absorption atrophy (read summaries, skip originals) 3 Competence illusion (having = understanding)
Defenses: 1 Make key judgments yourself 2 At least occasionally reread originals from AI summaries 3 Keep your own written paragraph in every note
The second brain is an add-on; the thinking part stays yours.

# One slot per day (write it in your daily template)
## One thing I figured out myself today
(no paste, no AI ghostwriting, one sentence counts)
```

Resource: Periodic Notes https://community.obsidian.md/plugins/periodic-notes

## 58. My notes are too shallow, even AI cannot save them. How do I make them "feedable"?

If it is all copy-paste excerpts, AI reads around and still says nothing useful, because there is none of you in it. A feedable note carries a bit of your own processing in every entry, even just one line, and uses frontmatter to mark the structure so AI retrieval and filtering work.

The easiest practice is to fix a few lines into a template: what the topic is, why you noted it, which existing note it relates to. The property system makes Dataview queries and AI filtering run; Claude finds all active projects by reading type and status, and you see this month's notes by querying created. Three lines of frontmatter cost twenty seconds when writing, and later AI strings your scattered judgments along these lines instead of just repeating excerpts. Bind this skeleton to new notes with Templater, and it is there before you even think about it.

Copy-paste template:

```
# "Feedable" note skeleton (auto-insert on new note)
---
topic: 
why noted: 
related: [[]]
status: raw
date: 2026-08-10
---

## Excerpt / original


## My judgment
One sentence is enough, state any one of these:
what it overturned in my earlier view / what it confirmed / what I plan to do with it

# How to bind
Settings -> Community plugins -> install Templater -> point Template folder to templates/
Save the above as templates/new-note.md, insert with one click when creating a note
```

Resource: Templater https://community.obsidian.md/plugins/templater-obsidian · Obsidian Properties docs https://help.obsidian.md/properties

## 59. What is it like when AI uses your links, and why is linking carefully worth it?

AI reading your vault is not just keyword matching; it does graph retrieval along the links: two notes you linked are treated as related and pulled together. A correct link directly trades for retrieval quality.

When you ask about a concept, it does not only find the page whose title hits; it also pulls the few pages connected by links, even if those pages never contain the word you asked. To decide whether a link should exist, ask one question: when I see A later, will I want to find B. Linking randomly creates noise; fewer but accurate links make AI clearly understand you better. Every permanent note carries at least two explicit links; the first is usually obvious, the second is where you must think how the idea fits the existing network, and that harder thinking produces better connections.

Copy-paste template:

```
# Link trade-off (review after each note)
Ask yourself: when I see A later, will I want to find B?
  yes -> link; hesitate -> do not link (fewer is better)
Every note keeps at least 1 outbound link to a higher MOC or concept page

# 10 minutes of link-catch-up per week (copy and ask AI)
List the notes in my vault with zero outbound and zero inbound links, sorted by modified time;
give me 2 candidate links and one reason per note, I decide.
```

Resource: Smart Connections https://github.com/brianpetro/obsidian-smart-connections

## 60. AI helps with periodic review and weekly reports, how do I let it write for me but not think for me?

The boundary for AI doing review must be strict: it writes for you, not thinks for you. Hand it your daily notes, project notes, and meeting records to draft; you decide what matters, how to phrase it, and what to expand.

The concrete practice is to fix a minimum frequency you will actually keep, say reviewing the inbox and this week's additions every two weeks, with review bundled into the weekend and triggered by opening the note, which beats relying on reminders. The most important blank in the weekly template is the two columns "biggest gain this week" and "focus next week" left empty for you to fill; that forces your own thinking. It saves the typing and summarizing effort; the judgment part stays with you, and those two columns are exactly what is valuable in a weekly report, which AI cannot give. Standard metadata (unified tags, dates, project links) also lowers AI retrieval cost.

Copy-paste template:

```
# Let AI draft the weekly report (you decide conclusions)
Based on this week's daily notes, project notes, and meeting records, draft a weekly report:
1. List what moved forward this week (grouped by project)
2. Flag the points worth expanding
3. Leave "biggest gain this week" and "focus next week" empty for me to fill
Write for me only, not think for me; conclusions and wording are mine.

# Companion setup
Settings -> Community plugins -> install Periodic Notes and Calendar
In Periodic Notes enable only weekly and monthly notes, turn off daily reminders
Fix review time to Sunday night, click that slot on the calendar to start
```

Resource: Periodic Notes https://community.obsidian.md/plugins/periodic-notes · Calendar https://community.obsidian.md/plugins/calendar

## 61. Can AI dig out hidden relations between notes, and how?

Yes, and this is where AI beats people. Hidden relations live in semantics; you did not realize two notes were related when you wrote them, but AI reading the whole vault can match them, like a pit from a project half a year ago and a similar problem in another project last month.

How accurate the dig is depends entirely on how tightly the instruction is bounded: give a time range, require paired note names, and attach one relation judgment per pair. Without bounds it only gives you empty talk like "both about efficiency". You review the pairs it digs out, and when you accept one, add a link, which immediately helps next retrieval. The premise holds: notes must have real content; an empty vault yields nothing. Each week, have AI scan recently created and modified notes for strong relations not yet made explicit; people are lazy to do this, AI can.

Copy-paste template:

```
# Hidden-relation mining (bound time range + paired output + relation judgment)
Look only at notes I created between 2025-01-01 and 2026-08-01.
Find 10 pairs of notes that are clearly related but currently have no link, output in this format:

[[NoteA]] <-> [[NoteB]]
Relation: one sentence on why, pick from: same pit / confirm each other /
  later overturns earlier / two applications of one method / two stages of one problem

Requirements:
1. Output only note names that really exist in the vault, do not invent
2. Be specific about the relation, no empty talk like "both about efficiency"
3. Put uncertain pairs in a separate "unsure" column
4. At the end tell me: of these 10 pairs, which one most deserves a link today
```

Resource: Smart Connections https://github.com/brianpetro/obsidian-smart-connections

## 62. My vault spans several years, how does AI use Dataview to index "me in time"?

For a multi-year vault to be read in time by AI, every note must carry a time mark, and you use a query like Dataview to pull notes out as a database. Daily notes are named by day, periodic notes grouped by week/month/season/year, and the date field in frontmatter is clear, so AI can pull notes from both ends along the timeline to compare.

The Dataview query below pulls the last 30 days of daily notes into a list; note that you must install the Dataview plugin before copying, otherwise pasting it only shows as a plain code block and runs nothing. Fix four review notes per week/month/season/year, and AI reviews and plans at different scales, so last year's you and this year's you are laid side by side. When you ask "how did my view on X two years ago differ from now", it needs exactly that line. Keep writing and add time marks, and the vault slowly becomes your own archive in time.

Copy-paste template:

```
# Install and enable the Dataview plugin first, otherwise it only shows as a plain code block
# Usage: create a code block, label the language as dataview, put these three lines in
LIST FROM #diary
WHERE file.cday >= date(today) - dur(30 days)
SORT file.cday DESC

# How to mark time (frontmatter of each daily note)
---
date: 2026-08-10
tags: [diary]
---

# Cross-time comparison (copy and ask AI)
Along the timeline, find my notes on [topic] from 2024 and 2026,
list 3 from each side, and state where my view changed and where it did not.
```

Resource: Dataview https://community.obsidian.md/plugins/dataview · Dataview example vault https://github.com/s-blu/obsidian_dataview_example_vault

## 63. How do I use daily notes to string scattered notes into "me in time"?

The daily note is the front door of the vault; everything lands in that day's note first, you only capture during the day and make no filing decisions, and process at night. One note per day, timestamped, recording what happened, what you captured, what you decided, and the timeline grows naturally.

The concrete practice: mark type: daily and date in the frontmatter of each daily note, and leave blocks for Morning Context, The One Thing, Captures, Decisions Made, End of Day. In the morning, have AI generate a brief from yesterday's open loops and project status and auto-link it in, so context is there the moment you open the note. AI can also read your daily note's Captures in the background, file tasks to project notes, turn ideas into permanent notes, and carry open loops to tomorrow's daily note. Do not ritualize the capture step; leave the structuring to compile, and let the daily note only record honestly.

Copy-paste template:

```
---
type: daily
date: 2026-08-10
day: Tuesday
---

# August 10, 2026

## Morning Context
[[2026-08-10-morning-brief]]

## The One Thing
> The single most important outcome for today

## Captures
* Everything that comes in lands here, no filing decisions during the day *

## Decisions Made
DECISION:
CONTEXT:
REASONING:

## Open Loops
* Unfinished items to carry forward *

## End of Day
What happened:
Carrying forward:
Tomorrow's One Thing:
```

Resource: Calendar https://community.obsidian.md/plugins/calendar · Obsidian Daily notes docs https://help.obsidian.md/Daily+notes

## 64. How do I design tags and properties so AI retrieval does not drift?

AI retrieval relies on the structured fields in frontmatter; the taxonomy in your head is something it cannot read. Fix type, status, created, and tags, and Dataview queries and AI filtering have something to grab, otherwise it can only guess from full text.

Make the naming convention "type + status + date + topic", so partial keywords locate any note: you know the type, roughly when it was created, and the topic, and those three pieces make every note findable without navigating folders. Use flat specific tags (like productivity, compounding, knowledge-systems), not deep hierarchies, so AI clustering by tag and filtering by property are both more accurate. Standard metadata (unified tags, dates, project-link format) directly lowers AI retrieval cost. Mark the type clearly in every permanent note's frontmatter, and the model gets the new-page vs. edit-page call right nine times out of ten.

Copy-paste template:

```
# Property system (carry in every note's frontmatter)
---
type: permanent        # permanent / literature / project / decision / daily
status: active         # active / archived / draft
created: 2026-08-10
tags: [productivity, compounding, knowledge-systems]
---

# Naming convention: type + status + date + topic
2026-08-10-permanent-obsidian-ai-note.md
2026-08-10-project-second-brain.md

# Templater binding (auto-fill date and type on new note)
Settings -> Community plugins -> install Templater -> point Template folder to templates/
```

Resource: Obsidian Properties docs https://help.obsidian.md/properties · Templater https://community.obsidian.md/plugins/templater-obsidian
