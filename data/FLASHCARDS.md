# Git Flash Cards

**How to study:** open this file in preview (`Ctrl+Shift+V`), read the question,
answer it out loud or in your head, *then* click to reveal. Or say
**"quiz me"** in chat, and the instructor will quiz you, weighting cards you've missed.

Cards are added only after you've actually seen the concept in a lesson, so
nothing here spoils an upcoming prediction.

Tags: `concept` (an idea), `command` (what a command does), `message` (how to
read Git's output), `cursor` (the Cursor interface), `safety` (avoiding or
fixing mistakes).

---

## L0: Git vs GitHub vs Cursor, and your first repo

**1. What is Git?** `concept`
<details><summary>Answer</summary>

A program on your computer that records snapshots (history) of a project's
files. It works entirely locally, with no internet or account needed.
</details>

**2. What's the difference between Git and GitHub?** `concept`
<details><summary>Answer</summary>

Git is the local version-control program. GitHub is a website that hosts
copies of Git repositories and adds team features: pull requests, reviews,
automated checks. Git works without GitHub; GitHub is built on Git.
</details>

**3. What does Cursor's Source Control panel actually do?** `cursor` `concept`
<details><summary>Answer</summary>

It's a set of buttons that run Git commands for you. Anything it does can be
typed in the terminal, which is why you learn the command first.
</details>

**4. Name Git's three areas, in the order a change moves through them.** `concept`
<details><summary>Answer</summary>

1. **Working tree**: the files on disk, where you edit.
2. **Staging area** (also called the index): changes selected for the next snapshot.
3. **Repository**: the permanent history of snapshots (commits).
</details>

**5. What is the `.git` folder?** `concept`
<details><summary>Answer</summary>

The repository itself: the hidden database that holds the project's history.
A folder with no `.git` (in it or any parent folder) is not a Git repository.
</details>

**6. What does `git status` do?** `command`
<details><summary>Answer</summary>

Reports the state of the repository you're in. It first finds the repository by
looking for a `.git` folder in the current folder, then in each parent folder.
It does not contact the internet.
</details>

**7. You see `fatal: not a git repository (or any of the parent directories): .git`. What does it mean?** `message`
<details><summary>Answer</summary>

Git searched this folder and every folder above it and found no `.git` folder,
so there's no repository here. `fatal` means Git stopped; nothing was changed
or harmed. Fix: `cd` into the right folder, or run `git init` if you intend to
start a new repository here.
</details>

**8. What does `git init -b main` do?** `command`
<details><summary>Answer</summary>

Creates a new, empty repository in the current folder by making a hidden
`.git` folder there, and names the first branch `main`. Your files are not
touched and not yet tracked.
</details>

**9. Where does a repository live? Is there a central Git library?** `concept`
<details><summary>Answer</summary>

No central library. Each repository is self-contained in its own `.git`
folder, inside the project folder. Copy or delete that folder and you copy or
delete the whole history.
</details>

**10. You ran `git init` in a folder that's already a repository and saw `Reinitialized existing Git repository`. Did you lose anything?** `message` `safety`
<details><summary>Answer</summary>

No. Re-running `git init` is harmless: it keeps the existing history. The
warning `re-init: ignored --initial-branch=main` just means the branch name is
already set, so `-b` was skipped.
</details>

**11. `git status` says `Untracked files:`. What does "untracked" mean?** `message` `concept`
<details><summary>Answer</summary>

Git sees the file in the working tree but has never recorded it in any commit
and isn't watching it for changes yet. It has nothing to do with GitHub or
pushing. `git add` is how you start tracking it.
</details>

**12. `git status` says `No commits yet`. What does it mean?** `message`
<details><summary>Answer</summary>

The local repository contains no snapshots. Nothing has been committed (saved
into history) yet. It says nothing about GitHub.
</details>

**13. What's the difference between committing and pushing?** `concept`
<details><summary>Answer</summary>

**Commit:** save a snapshot into your *local* repository (`.git` on your disk).
**Push:** send commits you already have to a remote copy, such as GitHub.
You must commit before there's anything to push. (Pushing comes in L5.)
</details>

**14. What does `On branch main` in `git status` tell you?** `message`
<details><summary>Answer</summary>

Which branch you're currently on. There's always a current branch while you
work, and new commits are added to it.
</details>

**15. Describe the journey of a brand-new file from your disk to GitHub, naming each step's command.** `concept`
<details><summary>Answer</summary>

Working tree (untracked), then `git add`, to the staging area, then
`git commit`, to the local repository (history), then `git push`, to GitHub.
The first three places are all on your computer.
Analogy: desk, then chosen for a photo, then photo in your album, then copy mailed to another city.
</details>

**16. When do you commit, and when do you push?** `concept`
<details><summary>Answer</summary>

**Commit often:** each time you finish one small, working, coherent step, or
before trying something risky. Commits are local and private.
**Push when the work should leave your computer:** to open or update a pull
request, after fixing review feedback or a conflict, or for an end-of-day
backup. One push sends every commit GitHub doesn't have yet, so you usually
make several commits per push.
</details>

**17. Name Git's three config scopes and where each is stored.** `concept`
<details><summary>Answer</summary>

- **System:** every user on this computer (written by the Git installer).
- **Global:** you, in every repo (`C:\Users\<you>\.gitconfig`).
- **Local:** this repository only (`.git\config` inside the repo).
</details>

**18. How do you check a setting's value *and* where it comes from?** `command`
<details><summary>Answer</summary>

`git config --show-scope --get <setting>`, for example
`git config --show-scope --get user.name` prints `global  Kyle Fisher`.
If it prints **nothing**, that setting isn't set at any scope.
</details>

**19. You ran a Git command and it printed nothing. Did it fail?** `message`
<details><summary>Answer</summary>

Usually not. Many Git commands are silent when they succeed. Failures
normally print `error:` or `fatal:`. Verify with an inspection command
(`git status`, `git config --get ...`, `git log`) rather than assuming.
</details>

**20. What does `git config --local core.editor "cursor --wait"` do, and why `--wait`?** `command`
<details><summary>Answer</summary>

Tells Git to open Cursor whenever it needs you to write text (such as a merge
commit message), for this repo only. `--wait` makes Git pause until you close
that tab, so Git knows you're finished. Without an editor set, Git falls back
to Vim.
</details>

**21. In the output `local   cursor --wait`, what is "local"?** `message`
<details><summary>Answer</summary>

The **scope** (which level the setting lives at), not a name. The setting's
name (`core.editor`) is what you typed in the command; `cursor --wait` is the
value. In `.git\config` it appears as `editor = cursor --wait` under `[core]`.
</details>

**22. Global says one value, local says another. Which does Git use in that repo?** `concept`
<details><summary>Answer</summary>

The **local** one, because the most specific scope wins: local beats global,
and global beats system. The global value still applies in every other repo that
doesn't override it.
</details>

**23. Why use your GitHub no-reply email for commits in a public repo?** `concept` `safety`
<details><summary>Answer</summary>

Every commit permanently records an author email, and anyone can read it on a
public repo. You can't remove it without rewriting history. The no-reply address
(`<id>+<username>@users.noreply.github.com`) still links commits to your
GitHub account but keeps your real email private.
</details>

**24. Do local settings (`.git\config`) travel with the repo when you push it or someone copies it?** `concept`
<details><summary>Answer</summary>

No. `.git\config` is never pushed or shared. Each copy of a repo on each
machine has its own local settings, so someone else's copy uses *their* global
settings unless they set local ones.
</details>

**25. What happens if you delete a project's `.git` folder?** `concept` `safety`
<details><summary>Answer</summary>

Your files stay on disk (at their current content), but the **entire history is
erased**: every commit, every branch, and the local settings. It can't be undone,
except from a copy pushed elsewhere, like GitHub. `git status` then prints
`fatal: not a git repository`. Git refusing is different from Git printing nothing.
</details>

**26. How do you quickly see what options a Git command accepts?** `command`
<details><summary>Answer</summary>

Add `-h`, for example `git config -h` or `git status -h`. It prints a short summary of
the options in the terminal. (`--help` opens the full manual instead.)
</details>

**27. `cd C:\Learning\Git Workflow Lab` fails with "cannot be found that accepts argument 'Workflow'." Why, and what's the fix?** `message`
<details><summary>Answer</summary>

PowerShell splits commands at spaces, so it saw three separate pieces. Put paths that contain
spaces in quotes: `cd "C:\Learning\Git Workflow Lab"`. Tip: press **Tab** to
auto-complete a path, and PowerShell adds the quotes for you. (This is a terminal issue, not Git.)
</details>

---

## L1: Working tree, staging, and commits

**28. What does `git add <file>` do?** `command`
<details><summary>Answer</summary>

It copies the file's **current version** into the staging area (the "tray"), so
it will be included in the next commit. It's a snapshot of that moment: if you
edit the file again afterward, the new edit is *not* staged until you
`git add` it again. Nothing is saved to history yet.
</details>

**29. What does `git commit -m "message"` do?** `command`
<details><summary>Answer</summary>

It saves everything in the staging area as a new commit in the repository (a
new page in the "album"), labeled with your message. It's local: nothing is
sent to GitHub. Anything not staged is left out.
</details>

**30. You ran `git commit` (or clicked Commit in Cursor with an empty message box) and it seems to hang. Why?** `message` `cursor`
<details><summary>Answer</summary>

Git is **waiting for you**, not stuck. With no `-m`, Git opens `COMMIT_EDITMSG`
in your editor (`core.editor = cursor --wait`) and pauses until you close that
tab. Type the message on line 1, save, and close the tab. If you close it with no
message, Git prints `Aborting commit due to empty commit message`. To skip the
editor, use `git commit -m "message"`.
</details>

**31. What do the three `git status` headings mean: `Untracked files`, `Changes not staged for commit`, `Changes to be committed`?** `message`
<details><summary>Answer</summary>

- `Untracked files`: Git sees the file but has never recorded it.
- `Changes not staged for commit`: a tracked file was edited, but the edit
  isn't on the tray.
- `Changes to be committed`: staged. This goes into the next commit.

These are fixed labels; Git always prints them the same way.
</details>

**32. In `git status`, what's the difference between `new file:` and `modified:`?** `message`
<details><summary>Answer</summary>

`new file:` means the file has never been committed before; it's entering the
repo for the first time. `modified:` means the file is already tracked and has
been changed since the last commit.
</details>

**33. What's the difference between `git diff` and `git diff --staged`?** `command`
<details><summary>Answer</summary>

- `git diff`: **working tree vs. staging** (desk vs. tray), meaning edits you
  haven't staged yet.
- `git diff --staged`: **staging vs. last commit** (tray vs. album), meaning
  exactly what the next commit will contain.

Each command compares two *neighboring* areas. Plain `git diff` never looks at the commit.
</details>

**34. In `git diff` output, what do `+`, `-`, and a leading space mean?** `message`
<details><summary>Answer</summary>

`+` = line added, `-` = line removed, leading space = unchanged context line
shown for orientation. `@@ -26,3 +26,5 @@` says where the change is (around
line 26, where 3 lines became 5).
</details>

**35. How do you unstage a file without losing your edit?** `command`
<details><summary>Answer</summary>

`git restore --staged <file>`. The file comes off the tray and goes back to
`Changes not staged for commit`, and your edit stays on disk. (Before a repo's
first commit, Git suggests `git rm --cached <file>` instead.)
</details>

**36. What's the danger of `git restore <file>` *without* `--staged`?** `safety`
<details><summary>Answer</summary>

It **discards** your uncommitted edits to that file, and you can't undo it.
Always check for `--staged` when you only mean to unstage.
</details>

**37. What does the `+` next to a file in Cursor's Source Control panel do?** `cursor`
<details><summary>Answer</summary>

It stages the file, the same as `git add <file>`. The file moves from
**Changes** to **Staged Changes**. Clicking the file name opens the diff editor.
</details>

**38. What does `(root-commit)` mean in commit output, and what does `create mode 100644 README.md` mean?** `message`
<details><summary>Answer</summary>

`(root-commit)` = the very first commit in the repo (nothing before it).
`create mode ... README.md` = this commit added `README.md` to the repo for the
first time. A commit that only *changes* an existing file has no `create` line.
</details>

**39. How do you list the files Git is tracking?** `command`
<details><summary>Answer</summary>

`git ls-files`. Untracked files don't appear in the list.
</details>

**40. What does `git log --oneline` show?** `command`
<details><summary>Answer</summary>

One line per commit: its short ID and message, **newest first**.
`(HEAD -> main)` marks the commit you're on now.
</details>

**41. What makes a good commit message?** `concept`
<details><summary>Answer</summary>

It starts with an imperative verb (Add, Fix, Update, Remove), as in "This commit
will...", is short (about 50 characters or less), and says *what* changed.
"Add Final Section heading to README" is better than "Lesson 1 - Self Test"
or "changes."
</details>

**42. What does a commit contain?** `concept`
<details><summary>Answer</summary>

- A **snapshot of the files** as they were in the staging area (the main part)
- The **author** (name and email) and the **date**
- The **message**
- A unique ID (the **hash**, e.g. `15809b4` short form)
- A link to the **previous commit** (its parent)

The metadata is the label on the album page; the snapshot is the photo itself.
</details>

## L2: History, HEAD, and .gitignore

**43. What is the `index 112149e..e53287c 100644` line in `git show`?** `message`
<details><summary>Answer</summary>

It is part of the diff, not the parent commit. The two short IDs are the old
and new versions of that one file, and `100644` is the file mode. The parent
is the previous commit, the one directly under this one in `git log`.
</details>

**44. After a commit, where does it show up in Cursor?** `cursor`
<details><summary>Answer</summary>

The Changes list stays empty when the working tree is clean, because that list
is only uncommitted edits. The commit remains in the Source Control graph and
in the file's Timeline (Explorer sidebar).
</details>

**45. What does `HEAD` point to?** `concept`
<details><summary>Answer</summary>

`HEAD` points at the current branch (`main`). That branch points at the commit
you have checked out. `git log` marks that commit with `(HEAD -> main)`.
</details>

**46. What does a `.gitignore` rule do to a matching untracked file?** `concept`
<details><summary>Answer</summary>

The file stays on disk. Git stops listing it in `git status`, so it is not
offered for the next commit. That is not a commit, and it is not a push.
</details>
