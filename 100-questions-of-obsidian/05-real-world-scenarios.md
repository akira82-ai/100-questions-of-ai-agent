# Chapter 5 · Real-World Scenarios: exam prep, writing, research, workplace, ready to use

Everything before was underlying capability; this chapter goes straight into scenarios. Each scenario gives you a copyable workflow; the only point is: AI gives the draft, you make the trade-offs. Do not hand out the judgment step.

## 65. Grad school / civil service exam: how to let AI generate mock questions and test points based on my notes?

Someone used Obsidian for exam prep, ranking near the top on the initial test, not by grinding others' questions but by turning their own notes into a question bank. The method is feed each chapter's notes to AI, let it generate mock questions based on your expression, then check against the test points you recorded for gaps.

Specifically, each section you recorded marks the key points clearly; let AI generate multiple-choice, short-answer, essay questions by your note structure, and the questions stick to your language, so at a glance you know which part you have not digested. Someone specifically used Obsidian for math exam prep stress-testing, linking formulas and derivations into a net, and AI generating questions along links is more accurate than blind grinding. Your notes are the question source, AI is responsible for deforming questions by your thread, you are responsible for doing and correcting. Practice this way, are you not tested exactly on what you already recorded?

Copy-paste template (use directly):

```
# Let AI generate mock questions based on your notes
Please read my [[Chapter X notes]], generate three types of questions by my recorded structure and expression:
- Multiple choice: test concepts I marked as key
- Short answer: test derivations / steps I recorded
- Essay: test which related notes I can string together
After generating, check against my recorded test points, mark where I have not digested.
```

## 66. Forgetting after memorizing, how to use AI to turn notes into flashcards (Anki-style)?

Forgetting after memorizing, the problem is no spaced review rhythm. Someone splits notes into Q&A pairs, imports into a flashcard tool, pushes by forgetting curve, and memorization efficiency clearly rises.

The method is let AI read one of your notes, extract the key concepts and corresponding answers, generate Q&A cards one by one, you review and delete the wrong ones, then batch import. Do not let it memorize the whole thing for you; let it cut your notes into small questions that can test you. Someone migrating from another tool made dropping the pursuit of perfect structure their first move; same for flashcards, first cut cards for the most important chapter, get running first. The cards are your own notes turned into them, not questions found online, sticking to your real weak points.

Copy-paste template (use directly):

```
Cut a note into Q&A pairs, then batch import into a flashcard tool:
- Front: What is Obsidian's core file format?
- Back: Local Markdown plain text (.md)
- Front: What syntax are links in Obsidian?
- Back: Wrap with [[note name]]
```

## 67. When writing gets stuck, how to let AI dig topics and material from my vault?

Someone writing novels and world-building, when stuck, lets AI flip their own vault, pulling out related settings, fragment inspirations, similar passages recorded before. Writing stuck is often not having nothing to write, but forgetting what you already recorded.

Let AI do association based on your vault; like you are writing a conflict about a character, it flips out a similar bridge you recorded half a year ago, and you have material at once. Someone reviewed saying the most valuable was exactly the casual fragments; letting AI surface these while writing is faster than staring at a blank page. You screen what AI digs out, not every paragraph should be used, but it puts the material buried in your vault on the table, and the stuck point breaks.

Copy-paste template (use directly):

```
# When writing gets stuck, let AI dig material from vault
Please read all fragments and old notes in my vault about [character / theme],
list: ① settings and bridges directly reusable ② similar passages recorded before but forgotten
③ contradictions worth expanding. I write after screening, not copying every paragraph.
```

## 68. An article half-written, let AI continue writing, will it go off track? How to control?

Someone let AI continue writing, only to find it veers more and more, because it does not know where you want to go. Controlling derailment, the key is give it boundaries first.

Before letting AI continue, first have it read what you wrote, then require it to list an outline of the next three paragraphs for you to confirm, and it writes only after you revise. Someone specifically looks at AI's diff, collecting each paragraph against it, sending back unsatisfactory ones on the spot. Do not hand "continue writing" fully to it; let it produce the draft and you collect paragraph by paragraph. You set direction and conclusion, it fills transitions and expansion, so what is written is still your article, not one it published for you.

Copy-paste template (use directly):

```
# Let AI continue writing without derailing (boundaries first, then write)
Please first read what I wrote, then:
1. List an outline of the next three paragraphs for me to confirm
2. Write only after I revise
3. After each paragraph, I collect against the diff, send back unsatisfactory ones on the spot
You set direction and conclusion, it fills transitions and expansion.
```

## 69. Self-media daily posting runs out of material, how to let AI generate 30 topics from old notes?

Daily posting most fears running out of food, but the fragments in your vault are the topic mine. Someone used AI to scan their own vault, gathering scattered ideas into groups of topics.

The method is let AI read your notes from recent months, cluster by theme, like you recorded three fragments about efficiency, two about tools, and it synthesizes for you a topic like "efficiency pits ordinary people most easily step on". Someone uses Smart Connections, and related old notes auto-surface while writing, topic inspiration comes from these surfaces. You screen AI's topics, pick those matching what you want to say now; it can list dozens at once, you pick five or six truly writable. The mine is in your vault, AI helps pan for it, not make up topics from nothing.

Copy-paste template (use directly):

```
# Generate 30 topics from old notes
Please read my notes from the last 3 months, cluster by theme, list 30 topics, each with an angle.
Example: combine 3 efficiency fragments + 2 tool fragments into "efficiency pits ordinary people most easily step on".
I pick 5-6 truly writable, the rest as inspiration pool.
```

## 70. Reading papers / reports, how to let AI summarize and auto-link to my existing notes?

Someone reading academic literature uses local AI for summary, then asks it to find associations against their own vault. The biggest fear reading a pile of papers is scattering after recording; AI helps connect the newly read with the already recorded.

The method is throw the paper to AI, let it first produce a structured summary, then require it to point out which old notes of yours this relates to, like a similar method or opposite conclusion you recorded before. Someone doing academic research specifically uses AI to string literature with their own thinking, not close after reading. This way a newly read paper is not an island, it auto-hangs into your existing network, and later when you ask related questions AI pulls it out together. At least occasionally revisit the original of summaries, do not fully trust its induction.

Copy-paste template (use directly):

```
# Read paper and auto-link to my old notes
Please read this paper: 1. produce structured summary (problem / method / conclusion / limitation)
2. point out which old notes of mine it relates to (similar method or opposite conclusion)
3. link the related parts back to my notes with links, let it hang into the existing network
I occasionally revisit the original of summaries, will not fully trust your induction.
```

## 71. Researcher: how to use local AI to read literature closely without leakage?

Researchers' literature is often confidential or confidential-level, throwing to cloud AI is risky. Someone runs close reading with a local model, data never leaves the computer.

Running an open-source model locally, reading literature, summarizing, extracting viewpoints all completed on your machine, no platform registration, no data transfer. The cost is hardware, answers slower than cloud, but enough for personal literature close reading. Someone uses a local encrypted vault for sensitive material, then lets local AI read, double insurance. Key sensitive content does not go cloud; local model plus local encryption, hold this line and close reading has no leakage worry. Insufficient hardware, reduce model scale, do not send secrets out for speed.

Copy-paste template (use directly):

```
# Local close reading without leakage (data never leaves machine)
1. Install Ollama, pull a 7B-level local model: ollama pull qwen2.5:7b
2. In Copilot fill Base URL http://localhost:11434/v1, no cloud key
3. Sensitive material first in Cryptomator encrypted vault, then let local AI read
Double insurance: local model + local encryption, secrets do not leave computer.
```

## 72. Workplace: how to let AI sink meeting records into retrievable action items?

Someone after a meeting, throws the recording or notes to AI, lets it organize into minutes with action items, retrievable by keyword later. The biggest fear of meetings is scattering after, no one follows action items.

The method is quickly note key points during the meeting, after the meeting let AI generate structured minutes based on your record: who, what discussed, conclusion, who does what by when. You review and make the vague concrete, then store in vault, tagging project and time. Someone uses an AI agent to sink knowledge into retrievable things, meeting minutes a typical scenario. Later you ask "are all action items on project X last month done", AI pulls the answer from your minutes. You write real key points first, AI responsible for categorizing and timing, do not let it fabricate who said what.

Copy-paste template (use directly):

```
## Attendees
## Topics
## Discussion and conclusion
## Action items
- [ ] who does what / deadline
```

## 73. Too much client / project material, how does AI surface the right one when I need it?

Someone manages dozens of clients, material scattered everywhere, never found when needed. Using a tool like Smart Connections, when you write a client proposal, related old material auto-surfaces beside you.

It embeds your client notes; when you write proposal A, it lists in the sidebar the A-client preferences you recorded before, the pitfall of last communication, the playbook of similar projects. Someone migrating from another tool, after dropping the pursuit of perfect structure, felt relieved, because surfacing is faster than flipping folders. The premise is the material itself has content and connections; an empty vault has nothing to surface. While you write it hands the right one to your side, no more flipping the whole vault.

## 74. Writing proposals / reports, how to let AI draft based on my historical material without making up?

Someone writing a proposal feeds all notes of similar past projects, meeting minutes, client preferences to AI, lets it draft the first draft based on these. The root of making up is AI not asked to account for sources, this applies here too.

Let AI cite which historical material it used when drafting, you can check at a glance. Someone uses an AI agent to sink knowledge into retrievable assets, calling historical conclusions directly when writing reports, no rewrite. The more real material you give, the closer the draft; you revise phrasing and priority against it. In the proposal, judgments like "why choose this direction" you make; AI responsible for laying out the evidence you recorded, connecting into a draft. Historical material is yours, the draft is its help, the final is still yours.

Copy-paste template (use directly):

```
# Draft proposal based on historical material (require sources)
Please draft [proposal name] first draft based on the historical material I provide (project notes / meeting minutes / client preferences),
note which of my materials each paragraph uses, for my checking.
Leave judgments like "why choose this direction" empty for me to fill, you only lay out evidence and draft.
```

## 75. Legal / medical and other sensitive industries, how to use AI without stepping on compliance red lines?

Once sensitive-industry data leaks out it is an accident. Someone uses a local encrypted vault for material, then lets local AI read, data never leaves the machine, most stable on compliance.

Key points: sensitive content never goes cloud, use local model plus local encryption; the vault connecting AI has an attack surface, minimum permission plus manual review is the bottom line; credentials opened with a dedicated email sub-account, rotated regularly, never into the vault. Someone took apart an attack surface, saying the vulnerability is not just the content itself, but untrusted content stacked with outbound channel. So for sensitive industries using AI, localization plus encryption plus permission control, the three-piece set, none dispensable, rather slow than step on the red line.

Copy-paste template (use directly):

```
# Sensitive-industry AI compliance three-piece set (none dispensable)
1. Localization: sensitive content goes local model, never to cloud
2. Encryption: material in Cryptomator encrypted vault, protected even at rest
3. Permission: the vault connecting AI minimum permission + manual review, key opened with dedicated email sub-account, rotated regularly
Rather slow, do not let secrets leave the machine.
```

## 76. Doing review: how to let AI synthesize "what I grew this year" from a year of notes?

Someone at year-end uses AI to scan a whole year of diary and project notes, letting it synthesize a growth review. A year's scattered fragments are tiring to string manually; AI helps gather.

The method is give it this year's periodic notes and project records, require it to distill by timeline what you did, where you got stuck, what progressed, and cite specific notes. The "biggest gain this week" "three things next week" you recorded with the weekly review template become ready raw material by year-end. Someone switched from pursuing perfect structure to dropping real ideas into the inbox every day, and over a year the vault is your time archive. AI synthesizes the draft, which counts as growth you decide, it does not make conclusions for you.

Copy-paste template (use directly):

```
## What did I complete this week
## Biggest gain this week
## What did not go well
## Top 3 things next week
```

## 77. Reading blogger: how to use AI to turn book excerpts into citable knowledge cards?

Reading bloggers most fear excerpting a pile but unable to use. Someone uses templates to structure each book's notes, then lets AI help distill into citable knowledge cards.

The method is after finishing each book, record with the reading-note template: one-sentence summary, core viewpoint, inspiration and action, golden-quote excerpt, frontmatter marking book author. Let AI generate knowledge cards one by one based on these, one card one concept, plain-language explanation plus example plus association. You review and fix inaccuracies, the cards can be posted directly. Someone specifically does one-concept-one-card knowledge cards, with links to related topics, and these cards are bricks when writing long articles later. The cards come from books you read, excerpts you recorded, AI helps shape them, not read the book for you.

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

## 78. Learning a foreign language: how to let AI do contextual practice based on my notes?

Learning a foreign language most fears practice disconnected from what you recorded. Someone feeds their foreign-language notes, example sentences, wrong-word lists to AI, lets it generate contextual questions based on these, not a generic question bank.

The method is let AI read your recorded notes, pick the key sentences and error-prone points you marked, generate a contextual dialogue or short essay question, you practice and it gives feedback based on your notes. The questions stick to the words and grammar you really recorded, you practice your weak points, not generic textbook questions. Someone doing academic research uses a similar approach, practicing based on their own material. Your notes are the question source, AI responsible for deforming practice by your thread, you responsible for practicing and correcting. Do not let it produce content not in your vault, that would deviate from your weak points.

## 79. Startup / side hustle: how to use vault+AI to manage ideas, not lose inspiration?

Startup ideas come in fragments, lose one and there is one less. Someone uses a capture plugin, inspiration flashes into the inbox, then lets AI categorize and connect periodically.

The method is any idea first one-click into the vault's inbox, not pursuing perfection on the spot. After a while let AI scan the inbox, gather similar ideas, mark which already done, which worth digging. Someone migrating from another tool made dropping the pursuit of perfection their first move; idea capture same, collect first then sort. Your ideas scattered in the vault, AI helps weave them into a net, you make trade-offs and push forward. The premise of not losing inspiration is collecting diligently; AI only gathers afterward, which one worth doing is still your call.

Copy-paste template (use directly):

```
## Inspiration inbox
- [ ] Idea: ___  | Source: ___  | Date: ___
- [ ] Idea: ___  | Source: ___  | Date: ___

# Periodically let AI scan this list, gather similar ideas, mark worth digging
```

## 80. Content repeats itself? How to let AI hint "you wrote a similar view three years ago"?

Someone writing always circles back to the same view, thinking it fresh. Using a tool like Smart Connections, while writing it surfaces related old notes, you see at a glance you wrote similar three years ago.

It does retrieval along links and semantics; while you write a paragraph, the sidebar lists similar ideas you recorded before, including those you long forgot. Someone reviewing three years of notes said the premise of linking is first thinking clearly about the relationship, AI surfacing same, link accurately then it reminds accurately. Before writing let it scan related old notes; repeated views it marks directly; you either change angle or cite what you wrote before, no pretending first discovery. This feature helps you say fewer wheel-rotating words, also helps you see how your thinking changed.

## 81. Cross-department collaboration material scattered, can personal vault+AI fill in? Where is the boundary?

Cross-department material scattered in everyone's hands, personal vault can fill part, but the boundary must be clear. Someone uses AI to sink their own material into retrievable assets, when needing cross-department info first search their own vault, ask people if not found.

What fills in is your personal accumulation, like project notes and meeting minutes you handled, AI helps quickly pull out. The boundary is permission and privacy; you should not store others' material in your vault, sensitive content does not go cloud, what the team should share goes through team tools not into personal vault. Someone uses an AI agent to sink knowledge into retrievable things, but that is personal, not team's. Personal vault plus AI keeps your own material untidy; cross-department collaboration still must be where there is permission.

## 82. A real workflow demo: from collecting to producing, where does AI work for me?

Someone ran the whole flow: see something good first drop into inbox, not pursuing digestion on the spot; periodically let AI gather inbox fragments, mark sources, link to corresponding topics; while writing AI surfaces related old notes; while drafting AI produces draft based on your historical material; you make judgment and trade-offs, finalize and send.

The steps AI works: categorize, mark sources, surface, produce draft. The steps you work: drop real ideas, review AI's categorization, set direction and conclusion, revise final. Someone used the LLM Wiki approach, AI responsible for compiling raw into wiki and maintaining the master index, he responsible for thinking and writing. In the whole flow AI is the hand of moving and summarizing; the thinking part is always your own. The distance from collecting to producing is saved by AI doing those manual labors for you.

Copy-paste template (use directly):

```
# Complete workflow: from collecting to producing
## You do
1. Drop three lines into inbox (background / conclusion / next step, see Q1)
2. Review AI categorization, set direction and conclusion, revise final
## AI does
3. Gather: read raw/ compile into wiki/, generate source pages, update index.md
4. Surface: Smart Connections lists related old notes while writing
5. Draft: based on wiki/ produce draft and cite sources

# Gather prompt (LLM Wiki compile approach)
Please read new material in raw/ compile into wiki/: 1. generate source-summary page per material keep source_url
2. extract concepts update wiki/concepts/ 3. update wiki/index.md
# Draft prompt (LLM Wiki QA approach)
Please first read wiki/index.md, draft [topic] first draft based on wiki/, cite specific source page per point.
```
