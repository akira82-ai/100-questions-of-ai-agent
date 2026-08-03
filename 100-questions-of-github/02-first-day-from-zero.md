# Chapter 2 · Day One From Zero: How to Use It Without Touching the Command Line?

First time opening GitHub, the screen full of English buttons is like walking into a foreign supermarket; you recognize half the words on the shelves but do not know where to start. This chapter will not teach you to memorize commands; it only tells you which spots to touch on day one, which buttons are safe to click, and which you can skip entirely. Most people get stuck not because it is hard, but because they try to understand Git on day one, you will not need the command line for your first three days. Get the web stuff smooth first, then decide whether to go deeper.

## Q15. A GitHub repo is all English buttons, which few should I look at on day one?

Entering a repo, do not be scared by that row of English. Just focus on the tab row at the top: Code is the code and download entry, Issues is where others raise problems and suggestions, Pull requests is changes others want merged in; the rest, Actions, Projects, Wiki, are basically unused in the first few days, treat them as invisible.

Scroll down; the numbers in the right-side About are worth a glance: Stars is how many liked it, Forks is how many copies were made, Languages tells you the main language.

First time viewing a repo, the order is: read the intro and README to understand what it does, then Issues to see what pitfalls others hit, and only then the code. Every word on the page is clickable, and you can go back if you click wrong, explore freely.

On day one, the only three things to remember the location of: Star, Watch, and Fork at top right, and where that green Code button is. Everything else is background; use it when needed.

## Q16. Without installing Git or typing commands, how do I store things via the web only?

Many think the first step with GitHub is installing Git and typing commands, not at all. After registering and logging in, click the plus at top right to create a new repo, give it a name and a one-line description, and it is built.

After building, there is an upload entry on the repo page; you can drag files from your computer in, or click to select files, write a commit message, and confirm, done. The whole process is mouse clicks, no command needed.

Editing files on the web is just as simple: open any file, the pencil icon at top right lets you edit; after editing, write a message and save, which itself is a commit. For day one, being able to drag and edit is enough.

When you later really upload code daily, consider installing Git or the desktop app. Get things on the shelf first; what tool feels handy matters less. The command line is later, not a threshold. Even if you later learn the command line, the repo and files you built via web on day one carry over, switching tools does not void them, so start from the simplest with confidence.

## Q17. What does that green Code button do, and why do newbies get most confused?

That green Code button is the entry to download and clone the repo. Clicking it pops a box with the repo URL, a Download ZIP option, and a button to open with the desktop app. It is not mysterious, it just gets the project into your hands.

Newbies get confused because there are too many options with unfamiliar names. The most common pit: wanting to download the zip, you slip and click Open with GitHub Desktop, and the computer starts installing software for no reason. Actually just choose Download ZIP to get a compressed package; unzip and view.

Another pit is that string of URL for Clone; newbies think they must copy it and type a command, but web download does not need it at all.

One line to remember: if you only want to view or store, click Download ZIP; only touch that URL string if you want the command line or desktop sync. On day one you most likely only need the single Download ZIP action.

## Q18. Star, Watch, Fork, what is the difference, and will random clicks cause trouble?

These three buttons get mixed up daily, but their purposes are completely different. Star is like a like and bookmark; one click collects the project into your likes list, retrievable later in Your stars, and gives the author a bit of popularity. Watch subscribes to activity; when the project updates, new Issue, new PR, you get a notification. Fork copies a copy under your account; you can change it freely and later open a PR to give it back.

Will random clicks cause trouble? Basically no. Star and Watch only receive information, never touch code; undo if wrong. Fork creates a copy under your account, but it is just a copy, will not affect the original, and will not auto-sync the author's updates, leaving it alone is fine.

One line: want to bookmark click Star, want updates click Watch, want to change code or contribute then click Fork. The first two are free to click; think before Fork, but none will bring the sky down.

## Q19. Others say Fork then change, is Fork a copy or a link?

Fork sounds like copy; specifically, it is GitHub making you a copy of someone else's repo. After Fork, a same-named repo appears under your account, that is your copy; the author's is called upstream.

The difference from a link: the copy is a real independent repo in your account; you can change it freely, and breaking it will not affect the author. But it is not auto-linked; when the author updates, your copy will not follow automatically, you sync manually.

So Fork is both a copy and a starting point: the copy gives you a base you can change; the starting point means you want to contribute to open source, the standard move is Fork first, change on your copy, then PR it back.

One reassuring note: Fork is not plagiarism; it is the standard open-source collaboration move, as long as you keep the author's copyright notice. Permissive licenses like MIT already allow you to Fork and modify.

## Q20. I want someone's project under my account, Clone or Fork?

First, what each does. Clone downloads the repo to your local computer for viewing and editing locally. Fork copies the repo under your own GitHub account, stored in the cloud.

If you just want to look at code, run it, study it, clone is enough, no account change needed. If you not only want to look but also change and push back to the original, you need Fork, because what you cloned is the author's repo and you have no permission to push directly into it.

The common combo is Fork plus clone: Fork to your account, then clone your own copy locally, push changes back to your copy, finally open a PR. This way you have both a cloud copy and a local editing environment.

In the first few days, if you only browse and bookmark, clone or just Download ZIP works. When you really want to contribute code, take the Fork path. Choose by need; do not do everything at once.

## Q21. Without installing software, pressing a period in the web opens an online editor, how to use it to start?

This is a lazy god-send many do not know. On a GitHub repo page, press the period key on your keyboard, and the browser jumps to a web editor called github.dev, with an interface almost like the common code tool, but nothing to install.

Inside, you browse files, change content, and save changes like a local editor. After editing, write a commit message and commit the change directly back, all in the browser, no Git install, no local environment setup.

Compared to clicking the pencil to edit a single file on the web, its strength is viewing multiple files at once, with a directory tree and search, more like a real working environment. Good for when you want to change something temporarily and do not want to install a whole toolset for that one move.

Remember this key: press period on the repo page. First use feels like finding treasure, especially when you just want to quickly edit a doc or try a small code snippet. It can even open files in others' repos to read, more convenient than clicking through directories on the web. You do not need to treat it as a formal dev environment; just a temporary workbench, close when done.

## Q22. Can I skip configuring Git username and email, and what if I do?

You cannot skip it, the first commit gets blocked, so this step cannot be avoided. Every Git commit stamps your change with an author mark recording who and what email. This mark is generated from user.name and user.email; without them, it does not know who to write, and the commit errors out.

Use the email you registered GitHub with, so commit records map to your account and the profile's green squares and contribution stats recognize you. If you entered wrong, do not panic, reset with the same command; commits recorded under the wrong account before will not auto-change, but future ones are correct.

If you use the desktop app or web upload, the tool often fills this for you; no need to type commands. Only the command-line route needs manual config.

So the conclusion: the command-line route cannot dodge this step, but it is just two commands, configure once and it lasts long. Treat it like swiping a card at the door, thirty seconds of trouble saves a pile of mismatch later.

Copy-paste template (use directly):

```sh
# Set the name and email shown on commits (use your GitHub registration email)
git config --global user.name "Your English name or nickname"
git config --global user.email "you@example.com"

# View all config at once
git config --global --list
```

## Q23. SSH key config keeps erroring "permission denied", which step is wrong?

The error "permission denied (publickey)" is eight or nine times out of ten about the public key, not a network issue. SSH is a pair of keys; the private key stays locked on your computer, the public key goes to GitHub, and only when both match are you let through. The error is basically about whether the public key was handed over correctly.

The most common mistake is not copying the public key fully: missing the leading ssh-ed25519, or truncating the trailing email, so pasting into GitHub naturally does not match. The correct way is to copy only the content of the file with the .pub suffix, selecting the whole segment from ssh- to the end of the email.

Another possibility is you never added the public key to GitHub: go to Settings, SSH and GPG keys, click New SSH key, paste the public key and save. After adding, test with ssh -T git@github.com; seeing "Hi your-username" means it is connected.

Never send the private key out or upload it to a repo; if leaked, delete that key immediately and regenerate. When erroring, first check whether the public key copy is a complete segment, eight times out of ten it is that.

Copy-paste template (use directly):

```sh
# 1. Check if keys already exist
ls -al ~/.ssh

# 2. Generate a new key (replace email with your registration email)
ssh-keygen -t ed25519 -C "you@example.com"

# 3. Copy the public key (only the one with .pub; never share the private key)
# macOS:
pbcopy < ~/.ssh/id_ed25519.pub
# Windows (Git Bash):
cat ~/.ssh/id_ed25519.pub | clip

# 4. Test the connection (seeing "Hi username" means it is set up)
ssh -T git@github.com
```

## Q24. GitHub is slow to spin in China, what speed-ups work without a VPN?

Direct GitHub access in China is slow, images break, clone stalls; the root cause is DNS pollution plus congested overseas nodes, but that does not mean a VPN is required. There are tricks that need no special tools.

Most recommended is editing hosts: use the daily auto-updated source maintained by GitHub520, paste that string of domains and IPs to the end of the system hosts file, refresh DNS and it works. This method installs nothing; with SwitchHosts you can set it to auto-update hourly, done once and for all.

If you do not want to edit a file, swapping github.com in the URL for a mirror domain also opens directly, and browser plugins can auto-redirect. Clone stalling on a big repo, switch https to ssh protocol for stronger interference resistance, provided you configured SSH keys.

One reminder: mirror and proxy sites are mostly read-only; do not log in or upload private code there, to prevent token leaks. Understanding the approach beats memorizing dead domains, because domains and IPs change.

## Q25. No verification email after registering GitHub, besides waiting, what can I do?

If the verification email does not arrive, do not rush to re-register. The most common reasons: the email landed in spam, the address was typed wrong at registration, the email provider blocked GitHub's mail, or you used a temporary email, which GitHub explicitly does not support for verification.

Troubleshoot step by step: first search spam for GitHub; after confirming the address is right, log into Settings, Emails and click Resend verification email to resend; still nothing, switch to a reliable personal email or contact GitHub Support. One reminder: the verification link expires in 24 hours; if it errors when clicked, request a new one. Many get stuck on school or enterprise emails, which sometimes block overseas mail, register with a personal email first, then switch-binding in settings is safer. Also GitHub does not support temporary emails for verification; do not use a one-time address for convenience, or password recovery later becomes a hassle.

## Q26. Before my first commit, GitHub Desktop or command line?

One line: use the desktop app on day one, do not touch the command line. GitHub Desktop is the official free, open-source graphical tool; commits and pushes are done by clicking in the interface, no command typed. For beginners, it hides those scary commands behind buttons.

The desktop app's strength is intuition: which files you changed and what message you wrote are clearly visible, less chance of messing up by a wrong command. The command line is efficient but demands understanding a bunch of concepts first; forcing it on day one easily puts people off.

When you feel the desktop app is not fast enough, or need batch processing or scripting, learn the command line then. Both routes do the same job, just different operation.

If you do not even want to install software, web upload and pressing period to enter the editor also complete the first commit. Tools are means; get things stored first, more important than which tool. Many old tutorials start you typing commands, that is for people who will write code. If you only store docs, materials, edit descriptions, you do not need to follow that path.

## Q27. Why does everyone tell you to read the README first, what if you don't?

Think of a repo as a shop; the README is the sign and manual at the door. Others, including future you, click in and read it first to judge: what is this, how to use, who maintains it. Skipping it and starting is like walking into a shop blindfolded.

The README usually shows automatically at the top of the repo home; the author puts the most important info there: what the project does, how to install, how to run, caveats. Many pitfalls the author already wrote clearly in the README; not reading means stepping on them yourself.

The direct cost of not reading is taking the long way: wrong version downloaded, key step missed, will not run and you think the project is broken. Two minutes reading the README saves two hours of fumbling.

Writing a good README is also high ROI, because it is the repo's face. For your first repo, also put a simple clear README so others get what you are doing at a glance.

## Q28. Saw a project I like and want to bookmark, Star or my own bookmark folder?

Conclusion first: bookmarking inside GitHub, Star is more reliable than your own folder. Star is the platform-native bookmark; one click puts the project in your Your stars list, visible across devices and browsers, with built-in time-order browsing.

If your own folder is browser bookmarks, they are lost on a new computer, and bookmarks only store the URL, you cannot see the project's updates or intro. Star at least keeps the basic info and a follow-up entry.

Another side benefit of Star: the author sees the star count rise, zero-cost encouragement for you. Many pick projects also by star count as reference; every star you click helps later readers.

Of course if you collect a lot and want your own categories, Star then manage with lists or labels. But step one, build the habit of Star-ing; more real than building your own system.

## Q29. Branches sound advanced, does a zero-basis day-one person need to touch them?

On day one you can completely skip branches; just store things and read the page. A branch is indeed an important concept, but it is a tool you need only when you later change things or collaborate, not a threshold on day one.

Analogy: a branch is like a side path off the main road; you change freely on the side path without affecting the main, and merge the two when done. Its existence is for multiple people changing at once, or for you to experiment without touching the main project. On day one, alone, only uploading your own stuff, just use the main road.

When you want to propose changes to others' projects, or try two ideas at once, open a branch. Then remember one rule: do not mess on the main branch directly; open a new branch for new features or bug fixes, delete the branch if you experiment wrong, main project unharmed.

So do not be scared by the word branch. It is lightweight, creation takes almost no space, but you will not need it on day one; when you really hit experimentation or collaboration, it appears naturally. On that day, remember one thing: open a new branch before changing, equivalent to saving first then experimenting; delete the branch if wrong, main project unharmed.

## Q30. I want to upload a local folder for the first time, fewest words to type?

If you take the command line, uploading a local folder for the first time centers on a few actions. First make sure Git knows you: configure user.name and user.email, do once.

Then enter your folder, initialize a repo, add files to the staging area, write a message and commit, then link the local repo to the empty repo you built on GitHub, finally push. The ones you actually type are init, add, commit, remote add, push.

If that is too many, the laziest alternative is no command line at all: create the repo on the GitHub web, go back locally and drag files into the upload area, or open a file and save after editing with the pencil, mouse clicks finish the upload.

So fewest words depends on whether you pick the command line. Pick it and it is those few actions; do not want to type, web drag-and-drop uploads with zero commands. On day one, whatever is easiest.

Copy-paste template (use directly):

```sh
# After entering your project folder, run in order
git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/your-username/repo-name.git
git push -u origin main
```

## Q31. The left-side Issues, Pull requests, Actions, who are they for?

These three tabs look intimidating, but each manages its own thing, and in the first few days you mostly view, not use.

Issues is the project's message board; others raise bugs, feature suggestions, questions here. As a user you come to see what pitfalls others hit, whether there is a ready answer; later when you have a problem you raise it here too.

Pull requests, PR for short, is the request others submit when they want their edited code merged into the project. Watching an active project you will understand: more PRs means someone keeps improving it.

Actions is the automation pipeline; a project can set automatic tasks, like running tests automatically on a commit. Ordinary users basically do not need it on day one; just know it exists.

One line: Issues is where you raise questions and suggestions, PR is where others ask to merge changes, Actions is where tasks run automatically. Early on you mainly browse Issues for answers; the other two you will get naturally once you participate.

## Q32. Can the GitHub interface be set to Chinese, and will that make English tutorials unreadable?

Yes, and GitHub officially supports Simplified Chinese UI, no plugin needed. After logging in, click the avatar at top right into Settings, find Appearance on the left, in Language preferences choose Simplified Chinese and save; the nav bar, buttons, and menus all turn Chinese. Without logging in you can also see Chinese: set the browser's preferred language to Chinese, or directly visit github.com/zh-CN to force load.

But know a boundary: this setting only changes GitHub's own interface text; code and README in repos stay in their original language, not translated. By the way, when you do not understand a feature, check docs.github.com/zh, the official Chinese docs site, easier than wrestling the English interface. Translations of some new or advanced settings may lag slightly, but core features' Chinese is comprehensive enough for daily use.

## Q33. Newbies easily confuse repo and project, are they the same on GitHub?

On GitHub these two words are not the same, but easily confused.

Repository is where code and files live; a project usually maps to one repo. The screen full of files you see is a repo. It is a real storage space; your code and docs lie inside.

Projects is another thing, a kanban tool in GitHub for task management, like arranging Issues and PRs into a board and tracking progress. You enter it by clicking the Projects tab; normal browsing barely uses it.

So the difference: repo stores things, project manages tasks. Many who say "I want to build a GitHub project" actually mean build a repo. In the first few days just understand the repo; the Projects board is an advanced feature to touch when you want systematic task management.

Do not get dizzy from the two words; remember repo equals the place for code, get that clear first.

## Q34. Does editing a file directly on the web count as a commit, and how is it different from local?

Yes, editing and saving a file on the web is itself a commit. You open the file, click the pencil to edit, scroll to the bottom and click that save button; GitHub records a commit, filling the author info and message framework for you, you just add a line.

The difference from local commit is in flow and tool. Local commit usually pairs with Git commands or the desktop app, staging changes then committing, good for batch, frequent edits to many files. Web edit suits quickly changing one or two files, like fixing a typo, no software needed.

Another difference: web edit is per single file, takes effect immediately in the repo; local can accumulate a bunch of changes and commit once, and check before pushing.

For day one, web edit is friendly enough, zero threshold. When you edit frequently, you will naturally want local or desktop for efficiency. Both commits record the same version history, no high or low, just convenience.
