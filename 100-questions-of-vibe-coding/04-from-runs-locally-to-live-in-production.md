# Chapter 4 · The thing that runs locally, how do I let others use it too?

## 45. Demo runs on my computer, how do I let the whole world access it (deployment in plain words)?

Direct answer: move the code from your computer to a public server that stays on, then give it a web address, and others can click it.

That local address, like "localhost:5173," only your computer recognizes. It's like a dish you stir-fried in your home kitchen; it smells good but the neighbor can't come in. To let others taste it, you put the dish at an outward-facing window.

Today's tools flatten this. With browser tools like Miaoda, WorkBuddy, or Tencent Marvis, you click "Deploy" after finishing and get a URL directly, no command line touched. With VS Code plus Copilot, the common route is push code to GitHub first, then connect to a hosting platform like Vercel, which generates a "xxxx.vercel.app" address in a minute or two. Send the link to friends and they open your app.

Don't get hung up on the scary word "server." For the vast majority of personal small tools, you don't need to buy a machine and install an OS. The platform runs that always-on computer for you; you only hand over what you built. When you truly have thousands of users and need complex custom logic, then consider renting your own server, and there's still time.

The core move of this step in one sentence: let the code leave your computer and live at an address others can also visit.

---

## 46. Does deployment need a rented server, any free one to test the water?

Direct answer: for personal testing, in most cases you don't need a rented server; free hosting platforms are enough to get your first shareable app running.

"Server" sounds like buying a machine for your home. But the mainstream approach today is "hosting": someone else keeps a pile of always-on computers and you borrow a bit by usage. Vercel and Netlify both give free tiers; deploying a pure-frontend small tool is basically zero cost. With browser tools (Miaoda, WorkBuddy, Tencent Marvis), the deploy button sits on top of these platforms, and you can go live without even knowing their names.

When do you need your own rental? Two cases: building a WeChat mini-program means following WeChat's publishing flow, which is different from web; or your thing got complex, needs a custom backend, connects many third parties, and traffic exceeds what free tiers cover. Even then, you start free and upgrade when short.

The advice is direct: for your first shareable app, firmly take the free hosting route. Get the positive feedback of "others can open my thing" first; think about money after it actually has users.

---

## 47. "Live" vs "live and usable," where's the difference, don't lie to yourself?

Direct answer: opening is only the start. A truly "live and usable" build also needs real data, user login, fault tolerance, and backup; missing any one doesn't count as done.

The easiest self-deception for beginners is localhost runs, you deploy, a friend screenshots and says "wow it works," and you feel "I'm done." That's at most "can open." A "live" build with fake data that exists only in your head, clears on refresh, and shows everyone everyone's data is far from usable.

There's a "last-mile wall" here: the first 70 percent of building a demo feels great, but the remaining 30 percent (real database, user auth, payments, production deployment) is where most people slip. You finish a little expense tracker, it looks perfect locally, deploy and find data doesn't persist, multiple users mix up accounts, and only then realize the front was just a shell.

To judge whether you've reached "live and usable," ask yourself four sentences: where does the data live, is it still there on refresh? Can other people log in and see each other's info? Do the money or privacy features run and stay safe? If my computer dies, can the thing still be recovered? If any one of the four can't be answered, you're not live yet, just posing.

Don't lie to yourself. Opening deserves joy, but after the joy, that 30 percent of homework must be honestly done for the thing to truly count as built.

---

## 48. Where does data live, Excel isn't enough anymore (database in plain words)?

Direct answer: for small tools, first use the browser's built-in localStorage to hold out; for multi-user sharing and long-term saving, move to a cloud database (like Supabase); you don't need to know SQL on day one.

Your first app can store data in the user's own browser; this is called localStorage. The upside is zero config, no backend, data persists on refresh. The cost is switching devices or clearing cache loses the data, and only that device sees it. For a single-machine small tool, it's enough.

When you need "what user A stores, user B can't see, but A can still see it after changing phones," local storage isn't enough; you need an independent, always-on place to store uniformly. That place is a database, think of it as a huge spreadsheet warehouse that never closes, where everyone accesses by permission.

The most beginner-friendly cloud database is Supabase; it wraps the database in an interface you can read, and many tools support it natively. You don't need to learn SQL first; tell AI "help me store tasks in Supabase, each user only sees their own," and it connects.

One sentence: first get localStorage running, then move to Supabase when you need multi-user sharing. A database isn't some deep object; it's the house where data lives and everyone enters and leaves by the rules.

---

## 49. Users need to register and log in, how to store accounts and passwords safely?

Direct answer: don't write your own login logic, use an off-the-shelf auth service (Supabase Auth, WeChat login, etc.), and never store passwords in plaintext in the database.

The easiest trap for beginners is telling AI "build me a login feature," and AI lazily writes the account and password verbatim into a table anyone can read. That's hanging the user's house key on the door. The right way: the password is hashed (turned into irreversible gibberish) before it's stored, so even if the database is dragged off, the hacker can't recover the original password.

The steadier path is to not touch this part. Services like Supabase and Firebase come with an "auth" module that handles registration, login, password recovery, and permission isolation for you. You only tell AI "use Supabase Auth for login, each user only sees their own data," and the rest connects. WeChat mini-programs call WeChat's login directly, so you don't even store passwords.

There's a deadly switch called "row-level security" (RLS). It decides whether user A can see user B's data. Don't turn it on, and everyone sees the same data, privacy running naked. Before going live you must confirm it's on, with the rule "each person only sees their own."

For account security, the best strategy for beginners is: use the big platforms' ready-made auth, don't build your own wheel. What you save is risk, not trouble.

---

## 50. What is a backend, why is a UI alone far from enough?

Direct answer: the frontend is the interface your eyes see; the backend is the "kitchen" hidden in the server that actually does the work. A storefront with no kitchen means customers can only look at the menu.

The pages, buttons, and colors AI builds for you are all "frontend." It's responsible for presenting things nicely to the user. But an app that can track expenses, send messages, and separate data by account needs more than an interface. Who computes "how much was spent this month"? Who remembers "this data belongs to which user"? Who sends that SMS? The one doing these jobs is the "backend."

By analogy: the frontend is the dining area and menu, the backend is the kitchen, warehouse, and ledger. The guest (user) only sees the front, but without a kitchen, no order can be cooked. A lot of what beginners build "looks about right but is empty on use" is exactly because there's a front but no kitchen.

Good news: in vibe coding the backend can also be generated by AI. You can say "build me a backend responsible for saving tasks, isolating data by user, and providing interfaces for the frontend to call," and AI writes the server code. For simple tools, you can even use a cloud database (Supabase) to partly replace writing your own backend, saving a pile of work.

Remember this distinction: what you see is the frontend; what you don't see but makes it "actually work" is the backend. To judge whether an app is reliable, don't just look at the face, look at whether the kitchen exists and is clean.

---

## 51. Want to plug in payments, maps, SMS, can AI help me connect them?

Direct answer: it can connect, and AI is good at writing code that "talks to third-party capabilities." But this kind of work involves keys and money, so you must guard the security side.

Payments, maps, SMS, weather, AI won't build a set from scratch. They're "public capabilities" the big platforms built long ago, offered outward through something called an API (interface), and AI's strength is reading the API docs and writing the calling code. You say "connect WeChat Pay, trigger payment after the user places an order," and it really connects.

This kind of integration shares a dangerous commonality: they all need "keys" (API keys), often tied to your money or user privacy. A real lesson: someone had AI connect a third-party service, AI took the shortcut and hardcoded the key into the code and turned on debug mode, exposing the key and internal links. When connecting payments and SMS, this carelessness can get you charged at midnight or leak user data.

So the principle: let AI write the integration code, yes, but keep the "keys" in environment variables, not in frontend code that gets published; for money features, do a small real test before going live.

One sentence: AI can help you connect payments, maps, and SMS, hand that part over boldly. How to keep the keys and how to verify before launch, you watch those yourself.

---

## 52. What is an API (interface), why can't you avoid it in real builds?

Direct answer: an API is the "menu" between two programs. The frontend "orders" from the server or a third party through it and gets back the data or capability; real builds basically can't avoid it.

The page you see doesn't conjure data by itself. When you refresh a to-do list, the page quietly sent a request to the back: "give me user A's tasks." The back replies: "here, three items." This "you order, I serve" agreement is the API. The frontend is the customer, the backend or third party is the kitchen, the API is the menu and pickup window at the kitchen pass.

Why can't you avoid it? Because modern apps are stitched together. Your page handles the looks, data lives elsewhere, payments and maps live at another house. The thread stitching them together is the API. When you have AI "fetch tasks from the backend for the list," you're writing "order by the menu" code.

Where beginners most crash here is "hardcoding the address." Say you build a points mall and AI hardcodes the interface address to the dev environment, and after launch it all fails. The right way is to put the address in an environment variable, dev, test, prod each using its own. If you don't state this clearly, deploying leaves a blank screen.

You don't need to understand the API's underlying protocol, but build this mental picture: things talk to each other through a "menu window." Next time AI says "I called the API," you know it's ordering by the menu, not doing magic.

---

## 53. After going live the URL has no little lock (https), is that a problem?

Direct answer: no lock means the address is still http; the account and password users type travel naked, and the browser lights a red "not secure" warning that makes many just close it.

Ever notice the little lock on the left of the address bar? Locked URLs start with https, unlocked are http. The difference: https encrypts the data transfer, like building a pipe between the user and server that only they hold the keys to; http is a postcard anyone on the path can read.

For someone building an app, no https costs you two real things. One, security: users log in, type phone numbers, enter addresses on your site, plaintext transmission can be intercepted by a middleman. Two, trust: browsers now directly label http sites "not secure"; a friend clicks your shared link, sees the red warning first, and eight out of ten think they hit a phishing site and leave.

Good news: proper hosting platforms (Vercel etc.) configure https for you by default on deploy, almost no effort. Only those who rent their own server need to manually apply for a certificate and configure encryption, and this step is often a beginner deployment snag.

The checklist in one sentence: before sending the link to others, first confirm the address bar shows the locked https. No lock, don't send, go back and turn on encryption. This isn't garnish, it's the minimum threshold for going live.

---

## 54. Deployment failed, red text says "build error," how does a beginner self-rescue without panic?

Direct answer: build errors are nine times out of ten dependency or config issues; don't edit blindly, paste the full red text to AI and let it locate, far faster than you understanding every line.

When deploying to production, the platform must first "build" your project (package the scattered code into a runnable artifact). If this step fails, it throws a pile of red text and beginners panic on sight. Steady first: the red text is the machine reporting where it stuck, not you being worthless.

The two most common causes. One, missing dependencies or wrong versions, like a package exists locally but not online, or the Node version is off. Two, wrong config files; a real case: someone had AI generate project config, AI defaulted to debug mode on and hardcoded environment values, not separating dev from prod, and on deploy it failed to start, with every iteration needing manual checks across several config files.

The standard self-rescue move: copy the complete text from error start to end in the terminal, along with "what I want to achieve" and "what I tried," paste to AI, let it fix. You don't need to understand every line first. But one premise: don't manually edit those scattered config files to fix one error, that digs a deeper hole for yourself. Have AI read config uniformly from environment variables and switch environments automatically, curing it once.

Remember: build errors are the norm in deployment, not your capability problem. Paste to AI and it fixes it before you finish panicking.

---

## 55. Can I maintain the live thing alone, how much effort?

Direct answer: simple tools one person can absolutely maintain; the effort mainly goes to three things: "update regularly, watch errors, back up," and complexity decides the burden.

A WeChat mini-program developer ran the numbers: about 80 percent of his complete product was AI-generated, 20 percent his own judgment and fixes. After launch he maintained it alone, by using AI as a "virtual dev team" rather than carrying all the technical details himself. So on manpower you're not alone; AI is always there.

What really burns energy isn't writing, it's these three: one, updates, follow along when platforms or dependencies upgrade or it suddenly won't run someday; two, watch errors, when a user reports "won't open" you must check logs and paste the error to AI; three, backup, push code to GitHub, export data regularly, don't lose it all overnight.

How much energy depends on how heavy your 30 percent is. A pure-frontend small tool might take a few hours a month. Once you add a real database, payments, custom backend, the ops surface widens and the things to worry about multiply. This is also why earlier I kept advising: build something light and usable first, don't pile on complexity on day one.

Conclusion: one person can maintain it, but don't expect "launch and done." Treat it like a potted plant; occasionally water (update), weed (check errors), repot (backup). Light apps need watering rarely, you can handle it.

---

## 56. More users, site slows down, my fault or AI's fault?

Direct answer: the slowdown blame most likely sits with architecture and database, not AI's "craft" of writing code. Most hosting platforms auto-scale, the real bottleneck is the data layer you didn't design well.

Separate two layers first. One layer is "enough compute": with platforms like Vercel, when traffic rises it auto-adds machines, this layer you basically don't manage, won't slow here. The other layer is "how your data is stored, how your logic is written": like all requests querying the same unindexed big table, or recomputing complex stats on every refresh, and it collapses under people. This layer is a design problem; AI just implemented your requirement as designed.

A reference: someone had AI plan an "extensible" structure at the architecture stage, leaving room from the start, and later when users grew they didn't panic much. Reverse: if your requirement description was vague and AI piled inefficient queries to cobble features, it naturally lags under people. So the slowdown blame often traces to whether your requirement was clear and whether the architecture left expansion room, not AI's "craft" itself.

Troubleshooting order: first look at the platform dashboard's traffic and response-time curves, confirm whether you truly hit the scaling boundary; then see if some specific interface is especially slow. Paste that slow interface to AI and have it check "any unnecessary full-table scans, can we add caching."

One sentence: runtime speed mainly depends on the foundation you designed; AI doesn't carry that blame.

---

## 57. How do I safely push a local demo online, don't upload the keys with it?

Direct answer: keep keys in environment variables, use an ignore file to exclude sensitive files, never write into frontend code that gets published; guard these three gates and pushing the demo live won't become a "leak scene."

Deployment often pushes code to GitHub then connects the platform, and the most common accident at this step is sending the things that should stay secret along. A striking figure: a security firm scanned apps built on a batch of platforms and found about 15 percent had third-party keys directly visible in public code, equal to posting your paid-interface password on your own door.

The right way is three gates. Keys (API key, database password) are not hardcoded in code; put them in environment variables, code only keeps the placeholder "go fetch the key from the environment variable." Use an ignore file (.gitignore) to exclude local config and key files, ensuring git never sends them out on push. Frontend code is visible in the user's browser, so any key can only live server-side, never appear in the frontend.

Write the instruction to AI clearly: "all keys read from environment variables, config separates dev and prod, key files added to the ignore list, frontend contains no keys."

Spend two minutes before pushing live: can I find plaintext keys in the code? Is the ignore file configured? Both "no" and you're safe.

---

## 58. Before going live, is there a checklist to walk through before publishing?

Direct answer: yes. A ten-minute checklist covering five blocks: function, data, keys, encryption, backup; tick them then publish, it blocks most beginner crashes.

Function block: click every button, walk every flow yourself, don't trust "AI says it's done." Many find after launch that some feature only passed on fake data, and crashes on real data. The acceptance standard is one line: walk it the way a real user would, not by looking at it "seems right."

Data block: confirm user passwords aren't plaintext, row-level security (each sees only own) is on, data persists across device login. Missing any of these three, user privacy runs naked.

Keys block: search the code, confirm no plaintext keys; keys go through environment variables; no key found in frontend code. Those 15-percent-leaking apps all fell at this block unchecked.

Encryption block: is the link the locked https? No lock, don't publish, the browser will scare off your users.

Backup block: code pushed to GitHub? Database has export or auto-backup? If the server vanishes someday, where do you recover from?

Write these five blocks as your own launch checklist, tick each before every publish. It doesn't guarantee perfection, but it stops most "I clearly tested it" low-level accidents. The value of a checklist isn't complexity, it's that you actually follow it.

---

Running locally only gets you the entry ticket. That 30 percent of launch homework, real data, login, encryption, backup, is what decides whether you truly "built" something.
