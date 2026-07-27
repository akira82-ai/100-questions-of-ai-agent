# Chapter 6 · What Real Things Can You Build With FDE After Switching

You survived those deployment hardships and finally entered. Yet the real question surfaces: are these dirty jobs I do daily actually building something? This chapter talks the other side of delivery, from the first non-crashing small project, to turning repetitive labor into reusable assets, to why so many FDEs end up starting companies. Deployment was never the end; it is only the start of the pile of real cases and on-site feel in your hands.

---

## 80. What should an FDE's first project be, to score easily yet not crash?

Do not pick the sexiest at once. The steadiest first project looks like this: high-frequency, now done by hand, done well it is clearly ten times faster, and the boundary is clear, wrong and it will not explode. The logic is in those three value-smell signals; first automate a small-scope repeated manual job, ship a runnable prototype in two weeks, far safer than holding back a big move. Pick a scenario where failure only wastes time and success immediately draws applause. The most feared first project touches core trading systems or safety compliance; one crash and reputation collapses. So the first order wants a win, not a big one. Say help sales automate the weekly hand-summarized client-follow-up sheet, save half a day, he immediately treats you to dinner; this small win's banked trust beats any plan. Win once and you have chips to talk the next harder project. When picking the first project ask one more time: after this, can I reuse it at another client; only if yes is it worth the opener. Greed for big-and-complete most easily drains trust and narrows the road.

---

## 81. A high-frequency high-cost process; how do I pick it out to be my first Agent?

Pick processes with value-smell's three rulers: happens frequently, now all by hand, done well ten times faster. First list a sheet of manual jobs you observed, score each on these three dimensions, prioritize the high scores. Once picked do not be greedy; version one automates only the most core segment, say pulling order numbers from a pile of emails into a table, leave the rest untouched. After the prototype runs, show it to the real user; his one on-site use beats ten demos. Remember the Agent does not take over everything; it replaces the most annoying step. A concrete one: support manually categorizes refund reasons daily; this is typical high-frequency hand work, score must rank high; once picked version one only does categorization, do not by the way also take over replies. Do not pick processes by guess; squat on-site three days and you know which job grinds most; do the high scorers first, do one and confidence and method are both ready, later smoother and smoother; step one narrow and steady beats complete.

---

## 82. A logistics firm manually picks order numbers into Excel; how does FDE eat this dirty job with AI?

This job is most typical: hundreds of orders daily, employees stare at the screen pulling order numbers, addresses, amounts from emails and PDFs, manually pasting into Excel. It is high-frequency, dull, error-prone, exactly what AI should take. The move: first squat on-site a day, note every step of how humans flip, what they flip, which field they fill, do not shout automation at once. Then build a minimal script: read email attachments, use the model to extract fields, write back to the table, first cover the most common order type. Leave a human-check spot on the side, catch one or two errors. Once smooth expand to exception items. Many teams buy an expensive platform at once; actually first running the common seventy percent with a script has the best ratio; the remaining thirty percent exception items human-backed is steadier. Seen too many teams spend big on a platform then jam at data integration; tool is a means, run through first then talk upgrade, do not let selection drag deployment to death. What stumps this job was never tech; it is whether you will squat down first to see how people actually work.

---

## 83. A financial firm has hundreds of tacit business rules; how to dig them out of old employees' heads and freeze them?

The rules in old employees' heads are not in documents; all by experience. Say how a loan gets approved, which field anomaly to report, hundreds scattered across a few people's memory. What FDE must do is turn this tacit knowledge into hard logic in the system. The method: pull old employees through several rounds of real case deduction: take a real business item, have him do and explain why he judges so, you sync-record as rule items, then feed the model as an eval set. Round one will surely miss; patch and run again, loop a few rounds and it thickens. Once frozen into the system, newcomers run by it; the old employee retires, experience no longer leaves with the person. After rules dug out, have the old employee spot-check the system's judgments; his nod counts; the person leaves yet experience still runs in the system. This is solider than consulting's one-time knowledge transfer, because knowledge finally stays in the production system, not locked in some PPT when the project ends; far more useful than opening a training session; the person leaves yet experience still runs; this is truly keeping knowledge.

---

## 84. Outreach workflow automation, from 10 to 500 emails a day; how to build without crashing?

At that scale, what crashes is not the model but the process. First think clear whether those 500 should be sent: is the target audience accurate, is the content truly substantive, will anyone reply. Blind volume only lands in the trash. Architect in layers: data source sets the audience, model writes the draft, human passes the key clients, system bulk-sends and logs replies. Every layer keeps guardrails, say similarity dedup, stop on unsubscribe, anomaly alert. Do not go full auto at once; first run 50 through, then scale. Before sending set metrics: open rate, reply rate, how many become leads; glance daily; if volume up but metrics drop, immediately roll back to the human-check layer. The most dangerous is mass-sending wrong content to 500; worse than handwriting ten. Past volume the most forbidden is turning off the human layer; automation is leverage, the other end of the lever needs a hand holding it; once metrics anomaly yet you cannot see it, the mass-send accident is in an instant; do not ruin reputation for full auto.

---

## 85. John Deere cut pesticides by seventy percent with AI; how do you negotiate such quantified value?

John Deere is a often-cited example in OpenAI enterprise deployment; in Iowa they turned AI into personalized intervention advice for farmers. The key to landing a number like cut pesticides seventy percent is not how flashy the tech is, but whether you can nail value into a measurable metric. Before talking ask clear: how much pesticide per acre now, how much money, what is the cost of over-application. Then calculate the amount AI intervention saves into money, match this account with the boss. Do not persuade laymen with model accuracy; talk with how much saved per acre, how long the payback. Many FDEs crash on having no baseline; the boss asks how much saved and they cannot answer, value floats. First get the current usage cost waste accurate, then AI's account has an anchor. When talking bring competitor references: which peer first used AI to press this cost down, and the boss's urgency spikes at once; value shifts from optional to mandatory. When talking you report numbers not boasts; the boss naturally believes the saving is real.

---

## 86. How much can I save an enterprise with FDE, to persuade the boss to renew?

Enough to renew depends on whether you can tell the saved money as an account the boss understands. The standard play is four accounts: the cost of not doing, how much invested, how much returned, the single most sensitive assumption. Say you saved him three heads, each annual cost two hundred thousand, that is six hundred thousand a year, while your maintenance fee is only a fraction. Do not only report tech results; report cash-flow impact. The CFO cares about payback period, not a feature list. The fiercest move is calculating what if not done: those three heads will get raises next year, a competitor first used AI to press cost down, you cannot even keep pace on price; lay this out and the boss sees not how much spent but how much lost if he does not act; renewal shifts from spend to stop-loss. One month before renewal season put this account on his desk; do not panic-talk when the contract expires, by then he is already comparing other quotes; actively nail value and renewal flows; normally bank value evidence in hand, at the key moment one sentence beats ten empty promises.

---

## 87. Finishing a project and leaving, versus making it a "product"; what differs, and how to roll the snowball?

What differs is whether assets stayed. Finish one order, take hourly fee, leave; next client from zero; this is selling time. Make it a product and you bank the pits stepped, connectors written, eval sets gathered this time into something directly reusable. Next similar client, you tweak and go live, deliver twice as fast, can even quote higher. The snowball rolls: first is custom, by the fourth already half-productized. Every delivery recharges your asset pool, not resets it. Assets accumulated enough and you can even wrap the first client's custom piece as the starter product for a second industry, quote doubled at once. The mistake newcomers make is treating each project as an island; to break free start from the second project spending half a day on banking. Once the snowball rolls you find: same week early could only deliver one client, later can push three at once, because you went from code-writer to assembler and decider; every roll the snowball takes you one step from pure time-selling, one step toward asset income.

---

## 88. How does asset compounding scale, and why can the fourth client be sold consulting fees not hours?

Compounding scales on assets in hand growing thicker. The first three clients you still write and tune live for each scenario; by the fourth you find this industry's needs mostly alike, last time's scenario templates, datasets, connectors directly fit. Now what you sell is no longer code-writing time, but your validated methodology and ready assets; the client pays to walk fewer wrong paths, that is consulting-fee logic. A concrete one: you did order extraction for three logistics firms; the fourth comes with connector ready, eval set ready, your quote is consulting fee, because the client buys the cognition you gained after stepping pits, not the code-writing itself. Hourly pricing has a ceiling, asset pricing none; this is the inflection where compounding switches from hours to assets. To scale fast lock onto one industry and do several in a row; same-industry asset reuse is highest, word-of-mouth compounds too, client referrals come; locking one industry beats casting a wide net for banking assets, and word-of-mouth compounds with it.

---

## 89. Why is FDE called the top startup bootcamp; what two capabilities let Palantir alumni build Anduril?

FDE is called startup bootcamp because it forces you to own the client's workflow end to end, ownership like a founder. Look at the Palantir crowd: Kalshi, Hex, Sourcegraph, Anduril's founding teams all did FDE, and Anduril's founding members came from this line. Two capabilities on them are most valuable: one, end-to-end product building, from discovering need to launch and ops all carried by self; two, high-density client alignment, able to dig out, align, deliver what the boss truly wants in ambiguity. These two capabilities happen to be the core of startups, so two years of FDE equals a free hardest startup class, more real than an MBA. Do not only treat FDE as a job; treat it as a place to bank startup capital; what you learn in these two years is the hardest ammo for going solo later; so work with bright eyes, treat every end-to-end delivery as drills.

---

## 90. How do I bank each FDE project I do into a template reusable next time?

Each delivery, do not only hand over a runnable system; by the way pull out four reusable types: scenario templates, datasets, engineering connectors, ops SOPs. Scenario templates are the standard-solution skeleton for this need class; datasets are the eval samples you banked; connectors are ready adapters for various systems; SOPs are the manual for post-launch ops. At a project's end, spend half a day pulling these out into the asset library. Next time a similar client comes, flip the library before acting, half the work already done. Name and classify each asset type well; half a year later you open the library like opening your own parts shop; assembling from parts for a new project is three times faster than banging from zero. Once the library stands, the startup cost for new clients drops visibly; same quote keeps more profit, same time takes more orders; this is assets working overtime for you. Many deliver then scatter, empty asset library equals rebirthing each time, too wasteful; once the library stands the new-client startup cost drops visibly, assets work overtime for you.

---

## 91. Two years in FDE; how does my resume go from "deliverer" to "industry expert"?

In two years you squat in one industry doing seven or eight projects, saw how this one jams and that one breaks; this density consulting firms cannot give. To go from deliverer to expert you must manage actively: after each project write a pain-map of this industry, connect the scatter points into lines; share the pits you stepped in industry communities, so others think of you when they hit problems; pick one or two vertical scenes to go deep, become the someone others name. One more move: dare to speak outward, write the pit-stepping as retrospectives and publish; the circle slowly recognizes your face. Expert is spoken and made; only doing not speaking, others do not know your depth. Industry cognition is not mixed out; it is seeing through at a glance the seventh time you meet the same pit; this intuition consulting firms cannot give, and is exactly where the boss pays premium for expert. The cognition banked in two years is your most expensive edge over ordinary engineers; write clearly on the resume which real problems solved, and the boss sees industry cognition not another code-writer.

---

## 92. How to judge whether a client deserves long-term accompaniment, or you should plan exit after one order?

Look at three things. One, soil; said before, state-owned firefighting with nobody deciding, professional team beaten by principal's hand-build, such places no matter how hard you try compound little, finish one order and leave. Two, can assets bank; every visit banks reusable pieces sellable to peers, this client deserves long-term accompany. Three, people; does your contact have drive and decision power; if he transfers you stay put, re-evaluate. Several exit signals to remember: contact keeps changing, needs bounce sideways, the asset banking you propose the other side will not let you touch; such clients drain labor then run, long accompany only sinks deeper. Split clients into three types: compounders get long accompany, one-shot deals get fast in-out, pure drains get dropped early; tilt energy to the first type. Do not fix the judgment once; review every three months; soil changed and strategy must adjust; a graceful exit beats a rotten forced hold. Do not fix the judgment once; review every three months; soil changed and strategy must adjust; freezing there is the most expensive mistake.
