# Chapter 1 · Can You Really Build an App Just by Talking?

## 1. Can you really build an app just by talking? Splash the cold water first, then start

Yes. It is real that you can talk to an AI and get a small clickable app out of it. But there is a gap between "made something" and "made something usable," and most people never saw it coming.

AI coding tools are far stronger than they were a year or two ago. Searches for this kind of tool rose more than twentyfold in a single year. The vast majority of people who write code now use one daily, and even many people with zero technical background have started building their own little tools. One person had three rough little games running within the first hour.

What AI is good at is pulling up a working shell from nothing, fast. You describe the idea, and it generates the interface, the basic logic, and the skeleton of a database all at once. That part really is absurdly quick.

The gap is what comes after. A prototype is easy to make. Actually shipping it, getting real users on it, and keeping their data safe is the step cut out of almost every "build an app in an hour" video. People who have shipped full projects say it plainly: this is best for prototypes and exploration, not for running as a production system. Your mom can make a little playable game, and your mom can make an e-commerce app that does not leak user passwords. Those are two different things.

This book starts by splashing cold water: figure out which one you actually want before you start.

## 2. If my mom and I can both build apps now, how far can an ordinary person really go with vibe coding?

An ordinary person can go further than most people think, but not as far as the videos suggest. Let's split it into two layers.

The first layer is prototypes and small internal tools. Here ordinary people go very far. A designer with no background wrote down the style and features in plain language and had a blog with publishing features up and reachable in two hours. If you want a small thing to track expenses, schedule a game, or remember anniversaries, you do not need to study programming for half a year first.

The second layer is production-grade systems. Here ordinary people do not go far. There is a telling real number: in one incubator batch, about a quarter of the startups had codebases that were over 90 percent AI-generated, but every one of those founders was a technical veteran who could have written the product themselves a year earlier. The AI did not fill in their judgment. It just amplified their hands.

So the truth is this. Vibe coding amplifies what you already have. If you are clear, it makes you clearer. If you are messy, it makes you messier. An ordinary person can easily clear the threshold from zero to one, but reaching a real system that serves many users takes more than chatting.

## 3. "I want to build an e-commerce site" is nonsense to the AI. How do you break it into steps it can do?

One sentence is too coarse, and the AI cannot catch it. That is normal, and it is not your fault.

The e-commerce site in your head is stuffed with unspoken assumptions: how users log in, how products get listed, how money gets collected, who sees what data. You understand these naturally from life, but the parts you did not say, the AI does not know which default to pick, so it guesses. When it guesses wrong, you feel it is useless.

The breakdown is simple. Walk it by people and actions. Do not throw "build e-commerce" at it. Instead say: who uses this, what each person can do when they come in, where the data goes afterward, and clearly what it does not do. Someone building a WeChat mini-program wrote only a short product vision, and the AI broke out a users table, a goals table, and an anniversaries table, even designing the relationships between them. See the difference. A person who can break things down gets an architect. A person who cannot gets a blind man.

On the ground, write a short paragraph before you start. It beats making a wish by ten times. The paragraph does not need jargon. Just answer those few questions in plain words.

## 4. Will programmers be replaced by AI? Conclusion first, then what you should do

Conclusion first. Programmers will not be replaced. The part that gets replaced is the part that only translates requirements into code.

Where is the difference. AI can write code, but it cannot judge whether a feature needs to exist, design a sound system architecture, or understand what users actually want. Those are exactly the more expensive abilities that sit above writing code. A senior engineer uses AI to get ten times the output, because they understand architecture and trade-offs and can see at a glance that the AI-generated code, though imperfect, is good enough.

So if your job is only mechanically turning someone else's requirements into code, that is genuinely at risk. AI is dozens of times faster there. But if you are practicing breaking down problems, judging right from wrong, and designing systems, you will not be replaced. You will become more valuable, because AI took the repetitive work off your plate.

For yourself: stop asking whether AI will replace you. Ask instead whether you are learning to write code or learning to direct AI to get things done. Those two paths diverge tenfold within a year.

## 5. I am a worker feeling the shock. No coding skills, any chance? Yes, and do this first

There is a chance, bigger than you think. But the chance is not in whether you can code. It is in whether you can say what you want clearly.

The shock anxiety mostly comes from one misjudgment: thinking AI coding is a programmer's business, unrelated to outsiders. It is the reverse. AI flattened the hardest part, writing code. What is left as the core skill is whether you can break a vague notion into steps the AI can understand and build. That is exactly a skill many workers already had. It just was never treated as valuable before.

A product friend who knows no frontend syntax got a working portfolio blog from chatting with AI in two hours. It was not technical skill. It was the ability to explain what he wanted.

The first thing to do is simple. Next time you have a chore you want automated, do not think "I can't code." Try explaining it to the AI. If you cannot explain it, force yourself to. As you explain, you will find that what blocked you was never the code. It was that you had not thought through what you actually wanted.

## 6. A boss wants to use AI instead of hiring programmers to save money. Does that math work?

Whether the math works depends on what you point the AI at.

Small tools and internal systems: the math works. A request that used to wait in a queue for developer resources can now be built by the boss or an ops person. What you save is waiting time and communication cost. One team measured that 80 percent of a WeChat mini-program's code was AI-generated, with 20 percent human judgment and correction, which is plenty for an individual or small team.

Production-grade systems that serve outsiders: the math does not work. The reason is hard. You may not review AI-written code, but authentication, payments, and user data must be understood and owned by someone. One cut-out fact is this: the stories of people who wrote zero code and pushed a product live with pure AI usually leave out that behind it either a pro caught the fall or they paid for the lesson after a crash.

So bosses should run a different calculation. AI lets you hire fewer people who repeat code-writing. It does not let you hire fewer people who set architecture, gate quality, and fight fires. Cut the latter too, and the savings come back doubled in some production incident.

## 7. Vibe coding, AI-assisted programming, agentic. What is the difference? Do not let the words spin you

These three get mixed up constantly. The simplest line is one: do you review the code.

You state the requirements clearly, the AI writes the code, you read it line by line, you test it, and you can explain to someone how it works. That is using AI to write software. You click accept directly, never look, never test, and grind by results and back-and-forth prompts. That is vibe coding. The person who coined the term said himself it was for one-off weekend projects, not real engineering.

Further out is agentic, meaning you no longer write yourself. You orchestrate a team of agents and act as supervisor and gatekeeper. That is the more serious usage. You set quality gates, run automated tests, and keep a human watching at key nodes.

You do not need to memorize definitions. One question is enough: when what I built actually breaks, do I understand it and can I catch it? If yes, any name works. If no, and you click accept anyway, no pretty name will save you.

## 8. Are those "build an app in an hour" posts on Xiaohongshu real? Which steps got cut

The prototype hour is real. What got cut is the steps from prototype to usable.

Someone had three rough little games running in the first hour. That happened. Today's tools really let you say a sentence and get a clickable interface in a minute. The video cuts there, with a surprised soundtrack, and it looks like magic.

The steps after look like this. You find the game logic has holes and must ask the AI to fix them again and again. You want to add login and store some data, and suddenly you need to know what a backend and a database are. You want other people to reach it, so you must deploy. Any one of those steps can stop you, and the video never shows it.

The demo is the easy seventy percent. The remaining thirty percent, the real database, user authentication, payments, and deployment, is where most people stop. The "build an app in an hour" claim did not lie to you. It just did not tell you how far that one hour's output is from something you can hand to real users.

So after watching that kind of video, do not panic and do not float. Remember: anyone can have a running demo. A usable product is the real dividing line.

## 9. Can a beginner really make something usable, or only toys?

You can make genuinely usable small things, but you cannot make a production-grade system. Believe both sentences together.

First, what you can do. A person who never touched programming used a browser AI tool and made a blog with publishing and categorization in two hours. That has happened. If you want an internal tool, a personal project, or to test a product idea, zero background is enough. You do not need a computer science degree first.

Now what you cannot do. Once your thing connects to real services, stores user info, or handles traffic, you need to understand the infrastructure you do not yet understand. Experienced people say plainly that today's tools are friendliest to people who already know a little programming, because sooner or later you go down to debug and refine. Pure beginners can go far, but they hit a wall at some point.

So do not get pulled to the extremes. Saying a beginner instantly becomes a developer is exaggeration. Saying it is all toys and useless is underestimating it. Its real place is in the middle. Using it to turn an idea into something you can touch is more than enough. Expecting it to carry a real business for you is still early.

## 10. "Made it" and "made it right" are two different things. What does that mean?

The interface opens, but that does not mean the business logic is correct, let alone that the data is safe. That is what the sentence means.

AI-written code has a trait: it is very confident, but it hallucinates. In real cases, generated code had wrong field names, forgot to wait where it should wait, and left out permission checks. The interface looks fine, but the business breaks on run. You see an app, but that does not mean it built the flow you wanted.

More hidden is security. Code that runs can lay out user data that should be hidden, or hard-code an admin password inside as a backdoor. These bugs do not error, do not turn red, do not scare you. They show up only on the day something actually breaks.

So after you make it, ask yourself three things: does it match what I wanted, will it mess with user data, and if it is wrong, can I tell? If you cannot answer one of the three, what you hold is not "made right." It is "happened to run."

Much of the rest of this book teaches you how to turn "happened to run" into "made right."

## 11. Giants are all building Miaoda, TRAE, Coze. Where is the ordinary person's chance?

When giants build tools, the ordinary person's chance is not in fighting them on the bottom layer. It is in running the path from requirement to prototype faster.

Look at the tool side first. Domestic AI-native editors like TRAE handle Chinese requirements well, have a free basic tier, and let beginners give commands smoothly. Platforms like Miaoda and Coze are more chat-to-use, letting non-technical people build small apps directly. These tools cut the threshold down to "can talk."

Where is the chance. Before, if you had an idea, you either studied programming for half a year, paid tens of thousands to hire someone, or found a technical co-founder, and often ended up with nothing. Now, alone, by mastering these tools, you can turn an idea into a clickable demo, show it to people, validate it, and iterate. The ceiling for solo developers is raised across the board. One person can design the product, write the backend, deploy, and maintain.

Giants earn from tools and compute. You earn from the specific idea in your head that they cannot build. Do not race them on whose engine is stronger. Race on who understands the people they serve better.

## 12. Who coined vibe coding, and why did everyone suddenly talk about it in 2025?

The term caught fire from a casual tweet by Andrej Karpathy, co-founder of OpenAI, in early 2025. He later said the tweet was a shower thought, sent on a whim, and unexpectedly it named a vague feeling in many people's minds at exactly the right moment.

Why did 2025 suddenly make everyone talk about it. At root, the capability arrived. Earlier AI code writing errored often, and you dared not really use it for anything. By 2025, models were strong enough that a non-technical person could build a small app by chatting. The demand was always there. The tools just finally caught up.

That year, related searches rose more than twentyfold, and the word was named a word of the year by a dictionary. It went from one person's joke to a development style people discuss seriously, and even many big companies and incubators use it as a default internally.

You do not need to care who coined the word. You should care whether the feeling it describes is something you are living through. If yes, keep reading.

## 13. I have a product idea in my head. Can AI make it real? First see how far it can take you

It can take you from idea to a clickable demo, but turning it into a real product still needs a few steps you must fill in yourself.

First, what AI can catch. You drop a product vision at it, and it can break out the feature modules, design the basic architecture, write the frontend and backend code, and even walk you through deployment. For a WeChat mini-program, architecture, entities, interfaces, pages, and deployment can all be handed to AI. You only set direction, control complexity, and judge right or wrong. Alone, with AI, you own a virtual development team.

Then what it cannot catch. Product positioning is your call. Whether to add social features, whether to touch privacy, that kind of judgment AI cannot give. And the steps before launch: real users come in, data must be safe, service must be stable. Someone who knows the field must gate those. The wall from demo to production, AI can bump it with you, but getting over takes you.

So do not ask whether AI can make your idea real. Ask which steps I am willing to fill in myself. Willing, the idea becomes real bit by bit. Want only to wish and wait for it served, and it stays an idea forever.

## 14. Who is this book for, and who is it not for? Test first whether you are in range

First, who it is for. You have a product in your head, or chores to automate, but empty-handed and cannot code. This book is written for you. You are a worker afraid of being shocked by AI and want to know what value you have left. Read it. You are a boss, or product and ops, who wants to build the prototype first and hand it to someone later. There is a seat for you here too.

Now who it is not for, and this must be stated hard. If you want wish-fulfillment success, thinking you say "build me a Taobao" to the AI and it gives you a money-making Taobao, this book cannot help you, and nothing on the market can. If you completely refuse to think and only want to click once for a finished product, do not open it. You will crash hard by chapter three.

One self-test at the end. Are you willing to grind seven or eight rounds with the AI over one small feature? Willing, you are in range. Not willing, go practice the word "willing" first, then come back. Vibe coding amplifies people willing to think things through, not people trying to skip thinking.

---

> What this book wants to say is plain. Building an app just by talking is real, but to actually make it, and make it right, the steps in between can only be thought through and filled in by you.
