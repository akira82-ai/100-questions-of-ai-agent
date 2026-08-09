# Chapter 2 · Practical Daily-Note Tactics

You have probably had this experience: you took hundreds of notes, but when you really need them not one can be retrieved. This chapter is not about AI; it explains the act of taking notes thoroughly. Only then can AI read your vault, and the premise is that the notes themselves have structure, not a pile of copy-pasted fragments. What you record has structure and connections, so that what AI answers based on it later is rooted.

## 15. I took 800 notes and never use them. What counts as "usable"?

Someone reviewing their note library said the most valuable part was actually the casual fragments jotted down, not the elaborate structure built later. Yet others found their vault slowly turned into a junk pile, impossible to restart. Taking notes without using them, the problem is usually in how you take them.

Storing without processing, the things piled in your bookmarks slowly lose value, and before long you cannot even be bothered to open them. A truly usable way to take notes is each one carries a bit of your own processing, like why you noted it, what it relates to among what you already know. Someone migrating from another tool made throwing away the pursuit of perfect structure their first move, switching to dropping real ideas into the inbox every day. When you take notes, write one extra sentence: this relates to that project of mine before, so AI has a thread to connect when it reads here later.

## 16. Others link like crazy, but when I link it gets messier. Where is the problem?

You see others' dense links and think it is advanced, but when you link it gets messier. The problem is not the links themselves, but how you link.

Links are for things used from different angles, like a concept that connects both to this reading note and to that project. Someone installed a plugin that auto-completes links, which smartly suggests vault titles while typing, and ended up linking unrelated notes on impulse, the noise in the vault growing. Someone else reviewing three years of notes said the premise of linking is you first think clearly about what relationship the two notes have; forcing links only turns the graph into a tangle.

Before linking, ask: will I jump from the same note to both of these later? If yes, link. Link few but accurate, better than many but messy.

## 17. What is an MOC, and why is it better suited to the AI era than folders?

MOC is Map of Content, a directory page that gathers same-topic notes. Say you have a writing topic; build an MOC and list the related reading notes, project reviews, and inspirations all with links.

Someone switched from pursuing a perfect folder tree to using MOCs to gather same-topic notes, and felt relieved. Folders suit clear-boundary things that will not belong to A today and B tomorrow; MOCs suit content that crosses over repeatedly, they do not move files, only surface the relationships. This matters more in the AI era: when AI reads your vault, the MOC is ready-made navigation, telling it which notes are a group, more efficient than digging through folders layer by layer. One MOC is a map, saving both you and the AI that will read your vault later.

Copy-paste template (use directly):

```
# An MOC skeleton (copy and fill)
# Writing Topic MOC
- [[Reading Note: Book Title]]
- [[Project Review: XX]]
- [[Inspiration: XX]]
## Resources
- [[Related Concept A]]
- [[Related Concept B]]
```

## 18. How do I tag without abusing it? Three counter-examples

Too many tags equals no tags; searching returns a pile of same-named tags and it gets messier. Three common counter-examples: one, emotional tags like important, to-read, where everyone is important means nothing is marked; two, dating by tags, which should go to the filename not tags; three, five or six tags per note, so the same concept scatters across a dozen tags.

Someone uses Dataview to query notes as a database, on the premise that tags are clean. The right approach is tags represent a stable category, like reading notes, projects, not one-off states. Few but accurate tags, AI and you can search with the same vocabulary, later querying all reading notes in one sentence, no missing due to tag sprawl.

## 19. Should I learn templates (Templater)? Just copy these 3 and you are set

Hearing "template engine" gives you a headache, feels Geek-only. Actually a plugin like Templater, a beginner just needs to copy the three most common templates, no need to understand the principle.

One is a diary template, auto-filling today's date and weekday on new note; one is a reading-note template, fixing columns of one-sentence summary, core viewpoint, inspiration and action, so every book follows this; one is a meeting-notes template, auto-splitting attendees, topics, action items. Someone reviewing years of notes said their biggest relief was establishing fixed templates back then, otherwise the same format would be hand-typed hundreds of times. Install Templater first, set the template folder, copy these three in, and daily recording is immediately tidy.

Copy-paste template (use directly):

```
# <% tp.date.now("YYYY-MM-DD") %> Diary
> Today is <% tp.date.now("dddd") %>.
## What happened today
## What I learned today
## What to do tomorrow
- [ ]
```

Config: Settings → Templater → Template folder location fill "Templates"; after creating a note press Ctrl/Cmd+P → Templater: Insert template.

## 20. How long should one note be? Too long and AI cannot read it either?

Someone migrating from another note app valued most being able to write short. How long a note should be depends on whether it covers one thing or several.

One note one concept is most stable, like a knowledge card explaining one concept in plain language plus an example plus related concepts. This way when AI reads, the granularity is fine and it can quote precisely, not lost in a five-thousand-word mishmash. Someone else, after managing several vaults, understood that instead of long writing, break big topics into multiple interlinked small notes, each retrievable independently.

The rule in one sentence: one note covers one main proposition, stop when done. Too long and AI cannot read it either, and you yourself may not want to revisit. Short but accurate notes are the good raw material of the AI era.

## 21. How do I turn links into an AI-usable "knowledge graph" instead of noise?

Linked right, AI reads your vault like walking a map; linked wrong, it is scattered fragments. The key is linking with reason.

There is discussion breaking this retrieval into three steps, one point being impulsively added links should be down-weighted, truly repeatedly referenced ones promoted. This matches human experience: links you carefully made often represent real relationships, AI following them can dig out hidden connections; randomly linked ones turn the graph into noise. Someone else used an auto-complete plugin and ended up linking a bunch of unrelated ones, the vault getting messier with use.

So think clearly about the relationship before linking, let links become retrievable real associations, then you see the value when AI uses them.

Copy-paste template (use directly):

```
# Ask before linking (careful links promoted, impulsive links down-weighted)
- Will I jump from the same note to both of these later? Link only if yes
- Is this link a real relationship, or noise from the auto-complete plugin?
- Truly repeatedly referenced links get auto-promoted in AI retrieval; impulsive links down-weighted
```

## 22. Daily stream-of-consciousness logging, how to avoid turning into a junk pile?

Logging a daily stream, piled over time, easily becomes a junk pile, impossible to restart. Someone went through a vault turning to junk and had to start over.

Stream logging itself is not wrong; the wrong part is leaving it there unmanaged after writing. The method is give each day a light structure: what I did today, what I learned, what to do tomorrow, three columns are enough. Someone uses a capture plugin to send fragments to a designated note with one click, not letting inspiration scatter. Someone else reviewing said the key is not how much you record, but spending a minute each day categorizing the day's records and linking one related old note. Stream plus a little light processing will not rot at the bottom of the warehouse, and when AI reads here later there is a thread to follow.

## 23. How to take reading/article notes so it is not "copy-paste then gather dust"?

Reading and articles most easily become copy-paste then gather dust, a whole passage excerpted, never opened again. The problem is only the original was stored, not your processing.

Someone uses a fixed template for reading notes, every book filling columns of one-sentence summary, core viewpoint, inspiration and action, golden-quote excerpt, forcing themselves to write one sentence of their own. Others found knowledge management that truly helps is making what you recorded retrievable and reusable, not dropping it in a drawer. After excerpting a sentence, write offhand this relates to that project of mine last month, and this note comes alive; later when AI answers based on it, your thinking is inside, not dry original text.

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

## 24. What is frontmatter (YAML header) for, and why does AI especially like it?

Someone specifically uses frontmatter to add a structured header to each note, finding AI especially likes it during retrieval. Frontmatter is the metadata block wrapped in three dashes at the top of a note, like book, author, tags, date.

Its benefit is machine-readable. You write one Dataview query and it lists all notes tagged reading-note, sorted by finish date, into a table; AI can also precisely filter by these fields instead of guessing from full text. Someone migrating from another tool made adding frontmatter their first move, because without this layer of structure, more notes are just a text pile.

So add a few stable fields to every important note: tags, date, type. Later when AI asks which books you read this year, it pulls straight from frontmatter, no guessing note by note.

Copy-paste template (use directly):

```
---
tags: reading-note
book:
author:
rating:
date-finished:
---
```

## 25. Using AI to help me write notes, will it make me stop thinking?

Someone only realized after angrily deleting their so-called second brain that what it ignored was your existing accumulation; it only saw the present moment you fed in. Others pointed out even the smartest AI will not proactively connect this chat with what you wrote before.

Using AI to write notes does have a trap: the smoother it gives, the easier you stop thinking, directly treating its output as finished. Cognitively this is called the illusion of competence; you think you mastered it, but actually only read what AI wrote. The guardrail is simple: what AI gives is always a draft; rewrite it in your own words, link one related old note, then it truly enters your vault. Let it write for you, not think for you. Hold this line and the notes are yours, not its.

## 26. How to store meeting/interview records so AI can find them later?

Meeting and interview records most easily get stored as one long blob, and later when you want to find who promised what you dig for ages. Someone uses a fixed template, each session splitting attendees, topics, discussion and conclusion, action items.

The key is action items listed separately, each with who does what and a deadline. This way later when AI reads your vault it can directly pull up the plan Zhang should submit from last week's meeting, instead of you digging from full text. Someone else found tagging a few labels while recording, project name, client name, locates that meeting in one sentence during search. Spend two extra minutes structuring at storage, save ten times the search time later for both AI and you.

Copy-paste template (use directly):

```
## Attendees
## Topics
## Discussion and conclusion
## Action items
- [ ] who does what / deadline
```

## 27. How do images, screenshots, PDFs enter the vault without becoming disconnected?

Images, screenshots, PDFs most easily become disconnected in the vault, stored but with no relation to text notes, impossible to remember to use later.

Someone uses an import plugin to bring material from Word, Notion, EverNote directly into the vault, keeping original structure and not losing links. Others use an image-viewing plugin to zoom images full-screen for detail. The key is do not just throw attachments into an island folder and call it done; write one sentence next to each image, each PDF, what it says and which note it relates to, link back with a link. This way when AI reads your project note, it can bring in the screenshots and PDFs inside, the material becomes connected, not loose sand.

## 28. What is a dumb-but-stable method for naming and directories?

Someone migrating from another note app was most relieved they used the dumb method back then: numeric prefixes for fixed ordering, folders no more than two levels.

Numeric prefixes like 00-Inbox, 01-Diary, 03-Projects, the system sorts by number, you do not need to remember order. Folders only two levels, deeper use MOC and links, not a bunch of nesting. Someone else, after managing several vaults, understood one handy vault beats ten pretty ones, the simpler the structure the easier to stick with. For naming, diary by year-month-day, project by project name plus status, you know at a glance what it is. The dumb method is not fancy, but three years later you can still find things in a second.

Copy-paste template (use directly):

```
my-vault/
├── 00-Inbox/      # temporary material, to be sorted
├── 01-Diary/        # auto-named by YYYY-MM-DD
├── 02-Weekly/        # YYYY-Www
├── 03-Projects/        # PARA Projects
├── 04-Areas/        # PARA Areas
├── 05-Resources/        # PARA Resources
│   ├── reading-notes/
│   ├── knowledge-cards/
│   └── learning/
├── 06-Archive/        # PARA Archives
├── 99-Attachments/        # images, PDFs, etc.
└── Templates/           # note templates of all kinds
```

## 29. What exactly should a diary record to become AI's future "context"?

A diary most easily becomes a stream of what I ate today, and half a year later you do not want to read it yourself. But someone reviewing years of notes said the most valuable was exactly the casual fragments, including the real thoughts in diaries.

To make the diary AI's future context, record the three columns of what happened today, what I learned, what to do tomorrow, plus a sentence of your current judgment and mood. Someone uses a periodic-notes plugin with calendar, weekly and monthly notes auto-generated. These real records accumulate, and when AI reads your vault later it can piece together the you across time from the diary, not just cold documents. The more honestly you write, the more AI understands you, and the answers can catch your thread.

Copy-paste template (use directly):

```
## What I did today
## What I learned today
## What to do tomorrow
- [ ]
```

## 30. My notes are too scattered, AI answers by piecing things together randomly. What to do?

Someone takes notes across tools, and the material fragments like drowning, AI answers by piecing randomly because the bottom is simply not connected.

The root of scattering is notes scattered in different places with no links to each other. First gather into the same vault, then use links and MOCs to string same topics. Someone migrating from another tool made dropping the perfect folder tree their first move, switching to MOC aggregation. Others found adding stable frontmatter to each note, tags, type, date, lets AI retrieve precisely instead of guessing from full text. A scattered vault is not scary; what is scary is not connecting. Once connected, AI's answer walks a map, not picking fragments off the floor.
