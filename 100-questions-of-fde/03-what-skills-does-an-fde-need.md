# Chapter 3 · What Skills Does an FDE Need?

You decided to try FDE, and the next question pops up at once: what exactly must I know. The recruiting JD lists a long string, Python, SQL, Agent frameworks, followed by a pile of "soft skills" nobody can define. The more you read, the more panicked: every line looks like a threshold, yet none looks fatal. This chapter lays these capabilities open so you can see which is the ticket, which can be trained, and which you already hold. With capabilities, first see the map, then the walk will not wander.

---

## 29. What does FDE's capability system actually look like, and why does training only tech get you nowhere?

Many think FDE's capability is a tech checklist: just drill Python and Agent frameworks. Believe that and you hit a wall in year one; the tech plan has no flaw, yet the project dies on the boss not understanding and employees not cooperating. After seeing too many such cases, you agree capability was never a checklist.

Break capability into three nested layers and you see it. The outermost is the boss's awareness: whether the client boss's expectation of AI is reasonable, whether employees are willing to cooperate. That door unopened, later capabilities have no stage. The middle is the seven capabilities, the full chain from discovering need to delivery to compounding. The base is the T-shaped three pillars, vertical depth plus horizontal width, the concrete grounding that decides your salary ceiling.

The three relate like a gym: the boss's awareness is the door, the seven capabilities are the process, the T-shaped three pillars are the muscle. Train only muscle without the door and process, and you are a muscular man blocked outside. Put a paper with tech on the left and non-tech on the right; if the right is blank, what you lack is not tech, it is the real ticket.

---

## 30. Why is the boss's awareness placed at the very front of the capability map, called "the first door"?

Many think the capability map should start with "what tech do I know." After seeing too many projects with perfect tech plans that died on the boss not understanding and employees not cooperating, you agree the boss's awareness is the door that jams you first. Many bosses learn AI from two things: short videos tell them it is omnipotent, sales PPT tells them it can cut half the headcount, so he slams the table for a 30% headcount cut next year.

That expectation is doomed to collapse. AI is no silver bullet; it can greatly lift efficiency in specific scenarios, not replace everyone's every job. The employee side is more real: you push a system, and the front line's first reaction is not that efficiency will rise, but whether the rice bowl is gone. Fear is instinct; feeling threatened, they find ways to make the project fail.

So the most important thing before FDE enters is not the plan, it is calibrating expectations. Expectations wrong, everything after is wrong. While the boss is still trapped in the AI-replaces-people fantasy, what you most should do is not write a plan, but help him see reality.

---

## 31. How exactly do you pass the "two doors" of the boss's awareness; before entering, no matter how perfect the system, it will not move?

Door one calibrates the boss's expectations. State four things: what AI can do, what it cannot, how long until effect, what it takes to invest. Expectations wrong, after launch one weak link and the boss feels deceived. Door two dissolves employee fear; three moves to remember.

First, do not let the system appear as replacing people; AI handles repetitive work, people handle work needing judgment. Second, make the first batch of users beneficiaries; first find willing cooperators, let them feel AI lightens my load, then let beneficiaries influence the watchers. Third, the boss must publicly back it; privately approving budget is useless, he must state in public that AI is to let everyone do more valuable things.

Miss either door and the project will not survive to launch. Build a key-people table: who decides, who is affected, who will sabotage. Use the four expectation questions on the boss, use the find-one-person-to-run-it-first tactic on the front line, and pin this table into every weekly report. Once these two doors run smooth, the seven capabilities have a stage; otherwise the prettiest system is a decoration.

---

## 32. Value smell reads three signals: why is a scenario that is "only 10% faster" not worth doing?

Enterprises say they want AI, but 80% of scenarios are not worth doing; not because AI cannot, but because doing it means nothing. To judge whether a scenario is worth it, read three signals. Is frequency high: things that happen every day, optimize a bit and the gain is large; things that happen three times a year, even 10x efficiency saves little. What solves it now: if entirely by hand, by experience, by old masters, there is room for AI to cut in. Can AI beat the current solution by 10x: 10% better nobody wants to switch, 10x better everyone fights to use it. A thing that happens three times a year, you use AI for 10x efficiency, the time saved is not even enough to tune the system.

Value smell is not a gift; it is trained. See a few more enterprises, hear a few more business scenarios, and the judgment comes. Many who chase the high salary get stuck at value smell on the first gate, wanting AI for every scenario they see, and end up building things nobody wants. So those 10%-faster scenarios, do not touch them; save your strength for high-frequency, manual, 10x-better places.

---

## 33. The client says "I want a knowledge-base Q&A": why must FDE ask "why" three layers deeper?

This is the most underrated FDE capability. The client says I want a knowledge-base Q&A system; you go do it directly, upload docs, retrieve, generate answers, technically fine, possibly unused in business. Because the client's real problem is often that the old expert retired, thirty years of experience cannot leave, the new hire takes half a year to ramp and keeps making mistakes meanwhile.

The surface need is knowledge-base Q&A; the deep problem is experience inheritance. FDE's core capability is hearing the subtext, translating the surface need into the real problem. The most typical scene: push smart customer service, the agents say they support it but deliberately test with the hardest questions, screenshot to the work group to show AI answers badly. They are not bad people; they are protecting themselves.

The drill is simple: on every requirement, ask why three layers deeper. Layer one clarifies what is wanted; layer two asks why do it now; layer three asks what happens if not done. By the third layer the real problem usually surfaces, and what you build will be used.

---

## 34. Is rapid building "writing code" or "assembling blocks": does FDE's biggest judgment often show in what NOT to build?

The AI era needs no build from scratch; coding tools have stomped the threshold to the floor, and Agent frameworks have packaged architecture into blocks. FDE's building power equals picking the right tools, combining and splicing, fast validating. The key is not how fast you write, but knowing what to write and what not to.

Often FDE's biggest judgment shows exactly in not building. Cut to three core features, prototype in a week, beats building ten features over three months by a hundred times. The client wants to see something runnable soon, not a feature list. Prototype running, then talk adding features; that beats heads-down three months then delivering, with success rates worlds apart.

So do not be scared by writing code. FDE is not about who writes more code, but who assembles and validates faster. If you can piece a client-wanted prototype out of ready tools, you have half the job. This is why many FDEs show the client something in week one while pure R&D heads down for two months; the gap is not code volume, it is assembly thinking.

---

## 35. Evaluation and guardrails take as long as development: if the Demo runs, why does that not equal production-ready?

A running Demo does not equal production-ready; this is the pit new people most fall into. FDE needs to know three things: how to build an eval set, how to set boundaries, how to have a fallback. A good FDE, while building the system, should spend as much time on evaluation and guardrails as on feature development.

Build an eval set: gather the questions the client will really ask into a test bank, run it after every change, see if answers regressed. Set boundaries: clearly tell the system what it must not do, such as any operation involving money or safety goes to a human. Have a fallback: think through what if it crashes, roll back to last version or switch to a human agent.

Many projects launch in glory and fall apart a week later; the root is insufficient eval and guardrails. Think about crash response while building, do not patch after the fact, by then the client no longer trusts you. The earlier you bank the eval set, the lower the regression cost of every later change; this is the watershed between FDE and amateurs.

---

## 36. Business cognition has three layers: which layer most easily becomes "wrong foundation, everything above wasted"?

Business cognition is not just knowing what the client does; it has three layers. Layer one business logic: how the work flows, what stages an order passes from order to delivery, which steps run automatically and who decides, where the bottleneck is. Layer two organizational logic: who calls the shots; the boss watches strategy, the division head fears power hollowed out, the front line fears replacement; attitudes differ completely. Layer three decision logic: how data becomes judgment; how much inventory to buy, which client to extend credit, behind all are rules.

Of the three, the easiest ignored is organizational logic; the tech plan perfect, often dies on pushing the wrong person, skipping the wrong process. Business logic is the foundation; foundation wrong, everything built above is wasted. Many FDE projects fail not on tech but on never understanding how the client's business runs.

No shortcut to improve, only soak at the client site. Follow sales for a day with a client, follow the warehouse to count once, follow finance to reconcile once, and you find the assumed flow differs from reality by a mile.

---

## 37. In organizational drive, "system launched does not equal business adopted": how to turn fear into cooperation with "three days to thirty minutes"?

System launched does not equal business adopted. You built an Agent, technically perfect, nobody uses it, equals zero. This is the least technical yet most likely to decide project life or death. Three things to handle.

Win the key person: every project has one person you must take; could be the IT lead or the business director; fail him and the project never pushes in. Dissolve employee fear: the system lightens your load, not cuts your post; your experience stays irreplaceable; say this to the heart. Small steps fast: do not roll out fully at once; run in a small scope first, let the first batch of users become your witnesses.

Quantify value, most useful. "Efficiency up" is too empty; state it clear: used to take three days, now thirty minutes; used to take three people, now one. Numbers do not lie; numbers are the best drive tool, turning fear into cooperation. Many FDEs crash here: tech delivered, promotion not done; the project succeeds in the report, disappears in the business.

---

## 38. Asset compounding says "first is custom, fourth is product": what should be banked as assets?

Many do FDE, finish one, charge one, start the next from zero, rewriting the plan, rebuilding the framework, re-stepping the pits. That is trading time for money, a very low ceiling. The FDE who truly earns long-term banks something reusable after every project.

Four asset types to remember. Scenario templates: first time doing smart scheduling took two weeks to learn the industry logic; second time reuse directly. Datasets: every project accumulates industry data; third time in the same industry, your eval set is already a moat others lack. Engineering connectors: once you integrated an ERP, you know how to integrate the second time. Operations manual: how to communicate, how to handle launch feedback, how to meet resistance, banked as SOP.

When assets accumulate to a degree, the first project is custom dev charging dev fees; from the fourth you sell industry solutions charging consulting fees. This is the shift from selling time to selling assets; the more you do, the stronger the compound, and all prior capabilities are amplified by it.

---

## 39. How to group the seven capabilities for easier memory, and why does asset compounding reverse-amplify all prior items?

The seven capabilities together are easy to mess up; grouping clarifies. The first four are "do it right": pick the right scenario, understand the real problem, know the business, ship fast. The middle two are "do it steady": no crash, can push. The last one is "do it long-term": make every project the start of the next.

Grouping is not for easy memorizing; it completes the cognition. Miss any link and your FDE path narrows. And the asset-compounding link reverse-amplifies all prior items: the more you do, the sharper the value smell, the deeper the business cognition, the faster the build, the smoother the push.

So do not treat the seven as seven isolated exam questions; they are one pipeline. The first four do it right, the middle two do it steady, the last makes all effort earn interest. Someone uses opening a shop as analogy: picking products is value smell, knowing customers is business cognition, old customers bringing new is asset compounding; think that way and it comes alive. Understand this structure and you know where to put effort each day.

---

## 40. The T-shaped three pillars: why does the last "wide horizontal" pillar decide the salary ceiling?

Besides the seven capabilities, there are three pillars. Pillar one core engineering, vertically deep, the ticket in. Pillar two AI and Agent specialty, vertically deep, the core that distinguishes FDE from on-site engineers. Pillar three strategy and communication, horizontally wide, decides how high you go.

The first two are tickets many have; the third is rare. Engineers who simultaneously hold deep engineering and consultant temperament are few; FDE's demand curve directly hits the talent supply ceiling, which is why salary keeps pushed up: overseas frontier labs' total comp median is about USD 380K, senior to USD 600K, top roles toward USD 1M; domestic independent service providers charge RMB 20K to 30K a month or tens of thousands to hundreds of thousands RMB per project. Same title, two pricing logics domestic and overseas. In other words, many have good tech; those who have good tech AND understand business AND can push through client politics are scarce enough to set price.

So do not only grind technical depth; that horizontal pillar is what separates you from ordinary engineers. You can push through fuzzy requirements, translate tech trade-offs into accounts the boss understands; the salary ceiling is decided by this pillar. Many grind tech, few grind communication; scarcity is where the premium sits.

---

## 41. Pillar one "core engineering": what exactly must you know, and what does that "5 to 8 year ticket" mean?

Pillar one is the ticket into FDE; without it nothing else counts. Specifically know these: programming languages Python, SQL standard, Java, Golang a plus. Cloud infrastructure needs AWS, GCP, Azure real combat. Data pipeline needs Airflow, dbt, Spark. Compliance and security should have touched frameworks like SOC 2, HIPAA, FedRAMP. Also full-stack ability, from API all the way to front-end.

The hardest threshold is experience: five to eight years of product-grade engineering, able to make architecture decisions in ambiguous environments. This is not name-dropping a few terms; it is carrying projects with real steel. Many switchers stall here, not unable to code, but never made architecture choices when nobody gave requirements.

So pillar one is the ticket, not the whole. It gets you in the door, but the in-door pay level is decided by the other two pillars. Those with thin tech base, fill this one first, or everything else is a castle in the air.

---

## 42. Pillar two "AI and Agent specialty": how does it differ from traditional algorithm engineers?

Pillar two is the core difference separating FDE from traditional on-site engineers. Specifically know these: Prompt engineering that writes reproducible eval sets, frameworks like LangGraph and CrewAI, RAG vector-store selection and retrieval tuning, model optimization and regression testing, cost-latency-quality routing across multiple models, building multi-step tool-call chains so the Agent calls APIs, reads databases, writes back to internal systems.

The difference from traditional algorithm engineers: algorithm engineers grind model performance; FDE grinds connecting the model into the client's twenty-year-old system and getting front-line employees to use it daily. One trains the model stronger, the other makes the model usable; completely two different things.

So do not measure FDE by algorithm-post standards; more papers published matters less than getting one old ERP through. This pillar feeds on engineering-landing experience, not research depth; switchers often find their footing here instead.

---

## 43. Pillar three "strategy and communication" is hardest to quantify yet most valuable: how can ordinary people train it?

Pillar three is the hardest to quantify yet most valuable. It includes several: high agency, still pushing amid internal politics, organizational resistance, unclear requirements. Business sensitivity, translating tech trade-offs into revenue-cost impact a CFO or CIO understands. Consultant temperament, doing discovery interviews, stakeholder analysis, discussing priorities with VP-level managers. Also delivering a usable prototype within a six-to-twelve-week timebox.

How ordinary people train it, no secret: start from projects with direct client contact, even just following sales to one client. On-site you hear the boss complain, watch the front line frown; that beats reading ten communication books. High agency is also forced out: take a small project with no backstop; if you cannot push it, you must find a way yourself.

This pillar is hardest to test yet most decides the salary ceiling. Tech can be filled; this drive to push things through in chaos is what the boss will pay extra for. In interviews this item cannot hide; a few words and they know whether you have really pushed things on-site.

---

## 44. Of the seven capabilities, which are innate and which trainable: here is a "capability self-check list"?

Three dimensions for self-check: technical depth, customer empathy, delivery drive. Technical depth: can you make architecture decisions independently in ambiguous environments; this leans acquired, built by projects. Customer empathy: can you hear the subtext, dissolve employee fear; some are born sharp, but most can train it. Delivery drive: seeing a problem you want to build and run it; this leans most on internal drive, cannot be faked.

Usage is simple: rate each strong / medium / short, and see at a glance where the short board is. Tech short can be filled, take a class, do a few projects, up it comes. Empathy and delivery-drive short are more hidden; many with solid tech stall facing clients, or think half a day without acting, the project stuck forever on PPT.

So do not only grind tech; those two short usually lose not on insufficient ability, but on not discovering where they are short. Fill this list each quarter and you see which direction you grow. Its greatest value is forcing you to admit those two are short, not pretend tech is enough.

---

## 45. From junior to senior FDE, how does the capability model evolve, and where do big-company FDE and "grassroots FDE" differ in capability weight?

Newcomers first fill three: business cognition, client communication, problem restructuring. Tech already meets bar; what lacks is hearing the business and breaking fuzzy needs. Fill these three and you can run small projects independently. Seniors fill three more: organizational drive, asset compounding, business sensitivity; from can-do FDE to good FDE relies on making projects compound and making the boss understand the accounts.

Big-company FDE and the grassroots FDE taking orders differ greatly in weight. Big-company eats the platform; process, SOP, client resources all ready, you focus on tech depth and cross-team collaboration. Grassroots FDE eats the site; self-acquire clients, self-deliver, self-backstop; that strategy-and-communication pillar is used almost daily; starting monthly pay often RMB 20K to 30K, but all banked assets are its own.

Both face the same problem; the only difference is whether the platform backstops. Want the stable big-company path, deepen pillars one and two. Want to run yourself, pillar three and asset compounding are life roots. So do not fret which path is nobler; first see whether you can carry the site with no platform to backstop.
