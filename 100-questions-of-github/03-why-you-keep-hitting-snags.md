# Chapter 3 · Why Do I Keep Hitting Snags? How to Avoid the Most Painful Ones

Getting snagged is something almost nobody skips. Sooner or later you will hit a push error, conflict markers, or slip and upload something you should not. This chapter is not to scare you; it is a dictionary-style first-aid card: hit which pit, flip to that question, follow along. No need to memorize first; come back when a problem arises. Remember one mantra: most lost code can be recovered with reflog, do not panic.

## Q35. Push says password auth removed, why does typing the password per tutorial fail?

You follow the old tutorial typing the password, Git errors authentication failed, not that you forgot the password, the rule changed. GitHub no longer supports account-password login on the command line; this is a platform-wide change the old tutorials did not catch up with.

Now there are two auth paths: either SSH keys, configured once and auto-allowed later; or a Personal Access Token, used as the password. The token is generated in GitHub settings, looks like a string of gibberish, much longer than a password.

Many get stuck exactly here: the tutorial says password, the platform wants token or key. Switch auth to one of these two and the error vanishes.

If you mainly use web or desktop, the tool usually handles auth for you, no token to manage. Only command-line push forces you to face this. Configuring SSH early is the cleanest way to dodge this pit.

## Q36. Slipped and committed a key, password, even an ID number into the repo, how to erase thoroughly?

First lock this in: once a key is uploaded, treat it as already leaked by default; the safest move is immediately revoke and reset that key on GitHub, do not trust that just deleting the file is safe.

If you just committed and have not pushed to GitHub, it is simple: delete it from the repo, add a .gitignore to exclude it, commit again to overwrite.

If you already pushed, adding .gitignore alone is not enough because the file is still in history. You must use a dedicated cleanup tool to wipe that history segment, then delete the file on GitHub and reset your token or key. Never use reset --hard to hard-delete; that leaves a trace in history and makes it worse.

The most worry-free is prevention: configure .gitignore from the start, keeping password files like .env out the door. Never upload a key early; once uploaded, treat as revoked.

## Q37. .gitignore written wrong, a pile of junk files got uploaded, how to fix?

.gitignore is a blocklist; files written in it are auto-ignored by Git. If you find .DS_Store, node_modules and such junk uploaded, the rules are likely wrong, or the file was already tracked by Git before the ignore rule was written.

First check the rules themselves: one per line, # starts a comment, * is a wildcard, trailing slash ignores only folders. One extra slash in the path may break it; use git status to verify what is still tracked.

A more common pit: the file was already committed, then writing it into .gitignore is invalid because Git is already managing it. Then you must unstage, use a command to remove the file from the repo while keeping it locally, then commit once, and it is truly ignored.

Finally remember to commit .gitignore itself into the repo, so everyone shares the same ignore rules. Configuring .gitignore at project start is far easier than fixing later.

Copy-paste template (use directly):

```text
# Comments start with #
.DS_Store            # macOS system file
*.log               # all log files
node_modules/       # dependency directory (trailing / means directory)
.env                # key/password file (never commit!)
dist/               # build output directory

# Tip: pick a .gitignore template when creating the repo, or search gitignore.io to generate online
```

## Q38. Commit messages a mess like "fix" "update", can't understand my own changes later, any rescue?

The commit message is the title you write each time you save. Newbies often write "fix", "update", a week later they cannot understand what they did that day.

First memorize the three standards of a good message: start with a verb stating the action, like "add login page", "fix button misalignment"; keep it to one line; if team collaboration, add a type prefix, like feat for new feature, fix for bug, docs for docs.

If you wrote wrong, there is a rescue. If the latest commit is wrong, or you missed a file, use the amend command to modify that most recent commit, no extrarecovery commit. But note: this rewrites history, only for local commits not yet pushed; do not touch already-pushed ones.

A good message is like a diary title; half a year later one glance tells what you did that day. Each commit around one clear small goal makes rollback and troubleshooting easy.

Copy-paste template (use directly):

```sh
# Good commit messages: verb first + say what changed
git commit -m "fix typo in README"
git commit -m "chore: add .gitignore"
git commit -m "feat: add login button"

# Common prefixes: fix bug / feat feature / docs documentation / chore chores
```

## Q39. Want to undo the last commit, reset, revert, checkout, which to use?

All three relate to undoing, but differ a lot in danger; do not misuse.

Haven't committed, just changed a file and want to drop it, use restore or the old-style checkout; they only touch the working area, not history, safest, re-edit if wrong.

Already committed, want to erase some history, two choices. revert creates a new commit that undoes that operation, original record fully kept, like posting a correction notice; team projects' first choice, never loses history. reset is the other, especially with hard it directly drops later changes, and do not use reset recklessly on commits already pushed to GitHub, it messes others' code.

When unsure, default to revert; it is least likely to cause trouble. Only for local, unpushed, pure personal draft consider the dangerous reset. A rhyme: public history uses revert, private draft uses reset.

## Q40. Merging branches spews conflicts, what are those <<<<<<< symbols?

Those symbols are not a bug; Git is asking you to decide. A conflict happens when two people changed the same line in the same place; Git does not know whose to listen to, so it lays the multiple-choice before you.

Open the conflicted file, you see three things: between <<<<<<< and ======= is the current branch content, between ======= and >>>>>>> is the incoming content. Keep the version you want, delete all three marker lines cleanly, and the file is fixed.

After deleting markers do not forget two steps: add the file back to staging, then commit once, conflict resolved. Miss these two and the merge is not finished.

If manual is tedious there is a lazy way: open the conflicted file in VS Code, the interface has buttons to accept current or accept incoming; or resolve online in the PR on the GitHub web. On conflict do not panic: read markers, keep the right, delete markers, commit, four steps done.

## Q41. git add single file or whole directory, and how to undo if wrong?

What follows git add is which files you want Git to notice this time. Differentwording, different scope.

Most precise is adding a single file, moving only that one into staging; recommended for newbies, slower but steady. For convenience you can add all changes in the current directory, but it adds unnoticed temp files too; always git status before adding to avoid mistakenly adding password files or dependencies.

There is also a chunk-add mode, committing only some changes within a file, making each commit more thematic.

Wrong add is fully undoable, no content lost: use restore to pull the file from staging back to working area, you can keep editing. Oldwording uses reset with filename, same effect.

Practical combo: git status to see state, precisely add what you want, status again to confirm. When unsure, add file by file; use directory add after proficiency.

## Q42. Why commit after add, one line on what staging actually blocks?

Many feel add then store directly is done, why the staging middle layer. Answer in one line: let you record history in batches and logically.

Git manages files like photo snapshots, in three layers. The normal folder you are editing is the working area, Git not yet managing; the list you pick to save is the staging area; the place that permanently saves history is the repo. Flow: working area via add to staging, then via commit to repo.

The value of staging: you changed ten files but this time only want to commit three related ones, so add only those three. It turns history from a mess into themed snapshots.

Remember a pit: changed but not added then directly commit, this commit has none of your changes, because commit only recognizes staging. Always git status to see which layer a file is in; the most valuable habit for newbies. Lock the three-layer analogy with photo snapshots, and every add or commit later you see through at a glance which layer the file is in.

## Q43. Those red and green files in git status, what do they mean, how to read without panic?

git status is the command to type when unsure what to do next; it tells you in plain words where you are and what you are holding.

The colors hint file state. Red usually means not yet noticed, changed but not in staging; green usually means already in staging, waiting to commit. You do not need complex definitions; just understand what changes I have now and whether they are ready to commit.

It also tells you which branch you are on, whether there are changed-but-unadded files, added-but-uncommitted files. Tap it before and after each commit for peace of mind.

Beyond status, a few searchlights: log flips the history book, diff sees uncommitted differences, checking before commit avoids mistakenly uploading passwords, show zooms into a single commit. Newbies who lose things do not panic; most can be found via reflog, the operation black box. First status, then act, steady basic skill.

## Q44. After committing I find a mistake, but don't want an undo record, any clean way?

If you worry undo leaves an ugly trace, revert is exactly for you. It does not tear the original; it posts a correction notice on history.

Specifically, revert creates a new commit whose content undoes that operation. The original commit stays fully in history, only its effect is canceled by the new commit. So history is clean and continuous; others see what you did and what you corrected, no blank gap erased.

This matters especially in team projects: everyone shares the same history; if you tear a commit, others' records mismatch. With revert, nobody is affected.

Compare: the dangerous reset truly erases history, and do not use reset recklessly on pushed commits. When unsure, default to revert; it never loses history, the least troublesome. Public history uses revert, private draft uses reset.

## Q45. Two people changed the same file, my change got overwritten, how to prevent early?

First clarify a fact: following normal Git flow, your change will not be silently overwritten. When Git meets two people changing the same place, it does not pick a side on its own, but lays the conflict for you to decide. The real problem is often not pulling latest before merging.

The key action to avoid overwrite: before merge or push, first pull to bring others' latest changes. If then you find both sides changed the same line, Git marks a conflict, you decide which to keep, instead of one side silently swallowed.

Build the habit: git status before acting, always git pull before merge, or you may overwrite others' new code or spawn unnecessary conflicts.

If you use it alone, no collaboration, almost no overwrite issue; overwrite only happens when multiple people change the same place without syncing first. If conflict already happened do not fear, it is not an error, it is Git asking you to decide. Read markers, keep right, delete markers, commit, four steps solve it. Pull early beats firefighting later.

## Q46. Following tutorials but always stuck at first push, what are the three most common breakpoints?

First push stuck comes down to three breakpoints.

First: not a git repository. This error mostly means you are not inside the repo folder; before typing commands confirm the current directory is right and has that hidden .git folder.

Second: push rejected, non-fast-forward. Means GitHub has commits you do not have locally, usually someone pushed first. Easy fix: pull to merge, then push.

Third: auth failed, keeps asking for password. Not a wrong password, GitHub long dropped password login on command line; switch to SSH key or token.

These three almost everyone stepped on. One mantra: when in doubt first git status, then git log, info is all there; try an uncertain operation in a test repo first. Most so-called stuck is locatable by reading the keyword in the error.

## Q47. Pull others' code errors "unrelated histories", what is it saying?

This says Git refuses to merge two commit histories with no common ancestor. The most common pit: you locally git init and committed a few times, then pull a repo on GitHub that already has a README; both have their own root, Git dares not blind-merge. From Git 2.9, merge and pull reject such merges by default, a safety guard against accidentally gluing two unrelated projects.

If you really want to merge, add one line: git pull origin main --allow-unrelated-histories (use master if the branch is master). This flag tells Git I know they are unrelated, stitch anyway. The root fix is simpler: create an empty repo on GitHub, do not check initialize README, or clone first then put files, avoid two independent histories from the root.

## Q48. Collaborating, my push rejected, says pull first, pull conflicts, dead loop how to break?

This is not a dead loop; the flow is not finished. Many newbies think they are in a dead loop, but breaking the three steps apart, each looks like an error, combined they are normal collaboration rhythm.

Push rejected, pull first, means remote has commits you do not have locally. Do not panic, pull those down. Pull merges others' changes into your local first; if two people changed the same place, conflict markers appear.

Conflict is not an error; Git asks you to decide. Open the conflicted file, delete those markers, keep the version you want, add the file back to staging, commit once, merge not finished until then. After conflict resolved, push again, this time it goes up.

Remember the chain: rejected then pull, pull conflicts then resolve, resolved then push. Always pull before merge, or you may overwrite others' new code. Step through and the so-called dead loop never appears; it is just the middle state of not finishing.

## Q49. Clone is an empty directory, but the web clearly has a pile of files?

Do not blame yourself first. Clone empty, the most common case: the repo you cloned has no commits at all, an empty repo; Git clearly tells you "cloned an empty repository", not your mistake, the source repo really has no content.

Another case: branch mismatch. A repo may have multiple branches; the files you see on the web may be on a non-default branch. Clone by default only pulls the default branch; you can switch branches to see if others have content.

Another possibility: the address you cloned is not the repo you meant; a wrong link pulls an unrelated empty place.

Troubleshoot order is simple: first see if the clone message has "empty repository"; then confirm the address; last check which branch those web files are on. Most empty directories locate in these three steps; you did not lose files.

## Q50. Repo suddenly shows inaccessible or 404, am I banned or wrong link?

Steady first; most 404s mean the link or repo itself is the problem, not that you are banned.

From the platform's returned info, 404 usually means wrong path: the owner/repo address you visited is wrong, or that repo does not exist. Common cases: repo renamed, deleted, set private, or your copied link missed a segment.

Verify yourself: paste the address into a browser incognito window, see if everyone is blocked; compare the repo home address format, confirm owner and repo segments are both spelled right. If it is a private repo, those unauthorized see 404, which does not mean your account is abnormal.

Real account bans are rare, and usually have a clear ban notice, not just a 404. So on 404, first check link and repo state, do not rush to suspect you are banned. Confirm address correct, repo exists and visible to you, problem basically solved.

## Q51. Deleted .git by mistake, lost a branch's code, wrong branch, how to rescue these crashes?

These three crashes have separate fixes, but one general mantra: most lost code can be found via reflog, do not panic.

Deleted the .git folder by mistake, local history is gone. If you previously pushed to GitHub, you can re-pull from the cloud, minimizing loss; if not pushed, the changes in the working area still exist, only history broke, re-init and continue.

Lost a branch's code, or committed to the wrong branch: switch to the correct branch, use cherry-pick to move that commit over as-is; if changed wrong branch but not committed, use stash-change, switch branch, restore-change to transfer, clean.

Misused reset and lost commits, immediately use reflog to find that commit number then reset back. reflog is your operation black box, even hard-deleted commits leave records.

So on crash do not panic; first think did I push, can reflog find it, most are rescuable.
