# Chapter 4 · Turning Notes into Assets with AI: from storing to using

Notes piled into a mountain still a pile of dust, the problem is not taking them but not using them. This chapter is about how to let AI turn your accumulation into usable things, not another smarter favorites folder. After connecting AI, the real value begins.

## 47. My notes pile into a mountain, how does AI help me "use" them instead of "store"?

Someone reviewing their vault said the most valuable was actually the casual fragments jotted down, yet more found the vault slowly turned into a junk pile, impossible to restart. Storing without processing, the things piled in the inbox slowly lose value, and before long you cannot even be bothered to open them.

The sign of using is simple: when you write, related old notes jump out on their own; when you ask a question, AI answers based on what you recorded before, not making up from zero. Someone uses Smart Connections, and while writing a paragraph it surfaces a few related old notes in the sidebar, that is the feeling of using. Storing just moves things into a warehouse; using is letting the warehouse feed you back. Do not pursue a perfectly organized vault first; let AI read it, even if just dropping real ideas into the inbox every day.

## 48. What is Vault QA, and how to let AI answer based on my accumulation?

Vault QA means using your notes as a knowledge base; when you ask AI a question it reads your vault first then answers. The biggest difference from asking a chatbot directly is the answer comes from your own accumulation, not generated from nothing by the model.

Someone built a vault with the LLM Wiki approach, splitting raw and wiki layers, with a master index.md in wiki. Before asking, let AI read index.md to understand the whole, then answer based on wiki content, and require it to cite specific source pages, and honestly say if the vault has no such info. This way when you ask "what was my conclusion about X last year", it flips through your own notes, not vague talk from the web.

Copy-paste template (use directly):

```
Please first read wiki/index.md to understand the whole, then answer my question based on wiki/ content: [your question]
When answering, cite the specific source page in wiki/; if the knowledge base has no related info, please tell me.
```

## 49. While writing, AI auto-surfaces related old notes, how to turn on this "cheat"?

This cheat is Smart Connections. It embeds your notes so that while you write, related old notes auto-surface beside you, no manual searching.

Someone migrating from another tool made dropping the pursuit of perfect structure their first move, because surfacing while writing is more practical than a perfect folder tree. You are writing a thought about a concept, and it lists three related notes you wrote half a year ago in the sidebar; you can pick up the previous thread at a glance. Its premise is the notes themselves have content and connections; an empty vault has nothing to surface. After installing, open any note and start writing, the sidebar comes alive, that is the cheat.

Copy-paste template (use directly):

```
1. Settings → Community plugins → Browse → search Smart Connections → install and enable
2. First open prompts to generate embedding (for Chinese vault choose Chinese embedding, see Q36)
3. Open any note and start writing, related old notes auto-surface in the right sidebar
4. Link unrelated notes correctly, surfacing quality improves with connections
```

## 50. Will my second brain just be a logbook? How to tell if it really "thinks"?

Someone directly deleted their second brain, saying it was just a mover, moving things from one place to another, not thinking more itself. Others, after using a vault for over five years, reflected that a big vault does not equal thinking. The difference between a logbook and real thinking is processing.

A logbook only records without processing, noting one today and one tomorrow, no connections between them, looking back is a pile of stream. Real thinking is when you make a judgment while recording: these two are related, that note overturned a previous conclusion, and periodically look back. Someone returned from digital tools to paper precisely because they found themselves only hoarding in the digital vault without reading. The criterion is straightforward: are there connections between your notes, have you processed them back, can the old ones be used when you write something new. If all three are empty, then it is indeed just a logbook.

Copy-paste template (use directly):

```
# Is your second brain "thinking" or a "logbook"? Three self-checks
- Are there connections between notes? (MOC / links)
- Have you processed them back? (periodic review, update conclusions)
- Can the old ones be used when writing something new? (AI can answer based on accumulation)
All three empty → just a mover; add processing to count as thinking
```

## 51. AI auto-builds my links/MOC, is that laziness or really useful?

Someone used AI to assist building the vault, auto-generating the master index and concept pages, saving lots of manual linking time. This is not laziness, it is acceleration, on the premise that you reviewed the links it built.

MOC is a map gathering same-topic notes; AI helps you put scattered notes into the corresponding MOC, saving you the manual labor. But whether the links are accurate is up to you; someone installed an auto-complete link plugin and while typing casually linked unrelated notes too, more noise. So let AI build the draft, you do the cutting and editing, faster than pure manual and cleaner than handing it all over. The value of links is in the connection itself; AI just helps spread the connection.

## 52. Let AI periodically review old notes, how to set it without notification hell?

Someone used periodic notes plus a review plugin, but set the frequency too dense, popping notifications daily, and finally just turned it off and never looked again. For reviewing, frequency matters more than intensity.

Use Periodic Notes with calendar, fix a time weekly or monthly to look back, not urging you daily. Someone switched from pursuing perfect structure to dropping real ideas into the inbox every day, and put review on the weekend. You set a minimum frequency you will actually execute, like flipping through the inbox and this week's additions every two weeks, AI helps pull out the related old notes from this period for comparison. Do not let it pop daily; that annoyance makes you abandon the whole system.

Copy-paste template (use directly):

```
# Let AI review periodically (every two weeks, not daily)
Please read my inbox and diary from the last two weeks, pick out old notes related to [current project],
list them with a sentence on how they can be used now. Do not pop notifications daily.

# Companion: Periodic Notes + Calendar
Settings → Community plugins → install Periodic Notes and Calendar → weekly / monthly notes auto-generated
```

## 53. AI helps distill my scattered fragments into a long article?

Fragments scattered everywhere, manually stringing into a long article is tiring. Someone used the LLM Wiki compile approach, letting AI read new material in raw, distill into wiki, generating source-backed concept pages and a master index.

The specific method is give AI a clear instruction: read new material in raw, generate a source-summary page for each and keep source links, extract important concepts to update or create concept pages, finally update the master index. You are not asking it to write viewpoints for you, but to first gather your recorded fragments, mark sources, then you write on top. This way the long article grows from your own accumulation, not made up by AI.

Copy-paste template (use directly):

```
Please read the new material in raw/ and compile it into wiki/.
1. Generate a source-summary page for each material, keep source_url.
2. Extract important concepts, update or create concept pages in wiki/concepts/.
3. Update wiki/index.md master index.
```

## 54. Using AI to organize notes, how to avoid getting messier (AI junkyard)?

Someone confidently let AI organize, only to find the vault not clearer but with an extra layer of AI-generated, sourceless pages, a junk pile on a junk pile. The way to avoid is regular health checks.

Give AI a health-check instruction: read the master index, find which pages lack sources, which concept definitions conflict, which pages are islands with no links, which concepts are repeatedly mentioned but not yet independent pages. Someone specifically uses this check to prevent vault rot. The key is you must let it mark sources, mark islands, then you decide delete or fill. AI organizing is not one-click done, it is rounds of review, each round clarifying sources and connections, so the vault does not get dirtier.

Copy-paste template (use directly):

```
Please read wiki/index.md and do a health check:
1. Which pages lack sources 2. Which concept definitions conflict with each other
3. Which pages are islands with no links 4. Which concepts are mentioned repeatedly but not yet independent pages.
```

## 55. Should I trust everything AI answers? Three ways to spot errors

Someone using Smart Connections found AI occasionally makes up content not in the notes, especially when you ask vaguely. AI answering based on your vault does not mean it does not err; three ways to spot.

First, see if it points to a specific note when answering; vague talk with no source gets a question mark. Second, directly ask it "which sentence in which note did you just cite"; one that truly read your vault can point it out, made-up ones expose themselves. Third, check against facts you clearly know, like you remember noting the opposite conclusion last month but it says no, that is hallucination. AI is an assistant that reads your vault, not an infallible god; your known judgment at the critical moment is the last gate.

Copy-paste template (use directly):

```
# Spot AI hallucination: three follow-up questions (copy and ask)
1. Which sentence in which note did you just cite?
2. Paste that sentence verbatim for me to see
3. I check against known facts: I recorded the opposite conclusion, you say no, explain
Cannot produce a specific source → probably making up, do not adopt
```

## 56. What does "an AI that gets me" rely on, links or the preface I wrote?

Someone adds frontmatter to notes, marking topic, status, relations in the header, and AI filters correctly at retrieval. Others rely on links to weave related notes into a net, AI follows links to find context. Neither is the whole.

Links give structure, telling AI these notes are a group. The preface gives intent, like you write clearly at the top of a note what problem this solves, which project it relates to, so AI reading here knows your purpose of recording it, not just the literal. Someone wrote a CLAUDE.md for the vault, explaining the vault's structure and rules to AI, equivalent to a user manual for AI. Links plus preface plus this manual, then AI truly understands your accumulation; relying on any single one is not enough.

## 57. How to make AI cite my note sources instead of making up?

The root of making up is AI was not asked to account for sources. Someone before asking explicitly instructed: answer based on wiki content, cite specific source pages, honestly say if the vault has none.

This one instruction suppresses hallucination by more than half, because AI knows after answering it must point you to which note, so it dare not fabricate a non-existent note. Someone also lets AI do Lint, reviewing the whole vault to find contradictory pages, conclusions overturned by new material, sourceless orphan pages. Citing sources is not just for your peace of mind, it also forces AI to truly read your vault. Every time you ask, require it to bring sources, it slowly builds the habit, and answers become more accountable.

Copy-paste template (use directly):

```
# Make AI cite sources (add this when Q&A based on vault)
Please answer based on my notes and note which specific paragraph of which note each conclusion comes from;
if the vault has no such info, tell me honestly, do not fabricate sources.

# Periodic Lint: force it to truly read the vault
Review the entire wiki/: find contradictory pages, conclusions overturned by new material,
sourceless orphan pages, give a report and suggest blank concepts worth creating.
```

## 58. My notes are too shallow, even AI cannot save them, how to record so it is "feedable"?

Someone found their notes were all copy-paste excerpts, and AI read around and could not say anything, because there was nothing of their own inside. Too-shallow notes, AI cannot catch.

A feedable way is each note carries a bit of your own processing. Someone uses frontmatter to mark book author rating clearly, then writes one sentence in the body that this relates to that project of mine before. Others reviewed saying the most valuable was exactly the casual fragments with their own judgment. When recording, write one extra sentence why you noted it, what it relates to among what you know; AI reads this sentence and has a thread to connect, and later answers can follow your thinking instead of just repeating excerpts.

## 59. What is the experience of AI using my links, and why is careful linking worth it?

Someone using Smart Connections found AI does not search your vault by keywords, but does graph retrieval along links; the two notes you linked, it defaults as related, pulling them together.

This experience differs from ordinary search. You ask a concept, AI not only finds the title-hit note, but also pulls out the several linked via links, even if those notes never contained the word you asked. Someone migrating from another tool made dropping the pursuit of perfect structure their first move, switching to careful linking, because correctly linked notes make AI's understanding much more accurate. Random linking creates noise, but few but accurate links make AI clearly understand you more; that is why careful linking is worth it.

## 60. AI helps me write weekly reports/summaries, how to not let it think for me, only write for me?

Someone deleted their second brain precisely because they found themselves thinking less and less, handing everything to the tool to summarize. AI writing weekly reports, the boundary must be clear: it writes for you, not thinks for you.

The method is give it your diary, project notes, meeting records, let it draft a weekly report based on these, which things are important, how to phrase, which to expand, you decide. Someone returned from digital to paper precisely to avoid not thinking. So let AI produce the draft, you make the judgment and trade-offs; it saves the typing and summarizing effort, the thinking part must stay with you. In the weekly report, judgments like "biggest gain this week" AI cannot give, you fill them yourself.

Copy-paste template (use directly):

```
# Let AI produce weekly report draft (you decide conclusions)
Please draft a weekly report based on this week's diary, project notes, meeting records:
1. List things advanced this week (grouped by project)
2. Mark key points worth expanding
3. Leave "biggest gain this week" "next week focus" columns empty, I fill them myself
Only write for me, not think for me; conclusions and phrasing decided by me.
```

## 61. Can AI dig out hidden relationships between notes? How?

Yes, and this is where AI beats humans. Someone using local RAG, AI does graph retrieval along links, digging out notes you never manually linked but content-related.

Hidden relationships hide in semantics; you did not realize the two were related when recording, but AI reading the whole vault can compare. Like you noted a pitfall of a project half a year ago, and another similar problem last month; AI placing the two side by side via links and semantics, you see you repeatedly step on the same pit. The premise of digging is notes have substantial content and connection foundation; an empty vault digs little. You periodically let AI do this relationship sorting, easier to bump into those hidden clues than flipping the vault yourself.

## 62. My vault spans years, how does AI understand "the me across time"?

Someone uses diary plus periodic notes, recording every day, week, year, and the vault has a timeline. AI reading these time-fielded notes can piece together your thoughts at different stages.

Mark the date clearly in frontmatter, diary named by day, periodic notes grouped by month and year; AI asking "how is my view of X two years ago different from now" can pull out the notes from both ends along the timeline for comparison. Someone switched from pursuing perfect structure to dropping real ideas into the inbox every day, and over time the vault becomes your own time archive. The me across time relies on continuous recording with time marks, so AI can string the scattered you into a line, not a pile of unordered fragments.

Copy-paste template (use directly):

```
LIST FROM #diary
WHERE file.cday >= date(today) - dur(30 days)
SORT file.cday DESC
```

## 63. Letting AI be my "second brain", how to prevent cognitive atrophy risk?

Someone deleted their second brain, saying they stopped thinking, handing everything to the tool to summarize, and over time could not even be bothered to organize their own thoughts. Cognitive atrophy happens to those who use it well, not those who do not.

Three risks: one, memory atrophy, storing everything in the vault and not memorizing yourself; two, absorption atrophy, only reading AI's summaries not the original; three, illusion of competence, thinking having it in the vault equals understanding. The prevention is not complicated: keep your own writing step, make key judgments yourself, at least occasionally revisit the original of AI's summaries. Someone returned from digital to paper precisely to force themselves to think. The second brain is an add-on, not a replacement; the thinking part cannot be handed out.

Copy-paste template (use directly):

```
# Cognitive atrophy three risks + three defenses
Risks: ① memory atrophy (store but not memorize) ② absorption atrophy (read summaries not originals) ③ illusion of competence (think having = understanding)
Defenses: ① make key judgments yourself ② at least occasionally revisit originals of AI summaries ③ keep your own writing step
Second brain is an add-on, not a replacement; the thinking part is always your own.
```

## 64. AI is not here to remember for you, but to help you think. How does this land in daily life?

Someone treats the vault as a mover, only in not out, and finally cannot be bothered to flip it themselves. To land this sentence, return to the tiny daily actions.

When recording, write one extra sentence of your own judgment, not just copy. When writing, let AI surface related old notes, you do the connecting and trade-offs, not copy verbatim. When asking AI, require it to bring sources, you keep the verification step. For weekly reports it produces the draft, you fill the important conclusions. Someone used the LLM Wiki approach, AI responsible for gathering and marking sources, he responsible for thinking and writing. AI helps activate your accumulation; the thinking part is always your own. Hold this line daily, and the vault is an asset, not another dusty warehouse.
