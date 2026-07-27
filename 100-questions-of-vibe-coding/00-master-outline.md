# 100 Questions on Vibe Coding · Master Outline

> Positioning: the sixth book. This one is meant to break out of the tech bubble. It does not follow the "reference manual" tone of the first five.
> Core promise: **how a non-technical person can actually use AI to build something real, and not crash and burn.**
> Audience (focus on the first four personas): non-technical founders, professionals feeling threatened by AI, small-business owners, product/ops/design people.
> Conversion: none planned for now (the book itself is the IP carrier).

---

## 1 · The four people we focus on, and where they get stuck

| # | Persona | One-liner | The stuck point (what the writing must hit) |
|---|---|---|---|
| 1 | Non-technical founder | "Can what's in my head actually become an app?" | Can't write specs; running does not mean correct; doesn't know security basics until after the fall |
| 2 | Professional threatened by AI | "Will I be replaced?" | Identity anxiety; doesn't know what to learn; can't tell whether "writing code" or "describing systems" is the valuable skill |
| 3 | Small-business owner | "Can I skip hiring programmers and just build internal tools?" | Can't tell demo from production; steps on security landmines; has no acceptance standard |
| 4 | Product / ops / design | "Can I prototype it myself first?" | Stuck between "runs locally" and "goes live"; knows nothing about backend / databases / deployment / security |

**Main spine:** persona 1 (aspiration) pulls, persona 2 (fear) pushes. Personas 3 and 4 are concrete, high-frequency scenes woven through every chapter.
**Word-of-mouth lever:** senior engineers (persona 6, not in the main line but drawn in by the failure / security chapters and likely to share).

---

## 2 · The seven chapters (arranged by reader journey, not by technical module)

| Chapter | Theme | Serves | Questions | Core job |
|---|---|---|---|---|
| 1 | Awareness and positioning: what it is, are you scared | shared start for 1/2/3/4 | 14 | Debunk the hype + face the anxiety + a cold splash (who it's for, who it isn't) |
| 2 | First step: from idea to the first instruction | 1/3/4, the hands-on people | 15 | Zero-base path, tool choice, how to write a requirement |
| 3 | Turn the idea into something that runs | 1/4, the toy-makers | 15 | Break it down, iterate, accept, contain the mess |
| 4 | From runs-locally to live-in-production | 3/4/1 stuck at local to prod | 14 | Deployment / database / backend / API in plain words |
| 5 | Failures and security: the truth behind three disasters a week | the fear anchor for all personas | 16 | Real incidents, security primitives, self-check list |
| 6 | Quality and control: something you can actually rely on | owner 3 / pro 2 / founder 1 | 14 | Testing, tech debt, acceptance standards, when to call a human |
| 7 | Boundaries, roles, and the future | everyone, the close | 12 | Replaced? Your value. Agentic. Who it fits |

**100 questions total.**

---

## 3 · The 100-question list (by chapter)

### Chapter 1 · Awareness and positioning (Q1–Q14)
1. What exactly is vibe coding? Explain it like a human.
2. Who said it first, and why did it suddenly blow up in 2025 (that Karpathy tweet)?
3. Is "talk and it writes programs" real, or just another gimmick?
4. Me and my mom can build apps now? How far can a non-technical person really go?
5. I have a product idea in my head. Can vibe coding make it real?
6. Will programmers be replaced? Conclusion first, reasons after.
7. I'm a junior coder and my company started using AI to write code. What do I do?
8. My boss wants to use AI to skip hiring programmers and save money. Is that sound?
9. What's the difference between vibe coding / AI-assisted programming / agentic?
10. Those "built an app in one hour" posts on Xiaohongshu, real or traps?
11. Can a total beginner actually build something usable, or just toys?
12. "Built it" and "built it right" are two different things. What does that mean?
13. The big platforms (Miaoda / TRAE / Coze) are all doing it. Where's the ordinary person's opening?
14. Who this book is for, who it isn't (the cold splash first).

### Chapter 2 · First step (Q15–Q29)
15. I know zero code. What do I install, where do I click first?
16. How to pick a tool: Cursor / Claude / Miaoda / TRAE / Lovable, which fits me?
17. Heard I need Node, Git. Can a non-technical person dodge that?
18. I don't want to touch the command line. Any pure-chat tool?
19. How do I turn "I want a expense-tracking app" into words AI understands?
20. A requirement for AI vs a requirement for a human, what's different?
21. One-line request vs a good spec, where's the gap?
22. Say it all at once, or build and tweak (the opening posture of iteration)?
23. How do I give the first instruction so it doesn't veer off?
24. It generated a pile of files I can't read. Normal?
25. Can it run locally, and what on earth is "localhost"?
26. A wall of red error text. Copy it to AI, or figure it out myself?
27. Do the tools cost money, how long does free credit last a beginner?
28. Picked the wrong tool / direction, can I switch midway, at what cost?
29. Is there a "minimum hands-on path for non-technical people" to follow?

### Chapter 3 · Turn the idea into something that runs (Q30–Q44)
30. The idea is too big for AI to finish at once, how to split so it doesn't collapse?
31. How do I split "build an e-commerce site" into blocks AI can do step by step and reassemble?
32. Build the UI first or the function first, where does a beginner get stuck if reversed?
33. What I want and what AI built differ, how do I rephrase so it really gets it?
34. Same bug, AI "fixes" it ten times and it's still wrong, getting messier (doom loop), how to break out?
35. How do I judge "this version counts as done", give me a non-feeling rough acceptance standard.
36. Demo runs fine but lags with more data, normal? How to fix?
37. AI's code is total gibberish to me, how will I ever change it, am I held hostage?
38. Project grows, AI starts dropping things and contradicting itself (context rot), how to contain it?
39. How do I make AI "remember" what we decided, not start from zero every time?
40. Multi-turn chat, AI forgot what we said earlier, how to pull it back on track?
41. I want to add a feature, AI says "sure", then it crashes. How to prevent in advance?
42. How do I leave a "manual" for myself so future changes are easy?
43. Prototype's done, how do I show friends and get feedback that's actually useful?
44. People say my UI is ugly, can AI help me make it look good?

### Chapter 4 · From runs-locally to live-in-production (Q45–Q58)
45. Demo runs on my computer, how do I let the whole world access it (deployment in plain words)?
46. Does deployment need a rented server, any free one to test the water?
47. "Live" vs "live and usable", where's the difference, don't lie to yourself?
48. Where does data live, Excel isn't enough anymore (database in plain words)?
49. Users need to register and log in, how to store accounts and passwords safely?
50. What is a backend, why is a UI alone far from enough?
51. Want to plug in payments / maps / SMS, can AI help me connect them?
52. What is an API (interface), why can't you avoid it in real builds?
53. After going live the URL has no little lock (https), is that a problem?
54. Deployment failed, red text says "build error", how does a beginner self-rescue?
55. Can I maintain the live thing alone, how much effort?
56. More users, site slows down, my fault or AI's fault?
57. How do I safely push a local demo online (don't upload the keys)?
58. Before going live, is there a checklist to walk through?

### Chapter 5 · Failures and security (Q59–Q74)
59. Are there real vibe-coding failures, give a few actual ones?
60. Three AI security disasters in one week (Lovable / Vercel / Bitwarden), what happened?
61. Why does nearly half of AI-written code fail security tests?
62. What is "prompt injection", how do hackers ride AI into my system?
63. What are RLS / auth, why not knowing them leaks user data?
64. My thing collects real info, how do I protect user privacy?
65. Someone's keys got leaked online (Moltbook, 1.5 million), how do I avoid that?
66. Will AI secretly call paid APIs I don't want and burn my money?
67. How do I stop AI hardcoding the "admin password" as a backdoor?
68. Before going live, how do I do the most basic security self-check myself?
69. Got hacked / data leaked, what's the first thing to do to stop the loss?
70. What must never be handed to vibe coding (red lines)?
71. Using AI to generate code, any copyright / compliance traps?
72. How do I judge whether an AI tool itself is trustworthy (skip the sketchy ones)?
73. In a security incident, who's liable (legal boundary in plain words)?
74. The "10 security bottom lines" for non-technical people.

### Chapter 6 · Quality and control (Q75–Q88)
75. It keeps throwing bugs, how do I make AI write fewer errors (the 70/30 rule)?
76. What is "testing", how does a non-technical person get AI to write tests first (TDD breaks the bug loop)?
77. What is AI's "tech debt", why does it pile up and bury your future self?
78. How do I make every AI change not break the good parts from before?
79. How do I set rules for AI (CLAUDE.md / ARCHITECTURE.md / Plan-Review loop), plain version?
80. The thing is built, how do I accept it as "good enough" to ship?
81. Boss's view: how to judge if outsourced / AI-delivered work is solid?
82. Team adopted AI, how to manage code quality (for the tech lead)?
83. How to level up from "AI writes, I flail" to "I specify, AI obeys" (5 prompt patterns)?
84. Docs and comments, let AI write or me, how to divide?
85. Project's a mess, is there a generic "clean up the wreckage" procedure?
86. How to control cost (token / quota / time), avoid the "ever-burning quota death spiral"?
87. When should I call a real programmer, don't tough it out until unrecoverable?
88. How to back up, don't lose it all overnight?

### Chapter 7 · Boundaries, roles, and the future (Q89–Q100)
89. Can vibe coding really replace programmers, one more honest answer?
90. For someone who can't code, what becomes their core value?
91. "Describing systems" vs "writing code", which is worth more?
92. How should programmers collaborate with AI to avoid being eliminated (survival guide)?
93. From vibe coding to agentic engineering, how much must ordinary people understand?
94. My small tool grew up, when should "the pros" take over?
95. Which projects fit vibe coding, which must never be touched?
96. Should kids / students still learn programming, or just learn to use AI?
97. What will vibe coding look like a year from now (trend call)?
98. 7 sincere tips for non-technical founders.
99. 7 sincere tips for the threatened professional.
100. Last line: you don't need to code, but you need to think clearly.

---

## 4 · Source mapping (make sure every chapter has real substance, not empty talk)

- Q2 / origin: 001, 007, 010, 012 (Karpathy's date needs verification: Feb / Feb 2 / Feb 6, three claims)
- Q3/4/11/13 feasibility: 009, 013, 014, 016, external search (Xinhua / TMTPost "everyone builds apps")
- Q5 / 30–44 practice: 005, 006, 009, 011, 016 (Lezhi Shiguang, WeChat mini-program cases)
- Q45–58 going live: 004, 007, 016
- Q59–74 security: 004 (7 incidents), 015 (three a week), 007 (45% security pass rate), 065 (Moltbook key leak)
- Q75–88 quality: 005, 006, 010, 012 (tech debt, CLAUDE.md, AI code 1.7x problem rate)
- Q89–100 boundaries: 008, 010, 012, 013, 014

**Conflicts to verify / cite:** Karpathy's date, the "Google Antigravity" in 007 (suspected non-real tool), and the inconsistent security-rate figures (45% / 40–62% / 2.74x). Cite sources line by line when writing the body.

---

## 5 · Writing norms (the sixth book's iteration over books 1–5, must land)

1. **Open each chapter by stating who it's for and what predicament it solves**, then go to the questions.
2. **Don't dodge failure and security:** Chapter 5 is the trust anchor; tell incidents concretely (who, what error, what consequence).
3. **Cut the AI smell, add the human smell:** fewer parallel structures, fewer emojis, more "I've seen a real case".
4. **Plain words first:** backend / API / RLS / deployment all introduced through a human predicament, not by front-loading jargon.
5. **Sliceability upfront:** tag each question with `[Xiaohongshu]` / `[short video]` / `[long read]` while writing, for later breakout.
6. **State boundaries clearly:** Q14, Q70, Q95 pin down "who it's not for, what must not be touched".
7. **Unified answer structure:** each question = one-line direct answer + why + how to get out (actionable).

---

## 6 · Next step

After this outline is confirmed, start writing from **Chapter 1** (14 questions). After each chapter, show it to you before moving to the next.
