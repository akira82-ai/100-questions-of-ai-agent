# Chapter 7 · Pitfalls and Guardrails

The previous six chapters taught you how to build and use. This chapter reverses, specifically about crashes. Not to scare you, but to step on them for you first. Almost everyone has fallen into these pits; the only difference is early or late. The line repeated across the previous six chapters is the negative example here: drop the conversation into your own vault, and AI truly works for you; do not let the vault live for you.

## 93. The 5 pits beginners most easily step on

A beginner, eight out of ten will first install a bunch of plugins, installing whichever looks cool, only to find the vault gets slower and slower, taking seconds to open. Someone moved over a perfect structure from others, folders nested four or five levels, stuck in organizing on day one, not a single note written. Others obsess over links, hard-linking a dozen per note, finally the graph messier than a maze. Most regrettable is the person who accumulated thousands of notes but never links, never reviews; the vault becomes a dead archive, switching tools collapses it entirely, all previous work wasted.

What you should really do is first get one or two minimum notes working, then slowly add. Two plugins are enough, folders no more than two levels, links connect naturally after writing smoothly. Someone else's perfect vault is someone else's, not your starting point.

Copy-paste template (use directly):

```
# Beginner 5-pit checklist (fix if hit)
1. Install a bunch of plugins → first install only 2, add after working
2. Folders nested four or five levels → no more than two levels, use MOC / links if deeper
3. Hard-link a dozen per note → link few but accurate
4. Move over others' perfect structure and organize on day one → first write one or two notes
5. Accumulate thousands but never review → periodic review, do not become dead archive
```

## 94. What happens to those who treat AI as "thinking for you"?

A psychology scholar in education described a phenomenon: the more you outsource thinking to AI, the less deep processing you do, because the brain grows capability by "thinking things through yourself". Someone uses an agent to auto-organize notes, finding the agent executes reliably, but the premise is you first think clearly what you want, it will not figure out the goal for you. Obsidian's founder also said something to the effect of not delegating the act of "understanding".

So AI is to help you think something through more deeply, not to birth the thought for you. Daily let it list outlines, find gaps, pick logic holes for you, you make the conclusion. Slack on this step, the smoother you use it, the faster your thinking muscle atrophies.

## 95. Connected AI but notes messier? How to avoid "AI junkyard"

Someone after connecting AI, mindlessly stuffed every conversation, every summary into the vault, three months later half the vault is AI-generated water goods, their own writing harder to find. The problem is not AI, but you did not set rules for it. AI-generated content goes in a separate folder, apart from human-written notes; only what you have read and revised is allowed into the main vault.

A directly copyable categorization: create an `AI Draft` folder for all AI products, review periodically, useful ones distilled into notes, useless ones deleted. Links only to content you truly read, not AI auto-generated. This way AI is a helper, not a junk maker. Some also use a three-step method of frictionless capture, auto-categorize, and instant retrieval on demand; someone who had piled their vault to the point of abandoning it used this to turn the inbox from ever-accumulating-annoyance into auto-empty, capture, sort, and retrieve all frictionless, the key being automation only handles capture and sort, while the retrieval judgment stays with the human.

## 96. Privacy three-piece set: private data, untrusted content, outbound channel

Local files do not equal safe, because Obsidian is always open, the vault is mostly plaintext most of the time, other programs can read it. To really defend, encrypt sensitive content separately; someone uses Cryptomator to wrap the whole vault, then sync to Nutstore, the cost is phone side more troublesome, free traffic limited. Others use disk-level encryption (BitLocker, Veracrypt) or community encryption plugins for static protection.

Block three things separately: private data with encryption, do not write passwords directly in plain text; do not fully trust AI content, it really makes things up; see the outbound channel clearly, before sending notes to a cloud model think whether this paragraph is worth leaving local. Do not encrypt everything up front; first think clearly who you are afraid of; over-encryption only makes it awkward for yourself. It is also worth learning to give an agent three tiers of folder permissions: private holds diary and trade secrets, completely invisible to the agent; readonly is read-only, like reading excerpts; read+write lets it create and edit. Only let it touch the part you want it to touch, and sensitive content never leaves local.

Copy-paste template (use directly):

```
# Privacy three-piece set (block three things separately)
1. Private data: encrypt sensitive content separately, wrap with Cryptomator then sync; do not write passwords in plain text
2. Untrusted content: do not fully trust AI content, it makes things up, glance before entering vault
3. Outbound channel: before sending to cloud model think whether worth leaving local; key opened with dedicated email sub-account, rotated regularly
```

## 97. Local models are not zero-cost, which "free tutorials" are cheating your hardware

Many tutorials say "local models completely free", half true. The model itself charges nothing, but running it eats GPU and memory. Someone tweaked local AI on an old phone, needing termux wake-lock to keep the machine awake, the actually runnable model very small. On a 16GB Mac, realistically the 7B to 8B parameter-level small models, bigger and it cannot run or is too slow to use.

So the hidden bill of "free" is your hardware. Old computers do not believe "install software and run large models", first see if your VRAM and memory are enough. Not enough, honestly use cloud models pay-as-you-go, or only run the smallest model locally for drafts. Do not, to save API money, turn the computer into a brick.

Copy-paste template (use directly):

```
# Local model hardware tier self-check
- 16GB Mac / 8GB VRAM: realistically run 7B-8B, bigger lags or slows
- Phone CPU only: about 10 tok/s, can run smallest model
- Old computer insufficient VRAM: do not believe "install software run large model", use cloud pay-as-you-go or only run smallest model for drafts
The hidden bill of "free" is your hardware, first see if VRAM and memory are enough.
```

## 98. Don't let conversations go to waste, but "full automation" is the bigger pit

Chatting AI without sinking indeed equals wasted chat, so earlier I taught you to collect conversations into the vault. But there is a deeper pit on the other end: someone pursues "full automation", letting an agent automatically read notes, auto-organize, auto-send summaries daily, themselves completely uninvolved. Result the notes get more automated and refined, the owner more automated and less thinking, finally the vault lives for the owner, the owner long unable to use it.

The balance in one sentence: conversations leave traces, organizing leaves hands. AI-generated things you review before collecting, periodic review you flip yourself. Automation can save you time, cannot make decisions for you. Fail to hold this line, the second brain changes from yours to AI's. The more hands you keep, the more rooted what AI answers based on your accumulation will be in the future. Someone put it plainly: let the agent take over your knowledge base; it sounds convenient, but only after truly letting go did they find it had changed things wrong without them noticing. The guardrails are two: use Git as an undo key so you can roll back if it messes up; run it in a sandbox to prevent it from running wild and deleting. Automation can save you time, but not make decisions for you; fail to hold this line and the second brain goes from yours to AI's.

## 99. The second brain is mythologized, which promises you must never believe

Someone shouts "build a second brain and no need to memorize yourself", others shout "AI automatically thinks for you", such talk just listen. Someone tinkered with a second brain for half a year, finally found it just a high-level logbook, what truly needed still had to be pulled from their own brain. Others, because the tool was too heavy, directly abandoned Obsidian, returning to pen and paper, the reason being more advanced tool does not equal better thinking, infinite editing instead trapped them in perfectionism.

Do not believe "once and for all". The second brain is external memory, supplementing details you cannot remember, not growing a brain for you. It is strong in instant retrieval, not losing across years, weak in not producing insights itself. Put its position right: it is your external hard drive, not your CPU. Also do not believe those who sell full automation as a selling point; an agent taking over the knowledge base sounds advanced, but once you truly let go, often the vault gets more refined while you get less able to use it. It is strong in instant retrieval, weak in not producing insights itself; do not let marketing blur this boundary.

## 100. 3 things understood only after a year of use

First, less is more. Obsidian official itself says "fewer dependencies safer", they even write their own chart library, do not run install scripts, and when you install a bunch of third-party plugins you are actually undoing this safety posture. Plugins enough is enough, more is burden and risk. Second, AI gives drafts, you make trade-offs. The outlines it lists, material it finds are good, but which sentence to cut, which to keep, how to conclude, must be your own; letting anyone do this for you is wasting your own thinking. Third, notes are yours. The benefit of local Markdown is the software dies and the vault remains, leave anytime you want. Tools come and go, what you wrote is what truly stays.
