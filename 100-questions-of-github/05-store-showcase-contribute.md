# Chapter 5 · How to Store Your Stuff, Show It Off, and Even Join Open Source?

Storing well, showing off, and even joining open source are the three steps from user to builder. Earlier chapters taught you to search and run, but the truly valuable part of GitHub is that it keeps your stuff safe, shows your ability in public, and lets you build a project together with strangers worldwide. This chapter assumes no coding knowledge; it only covers three things any ordinary person can use: storing, showing, and contributing. How to make your first repo, how to use Pages for a homepage, and how to contribute to open source without writing code.

## Q70. What should my first repo hold, and does an empty repo make me look amateurish?

Many people agonize over what to put in their first repo, afraid an empty one looks weak. In fact GitHub treats your profile as a living resume; even schoolwork or a small practice project looks better uploaded than left empty. Your first repo can hold a self-intro, study notes, or a small exercise you followed from a tutorial. The point is to have something first, then enrich it gradually.

One reminder: GitHub defaults to public; if you do not want a repo seen, pick Private when creating it. An empty repo is no shame; never daring to create one is the real waste. Upload one first and see; a profile is a snowball, and the earlier you start the bigger the compound. Even just a book list or a study log you organized is a digital footprint that beats only thinking about it. Do not wait until ready; your first audience is the future you, and looking back at these starting records shows your progress more clearly than any tutorial. Many people's first repo is just study notes, and months later even they are surprised how far they came.

## Q71. How do I write a README people get at a glance, good-looking without knowing layout?

The README is the repo's signboard plus manual; GitHub shows it automatically on the home page, so writing it well pays off hugely. No layout skills needed: GitHub uses Markdown, a simple format; open the file on the web and the pencil at top right edits it, with a Preview above the box to check the effect before saving.

Just fill a clean template: three blocks of intro, usage, and contact, with clear words mattering more than looks. After writing, visitors know at a glance what this is and how to use it, saving a pile of questions. Remember the file must be named README.md for GitHub to recognize it; a wrong name makes it a plain file that will not render. Pretty writing is not required; clear writing already wins half, since readers want information not a layout contest. Templates are everywhere; search resume template or github readme template and copy-edit beats staring at a blank page.

Copy-paste template (use directly):

```markdown
# Project name

One sentence on what this project does.

## Features
- Feature one
- Feature two

## How to use
1. Step one
2. Step two

## Contact
Questions welcome, open an Issue!
```

## Q72. Markdown has so many syntaxes, which few do I need first for a README?

Only four syntaxes really matter for a README: # plus space for a heading, two asterisks around text for bold, a minus at line start for a list, and backticks around code. These four cover ninety percent of cases, with clear headings, emphasized points, and tidy items that ordinary readers grasp at a glance.

Learn links and images later: square brackets plus parentheses for a link, exclamation plus square brackets plus parentheses for an image. One iron rule: a # must be followed by a space; writing #heading will not enlarge it. The file must be named README.md for GitHub to recognize it. Do not let syntax scare you; learn these four first, and look up the rest when needed. Ready-made Markdown cheat sheets exist; keep one on your phone and glance at it when stuck, no need to memorize. Treat format as a tool not a gate; what blocks beginners is never syntax but fear of writing wrong, yet you can edit and save anytime. Markdown also stays neat wherever opened, unlike Word which messes up layout on another computer, a big plus for newcomers.

Copy-paste template (use directly):

```markdown
# Big heading        (# followed by a space)
## Small heading
**Bold text**
- List item
`one line of code`
[Link text](https://url)

Multi-line code: wrap with three backticks, then the language name (e.g. python)
```

## Q73. I want to upload code but fear it looks bad and gets laughed at, how to package the first repo?

Fear of being laughed at is overthinking. What GitHub watches is whether you are willing to act; an active, tidy profile persuades more than fancy volume. Packaging the first repo is simple: drop in a clean template with intro, usage, and contact filled clearly; use # to space heading levels; after editing, use the web Preview to check rendering before saving.

No need for cool effects; just state what the project does and how to run it. Even practice work uploaded is proof of your growth; no one laughs at someone who starts seriously. A blank profile instead makes people think you only watch. The community watches attitude not talent; whoever dares upload first already beats most who only look. A profile is a growth log, not a finished portfolio on display; the earlier you leave traces the more you see progress, and perfectionism is the first repo's biggest enemy. Truly out of ideas, search a few high-star practice project homepages and copy their structure; faster than imagining from scratch.

## Q74. What is GitHub Pages, and how to turn a repo into a personal homepage or resume?

Pages is GitHub's free built-in static web service that turns your repo into a site reachable by URL. A common use is a personal homepage or resume: upload your web files to the repo, enable Pages in Settings, pick the branch and folder, and visit it at username.github.io/repo-name.

It fits resumes, project description pages, and docs perfectly. Versus a PDF resume, an online page shows skill, shares easily, and updates instantly; an interviewer clicks a link to view. For those avoiding complex site tools, Pages is the laziest way to turn a repo into a public portfolio. You need not be a front-end expert; resume templates are everywhere, download, edit text, upload, and Pages only publishes it, pushing the tech bar for self-showcase to the floor. Some even host class schedules or reading lists on it; it is free, and one more public entry means one more chance to be seen.

Copy-paste template (use directly):

```html
# 1. Create a repo named: username.github.io
# 2. Upload the index.html below
# 3. Settings - Pages, pick a branch, visit https://username.github.io

<!DOCTYPE html>
<html>
<body>
  <h1>Hi, I am XXX</h1>
  <p>This is my GitHub homepage</p>
</body>
</html>
```

## Q75. Do I need to buy a server and domain for a Pages site, is it enough for ordinary people?

No need to buy. Pages hosts for free and ships a username.github.io domain; once the repo enables Pages you use it directly, saving both server and domain. It only supports pure static pages (HTML, CSS, JS) and cannot run back-end programs, but for resumes, portfolios, and description pages it is plenty.

If you later want a custom domain, you can bind it separately, but that is a bonus not a must. For ordinary people, getting it running at zero cost beats fussing over domains. Many stall at the buy-a-domain step and never build the site. Run on the github.io domain for a full month first; consider a custom domain only after real visitors arrive, and do not reverse the order. The free plan covers most personal display needs; do not let side details delay the main task. Upgrade later once the homepage has steady visitors, by then you know what you actually need. Many run on the github.io domain for a year or two without switching and still land interviews from their homepage.

## Q76. How do I get my homepage to rank high when a recruiter searches my name?

Both your GitHub profile and your username.github.io site get indexed by search engines, so step one is to put the homepage link where you control it: resume, blog, and social bio all filled in, so these results surface when others search your name. The homepage itself ranks by being complete.

Write a clear README for every repo, pin a few representative works or add descriptions, and the profile looks substantial. Rather than study ranking tricks, make the homepage active and clear; HR often checks GitHub directly, and a tidy homepage persuades more than writing familiar with programming on a resume. Also put the homepage link in your email signature and resume header; place it wherever a contact field exists, since appearing in others' sight beats waiting for search, and exposure is made not waited for. Casually fill the GitHub link on LinkedIn too; overseas recruiters will follow it to your work.

## Q77. How to make my GitHub homepage look cool (dynamic stats, templates), done in 10 minutes?

GitHub has loads of ready-made profile templates and dynamic stat cards; no need to design from zero. Search github profile readme template to find templates with dynamic cards like language share and consecutive contribution days; copy and edit the name and info to use.

The trick is these cards read your public contribution data and auto-generate images; placed in the homepage README they move. Ten minutes is enough for a decent version. Ordinary users should not chase complexity; pick a clean template, worth more than hours tuning style. Most templates are open source and free; pick one with high stars and recent updates so the author maintains it and you hit fewer bugs. Do not get greedy; cool is a result not a goal, and steady content updates naturally make people think you are cool. Card updates rely on your continued commits, so rather than fiddle with style, keep the repo moving weekly and the data looks good on its own.

## Q78. I see an open source project I like and want to help, but I cannot code at all, what can I contribute?

You can contribute far more than you think, and without code. Typo fixes, translations, and clearer usage steps are real contributions; reporting a clear bug, answering newcomer questions, doing design or writing tutorials are all welcome by maintainers.

What open source lacks most is often who makes it more understandable and usable; coding comes second. Start from your strength: good writing fixes docs, careful eyes report bugs, design skill makes art. Many projects open welcome or help wanted boards to recruit help; even translating one paragraph is a timely help. Open source kindness goes both ways; you help it and it puts your name among contributors, the positive loop being why many stay. Many projects even run a docs group with meetings open to newcomers; you are not alone, ask directly what you lack, since the community welcomes those who reach out.

## Q79. Do typo fixes and doc additions count as contributions, does the author really welcome them?

Yes, and this is the lowest-bar, least-rejected contribution. Many projects have errors in docs and sample code that maintainers cannot fix alone; you fix one typo or add one unclear sentence and they could not be happier. In open source, doc contributions are respected as much as code.

Do not think small things are nothing; many small fixes make a project better. Make your first PR a doc fix; once the flow works, code later will not scare you. What maintainers fear most is no one willing to reach out; how little you change does not matter. Many big projects' first contribution is a doc fix, and maintainers thank sincerely on merge, a feedback loop that hooks you. What you think trivial is often someone's long-stuck annoyance; low bar does not mean no value, quite the opposite, it is the most needed. Maintainers often list doc contributors separately in thanks; your name appears on the project home with them, a recognition solider than a like and a line you can write on a resume.

## Q80. Is the good first issue label for newbies, and how to use it for a first step?

Exactly for newcomers. Many open source projects tag tasks fit for a first try with good first issue, meaning the work is simple and someone will guide you, meant for practice. Filter this label in the repo Issues, pick one you understand, change by its steps, then open a PR.

Many newcomer-friendly projects carry this label, and authors recommend starting here. It skips the task-picking dilemma and drops you straight into the flow, the steadiest entry for a first step. When filtering, prefer repos with this label and recent merges, meaning someone truly mentors newcomers and will respond. Pick one with clear steps and follow; the first contribution often goes smoother than imagined. Do not be greedy and open several at once; finishing one full flow is most valuable. After going through, write a short post on the experience; it helps the next newcomers and keeps a record for yourself, a showable footprint far more convincing than saying you can do open source.

## Q81. I want to suggest or report a bug to someone's project, how to write an Issue that is not ignored?

Writing a good Issue has four steps: first search existing Issues to avoid duplicates; pick the project's template; state three elements: symptom, steps to reproduce, and your environment (system version); add a fitting label. A good Issue looks like this: title states the problem, body states what you clicked, what you entered, and where expected differs from actual.

A bad Issue is just one line saying the software crashed again, which no one can help with. Remember one Issue says one thing; questions on how to learn programming go to Discussions, not mixed in. The clearer you describe, the faster others help, and you practice expression. A good Issue also keeps a polite tone and attaches screenshots; maintainers prefer helping those with good attitude, treating them as collaborators not support, and communication quality decides whether your problem gets solved. Search existing answers before writing also shows sincerity. Treat the other as collaborator not support and they reach out more; this is near-unspoken etiquette in open source.

Copy-paste template (use directly):

```text
[Title] [Bug] Login button unresponsive on click in Safari

[Symptom] Clicking login does nothing
[Reproduce] 1. Open home 2. Click login 3. No response
[Environment] macOS 14 / Safari 17 / App v2.3

(one Issue says one thing; the clearer you describe the faster others help)
```

## Q82. What exactly is a Pull Request (PR), and how does it differ from editing a file directly?

A PR hands the original author a finished homework asking him to grade it: please merge my change into the main repo. Editing a file directly usually means editing in your own repo on the web, which only affects you; a PR is the collaboration flow where you Fork a copy, change it, open a PR, and only after the original author reviews and approves does it merge into the original project, visible to all.

So a PR adds a review step, and that review is exactly what keeps quality and avoids messy changes. To contribute to open source, the standard move is Fork, change, open PR, not editing someone's repo directly. A PR makes changes traceable and discussable, the bedrock of large-scale open collaboration. Editing your own repo is invisible to all; a PR lets the world see your participation record, and even one line through the full flow makes you a formal contributor, credit being the hardest currency in open source. Even fixing one punctuation, going through Fork, change, open PR, you have formally stepped into collaboration.

Copy-paste template (use directly):

```text
Title: Fix login button misalignment in Safari

Description:
- Why change: style misaligned in Safari
- How tested: verified locally on Safari 17
- Related Issue: Closes #123

(one PR does one thing; writing Closes #number in the description auto-closes the Issue on merge)
```

## Q83. My first PR got rejected, does that mean I am no good, or is it normal?

Totally normal, and in no way means you are no good. Code Review asks someone to glance before merge; the review targets the code not you, and being asked to change is ordinary daily life. Every senior engineer has been reviewed hundreds of times; no need to delete the repo and run after feedback.

Treat feedback as free guidance; respond point by point, push again on the same branch after changing, and the PR updates automatically, no need to reopen. A PR is a conversation; polite talk and small fast steps suffice. Many projects even encourage more PRs for practice; rejected then changed and resubmitted is the norm, no one holds grudges. See each feedback as free one-on-one tutoring, and you improve faster than slogging alone; what blocks newcomers is not rejection but fear to open a second PR. Many project homes post contributor stories where most people's first PR was sent back to rewrite, so you are not alone. Rejection is just the most ordinary link in collaboration; even senior maintainers often get change requests, the only difference being they change then resubmit.

## Q84. What is the difference between Discussions and Issues in a project, and where should I talk?

Simple split: Issues are repair tickets for concrete things like bug reports and clear feature requests; Discussions are the water cooler plus bulletin board for ideas, usage questions, and announcements, lighter than Issues. Go to Discussions for Q&A and brainstorms, go to Issues for clear bugs and features, do not reverse.

The two pair with a Projects board for progress; the trio is Issues for tasks, Projects for progress, Discussions for ideas. After clarifying a need in chat, one click turns the discussion into an Issue to enter development. Newcomers often err by asking how to use this library in an Issue; the right place is Discussions Q&A, and only the right place gets someone to pick up. Clear rules give the community a good first impression and show you know basic collaboration etiquette. The Projects board also lets you see where your requested feature ranks; watching it move from to-do to done feels great.

## Q85. I want to use GitHub to manage my own writing, notes, and materials, how is it stronger than a net disk?

Stronger because it records versions. GitHub is like a code safe plus time machine; each save is a node, and you can return to any historical version, recovering mistaken deletes and edits, which a normal net disk cannot give. Writing in plain text or Markdown is most comfortable, with additions and deletions visible at a glance.

Worried about privacy, build a Private repo, invisible to others by default. Cross-device sync is easy; pull it down on another computer. For those who love writing, it is a cloud note with rollback, steadier than mere file storage. GitHub's free private repo quota is enough for personal use, so sensitive notes store safely. Compared with hunting backups and fearing overwrites, this certainty matters hugely to writers; long-term writers fear version chaos most, and it cures exactly that. Plain text takes tiny space; thousands of notes will not fill a free repo, no pressure to accumulate, and one day you can export and pack it all away, locked to no platform.

## Q86. I heard GitHub can auto-run tasks (Actions), what can ordinary people use it for?

Actions is the auto-worker robot in GitHub; you set rules and it runs automatically on triggered events. Scenarios ordinary people find useful are many: run a backup on a schedule, auto-post content daily, deploy the web page automatically after pushing code.

Its marketplace has many ready templates, many usable by editing config, no need to write complex code yourself. For example, if you want your personal site to publish on every update, attach a ready workflow. No need to know the principle; knowing how to use a template saves repeating labor. Search github actions template in the marketplace to copy directly; many run without reading code, just fill a few parameters. Ordinary people use it for scheduled backups and auto weekly reports, enjoying automation with zero code; do not fear the word automation, it is just a set scheduled task. Worried about mistakes, the workflow only emails you if it fails and will not touch any existing file in your repo.

## Q87. Can a non-coder use the Copilot command line to operate GitHub for me?

Yes. GitHub has a Copilot command line tool; you tell it in plain words what you want, and it writes the matching command for you, and can also explain what an unfamiliar command does. After setup, two short aliases are most used: one suggests commands, one explains commands.

It asks for confirmation before running, so no fear of it acting wild. For those unfamiliar with commands, this is like having an always-on helper, so you will not shy from GitHub operations for forgetting instructions. After install it stays in the command line; ask any operation you think of, no need to flip tutorials. For non-technical users, it turns GitHub from command-line fear into chat-style operation, a big friendliness boost; dare to ask and dare to use, which is exactly its point. It also breaks a long complex operation into steps you understand, learning while doing and incidentally memorizing commands, until you can type alone without it, which is its true value.

## Q88. Use GitHub plus jsDelivr to build a free image host, CDN-accelerate blog images?

Yes, a classic play for many. Upload images to a public GitHub repo as storage, then use the jsDelivr CDN to speed access; in the blog paste the accelerated link directly, and images load faster and steadier. Config is not complex, but two things to note.

One, the repo is public, so do not upload private images; two, do not stuff the repo too large, past a certain size it risks manual review or even cleanup. For occasional bloggers this free plan is enough, just do not treat it as unlimited disk and pour in. Ready image-host tools upload with one click and auto-apply the accelerated link, no manual address stitching. Newcomers use the tool for peace of mind; remember to build a separate repo just for images, not mixed with code for hard cleanup, and clear placement keeps this free plan stable for long. With many images, build subfolders by year for easy find and cleanup, not all in the root, or months later you cannot tell which is which.

Copy-paste template (use directly):

```text
# Use images in the repo as external links (public repo)
https://cdn.jsdelivr.net/gh/username/repo-name@main/image-path.png

# Example: images/logo.png in repo my-blog
https://cdn.jsdelivr.net/gh/my-blog/my-blog@main/images/logo.png
```

## Q89. Earn via open source tips (GitHub Sponsors), do real people pull it off?

Real people do, and GitHub is generous with this money: the platform takes no cut, and the sponsorship amount goes one hundred percent to the developer. The logic is, the project you maintain helps others, and they can sponsor you monthly or one-time via Sponsors, with a Sponsor button on the homepage.

But do not mistake it for easy money: the premise is your project is truly used and contributes real value, and the platform also reviews applicants. It is a sustainable income path for continued open source contributors, not a shortcut newcomers cash in on at once. Indeed some in the circle gain steady funding via it, on the premise the project truly solves others' problems and builds trust. See it as a reward for your continued effort, not traffic cash-out; with the right expectation the road goes far. Make the project solid first and truly help others, and tips follow naturally. The platform reviews applicants, so do not slap a button on day one; opening it after real users arrive feels more natural.
