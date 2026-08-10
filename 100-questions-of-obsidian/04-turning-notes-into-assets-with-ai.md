# Chapter 4 · Turning Notes into Assets with AI: from storing to using

Hundreds of notes piled up and still gathering dust: the problem is not the recording, it is that nothing gets used. This chapter is about making AI turn your accumulation into something usable, not another smarter favorites folder. The real value starts after you connect AI. The more AI can answer from what you have stored, the more your notes become assets instead of a digital junk pile.

## 47. My notes pile into a mountain, how does AI help me "use" them instead of "store" them?

Store without processing and everything in the inbox loses value on a slope. Give it a few weeks and you will not bother opening it yourself. There are only two signs of actually using it: related old notes jump out on their own while you write, and AI answers your questions from what you recorded before rather than inventing from zero.

Someone installed Smart Connections, wrote one paragraph, and three notes from six months ago floated up in the sidebar. That is what using feels like. Storing moves things into a warehouse; using makes the warehouse feed you back. Do not wait for a perfectly organized vault before connecting AI. Make it readable first, and one real thought dropped into the inbox each day is enough. Once links weave the notes into a web, AI can also surface patterns you never noticed, like stalling on the same type of goal every quarter-end.

Resource: Smart Connections https://github.com/brianpetro/obsidian-smart-connections

Copy-paste template (use directly):

```
# Three switch-on moves, from "store" to "use"
1. Install Smart Connections so old notes float into the sidebar while you write
2. Drop 1 thought with your own judgment into inbox/ each day (not just a link)
3. Ask your vault once a week (copy this to your AI):
   What did I record about [topic] in the last six months? List it by date,
   mark which note each item comes from, and add nothing that is not in the vault.
```

## 48. What is Vault QA, and how do I get AI to answer from my accumulation?

Vault QA means treating your notes as the knowledge base: AI reads the vault first, then answers, so the answer comes from your own accumulation. It has a ceiling. When notes are not connected, or the question needs synthesis across several years, retrieval tends to grab a few superficially related items and answer off target.

A workable vault has two layers: raw/ for original material, wiki/ for processed concept pages, with a master index.md inside wiki/. Before asking, have AI read index.md to get the whole picture, then require it to point at the specific source page and to say plainly when the vault has nothing. Ask "what was my conclusion about X last year" and it flips through your own notes instead of generic web talk. The denser the links and the more you process afterwards, the more accurate it gets.

Resource: Copilot for Obsidian https://community.obsidian.md/plugins/copilot

Copy-paste template (use directly):

```
Please first read wiki/index.md to understand the whole, then answer my question based on wiki/ content: [your question]
When answering, cite the specific source page in wiki/; if the knowledge base has no related info, please tell me.

# The two-layer structure (build it like this)
raw/    original material, keep source_url, no processing
wiki/   processed concept pages, source noted at the top of each page
wiki/index.md   master index, AI reads this first every time
```

## 49. While writing, AI auto-surfaces related old notes. How do I turn on this "cheat"?

The cheat is Smart Connections. It embeds your notes so related old ones surface beside you while you write, with no manual searching. The premise is that the notes have content and connections; an empty vault has nothing to surface.

Someone migrating from another tool made dropping the perfect-folder-tree habit their first move, because surfacing while writing beats a tidy directory. You are writing a thought about a concept and it lists three notes you wrote six months ago, and you pick up the old thread at a glance. After installing, open any note and start writing; the right sidebar comes alive. For a non-English vault, pick the matching embedding model (see Q36), since the wrong one degrades surfacing quality badly.

Resource: Smart Connections https://github.com/brianpetro/obsidian-smart-connections

Copy-paste template (use directly):

```
1. Settings → Community plugins → Browse → search Smart Connections → install and enable
2. First open prompts embedding generation (match the model to your vault language, see Q36)
3. Open any note and start writing; related old notes surface in the right sidebar
4. When surfacing is off, go add the links that should exist; quality follows connections

# Connect a new note to old accumulation on the spot (ask AI on the open note)
Based on the notes already in my vault, list 3-5 links worth adding to this note,
each with one sentence on why. Put anything uncertain in a separate list for me to decide.
```

## 50. Will my second brain just be a logbook? How do I tell if it really "thinks"?

A big vault does not equal thinking. A logbook only records without processing: one entry today, one tomorrow, nothing connected, and looking back gives you a stream of sludge. Real thinking means you made a judgment while recording, that these two relate, that one overturned an earlier conclusion, and you go back and revise on a schedule.

Someone kept a vault for over five years and then deleted it, saying they had only been a mover, shifting things from one place to another with the brain switched off. Treating favoriting as effort and vault size as growth mostly hoards things you never read. Three self-checks are the most direct: are there connections between notes, have you processed them afterwards, can the old ones be used when you write something new. All three empty and it really is just a logbook. Whether your vault thinks decides whether what AI answers from it later has roots.

Resource: Dataview https://community.obsidian.md/plugins/dataview

Copy-paste template (use directly):

```
# Is your second brain "thinking" or a "logbook"? Three self-checks
- Are there connections between notes? (MOC / links)
- Have you processed them afterwards? (periodic review, updated conclusions)
- Can the old ones be used when writing something new? (AI can answer from accumulation)
All three empty → just a mover; add processing before it counts as thinking

# Quantify check one: pull out every island note
# Install and enable the Dataview plugin first, then put these three lines in a code block tagged dataview
LIST
WHERE length(file.outlinks) = 0 AND length(file.inlinks) = 0
SORT file.mtime DESC
```

## 51. AI auto-builds my links/MOC. Is that laziness or really useful?

AI-built links are acceleration, on the condition that you review every one it creates. An MOC is a map gathering same-topic notes; AI drops the scattered ones into the right MOC and saves you the manual labor, while accuracy stays your call.

Someone installed an auto-complete link plugin to save effort and ended up linking unrelated notes on reflex, producing more noise than value. So fix the flow in two steps: AI drafts, you cut and edit. Use completion plugins as typing accelerators, pick from the popup yourself, and never let them decide what connects to what. The value of links sits in the connection itself; AI only spreads the work of connecting.

Resource: Various Complements https://community.obsidian.md/plugins/various-complements

Copy-paste template (use directly):

```
# Let AI draft the MOC (you cut and edit)
Scan every note under notes/ and cluster them into 5-8 topic groups. For each group give me:
1. A suggested MOC name
2. The notes in that group (written as [[links]])
3. One sentence on why they group together
Put anything uncertain under "undecided"; do not force it into a group.
Only output note names that actually exist in the vault; invent nothing.
```

## 52. Letting AI review old notes periodically, how do I set it up without notification hell?

For reviewing, frequency matters more than intensity. Set it too dense with daily popups and you will eventually switch off the whole system, dragging the accumulation you already built down with it.

Someone paired periodic notes with a review plugin, set reminders to daily, and uninstalled two weeks later. The fix is simple: pick the lowest frequency you will actually keep, say flipping through the inbox and this week's additions every two weeks, put the review on the weekend, and give it one fixed slot on the calendar where AI does all its work. Use Periodic Notes with Calendar to generate weekly and monthly notes, turn every notification off, and trigger the review by opening the note. That is far more reliable than reminders.

Resource: Periodic Notes https://community.obsidian.md/plugins/periodic-notes · Calendar https://community.obsidian.md/plugins/calendar

Copy-paste template (use directly):

```
# Let AI run your periodic review (every two weeks, not daily)
Read my inbox and daily notes from the last two weeks, pick out old notes related to [current project],
list them, and add one sentence per item on how it can be used now.
Only list notes that actually exist; invent nothing.

# Companion setup
Settings → Community plugins → install Periodic Notes and Calendar
In Periodic Notes enable weekly and monthly only; turn the daily reminder off
Fix the review slot at Sunday evening; click that calendar cell and start
```

## 53. How does AI distill my old fragments into a long article?

Fragments scattered everywhere are exhausting to string together by hand, and asking AI to "just write it" gives you a piece that does not sound like you. The workable route is gather first, write second: AI compiles the fragments into source-backed concept pages, and you write your viewpoints on top of that skeleton.

Give it one clear instruction: read the new material in raw/, generate a source-summary page for each while keeping the original link, extract important concepts to update or create concept pages, then update the master index. When compiling finishes you hold a skeleton with citations, and the long article grows out of your own accumulation. Do not skip the source-marking step, because without it you will never trace where a sentence came from.

Resource: Copilot for Obsidian https://community.obsidian.md/plugins/copilot

Copy-paste template (use directly):

```
# Step 1: compile (AI does this)
Please read the new material in raw/ and compile it into wiki/.
1. Generate a source-summary page for each material, keep source_url.
2. Extract important concepts, update or create concept pages in wiki/concepts/.
3. Update wiki/index.md master index.

# Step 2: skeleton (AI does this)
Based on the pages in wiki/concepts/ related to [topic], give me a long-article outline:
under each section list the concept pages that support it, leave the viewpoint slots empty for me.

# Step 3: write (you do this)
Viewpoints, trade-offs and conclusions are yours; AI only fills in facts and sources.
```

## 54. Using AI to organize notes, how do I avoid making it messier (the AI junkyard)?

Turn AI loose on organizing and the usual result is a vault that got no clearer plus an extra layer of sourceless AI-generated pages, one junk pile stacked on another. The way to block it is a regular health check that puts every round of output through review.

Someone runs a health check on the vault monthly: read the master index, find which pages lack sources, which concept definitions contradict each other, which pages sit as islands with no links, which concepts get mentioned repeatedly without a page of their own. Treat the result as a checklist only; deleting or filling stays your decision. This kind of check can also live as a standing Dataview query, and the community keeps ready-made example vaults you can copy, which beats writing from scratch. AI organizing is round after round of review, and clarifying sources and connections each round is what keeps the vault from getting dirtier.

Resource: Dataview https://community.obsidian.md/plugins/dataview · Dataview example vault https://github.com/s-blu/obsidian_dataview_example_vault

Copy-paste template (use directly):

```
# Monthly health check (copy this to your AI)
Please read wiki/index.md and run a health check:
1. Which pages lack sources 2. Which concept definitions conflict with each other
3. Which pages are islands with no links 4. Which concepts are mentioned repeatedly but have no page yet.
List only pages that actually exist, return a checklist, and do not delete or edit anything for me.

# Standing query: catch pages with no source
# Install and enable the Dataview plugin first, then put these three lines in a code block tagged dataview
TABLE file.mtime AS Modified
FROM "wiki"
WHERE !source AND !source_url
```

## 55. Should I trust everything AI answers? Three ways to spot errors

AI answering from your vault does not mean it gets things right. The vaguer your question, the more likely it patches in content the vault never contained. Three ways to catch it on the spot.

First, check whether the answer points at a specific note; vague talk with no source gets a question mark. Second, follow up with "which sentence in which note did you just cite" — anything that truly read your vault can point, and fabrication exposes itself immediately. Third, test it against a fact you know: you remember writing the opposite conclusion last month and it claims the vault has nothing, that is hallucination. Someone using Smart Connections caught fabrication exactly with that second question. The last gate is always your own known judgment.

Resource: Smart Connections https://github.com/brianpetro/obsidian-smart-connections

Copy-paste template (use directly):

```
# Spot AI hallucination: three follow-ups (copy and ask)
1. Which sentence in which note did you just cite?
2. Paste that sentence verbatim so I can see it
3. Checking against a known fact: I recorded the opposite conclusion, you say I did not. Explain.
No specific source → probably fabricating, do not adopt
```

## 56. What does "an AI that gets me" rely on, links or the preface I wrote?

Links and prefaces give two different things, and missing either leaves AI with half the picture. Links give structure, telling it these notes belong together. The preface gives intent: write at the top of a note what problem it solves and which project it belongs to, and AI knows why you recorded it instead of reading only the surface.

Someone adds frontmatter to every note, marking topic, status and relations in the header, so retrieval filters correctly on the first pass. One level up, put a usage manual for the whole vault in the root directory (commonly named CLAUDE.md or AGENTS.md) explaining the folder structure, the naming rules, and how you want AI to work with this vault, so it reads that first every time. Worth more than the manual is a me.md: who I am, what I am working on, what I care about, what not to do to me. Any AI can read that file, and you stop reintroducing yourself every time.

Resource: Obsidian Properties documentation https://help.obsidian.md/properties

Copy-paste template (use directly):

```
# me.md minimal skeleton (vault root; have AI read it first every time)
---
type: profile
updated: 2026-08-10
---

## Who I am
One line: profession / field / current role

## What I am working on
- Main: [[Project A]] (goal, and where it is stuck right now)
- Side: [[Project B]]
- Long-running questions I care about:

## How my vault is organized
- inbox/ unprocessed · notes/ processed · wiki/ concept pages
- Naming rule: YYYY-MM-DD-topic
- Link only what is genuinely related; fewer and accurate beats many

## What I want AI to do
- Answer from this vault, cite the source note for every conclusion
- Say so plainly when the vault has nothing; do not patch it
- Conclusions and wording stay mine; you gather, retrieve, and draft
```

## 57. How do I make AI cite my note sources instead of making things up?

Fabrication starts where nobody asked for sources. Put "point to which paragraph of which note" into the prompt and hallucination drops by more than half, because it knows you will check and will not risk inventing a note that does not exist.

Beyond adding that line to every question, add a periodic lint: have it review the whole vault for contradictory pages, conclusions overturned by newer material, and sourceless orphan pages, then hand you a report. Demanding sources is not only for your peace of mind, it forces the model to actually read the vault. Ask every time and it runs out of room to bluff, and the answers become accountable.

Resource: Copilot for Obsidian https://community.obsidian.md/plugins/copilot

Copy-paste template (use directly):

```
# Make AI cite sources (add this to any vault-based question)
Answer from my notes and mark which specific paragraph of which note each conclusion comes from;
if the vault has no such information, tell me plainly and do not fabricate a source.

# Periodic lint: force it to actually read the vault
Review the entire wiki/: find contradictory pages, conclusions overturned by newer material,
and sourceless orphan pages. Give a report and suggest blank concepts worth creating.
```

## 58. My notes are too shallow for AI to save. How do I record so they are "feedable"?

When everything is a copy-pasted excerpt, AI reads the whole pile and has nothing to say, because none of it is yours. Feedable notes carry a bit of your own processing in every entry, even a single sentence.

Someone recorded books with nothing but title, author and rating, then forced one line under each entry saying "this connects to that project from last year", and AI immediately had a thread to follow. The cheapest way is to freeze those lines into a template: what the topic is, why you recorded it, which existing note it relates to. Three lines of frontmatter cost twenty extra seconds, and later AI follows those three lines to string your scattered judgments together instead of reciting excerpts. Bind the skeleton to new notes with a template plugin and it shows up without you thinking about it.

Resource: Templater https://community.obsidian.md/plugins/templater-obsidian · Obsidian Properties documentation https://help.obsidian.md/properties

Copy-paste template (use directly):

```
# "Feedable" note skeleton (auto-inserted on new notes)
---
topic: 
why_recorded: 
related: [[]]
status: raw
date: 2026-08-10
---

## Excerpt / original


## My judgment
One sentence is enough. Pick any of these:
what it overturns for me / what it confirms / what I plan to do with it

# How to bind it
Settings → Community plugins → install Templater → point Template folder at templates/
Save the block above as templates/new-note.md and insert it with one command
```

## 59. What is it like when AI uses my links, and why is careful linking worth it?

AI reading your vault is not plain keyword matching; it walks the links as a graph, and two notes you linked are treated as related and pulled together. Links you got right convert straight into retrieval quality.

Ask about a concept and it returns not only the title match but the notes attached through links, even ones that never contain the word you asked about. Someone migrating vaults moved all the folder-tidying effort into linking for exactly this reason. Random linking manufactures noise, while few and accurate links make AI visibly better at understanding you. To decide whether a link belongs, ask one question: when I later land on A, will I want to find B?

Resource: Smart Connections https://github.com/brianpetro/obsidian-smart-connections

Copy-paste template (use directly):

```
# Link trade-off (run this after finishing a note)
Ask yourself: when I later land on A, will I want to find B?
  Yes → link it; hesitating → skip it (fewer and accurate)
Leave at least 1 outgoing link per note, pointing to a higher-level MOC or concept page

# Ten minutes of link repair each week (copy to your AI)
List the notes in my vault with zero outgoing and zero incoming links, sorted by modified time;
give me 2 candidate links per note with one sentence of reasoning, and I will decide.
```

## 60. AI writes my weekly report. How do I stop it from thinking for me and keep it to writing?

The boundary for AI-written weekly reports has to be hard: it writes for you, it does not think for you. Hand it your daily notes, project notes and meeting records and let it draft; which items matter, how to phrase them, what deserves expansion, you decide.

Someone deleted their second brain because everything got tossed to the tool to summarize, and over time they stopped bothering to organize their own thoughts. The way around it is a template with holes in it: the "biggest gain this week" and "next week's focus" columns must arrive empty, forcing you to fill them. AI saves the typing and the aggregation; the judgment stays with you. Those two columns are the only truly valuable part of a weekly report, and AI cannot supply them.

Resource: Periodic Notes https://community.obsidian.md/plugins/periodic-notes

Copy-paste template (use directly):

```
# Let AI draft the weekly report (you decide conclusions)
Draft a weekly report from this week's daily notes, project notes and meeting records:
1. List what moved forward this week (grouped by project)
2. Mark the points worth expanding
3. Leave "biggest gain this week" and "next week's focus" empty for me
Write for me, do not think for me; conclusions and wording are mine.
```

## 61. Can AI dig out hidden relationships between notes? How?

It can, and this is where AI beats people. Hidden relationships hide in semantics: you did not notice two notes were related while recording them, and AI reading the whole vault can compare, say a project pitfall from six months ago against a similar problem in another project last month.

Someone used this to discover they had written the same lesson into project reviews three years running, treating it as a new problem every time. Accuracy depends entirely on how tightly you constrain the instruction: give a time range, require paired note names as output, and demand one sentence of relationship judgment per pair. Leave the range open and you get a pile of "both relate to productivity" filler. Review the pairs yourself, and when you accept one, add the link so the next retrieval uses it. Same premise as always: the notes need real content, an empty vault yields nothing.

Resource: Smart Connections https://github.com/brianpetro/obsidian-smart-connections

Copy-paste template (use directly):

```
# Hidden relationship mining (time range + paired output + relationship judgment)
Look only at notes I created between 2025-01-01 and 2026-08-01.
Find 10 pairs of notes that are clearly related in content but currently have no link between them.
Output in this format:

[[Note A]] <-> [[Note B]]
Relationship: one sentence on why they relate, chosen from:
      same pitfall / mutually confirming / the later one overturns the earlier /
      same method applied twice / different stages of the same problem

Requirements:
1. Only output note names that actually exist in the vault; invent nothing
2. Be specific; filler like "both relate to productivity" is rejected
3. Put uncertain pairs in a separate "unsure" section
4. Finish by telling me which single pair is most worth linking today
```

## 62. My vault spans years. How does AI understand "me across time"?

For AI to read time out of a multi-year vault, every note needs a time mark. Name daily notes by day, group periodic notes by week, month, quarter and year, and write the date field clearly in frontmatter, so AI can walk the timeline and pull both ends together for comparison.

Someone fixed four kinds of review notes, weekly, monthly, quarterly and yearly, so AI could look back and plan at different scales, and last year's you and this year's you finally get laid side by side. Ask "how does my view of X differ from two years ago" and this line is exactly what it needs. Keep recording, keep the time marks, and the vault gradually becomes your own time archive. The Dataview query below pulls the last 30 days of daily notes into a list. Install the Dataview plugin before you copy it: without the plugin, pasting it just renders a plain code block and returns nothing.

Resource: Dataview https://community.obsidian.md/plugins/dataview · Periodic Notes https://community.obsidian.md/plugins/periodic-notes

Copy-paste template (use directly):

```
# Install and enable the Dataview plugin first, or this renders as a plain code block
# Usage: create a code block, tag the language as dataview, put these three lines inside
LIST FROM #diary
WHERE file.cday >= date(today) - dur(30 days)
SORT file.cday DESC

# How to mark time (frontmatter of each daily note)
---
date: 2026-08-10
tags: [diary]
---

# Cross-time comparison (copy to your AI)
Walk the timeline and find my notes about [topic] from 2024 and from 2026,
list 3 from each side, and tell me which part of my view changed and which part did not.
```

## 63. Letting AI be my "second brain", how do I prevent cognitive atrophy?

Cognitive atrophy happens to the people who use it well. Three risks sit there: memory atrophy, where everything goes into the vault and nothing into your head; absorption atrophy, where you read AI summaries and never the original; and the competence illusion, where having it in the vault feels like understanding it.

Someone retreated from digital tools back to pen and paper to force their own thinking. You do not need to retreat that far. Hold three lines instead: make the key judgments yourself, revisit the original behind an AI summary at least occasionally, and keep one passage you wrote yourself in every note. To judge whether a note passes, look for one sentence only you could have written. The second brain is an add-on, and the thinking part cannot be handed over.

Resource: Periodic Notes https://community.obsidian.md/plugins/periodic-notes

Copy-paste template (use directly):

```
# Three atrophy risks + three defenses
Risks: ① memory atrophy (store but never retain) ② absorption atrophy (summaries only, never originals) ③ competence illusion (having = understanding)
Defenses: ① make key judgments yourself ② revisit originals behind AI summaries at least occasionally ③ keep one passage you wrote in every note
The second brain is an add-on; the thinking part stays yours.

# One slot a day (put it in the daily note template)
## One thing I figured out myself today
(No pasting, no AI ghostwriting; one sentence counts)
```

## 64. AI is not here to remember for you, it is here to help you think. How does that land day to day?

Landing this line depends on a few tiny daily actions, not on one big cleanup. Fix the division of labor first: AI gathers, retrieves and marks sources; you think and write.

When recording, add one line of your own judgment instead of copying only. While writing, let AI surface related old notes and do the connecting and the trade-offs yourself instead of transcribing. When asking AI, require sources and keep the verification step. For weekly reports it drafts, and you fill in the biggest-gain column. Hold that line daily and the vault is an asset, not another warehouse gathering dust.

Resource: Smart Connections https://github.com/brianpetro/obsidian-smart-connections · Periodic Notes https://community.obsidian.md/plugins/periodic-notes

Copy-paste template (use directly):

```
# Five minutes a day: point AI at "helping you think"
Morning: open today's daily note, write one line about what you figured out yesterday (yourself)
Midday: for every quick capture, add one line of "why I recorded it" (yourself)
Evening: copy this to your AI (it gathers, you judge)
    Find 2-3 groups where what I recorded today relates to older notes in my vault.
    Give the note names and one sentence of relationship per group, using only notes that exist.
Weekend: have it draft the weekly report with "biggest gain this week" left empty for you
```
