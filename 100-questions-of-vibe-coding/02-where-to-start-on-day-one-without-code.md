# Chapter 2 · Day One With Zero Code: Where Do You Start?

## 15. Zero code background. What do I install, where do I click, and can I skip the command line?

Conclusion first. On day one you probably install nothing. Open a tool that runs in the browser, type, and it produces something. The command line is none of your business for now.

Many people get stuck at step one because they read tutorials written for programmers. Those tutorials start with installing Node, installing Git, configuring the environment. That is a different path. You are on the "talk in the browser and it builds" path. The runtime is managed by the platform in the cloud. You only collect results.

Today, do exactly one thing. Sign up for a browser tool (Miaoda, WorkBuddy, or Tencent Marvis all work), type three sentences describing what you want in the input box, press enter, and watch it run. Take Miaoda as an example: it first generates a requirements document for you, you click generate app, and the code is written on the platform's side. The whole process, you never touch a line of code. Environment, command line, syntax, all pushed back. Wait until you know you are building a real project before touching those.

## 16. How to pick a tool: fully-managed platform vs self-built. Which of Miaoda, WorkBuddy, Tencent Marvis, Zhipu zcode fits me now?

First split tools into two types. This split saves you half a year of wrong turns.

The first type is the fully-managed platform. Miaoda, WorkBuddy, and Zhipu zcode belong here. You only talk. It handles the runtime and the deployment. The second type is self-built. Cursor, Claude Code, and Trae belong here. They are powerful, but you install the editor yourself, touch the terminal, and manage files. Beginners should start with the first type for stability.

The easiest trap for newcomers is downloading Cursor because it is the hottest, then facing a screen full of "repository" and "terminal" errors and giving up within an hour. That is like learning to walk and immediately driving a manual sports car.

One signal tells you when to move to a stronger tool. When you find the platform cannot build the complex logic you want, or you want to connect your own database and fine-tune control, that is the time to upgrade. Before that, most people's first project does not need to switch at all. Start from the browser tool. Switch to a heavier tool only when the project truly demands it.

## 17. They say I must install Node and Git. Can a non-technical person avoid them, and how?

You can avoid them. Node and Git belong to the programmer's equipment line. On the browser-tool path, the platform manages them behind the scenes. You could go your whole life without knowing what they look like.

Why do so many tutorials talk about setting up an environment? Because those tutorials are written for people who code. They were always going to use those tools. Node runs the code, Git records every change. You are not that person, so those steps do nothing for you. Skip them.

The laziest way is to look for one label: "no-code" or "natural language generation." Tools with that label take you from sign-up to output entirely inside a web page, with no popup asking you to install software. Anything that says "download the installer first," set it aside. That is not your path. Version control like Git is already handled in the platform's backend. You do not need to know what it is.

## 18. I hate the command line. Is there a pure-chat tool that builds the whole thing?

Yes, and this is the most mature type right now. Miaoda, WorkBuddy, and Tencent Marvis are all pure-chat. You type your idea in the input box on the left, and the app grows on the right in real time. Zero install, zero command line, throughout.

These tools are browser-based code generation platforms at their core. All code is generated and run on the platform's servers. You only deal with one chat box. You do not even need to know the code exists. Take WorkBuddy as an example: it strings requirements, design, development, and review into one pipeline. You say what you want in the web page. It writes code, runs the terminal, and produces a preview in a cloud environment. You never see a black window.

Look for the words "online" or "browser." Avoid any tool that asks you to download, install, or open a black window and type commands. The black-window path is not wrong. It is built for a different crowd. You pick the chat path, so chat from start to finish.

## 19. How do I turn "I want to build an expense-tracking app" into words the AI understands and can build?

The core move is to break the vague noun into four things: who uses it, what they do, what they see, and where the data goes.

Take the expense app. "I want to build an expense-tracking app" gives the AI no handle, so it tends to hand you an empty shell. Change it to this: the user opens it and sees a monthly income-and-expense overview; they click "add an entry" and fill in an amount and a category; the data is stored locally and is still there after closing and reopening. Now the AI is clear.

There is a key shift here. You used to think in words like "smart," "easy to use," "convenient." The AI does not understand those. You must switch to words that paint a semantic picture: what the user can click, what they see, where the data goes. This style is really breaking the requirement into five elements: goal, constraints, input, output, and acceptance. Miss any one and the output drifts. The more the description looks like a picture, the closer the result is to what you want. The AI will not read your mind. The more specifically you describe, the more the output matches.

## 20. Before starting, write the AI a PRD (requirements doc). What does it look like, and why "what it does NOT do" matters more than "what it does"?

A PRD is the three or four paragraphs you write for the AI before you start. What it most needs to state clearly is exactly what you do not want. Many people only list feature checklists and leave out that one line. That is where the trouble starts.

A common beginner mistake: only writing "I want a yoga studio booking tool." The AI free-styles and adds payments, a membership system, and a bunch of things you never wanted, bending the core out of shape. A simple PRD looks like this: build a small yoga studio booking tool; users see the weekly class schedule, pick a class, and sign up with name and email; the teacher can log in and see who signed up; mobile style is green and white. The crucial last line: no payments this time, booking only.

See, that last line "no payments" is the soul. It blocks the AI's over-enthusiasm for you. Spending ten minutes on this doc before starting saves more than ten rounds of later fixes. It nails the boundary first. The clearer the boundary, the less the AI drifts.

## 21. A one-liner requirement vs a good spec. How big is the gap, and how detailed should I get?

Ten times, no exaggeration. You say "build a mall" and the AI gives you a useless toy. You write "product list page, three products per row, showing image, name, and price," and it gets it right.

The density of description directly decides output quality. Every specific element you add bumps the result up a level. A vague requirement forces the AI to guess, and wrong guesses mean rework. A specific requirement needs no guessing and lands close the first time. Missing any of the five elements has consequences: miss the goal and the AI guesses your intent, possibly drifting; miss constraints and the AI uses a stack you do not know, and the code will not even integrate into the project.

How detailed then? One practical standard: when you can close your eyes and picture where every button is on the screen and what you see after clicking it, you are about there. You do not need technical parameters. But write clearly "what the user does, what they see, what they input, and what counts as done." At that level of detail, the AI almost never drifts.

## 22. Should I say the whole idea at once, or build and refine as I go? The right starting posture for beginners

Build and refine as you go. This is the one posture a beginner should not hesitate on. Dumping the entire idea at once tends to produce a shapeless thing that touches every edge but fits none, and you still have to take it apart.

The right rhythm: first get the smallest runnable version out, even if it is ugly and crude. Then add one feature, get it running, then add the next. Only move one thing per round. Concretely, three steps: you state the need, it proposes a plan, you confirm, it writes code, and you verify it runs before the next round. Verify each step as you complete it. Move to the next loop only after it passes.

Behind this is a principle: first get something, then get it good, then get it excellent. The first version's only goal is "it runs," not "it is perfect." Many people get greedy and try to pack every feature into version one, then it crashes and they cannot tell where the error is. One small reminder: before adding any new feature, confirm the old ones still work. The favorite beginner mistake is piling new on top before the old is stable, and everything falls apart.

## 23. How do I give the AI the first instruction without drifting? Do not waste it at the start

Give the first instruction three things: goal, constraints, acceptance. Do not just throw "build an expense tracker."

Write it like this: build an expense page where the user fills in an amount and a category, and after clicking save it shows in a list below; no backend, no network this time. See, goal (expense page), constraint (no backend), acceptance (list shows after save) are all there. Give context before asking for code. Once the context stands, the AI does not run wild.

Miss any one, and the AI fills in a version you did not want. No constraint, and it may pull in a framework you have never heard of. No acceptance, and when it is done you will not know if it is done. For the first instruction, state the three up front: what I want, what I do not want, and what counts as good. After that it flows. Later changes are also cheaper than rebuilding from zero. In the constraints, write the tech stack and what you explicitly do not want especially clearly.

## 24. The AI generated a pile of files I cannot read. Normal? Should I care?

Completely normal, and early on you do not need to care about a single one. Those files are the AI's intermediate work product, like the ingredients a chef has chopped. You do not need to understand what each one is. You only taste whether the dish is good.

Beginners often misunderstand and think they must read every line of code to have really learned, and if they cannot, they feel incompetent and freeze in fear. You do not. Your only task right now is to see whether what it built is right and usable. You do not need to write code, but you should be able to read the skeleton. That is for changing it yourself later, not for day one.

One analogy is sharp: those files are the AI's scratch paper. When you hire someone to write a proposal, you do not demand to first understand the "each" loop they used. You only look at the deliverable. When you later want to change things yourself and keep the project clean, learning the structure can wait. Chapter one mentioned this boundary. You do not need to write, but you should be able to read.

## 25. Can it run locally? What on earth is "localhost," and what does it have to do with what I finally want?

Localhost is a temporary address on your own computer that only you can open. Its purpose is to prove the thing you built actually runs. But other people cannot reach it, because your home router has not opened the door.

"Runs locally" equals "made it." "Other people can reach it too" equals "done." Between those two is one step called deployment, which is a dedicated chapter later. From a locally running mini-program to one truly live for users, there is often a lot of deployment detail in between.

So on day one, seeing it run on localhost is worth celebrating, but know it is not the end. It is like an internal screening room that only you can watch. To truly let people use it, you move it to a public server. In this chapter you only need to confirm "it runs on my machine." Leave the rest for later chapters. Do not think you are done at this stage.

## 26. A wall of red error text. Should I copy it straight to the AI, or puzzle over it myself?

Copy the whole thing straight to the AI. Do not puzzle over it yourself. This is the most labor-saving part of vibe coding. You hand it the error, and it analyzes and fixes. You do not need to understand what the red text says.

Beginners see red text and panic, thinking they broke something and ruined the project. Errors are normal. Even veterans hit them daily. It is not punishing you. It is telling the AI "something broke here, you fix it." Hand the error to the AI and it analyzes and repairs automatically. Red text is the AI's navigation, not your verdict.

The right move: select the whole error (red text included), copy, paste to the AI, and say "here is the error, how do I fix it." Do not delete or edit it yourself, and do not try to guess the meaning. The more originally you submit the error, the more accurately the AI fixes it. This is the one part of working with the AI where you should never carry it alone. Editing blindly can turn something fixable into something unfixable.

## 27. Do the tools cost money? How far does the free tier get a beginner?

Getting started is basically free. Most browser tools have a free tier with enough allowance to finish your first small demo, even your first few practice projects.

You really pay when you decide to run long-term, need higher allowance, or want more features. By that stage you already know whether it is worth it, so paying hurts less. Prices change, so check the official site for live numbers. At writing time the mainstream tiers were roughly twenty to fifty dollars a month, but a beginner never touches that in step one.

One trap to name early. Browser tools bill by allowance, and every bug-fix round with the AI deducts allowance. If the AI creates a new bug and you ask it to fix again, the allowance keeps burning. Someone burned forty or fifty dollars in a week and was still spinning in place. So the free tier is enough to learn the basics. Do not fall into repeated fixes and repeated deductions at the starting stage. Step one's goal is to get a demo, not to balance accounts.

## 28. Picked the wrong tool or direction. Can I switch midway, and what is the real cost?

You can switch, and the cost depends on how far you have walked.

If it is only switching tools, say from Miaoda to WorkBuddy, the cost is low. Keep the requirements doc you wrote, export it, and reuse it. Nothing is lost. Start simple, migrate when needed, and carry the requirements doc the whole way. If the direction was wrong, say you are halfway through and realize this is not what you wanted, the cost is the time spent, but the requirements doc can be rewritten and restarted. Not wasted.

So in week one, do not agonize over "did I pick right." Build a running thing first. If you do not like it, switch. The worst is refusing to start for fear of picking wrong, and ending up with zero demos. One useful habit: at the start of every project, write that three-to-five-sentence requirements note first. It costs little time, but when you switch tools or directions, all your thinking has a basis. You do not reconstruct from zero what you wanted.

## 29. Is there a "minimum starting path for non-technical people" I can just follow to get a demo?

Yes. Follow these six steps and you get your first demo in half a day.

Step one, pick a browser tool and sign up. Do not spend more than ten minutes choosing. Step two, write a three-sentence requirements note: what it does, who uses it, what it looks like, plus one line of "what it does NOT do this time." Step three, paste the note into the chat box and let it produce version one. Step four, look at the preview and stare at only one question: did it build it. Step five, pick one feature to add, get it running, then add the next. Step six, test every round of changes; if wrong, copy the error to it.

The core of this path is "small steps, fast runs." Do not seek one-time perfection. Push a little each round and confirm direction each step. One reference rhythm: day one set the project and write the note, day two first generation, days three and four concrete iteration, day five run a safety check, days six and seven show it to people. When stuck, return to two questions: did it build, and where is it wrong. Answer those clearly and you can walk all the way to the demo.

---

> On day one you only need to do one thing: get it running. Principles can come later, slowly. But that running app is the real starting point for all your learning after.
