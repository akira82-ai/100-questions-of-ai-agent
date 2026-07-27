# Chapter 1 · Who Is an AI PM, Really?

## 1. The JD says "lead AI products," but after you join you're drawing wireframes and writing docs. How do you spot a bait-and-switch AI PM role?

There is one kind of role that draws the most complaints. The JD shouts "lead AI products," but once you're in, the work is project manager plus delivery: no real product decisions. This fake AI PM has become a standard listing on the hiring market, far more common than people think.

Its shape is usually the same. The JD screams AI, but inside you do scheduling, chase progress, write weekly reports. What the product becomes is not yours to decide, and you have no say in model selection. The word "AI" is mostly marketing copy for clients and investors. More commonly, the company has no real model iteration at all. The so-called AI product is just an open-source API wrapped in a chat UI, with a few business prompts added, and that ships. What you do every day is still the old wireframe-and-doc routine.

To avoid falling in, ask a few hard questions in the interview and you will see through it. Who designs this product's evals? Does the PM have a say in model selection? After launch, do we do data-driven iteration? If two of the three answers are no, the role is basically a bait-and-switch.

The line between a real AI PM and a traditional PM comes down to one concrete thing: are you managing the model's capability, or only managing feature flows? The former is what makes this role valuable; anyone can do the latter. You spend years transitioning, only to land in a fake role, and what you waste is the most valuable time in this window.

## 2. Which PM jobs have actually been killed by AI, and which skills have become more valuable instead?

The PM role is being re-layered by AI. Some work is visibly disappearing; other parts have become more valuable. The dividing line falls between "execution" and "judgment."

What is being eaten fast is the procedural, templated, standardizable part. Writing standard PRDs, building competitor feature comparison tables, organizing the requirements pool, producing weekly project reports, work that used to take half a PM's time can now be drafted in minutes with a large model. The two roles hit most directly: one is the pure requirements courier, translating business speak into docs developers can read; the other is the low-decision feature PM, whose main job is tracking progress and pushing launches. Demand for both is shrinking. Putting "good at writing PRDs" on a resume no longer supports a premium.

What is genuinely more valuable is the other end. People who can define sharp problems, make product calls with incomplete information, and state clearly what to do and what not to do are scarcer than three years ago. Engineers use AI to pull development speed too far ahead, and the PM has become the bottleneck of the whole chain. That is increasingly obvious. The bottleneck is not in writing requirement docs; it is in not being able to decide fast enough what to build, what to skip, and how to tell whether it is right at all.

What to really worry about is people who still treat "I can write PRDs" as their core competency. The execution part is indeed losing value, while demand for the judgment part is expanding fast. The two are moving in opposite directions.

## 3. The JD says "familiar with large models." What depth does the interviewer actually want? What are the three scoring tiers?

The line "familiar with large models" is probably the vaguest and most underestimated requirement of all. It appears on almost every AI PM posting, but interviewers' internal standards vary wildly. If you force it into tiers, there are three.

The lowest tier can explain what a large model can and cannot do, knows basic concepts like Token, context window, and temperature, and has called a few mainstream APIs. This level passes resume screening, but a technical interview will pick it apart. The interviewer wants to hear whether you can explain what these things mean for the product. Just knowing the concepts exist does not count.

The middle tier is the real bar for most big-tech mid-level roles. At this tier you should explain roughly how a Transformer works, understand what the attention mechanism means in engineering terms for product design, and judge, given a concrete scenario, whether to use RAG, fine-tuning, or an Agent. The hard part is connecting technical understanding to product judgment. Memorizing concepts is not enough.

The highest tier can discuss model selection with the algorithm team as an equal. Handed a business goal, you can reason backward to a rough technical plan, and make an evidence-based trade-off between "use a large model or not." Big-tech AI product interviews almost always include layer-by-layer probing of your projects. The core of every probe is always "what is your basis for choosing this." Knowing that something exists will not survive the second round.

A simple self-test for your tier: when an engineer says "this requirement is not suited to a large model," can you ask the second-layer question? Is latency too high, is cost unsustainable, or is the data volume insufficient? If you can reach that layer, you have basically crossed the line of the middle tier.

## 4. Why are AI PMs in 2026 moving from Prompt Engineering to Context Engineering?

The 2024 wave of Prompt Engineering hype turned "prompt engineer" into a hot title, with tutorials and courses everywhere. People who actually built products soon hit an awkward truth: spending a whole day polishing a few prompt lines often improved results less than swapping in a better batch of retrieved documents.

The problem lies at the boundary of the Prompt concept. Early on, people understood a Prompt as the sentence fed to the model: add few-shot, add chain-of-thought, tune temperature, all the effort on "how to ask the question well." But what the model actually reads on each answer is far more than those few lines. The retrieved documents, the user's past behavior, the results returned by tool calls, the constraint rules injected by the system, all of it mixed into the input. The carefully written prompt lines may occupy only a small slice. What finally decides the output lands on this whole layer of information environment. One particular phrasing becomes less critical.

This layer was later called Context Engineering, roughly an order of magnitude larger in granularity than Prompt Engineering. It was forced out by reality. Once the Prompt box could no longer hold the product's real information environment, the larger concept naturally emerged. For the PM, the skill stack as a whole has to move up one notch: in the past you optimized "how to ask"; now you optimize "in what information environment the model answers." Unpacked, this touches many links: RAG retrieval quality, tool design, the trade-offs in memory mechanisms, multi-turn context compression. Each matters more to the final result than a single prompt line.

You still write prompts; they have just been downgraded to one link in the whole context engineering chain. PMs who still put "proficient in Prompt Engineering" as core competency on their resume are missing the window of this skill migration.

## 5. The interviewer asks you to "design an AI customer-service feature." What are the 4 judgment points you must state clearly within 3 minutes?

This is a classic case question in big-tech AI PM interviews, with a high elimination rate. The main reason is that many people jump straight to features without judging first. To state it clearly in three minutes, you are really answering four questions, and the order keeps you from getting lost.

The first judgment is whether this scenario can even be done well with a large model, and where the risk is. The most fatal thing in customer service is not a weak answer but hallucination: the model may invent a return policy that does not exist. The cost of that error far exceeds an ordinary chat product. Lay this risk open first, and the interviewer knows you have a grip on it.

How to choose the technical plan is the second thing to cover. Pure Prompt, RAG, or fine-tuning? A customer-service knowledge base usually has a large, frequently updated document set, so in most cases you should go RAG plus Prompt. Fine-tuning is only considered when you need to fix a brand voice. Giving the selection rationale matters more than reporting the plan directly.

The fallback mechanism is the third layer: what if the model cannot answer, and what if it answers wrong? A good design includes three things: a confidence threshold, a human-takeover path, and a user-feedback loop. Miss any one and you will be pressed.

Last is effect evaluation: how do you define "doing well"? Answer accuracy, human-takeover rate, user satisfaction, average handling time, these indicators must be read together. Staring only at DAU will get you challenged.

These four points are in fact the four questions any AI feature must answer. If you can break them down in this order, the interviewer feels you are making product judgments. People reciting a feature checklist get cut off before the third point.

## 6. Why does a big chunk of an AI PM's high salary go back to model APIs? How do you count the hidden cost?

Salary data makes AI PM look like a gold job. In first-tier cities, 3 to 5 years of experience commonly earns 40K to 65K a month; senior roles reach 800K to 1.5M a year; core roles at top companies can break 2M; a programmer switching to AI PM with a 40% raise is routine. But behind the high salary there is a hidden cost almost nobody counts. The marginal cost structure of this role's products is completely different from traditional software.

The main cost of traditional SaaS is R&D labor and servers; one more use by a user adds almost no cost. AI products run the other way. Every call burns Token. The more active the users, the thicker the bill. Product success and cost pressure are tied together. For many AI startups, Token cost takes 30% to 40% of revenue, and some exceed 50%. A good part of an AI PM's high salary is eaten by the API bill.

What is harder to dodge is that model price cuts do not necessarily solve this. When GPT dropped from 30 dollars to 3 dollars, many products' monthly bills tripled instead: usage exploded, and Agent multi-turn calls amplified the token cost of a single task. In economics this is called the Jevons paradox: the more efficient and the cheaper per call, the larger the total consumption. To count an AI PM's real income, you must fold in this Token pressure at the product level. The high salary is real, and so is the cost-structure pressure this role carries.

## 7. Do ToC AI PMs really not write code? How much code does a ToB Agent PM need, and how do you match it to product type?

Whether "an AI PM needs to code" is a repeatedly argued question. The answer lands directly on product type.

ToC conversational or content-generation AI PMs indeed rarely need to code. The core of these products is interaction design, user insight, and growth strategy. The technical bar is mainly whether you understand the model's capability boundary; being able to build a Demo with low-code tools is enough. This is also the mainstream AI PM role on the market, far from production code.

ToB Agent and platform PMs are another creature. These products design tool calls, multi-Agent collaboration, and data pipelines. If the PM cannot read code at all, it is easy to plant landmines in the requirements phase; the PRD written cannot be implemented directly by the engineering team.

The counter-intuitive part is that in the AI era, senior PMs are pushed closer to code. A veteran of over twenty years now writes code more often than in the past decade, because products sit closer to models and engineering, and being too far from code loses you voice in technical reviews.

To judge whether you need to add code, one metric is enough: how close your product is to models and engineering is how close you should be to code. Those far away need not panic; those close should not hide. You cannot hide; sooner or later it surfaces at the review table.

## 8. Is an algorithm engineer turning into an AI PM a dimensionality reduction, or mutual downgrade? What does each type lack?

Both algorithm engineers and traditional PMs transitioning into AI PM are common, but what these two types lack is completely different. Neither is a dimensionality reduction over the other.

The algorithm engineer's advantage is hard: technical depth overwhelms, no barrier communicating with the algorithm team, can judge model selection independently, will not be fooled in technical reviews. The short board is equally clear, usually stuck on product judgment and user insight, easily trapped in the technical excitement of "the model can do it," ignoring the colder product reality of "will the user actually use it." The most common failure mode for technical backgrounds doing product is starting from model capability and reverse-searching for a scenario, instead of pushing forward from the user's pain point. The direction is reversed; no matter how advanced the model, it cannot save you.

The traditional PM's problem flips exactly the other way. Product intuition, user insight, and project management are all online, but technical depth is insufficient. In dialogue with the algorithm team they easily show weakness, cannot get a word in on core decisions like model selection and evaluation systems, and naturally lose voice.

So both types transitioning into AI PM are, in the end, patching their own short boards. The algorithm-turned must add product sense and sharp-problem identification; the traditional-turned must add technical understanding and evaluation thinking. Eighty percent of failed transitions die on their own short board, not pushed out by the other type, but held back by the inertia of their original long board.

## 9. Should model selection listen to the algorithm team or the PM? How does a real meeting's power game play out?

This is one of the most subtle daily games for an AI PM. On the surface it is a technical decision; underneath it is a hybrid of product decision and resource allocation. Three sides sitting together, each with their own agenda, is the norm.

The typical scene goes like this: the PM says "user experience latency must stay under 3 seconds, answers must be stable"; the algorithm replies "to get that effect we need GPT-4 or Claude, cost doubles"; the boss cuts in "can we use a domestic model to save money." Each holds their ground, none convinces. This deadlock is hard to break because everyone is protecting something right. The algorithm protects the reasonableness and explainability of the technical plan; the PM protects user experience and cost balance; the boss protects ROI. The positions are all right, just from different angles.

The key to breaking it is not to decide who is right or wrong, but to split the selection decision into two layers. The technical-feasibility layer mainly listens to the algorithm team; they know best what the model can do and where the boundary sits. The product-trade-off layer, the balance among latency, cost, and effect, lands on the PM's side to decide. That is a product decision.

A smoother rhythm in practice: the PM first lays out the business constraints, including latency ceiling, cost ceiling, and effect floor; the algorithm gives a candidate model list within those constraints; the PM makes the final choice from the product angle. Splitting the decision beats arguing it out at one meeting table, and each side gets the piece they care about.

## 10. Why is Prompt Engineering no longer an independent skill in 2026? What should the PM add instead?

Saying Prompt Engineering no longer counts as an independent skill in 2026 has two hard reasons.

The first is that the models themselves got smarter. When GPT-4 first came out, writing good prompts was real craft: how to give few-shot, how to guide chain-of-thought, how to tune temperature, every choice directly affected output quality. By the end of 2025, mainstream models' tolerance for prompts rose sharply. The carefully designed writing of the past now gets roughly the same result in plain language. The smarter the model, the thinner the skill premium of prompting.

The second reason is that engineering practice has been worked out. Version management for System Prompts, A/B testing, and effect tracking all have standard tool chains now. No more black magic. The old scarcity of "I can tune prompts" was flattened directly by tools.

Interestingly, the frequency of prompt-related questions in large-model PM interviews is still over 80%, but the focus has shifted. The past tested "can you write it"; now it tests "do you understand that the prompt is part of product design," whether you treat it as an independent skill or as a part inside a larger engineering effort.

What the PM should really add is Context Engineering. It does not solve how to write one sentence the model understands, but how to design the entire information environment the model works in. The quality of retrieved documents, the return structure of tool calls, multi-turn context compression, the injection method of the user's past behavior, each matters more to the final result than a single prompt line, an order of magnitude larger in granularity. You still write prompts, but they can no longer hold up an independent role.

## 11. The big-tech interviewer asks "what AI projects have you done?" How do candidates at three levels answer?

This question has a high elimination rate, but the interviewer is not asking for the project list itself. They are asking whether you have judgment about what you built; the project is just a lead-in. Whether you pass this line comes down entirely to how you tell it.

The lowest-level telling is "what I did." Owned an AI customer-service product, designed the conversation flow, DAU grew by some amount after launch. Sounds complete, but the whole answer exposes no technical decision and no product judgment. The interviewer walks away feeling you are a project coordinator: knows the project ran, not why it ran that way.

The middle level tells "why I did it this way." Chose RAG over fine-tuning because the knowledge base updates often; set the confidence threshold at 0.7 because below 0.6 the human-takeover rate exceeded 30% and was not worth it. Reaching this layer shows every decision had a trade-off behind it. This group passes most mid-level interviews.

The highest level tells "what I learned, and what I would do differently." After launch, the biggest problem turned out to be that users do not know how to ask; model accuracy was secondary. So they went back and redesigned the guidance flow. Token cost was 3 times the expectation because multi-turn dialogue amplified the context; later they compressed cost with summarization. This kind of answer shows judgment evolving, shows reflection after stepping on landmines. It is what senior roles and top companies are really looking for.

The key difference among the three tiers sits at that top layer. Whether you can tell the landmines you hit and the evolution of your judgment is the hard standard separating real from fake AI PMs. The first two tiers anyone can memorize; the third cannot be faked.

## 12. The company has no AI business. How do you cobble together your first AI product experience?

This is the most frequent pain point for career switchers. "3+ years of AI product experience" or "at least one complete AI project" is almost a hard gate; resumes without real project experience rarely pass initial screening. There are three viable paths, with very different value.

The least effortful is an internal transfer: proactively take any AI-adjacent requirement in the company, even just adding an AI chat entry to an existing product counts as a real project. The downside is low control; you wait for the opportunity. Building a Demo yourself is the highest-value path: use the GPT or Claude API to build a small product, deploy and launch it. Even with only 100 users, it is far more convincing than "I studied it." Interviewers value hands-on ability most. In between is reverse analysis: pick an existing AI product and write a product doc on "how I would change it if it were mine." It shows product judgment but cannot replace a real project.

For a serious switch, a 6-month rhythm works. The first two months build awareness and hands-on habits; the middle two months do one or two complete projects, like document Q&A, smart customer service, or a content generator that actually runs; the last two months prepare for the job search. For tools, pick low-code platforms like Coze, Dify, FastGPT (Coze's China version). Production-level coding is not required. One last point: an AI PM resume cannot just say "what I did"; it must say "what the data result was." An AI project with no data is, in the interviewer's eyes, roughly as good as not done.

## 13. After 3 years as an AI PM, what is the dividing line between those who stay and rise and those who leave or stall?

Observing people who have done AI PM for over 3 years reveals a clear split. The dividing line between those who stay and keep rising and those who leave or stall is not technical depth. It lands in a more hidden place.

Those who leave share one trait: after 3 years their core ability is still "call an API and wrap a UI." They may have changed three or four companies, title up, salary up, but the work is the same from start to finish: take a large-model API, wrap a chat UI, add a few business prompts, ship. By year 3 this group hits a clear ceiling, because the market starts to realize this ability is commoditized and will not support a higher salary.

Those who stay and rise usually start rooting in two directions in year 2. One is evaluation and the data flywheel: truly understand how "the model gets better," can build an evaluation system, can design a feedback loop, can judge when to fine-tune. The other is product judgment and business model: having a voice in decisions like "do AI or not," "which kind of AI," "how to make the numbers work."

Looking back, the three dimensions of technology, prompt, and data are only the entry ticket. What really widens the gap is the two dimensions after: product judgment and business execution. Year 3 is a key node. Those stuck in the first three dimensions can hardly rise further; those who have rooted in the latter two begin to pull clearly ahead by this point.
