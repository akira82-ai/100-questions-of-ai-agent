# Chapter 6 · How do you know what it built is actually reliable?

## 75. It keeps producing bugs. How do you make AI write fewer of them? (the 70/30 rule)

When the output keeps breaking, most of the time it is not that AI is dumb. It is that you handed it the parts you were supposed to check yourself.

Vibe coding has an experience rule called 70/30: let AI do seventy percent, but you or a human engineer must hold the line on the other thirty. The seventy percent AI is good at is the repetitive stuff: boilerplate, tests, docs, refactoring. The thirty percent it is bad at and a human must guard is architecture, complex logic, security, and code review. A lot of people get carried away and throw ninety-five percent at AI. Then they get more bugs than hand-written code, because security and architecture are exactly what AI skips first.

Holding that thirty percent does not require you to code. You only need to call a stop at the key nodes: this part touches user data and money, I set the rules, AI follows. Do not flip the ratio. Handing ninety-five percent to AI is planting a landmine for your future self. A research group at Columbia took apart mainstream coding agents and listed nine failure modes. The worst were error handling and business logic, the two areas a human should guard.

---

## 76. What is a "test," and how do non-technical people get AI to write tests before code? (breaking the bug loop with TDD)

A test is not an exam written for you to read. It is the acceptance criteria you hand to AI. Its biggest use is keeping AI from spinning in a bug loop.

A lot of painful stories go like this: a bug gets sent to AI to fix, it says fixed but it is not, you push it harder and it gets messier, and you fall into a back-and-forth death spiral. The root cause is no feedback given to AI. Experienced developers have pointed this out: the missing test is what causes the bug loop, because AI has neither the context nor a definition of what "broken" looks like. Writing the test first nails down "what counts as correct" before anything else. Every step AI takes gets checked, and the loop breaks on its own.

You do not write the test code yourself. What you do is make AI write it first: describe the behavior you want clearly, let it write the test, then the implementation, and you only look at whether it passes. This is called Test-First, and a non-technical person can direct it. The tool will not write the test for you, but it tests against the standard you set, and you only watch the green and red lights.

---

## 77. What is the "technical debt" AI racks up, and why it buries your future self

Technical debt is the bill you run up by cutting corners for speed, and you pay it back with interest later. Vibe coding piles up technical debt especially fast.

Every time you let AI slap on a patch because it is convenient, it often writes new detour logic to avoid breaking other parts, and the code gets more twisted. Change one spot, three break, you send AI to patch again, and the hole grows. When a project has been churned by countless AI patches into a tangle where starting over is faster than continuing, that is the state where the local demo was fun but real launch became a grind. Even the person who first named this phenomenon admits it.

The research group also observed something: vibe coding usually only gets you to seventy percent. The first draft looks great, but the moment you add features and iterate, it cracks, and the remaining thirty percent needs a human. Do not wait until you are in hell to act. Before adding each feature, confirm the old parts are not broken. Periodically have AI do a refactor that straightens the detour logic. Debt is paid down slowly, not all at once when it collapses.

---

## 78. How do you make every AI change not break the parts that already worked

To stop every change from flipping over the parts that worked, the key is "review after the change, then continue."

The safest move is to have AI finish a change, then you or a second AI act as reviewer and go through it, watching three spots: is error handling enough (will it fail silently when something goes wrong), is the test coverage there, are there security holes. This is far safer than letting it change and fix inside the same conversation, because long conversations suffer context rot and drift further off with every edit.

Two rules in practice: change only one thing at a time, do not cram ten requirements into one change; after each step, run verification to confirm the old parts still work before moving to the next. One trick works well: after each AI change, run the tests you previously passed, and any line that turns red tells you instantly which block it broke. Small steps fast beats a big rewrite that blows up half of it and then needs rescuing. This one suits non-technical people especially: you cannot watch the code, but you can watch "does the old feature still work."

---

## 79. How do you set rules for AI? (CLAUDE.md / ARCHITECTURE.md / the Plan-Review loop), in plain language

Setting rules for AI, in plain language, is this: write it a "project spec" and put it at the project root, then set up a "talk it clear before you act" loop.

That spec is called ARCHITECTURE.md. It writes down four things: what tech stack you use, how the directories are split, what the code conventions are, what you are working on right now. It is not for you to read. It is the backdrop AI uses in every conversation, so it does not have to guess from scratch each time, and the generated code fits your pattern better.

Add the Plan-Review loop: do not let AI write code the moment you start. First talk the plan clear in the doc, then get a second AI to act as reviewer and poke holes, fold the feedback back, and repeat until everyone is satisfied before touching code. You do not need to code. Write the idea in your head into clauses and hand it as context, and the rules are set. This loop looks heavy, but what it saves is countless reworks later.

---

## 80. How do I accept what it built? What counts as "good enough" to ship

Accepting something as good enough is not "looks like it runs." It is going through it with an eye for "how will it fail."

Walk the three questions. First, are edge cases handled. Empty values, weird inputs, users typing garbage, the things outside the normal path, these are what AI misses most. Second, is error handling enough, will it fail silently instead of failing loud and clear. Third, will it leak or crash, this layer refers to the security chapter earlier.

The easiest trap is only testing "normal use," clicking a few times and thinking it is fine. Shove wrong things in on purpose, try the most wicked inputs, and if it still does not crash or freak out, that is truly good enough. Some teams have AI act as the acceptance inspector and hand you a list of "which edges it tested," then you pick two of the wickedest and click them yourself. That beats trusting it fully. If you can state three sentences clearly, what it should do, what it should not do, what to do when it breaks, the thing can ship.

---

## 81. The boss view: how do you judge whether outsourced or AI-delivered work is reliable

A boss does not need to code, but asking three things tells you if the delivery is reliable.

One, is there a test. AI code with no test is like a product shipped with no quality check, shiny outside and maybe shatters at a touch. Two, can it explain the architecture and data flow. If AI can make clear "where data comes from, where it lives, who is allowed to see it," that shows it actually thought it through, not just generated and called it done. Three, did the security baseline pass, the gates of keys, permissions, privacy, check them one by one against the ten points in that earlier chapter.

The deliverable should carry three sentences: what it can do, where its boundaries are, who is responsible. If those three cannot be stated, no matter how fancy the code, do not sign off easily. AI and outsourcing are the same here: signing is you taking the blame. One ruthless move: have AI play the challenger, simulate a malicious user attacking your app, see if it can bypass the paywall or dig into someone else's data. If it breaks in, the delivery has a hard flaw.

---

## 82. How does a team manage code quality after using AI? For the tech lead

After a team adopts AI, managing code quality comes down to one rule: do not remove the human review gate.

Letting AI be the first reviewer is great. It quickly scans for bugs, duplicate code, over-engineering, and it is especially good at watching the three blocks of error handling, test coverage, and security. But a human must make the call. Write into the team spec which things must be human-guarded: security, architecture, release permissions, these AI only suggests, it does not decide for you.

Concrete rollout: every AI-generated feature must pass a human review sign-off before it enters the main branch; the pre-release security scan is confirmed by a person, not left to AI to auto-approve. Tools boost efficiency, but the management and accountability steps cannot be skipped. The most forbidden thing is "trust what AI wrote," which equals outsourcing quality to an intern that hallucinates. Hold the thirty percent human gate from the 70/30 rule, and team output goes up without the pits doubling.

---

## 83. How to upgrade from "AI writes, I blindly try" to "I state clearly, AI obeys" (five prompt patterns to copy)

Upgrading from "AI writes, I blindly try" to "I state clearly, AI obeys" has five ready-to-copy prompt patterns.

One, context first: give background before asking for code, do not open with "build a login." Two, constraint style: say not only what you want but clearly what not to do, AI eats this up. Three, incremental build: ask for one step at a time, accept each step before the next, do not ask for a full e-commerce backend in one prompt. Four, example-driven: give it a few well-written snippets from your codebase as templates, it learns fast. Five, rubber-duck: use AI as a thinking partner, talk the idea clear before writing, and often you figure it out yourself mid-talk.

These five are not magic. They fill in the lesson of "state it clearly" for you. The gap from trial-and-error to setting rules is really whether you can use patterns to frame AI. More patterns is not better. Get constraint style and incremental build fluent first, and you shake off most of the "blind trying."

---

## 84. Docs and comments, let AI write or write myself, how to split the work

Docs and comments, boldly let AI write the first draft, but split the work with a plan.

This kind of task sits in AI's strongest range: translating existing code into plain language, filling in formatted explanations, it is fast and steady. You let it write, and you only confirm it did not make things up, like writing a wrong interface name, or still referencing a function you deleted early. That kind of hallucination you have to catch.

What you should write yourself is the business intent of "why we do it this way." AI does not understand your business, it does not know if this feature backs a process the boss dictated or a hard compliance requirement. One yardstick: hand "how to do it" to AI, keep "why we do it" for yourself. The former it can learn, the latter only you know. AI writes the spec, you write the business logic, and together they make docs a later person can read. Dump it all on AI and it writes the syntax but not the reasoning you had that day. So do not skip this step of writing it yourself, it is what makes the doc worth something.

---

## 85. The project got messy, is there a general "clean up the mess" procedure

When a project gets messy, do not force a rescue. Three general steps stop the bleeding.

Step one, stop and let AI only diagnose, not fix. A lot of people panic and push AI to keep changing, and it gets messier. The iron rule is separate diagnosis from repair: make it explain "where is the root cause" clearly, and you act after confirming. Step two, reopen a plan doc and talk the requirements and boundaries clear in writing, instead of stitching on top of rotten code. This step often reveals: you yourself did not think through what you wanted. Step three, either tear down and restart, which is often faster than stitching, or have AI refactor by the three layers, realigning the data, logic, and interface triad.

When it truly cannot be saved, tearing down and restarting is often faster than stitching. One person's dog-health-tracking mini app fought AI a whole weekend fixing bugs with no result, and the second version took under an hour. The root was not thinking clear on the first pass. The root of mess is almost always requirements and the three layers out of sync. Align first, then act, beats blindly changing ten times.

---

## 86. How to control cost (tokens / quota / time) and avoid the "the more I fix, the more it burns" quota death spiral

The "quota death spiral" goes like this: fixing one bug spawns a new one, every AI fix deducts quota, and you burn forty or fifty dollars a week going in circles while the app stays broken. Repeated patching itself is a tax you cannot shake.

The fix is not complicated, but it is counterintuitive. First, do not let AI loop in the same conversation, if it is stuck, switch conversations, or command it to "diagnose only, do not fix," figure it out before you move. Second, think clear about what you want before acting, vague requirements are the biggest source of burned money. Third, hold the 70/30, do not throw ninety-five percent at AI, the more free it is the more likely it writes rework-needing code, and rework is burned money.

There is also a hidden cost: long conversations let AI's context rot, it drifts further off, and you are still paying for the drifted work. If stuck, open a new conversation, do not grind on for sunk cost. Read the iteration tax as a signal: being stuck is not burning money, it is burning direction. Stop when you should, find a person or rethink, cheaper than grinding.

---

## 87. When should you get a real programmer, do not tough it out until it is unsalvageable

Do not treat "getting a real programmer" as losing. It is leverage, used right it saves big money.

The signals to get a human, plainly, are these few: code that is security-critical like money, auth, encryption, should be human-guarded from the start; high-concurrency production systems, where performance and stability are not "tried out" by AI; legal compliance, which AI does not understand regulation. One very practical judge: stuck in the same bug loop for over half a day and still circling, that usually means it is time for a different brain.

In the experience rule, security-critical, performance-critical, brand-new domain, compliance code, and while you are still learning, none of these should go fully to AI. It makes the draft, a human guards the thirty percent and the life-death gates. Put bluntly, AI freed you from writing code, not from being responsible for the result. The money you spend on the guard pass is insurance, not a waste. Compared to paying after something breaks in production, getting a human to guard is far cheaper. By any math that money should be spent.

---

## 88. How to back up, do not go back to square one overnight and lose it all

Backup is not a ritual only veterans do. It is a habit you should have before every move. Vibe coding crashes often send you back to square one in a second.

Three most practical moves. Have AI commit after each step and push to a remote repo regularly, so you can roll back whichever step went wrong. Export and back up the database separately, do not keep it only locally, recovering code with lost data is still a loss. Keep one copy of "the currently runnable version" compressed and stored as a floor.

Why be this strict? Because when AI changes something wrong, it easily wipes the good parts along the way, and it is all gone before you notice. With a backup you dare to try boldly and change boldly. Do not trust "auto-save" is enough, many platforms only store the current session, and if you did not commit manually, a refresh or device switch loses the changes. A ten-minute habit can save a whole week of work someday.

---

Vibe coding made writing code cheap, but reliability was never something cheap automatically buys. It rests on you holding those few gates.
