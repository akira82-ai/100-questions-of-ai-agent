# Graph Engineering · 100 Questions

> Mode: Mode A (reference book, 6 chapters) | Reader: builders with real agent deployment experience who hesitate over "should I adopt graphs?"
> Concept anchor: Graph Engineering = the engineering of orchestrating AI agents (coined by Peter Steinberger, 2026). Not knowledge graphs. Not GraphRAG.

## The Hidden Thread and a Reading Introduction (for readers, and for the writer)

This is not a manual on "how to draw a graph." It is a book of judgment, and its backbone is "anti-hype judgment." The main line runs: the four ways a single loop breaks (ch1) to how graphs break too (ch3) to when to adopt a graph and how to add anchors (ch4). Chapter 2 looks like it is about architecture, but it is really "the vocabulary floor you need to make judgments"; the question of judgment is not confined to chapter 4, it runs through ch1, ch4, and ch6. After reading, you should be able to answer: for my scenario, should I loop, workflow, or graph? The book's memory anchor is "reality anchors." A graph without anchors is just organized nonsense.

---

## I. Foundations and Positioning

1. What is Graph Engineering, really?
2. Why is a graph not just "a loop plus a few nodes"?
3. Everyone says a graph is a superset of a loop. So do we still write loops at all?
4. Why do some people call "loop vs. graph" a false problem? (Side note: you also cannot directly ask an agent whether it is in a loop. Only a mathematical proof works.)
5. Is Graph Engineering just another round of rebranding, fundamentally still a state machine?
6. My agent runs fine on a loop right now. When will that stop being enough?
7. How does Goodhart's trap push a self-improving loop further and further off course?
8. What does "loops fighting each other" mean? Two loops both working normally, yet sabotaging each other?
9. Why does the upward blind spot keep a loop from ever questioning its own goals?
10. What does "broken measurement" mean? What happens when the watcher has no one watching them?
11. How do Prompt, Context, Harness, Loop, and Graph string together into one evolution chain? (Filling the missing Harness Engineering node that the LangGraph blog left out.)
12. Why do people in the field say a graph's reality anchors matter more than the graph itself? Without reality anchors, is a graph just organized nonsense? (Merged with former Q11.)
13. Why does the LangGraph team itself say some tasks should not be crammed into a graph?
14. Terms change every six months. How do I judge whether Graph Engineering is genuinely worth learning?
15. Why did Steinberger's nine-word tweet ("are we still talking loops or did we shift to graphs yet?") trigger a wave of Graph Engineering debate and hit 2.8 million views? What exactly did it hit on? (Origin hook + anti-hype status signal.)

---

## II. Core Architecture and Key Mechanisms

16. Why are a graph's nodes, edges, and state all indispensable?
17. People say a loop is a simple graph. Where exactly is it simple, and what does it lack?
18. DAG or cyclic graph: which should I use? Must a graph be acyclic?
19. Why are production graphs often not DAGs, while textbooks always teach DAGs?
20. How can a deterministic path and an agentic step coexist in the same graph?
21. Why should state be a typed structure instead of being stuffed into the chat log?
22. How do you write conditional edges without degrading them into a pile of nested if-else?
23. When should you use a subgraph to encapsulate an expert's internal flow?
24. What does dynamic dispatch (the Send API) solve that an ordinary edge cannot?
25. Why must state be shared across runs? What lets a graph resume after a restart?
26. Is human approval a node or an edge in a graph? How big is the difference?
27. Who decides which path to take next: the model or me?
28. How do you choose among supervisor, hierarchical, swarm, and fan-out-fan-in topologies?
29. Why does picking the wrong topology often cost more than picking the wrong framework (but don't ignore the long-term cost of framework lock-in)?
30. In principle, what does a graph's recoverability recover: nodes, the whole state, or a layer in between? (Conceptual layer, paired with the operational layer in Q73.)
31. What is the difference between multiple agents sharing a state object versus passing messages to each other?
32. Why can a graph write "who can stop it" and "what counts" into its structure?
33. Can a graph contain both automatic branches and human gates at the same time?
34. State diffs are recorded at every checkpoint. What exactly do you look at when debugging?
35. Why is a graph's boundary harder to define than the graph itself?

---

## III. Pitfalls and Anti-Patterns

36. Why is a 40-agent graph harder to debug than a single loop?
37. What is over-orchestration, and how do I tell if I am graphing for graphing's sake?
38. Why is the pit of losing information when passing context between sub-agents so common?
39. How does a hidden loop make an agent look busy while making no real progress?
40. What is false success, where the final result looks great but the process is already rotten?
41. Where does a retry storm come from? How does one flaky API burn through the whole budget?
42. At which step does token explosion usually spiral out of control?
43. Why does drawing agents along organizational lines almost always fail?
44. Why does a graph loop into self-deception, treating mutual confirmation as truth? And how does a graph without reality anchors efficiently amplify errors? (Merged the "amplify errors" angle from former Q45.)
45. Why is the God agent an anti-pattern? What happens if you cram 50 tools into it?
46. How does silent failure let an agent swallow an exception and pretend nothing happened?
47. What is context poisoning? How does dirty data from upstream hit downstream?
48. Why are multi-agent setups in a linear writing pipeline often less controllable and more troublesome than a single agent, only earning their keep when multi-perspective verification is needed? (Added qualifier to avoid overstatement.)
49. How do I decide whether to add an agent now or first fix the single agent's prompt?
50. If you treat the graph as a silver bullet, what are the three most common costs?
51. Why do some teams spend months building multi-agent systems when fixing the prompt would have been enough?
52. How do you prevent side effects like double charges and duplicate messages in a graph?
53. How do you avoid the pit of binding too tightly to a framework, where switching one means throwing everything away?
54. Why can't you take the "85% cost reduction" that marketing accounts tout at face value? What should you look at?
55. How does tool-output prompt injection hijack an agent and turn a graph into an RCE entry point? Through which surfaces do indirect injections enter via MCP tool descriptions, memory stores, and RAG? (Paired with a vendor's 2026 disclosed real injection-to-RCE vulnerability and the OWASP prompt-injection taxonomy; forms a security line with Q100.)

---

## IV. Verification, Quality, and Advanced Techniques

56. When should you adopt a graph? Is there a checklist you can copy verbatim?
57. How many upgrade signals must you hit before it is truly time to upgrade a loop into a graph?
58. If none of the six signals apply, should I just stay with the loop?
59. How do you add reality anchors so the graph cannot fool itself?
60. If a graph is built wrong and you want to fall back to a loop, what are the obvious fallback signals?
61. How do you test a graph? You can't just test the final answer, right?
62. Why does scoring only the final answer make a false-success system look especially strong?
63. How do you actually implement binding evaluation to real traces?
64. How do you prioritize these three: state exceeding the window, needing to survive crashes, and needing mid-way approval?
65. Are parallel branches and dynamic dispatch the hardest reasons to adopt a graph?
66. Why has replayable audit become a hard requirement for adopting graphs rather than a nice-to-have?
67. Besides money, what hidden costs of graphs does no one mention?
68. How do I prove to my team that adopting a graph is worth it, not just that it sounds advanced?
69. When does a graph actually slow delivery, so you would rather use a workflow first?
70. Is there an anti-pattern in the act of deciding whether to adopt a graph itself?

---

## V. Engineering in Practice and Real Scenarios

71. How do you design a state schema so you don't crash the whole graph every time you change a field?
72. Where should checkpoints go? Should every node be a recovery point?
73. After a crash, what does recovery from a checkpoint restore: the message history or the entire state object? How does it pair with an idempotency key? (Operational layer, paired with the conceptual layer in Q30.)
74. How do you tier human gates? Which steps truly need a human nod?
75. How do you add an idempotency key so ten retries never send the email twice?
76. How do you isolate side effects (sending messages, charging) so the graph doesn't break on a careless rerun?
77. What exactly should observability capture, and why are logs alone not enough?
78. With no trace, how do I debug a graph that went off the rails at 2 a.m.?
79. How do you do cost routing so a simple query never goes to the most expensive model?
80. When a tool call fails, how should you configure backoff, retry, and circuit breaking?
81. What is time-travel debugging, and why does a graph need it more than a loop?
82. When choosing a framework, should you separate the orchestration model from the durability layer?
83. Where exactly do LangGraph, the OpenAI Agents SDK, and ADK differ: in orchestration or in ecosystem?
84. With no one to operate it, where should a small team start with graph productionization?
85. For the scenario in front of me, should I draw the state first or the nodes first?

---

## VI. Boundaries, Alternatives, and Reflections

86. Is Graph Engineering actually new? State machines and workflow engines have existed for ages. Why does the "rebranding" narrative keep recurring, and what is its real impact on what we learn today? (Merged former Q86 + Q95, separating "true/false judgment" from "rebranding stakes".)
87. What do you look at in a framework comparison, and why can't star counts and download numbers be gospel?
88. What is the durability axis (grounded vs. ungrounded), and why does it matter more than the framework?
89. What is the relationship between graphs and Context Engineering? Are they two sides of the same thing?
90. Why do people in the field say the next buzzword will come sooner or later? Is that normal?
91. In which scenarios should I clearly not adopt a graph, where using one makes things worse?
92. Who is CrewAI's role-based crew for, and who is LangGraph's graph for?
93. Why is a durable execution layer like Temporal often placed underneath a graph?
94. Open-source frameworks vs. managed runtimes: how do you choose based on your team's operational capacity?
95. For a one-person company or small team, which parts of a graph can start in their simplest version?
96. Why is the "40-agent department-style graph" a textbook anti-pattern (see Q43), not a big-tech production paradigm? What pitfalls do you hit if you take "draw agents by org chart" seriously? (Removed the unsourced "big tech doesn't use it" claim; reframed as an anti-pattern caution.)
97. When learning Graph Engineering, which marketing phrases should you be most wary of?
98. If a new buzzword replaces it next year, is what I'm learning about graphs still worth it?
99. Looking back at steipete's tweet, what did Graph Engineering actually leave behind?
100. A graph's trust boundary: when cross-node authorization is not propagated cleanly (authorization confusion), how do you achieve fail-closed? (Paired with a real prefactor support-bot scam-refund case; forms an "authorization trilogy" with Q66 replayable audit and Q32 who-can-stop-it.)

---

## Propagation Boosters (executed during writing, not counted in the 100)

The following assets are embedded while writing each chapter. They are the core leverage for the book's "save / like / share / comment / follow":

- **3 pull-out cheat sheets** (the strongest save drivers): 1) a "should you even adopt a graph?" decision tree (deriving loop/workflow/graph backward from the 6 signals); 2) a myth vs. reality table ("85% cost reduction," "40-agent department graph," "prompt engineering is dead" each addressed head-on); 3) a failure-mode to fix cheat sheet (zostaff's 5 errors combined with agentmarketcap's 5 failure modes).
- **Quote hooks** (share + like): ericosiu's "Graph = rails, Loop = engine"; Lao Jin's "Graph forces you to answer who watches the loop, what counts, who can stop it"; Prompeter's "a graph is an org chart, a loop is a single employee"; Data Science Dojo's "it just gave a name to something that has run in production for years."
- **Hard data** (save + share, must be labeled "industry estimate / projection," not fact): 2.8 million-view origin, 40% of multi-agent pilots failing within 6 months, compound-error math (95% to the 20th power ≈ 36%, usable as a hard conclusion), a vendor's 2026 disclosed real injection-to-RCE vulnerability (industry proof).
- **Controversy hooks** (comments): prompt engineering is dead, loop vs. graph is a false problem, you cannot ask an agent whether it is in a loop.
- **Follow hook**: chapter 6 closes on "the rebranding old habit." The truly durable axis is "does it have roots." Next time a word gets hyped, this lesson stays. The explicit promise: "follow me, and I'll keep taking apart the next hyped word."

---

## Version Record

- Source file: `00-100问总纲.md` | Translated file: `00-master-outline.md`
- Current version: **v1.5**
- Previous version: v1.4 (added refined source material, strengthened 4 questions)
- Change date: 2026-07-27
- v1.5 change summary (full rewrite of Q2-100 under the zero-number iron law):
  1. Per reference.md "Zero, Content Iron Law (highest priority)," Q2 through Q100 (99 questions) were redone question by question: the body only faithfully translates the source material, with no self-summarizing or self-judging; removed self-authored hypothetical examples, unsourced precise numbers, hollow summary sentences, and repetitive filler.
  2. The six chapters were executed in parallel by editing sub-agents; each question used grep in 资料/ (source material) to verify its basis sentence by sentence; any content unsupported by sources was deleted or replaced with a faithful translation of source text per the iron law.
  3. Loose ends: Q64's precise "eight-thousand-token" figure was unsourced and deleted per the iron law (the context-overflow mechanism description was kept); Q67's "ten to fifty milliseconds" is sourced (Alex_Prompeter's five-node Postgres graph overhead) and kept with an "approximately" hedge.
  4. Compliance recompute: across all 6 chapters, grep for banned sentence patterns (not X but Y / em-dash / template filler / AI summary voice) returned 0 hits; unsourced phrases (forty-thousand / ten-kilobyte / invariant detection / OpenClaw-style framework / weekly report) returned 0 hits; spot-reads of Q16-22 / 36-38 / 71-75 / 86-89 all showed source-faithful texture with adequate information density.
  5. Word counts per question stayed within 300-500 (the Bash script failed this round and the full run did not execute; openings of each chapter were spot-read to confirm no sub-300 short questions; if the script later finds out-of-range values, fix then).
- v1.4 change summary (added refined source material, strengthened 4 questions):
  1. Q11 folded in beamnxw's three-layer model (harness/loop/graph): added the "delete the model and what remains is all harness" test, plus the environment to feedback to process mental model, plus the "one lever per layer" diagnostic.
  2. Q40 folded in Argona/Akshay's quantification of unreliable self-verification: the probability that a model recognizes its own output and scores its own answers higher is markedly elevated; "checking itself" amounts to letting water through; multiple agents sharing a flawed context confirm each other and package errors as consistent conclusions (hedged, no source attribution, no precise percentages).
  3. Q56 folded in h100envy's topology mechanics: before the judgment checklist, first compute the theoretical parallel speedup; if the ceiling approaches one, the work is inherently serial and graphing only adds overhead, so the first question should be "can this work actually be parallelized?"
  4. Q97 folded in h100envy's base-rate precision trap plus Akshay's token reality: multi-agent setups often burn ten-plus times more tokens than a single agent; a verifier's precision depends on the garbage ratio of its input, and at low hit rates a near-half of filtered items still slip through, the problem usually living at the generation end rather than the verification end (hedged).
  5. The four questions came to 432 / 423 / 449 / 482 words, all within 300-500; banned sentence patterns / em-dashes / template filler returned 0 hits.
- v1.3 change summary (global question-number reindex):
  1. All 100 questions were renumbered from the "chapter.question" scheme (1.1-6.15) to a global continuous numbering 1-100; mapping: ch1 = 1-15 / ch2 = 16-35 / ch3 = 36-55 / ch4 = 56-70 / ch5 = 71-85 / ch6 = 86-100.
  2. Synchronized the reindexing of the 01-06 chapter H2 titles and the six outline question lists; corrected all cross-references inside the outline's question notes from "Qx.y / chX Qx.y" to "Q N".
  3. Chapter count and total question count unchanged (still 100).
- v1.2 change summary (fact review with truth-softening):
  1. Removed the specific vulnerability number "Microsoft CVE-2026-26030" in three places (outline Q55 note, quality-boost hard data, version change summary) because the local source corpus did not contain that number; unified to "a vendor's 2026 disclosed real injection-to-RCE vulnerability (industry proof)." The body text of Q55 / Q100 had already been softened to "a vendor disclosed in 2026," and was unaffected.
- v1.1 change summary (per the Outline Review Report P0-P3 plus the Quality Boost Plan):
  1. Merged redundant reality-anchor content: former Q11 folded into Q13; former Q45's "amplify errors" folded into Q44 (mechanism + consequence as a pair).
  2. Merged near-synonym duplicates in ch6: former Q86 and Q95 merged into this Q86 (true/false judgment + rebranding stakes, two layers).
  3. Revised unsourced claims: former Q97's "big tech doesn't use 40-agent graphs" changed to an anti-pattern caution, flagged as a cautionary construct, not big-tech proof.
  4. Added evolution-chain node: Q12 added Harness Engineering (aligned with the LangGraph blog prompt to context to harness to loop to graph).
  5. Softened absolute claims: Q29's "more fatal" to "often costs more" with a note on framework lock-in cost; Q48's "often worse than a single agent" to "in a linear writing pipeline / only earns its keep under multi-perspective verification" qualifier.
  6. Clarified concept vs. operation division: Q30 (what is recoverable, principle layer) separated from Q73 (restore message history or state object + idempotency, operational layer).
  7. Added 3 questions (keeping total at 100): Q15 origin hook (2.8 million views), Q55 tool-output injection to RCE (real vulnerability proof), Q100 cross-node authorization fail-closed.
  8. Added controversy hook: Q4 embedded "you cannot ask an agent whether it is in a loop, only a mathematical proof."
  9. Added the "Hidden Thread and Reading Introduction" section (dissolving the mismatch of "a judgment book that teaches 20 architecture questions first") and the "Propagation Boosters" section (3 pull-outs + quote/data/controversy/follow hooks).
- Chapter question counts: global numbering 1-100, mapped as ch1 = 1-15 / ch2 = 16-35 / ch3 = 36-55 / ch4 = 56-70 / ch5 = 71-85 / ch6 = 86-100 (total 100, unchanged).
