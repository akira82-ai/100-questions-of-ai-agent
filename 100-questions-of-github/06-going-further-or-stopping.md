# Chapter 6 · Want to Go Further, or Where to Stop

By this chapter, you can search, run, store, show, even dare to PR. How to walk the next road has no standard answer: some drill deeper into branches and automation, some feel enough and stop here. This chapter will not push you to advance; it only clarifies a few advanced features worth knowing and what GitHub is actually not good at, letting you judge where to go next and where to stop.

## Q90. After getting started, next learn branch management or directly collaboration?

No need to force-choose and grind. Advancement is picked by goal: want releases learn Releases, want showcase learn Pages, want less repetitive labor touch Actions. Branch is the base of collaboration, but you need not learn it through first; directly start from Forking projects, picking good first issue, opening PR, and branch usage comes naturally in practice.

Rather than learn in textbook order, first clarify what you want GitHub for, then go targeted, more cost-effective. Read tutorials ten times beats less than upload ten repos yourself; consistent use is the right path. The official advancement map is Tag for versions, Releases for publishing, Pages for showcase, Actions for automation, contributing to open source; you see branch does not occupy a separate block, it is already embedded in every collaboration step. So rather than agonize which to learn first, directly enter a real project, learn what you need on demand, this choice saves more effort than gnawing concept books.

## Q91. In multi-person projects what does Code Review actually examine, how to avoid being picked on as a newbie?

It examines whether logic is right, whether edge cases are missed, whether new bugs or performance issues are introduced, whether naming and comments are clear. Key point: review targets the code, not you, so do not be defensive, treat feedback as free guidance.

Newbies should remember most: nobody wants to review a huge PR, keep one change within reviewable size; on feedback respond point by point, change and push the same branch, auto-update, no reopen. See Review as two people together getting things right; being questioned is someone covering for you, a good thing. A good review gives specific suggestions, like here a loop is more readable, not just dumping "what is this"; the Suggestion feature can directly give a fix snippet for the author to adopt with one click. Conclusions are three: can merge, has thoughts but not blocking, must fix before merge. As the submitter, politely state reasons where you disagree; not all feedback must be taken as-is.

## Q92. Can Projects board be used as project management, stronger than Excel where?

Yes, and naturally wired with code tasks. The board treats Issues and PRs as sticky notes, drag to todo, in progress, done, progress visible at a glance; also add owner, due date, priority fields, switch table view to filter. Its base is still Issue/PR; deleting the board does not affect original tasks, more reassuring than Excel, you no longer sync task status in two places.

For personal todo, release tracking, light planning, enough; more than pure tables it has the real-time feel tied to code, especially handy in collaboration. Remember the board card only means something if you drag it on start and finish; otherwise it expires fast. It forms the collaboration trio with Discussions and Issues: Issue manages things, Projects sees progress, Discussions chats ideas; with all three collaboration does not lose way. Versus Excel where you manually move status, the board pulls tasks directly from the code repo, saving that sync effort.

## Q93. Actions auto-build, deploy sounds advanced, should newbies touch now?

Yes, but first apply ready templates, do not rush to write complex workflows yourself. Actions runs a task automatically after some event; the most useful for ordinary people is hanging a ready template for timed backup, or auto-publishing the personal site on each update; search "github actions template" in the marketplace to copy, many run with a few params.

You do not need to know its internals now; know how to apply templates and hand repetitive labor off. When you really have automation needs then learn deep; not knowing principles does not block using it first. The marketplace has many ready workflows; newbies tweak config to use, like others' written "run tests on each push", "auto-deploy on web change", copying steadier than writing from zero. Really contributing to open source, remember read the project's CONTRIBUTING guide before PR, do not crash in. Treat Actions as an obedient auto-worker; you give instructions it executes; first run the simplest backup and publish smoothly, then talk complex play.

Copy-paste template (use directly):

```yaml
name: CI
on: [push]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: echo "auto-run on each push"

# File at: .github/workflows/ci.yml
```

## Q94. Actions' "variables" and "cache" solve which pain points?

Variables solve the pain of writing the same value everywhere, change one place must change many: env manages values inside a single workflow, vars in Settings manages values shared across workflows even across repos, change once global effect. Cache solves the pain of reinstalling dependencies every run: store dependencies like node_modules by key, next hit skips install, build time from minutes to tens of seconds, dependency change auto-refreshes key.

Both ultimately help you do less repetitive labor, among advancement the two most worth knowing. Variables also pass values across steps and jobs: a step's computed result written to the env file, later steps read directly; upstream job defines output, downstream references. Cache has boundaries to know: single repo limit 10 GB, no access for 7 days auto-clears, isolated by branch, so do not stuff sensitive info like keys into cache. Understand these two, your automation is both fast and not silently erroring.

Copy-paste template (use directly):

```yaml
- name: Cache node modules
  uses: actions/cache@v4
  with:
    path: ~/.npm
    key: ${{ runner.os }}-npm-${{ hashFiles('**/package-lock.json') }}
    restore-keys: |
      ${{ runner.os }}-npm-

# Cache limit 10GB/repo, auto-clear after 7 days unused, isolated by branch
```

## Q95. Shortcuts and command palette efficiency folks use, which most worth remembering on day one?

Remember these few: any page press `?` pops all shortcuts of the current page, the laziest memory method; `G` navigation keys, G C jump code, G I jump Issue, G P jump PR, G A jump Actions, move without leaving the keyboard; `y` freezes the file URL into a permanent link; `t` quickly finds files in big repos; `.` opens github.dev editor to edit directly.

When you cannot remember shortcuts, press Ctrl or Command plus Shift plus K to open the command palette, type to jump directly, the fallback entry when you forget. In the command palette press `#` to search Issues and discussions, `@` to search users and repos, `/` to search files in the repo; when open press `>` to switch to command mode to run operations like create repo, switch theme directly; Esc or press the shortcut combo again to close. If you fear pure-character shortcuts mis-trigger, in account Settings' accessibility options you can turn them off, keep only modifier-key ones.

## Q96. What is the use of pressing "y" for a permanent link, why not send the current URL when sharing code?

Ordinary file URLs carry the branch name, like /blob/main/; once the branch advances, content changes; the link you copied today may not be the original when others click later. Pressing `y` replaces the branch name in the URL with a specific commit ID, generating an unchanging permanent link, what the other sees is exactly what you saw.

It can also generate a permanent link for one or a few lines of code, especially handy when quoting in Q&A and discussion. So whenever you want to reference a code segment long-term, press `y` then copy, steadier than sending the current URL. The reason ordinary URLs drift is they point to the branch's latest head; new commits change content; while the permanent link replaces the branch name with a commit number nobody can change. Actually URL can hold branch name, commit number, or tag; as long as it locates a commit it is stable. Any page press `?` calls all shortcuts; y is just one that helps you fix the reference.

## Q97. Can the hover card let me see what a link is without clicking in?

Yes, this is a tab-saving trick when reading GitHub docs. In Docs, focus on a link to an article, press Alt or Option plus Up arrow, a hover card pops, previewing another article's summary, no need to jump away from the current page. Mouse hover also triggers; after the card opens press Enter to follow the link, Esc to close.

It is operable purely by keyboard, paired with the `?` shortcut and command palette mentioned earlier, reading docs noticeably more efficient, fewer tabs opened. It only takes effect on the GitHub docs site; most links between articles support it. Besides keyboard, mouse hover also pops the card; in the card press Enter to jump, Esc to collapse, both ways work. Paired with `?` for shortcuts and command palette direct jump, the trio used together, you do not need a screen full of tabs when reading a long doc string, and your train of thought is not broken.

## Q98. How to set Copilot CLI aliases, how many characters saved?

For GitHub Copilot command line, two short aliases are most practical: ghcs replaces gh copilot suggest, suggests commands, ghce replaces gh copilot explain, explains commands. Key is you cannot handwrite a normal alias; you must use the official gh copilot alias command to generate it, so it can execute commands for you; for example Zsh users add that eval line to ~/.zshrc.

After config ghcs asks for confirmation before executing by default, no fear it acts recklessly. Beyond fewer characters typed, those unfamiliar with commands dare to ask it directly. One pit when setting: you must run the official eval command to write the alias into the shell config; a hand-written normal alias looks the same but Copilot cannot execute commands for you. After config, gh copilot config can also change the default confirm behavior; if you do not want to contribute anonymous usage data, turn off Optional Usage Analytics in the same settings. Configure once, save long-term.

Copy-paste template (use directly):

```sh
# Zsh / Bash: add to ~/.zshrc or ~/.bashrc
echo 'eval "$(gh copilot alias -- zsh)"' >> ~/.zshrc

# Then use two short aliases:
ghcs   # = gh copilot suggest (suggest commands)
ghce   # = gh copilot explain (explain commands)

# Note: must use the official alias command to generate, cannot handwrite a normal alias
```

## Q99. At what point is it "enough", what deep areas need not hard-grind for ordinary people?

The standard for enough is simple: if you can get things done via web, Fork, PR, README, Pages, that is enough. Do not envy those who memorized Git commands fluently; for most ordinary people, web can upload and edit, can collaborate, already uses GitHub's most valuable part. No need to hard-grind a string: rebase, cherry-pick such complex Git commands, writing Actions workflows from scratch, branch internals, and CI's fiddly config.

These are not needed now, but when you really hit a snag, looking up is soon enough. GitHub's advanced features are too many to finish; hard-grinding easily puts people off; put energy into the part you can use immediately, the rest as a look-up dictionary, which is the ordinary person's labor-saving posture. Rather than memorize commands, consistent use is the right path; read tutorials ten times beats less than upload ten repos yourself for hands-on feel.

## Q100. What can GitHub not solve, what is it actually worse than dedicated tools?

It is strong in the chain of code, version, collaboration, open source, showcase, but a few types of work it really is not good at: pure file sync it is less handy than net disks like Nutstore, OneDrive; real-time discussion less fast than group chat, Discussions leans to announcements and slow chat; running backend, storing data it cannot, Pages only serves pure static web; complex project management it loses to professional tools like Jira.

So do not mythologize it; treat it as the hub of collaboration and showcase, hand heavy work to dedicated tools, clear division uses it more happily. One reminder: open source is not free-for-all; every project carries a License, before commercial use check whether and how to attribute. Set expectations right; in your toolbox GitHub should be the hub managing code, collaboration, showcase, not a place to stuff everything. It solves the chain from writing software to shipping to joint editing; work outside that chain, hand to more suitable tools, more efficient.
