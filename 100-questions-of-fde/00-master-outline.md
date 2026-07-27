# 100 Questions on the Forward Deployed Engineer · Master Outline

> Companion file: `The 100 Questions on FDE.md` (the 100-question skeleton).
> This outline is a navigation map for the writer (and you) to expand into a book.

---

## 0 · What This Book Is

- **Title**: *100 Questions on the Forward Deployed Engineer* (FDE = Forward Deployed Engineer)
- **Positioning**: A "hook book", using 100 questions readers actually ask, it strings together a complete inner journey for an ordinary person, from "I heard there is such a role" to "thinking through whether to enter, how to enter, and whether entering was right."
- **Primary audience**: Individual career switchers who want to enter or transition into FDE (backgrounds in SWE, PM, consulting, SA, data and algorithms, 3 to 8 years of experience, torn between "should I switch, how do I switch, is it a bubble"). Enterprise decision-makers are a secondary audience woven in.
- **Mode**: Mode B (hook book, user journey), not an L3 technical manual. The audience sits at L1/L2 (anxiety plus scenarios), not pure technical readers.
- **Emotional through-line (dual tracks in parallel)**:
  - Surface track: "How exactly do I become an FDE" (growth, career switch).
  - Hidden track: "Is it the savior of AI deployment, or an old role repackaged" (doubt, hype tension).
  - The hidden track must run through the whole book: every seemingly affirmative conclusion must leave room for "the opposing voice" (this is the most shareable part of the book).
- **Source base**: `materials / China-local FDE /` (27 first-hand sources) plus 4 methodology repos under `materials /` plus Chinese and English community research (Reddit, HN, a16z, FDE Pulse, Zhihu, Huxiu's Shen Yue oral account, and others). All data and cases are grounded; fabrication is forbidden.

---

## 1 · Book Structure Overview

| Ch | Theme | Reader mindset | Qs | Key anchors |
|---|---|---|---|---|
| I | Is FDE a golden opportunity, or an old job repackaged? | Decision, doubt | 14 | 42x / 800% / 95% of pilots fail / the "three months to RMB 1M salary" scam |
| II | What exactly is the FDE role, and how is it different? | Cognition, boundaries | 14 | gravel road to asphalt road / Coase's asset specificity / 6:1 software-to-service ratio / Delta and Echo |
| III | What skills does an FDE need | Capability, foundation | 17 | boss's awareness / seven capabilities / T-shaped three pillars |
| IV | How do I break in: which path for which background? | Getting started, path | 15 | five backgrounds' shortest paths / interview tests three things / three industry gates |
| V | Why real deployment is ten times harder than it looks | Setback, China reality | 19 | Shen Yue's oral account (SOE: win over people; private firm: win over the task) / 9-year veteran: "audit is the whole game" |
| VI | What real things can you build after switching | Application, value | 13 | old principal's three-day hand-build / John Deere cuts pesticide 70% / startup bootcamp |
| VII | Is FDE a transitional role, and where should you go? | Advancement, boundaries | 8 | three paths / experience does not depreciate / the last-train question |
| | | | 100 | |

---

## 2 · Chapter-by-Chapter Detail

### Chapter I · Is FDE a Golden Opportunity, or an Old Job Repackaged? (Q1 to 14)
**Reader mindset**: "My feed is all hype, but I don't dare believe it. Is this an opportunity or a scam?"
- **A. Is the wave real (Q1, Q2, Q8, Q10)**: 42x in two years, 800% job growth in 2025, real wave or a statistics game? Who defines "the last mile"? Is China genuinely short of people or just slapping on labels? Is OpenAI building its own Deployment arm a trend or bandwagon-following?
- **B. Old wine in a new bottle (Q3, Q4)**: How does it differ from what implementation consultants did daily ten years ago? Will it be eaten by standardized products in three years?
- **C. Personal fit and anxiety (Q5, Q9, Q11, Q14)**: Is an SWE switching up-leveling or downgrading? Is there a place for PMs? Is 35-year-old coding panic a way out? Who gets amplified, who gets ground down?
- **D. Bubble, scam, threat (Q6, Q7, Q12, Q13)**: Can FDE fill the 95% of pilots with no return? Can "zero background, three months, RMB 1M salary" be believed? A friend says "it's just high-end outsourcing", still enter? As models get stronger, will FDE be done in by its own tools?

### Chapter II · What Exactly Is the FDE Role, and How Is It Different? (Q15 to 28)
**Reader mindset**: "I can't even say the name right. First figure out what it is and how it differs from my current role."
- **A. Name and where it belongs (Q15, Q24, Q28)**: Is the F front-end or front-line? Why does it mostly sit in product engineering rather than services and delivery? Why is its essence a "value deliverer," not a senior SWE?
- **B. vs SWE (Q16)**: Both write code; where does the "definition of success" differ?
- **C. vs SA (Q17, Q22)**: One writes production code, one doesn't, who is irreplaceable? How do Palantir's Delta and Echo divide the work?
- **D. vs consulting (Q18)**: Consultants deliver PPT; what does an FDE deliver, and why the gap?
- **E. vs outsourcing and pre-sales (Q19, Q20)**: On-site coding is just high-end outsourcing? Who is closer to the money, FDE or pre-sales?
- **F. vs PM (Q21)**: Both understand the business; why must an FDE still code?
- **G. Theory anchors (Q23, Q25, Q26, Q27)**: How does "repairing the gravel road into asphalt" feed back to HQ? Why does Coase's "asset specificity" fit? Every RMB 1 spent on software needs RMB 6 on people to land it, what does that say? Where does a big-company FDE differ from a "grassroots FDE" in risk resistance?

### Chapter III · What Skills Does an FDE Need? (Q29 to 45) (key chapter)
**Reader mindset**: "OK, suppose I'm in. What exactly do I have to become?"
> This chapter is the book's capability foundation, unfolding as "system panorama, boss's awareness, seven capabilities, T-shaped three pillars, self-check and evolution." Companion quick-reference diagram in section 3.
- **A. Capability system panorama (Q29, Q39)**: How do boss's awareness plus seven capabilities plus T-shaped three pillars nest; why does training only tech get you nowhere? How to group the seven (first four "do it right", middle two "do it steady", last one "do it long-term")?
- **B. Boss's awareness (Q30, Q31)**: Why is it called "the first door," placed at the front of the capability map? When the boss still believes "AI replaces people," the priority is not a plan but calibrating expectations. Two doors: calibrate the boss's expectations (AI is no silver bullet) plus dissolve employees' fear (fear of layoffs makes them sabotage).
- **C. Seven capabilities one by one (Q32 to Q38)**: value smell (high-frequency, manual, 10x better; "only 10% faster" is not worth it); problem restructuring (ask why three layers deeper; surface needs are often inherited experience); rapid building (assemble, don't write from scratch; cut to 3 features for a one-week prototype; judgment is in what NOT to build); evaluation guardrails (time comparable to development; Demo is not production; eval set, boundaries, fallback); business cognition three layers (business logic, organizational logic, decision logic; wrong foundation ruins everything); organizational drive (launch is not adoption; win key people and quantify value); asset compounding (first custom, fourth product; bank templates, datasets, connectors, SOPs; sell time, sell assets).
- **D. T-shaped three pillars (Q40 to Q43)**: Why does the last "horizontal-wide" pillar (strategy and communication) decide the salary ceiling (USD 350K starting)? First pillar core engineering (Python, SQL, cloud, data pipeline, compliance, full-stack, 5 to 8 year ticket); second pillar AI and Agent specialty (reproducible eval sets, Prompt, Agent frameworks, RAG, multi-model routing, tool-call chains) vs traditional algo engineering; third pillar strategy and communication (High Agency, business sensitivity, consultant temperament, 6 to 12 week timebox) and how to train it.
- **E. Capability self-check and evolution (Q44, Q45)**: Which of the seven are innate, which trainable; attach a "capability self-check list" (technical depth, customer empathy, delivery drive); how junior evolves to senior (junior fills business cognition, customer communication, problem restructuring; senior fills organizational drive, asset compounding, business sensitivity); where big-company FDE vs grassroots FDE differ in capability weight.

### Chapter IV · How Do I Break In: Which Path for Which Background? (Q46 to 60)
**Reader mindset**: "If I really switch, how exactly do I walk my specific path?"
- **A. Five backgrounds' shortest paths (Q46 to Q52)**: Backend 5 years, fill business or communication? What hard skills should a PM learn first? Is the biggest hurdle for consulting to FDE coding or delivering the whole thing? How does data engineering fill industry cognition? How does algo-engineering thinking turn into business value? Can a fresh grad do it directly (Palantir excepted)? Is just-hit-3-years enough?
- **B. Hard-skill threshold (Q53)**: Why do Python, SQL, REST appear in nearly every job posting?
- **C. Soft skills and client experience (Q54)**: No consulting background, where to accumulate client-communication experience?
- **D. Interview (Q55)**: What three things does the "client scenario simulation" actually test, technical depth, customer empathy, delivery drive?
- **E. Industry choice (Q56 to Q58)**: No experience, which industry to dive into first for volume? The three gates "find industry, pick direction, enter with your body," how to choose the first? Why can't industry cognition be rushed, and where must you "soak"?
- **F. Independent FDE start (Q59, Q60)**: "Grassroots FDE" serving SMEs, where do the first clients come from? Does switching mean a pay cut first, and how big a cost?

### Chapter V · Why Real Deployment Is Ten Times Harder Than It Looks (Q61 to 79)
**Reader mindset**: "Sounds easy, but why is it all pitfalls when I actually do it?" (the chapter heaviest on China reality)
- **A. Digging the pain point (Q61, Q62)**: Client says "efficiency"; where is the pain hidden, how to dig it? The demand side is a middle digitalization team, not the front line, what if the signal distorts?
- **B. Organizational resistance (Q63, Q65, Q70)**: SOE stuck on "nobody owns the decision," how to push without taking the blame? Employees afraid of replacement deliberately obstruct, how to break it? Private firm "win the task," SOE "win the people," how to switch between the two playbooks?
- **C. Sales over-promise (Q64)**: Sales over-promise to close; is FDE doomed to fill the hole on entry?
- **D. Over-design and boundaries (Q66 to Q69)**: Three months of full-chain vs the old principal's three-day hand-build? How to judge the "good enough" boundary? Core system switch cost is high, force it or detour? Client shouts "replace 3,000 people" but AI replaces tasks not roles, how to calibrate?
- **E. Business model (Q71 to Q73)**: On-site travel not covered; how does an independent FDE price so it's not wasted? Pay-for-outcome vs monthly maintenance, which is steadier? Data siloed, systems legacy, fix data first or Demo first?
- **F. Drive and ROI (Q74 to Q77)**: How to explain ROI to a non-technical boss? Why "launch is not adoption," getting the client to truly use it is harder than launching? 9-year veteran "audit is the whole game," what to check in discovery? Architecture before AI, but client urges Agents now, how to hold the line?
- **G. Safety guardrails and failure attribution (Q78, Q79)**: The line "80% AI writes, 20% human reviews, 0% touches safety and payment," how to hold it? How to tell if a project failed technically or as change-management, and where should FDE push?

### Chapter VI · What Real Things Can You Build with FDE After Switching (Q80 to 92)
**Reader mindset**: "Fine, but after surviving that, what decent thing can I actually deliver?"
- **A. First project (Q80 to Q84)**: What is easiest to score without crashing? How to pick a high-frequency high-cost process as the first Agent? Logistics manually copying tracking numbers into Excel, how to let AI eat that dirty work? A financial firm's hundreds of implicit rules, how to extract them from old employees' heads and codify? A lead-gen workflow from 10 to 500 emails a day, how to build without collapse?
- **B. Quantify value (Q85, Q86)**: John Deere cut pesticide 70% with AI, how to talk about such quantified value? How much a company must save to justify the boss renewing?
- **C. Asset compounding and productization (Q87, Q88, Q90)**: Project ends vs built into a "product," the difference, and how to snowball? How asset compounding starts, why the fourth client can be sold consulting fees not hours? How to bank each project as a reusable template?
- **D. Startup bootcamp (Q89)**: Why called "the top startup bootcamp," Palantir alumni built Anduril; which two abilities, "end-to-end product building" and "high-density client alignment"?
- **E. Personal brand (Q91, Q92)**: Two years in, how does the resume go from "deliverer" to "industry expert"? How to judge if a client is worth a long partnership or just one-and-done?

### Chapter VII · Is FDE a Transitional Role, and Where Should You Go So It Is Not Wasted (Q93 to 100)
**Reader mindset**: "Betting on this role, will I still be at the table in three to five years?"
- **A. Role survival (Q93, Q97, Q98)**: Once everyone who understands the business can use AI to deploy themselves, is a dedicated FDE still needed? Models change every 90 days, how does experience not depreciate? The risk of turning into a "consulting firm" selling labor?
- **B. Path choice (Q94 to Q96)**: Three paths, technical expert, industry BD, entrepreneurship, which fits? Industry CTO vs partner, where do the capability models differ? Does the "field feel" you banked reset to zero when you change industries?
- **C. Loop and endgame (Q99, Q100)**: Boss's awareness handled, next boss again doesn't understand AI, infinite loop? Ten years on, was doing FDE betting on a trend or catching the last train?

---

## 3 · Capability System Quick Reference (companion table when writing the capability chapter)

> Sources: *The Seven Capabilities of FDE* (WilleAi notes) plus *FDE Guide 2026* (Hulian Hushuo, a Chinese industry outlet).

**Boss's awareness = the first door (cannot enter, the seven capabilities have no stage)**
- Door one, calibrate boss expectations: AI is no silver bullet, cannot replace everyone; state can, cannot, how long, investment.
- Door two, dissolve employee fear: the system arrives as "lighten the load," not "replace"; make the first users beneficiaries; boss publicly backs it.

**Seven capabilities (first four "do it right", middle two "do it steady", last one "do it long-term")**
| # | Core question | One line |
|---|---|---|
| 1 Value smell | What scenario is worth doing | High-frequency, manual, 10x better; "only 10% faster" is not worth it |
| 2 Problem restructuring | What the client truly wants | Ask why three layers deeper; surface needs are often inherited experience |
| 3 Rapid building | How to run fastest | Assemble, don't write from scratch; cut to 3 features for a one-week prototype |
| 4 Evaluation guardrails | How not to crash | Demo is not production; eval time is about development |
| 5 Business cognition | How the business runs | Three layers: business logic, organizational logic, decision logic |
| 6 Organizational drive | How to get it used | Launch is not adoption; quantify value to break fear |
| 7 Asset compounding | Is the next one faster | First custom, fourth product; bank templates, datasets, connectors, SOPs |

**T-shaped three pillars (last pillar decides the salary ceiling)**
- Pillar one, core engineering (deep vertical): Python, SQL, cloud, data pipeline, compliance, full-stack, 5 to 8 year ticket.
- Pillar two, AI and Agent specialty (deep vertical): reproducible eval sets, Agent frameworks, RAG, multi-model routing, tool-call chains.
- Pillar three, strategy and communication (wide horizontal): High Agency, business sensitivity, consultant temperament, 6 to 12 week timebox delivery.

---

## 4 · Source Base and Fact Anchors (cite on demand when expanding; mark the source file)

**Global signals**
- LinkedIn 2026.1: FDE roles up 42x in two years, AI engineers 13x; globally at least 1.3 million new AI roles. (*FDE Guide 2026*)
- MIT NANDA *The GenAI Divide* 2025.7: 95% of enterprise GenAI pilots produce no quantified P&L; investment USD 30 to 40 billion. (*FDE Guide 2026*)
- 2026.5, three things in one week: OpenAI Deployment (19 partners invest USD 4 billion, valuation about USD 14 billion, acquires Tomoro, about 150 FDE); Anthropic with Blackstone and Goldman Sachs USD 1.5 billion (first batch Bank of Montreal); Google Cloud opens 59 new FDE roles. (*FDE Guide 2026*)
- Salary: Palantir USD 205K to 486K (Staff USD 630K plus), OpenAI and Anthropic USD 350K to 550K, Google USD 238K (senior USD 700K); geography NYC 35%. (compiled by Exponent, Levels.fyi, The New Stack, *FDE Guide 2026*)

**China signals**
- ByteDance (Doubao) AI large-model FDE top annual salary RMB 1.05 million; Ant Digital B-side FDE top RMB 900K; Zhipu FDE lead top RMB 1.2 million; junior RMB 20K to 30K a month, mid-senior package RMB 400K plus. (*FDE Guide 2026*)
- Shen Yue oral account (Huxiu): SOE "win the people," private firm "win the task"; demand side is a middle digitalization team causing signal distortion; employees afraid of replacement deliberately uncooperative; old principal's three-day hand-build beats three months of full-chain. (*China FDE Real Picture*)
- 9-year veteran (Reddit and community): "audit is the whole game," discovery phase must be checked through. (community research)
- Greater Bay Area Industry-Education Alliance launched China's first official FDE talent program in 2026.4. (*FDE Guide 2026*)

**Theory anchors**
- "From gravel road to asphalt road": FDE front line feeds back to HQ product. (Palantir practice)
- Coase's "asset specificity": the economics explanation of the FDE role. (*Popular Science, FDE vs Consulting, Outsourcing, Employees*)
- 6:1 software-to-service ratio: every RMB 1 on software needs RMB 6 on people to land it. (same as above)
- Startup bootcamp: Palantir alumni Palmer Luckey (Anduril), Joe Lonsdale (Addepar). (*FDE Guide 2026*)

---

## 5 · Expansion Rules (turn a "question" into a "section")

Expand each question into a book section, suggested fixed structure:

1. **L1 hook (required)**: Open with the reader's real emotion, anxiety, or pain, "Have you also heard…", "Many people get stuck here…". Plant the first cut of the hidden track (doubt the hype) here.
2. **L2 breakdown (framework, method)**: Give an actionable judgment framework or steps, no empty talk.
3. **L3 case (real data, first-hand oral)**: Cite one anchor from section 4, mark the source file. China-reality chapters prefer Shen Yue's oral account and the 9-year veteran.
4. **Action (next step the reader can take)**: Give at least one concrete "do it tomorrow" move.
5. **Opposing voice (close the hidden track)**: Leave one line for the "skeptics" at the end of the section, "Of course, some also argue…". Hold the savior-vs-hype tension.

**Taboos**: All numbers and cases must come from landed files under `materials /`, fabrication is forbidden; questionable data marked "per XX report".
