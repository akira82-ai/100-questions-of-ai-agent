# Chapter 4 - Write Instructions That Get Heard

> This is the most copyable chapter in the book: all 18 questions are hands-on — CLAUDE.md's line-count red line, whose rule wins on conflict, where to place cache breakpoints, how to control formatting now that prefill is banned. Every prompt technique readers asked for lives here. Each question ends with something you can paste directly; read with your editor open.

## 055. How many lines should CLAUDE.md have — and what happens past the limit?

A hard number: keep a single file under 200 lines. Nothing errors past that, but the longer the file, the more context it eats and the lower the adherence — your rules start discounting from line 200 onward, and past 4 MiB Claude Code skips the file entirely without loading a word (as of 2026-09-07). Splitting with `@import` doesn't help: imported files still enter the window in full at startup — you've moved content from file A to file B and the bill is unchanged.

Copyable template (paste as-is):

```bash
# Line-count red line: under 200 lines
wc -l CLAUDE.md CLAUDE.local.md
# Size red line: past 4 MiB the whole file is skipped
ls -lh CLAUDE.md
# Health check: auto-proposes deleting what's derivable from code (v2.1.206+)
# Run /doctor in a session
```

Past the limit there are two legitimate roads. One: move content into `.claude/rules/` with a `paths` header so it loads only when matching files are involved — an API spec that applies only to `src/api/**`, for instance. Two: cut — directory structure, dependency lists, anything the model can derive from reading the code, all of it goes. `/doctor`'s pruning logic is exactly this standard: delete the derivable, keep pitfall records, design rationale, and conventions that differ from defaults.

Before writing a line, ask whether it deserves one: build commands, coding conventions, project layout, "always do X" — hard facts that belong in every session are the only things that earn the lines. Keep CLAUDE.md's identity straight: it is context, not enforced configuration. Tokens spent in the window participate in attention allocation; long files dilute signal. Multi-step procedures and rules that matter only to one code area belong in a skill or path-scoped rules instead. In a monorepo, if other teams' CLAUDE.md files keep sweeping in, exclude them by path with `claudeMdExcludes`. One reverse reminder: 200 lines is a ceiling, not a target — compress toward a hundred lines where every line is executable, and only then does adherence get to call itself stable.

1) Claude Code docs, How Claude remembers your project https://code.claude.com/docs/en/memory

2) Claude Code docs, Extend Claude with skills https://code.claude.com/docs/en/skills

## 056. Why do rules written into CLAUDE.md get ignored?

The rule is in CLAUDE.md, black on white, and the model shrugs it off — for two reasons. First, injection position: CLAUDE.md content is delivered as a user message after the system prompt; it isn't in the system prompt at all, so strict compliance can't be promised. Second, conflict handling: when two files give contradictory instructions on the same thing, the model may pick one arbitrarily.

When ignored, troubleshoot in this order — the first two steps clear most false accusations: run `/context` in the session and check the Memory files list for your file; if it's not there, the path or scope is wrong and writing more was never going to land. A verbal "okay" from the model proves nothing — the loaded list is the evidence. Then rewrite vague rules as verifiable concrete actions; contradictory old rules are the second-most-common cause, and pruning stale rules regularly beats piling on new ones. Still ignored? Change the enforcement layer: things that must happen at fixed moments (before every commit, after every file edit) become hooks — shell commands that don't care about the model's mood; pure prohibitions go straight into settings permissions, no model involved; for system-prompt-level weight use `--append-system-prompt`, accepting that every launch carries it. Keep the two channels straight: if you want it to "generally use pnpm," it will file that into auto memory itself; if you want it in CLAUDE.md, say "add this to CLAUDE.md" — don't let rules scatter into notes.

Copyable template:

```text
Vague (easily ignored): keep the code clean.
Concrete: use 2-space indentation; run npm test before committing.
Must fire at a fixed moment: write a PreToolUse hook, not a CLAUDE.md line.
Need system-level weight: --append-system-prompt (for scripted setups).
```

1) Claude Code docs, How Claude remembers your project https://code.claude.com/docs/en/memory

2) Anthropic docs, Prompting best practices https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices

## 057. Between CLAUDE.md, rules, and AGENTS.md — whose rule wins?

The same rule written in two files, and they conflict — who listens to whom? It splits by host. Claude Code concatenates everything without overriding: enterprise policy, user-level `~/.claude/CLAUDE.md`, project-level, then `CLAUDE.local.md` enter context in sequence — closer to the working directory means read later, read later means fresher. Codex layers overrides: starting from global `~/.codex`, down from the repo root, at most one file per directory — deeper position appears later and overrides, everything combined capped at 32 KiB (tunable via `project_doc_max_bytes`). Subagent definitions have their own priority chain: managed settings beat CLI flags, project `.claude/agents/` beats the user directory, plugins last.

| Host | Discovery order (first → last) | Merge rule |
|---|---|---|
| Claude Code | Enterprise → user → project → local | Concatenate, no override; closer reads later |
| Codex | Global → repo root → directories down to cwd | Root-down concatenation; later overrides; one file per directory |
| Subagent defs | Managed → `--agents` → project → user → plugins | Same name, higher priority wins |

To make both hosts read the same rules, don't copy — import: neither reads the other's file by default (Codex ignores CLAUDE.md, Claude Code ignores AGENTS.md), and one line at the top of CLAUDE.md — `@AGENTS.md` — merges the streams. Copyable template:

```markdown
@AGENTS.md

# Claude Code only
Changes under src/billing/ go through plan mode first.
```

After configuring, don't guess — both hosts have acceptance checks: Claude Code runs `/context` to show the Memory files list; Codex asks it to recite current instructions (`codex --ask-for-approval never "Summarize the current instructions."`) and it reads back the loaded files in priority order. Codex also holds a temporary card: an `AGENTS.override.md` in the directory makes the sibling AGENTS.md ignored; delete it to restore — good for trialing different rules without touching the shared file. If the repo already has a rules file under a custom name (say `TEAM_GUIDE.md`), list it in `project_doc_fallback_filenames` and it gets discovered as an instruction file.

1) Claude Code docs, How Claude remembers your project https://code.claude.com/docs/en/memory

2) OpenAI Codex docs, Custom instructions with AGENTS.md https://learn.chatgpt.com/docs/agent-configuration/agents-md

3) Claude Code docs, Create custom subagents https://code.claude.com/docs/en/sub-agents

## 058. In long context, where do critical instructions go so they don't get diluted?

Once twenty-odd pages of material are in the window, where an instruction sits decides how much of it gets heard. For long context (20K tokens and up) the layout rule is explicit: long documents on top, your question last. In tests, putting the query last improved response quality by up to 30%, most visibly on complex multi-document tasks — 30% is the test ceiling, not a guaranteed floor; measure your own scene. Why the two ends? The position mechanics were covered in Question 003: attention is U-shaped — both ends profit, the middle gets skimmed — and the more material, the more instructions parked in the middle get diluted. Restraint applies to the material itself: past twenty documents, adding more returns pocket change, and every additional piece should justify its seat.

Two companion moves compress the dilution further. For multi-document, tag-partition: wrap each source in `<document>` with source metadata so the model knows who said what — the side benefit is traceable citations, halving your fact-checking effort. And quote before answering: have it pull relevant passages into a `<quotes>` tag first, then answer from them — attention gets pinned to relevant passages, and if the extracted quotes don't match the question, the fix is different material, not different phrasing. This layout applies to one scene only — multi-document long context; single-turn short prompts needn't copy it.

Copyable template:

```xml
<documents>
  <document index="1">
    <source>annual_report_2023.pdf</source>
    <document_content>{{full document text}}</document_content>
  </document>
</documents>
First extract the sentences from the documents above that relate to the question, into <quotes>;
then answer only from those quotes: {{your question}}
```

1) Anthropic docs, Prompting best practices https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices

2) Lost in the Middle (arXiv 2307.03172) https://arxiv.org/abs/2307.03172

## 059. Which lines in a system prompt are pure waste, and which are worth their weight in gold?

Wasted lines come in two flavors, conveniently the two extremes. One is brittle-hard: dozens of lines of if-else flow jammed into the system prompt to control every step — it still derails on unseen edge cases, and maintenance is expensive. One is uselessly soft: "You are a helpful assistant" gives the model nothing to decide with but guesses. A third hides better: restating what the model does by default, like "write syntactically correct code" — zero information, full token bill. What this spectrum wants is right altitude: specific enough to steer behavior, flexible enough to absorb variation.

Gold-tier lines look like this: pitfall records (this library's endpoint returns duplicate data), design rationale (why we skipped foreign keys), and any convention that differs from default behavior. The acceptance test runs `/doctor`'s pruning logic in reverse — anything the model can derive from reading the code (directory structure, dependency lists) is filler; what it can't derive is the asset. Treat the system prompt as a continuously tuned parameter too, not a frozen artifact: baseline with a minimal prompt, add one rule per observed failure, retest. A one-second test per line: if I delete this sentence, will the model do something wrong, or just miss a pleasantry? Keep the former, delete the latter.

Copyable template:

```text
Don't write: You are a helpful coding assistant.
Don't write: 40 lines of if-else nailing down every step.
Write: for bug fixes, change the minimal scope and add no dependencies;
run npm test before committing — on failure, stop and report (don't route around it).
```

1) Anthropic engineering blog, Effective context engineering for AI agents https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents

2) JavaGuide context engineering tutorial (2026-08 edition) https://javaguide.cn/ai/agent/context-engineering.html

## 060. Why do old prompts need subtraction when models upgrade?

Old prompts drag new models down because the model got smarter: the old moves turned from targeted medicine into overhead. The throughline of migration advice is subtraction, because old instructions were prescriptions for old models' diseases: older models slacked and wouldn't touch tools, so you wrote harsh commands to force them. The watershed sits at the 4.5/4.6 generation — they're more sensitive to system prompts; the old disease is cured and the harsh medicine becomes an over-trigger lesion.

The subtraction checklist (do as written):

1. Delete the harsh talk — "CRITICAL: You MUST use this tool when…" — the reference treatment downgrades it to a plain "Use this tool when…". New models read system prompts more sensitively; harsh talk just makes them jump to act when they should ask the user.
2. Delete self-check instructions. The latest flagships verify natively; an old prompt's "double-check before finishing" causes over-verification — burning tokens and latency. The disposition is deletion, not rewording.
3. Delete anti-slack phrasing like "be thorough, double-check" — same over-trigger triggers.
4. Manual thinking budgets (`budget_tokens`) return a 400 error outright on post-4.7 models — migrate to the `effort` parameter to control depth.
5. Don't delete everything at once: change one item, run your own eval, confirm no behavior drift, then move to the next. Before deleting, run the old prompt once and note the symptoms — grabbing files, spawning subagents, compulsive self-checks — and delete the matching line, not by feel.

The reverse scenario has a ready fix too: when you need the model more proactive, there's a ready-made `<default_to_action>` snippet to add.

1) Anthropic docs, Prompting best practices · Migration considerations https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices

2) Anthropic engineering blog, Effective context engineering for AI agents https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents

## 061. Prefill is banned — what replaces it for format control?

Requests suddenly returning 400 after a model upgrade is almost always prefill: from the 4.6 generation, stuffing half an assistant reply into the last assistant turn for the model to continue is no longer supported — such requests are rejected outright. Models' instruction-following has gotten strong enough to skip prefill, and the five affected scenarios each have a replacement path — the migration section's own headings are the index: Controlling output formatting, Eliminating preambles, Avoiding bad refusals, Continuations, Context hydration and role consistency. Match yours line by line.

| Prefill's old use | The replacement now |
|---|---|
| Forcing JSON/YAML and other fixed formats | Structured Outputs, or enum fields on a tool |
| Removing "Sure, here's…" preambles | System prompt says no preamble; catch leftovers in post-processing |
| Bypassing needless refusals | Write the request clearly in the user message; no theatrics |
| Continuing a truncated answer | Put the truncated text in the user message; ask it to continue |
| Periodic context-refresh annotations | Move reminders into a user turn, or hand off to compaction |

The first row deserves expansion: Structured Outputs exists precisely to constrain output structure — start by directly requiring schema compliance; new models comply well, and retries as the safety net make it stable. Classification tasks get a cheaper variant: define a tool with an enum field and the "output" becomes a tool call. The de-preamble instruction has a ready template line — "Respond directly without preamble." Continuations, the most common case: paste the truncated text into the user message, state where the previous reply broke off, and ask it to resume from that point.

Know the blast radius too: only prefill on the last assistant turn is banned; assistant messages in middle turns are unchanged — this is API behavior with no gradual rollout. Both Structured Outputs and the prefill ban are as of 2026-09-07 and may shift with versions; re-check before migrating. Close by matching the table row by row: all five old uses have a replacement path; the one thing with no stand-in is stuffing half a reply into the last assistant turn — strike it from the design entirely.

1) Anthropic docs, Prompting best practices · Migrating away from prefilled responses https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices

2) Anthropic docs, Compaction https://platform.claude.com/docs/en/build-with-claude/compaction

## 062. Where do cache breakpoints go so every turn saves money?

Price tags first: cache reads run at 10% of base input price, down to 2.5% on some newer models, and a write costs only 25% extra. But a breakpoint in the wrong spot saves nothing. The core principle is one line: put `cache_control` on the last block whose prefix stays identical across the requests you want to share a cache. Cache writes happen only at breakpoints — where the breakpoint sits is where the prefix hash stops; any block before it changes and the hash collapses, forcing a full recompute next turn.

The classic cautionary tale is the timestamp: a to-the-second clock at the top of the system prompt with the breakpoint at the end means the prefix hash changes every second and you pay full rewrite price forever. Manus's engineering retrospective lists timestamps among the most common face-plants: a one-token difference at the start kills every cache entry after it. Placed right, the effect compounds — which is why it resembles a CPU cache line: hits make everything fly, misses reload line by line.

Copyable template (breakpoint at the end of the system prompt; history append-only):

```json
{
  "model": "claude-sonnet-5",
  "max_tokens": 1024,
  "system": [
    {"type": "text", "text": "Stable system instructions, no timestamps",
     "cache_control": {"type": "ephemeral"}}
  ],
  "messages": [
    {"role": "user", "content": "this turn's new message"}
  ]
}
```

Breakpoints are free, up to 4, and three companion numbers matter. Automatic caching: put one `cache_control` at the request top level and the system places the breakpoint on the last cacheable block, advancing it as the conversation grows — the default for multi-turn; mixed with explicit breakpoints it occupies one of the 4 slots, and a fifth placement errors with a 400. The 20-block lookback: when a breakpoint can't find cache, the system walks back up to 20 positions looking for a prior entry; consecutive tool-call blocks count as one position, so parallel tool calls don't push the last turn out of range. Minimum cacheable length: 512 to 4,096 tokens depending on model — shorter prompts gain nothing from a breakpoint. And don't judge hits by feel: read the response's usage fields (as of 2026-09-07).

1) Anthropic docs, Prompt caching https://platform.claude.com/docs/en/build-with-claude/prompt-caching

2) Manus engineering blog, Context Engineering for AI Agents https://manus.im/blog/Context-Engineering-for-AI-Agents-Lessons-from-Building-Manus

## 063. Why does changing one tool definition invalidate the entire cache?

One word changed in a tool description, and the next turn's bill goes full price — the cache judges by layered prefix, in the order `tools` → `system` → `messages`, and a change at any layer invalidates that layer and everything after it. Tool definitions sit first in line, so touching them is a chain detonation: tool cache, system cache, and message cache all gone — dozens of turns of accumulated prefix wiped overnight.

The invalidation table:

| What you touched | Tool cache | System cache | Message cache |
|---|---|---|---|
| Tool definitions (name/description/params) | Invalidated | Invalidated | Invalidated |
| System prompt, web-search/citations toggles | Unchanged | Invalidated | Invalidated |
| Message content, images added/removed | Unchanged | Unchanged | Invalidated |

Two landmines to add to the table: toggling web search or citations is effectively editing the system prompt — flipping either detonates two layers; changing `tool_choice` also voids the cache, listed alongside image changes; thinking and effort parameters' cache effects vary by model, but the message cache always goes. Concurrency hides a second mine: a cache entry isn't ready until the first response starts, so simultaneous first requests all miss — to eat cache, send one request and release the rest once it starts replying. The biggest victim is the long session — dozens of turns of message cache, reloaded in full because one tool got renamed. The self-defense rule is one line: treat tool definitions as compiled artifacts, frozen for the life of a session; if you must change, accept "change once, detonate once, reload once" — and pick a session gap to do it.

1) Anthropic docs, Prompt caching · What invalidates the cache https://platform.claude.com/docs/en/build-with-claude/prompt-caching

2) Anthropic engineering blog, Writing effective tools for agents https://www.anthropic.com/engineering/writing-tools-for-agents

## 064. How do you lay out multi-turn prompts to collect the full cache dividend?

Manus ranks KV-cache hit rate above every other metric for a production agent: it directly moves both latency and cost. And hit rate is almost entirely decided by layout. The multi-turn layout checklist (do as written):

1. Static content goes first in the fixed order tools → system → messages — this is the program's static segment: resident from process start, untouched for the whole run, where nobody injects temporary variables.
2. Timestamps, random IDs, today's date — anything that changes every request — go at the very end of the message stream, as far from the breakpoint as possible.
3. History stays append-only: no editing old messages, no rebuilding the system mid-conversation, no summarizing old turns in place — everything after the edit point loses its cache; on older models earlier thinking blocks get stripped entirely (Opus 4.5+/Sonnet 4.6+ preserve them by default), and the reasoning chain goes down with them.
4. Mid-conversation instructions go into an appended system message inside messages rather than editing the top-level system field (Fable 5.1-class models support this; Sonnet 5 doesn't — top-level edit, cache detonates, accepted).
5. Keep each turn's additions within 20 blocks and a single breakpoint holds; heavy scenes pushing past 20 blocks per turn should plant a second breakpoint mid-way in advance. Don't count blocks anxiously: consecutive tool-call blocks count as one position, and ordinary conversation rarely approaches the line.
6. Close every turn by reading the three usage fields: `cache_read_input_tokens` high, `cache_creation_input_tokens` near zero, `input_tokens` holding only this turn's increment — that's full dividend.

Manus's two companion disciplines are worth copying too: keep tool calls in their original format — the rhythm itself is part of prefix stability; never compress error traces — the failure scene stays in context exactly as it happened, on the theory that the model corrects itself on failure evidence, with prefix stability as the by-product. And a timing note: the 5-minute TTL counts from the start of the request, so if a response streams for 4 minutes, the next turn has 1 minute left — conversations with long gaps should raise cache TTL to 1 hour; Question 078 does that math.

1) Anthropic docs, Prompt caching https://platform.claude.com/docs/en/build-with-claude/prompt-caching

2) Manus engineering blog, Context Engineering for AI Agents https://manus.im/blog/Context-Engineering-for-AI-Agents-Lessons-from-Building-Manus

## 065. How do you pick examples for the model that earn their token price?

Examples are the most expensive real estate in the window; picking wrong burns all three ways. Three selection criteria: relevant — mirrors your real use case, no toy demos; diverse — covers edge cases with enough variation, or the model learns patterns you never meant to teach; structured — each wrapped in an `<example>` tag, several inside `<examples>`, so the model can tell instruction from demonstration.

Copyable template:

```xml
<examples>
  <example>One real business input + your approved standard output</example>
  <example>Same strategy, different scenario, one more</example>
  <example>Deliberately include one edge case showing the handling</example>
</examples>
```

The field test for "worth it": mask the examples and run again — identical output means they were never used, pure burn; changed output but learned wrong means diversity is short, the most neglected of the three: examples all shaped alike teach the model their surface features as the rule. A good example beats a thousand words of description — use examples as behavior anchors, not as documentation.

Two more savings: uncertain about candidates? Have the model judge them — send the pool, ask it to score relevance and diversity or fill gaps, then finalize by hand; and examples are static content across requests — put them in the cache prefix zone so scaled-up marginal cost still rides the cache discount — that's how caching unlocks example scale. How many, and scaling past 20, is a budget question — Question 021 does that accounting. The closing criterion in one line: relevant, diverse, structured — all three before entering the window; unsure ones face the mask-and-rerun test first, and unchanged output means delete.

1) Anthropic docs, Prompting best practices · Use examples effectively https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices

2) Anthropic engineering blog, Effective context engineering for AI agents https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents

## 066. How do you build a multi-window workflow, and why does it beat one stretched window?

Chapter 1 covered where one stretched window ends: the longer the chat, the dumber it gets. The long-task answer is slicing work across windows, in six moves: window one does scaffolding only (write tests, build the init script); later windows work from the checklist; store tests in structured format (say `tests.json`) and state plainly that deleting tests is unacceptable; prepare tools that let a new window get productive fast (`init.sh` one-shot for server and lint); when context clears, prefer a brand-new window over compaction — the latest models are excellent at recovering state from the local filesystem, but give them an opening move; as the task grows, hand it self-serve verification tools; finally, encourage it to finish the current component before starting the next. Multi-window's essence is outsourcing state recovery to the filesystem, and git is the natural state ledger. Order matters too: the first window builds scaffolding and no business logic — once the frame stands, later windows have a checklist to work from.

The mature version is three-stage: research produces a research doc, plan produces an implementation plan, implement works the plan — research and plan land as files, and the human reviews only documents at two gates. The reasoning is practical: nobody can read two thousand lines of code, but everyone can read two hundred lines of a good plan; reviewing research conclusions and plans carries more leverage per minute than reading code line by line. A budget reference point: keep a single session under 120k input tokens (2026-03 archived figure; a rule of thumb, not a hard standard).

Copyable template (new-window opening move):

```text
Run pwd first; you may only read and write inside this directory.
Read progress.txt, tests.json, and git log, in that order.
Before implementing, run the basic integration tests manually once.
This is a relay window for a long task — finish this component before opening the next.
```

1) Anthropic docs, Prompting best practices · Workflows across multiple context windows https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices

2) HumanLayer, Advanced Context Engineering for Coding Agents https://humanlayer.dev/blog/advanced-context-engineering

3) SitePoint, Context Management for Long-Running Claude Code Sessions https://www.sitepoint.com/claude-code-context-management/

## 067. Why is "show the prompt to a colleague" the best test?

One technique earns the name golden rule, from the be clear and direct principle: hand the prompt to a colleague with zero background on the task and ask them to follow it; if they're confused, the model will be too. The trick works because it swaps the tester: you write and read your own prompt, your brain silently fills in the context you never typed, so the holes never surface; your colleague has no such cache — wherever they stall is exactly where the prompt is thin.

Before handing it over, spend a minute self-checking three things the technique targets: are output format and constraints concrete ("build a dashboard" and "build a feature-complete dashboard" are two different prompts); when steps have dependencies, are they in a numbered list; when you ask for an extra action, is the motive stated — the controlled pair is "never use ellipses" upgraded to "the reply will be read aloud by a voice engine, which can't pronounce ellipses," and the model generalizes from the reason. Once all three pass, hand it over — your colleague's pass is your free eval.

The move travels beyond prompt writing: use it to health-check old prompts after a model upgrade — if the colleague still understands, the expression layer is intact and the remaining failures live in the mechanics, like position and dilution (Question 058).

1) Anthropic docs, Prompting best practices · Be clear and direct https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices

2) Anthropic engineering blog, Effective context engineering for AI agents https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents

## 068. Why does telling the model what NOT to do barely work?

"Don't use markdown," "don't be verbose" — such prohibitions are chronically unreliable. The weakness has a reason: a prohibition says where not to go, never where to go, and the model can only loiter at the edge of the forbidden zone guessing. Production pipelines that need stable formatting fear exactly this instability. The first formatting technique is the reverse: tell the model what to do. A same-topic pair makes it concrete — the negative line ("don't use markdown in your reply") underperforms while the positive one ("your response should be composed of smoothly flowing prose paragraphs") gives the model an executable target picture instantly. A prohibition fences off a wide exclusion zone; a positive instruction lays down one clear runway — the runway is naturally easier to follow.

There's also style matching: a prompt itself full of markdown lists breeds markdown output; rewrite the prompt as plain prose and the markdown in the output drops with it. Whatever you want out, write the prompt in. When rewriting any prohibition, ask: after reading this, does the model know its next action? No — rewrite as a positive instruction. Stating the motive is the prohibition's best partner — the model is smart enough to generalize from a reason into scenarios the rule never covered. Reverse constraints aren't banned outright: heavy format templates do carry "don't use numbered lists" clauses; the key is pairing — positive goal first, prohibition as boundary; prohibitions alone with no direction are the ineffective write.

Copyable template:

```text
Prohibition (weak): don't use markdown in your reply.
Positive (contrast): your reply should be composed of smoothly flowing prose paragraphs.
Style matching: strip markdown from the prompt itself,
and the markdown in the output drops accordingly.
Prohibition with motive (contrast): this reply will be read aloud by a voice engine;
don't use ellipses — it doesn't know how to pronounce them.
```

1) Anthropic docs, Prompting best practices · Control the format of responses https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices

2) Claude Code docs, How Claude remembers your project https://code.claude.com/docs/en/memory

## 069. Your hand-tuned context tests worse than doing nothing — why?

A production configuration with real users pulled 58% memory recall, fell to 38% on retest, and cost twice as much as doing nothing — a measured result bought with several hundred dollars of eval fees (note: percentages come from low-trial runs; absolute values carry noise, the ordering is stable). That production preset stacked three middleware layers: clearing stale tool outputs past five thousand tokens, summarizing old turns above 30k tokens, trimming sources by preference. Each layer alone looked "obviously reasonable"; stacked, they lost to a completely untouched full history. Blind judges rated those answers pretty well — the naked eye can't see the degradation at all. "Looks good" and "didn't lose memory" are two different things, and the whole industry still owes that lesson.

Practitioners keep circling back to the same lesson: don't vibe, eval — the config space is too large to tune by eye, and eyeballs are guaranteed to miss. A hand-tuned context must pass the same gate: same task, same data, run your preset against a do-nothing keep-all group, score only the planted probes (probe method in Question 090), then read the cost curves. The person who tuned that preset was burned by a metric once themselves: a "recall jumped from 50% to 96%" triumph turned out to be a counting artifact — the metric only credited the retrieval tool's hits while everything found via grep was recorded as a miss; once the counting rule was fixed, the conclusion reversed. The conclusion can be counter-intuitive — in the cache era, touching context (especially summarize-and-rewrite-the-prefix moves) is often negative yield.

Copyable template (minimal paired experiment):

```text
1. Fix 20-50 real tasks, plant fact probes
2. Run both arms: your preset vs do-nothing (keep-all)
3. Score probes only; blind the judge to which arm is which
4. Log per-turn cost and hit rate alongside
```

1) louisbouchard.ai, Context Engineering in 2026: Why We Stopped Compacting https://www.louisbouchard.ai/context-engineering-2026/

2) Hacker News discussion of Anthropic's context engineering post (I) https://news.ycombinator.com/item?id=45418251

## 070. Why does a one-line instruction often beat a page of rules?

The thicker the rule stack, the thinner the adherence — Question 055's 200-line red line is one face, Question 060's subtraction migration another; this question is the root: agent building's universal principle is start with the simplest thing that works and add complexity only when needed. On prompts: if one sentence does it, don't write a paragraph. On CLAUDE.md it's the same sentence: the more specific and concise the instruction, the more stable the compliance — specific and concise aren't opposites; verbosity is the enemy. A long rulebook's hidden cost is diluted attention: forty rules share the attention such that no single rule gets the weight it needs to be executed.

The one-line instruction skeleton (copyable template):

```text
You are (role). Please (specific action), then deliver as (deliverable form),
acceptance: (verifiable criterion). Background: (one sentence on why).
```

Filled in: "You are a senior code reviewer. Review only the auth changes in this commit, deliver as a change list with every item pointing to file and line. Background: an expired token slipped through last time." Sixty characters, all five elements present. When you can't compress, run two checks: process steps hiding in the rules move to the workflow (multi-window opening moves in Question 066); domain knowledge hiding in them moves to CLAUDE.md or examples — the prompt keeps only this call's intent. The principle has a boundary: genuinely complex multi-step procedures should stay long — Question 066's opening move runs four lines, but every line works and none makes small talk. The other end of the boundary holds equally: concise is not vague — a one-liner like "keep it tidy" is just as dead, and Question 056's contrastive phrasing remains the floor. Before sending, check the skeleton: role, action, deliverable, acceptance, background — five elements make it a one-line instruction; fill whichever is missing.

1) Anthropic engineering blog, Building effective agents https://www.anthropic.com/engineering/building-effective-agents

2) Anthropic docs, Prompting best practices https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices

## 071. Is "context is the model's memory" actually right?

The line circulates widely, common in Chinese translations and commentary posts (a view popular in the Chinese-speaking community). One name correction first: the metaphor's full original is working memory — the qualifier got lost in circulation, leaving just the vague "memory." As an on-ramp metaphor it earns its keep, but as a design basis it wrecks you — it fuses working memory and disk into one thing.

What the metaphor gets right: context really is immediate, finite, and volatile. The rebuttal is two existing designs. One, Claude Code builds "memory" as two channels: CLAUDE.md holds rules you wrote for the model; auto memory holds notes the model wrote itself (typed user, feedback, project, reference), loaded and unloaded separately — if context were memory, nobody would build a second channel, let alone give it write discipline like "don't record what's derivable from code; don't record what CLAUDE.md already says." Two, Letta's memory blocks build memory as persisted partitions: each block has a label, a limit, lives in a database, and only compiles into context when a request comes in. Memory is external storage; context is the working set loaded at each boot.

So correct the sentence to: context is working memory, memory is external storage, and loading-and-write-back connects them. The action item is a three-way checklist (do as written): what this task needs goes into context; rules that hold across sessions go into CLAUDE.md; cross-session facts and preferences land in external memory files, recalled on demand. Selection detail in Question 024.

1) Addy Osmani, Context Engineering (original long-form; Chinese translations cite from here) https://addyo.substack.com/p/context-engineering-bringing-engineering

2) Claude Code docs, How Claude remembers your project https://code.claude.com/docs/en/memory

3) Letta blog, Memory Blocks https://www.letta.com/blog/memory-blocks/

## 072. Why did Tobi write "can you load context" into performance reviews?

In April 2025, Shopify CEO Tobi Lütke published the internal memo that has since been screenshotted the most, with two provisions in black and white: AI usage would enter the performance and peer-review questionnaire; and before requesting more headcount and resources, teams must demonstrate why AI can't do it. The first provision aims straight at this chapter's theme — learning to prompt and load context gets named as a bona fide skill; his observation was that too many people give up after one unsatisfying prompt, and this skill can only be trained through heavy use.

Why put it in performance reviews? Because loading context is the step most easily skipped inside a company: an individual tries twice, decides it's useless, falls back to the old way, and nobody asks whether it was the prompt, the missing context, or the fact that there was never a second try. Attaching it to reviews forces "can you load context" from personal craft into organizational requirement. The memo's scope is explicit too: everyone, including him and the entire executive team; AI even became a field inside GSD (Shopify's internal project flow) — every GSD project's prototype phase leads with AI exploration. A year later he posted the retrospective: the memo had large internal impact, adoption curves visibly rising, and the once-controversial proposals now look self-evident. One framing note first: this is management narrative, not measured data — claims like "hundredfold output" have drawn standing skepticism, and the top-voted question under the original post remains unanswered.

Borrowed as a team self-review checklist:

```text
1. How many reusable prompt/context assets did you bank this month?
2. Before requesting headcount, did you verify the agent approach actually fails?
3. In peer review, did anyone give you feedback on your context-loading?
```

1) Tobi Lütke's original memo post (X, 2025-04-07) https://x.com/tobi/status/1909251946235437514

2) Tobi Lütke's one-year retrospective post (X, 2026-04-26) https://x.com/tobi/status/2048503798143017382
