# Chapter 3 · Why does what my AI builds always come out wrong?

## 30. The idea is too big for AI to finish at once, how do I split so it doesn't collapse?

Get one tiny thing running right first, then stack on top. Don't ask it to build a whole mall on day one.

The "build me an e-commerce site" in your head is a bundle of dozens of features. If AI swallows it all at once, it half-builds each one and none of them ever takes shape. A research team at Columbia broke down several of the most advanced coding agents and found the same pattern: the first generation looks fine, but the longer you iterate the more it falls apart, with the gap sitting around 70 percent and the remaining 30 percent needing a human to take over. Asking for too much at once is you planting your own landmine.

Here's the split that works: take a piece of paper, write down the one thing without which the whole thing is useless, and let AI get just that one thing right. Once it runs, tell it "now add the second thing." After every addition, run it before continuing. If it really breaks, you know exactly which block you just added, and the rollback cost is near zero. The finer you split, the higher the odds of a first success, and the faster your confidence arrives.

---

## 31. How do I split "build an e-commerce site" into blocks AI can do step by step and still reassemble?

Split by three layers: data, logic, interface, with a clear interface between each, so reassembly doesn't fight itself.

Software comes down to three layers. The data layer governs where things live (products, orders). The logic layer governs how things run (how to place an order, how to compute the price). The interface layer governs what you can see. A lot of bugs trace back to AI changing the interface but forgetting to sync the data and logic; the three layers fall out of alignment and a feature silently breaks.

Your instructions to AI can be ordered like this: step one, design the data structures for products and orders. Step two, write the create/read/update/delete interfaces. Step three, build the interface that calls them. This matches the validated split the industry uses: schema first, then interfaces, then authentication. After each layer, have it state "what this layer exposes outward" so the next layer can lock on. Skip the middle steps and demand the finished product, and assembly will be chaos.

---

## 32. Build the UI first or the function first, where does a beginner get stuck if reversed?

Getting one minimal functional line running is the most stable start. A pretty UI that doesn't run is only self-comfort; once the function works, then beautify, and your mind stays at ease.

A designer's experience is to walk three layers: explore, build a minimum usable version, then proper engineering. Do the layer that runs first, then add the pretty and the consistent. If you open by telling AI "make a gorgeous page," it piles up pretty shells while the data behind them is fake and hardcoded. When you later connect real features, all of it needs rework, and that is what truly stalls you.

The right posture: have AI make an "ugly but genuinely orderable" version first, get the main flow running. Once it runs, point it at a benchmark page you like and have it unify the style. You can also borrow the incremental approach: place a static layout with placeholder content, add one interaction, fill in that interaction's states, then add the next feature, and refactor when you spot a repeated pattern. Bone before skin; reverse the order and it costs the most effort.

---

## 33. What I want and what AI built differ, how do I rephrase so it really gets it?

State three things: what it should look like, what the input is, what to do on error. Say "don't do X" instead of "do X," and it understands better.

Vague instructions breed buggy code. You say "write a function to fetch user info," AI guesses your intent, guesses wrong without erroring, and the code runs like nothing's wrong while doing none of what you wanted. That error is the most dangerous because it doesn't throw red text, it just quietly does the wrong thing, and by the time you notice the damage is done.

The rephrase template works like this: I want an async function that fetches user data by ID from a given address; return empty if not found; throw a clear error on network failure. Then state what not to do: "don't hardcode the address, don't swallow exceptions, don't assume the data always exists." The more specific the constraints, the lower the odds it freestyles into a crash. Lay the context down first, then give the specific instruction. Don't reverse the order.

---

## 34. Same bug, AI "fixes" it ten times and it's still wrong, getting messier (doom loop), how to break out?

Stop immediately, open a brand-new chat, have it "diagnose only, don't fix," find the root cause, then let a separate chat fix it.

This is a pit everyone who writes code with AI will hit eventually: the doom loop. You report a bug, it says fixed, you run it and it's still wrong. You say fix again, it strays further, because the old chat is now clogged with contradictory attempts and it's confused too, stuck in a deadlock of "says fixed but isn't."

The breakout is one move: don't let it keep editing inside that tangle. Open a new chat, paste the error and that block of code, and say clearly "you only analyze the root cause, write no code." Once it states "the problem is at point A," open a third chat and have it fix according to that diagnosis. There's a real case: building a dog health tracker, a whole weekend was burned getting AI to fix a bug, then abandoned and restarted, and the second attempt got it right in under an hour. The key was the restart.

---

## 35. How do I judge "this version counts as done," give me a non-feeling rough acceptance standard?

It runs end to end, doesn't crash on edge cases, and you can clearly state what it can and can't do now. All three met, and this version stands.

Beginners most easily fool themselves. AI's first draft often "looks like it works," then falls apart on iteration, which is that 30 percent gap the industry agrees on. Judging by a pretty interface and a demo that clicks through is not "done." A designer offered a practical angle: is it really built? Is the style consistent? Can it extend and continue? Will someone still be able to pick it up a month later? Of those four questions, the first two you can use today.

Hold yourself to these three: first, the main flow from open to finish runs clean without veering off. Second, deliberately click randomly, submit empty fields, flip to the last page, and it doesn't white-screen or crash. Third, you close the laptop and can tell a friend in one sentence "it can do X now, still can't do Y." Missing any one of the three means one step short, so don't rush to add features.

---

## 36. Demo runs fine but lags with more data, normal? How to break this?

Normal, but it's not your fault, it's that AI's default generation didn't consider performance. Tell it to add pagination and a count limit to the queries and it breaks.

Locally with a few rows it's fast; on real data it spins. The reason is AI's read pattern tends to "grab everything back then pick slowly"; with little data you don't see it, with more it overflows. This has little to do with how fast your computer is; it's the write style, professionally called missing limits and indexes.

Don't rush to switch tools or doubt yourself. Give AI one clear instruction: "the list fetches only the first twenty each time, paging fetches the next batch, and add indexes at the database layer." It mostly fixes it right. After the fix, deliberately stuff in a few hundred rows to test; the spin disappears and you've passed this gate. Going forward, "can it handle data volume" will always be a thread you watch. Build that awareness today. The earlier you understand the data-volume threshold, the fewer falls you take later.

---

## 37. AI's code is total gibberish to me, how will I ever change it, am I held hostage?

You don't need to write it, but you must understand the skeleton. Every time, have it explain "what this block does" before you decide, and it can't hold you hostage.

A common trap lives in your head: AI's output looks good, runs, ships fast, and you blurt out "trust it" then stop thinking. Then one day you need to change something and have no idea where to start, so you ask AI again, believe whatever it says, and the steering wheel quietly leaves your hands.

The fix is simple: after each block, have it explain in plain words what this part is responsible for, where the data comes from, and what to touch when changing it. If you understand the outline, you always hold the wheel. You can shout stop when it veers, and spot it when it makes things up. At the end of the day, AI here is like a new intern: it does the work, but you decide what can ship and what gets sent back for redo. Don't hand that over just to save effort.

---

## 38. Project grows, AI starts dropping things and contradicting itself (context rot), how to contain it, no messy ending?

Open new chats on purpose, write the decisions you've made into a file, and have it read that file at the start of every chat.

The longer a chat drags on, the worse AI performs; this is called context rot. It forgets the rules you set two weeks ago, the new code fights the old style, the three layers (data, logic, interface) fall out of alignment, and stubborn bugs appear. Don't blame it for getting dumber; blame that chat being diluted by too much, with useful context drowned in the back-and-forth.

In practice: don't grind in one chat to the end; actively open new chats between feature blocks. At the start of each new chat, set the rule first: "read the project notes file first, follow what's in it," rather than rushing a new instruction. Rules in a file are far more reliable than rules buried in chat history. The document is the anchor, the chat is the flow; use the anchor to fix the flow, and no matter how big the project, it won't drift away.

---

## 39. How do I make AI "remember" what we decided, not start from zero every time?

Don't rely only on chat memory; put the decisions into a notes file in the project, and have it read that file at the start of every new chat.

Chat is volatile; close and reopen, and AI's understanding of your project resets to zero. If you re-explain the background every time, it's tiring and easy to miss things, and when you miss, it writes according to its own assumptions, producing something that doesn't fit your existing system.

Create a notes file at the project root that records three things: what tech is used, how the directories are arranged, and what the current focus is. At the start of every new chat, say "read this file before you start." After it reads, the code it gives fits your existing structure instead of each writing its own. Professional developers treat this file as the context base for every AI interaction, and it visibly lifts suggestion quality. Build this habit and the bigger the project the more peace of mind, and it's also the key move for managing quality later. Once the context base stands, iteration runs steadier.

---

## 40. Multi-turn chat, AI forgot what we said earlier, how do I pull it back on track?

It's not truly forgetful; that chat's context got diluted. Paste the correct requirement from before back to it, or just open a new chat and restate the background.

The rule you set in the first two sentences, by the tenth round it starts violating, like you said "buttons are blue" early and later it generated green. You're furious, it's innocent, because in that chat the early constraint got buried under later content.

The fastest pull-back: isolate that correct requirement from before and paste it, "look at this again, the green button generated earlier was wrong, fix it per this." If it's a mess, don't patch, open a new chat and state three things at once: the background, the rules already set, and the one thing to do now. A clean background beats ten rounds of remediation; don't expect to talk it back inside the same tangle.

Another case: you toss it a small snippet to change without saying which feature it belongs to and what surrounds it. Missing context, it can only guess your intent, and guessing wrong it keeps straying. When you hand it something, mention the background along the way; that saves more than pulling it back later.

---

## 41. I want to add a feature, AI says "sure," then it crashes. How to prevent in advance?

Before adding, have it list "which existing parts will move, where might it break," don't let "sure" pass.

AI's willingness to say "sure" far exceeds what it can actually do. Especially after you changed your mind midway, the old code already buried logic serving the old requirement, and stacking the new feature on top makes the two layers fight, crashing where you didn't expect. In research, the two most severe failure categories are error handling and business logic; they often fail silently, the interface runs fine while behind it things are already a mess.

The preventive ask: before letting it act, ask "adding this feature, which existing parts will it touch? Where is it most likely to break?" Once it lists the risk points, you decide which to patch first. Turn a light "sure" into "sure, but handle X first, then act," and the accident rate drops sharply. Have it plan first, you review first; that's far steadier than direct approval.

---

## 42. How do I leave a "manual" for myself so future changes are easy?

After finishing each small block, have AI write one line "what this block is for, what to touch when changing it," store it in a file, paired with a record each time.

You will forget. The logic clear today reads like gibberish two weeks later, especially since the code is AI-written and you didn't write it line by line. Without a manual, changing one spot next time pulls out a string of errors, and you have no idea where the mines are buried, so you ask AI to guess again, and guessing makes it messier.

The practice: after completing each feature block, have AI add a plain-language note to the corresponding spot in the project notes file. At the same time, commit after each block with a clear note of what this round did; this step lets you return to any clean node anytime. Together, these two are your regret medicine. Someday when you need to change something, read the notes first, then the history, no need to recall from zero. Whoever takes over (including you a month later) can follow the thread and change, not face a black box.

---

## 43. Prototype's done, how do I show friends and get feedback that's actually useful?

Don't ask "is it easy to use," ask "what were you trying to do, where did you get stuck." Have friends think aloud while using it; that's worth more than a hundred impressions.

You're used to it and everything flows, so you can't see the problems. A friend sees it for the first time; every point where they get stuck is a pit you skipped with eyes closed. But you ask "what do you think" and they politely say "pretty good" because they have no standard to judge by.

The right way to collect: send the link, no explanation, let them poke it themselves. You sit beside them and ask them to "say whatever comes to mind, shout when stuck." Where they can't find the button, thought they clicked wrong, finished filling and didn't know the next step, those live reactions are gold. There's a real case: writing a WeChat mini-program from zero with AI, it was exactly by having real users think aloud while using that the awkwardness no one else could find got exposed. Write it down, go back and have AI fix those specific spots, more accurate than any questionnaire.

---

## 44. People say my UI is ugly, can AI help me make it look good?

Yes, but only if you first set a "benchmark page" as the standard, then have it unify to that; otherwise its aesthetic drifts on every page.

AI can make pretty interfaces, but only if you know what style you want. Its most common problem isn't technical, it's drift: this page has 16-pixel spacing, the next becomes 24, the buttons look alike but not quite, and the whole thing looks patched together, not like one product. A designer pointed out that the most dangerous bug is often not technical, it's in your head; you too easily say "trust it" and stop managing the style.

The concrete practice: pick the page you're most satisfied with and make it the unified standard. After that, command AI on every new page to "follow this standard page, use real component names, like 'primary button' instead of 'make a blue button'." With the standard fixed, it won't freelance. Consistency is a cultivated habit, not a one-time fix; when you spot a drifting page, pull it back to compare, and slowly the whole product becomes one.

---

AI writing code isn't the hard part; the hard part is you keeping clear on what you want. When you're not clear, it just helps you make the wrong thing faster.
