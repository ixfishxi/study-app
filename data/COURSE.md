# Git Workflow Course

Goal: make the everyday Git workflow second nature, then run it with Cursor's
agents. By the end of Part 1 you can take a real request from branch creation
through pull request, review, merge, and cleanup without instructions. By the
end of the course you run many agent work requests, each in its own isolated
copy, from one project brain committed in the repo, and `main` changes only
when you accept a finished request.

Reference card: [resources/Git_Development_Workflow.pdf](resources/Git_Development_Workflow.pdf)
Progress and next step: [PROGRESS.md](PROGRESS.md)

To continue in any chat, type **`/learn`** (or say "resume my Git course").
Also: `/learn quiz` for flash-card review, `/learn status` for a progress summary.

**One chat per lesson:** when a lesson is complete, the instructor runs an
end-of-lesson cleanup (removing demo leftovers and condensing notes, while keeping
all progress), then tells you to start a new chat and type `/learn`. Your
progress lives in the files, not the chat.

## Course map

The course has eleven parts, taught in order. Each lesson starts only after
the one before it is Mastered. Part 2 is L16–L20. Lesson 21 starts after L20.

| Part | Lessons | What it teaches | Why it's a separate part |
|------|---------|-----------------|--------------------------|
| 1. Core Git workflow | L0–L15, Capstone | Git and GitHub by hand, from a request to a merged pull request, plus history cleanup, cherry-pick and stash, tags, and bisect | Everything later depends on it. The capstone proves the whole Git workflow before any agent work. |
| 2. Salesforce orgs | L16–L20, callback on L42 | A reviewed commit promoted through Salesforce orgs, a change set that matches that commit, and a production deploy described on paper | Orgs are deploy targets. Part 3 starts after L20. |
| 3. Cursor's AI tools | L21–L26 | Editor navigation, Tab and Inline Edit, agent chat, sandbox and run modes, secrets, undoing agent work | Learn each tool, and its safety limits, in your own checkout before you trust an agent with a real request. |
| 4. Directing an agent | L27–L30 | Writing a work request, Plan and Ask modes, chat scope, the Agents Window | A clear request, an approved plan, and one request per chat decide most of what the agent gets right. |
| 5. Checking and correcting agent work | L31–L35 | Review and testing, weakened tests, triaging review findings, revising agent work, debugging | "Finished" from an agent is where your job starts: prove it, check the checks, send problems back, and find bugs with evidence. |
| 6. The project brain | L36–L38 | `AGENTS.md`, rules, and skills, where each piece of guidance belongs, and Milestone 1 (a solo agent sprint) | What should outlast a chat goes in committed files, before any work runs in a copy. The milestone joins Parts 3–6 on one real feature. |
| 7. Code you didn't write | L39–L40 | Mapping an unfamiliar codebase, characterization tests, small-step refactors | Most real work is in code someone else wrote. Learn it and pin down its behavior before you change it. |
| 8. A repo that stands on its own | L41–L44 | Pinned dependencies and one setup command, a command-line test and a linter in CI, a fresh clone, and Milestone 2 (taking over a teammate's branch) | Every copy starts from what's committed. The repo must set itself up and check itself without your machine. |
| 9. Isolated copies | L45–L50 | Git worktrees, Cursor `/worktree`, cloud agents, setting up each copy to test, moving work between local and cloud | Each request gets its own copy, so your folder and `main` stay as they are until you accept the work. |
| 10. Planning and parallel work | L51–L55 | Task breakdown, GitHub Issues, two requests at once, semantic conflicts, and Milestone 3 (a release built by parallel agents) | Bigger and parallel work collides in ways a single request never does. |
| 11. Tools, guardrails, and automation | L56–L66 | Subagents, MCP, prompt injection, hooks, Projects, subscriptions, Automations, brain pruning, measuring the workflow, and an agent capstone | More agents and more reach need hard limits, a coordinator whose results you still check, and evidence that the workflow pays off. |

---

## The workflow backbone

Every lesson builds toward this loop:

1. Understand the request and define what "done" means.
2. Check the repository and start from an up-to-date, clean base.
3. Create a focused branch.
4. Make a small change and inspect the diff.
5. Stage deliberately, commit, and inspect the history.
6. Push the branch and open a pull request.
7. Review the PR, respond to feedback, and run checks.
8. Bring in changes from `main` and resolve a conflict when needed.
9. Merge the PR and clean up the branches.
10. Return to an updated `main` and repeat.

From Part 3 on, the same loop runs with agents doing the edits:

1. Write the request with an outcome, files to follow, and a check the agent can run.
2. Approve a plan before any file changes.
3. Run it on a branch in an isolated copy that can install and test.
4. Prove it: tests, your diff review, and an agent review. Send problems back to the same agent.
5. Accept it by merging. Until then, `main` stays as it is.
6. Write what you learned into the project brain, in its own small commit.

---

## Workspace layout

```
Git Workflow Lab\          course home (NOT a git repo)
  COURSE.md                this file
  PROGRESS.md              status, evidence, mistakes to revisit, next step
  resources\               reference material (e.g. Git_Development_Workflow.pdf)
  study\                   flash cards and study material
    FLASHCARDS.md            cards added as you learn; say "quiz me" to review
    study.html               your spaced-repetition app; a finished session is saved here and on the website
    flashcards-progress.json a backup of your review history (the app saves to the cloud copy)
    sync-cloud.ps1           updates the app's cloud copy (private GitHub repo) after each lesson
  .cursor/rules/           tells the AI how to teach this course
  .cursor/skills/learn/    the /learn command: resume, quiz, status
  practice\                YOUR repo: you run every command here
  sandbox\                 instructor demo area (local only, never pushed; emptied after each lesson)
```

`sfwork\` is not in the tree yet. L17 creates it as its own repo for the
Salesforce drills. It is not `practice\`. In those lessons, "Salesforce
sandbox" means a Salesforce org. `sandbox\` is still the demo area.

The practice project is a tiny Python unit converter:

- `converter.py`: conversion functions plus a small command-line interface
- `test_converter.py`: the test suite, run with `python -m unittest`
- `README.md`: usage and the list of supported conversions

---

## How every lesson runs

1. **Warm-up:** one recall question from an earlier lesson.
2. **Concept:** a short explanation.
3. **Demo:** the instructor runs it once in `sandbox\`, shows the effect with
   `git status`, `git diff`, or `git log`, then shows the Cursor equivalent.
4. **Predict:** you say what will happen *before* running anything.
5. **Perform:** you run it in `practice\`, terminal first, then Cursor's interface.
6. **Inspect:** we verify the result together.
7. **Explain back:** you describe it in your own words.
8. **Independent exercise:** you do it alone. If you're stuck you get a hint, then you retry.
   Mistakes lead to a smaller exercise and a reassessment.

### Mastery gates

A lesson is **Mastered** only when all four are observed and recorded in
PROGRESS.md:

- **Explain:** you can say *why* the step exists and what Git is doing.
- **Predict:** you correctly predict the result before running it.
- **Perform:** you complete the independent exercise without the answer.
- **Verify:** you prove the result with an inspection command.

Statuses: `Not started`, `In progress`, `Needs review`, `Mastered`.

---

## Part 1: Core Git workflow

### L0: Git vs GitHub vs Cursor, and your first repo

*Foundation for every step.*

**Objectives**
- Distinguish Git (local version control), GitHub (hosting and collaboration),
  and Cursor's Source Control panel (a visual front end that runs Git commands).
- Name the three areas: **working tree**, **staging area (index)**, and
  **repository (commits)**.
- Understand config scopes: system, global, and local (per repo).

**Hands-on**
- Verify your tools: `git --version`, `gh auth status`.
- Predict what `git status` prints in a folder that is not a repo, then run it.
- Create the repo: `git init -b main`.
- Configure the practice repo only: its editor (`core.editor`) and its commit email.

**Independent exercise**
- Show which config scope each of your settings comes from, and explain why
  the practice repo needed `-b main` on this machine.

**Mastery check**
- Explain the three areas without notes.
- Explain what the `.git` folder is and what would happen if it were deleted.

---

### L1: Working tree, staging, and commits

*Workflow steps 4 and 5.*

**Objectives**
- Move changes deliberately from the working tree, to staging, to a commit.
- Read `git status` and `git diff` fluently.

**Commands:** `git status`, `git diff`, `git add <path>`, `git diff --staged`,
`git restore --staged <path>`, `git commit -m "..."`, `git log --oneline`

**Cursor:** the Changes list, the diff editor, `+` (stage), `-` (unstage), the
commit message box, and the Commit button.

**Hands-on**
- Make the initial commit of the starter project.
- Stage a file, unstage it, and stage it again, checking `git status` each time.

**Independent exercise**
- Edit two files, but commit only one of them. Predict the output of
  `git status` before each command you run.

**Mastery check**
- Explain the difference between `git diff` and `git diff --staged`.
- Explain what a commit contains.

---

### L2: History, HEAD, and .gitignore

*Workflow step 5.*

**Objectives**
- Navigate history and understand commit hashes and `HEAD`.
- Keep generated files and secrets out of Git.

**Commands:** `git log --oneline --graph`, `git show <commit>`,
`git check-ignore -v <path>`, `git rm --cached <path>`

**Cursor:** the Source Control Graph and the file Timeline (Explorer panel).

**Hands-on**
- Inspect a commit two different ways (terminal and Cursor).
- Create a `.gitignore` and watch files disappear from `git status`.

**Independent exercise**
- Running the tests creates a `__pycache__\` folder. Also create a fake
  `.env` file containing `API_KEY=not-a-real-key`. Keep both out of Git, commit
  your ignore rules, and *prove* both are ignored.

**Mastery check**
- Explain what `HEAD` points to.
- Explain why `.gitignore` does not affect a file that is already tracked.

---

### L3: Defining the request, and branches as pointers

*Workflow steps 1 to 3.*

**Objectives**
- Turn a request into an outcome, a scope, and 1 or 2 "done when" checks before
  editing anything.
- Understand a branch as a movable pointer to a commit.

**Commands:** `git branch`, `git switch -c <branch>`, `git switch <branch>`

**Cursor:** the branch picker in the status bar (bottom left).

**Hands-on**
- Create a branch, commit on it, switch back to `main`, and watch the files on
  disk change.
- Observe what happens to *uncommitted* changes when you switch.

**Independent exercise**
- Request: *"Add a pounds-to-kilograms conversion (`lb-to-kg`)."* Write the
  outcome, scope, and done-when checks. Then branch, implement, test with
  `python -m unittest`, update the README, and commit.

**Mastery check**
- Explain what actually happens inside `.git` when you create a branch.
- Predict which files change on disk when you switch branches.

---

### L4: Local merge and your first conflict

*Workflow step 8, local version.*

**Objectives**
- Distinguish a fast-forward merge from a merge commit.
- Resolve a conflict based on the *intended behavior*, not by picking a side
  blindly.

**Commands:** `git merge <branch>`, `git merge --abort`, `git branch -d`,
`git branch -D`

**Cursor:** conflict decorations (Accept Current / Incoming / Both) and the
3-way merge editor.

**Hands-on**
- Merge your L3 branch into `main`, then delete the branch safely.

**Independent exercise**
- Create two branches that edit the same README line in different ways.
  Predict whether merging them will conflict, merge both, resolve the conflict
  so the README is correct, and verify there are no leftover conflict markers.

**Mastery check**
- Explain why Git could not resolve the conflict on its own.
- Explain the difference between `-d` and `-D`.

---

### L5: Remotes, origin, and fetch vs. pull

*Foundations for workflow steps 2 and 6.*

**Objectives**
- Understand remotes, `origin`, remote-tracking branches (`origin/main`), and
  upstream tracking.
- Know exactly what `fetch`, `pull`, and `push` each do.

**Commands:** `git remote -v`, `git remote add origin <url>`,
`git push -u origin main`, `git fetch`, `git pull --ff-only`, `git branch -vv`,
`git log main..origin/main`

**Cursor:** Publish Branch, Sync Changes, Fetch, and the ahead/behind arrows
in the status bar.

**Hands-on (setup for real pull requests)**
- Create a public GitHub repo yourself (web UI, then see the `gh` equivalent).
  Choose the MIT license on that screen. A public repo with no license is all
  rights reserved.
- Connect it as `origin` and push `main`.

**Independent exercise**
- Edit a file directly on GitHub's website. Then, locally, *fetch* and inspect
  what's incoming before you pull. Explain why your files didn't change after
  `fetch` alone.

**Mastery check**
- Explain `pull` in terms of two other commands.
- Explain what Cursor's Sync Changes button actually runs.

---

### L6: Protecting main (CI checks and a ruleset)

*Setup for workflow steps 6 and 7: `main` changes only through a pull request with passing checks.*

**Objectives**
- A GitHub Actions workflow is a file in the repo that tells GitHub to run
  commands, such as the tests, on every pull request.
- In that file, an event starts a job. The job's steps run on a runner. The
  event is `pull_request`, so the test check exists before merge. Pin each
  `uses:` action to a version. Set `permissions` so the workflow token can only
  read the repo.
- A ruleset on `main` makes the process binding: changes come in through a pull
  request, the test check must pass, and force pushes are blocked.
- The workflow is a committed file. The ruleset is a GitHub setting, not a file.

**Commands:** `git add .github/workflows/<file>`, `git commit`, `git push`,
`gh run list`, `gh run view`

**Cursor:** the workflow file in `.github/workflows/`, then the Actions tab and
the ruleset settings on GitHub.

**Hands-on**
- Add a GitHub Actions workflow that runs the tests on `pull_request`. Pin each
  `uses:` action to a version, and set `permissions` so the token can only read
  the repo. Commit it, push it, and watch its first run.
- Add a ruleset on `main`: require a pull request, require the test check, and
  block force pushes.

**Independent exercise**
- Try to edit a file directly on GitHub's website, on `main`. Predict what GitHub
  lets you do. Show where the ruleset stopped the direct change and what GitHub
  offered instead. Show with `gh run list` that the latest workflow run passed.

**Mastery check**
- Explain why the ruleset, not the workflow file, is what protects `main`.
- Explain what "require the test check" adds to "require a pull request."
- Explain why each `uses:` line names a version, and why the workflow token is
  read-only.

---

### L7: Your first full pull request

*Workflow steps 2 to 6.*

**Objectives**
- Run the start-of-work routine automatically: check status, update `main`,
  then branch.
- Publish a branch and open a well-described PR.

**Commands:** `git switch main`, `git pull --ff-only`, `git switch -c`,
`git push -u origin <branch>`, `gh pr create`, `gh pr view --web`,
`gh pr checks`

**PR description:** purpose, key changes, test result, remaining risk.

**Hands-on**
- Take a request from a clean `main` all the way to an open PR with passing checks.

**Independent exercise**
- Request: *"Add Celsius to Fahrenheit (`c-to-f`) with tests and docs."*
  Everything from start to PR opened, with the instructor only observing.

**Mastery check**
- Explain why you update `main` *before* creating the branch.
- Explain what `-u` did on your first push.

---

### L8: Review, feedback, and a failing check

*Workflow step 7.*

**Objectives**
- Read your own PR the way a reviewer would.
- Respond to review feedback with new commits on the same branch.
- Diagnose a failing automated check.

**Commands:** `gh pr diff`, `gh pr view --comments`, `gh pr checks`,
`gh run view --log-failed`

**Hands-on**
- The instructor posts review comments on your PR, labeled "Instructor
  review." Address each one, push, and reply.

**Independent exercise**
- You'll get a new request whose first implementation turns the CI check red.
  Find out why from the check output, fix it, and get the PR green.

**Mastery check**
- Explain why feedback goes on the same branch instead of a new PR.
- Explain the difference between "passes on my machine" and "passes in CI."

---

### L9: Main moved, and your PR conflicts

*Workflow step 8.*

**Objectives**
- Bring the latest `main` into your branch and resolve a conflict in a PR.

**Commands:** `git fetch origin`, `git merge origin/main`, `git merge --abort`,
`git add <resolved-file>`, `git commit`, `git push`

**Hands-on**
- While your PR is open, a "teammate" change is merged into `main` on GitHub.
  Your PR reports a conflict.

**Independent exercise**
- Resolve the conflict locally, retest, push, and confirm on GitHub that the
  PR is mergeable and the checks pass.

**Mastery check**
- Explain why we merge `origin/main` rather than local `main` here.
- Explain what `git merge --abort` restores.

---

### L10: Merge and cleanup, then repeat

*Workflow steps 9 and 10.*

**Objectives**
- Choose a merge method (squash by default here) and merge safely.
- Clean up remote and local branches, and return to an up-to-date `main`.

**Commands:** `gh pr merge --squash --delete-branch`, `git switch main`,
`git pull --ff-only`, `git fetch --prune`, `git branch -vv`, `git branch -D`

**Hands-on**
- Merge a PR, then clean up. Observe why `git branch -d` refuses after a squash
  merge, and confirm the PR merged before using `-D`.

**Independent exercise**
- Request: *"Show a friendly error instead of crashing when the value isn't a
  number."* One full cycle from request to cleaned-up `main`, with minimal
  prompting.

**Mastery check**
- Explain the difference between merge commit, squash, and rebase merges.
- Explain what `[gone]` means in `git branch -vv`.

---

### L11: Safe recovery (inspect first, then choose)

*Protects every step.*

**Objectives**
- Always diagnose before undoing: `git status`, `git log --oneline --graph --all`,
  `git reflog`.
- Pick the least destructive command that fixes the actual state.

**Toolkit:** `git restore`, `git restore --staged`, `git commit --amend`,
`git stash`, `git revert`, `git reflog`, `git reset` (and when *not* to use it)

**Cursor:** Discard Changes (permanent), Undo Last Commit, Stash.

**Hands-on**
- Recover a commit that seems "lost."
- Undo a commit that has already been pushed, without rewriting shared history.

**Independent exercise (surprise drills)**
- The instructor puts your repo into a broken state, such as accidentally
  committing to `main`. You diagnose it and repair it without being told
  which command to use.

**Mastery check**
- For each state, name what you'd inspect, then the command, and explain why it's safe.
- Explain why rewriting pushed history is dangerous.

---

### L12: Cleaning up history (interactive rebase, and rebase vs. merge)

*Tidy your own commits before review, and know when to rebase instead of merge.*

**Objectives**
- Interactive rebase rewrites the commits on your branch: squash several into
  one, reword a message, or drop and reorder commits.
- Rebasing a branch onto `main` replays your commits on top of the latest
  `main`. Merging `main` in keeps both histories and adds a merge commit.
- Rebasing gives commits new hashes. Only rewrite commits no one else has built on (L11).
- After rebasing a branch you already pushed, push it with `--force-with-lease`.
  Your ruleset still blocks force pushes to `main`.

**Commands:** `git rebase -i main`, `git rebase main`, `git rebase --abort`,
`git log --oneline --graph`, `git push --force-with-lease`

**Cursor:** the rebase to-do list opens in Cursor as your Git editor (L0), and
the Source Control Graph.

**Hands-on**
- In `sandbox\`, the instructor squashes three commits into one, then rebases a
  branch onto a `main` that moved, showing `git log --oneline --graph` before and
  after. You say what happened to the hashes.

**Independent exercise**
- On a branch, make three small commits for *"Add a centimeters-to-millimeters
  conversion (`cm-to-mm`)"*: the code, the test, and a README line, with one
  commit message that has a typo. Push the branch.
- Merge a separate one-line README fix to `main` through its own pull request,
  so `main` moves. Predict the graph after each step. Squash your three commits
  into one with a clear message, rebase onto the updated `main`, push safely,
  and merge the pull request.

**Mastery check**
- Explain why rebasing changed the hashes, and why that matters only for shared commits.
- Explain when you would merge `main` in instead of rebasing.

---

### L13: Moving commits around (cherry-pick, and stash in depth)

*Copy one commit to another branch, and set aside exactly the work you choose.*

**Objectives**
- `git cherry-pick <commit>` copies one commit onto the current branch as a new
  commit, with a new hash.
- Cherry-pick takes one fix without the rest of a branch. It can conflict, like a merge.
- A named stash (`git stash push -m`) or a partial stash (one path, or `-p` to
  choose pieces) sets aside only what you pick. `git stash list` and
  `git stash apply` bring it back.
- A stash is local and easy to forget. For anything you want to keep, prefer a
  commit on a branch.

**Commands:** `git cherry-pick <commit>`, `git cherry-pick --abort`,
`git stash push -m "<message>" <path>`, `git stash push -p`, `git stash list`,
`git stash apply stash@{<n>}`, `git stash drop`

**Cursor:** the Source Control `...` menu > Stash, and the Source Control Graph
to find commit hashes.

**Hands-on**
- In `sandbox\`, the instructor cherry-picks one commit from a branch that has
  three, then makes a named stash of one file. You say what each command moved
  and what it left behind.

**Independent exercise**
- On a branch, make two commits: a README wording fix, then an experimental
  change you don't want yet. Bring only the wording fix to `main` using a new
  branch, `git cherry-pick`, and a pull request. Predict whether the copied
  commit keeps its hash.
- With two files edited, stash only one of them under a name, switch branches
  and back, and restore it. Prove each step with `git log --oneline` and
  `git stash list`.

**Mastery check**
- Explain why the cherry-picked commit has a new hash.
- Explain when a stash is riskier than a commit.

---

### L14: Tags and releases (marking a version)

*Name a version of the code, and publish it as a release on GitHub.*

**Objectives**
- A tag is a name fixed to one commit, such as `v1.0.0`. Unlike a branch, it does not move.
- An annotated tag (`git tag -a`) stores a message, an author, and a date. Tags
  are pushed separately from branches.
- A GitHub release is built on a tag and adds release notes.
- Version numbers can say what changed: major for breaking changes, minor for
  new features, and patch for fixes.

**Commands:** `git tag -a v1.0.0 -m "<message>"`, `git tag`, `git show v1.0.0`,
`git push origin v1.0.0`, `gh release create`, `gh release view`

**Cursor:** the Source Control Graph, which shows tags on commits.

**Hands-on**
- In `sandbox\`, the instructor tags a commit, adds a commit after it, and shows
  where the tag and the branch point now. You say how a tag differs from a branch.

**Independent exercise**
- Tag the current `main` of the practice repo as `v1.0.0` with an annotated tag,
  push the tag, and create a GitHub release with short notes.
- Merge *"Add a millimeters-to-inches conversion (`mm-to-in`)"* through a pull
  request, then release the next version. Predict which version number it
  should be and where each tag points afterward. Prove it with `git show` and
  `gh release view`.

**Mastery check**
- Explain why a tag stays put when `main` moves.
- Explain why you chose that second version number.

---

### L15: Finding a bad commit (git bisect)

*Let Git search your history, halving it each step, for the commit that broke something.*

**Objectives**
- `git bisect` checks out the commit halfway between a known good commit and a
  known bad one. You mark each one good or bad until Git names the first bad commit.
- A test command can do the marking for you: `git bisect run`.
- Always finish with `git bisect reset` to return to where you started.
- Bisect finds where a bug came in. The fix is still a normal branch and pull request.

**Commands:** `git bisect start`, `git bisect bad`, `git bisect good <commit>`,
`git bisect run python -m unittest`, `git bisect reset`, `git log --oneline`

**Cursor:** the Source Control Graph, to pick the known good commit.

**Hands-on**
- In `sandbox\`, the instructor bisects a short history with one planted bad
  commit, first by hand, then with `git bisect run`. You say how many steps it
  took and why.

**Independent exercise**
- The instructor tells you first, then adds a short series of commits to a
  branch in the practice repo, one of which quietly breaks a conversion. Predict
  how many steps bisect will need. Find the bad commit with bisect, prove it with
  `git show`, run `git bisect reset`, and fix it through a normal pull request.

**Mastery check**
- Explain why bisect needs so few steps.
- Explain what `git bisect reset` protects you from.

---

### Capstone (the Git workflow, on an unfamiliar request)

You receive an **unfamiliar, realistic development request**. It's revealed only
when the capstone starts. Expect surprises along the way: a teammate change that
conflicts, and review feedback. Complete all 10 workflow steps with minimal
prompting.

**Rubric** (each step is scored Solid, Shaky, or Missed)
- Done-criteria defined before editing
- Clean, current base verified
- Focused, well-named branch
- Small change, diff inspected before staging
- Deliberate staging and a clear commit message
- Pushed with upstream set; PR description has purpose, changes, test result, and risk
- Feedback addressed on the same branch; checks green
- Conflict resolved by intended behavior and retested
- Merged and cleaned up (remote and local)
- Back on an updated `main`, ready for the next request

Any Shaky or Missed item goes into "Mistakes to revisit" for a targeted retest.

When the capstone is Mastered, the next chat starts L16.

---

## Part 2: Salesforce orgs

This follows the Git capstone and comes before Lesson 21. L16–L20 are required
and use the same four gates as every other lesson. Their gates count toward
the course percentage.
L17 and L18 run in `sfwork\`, not in `practice\`. You name the Salesforce sandbox
when L17 starts. L19 and L20 stay on paper. No lesson in this bridge deploys to
production or uploads a change set.

The source of truth is the Git commit. Each org has one job:

- **Your org** (a scratch org, or your own Developer sandbox) builds one branch.
- **Integration** is a shared Salesforce sandbox. It receives merged commits.
- **Staging** is a Partial Copy or Full sandbox. It receives a release tag.
- **Production** receives that same tag after staging has passed. You name it
  in these lessons. You do not deploy to it.

### L16: One commit, four orgs

*A branch is where you build. A Salesforce org is where a commit is deployed.*

**Objectives**
- Your org is the only one that receives work from a feature branch.
- The integration sandbox receives the merge commit, not the open branch.
- Staging and production receive one tag of that commit, after the merge.
- A long-lived branch per org is not this flow. The commit is what moves.

**Commands:** none. You trace the commit with the Git words you already use
(`branch`, merge commit, `tag`).

**Cursor:** none.

**Hands-on**
- In the chat, the instructor walks one commit across the four orgs. You say
  which org a feature branch may be deployed to, and which orgs wait for a
  merge or a tag.

**Independent exercise**
- Write a trace of one change from a new branch through to production. For
  each step, name the Git object and the org that receives it. You do not log
  in to Salesforce.

**Mastery check**
- Explain why the integration sandbox does not take the feature branch.
- Explain what production is supposed to receive.

---

### L17: Build on a branch in your own org

*One change, in your org, committed on a branch.*

**Objectives**
- `sfwork\` is its own repo. `practice\` stays the Python course repo.
- You name the Salesforce sandbox at the start of this lesson, then build there
  on a branch. It is a scratch org or your own Developer sandbox.
- The metadata you changed comes onto that branch and is committed there.
- A pull request is how the change leaves your org. You do not deploy it to
  the shared sandbox in this lesson.

**Commands:** `sf org login web`, `sf org list`, `sf project retrieve start`,
`sf project deploy start`, plus the Git commands from Part 1.

**Cursor:** Source Control on the `sfwork\` folder.

**Hands-on**
- Predict what `git status` will show after the source for one component is
  retrieved onto a new branch. The component is named when the lesson starts.
  Then you run that retrieve.

**Independent exercise**
- On a second branch, bring a second component from your own org onto the
  branch, commit it, push, and open a pull request. Show `git diff` and the
  deploy result for your org. The component is named when the lesson starts.

**Mastery check**
- Explain why this repo, not the org, is the copy the pull request reviews.
- Explain why this lesson stops before the shared sandbox.

---

### L18: Promote the same commit

*Staging receives the commit you already merged, then you tag it.*

**Objectives**
- The second org is a Salesforce sandbox you are allowed to deploy to. It is
  not production.
- You deploy the merge commit, not a new edit made in that org.
- The tag names that same commit. `git show` on the tag and the deploy refer
  to one snapshot.
- Production would receive that tag next. This lesson does not deploy there.

**Commands:** `sf project deploy start`, `git tag -a`, `git show`, `git rev-parse`

**Cursor:** Source Control Graph, to see the tag on the merge commit.

**Hands-on**
- Predict what the second sandbox will contain after the merged commit is
  deployed, then deploy it.

**Independent exercise**
- Tag that commit. Show the deploy output and `git show` on the tag, and show
  that both refer to the same commit.

**Mastery check**
- Explain why the second sandbox does not get its own branch.
- Explain what you would hand production, and why you did not deploy it here.

---

### L19: A change set that matches the commit

*Git names the components. A change set only carries that list from one org to another.*

**Objectives**
- An outbound change set is a list of components in a Salesforce org. Git does
  not store that list.
- The commit's diff is the list that belongs in the change set.
- A component in the change set that is not in the commit makes the target org
  differ from the snapshot you reviewed.
- This lesson writes the list. It does not upload or deploy a change set.

**Commands:** `git show`, `git diff`

**Cursor:** the commit diff in Source Control.

**Hands-on**
- The instructor shows one diff. You say which components belong in the
  outbound change set, and which file in the diff is not a component to add.

**Independent exercise**
- From the tag you made in L18, write the component list a release manager would
  put in the outbound change set. Mark anything in the org that you would
  refuse to add because it is not in that commit. Show the list next to
  `git show` of the tag.

**Mastery check**
- Explain why the change set is not the source of truth.
- Explain what goes wrong when the change set and the commit disagree.

---

### L20: Production on paper

*Say what production would receive. Do not deploy it.*

**Objectives**
- Production receives the same tag staging already received.
- The transport can be a CLI deploy or an inbound change set built from that
  tag's component list. Either way the snapshot is the tag.
- A deployment note names the tag, the orgs that already have it, who would
  approve, and the previous tag you would return to.
- You stop before the production deploy. Nothing in this lesson logs in to
  production.

**Commands:** `git show`, `git tag`

**Cursor:** the Source Control Graph, to read the tag.

**Hands-on**
- You say which Git object production would receive, and which earlier tag a
  rollback would name.

**Independent exercise**
- Write the deployment note for the L18 tag: the commit, the orgs that already
  received it, what production would receive, and the command or change-set
  upload you will not run. The instructor checks the note against `git show`.

**Mastery check**
- Explain why production does not get a new list built from memory.
- Explain why the note is finished without a production login.

---

## Part 3: Cursor's AI tools

This follows L20. Parts 3 to 11 start once the capstone and L16–L20 are Mastered.
You still need to be able to branch, commit, push, and open a pull request.

Each lesson from here on runs like the lessons before it: a short concept, one
demo, you predict, you perform in `practice\`, we inspect, you explain it, then
you do the independent exercise. A lesson is Mastered only when Explain,
Predict, Perform, and Verify are all observed. A miss gets the same feedback as
before: the specific misconception, a smaller exercise, and another check. The
next lesson starts only after this one is Mastered, in a new chat.

The end state for Parts 3 to 11: one project brain in committed files, many work
requests, each in its own isolated copy, a knowledge base that can grow, and a
`main` that changes only when you accept a finished request. Everything these
parts add to `practice\` goes in through a branch and a pull request. Secrets in
these lessons are always fake.

This part covers the tools themselves, one at a time, in your own checkout on a
branch: finding your way in the editor, small edits with Tab and Inline Edit, an
agent chat, what its commands can reach, keeping secrets out of its reach, and
undoing what it did.

### L21: Editor navigation (Command Palette, Quick Open, symbols, and search)

*Find any command, file, or function without scrolling.*

**Objectives**
- The Command Palette (Ctrl+Shift+P) runs any command by name, including ones
  with no button.
- Quick Open (Ctrl+P) opens a file from part of its name.
- Go to Symbol finds a function by name, in this file (Ctrl+Shift+O) or across
  the project (Ctrl+T). Go to Definition (F12) and Find All References
  (Shift+F12) follow the code both ways.
- Search across files (Ctrl+Shift+F) finds text everywhere in the project.
- Your own navigation is how you check what an agent tells you about the code.

**Commands:** none new. This lesson is the editor itself.

**Cursor:** Command Palette, Quick Open, Go to Symbol, Go to Definition, Find All
References, Search, and Keyboard Shortcuts (Ctrl+K, then Ctrl+S).

**Hands-on**
- In `sandbox\`, the instructor finds the same function three ways: Quick Open,
  Go to Symbol, and Search. You say which was fastest and why.

**Independent exercise**
- In `practice\`, without scrolling or using the Explorer: open
  `test_converter.py`, jump to the test for `km-to-miles`, jump from it to the
  function it tests, and find every place `KM_PER_MILE` is used. Predict how
  many places before you search.
- Open the terminal and the Keyboard Shortcuts list from the Command Palette.
  Show that your count matches the search results.

**Mastery check**
- Explain when you would use Quick Open, Go to Symbol, and Search.
- Explain how you would check an agent's claim that a function is used in only one place.

---

### L22: Tab and Inline Edit (small edits in the editor)

*Tab finishes what you started. Inline Edit changes a selection. You accept or reject each one.*

**Objectives**
- Tab suggests the next edit as you type, based on your recent edits and the
  code around you. Tab accepts, Escape rejects, and Ctrl+Right accepts one word.
- Inline Edit (Ctrl+K) changes the code you select from a short instruction,
  and shows a diff you accept or reject.
- Know what Git sees before and after you accept a suggestion.
- Use these for small edits in one place. Use an agent chat when the change
  spans files or needs commands.

**Commands:** `git status`, `git diff`, `python -m unittest`

**Cursor:** Tab to accept, Escape to reject, Ctrl+Right to accept a word, and
Tab again to jump to the next suggested edit. Ctrl+K for Inline Edit. The Tab
indicator in the status bar to snooze it or turn it off.

**Hands-on**
- In `sandbox\`, the instructor types the start of a small function, accepts one
  Tab suggestion, rejects another, then makes one Inline Edit. You say what each
  one did.

**Independent exercise**
- Request: *"Add a kilometers-to-meters conversion (`km-to-m`)."* On a branch,
  type the start of the function yourself and let Tab help finish it and the
  other places it belongs. Accept or reject each suggestion on purpose.
- Select the new function and use Inline Edit to add a one-line docstring.
  Before you accept, predict what `git diff` shows. Run the tests, and take it
  through your normal pull request.

**Mastery check**
- Explain what `git diff` showed before and after you accepted the Inline Edit, and why.
- Explain when you would use Tab or Inline Edit instead of an agent chat.

---

### L23: Agent chat basics (context, commands, and models)

*Start a chat, give it the right context, and read every command before it runs.*

**Objectives**
- An agent chat can search the code, read and edit files, and run terminal
  commands to finish a request.
- If you know the exact file, tag it with `@`. If not, let the agent search.
  Extra files can confuse it.
- Watch the edits as they happen, and press Stop if it heads the wrong way. A
  message typed while it works can wait in the queue, or steer it now.
- Read every command the agent asks to run before you approve it. Which commands
  run without asking is the next lesson.
- You pick the model. Know where to see your usage, because larger models can cost more.

**Commands:** `git status`, `git diff`, `python -m unittest`

**Cursor:** the agent panel (Ctrl+I), `@` to tag a file, Stop, the message queue,
the model picker, and the command approval prompt.

**Hands-on**
- In `sandbox\`, the instructor gives an agent a small request, tags one file,
  stops it once, and approves one command after reading it aloud. You say what
  the agent did without asking, and what it asked for.

**Independent exercise**
- Request: *"Add a kilograms-to-grams conversion (`kg-to-g`)."* On a branch, in
  one chat, without tagging any file. Choose the model on purpose and say why.
  Before you send it, predict which files the agent will change.
- When it asks to run a command, say what the command will do before you
  approve or deny it. Compare `git status` and `git diff` with your prediction,
  then take it through your normal pull request.

**Mastery check**
- Explain what the agent could do without asking you, and what it had to ask for.
- Explain when you would tag a file and when you would let the agent find it.

---

### L24: Sandbox and run modes (what agent commands can reach)

*Most agent commands run inside a sandbox. Know what it can reach, and what happens when it needs more.*

**Objectives**
- In the default run mode, Cursor runs agent terminal commands in a sandbox when
  it can. A sandboxed command can work in your project, with limits on what else
  it can reach.
- Some paths are protected even inside your project, such as `.git/config` and
  `.git/hooks`.
- When a command needs to step outside the sandbox, the agent has to ask, and you decide.
- Run modes: Auto-review (the default), Allowlist, and Run Everything. Know which
  one you use and what it lets through.
- `sandbox.json` and `permissions.json` can change these limits. You don't need
  either to start.

**Commands:** `git status`, `python -m unittest`

**Cursor:** the run mode setting, the command approval prompt, and how the chat
shows whether a command ran in the sandbox.

**Hands-on**
- In `sandbox\`, the instructor has an agent run one command that stays in the
  project and one that reaches the internet, and shows what happened each time.
  You say what the sandbox allowed.

**Independent exercise**
- In one chat in `practice\`, ask the agent to: run the tests, fetch a web page
  with a terminal command, download a Python package into a temporary folder,
  and write a file outside `practice\`. Before each one, predict whether it runs
  without asking, asks first, or fails.
- Approve or deny each request based on what the command will do. Show the
  results in the chat and with `git status`, clean up anything it created, and
  write down which run mode you use.

**Mastery check**
- Explain why the sandbox lets most commands run without asking.
- Explain what you check before approving a command that leaves the sandbox.

---

### L25: Secrets and `.cursorignore` (what agents can't read)

*`.cursorignore` stops the agent reading. `.gitignore` stops the commit.*

**Objectives**
- `.cursorignore` uses `.gitignore` patterns. Files it matches are hidden from
  Agent, Tab, Inline Edit, and `@` mentions.
- `.cursorignore` does not stop a commit. `.gitignore` (L2) does. A secret file
  needs both covered.
- Cursor already hides some files by default. Check what is hidden instead of guessing.
- Know what `.cursorignore` does not cover. Never put a real secret in the practice repo.

**Commands:** `git check-ignore -v <path>`, `git status`, `git ls-files`

**Cursor:** `.cursorignore` at the repo root. The global ignore list in Cursor
settings, for patterns you want in every project.

**Hands-on**
- In `sandbox\`, the instructor makes a fake key file and asks an agent to read
  it, before and after adding `.cursorignore`. You say what it showed.

**Independent exercise**
- Create a fake key file, `secrets/service-key.txt`, containing
  `NOT-A-REAL-KEY`. Make sure no work-request agent can read it and no commit
  can include it. Commit your ignore rules, not the file.
- In a new chat, ask the agent to read the key file. Then run a small request:
  *"Add a liters-to-milliliters conversion (`l-to-ml`),"* and let the agent
  commit it. Predict both results first. Prove the agent couldn't read the key,
  and prove the key is in no commit.

**Mastery check**
- Explain which file stopped the agent reading the key, and which stopped the commit.
- Explain one way the key could still reach the agent, and what you would do about it.

---

### L26: Undoing agent work (Keep, Undo, checkpoints, and Git)

*Commit first. Then any agent step can be taken back.*

**Objectives**
- Review the agent's edits, then Keep or Undo them, one file at a time or all at once.
- Cursor saves checkpoints during a chat. Restoring one puts the files back to
  how they were at that point. The conversation stays.
- Checkpoints are local and separate from Git. Know what they cannot undo.
- Commit before an agent session, so Git is the real safety net. The L11
  recovery commands still apply.

**Commands:** `git status`, `git diff`, `git log --oneline`, `git restore`

**Cursor:** Keep and Undo on agent edits. Restore Checkpoint in the chat. The
file Timeline (L2) for one file's history.

**Hands-on**
- In `sandbox\`, the instructor lets an agent make two changes in one chat, then
  restores the checkpoint from before the second. You say what came back and
  what stayed.

**Independent exercise**
- Commit so `practice\` is clean. On a branch, in one chat, ask for:
  *"Add a Celsius-to-Kelvin conversion (`c-to-k`)."* Then, in the same chat, ask
  it to rename `km_to_miles` to `kilometers_to_miles` everywhere. Undo the rename
  by restoring the right checkpoint. Predict the files first.
- Ask the agent to create `scratch.txt` with a terminal command, then restore
  the checkpoint from before that. Predict whether `scratch.txt` is still there.
- Prove each result with `git status` and `git diff`. Clean up with Git, and
  take only the `c-to-k` change through your normal pull request.

**Mastery check**
- Explain why you committed before starting.
- Explain what the checkpoint restored, what it did not, and what you used instead.

---

## Part 4: Directing an agent

How to hand an agent one request: write it so the agent can check its own work,
approve a plan before any file changes, keep each chat to one request, and find
your conversations again when there are many.

### L27: Writing a work request (outcome, files, and a check the agent can run)

*A specific request with a check the agent can run beats a vague one.*

**Objectives**
- A good request says the outcome, the file or pattern to follow, what "done"
  means (L3), and a check the agent can run by itself.
- Tests are the best check. With tests, the agent can change code, run them, and
  keep going until they pass.
- Test first: ask for the tests, see them fail, commit them, then ask for the
  code without changing the tests.
- Keep one request small enough that you can review all of it.

**Commands:** `python -m unittest`, `git log --oneline`, `git show`

**Cursor:** the agent chat, and `@` to point at the file whose pattern it should follow.

**Hands-on**
- In `sandbox\`, the instructor sends the same request two ways, vague and
  specific, in two new chats, and compares the diffs. You say what the specific
  version changed about the result.

**Independent exercise**
- Request: *"Add a pints-to-liters conversion (`pt-to-l`)."* Write the request
  yourself: outcome, the file and pattern to follow, done-when, and the check.
- Do it test first, on a branch. Predict what the tests report after you commit
  them. Then have the agent write the code without touching the tests. Prove
  with `git log` and `git show` that the tests came first and did not change.
  Take it through your normal pull request.

**Mastery check**
- Explain what the check in your request let the agent do on its own.
- Explain why the tests were committed before the code.

---

### L28: Plan and Ask modes (approve the plan before any edit)

*The agent researches and writes a plan. Nothing changes until you accept it.*

**Objectives**
- In Plan mode, the agent asks questions, researches the repo, and writes a
  plan. You review the plan before any file changes.
- You can edit or reject the plan. Files change only after you choose to build it.
- Ask mode answers questions and stays read-only.
- When a build goes wrong, revert and fix the plan instead of stacking
  follow-up fixes.

**Commands:** `git status`, `git diff` (before the plan, while you review it,
and after the build)

**Cursor:** the mode picker, or Shift+Tab: Agent, Plan, Ask. The plan's build
button. "Save to workspace" for a plan you want to keep.

**Hands-on**
- In `sandbox\`, the instructor asks for a plan and checks `git status` while
  the plan is open. You say in one sentence what it showed.
- In `practice\`, you ask one question about the code in Ask mode, then check
  `git status`.

**Independent exercise**
- Request: *"Add a feet-to-meters conversion (`ft-to-m`)."* On a branch, in
  Plan mode. Before you build, predict what `git status` shows. Change at least
  one thing in the plan before you accept it, such as what "done" means. Build,
  compare the diff with the plan, and take it through your normal pull request.

**Mastery check**
- Explain what you protected by reviewing the plan before any file changed.
- Explain when you would stop and fix the plan instead of asking for another fix.

---

### L29: Chat scope (one request per chat, and when to start fresh)

*New request, new chat. A chat is not the brain.*

**Objectives**
- One chat handles one work request. When the request changes, start a new chat.
- Keep the context small. A long chat collects noise, and the agent can lose
  focus. A new chat starts clean.
- A chat's history, and any saved chat memory, stay in Cursor. They are not in
  the repo.
- What should last needs a place in the repo. The project brain lesson (L36)
  builds that place.

**Commands:** `git status`, `git log --oneline`

**Cursor:** New Chat. `@` to tag a file. `@` a past chat when you really need
its transcript. Saved chat memories, if your Cursor version has them.

**Hands-on**
- In `sandbox\`, the instructor tells one fact to a chat, and commits a
  different fact to an `AGENTS.md`. Then a new chat is asked about both. You
  say what it showed.

**Independent exercise**
- Request 1: *"Add an ounces-to-grams conversion (`oz-to-g`)."* One chat, its
  own branch. During it, tell that chat one working preference of your choice,
  in chat only.
- Request 2: *"Remove the duplicated test instructions from the README."* Start
  it in a new chat. Predict whether the new chat follows your preference. Show
  from Git whether the preference is anywhere in the repo. Keep a note of it for
  the project brain lesson (L36).

**Mastery check**
- Explain why a saved chat memory still does not count as the project brain.
- Explain when you keep the same chat, and when you start a new one.

---

### L30: The Agents Window (every agent and conversation in one place)

*One place to see every agent, workspace, and conversation.*

**Objectives**
- The editor is built around files. The Agents Window is built around agents:
  local, worktree, and cloud conversations all appear in its sidebar.
- A workspace is a project folder. One Agents Window can hold several workspaces.
- Find a past conversation by searching, and pull its context into a new chat
  with `@` when you need it.
- Know which files an agent started from the Agents Window is changing.

**Commands:** `git status`, `git log --oneline`

**Cursor:** Command Palette > Open Agents Window. The sidebar. Conversation
search (Ctrl+K in the Agents Window). Side chats (`/side`). Opening the
workspace in the editor.

**Hands-on**
- In `sandbox\`, the instructor opens the Agents Window, adds the sandbox as a
  workspace, starts one agent, and finds an older conversation by search. You
  say what the sidebar showed.

**Independent exercise**
- Open the Agents Window and add `practice\` as a workspace. Find your L29 chats
  by searching for a word you used in them.
- Start a new agent on `practice\` from the Agents Window: *"Add a
  miles-to-feet conversion (`mi-to-ft`)."* on a branch. Before it edits, predict
  whether the change will show in the editor's Source Control view. Prove it
  with `git status`, then take it through your normal pull request.

**Mastery check**
- Explain the difference between a conversation and a workspace.
- Explain why finding an old conversation still does not make it part of the project brain.

---

## Part 5: Checking and correcting agent work

"Finished" from an agent is where your job starts. This part covers what happens
after the agent says it's done: prove the work, check that the tests still mean
something, decide which review findings are real, send problems back to the same
agent, and track down a bug with evidence instead of guesses.

### L31: Review and testing (proof before merge)

*Finished is not done until something checks it.*

**Objectives**
- "Finished" from an agent means ready to check, not ready to merge.
- Three kinds of proof: the tests pass, you review the diff, and an agent
  review looks for problems.
- You merge only after the proof, and you can say what the proof showed.
- Small changes are easier to prove. A change too big to review gets split.

**Commands:** `python -m unittest`, `git diff main...<branch>`, `gh pr diff`,
`gh pr checks`

**Cursor:** Review > Find Issues after an agent finishes. Agent Review in the
Source Control view. Bugbot on pull requests, if you turn it on.

**Hands-on**
- In `sandbox\`, the instructor runs each kind of proof once on a small change.
  You say what each one checked.

**Independent exercise**
- The instructor tells you first, then opens a small "finished" pull request in
  the practice repo. Decide whether to merge it. Use at least two kinds of
  proof. Predict what each one will show before you run it. Merge only if you
  would stand behind the change; otherwise request changes. Show what each
  check found.

**Mastery check**
- Explain why a green test run is not enough on its own.
- Explain what would have reached `main` if you had skipped the review.

---

### L32: Tests that lie (catching weakened tests)

*Green checks prove nothing if the tests were changed to pass.*

**Objectives**
- An agent told to "make the tests pass" can do it the wrong way: loosen an
  assertion, skip a test, delete one, or change an expected value to match
  wrong output.
- Review test changes separately from code changes. Ask whether each test still
  checks what it checked before.
- In a request, say which tests must not change.
- Changing a test is right when the intended behavior changed. Then the request
  should say so.

**Commands:** `git diff main...<branch> -- test_converter.py`, `gh pr diff`,
`git log -p -- test_converter.py`, `python -m unittest`

**Cursor:** the diff editor, looking at the test file on its own. Agent Review.

**Hands-on**
- In `sandbox\`, the instructor shows two green test runs, one honest and one
  where a test was weakened, and compares the two test diffs. You say how you
  told them apart.

**Independent exercise**
- The instructor tells you first, then opens a pull request in the practice repo
  with green checks. Decide whether its tests still prove what they claimed.
  Predict what the test diff will show before you open it. Merge only if you
  would stand behind it; otherwise request changes, naming the exact test and why.

**Mastery check**
- Explain why green checks were not enough here.
- Explain when changing a test is the right call.

---

### L33: Triage a review finding (fix it or explain it)

*Not every finding is right. Check it, then fix it or answer it with evidence.*

**Objectives**
- A review finding, from Agent Review, Bugbot, or a person, is a claim. Check it
  before acting on it.
- To check a claim, reproduce it: run the code, or write a test that would fail
  if the claim is true.
- If it is real, fix it on the same branch and prove it. If it is not, reply
  with the evidence and leave the code alone.
- Keep the reply short: what you checked, what happened, and what you decided.

**Commands:** `python converter.py <conversion> <value>`, `python -m unittest`,
`gh pr view --comments`, `gh pr comment`

**Cursor:** Review > Find Issues, Agent Review in the Source Control view, and
replying on the pull request.

**Hands-on**
- In `sandbox\`, the instructor runs Agent Review on a small change, checks one
  finding with a quick test, and decides. You say what evidence decided it.

**Independent exercise**
- Request: *"Add a fluid-ounces-to-milliliters conversion (`floz-to-ml`)."* Have
  an agent do it on a branch and open a pull request. Run Agent Review.
- The instructor tells you first, then adds findings of its own, labeled
  "Instructor review." For every finding, predict whether it is real, check it
  with evidence, then fix it or reply with the evidence. Merge when every
  finding is closed.

**Mastery check**
- Explain what evidence settled each finding.
- Explain what it costs to "fix" a finding that was not real.

---

### L34: Revising agent work (feedback to the same agent, same branch)

*When review finds a problem, the fix goes back to the same agent, on the same branch.*

**Objectives**
- A problem found in review belongs to the same request. Send it to the same
  chat, and the fix goes on the same branch, like review feedback in L8.
- Good feedback names the file and line, what it does now, and what it should do.
- Prove the work again after the fix. The earlier proof no longer counts.
- If the approach is wrong, not just a detail, revert and fix the plan instead (L28).

**Commands:** `gh pr view --comments`, `gh pr diff`, `gh pr checks`,
`git log --oneline`, `python -m unittest`

**Cursor:** a follow-up in the same chat. The message queue, or steering while it works.

**Hands-on**
- In `sandbox\`, the instructor reviews an agent's change, sends one follow-up
  in the same chat, and shows the new commit on the same branch. You say what it
  showed.

**Independent exercise**
- Request: *"Add a tablespoons-to-milliliters conversion (`tbsp-to-ml`)."* Have
  an agent do it on a branch and open a pull request.
- The instructor tells you first, then leaves an "Instructor review" comment.
  Send the feedback to the same agent. Predict how many branches and pull
  requests exist afterward. Prove the pull request was updated, prove the work
  again, and merge.

**Mastery check**
- Explain why the fix went to the same chat and branch, not a new one.
- Explain when you would revert and re-plan instead of sending a fix.

---

### L35: Debugging with an agent (Debug mode, evidence first)

*Reproduce it, collect evidence, then make a small fix.*

**Objectives**
- Debug mode does not guess. It lists possible causes, adds temporary logging,
  asks you to reproduce the bug, reads what happened, then makes a small fix.
- You reproduce the bug and you confirm the fix. The agent removes its logging
  after you confirm.
- A good bug report has the steps, the expected result, the actual result, and
  any error message.
- Add a test that fails without the fix, so the bug stays fixed.

**Commands:** `python converter.py <conversion> <value>`, `python -m unittest`,
`git status`, `git diff`

**Cursor:** Debug mode in the mode picker, and the reproduction steps it asks you to run.

**Hands-on**
- In `sandbox\`, the instructor runs Debug mode on a small planted bug. You say
  what evidence the agent used to choose its fix.

**Independent exercise**
- The instructor tells you first, then plants one bug in `practice\` on a branch
  and gives you a one-line bug report. Turn it into a full bug report in Debug
  mode. Predict the cause before the agent's evidence comes back. Reproduce when
  asked, confirm the fix, and add a test that fails without it.
- Prove with `git diff` that no logging is left and only the fix and the test
  changed. Take it through your normal pull request.

**Mastery check**
- Explain what the runtime evidence showed that a guess would not.
- Explain why you added a test that fails without the fix.

---

## Part 6: The project brain

What should outlast one chat goes in committed files. Build the project brain,
then put each piece of guidance where it applies. This comes before any copies,
so every copy starts with the brain. The part ends with Milestone 1: one real
feature through everything since Part 3.

The brain files belong in `practice\`, not in this course folder's `.cursor\`
rules. Those course rules tell the instructor how to teach.

### L36: The project brain (AGENTS.md, rules, and skills)

*A chat is not the memory.*

**Objectives**
- The lasting brain is files in the `practice\` repo: `AGENTS.md` at the repo
  root, rules in `.cursor/rules/`, and skills in `.cursor/skills/`.
- Rules are there for every chat. A skill is read when the task fits.
  `AGENTS.md` is plain instructions for this repo.
- A file counts after it is committed and pushed. Every new chat reads the repo
  as it is. A sentence typed in a chat does not travel.

**Commands:** the branch, commit, and pull request workflow you already know.
`git ls-files`, `git show`, `git log --oneline origin/main`.

**Cursor:** `AGENTS.md` at the repo root, `.cursor/rules/`, `.cursor/skills/`, and
invoking a skill with `/` in the chat.

**Hands-on**
- In `sandbox\`, the instructor adds an instruction to `AGENTS.md` without
  committing it, then commits it, and shows what `git status` and `git show`
  report each time. You say what that showed before moving on.

**Independent exercise**
- On a branch in `practice\`, add an `AGENTS.md`, one short rule, and one short
  skill, in your own words. They should say how to run this repo's tests, that
  `main` changes only when you accept a request, and the preference you kept
  from L29. Review, merge, and push.
- Start a new chat and give it a small request without repeating any of those
  instructions. Predict whether it follows them. Prove from Git and GitHub that
  the files are on `main`.

**Mastery check**
- Explain why the L29 preference was not part of the project brain until you
  committed it.
- Explain what a later worktree or cloud agent will get from these files, and why.

---

### L37: Scoped rules (and which brain file to use)

*Put each piece of guidance where it applies, and nowhere else.*

**Objectives**
- A project rule can apply always, only to files that match a pattern, when the
  agent decides it is relevant from its description, or only when you `@` it.
- Scope a rule to the files it is about, so it doesn't use up context in every chat.
- Choose the right home: `AGENTS.md` for plain repo-wide notes, a rule for a
  convention, a skill for a multi-step workflow, and nothing at all when a
  script or a check already enforces it.
- A User Rule in Cursor settings follows you to every project, but it is not in
  the repo, so worktrees and cloud agents never see it. Keep personal
  preferences there and project knowledge in the repo.
- Project rules are `.mdc` files in `.cursor/rules/` with a short header:
  `description`, `globs`, and `alwaysApply`.

**Commands:** `git ls-files .cursor`, `git show`

**Cursor:** the rule header, `@` a rule by name, and the rules list in Cursor settings.

**Hands-on**
- In `sandbox\`, the instructor adds a rule scoped to Markdown files, then gives
  one chat a Python edit and another a Markdown edit. You say when the rule applied.

**Independent exercise**
- On a branch in `practice\`, add a rule that applies only to test files and
  says tests must not be weakened (L32). Move one piece of guidance from your
  L36 brain files to the home where it belongs, and remove it from the old place.
- Predict which of two requests picks up the test rule: one that edits
  `README.md`, and one that adds a test. Show evidence from each chat, then take
  it through a pull request.

**Mastery check**
- Explain why you scoped the rule instead of making it always apply.
- Explain when you would write no rule at all.

---

### L38: Milestone 1: Solo agent sprint (Parts 3–6 on one real feature)

*One agent, one real feature, and everything since Part 3, without being told which lesson comes next.*

**Objectives**
- Take one feature from request to merged pull request with a single agent in
  your own checkout, choosing each step yourself.
- Use Parts 3–6 together: a request the agent can check, an edited plan, one
  chat, proof before merge, feedback to the same agent, Debug mode when
  something fails, and a brain update.
- Catch the planted traps: a review finding that's wrong, and a chance for the
  agent to weaken a test.

**Commands:** anything from L21 to L37

**Cursor:** anything from L21 to L37, chosen by you.

**Hands-on**
- No demo. Before you start, you say your plan: the steps in order and what each
  one proves. That is your prediction. The instructor then only observes, apart
  from the planted traps.

**Independent exercise**
- Request: *"Accept a comma-separated list of values, such as `km-to-miles 1,5,10`,
  and print one result per line, with tests and docs."*
- Write the request with done-when checks and a test the agent can run, approve
  an edited plan, and keep the work to one chat on a branch.
- The instructor tells you first, then plants a wrong review finding and a moment
  where the agent could weaken a test to get green. Handle both with evidence.
  Send one real problem back to the same agent, and chase one failing case in
  Debug mode.
- Merge only after at least two kinds of proof. Then add one scoped rule you
  learned to the brain, in its own commit.

**Mastery check**
- For each trap, explain what you noticed and how you proved it.
- Explain which step you'd be most tempted to skip next time, and what skipping it
  would have let through.

---

## Part 7: Code you didn't write

Most real work happens in code someone else wrote. Learn it before you change
it: map it and check the map, then pin down what it does today before you
reshape it.

### L39: Map an unfamiliar codebase (a code map in the brain)

*Before changing code you didn't write, learn where things are, and check what the agent tells you.*

**Objectives**
- Start by asking, not editing: the entry points, how data moves, where the
  tests are, and what is risky to touch.
- An agent's summary can be wrong. Check each claim against the code with the
  navigation from L21.
- Save what you learned as a short code map in the brain, so the next chat and
  every copy starts with it.
- Keep the map short, and point to files instead of copying code.

**Commands:** `python -m unittest`, `git log --oneline -- <path>`, `git show`

**Cursor:** Ask mode, Go to Definition, Find All References, and `@` a folder.

**Hands-on**
- In `sandbox\`, the instructor asks an agent to map a small unfamiliar folder,
  then checks two of its claims with Go to Definition and Search. You say which
  claim held up.

**Independent exercise**
- The instructor tells you first, then adds a small module to `practice\` as a
  "teammate" change that you have not read. Before asking anything, predict
  where its entry point is.
- In Ask mode, build a map: entry points, what calls what, where it is tested,
  and one thing that is risky to change. Check every claim yourself. Commit the
  map to the brain through a pull request.

**Mastery check**
- Explain how you caught, or ruled out, a wrong claim in the agent's map.
- Explain why the map lives in the brain and not in a chat.

---

### L40: Characterize, then refactor in small steps

*Pin down what the code does today, then change its shape without changing what it does.*

**Objectives**
- Characterization tests record what the code does now, including the odd
  parts. They are a safety net, not a statement that the behavior is right.
- A refactor changes structure, not behavior. The characterization tests should
  pass before and after every step.
- Refactor in small commits you could review one at a time. Push after each, so
  CI checks every step.
- If you find a real bug while refactoring, note it and fix it in a separate request.

**Commands:** `python -m unittest`, `git log --oneline`, `git push`, `gh run list`

**Cursor:** the agent chat, and Plan mode for the refactor steps.

**Hands-on**
- In `sandbox\`, the instructor writes one characterization test for a small
  function with an odd edge case, then refactors it in two commits. You say what
  the test protected.

**Independent exercise**
- On a branch, write characterization tests for the teammate module from L39,
  with an agent's help, including at least one odd case. Commit them.
- Plan a refactor of that module in at least three small steps, with one commit
  per step, pushing each. Predict which step is most likely to break a test.
  Prove with `gh run list` that every step was green, and that no test changed
  after the first commit. Take it through a pull request.

**Mastery check**
- Explain why you kept an odd behavior instead of fixing it during the refactor.
- Explain what the small commits gave you.

---

## Part 8: A repo that stands on its own

Every copy of the repo, a worktree, a cloud agent, or a teammate's clone, starts
from what is committed. Before you hand work to copies, make the repo able to
set itself up and check itself: pinned dependencies with one setup command,
more automatic checks in CI, and a fresh clone that proves none of it depends on
your machine. The part ends with Milestone 2: taking over a teammate's branch.

### L41: Dependencies and one setup command (pinned versions)

*The repo lists what it needs, at exact versions, and sets itself up with one command.*

**Objectives**
- A dependency is outside code your project uses. Development tools, like a
  linter, are dependencies too.
- Pin exact versions in a file in the repo (for Python, a requirements file with
  `==`), so every copy installs the same thing.
- Install into a virtual environment inside the project, and keep that folder out of Git.
- Document one setup command in the README and `AGENTS.md`, so people and agents
  start the same way.

**Commands:** `python -m venv .venv`, `.venv\Scripts\activate`,
`python -m pip install -r requirements-dev.txt`, `python -m pip freeze`,
`git status`, `git check-ignore -v .venv`

**Cursor:** the integrated terminal, and choosing the project's Python
interpreter from the Command Palette.

**Hands-on**
- In `sandbox\`, the instructor adds one pinned tool, installs it into a fresh
  virtual environment, and shows `git status` before and after ignoring that
  folder. You say what belongs in Git and what does not.

**Independent exercise**
- On a branch in `practice\`, add one linter as a pinned development dependency
  (Ruff is a good choice). Create the virtual environment, install from your
  requirements file, keep the environment out of Git, and document the one setup
  command in the README and `AGENTS.md`. Predict what `git status` shows after
  installing.
- Delete the virtual environment, rebuild it using only your documented command,
  and show the linter runs. Take it through a pull request.

**Mastery check**
- Explain why the version is pinned.
- Explain why the requirements file is committed but the virtual environment is not.

---

### L42: More automatic checks (a command-line test and a linter in CI)

*Tests check behavior. Other checks catch other mistakes, and CI runs them all on every pull request.*

**Objectives**
- Unit tests call one function. A command-line test runs the program the way a
  user does, and catches wiring mistakes that unit tests miss.
- A linter flags likely mistakes without running the code.
- Each check is another signal an agent can run by itself, and another thing
  that must be green before you accept.
- Add the checks to the CI workflow from L6, and make them required, like the tests.
- Fix what a check finds, or configure it on purpose. Don't silence it to get green (L32).

**Commands:** `python -m unittest`, the linter's check command, `gh pr checks`,
`gh run view --log-failed`

**Cursor:** the workflow file in `.github/workflows/`, and the ruleset page on GitHub.

**Hands-on**
- In `sandbox\`, the instructor shows a unit test that passes while running the
  program fails, then a lint finding in code that runs fine. You say what each
  check caught that the other did not.

**Independent exercise**
- On a branch, add one command-line test that runs `converter.py` the way a user
  would and checks what it prints.
- Add the linter from L41 to the CI workflow next to the tests, and make both
  required on `main`. Predict whether the current code passes the linter. Fix or
  deliberately configure what it finds. Show every check green on the pull
  request, then merge.

**Mastery check**
- Explain what the command-line test catches that the unit tests do not.
- Explain why a new check only protects `main` once it is required.

**Salesforce callback.** You also add a workflow that deploys the merge commit
to your integration sandbox. L20 is already Mastered by this point. Production
stays out of this lesson. A package version installed in each org is the later
form of that same promotion.

---

### L43: A fresh clone (does the repo work without your machine?)

*Clone the repo into a new folder. If it doesn't set up and pass there, a cloud agent can't either.*

**Objectives**
- `git clone` copies a repository from GitHub into a new folder, with its
  history, and sets `origin` for you.
- A fresh clone has only what is committed and pushed. Anything that exists only
  on your machine is missing.
- The repo should set itself up with the documented command and pass every check
  from a clean folder. That is the starting point every cloud agent gets.
- Fix what is missing in the repo, not on your machine.

**Commands:** `git clone <url> <folder>`, `git remote -v`, `git log --oneline -3`,
`git config --show-scope -l`, the setup command from L41, `python -m unittest`,
and the linter.

**Cursor:** the Command Palette's Git: Clone, and File > Open Folder.

**Hands-on**
- In `sandbox\`, the instructor clones a small local repo into a new folder and
  shows what came with it and what did not. You say what was missing and why.

**Independent exercise**
- Clone the practice repo from GitHub into a new folder beside `practice\`.
  Before you open it, predict three things that will be missing.
- Follow only the README to set it up, run every check, and confirm the brain
  files are there. Fix anything the clone exposed, through a pull request in
  `practice\`. Then delete the clone.

**Mastery check**
- Explain why a cloud agent's starting point is like your fresh clone.
- Explain why the fix went into the repo instead of onto your machine.

---

### L44: Milestone 2: Take over a teammate's branch (Parts 7–8 with L12)

*Learn someone else's code, pin it down, tidy its history, and leave the repo able to stand on its own.*

**Objectives**
- Inherit an unfamiliar module safely: map it, check the map, and pin down its
  behavior before changing it.
- Refactor in small, green steps, and clean up the branch's history before review (L12).
- Leave the repo self-sufficient: one setup command, the checks in CI, and a fresh
  clone that passes.

**Commands:** anything from L12 and L39 to L43, including `git rebase -i`,
`git clone`, and `gh pr checks`

**Cursor:** Ask mode, Go to Definition, Find All References, Plan mode, and the agent chat.

**Hands-on**
- No demo. Before you start, you say the order you'll work in and what each step
  protects. That is your prediction.

**Independent exercise**
- The instructor tells you first, then pushes a "teammate" branch with a small
  module you haven't read and a messy history: vague messages, a fix-up commit,
  and a stray debug line.
- Map the module, check every claim, and save the map to the brain. Write
  characterization tests, then refactor in at least two small commits, each green in CI.
- Before opening the pull request, clean the branch with interactive rebase so
  each commit is one clear step. Add any checks the module needs to CI, prove the
  whole repo sets up and passes from a fresh clone, and merge.

**Mastery check**
- Explain why you pinned down the module's behavior before refactoring it.
- Explain why the history was cleaned before review, and not after the merge.

---

## Part 9: Isolated copies

Each request gets its own copy of the repo, so your folder and `main` stay as
they are while the work happens: first on your machine (worktrees), then on
another machine (cloud agents). Each kind of copy also needs setup so it can
install and test, and you learn to move a task between your machine and the
cloud.

### L45: Git worktrees (one repo, several folders)

*A second checkout of the same repo. The main folder stays put.*

**Objectives**
- A worktree is another folder, checked out from the same repository, on its own branch.
- Creating one does not switch the `practice\` folder. Edits in the extra folder stay there.
- Create a worktree, list them, and remove one.

**Commands:** `git worktree add -b <branch> <path>`, `git worktree list`,
`git worktree remove <path>`, plus `git status` in each folder.

Put the extra folder beside `practice\`, not inside it.

**Cursor:** none in this lesson. You use the terminal so you can see the two
folders. The next lesson is Cursor's `/worktree` command.

**Hands-on**
- The instructor creates a worktree in `sandbox\`, changes a file only in that
  folder, and you compare `git status` in both folders.
- You do the same once in `practice\`: add a worktree, list it, compare status,
  then remove it.

**Independent exercise**
- Create a worktree on a new branch, outside `practice\`. Before you open it,
  predict whether your L36 brain files are in the new folder, then check.
  Change a file only in that folder. Predict `git status` in both folders before
  you look. Remove the worktree. Show what happened to the extra folder and to
  the branch.

**Mastery check**
- Explain why the `practice\` folder did not pick up the other folder's edit.
- Explain what removing the worktree took away, and what you could still find
  in the repository afterward.

---

### L46: Cursor `/worktree` (review, then apply or discard)

*Start with `/worktree`. Review the diff. Apply or discard. Then delete.*

**Objectives**
- `/worktree` runs that one request in a separate checkout. The main checkout
  stays untouched while the work is going on.
- You review the diff before the result comes back.
- `/apply-worktree` brings the result into the main checkout. Discarding does
  not. `/delete-worktree` removes the extra checkout after either choice.

**Commands:** `git worktree list`, `git status`, `git diff`

**Cursor:** `/worktree`, then review the diff, then `/apply-worktree` or
discard, then `/delete-worktree`. In the IDE these are the worktree commands.
Setting up a new worktree so it can test is the next lesson.

**Hands-on**
- You start the request in a separate agent chat. The instructor does not run
  it for you. Before you apply or discard, predict what each choice does to
  the `practice\` folder.

**Independent exercise**
- Request: *"Add a grams-to-kilograms conversion (`g-to-kg`)."*
  Start it with `/worktree`. Check it with at least one kind of proof from L31.
  Apply it or discard it, then `/delete-worktree`. Prove the extra checkout is gone, and prove whether the
  `practice\` folder received the change.

**Mastery check**
- Explain what `/worktree` kept out of the main checkout until you chose.
- Explain what the other choice (apply or discard) would have done to that folder.

---

### L47: Worktree setup (`worktrees.json`, so local copies can test)

*`.cursor/worktrees.json` sets up each new worktree. Your main checkout stays as it is.*

**Objectives**
- A new worktree starts with the committed files only. Ignored things, such as
  a virtual environment or installed packages, are not there.
- `.cursor/worktrees.json` lists setup commands Cursor runs when it creates a
  worktree. On Windows, `setup-worktree-windows` is used before `setup-worktree`.
- The file is committed, so every new worktree gets the same setup.

**Commands:** `git worktree list`, `git status` in both folders,
`python -m unittest` in the worktree

**Cursor:** `.cursor/worktrees.json`. Output panel > **Worktrees Setup** to see
what ran. `/worktree`, `/apply-worktree`, `/delete-worktree`.

**Hands-on**
- In `sandbox\`, the instructor creates one worktree without a setup file and
  one with it, and runs the tests in each. You say what it showed.

**Independent exercise**
- Add `.cursor/worktrees.json` so each new worktree creates its own Python
  virtual environment, runs your setup command from L41, and runs the tests
  once. Take it through a pull request.
- Start `/worktree` with the request: *"Add a miles-per-hour to
  kilometers-per-hour conversion (`mph-to-kph`)."* Predict what `git status`
  shows in the new worktree right after setup, and in `practice\`. Prove both
  from the setup output and Git. Finish the request as in L46.

**Mastery check**
- Explain why a fresh worktree needed setup at all.
- Explain how you proved the setup did not touch your main checkout.

---

### L48: Cloud agents (work on another machine, returned as a PR)

*The agent works on its own branch and opens a pull request. `main` changes only when you accept it.*

**Objectives**
- A cloud agent clones the repo and edits on its own branch, on another machine.
  Your `practice\` folder is not where the edit happens.
- The result comes back as a pull request.
- `main` stays as it is until you accept that request by merging. Local `main`
  still does not have it until you pull.

**Commands:** `gh pr view`, `gh pr diff`, `gh pr checks`, `git status`,
`git switch main`, `git pull --ff-only`

**Cursor:** choose **Cloud** in the dropdown under the agent input. You can
also start one from [cursor.com/agents](https://cursor.com/agents). One run is
enough. It uses your Cursor plan and can cost money; set a spend limit if
Cursor asks.

**Hands-on**
- The instructor does not start the agent. You start one cloud agent on the
  practice repo. While it works, `git status` on your `main` is the check that
  your folder was not the place being edited.

**Independent exercise**
- Request: *"Add a meters-to-centimeters conversion (`m-to-cm`)."*
  Let the agent open the pull request. Before you merge, predict whether
  GitHub `main` and your local `main` contain the change. Check the pull
  request with the proof from L31. Accept the request only if you mean to.
  Pull, and prove when `main` changed.

**Mastery check**
- Explain why your files stayed as they were while the agent was working.
- Explain what you did by merging that the agent did not do.

---

### L49: Cloud environment setup (`environment.json` and secrets)

*The cloud environment installs and tests on another machine.*

**Objectives**
- A cloud agent needs an environment: the repo, tools, dependencies, and any
  secrets. Without it, the agent can edit but can't prove its work.
- Cursor's guided setup prepares the environment. Its configuration can be
  saved in the repo as `.cursor/environment.json`. The `install` step runs when
  Cursor prepares a Build.
- Cloud-agent secrets go in the Secrets tab on cursor.com, not in the repo.
- Cloud-only setup notes can go in their own section of `AGENTS.md`.

**Commands:** `gh pr view`, `gh pr diff`, `gh pr checks`,
`git log --oneline -- .cursor/environment.json`

**Cursor:** the Cloud Agents dashboard (environments, Builds, Secrets). Cloud
in the dropdown under the agent input. Setup and one agent run use your Cursor
plan and can cost money.

**Hands-on**
- In `sandbox\`, the instructor shows a sample `environment.json` and what each
  part does. The cloud steps are yours; the instructor doesn't start them.

**Independent exercise**
- Set up the practice repo's cloud environment so an agent can run your setup
  command, the tests, and the linter. Commit its configuration through a pull request. Add a
  short "Cursor Cloud specific instructions" section to `AGENTS.md` in your
  own words.
- Start one cloud agent: *"Add a kilometers-per-hour to miles-per-hour
  conversion (`kph-to-mph`)."* Before you start it, predict which branch's
  configuration it uses. Show from the run that the tests ran on that machine,
  and show `main` unchanged until you merge.

**Mastery check**
- Explain why a cloud agent that can't run the tests hasn't proven anything.
- Explain why the secret belongs in the Secrets tab, not in `environment.json`.

---

### L50: Moving work between local and cloud (`/in-cloud` and back)

*Hand a task to the cloud, keep working, then bring the result back to test.*

**Objectives**
- From a local chat, `/in-cloud` sends the next task to a cloud agent on its own
  machine and branch. Your checkout stays free.
- A cloud agent's branch can come to your machine: fetch it and switch to it, or
  move the agent to local in the Agents Window, then test it yourself.
- You can follow up on a cloud agent from cursor.com/agents or the Cursor phone app.
- Cloud agents leave evidence, such as logs and screenshots. Use it alongside
  your own checks, not instead of them.

**Commands:** `git fetch`, `git switch <branch>`, `python -m unittest`,
`gh pr view`, `gh pr checks`

**Cursor:** `/in-cloud`, moving an agent between cloud and local in the Agents
Window, cursor.com/agents, and the Cursor phone app. One cloud run uses your
Cursor plan and can cost money.

**Hands-on**
- No sandbox demo: this runs in the cloud. Before you start, the instructor goes
  through where each control is with you.

**Independent exercise**
- Request: *"Add a hectares-to-acres conversion (`ha-to-ac`)."* Send it to the
  cloud with `/in-cloud`. While it runs, make a small local change on a
  different branch. Send one follow-up to the cloud agent from the web or your phone.
- When it opens a pull request, bring its branch to your machine and run the
  tests. Predict which branch your folder is on at each step. Check the pull
  request with the proof from L31, then merge.

**Mastery check**
- Explain what stayed free on your machine while the cloud agent worked.
- Explain why you tested the cloud branch yourself even though it came with its own evidence.

---

## Part 10: Planning and parallel work

Bigger requests, and more than one at a time. Split a request into tasks and see
which can run side by side, keep the queue in GitHub Issues, and handle the two
ways parallel work collides: text conflicts that Git reports, and clashes in
behavior that it doesn't. The part ends with Milestone 3: shipping a release
built by parallel agents.

### L51: Break a big request into tasks (what goes first, what runs in parallel)

*Some tasks must go first. Others can run side by side.*

**Objectives**
- A request too big for one reviewable pull request gets split into tasks, each
  small enough for one pull request.
- Some tasks depend on others. Write down which must go first. The longest chain
  of dependent tasks sets the shortest possible finish.
- Tasks that don't depend on each other can run in parallel, each in its own copy.
- Save the plan in the repo, so every task, chat, and agent can read it.

**Commands:** `git log --oneline`, `gh pr list`

**Cursor:** Plan mode, and "Save to workspace" (saved plans go in `.cursor/plans/`).

**Hands-on**
- In `sandbox\`, the instructor splits a small request into three tasks and marks
  which depends on which. You say which two could run at once.

**Independent exercise**
- Request: *"Group the conversions by category (length, weight, volume,
  temperature) in the help text and the README."* In Plan mode, break it into
  tasks, each small enough for one pull request. Mark which must come first and
  which can run in parallel. Predict how many pull requests it needs.
- Save the plan to the repo through a pull request, then do only the first task.

**Mastery check**
- Explain why the first task had to go first.
- Explain what would go wrong if two dependent tasks ran at the same time.

---

### L52: GitHub Issues as the request queue (and `@cursor`)

*Each request becomes an issue. Each pull request closes one.*

**Objectives**
- An issue holds one request: the outcome and what "done" means. Open issues are
  the queue of work waiting for an agent or a person.
- A pull request that says `Closes #<number>` closes that issue when it merges,
  linking the request to the change.
- Commenting `@cursor` on an issue or pull request can start a cloud agent on it,
  once the GitHub integration is connected.
- Issue text is input the agent reads. Anyone who can write an issue is writing
  into the agent's instructions.

**Commands:** `gh issue create`, `gh issue list`, `gh issue view`,
`gh pr create`, `gh pr view`

**Cursor:** `@cursor` in a GitHub comment, and cursor.com/agents. One cloud run
uses your Cursor plan and can cost money.

**Hands-on**
- No sandbox demo: issues live on GitHub. You create the first issue with the
  instructor watching, and you say what each part of it is for.

**Independent exercise**
- Turn the remaining tasks from L51 into issues, one per task, each with an
  outcome and done-when.
- Start one task by commenting `@cursor` on its issue. Do another with a local
  agent. Predict what happens to each issue when its pull request merges, and
  prove it with `gh issue list`.

**Mastery check**
- Explain what the `Closes` link gives you that a pull request alone does not.
- Explain why issue text needs the same care as anything else an agent reads.

---

### L53: Two requests at once (parallel copies, and the one that goes stale)

*Run two at once. When one merges, the other must catch up and be proven again.*

**Objectives**
- Two requests can run at the same time, each in its own copy and on its own branch.
- When the first merges, the second branch is behind `main`. If both changed the
  same lines, its pull request conflicts.
- Bring the second up to date with `main` (L9), resolve by the intended result,
  prove it again, then merge.
- Smaller, separate requests conflict less. An agent can help resolve a
  conflict, but you review the result.

**Commands:** `git worktree list`, `gh pr list`, `git fetch origin`,
`git merge origin/main`, `gh pr checks`

**Cursor:** two `/worktree` chats, or one worktree and one cloud agent. The merge editor.

**Hands-on**
- In `sandbox\`, the instructor runs two worktrees that change the same line,
  merges one, and shows the other. You say what happened to the second.

**Independent exercise**
- Request A: *"Add a cups-to-milliliters conversion (`cup-to-ml`)."* Request B:
  *"Add a quarts-to-liters conversion (`qt-to-l`)."* Start both before either
  finishes, each in its own copy. Predict which files both will change, and
  whether B conflicts after A merges.
- Prove and merge A. Bring B up to date, resolve any conflict, prove it again,
  and merge. Remove both copies and show `git worktree list`.

**Mastery check**
- Explain why B had to be proven again after the update.
- Explain how you would split requests to make that conflict less likely.

---

### L54: Semantic conflicts (both pass alone, fail together)

*Git merges the text. Only a test or a review catches a clash in behavior.*

**Objectives**
- Two changes can merge with no conflict in Git and still break when combined,
  because each assumed something the other changed.
- Checks that ran before the other change merged no longer count. Test the
  combined result.
- GitHub can require a branch to be up to date before it merges. Know whether
  your ruleset does.
- Decide which change reflects the intended behavior, and fix the other on its own branch.

**Commands:** `git fetch origin`, `git merge origin/main`, `python -m unittest`,
`gh pr checks`, `gh run list`

**Cursor:** two `/worktree` chats, or one worktree and one cloud agent. The
ruleset page on GitHub.

**Hands-on**
- In `sandbox\`, the instructor merges two branches that don't touch the same
  lines but together break a test. You say why Git didn't warn.

**Independent exercise**
- Request A: *"Round every conversion to 3 decimal places, and add a test that
  checks every conversion does."* Request B: *"Add a feet-to-inches conversion
  (`ft-to-in`)."* Run both at once, each in its own copy, and prove each alone.
- Merge A. Predict whether B conflicts in Git, and whether B still passes
  afterward. Bring B up to date, find out, fix it on B's branch, prove the
  combined result, and merge. Check whether your ruleset would have stopped B
  from merging while it was out of date.

**Mastery check**
- Explain how two changes can merge cleanly and still break.
- Explain why B's earlier green checks did not count.

---

### L55: Milestone 3: Ship a release with parallel agents (Parts 9–10 with L14)

*Split a request, run it in parallel isolated copies, catch the clash, and ship a tagged release.*

**Objectives**
- Break a medium request into dependent tasks, track each as an issue, and run
  the independent ones at the same time in isolated copies.
- Keep `main` safe while parallel work lands: prove again anything that went
  stale, and catch a clash in behavior that Git can't see.
- Ship: tag a release with notes (L14), then record what you learned in a
  separate knowledge commit.

**Commands:** anything from L45 to L54, including `gh issue list`, `git tag -a`,
and `gh release create`

**Cursor:** `/worktree`, a cloud agent, the Agents Window, and Plan mode. Cloud
runs use your Cursor plan and can cost money.

**Hands-on**
- No demo. Before you start, you sketch the task order and say which tasks can
  run together and why. That is your prediction.

**Independent exercise**
- Request: *"Add area and speed conversions, for example `sqft-to-sqm` and
  `knots-to-kph`, that share one new rounding helper."*
- Plan the tasks and turn them into issues. Run two at once in separate worktrees
  and one on a cloud agent, each on its own branch.
- Prove and merge them one at a time, bringing each later branch up to date
  first. When the tasks meet, find and fix the clash in behavior (there will be
  one), and prove the combined result.
- Tag the release and publish it on GitHub with notes. Then update the knowledge
  files in a separate small commit, and show that `main` changed only when you merged.

**Mastery check**
- Explain which tasks could run in parallel, and why the rest had to wait.
- Explain how you knew the combined result worked, not just each piece.

---

## Part 11: Tools, guardrails, and automation

Workers, outside tools, and agents that start work without you. Each step gives
agents more reach, so each lesson adds a limit: read-only workers, one tool with
the least access, reading untrusted text as data, a hook that blocks production
writes, a coordinator that delegates but does not write the change, and
automations that still end in work you review. The part ends by pruning the
brain, measuring whether your workflow pays off, a guided run through every
control, and a capstone you do on your own.

### L56: Subagents (workers that search, test, or review)

*The parent request stays in charge. Workers search, test, or review.*

**Objectives**
- A subagent is a worker with its own clean context. The parent gives it a
  prompt, it does one job, and it reports back.
- The parent keeps the request. It decides what changes and hands one result
  back for you to check.
- A worker can be read-only (`readonly: true`): no file edits, no commands that
  change anything.
- Subagents share the parent's checkout unless you ask for isolation.
- Custom workers live in `.cursor/agents/` and are committed, like the rest of the brain.

**Commands:** `git status`, `git diff`, `git log --oneline`

**Cursor:** the built-in workers (Explore, Bash, Browser). A custom worker file
in `.cursor/agents/`. `/name` to call a worker by name.

**Hands-on**
- In `sandbox\`, the instructor has the parent send a search to a worker and
  shows what comes back to the parent. You say what it showed.

**Independent exercise**
- Add one read-only worker in `.cursor/agents/` that checks finished work by
  running the tests and reporting what passed. Commit it through a pull request.
- Run the request *"Add a stones-to-kilograms conversion (`st-to-kg`)"* in a
  worktree, and have the parent use your worker before handing back. Predict
  what the worker will change. Prove from the chat and from Git who changed what.

**Mastery check**
- Explain why the worker's report is not the same as you accepting the work.
- Explain why this worker was read-only.

---

### L57: MCP tools (one tool, least access)

*One MCP server, with only the access it needs.*

**Objectives**
- MCP connects the agent to an outside tool, such as GitHub, so the agent can
  read or act there.
- The tool can do only what its access allows. Give it the smallest access that
  works, for one repo.
- Cursor asks before it uses an MCP tool. Read the arguments before you approve.
- Connect one tool, test it, and turn it off when you don't need it.
- The key never goes in the repo. A project `.cursor/mcp.json` can point to an
  environment variable instead.

**Commands:** `gh pr list`, `git fetch`, `git log --oneline origin/main`

**Cursor:** Customize (add, enable, and disable MCP servers). `.cursor/mcp.json`
with `${env:NAME}`. The tool approval prompt. Output panel > **MCP Logs**.

**Hands-on**
- In `sandbox\`, the instructor shows a sample `.cursor/mcp.json` that points to
  an environment variable, and what an approval prompt shows. You say what the
  file does and does not contain.

**Independent exercise**
- Before connecting anything, write down what the GitHub tool should be allowed
  to do in the practice repo, and what it should not.
- Connect a GitHub MCP server with access to the practice repo only, able to
  read but not merge or push. Ask the agent to list your open pull requests.
  Then ask it to merge one. Predict each result. Show what happened, show that
  `main` did not change, and turn the server off.

**Mastery check**
- Explain what decided whether the merge could happen.
- Explain why you connect one tool at a time.

---

### L58: Prompt injection (read it as data, not orders)

*Anything an agent reads can contain instructions. Treat it as data.*

**Objectives**
- Issues, web pages, files, and tool results are input. Some of it can contain
  instructions written to steer an agent.
- The agent should report such text, not follow it. You check what it actually did.
- Keep reading and writing apart: an agent that reads untrusted text should have
  the least power to write (L57).
- Your defenses stack: least access for tools, approvals, hooks (next lesson),
  and review before merge.

**Commands:** `gh issue view`, `git status`, `git log --oneline origin/main`

**Cursor:** the tool approval prompt, and the GitHub tool from L57 or `gh`.

**Hands-on**
- In `sandbox\`, the instructor puts a harmless planted instruction inside a text
  file and asks an agent to summarize the file. You say what the agent did with it.

**Independent exercise**
- The instructor tells you first, then opens an issue in the practice repo that
  contains a harmless planted instruction. Ask an agent to read the issue and
  plan a fix, without mentioning the planted text. Predict what it will do.
- Show whether it followed the planted text, and show that nothing was written
  without your approval. Add one line about untrusted input to the brain through
  a pull request.

**Mastery check**
- Explain how the issue's author was able to steer the agent at all.
- Explain which of your defenses would have stopped a harmful write, and in what order.

---

### L59: Hooks (a hard block on production writes)

*A rule can be ignored. A hook can block. Keep the approval prompt too.*

**Objectives**
- A rule is an instruction. The agent usually follows it, but nothing forces it.
- Keep Cursor asking before shell commands you have not allowed. That is a
  person deciding, one command at a time.
- A hook is a script Cursor runs at a step in the agent loop. A
  `beforeShellExecution` hook can deny a command before it runs.
- Project hooks live in `.cursor/hooks.json`, are committed, and also run in
  cloud agents.
- A hook that crashes lets the command through unless it is set to fail closed.

**Commands:** `git push`, `git fetch`, `git log --oneline origin/main`

**Cursor:** `.cursor/hooks.json` and a hook script in `.cursor/hooks/`. The
command approval prompt. The run mode setting for agent commands.

**Hands-on**
- In `sandbox\`, the instructor adds a rule against a harmless command, then a
  hook that denies it, and asks an agent to run it each time. You say what it showed.

**Independent exercise**
- Add a project hook that stops a work-request agent from deploying or writing
  to production: deny any command that deploys, and any push to `main`. It must
  fail closed. Commit it through a pull request.
- In a worktree, ask the agent to push straight to `main`, and separately to
  push its own branch. Predict both results. Show the block message, show
  `origin/main` unchanged, and show the allowed push worked.

**Mastery check**
- Explain why a rule alone was not enough.
- Explain how you knew the hook stopped the push, and not GitHub's rule on `main`.

---

### L60: Projects (a coordinator that delegates)

*A Project plans and delegates. It does not write the production change.*

**Objectives**
- A Project is a coordinator chat in the Agents Window. It plans the work,
  starts agents that write the code, and brings the result back to you.
- The workers run in isolation. `main` changes only when you accept a pull request.
- A Project keeps its own shared notes. Those notes are not the committed
  brain. What should last goes into the repo's knowledge files.
- The knowledge update is its own commit, after the request is accepted.

**Commands:** `gh pr list`, `gh pr diff`, `gh pr checks`, `git log --oneline`, `git show`

**Cursor:** Agents Window > Projects > New Project. The coordinator chat.
Opening a worker the coordinator started. Projects run on cloud agents, use
your Cursor plan, and are not available with Privacy Mode (Legacy) or on
Enterprise plans.

**Hands-on**
- No sandbox demo: Projects run only in the cloud. Before you create anything,
  you tell the instructor what the coordinator will do and what it will not do.
  The instructor checks it against the docs with you.

**Independent exercise**
- Create a Project on the practice repo. Give it: *"Add a yards-to-meters
  conversion (`yd-to-m`)."* Tell it the coordinator must not write the change
  itself. Predict where the change will be written.
- Check the worker's pull request with the proof from L31, then accept or
  reject it. Then write what you learned about the coordinator into the
  knowledge files, in its own commit.

**Mastery check**
- Explain why the coordinator does not write the change itself.
- Explain why the Project's shared notes do not replace the committed knowledge files.

---

### L61: Project subscriptions (schedules and GitHub events)

*A schedule or a GitHub event can start a new request. You still accept the result.*

**Objectives**
- A subscription tells the Project to act on a signal: a schedule, pull request
  activity, or CI runs on a branch.
- Each signal becomes a new work request, done by a worker in isolation.
- The Listening list shows every subscription, and you can remove one there.
- Keep one subscription at a time while you learn it.

**Commands:** `gh pr list`, `gh run list`, `git fetch`, `git log --oneline origin/main`

**Cursor:** asking the coordinator to subscribe. The **Listening** pill above
the chat input. Removing a subscription from that list.

**Hands-on**
- No sandbox demo: subscriptions run only in the cloud. Before you subscribe,
  you tell the instructor the signal, what the coordinator should do, and what
  it must not do. You read the Listening list together after you add it.

**Independent exercise**
- Subscribe the practice Project to one GitHub event in the practice repo, such
  as a failed CI run on a branch. Trigger it once yourself. Predict what the
  coordinator will do and what happens to `main`.
- Show the worker's result, check it, and accept or reject it. Remove the
  subscription and show the Listening list afterward.

**Mastery check**
- Explain what the subscription could do without you, and what it could not.
- Explain why you removed it at the end.

---

### L62: Automations (new work from a trigger)

*An automation starts a new cloud agent run each time its trigger fires.*

**Objectives**
- An automation runs a cloud agent in the background, on a schedule or when an
  event happens, such as CI finishing on a pull request.
- Each run is new work. A Project subscription (L61) wakes the same coordinator
  conversation instead. A hook (L59) runs inside an agent's own steps and can block them.
- Set what it can touch: which repo, which tools, and whether it may open pull
  requests. Each run costs money.
- It still ends in a pull request or a comment you review. `main` changes only
  when you accept.

**Commands:** `gh run list`, `gh pr list`, `gh pr view --comments`,
`git log --oneline origin/main`

**Cursor:** `/automate` in a chat, or the Automations page on cursor.com.
Triggers such as "CI completed." Run history. Turning an automation off.

**Hands-on**
- No sandbox demo: automations run in the cloud. Before you create one, you tell
  the instructor the trigger, what it may do, and what it must not do.

**Independent exercise**
- For three situations the instructor gives you, predict whether an automation,
  a subscription, or a hook fits each one.
- Create one automation on the practice repo that, when CI fails on a pull
  request, reads the failure and comments with a diagnosis. It must not push to
  `main`. Trigger it once with a branch whose test fails. Show the run history
  and its comment, check the diagnosis yourself, then turn the automation off.

**Mastery check**
- Explain which of the three you would use for a nightly check, for blocking a
  command, and for continuing one ongoing piece of work.
- Explain why you turned the automation off at the end.

---

### L63: Pruning the brain (remove what's duplicated, wrong, or unused)

*A brain that only grows goes stale. Remove what is duplicated, wrong, or unused.*

**Objectives**
- Every chat, copy, and cloud agent reads the brain. A wrong rule spreads to all of them.
- Duplicated or conflicting guidance confuses the agent, and always-on rules use
  up context in every chat.
- When an agent keeps making the same mistake, trace it to its source: a missing,
  vague, or harmful line.
- Pruning is its own small commit, like any knowledge update.

**Commands:** `git log --oneline -- AGENTS.md .cursor`, `git show`, `git diff`

**Cursor:** `AGENTS.md`, `.cursor/rules/`, `.cursor/skills/`, and a fresh chat to
test the result.

**Hands-on**
- In `sandbox\`, the instructor shows two rules that contradict each other and a
  chat that follows the wrong one. You say how you would find which line caused it.

**Independent exercise**
- The instructor tells you first, then adds one "teammate" change to the brain
  that makes agents do something wrong. Give a new chat a small request, notice
  the wrong behavior, and predict which file causes it before you look. Fix it.
- Read the whole brain and remove anything duplicated, outdated, or unused. Take
  the cleanup through a pull request, and show a fresh chat doing the request correctly.

**Mastery check**
- Explain how you traced the behavior to its source.
- Explain why pruning is its own commit.

---

### L64: Measuring your agent workflow (time, rework, and cost)

*Decide how to work from evidence, not habit.*

**Objectives**
- Three numbers show whether a way of working pays off: time from request to
  accepted work, how much rework it needed, and what it cost.
- Pull request timestamps and commit history show time and rework. Your Cursor
  usage page shows cost.
- Change one thing at a time, such as the model, Plan mode, or local vs. cloud,
  so you know what made the difference.
- A few requests only hint at an answer. Say what your numbers cannot tell you.

**Commands:** `gh pr list --state merged --json number,title,createdAt,mergedAt`,
`gh pr view <number> --json commits`, `git log --oneline`

**Cursor:** the usage page in your Cursor dashboard.

**Hands-on**
- The instructor finds the three numbers for two of your past pull requests
  (read-only) and shows where each came from. You say which number surprised you.

**Independent exercise**
- For your last five accepted requests, record the time to accept, the revision
  commits after the first review, and the cost where you can find it. Predict
  which way of working was cheapest per accepted request.
- Pick one thing to change, then do the request *"Add a miles-to-nautical-miles
  conversion (`mi-to-nmi`)"* with that change. Compare the numbers, and commit a
  short note of what you found to the knowledge files, in its own commit.

**Mastery check**
- Explain why you changed only one thing.
- Explain one thing your numbers cannot prove.

---

### L65: Full-loop practice (one request through every control)

*Plan, hide secrets, test in an isolated copy, review, block, decide, then update the brain.*

**Objectives**
- Take one work request through every control in order, with proof at each step.
- Say what each step protected.

**Commands:** everything from L21 to L64

**Cursor:** everything from L21 to L64. You choose which controls to use at each step.

**Hands-on**
- Before you start, you list the steps in order and what each one proves. That
  list is your prediction. The instructor only observes.

**Independent exercise**
- Request: *"Add a US-gallons-to-liters conversion (`gal-to-l`)."*
  - Plan it in Plan mode. Accept the plan only after you have reviewed and edited it.
  - Show that the fake key from L25 is hidden from the agent and can't be committed.
  - Run the work on a branch, in a worktree or with a cloud agent that installs
    and runs the tests.
  - Review the result with at least two kinds of proof.
  - Show the hook blocking a push to `main` during the request.
  - Accept or reject the request.
  - Update the knowledge files in a separate small commit.

**Mastery check**
- For each step, name the proof you showed and what it protected.
- Explain what was true of `main` at each step before you accepted.

---

### L66: Agent capstone (an unfamiliar request, scored)

*One realistic request, revealed when it starts. Minimal prompting.*

**Objectives**
- Take a request you have not seen from intake to accepted work, choosing every
  step yourself.
- Handle surprises along the way without being told which lesson they come from.

**Commands:** anything from L21 to L65

**Cursor:** anything from L21 to L65, chosen by you.

**Hands-on**
- No demo. The instructor reveals the request. Before you start, you say your
  plan and what each step will prove. That is your prediction. The instructor
  then only observes and scores.

**Independent exercise**
- You receive an **unfamiliar, realistic request**. It is revealed only when the
  capstone starts. Expect surprises along the way: a second request that
  overlaps, review feedback, a failing check, and an attempt to write to
  production.

**Rubric** (each item is scored Solid, Shaky, or Missed)
- Request written with an outcome, the files to follow, done-when, and a check the agent can run
- Plan reviewed and edited before any file changed
- Secrets hidden from the agent and out of every commit
- Work done on a branch, in an isolated copy that installs and tests
- At least two kinds of proof before accepting
- Test changes checked, and no test weakened to make the checks pass
- Each review finding checked, then fixed or answered with evidence
- Text from issues, pages, or tools treated as data, not instructions
- Review feedback sent to the same agent, on the same branch
- The overlapping request brought up to date, resolved, and proven again
- The production write stopped by the hook, not by luck
- Accept or reject decided and explained
- Knowledge files updated in a separate small commit
- Cleanup: copies removed, no MCP server or subscription left on, local `main` updated

Any Shaky or Missed item goes into "Mistakes to revisit" for a targeted retest.

**Mastery check**
- For each surprise, explain what you noticed and why you chose your response.
- Explain what was true of `main` at each step before you accepted the work.

---

## Command and Cursor reference

| Goal | Terminal | Cursor Source Control |
|------|----------|-----------------------|
| See what changed | `git status`, `git diff` | Changes list; click a file for the diff editor |
| Stage a file | `git add <path>` | `+` next to the file |
| Unstage a file | `git restore --staged <path>` | `-` next to the staged file |
| See staged changes | `git diff --staged` | Click a file under "Staged Changes" |
| Commit | `git commit -m "..."` | Type the message, then click Commit |
| Discard edits (permanent) | `git restore <path>` | Discard Changes (curved arrow) |
| See history | `git log --oneline --graph` | Source Control Graph; file Timeline |
| Create or switch branch | `git switch -c <b>` / `git switch <b>` | Branch name in the status bar |
| Merge a branch | `git merge <b>` | `...` menu > Branch > Merge |
| Resolve a conflict | Edit markers, then `git add` | Accept Current / Incoming / Both, or the merge editor |
| Download remote changes | `git fetch` | `...` menu > Fetch |
| Fetch plus merge | `git pull --ff-only` | `...` menu > Pull (Cursor uses your pull settings) |
| First push of a branch | `git push -u origin <b>` | Publish Branch |
| Pull then push | `git pull` then `git push` | Sync Changes (arrows in the status bar) |
| Set work aside | `git stash` | `...` menu > Stash |
| Undo last commit (keep changes) | `git reset --soft HEAD~1` | `...` menu > Commit > Undo Last Commit |
| Add a second checkout | `git worktree add -b <branch> <path>` | `/worktree` starts an agent in one |
| List checkouts | `git worktree list` | |
| Remove a second checkout | `git worktree remove <path>` | `/delete-worktree` |
| Bring a worktree result into this folder | | `/apply-worktree` |
| Agent on another machine | `gh pr diff`, then merge when you accept | Cloud, under the agent input |
| Run any command by name | | Command Palette (Ctrl+Shift+P) |
| Open a file by name | | Quick Open (Ctrl+P) |
| Find a function | | Go to Symbol (Ctrl+Shift+O, or Ctrl+T for the project) |
| Search every file | | Search (Ctrl+Shift+F) |
| Work with issues | `gh issue create`, `gh issue list` | `@cursor` in a GitHub comment |
| Copy a repo from GitHub | `git clone <url> <folder>` | Command Palette > Git: Clone |
| Accept an AI suggestion | | Tab (Escape rejects) |
| Change a selection | | Inline Edit (Ctrl+K) |
| Undo agent edits | `git restore`, `git revert` | Undo, or Restore Checkpoint |
| Debug with evidence | `python -m unittest` | Debug mode |
| Plan before editing | | Plan mode (Shift+Tab), then build |
| Ask without editing | | Ask mode |
| Hide files from the agent | | `.cursorignore` |
| Set up each new worktree | | `.cursor/worktrees.json` |
| Block a command | | `.cursor/hooks.json` |

**Cursor traps to know**
- Clicking **Commit** with nothing staged may offer to stage *everything*.
  Stage deliberately instead.
- **Discard Changes** cannot be undone for uncommitted work.
- **Sync Changes** pulls *and* pushes in one click. Know which direction you need.
- The AI commit-message button is fine to use, but you own the message. Read it.
- `/apply-worktree` writes the result into your main checkout. Discarding, then
  `/delete-worktree`, does not.
- A cloud agent's pull request does not change `main` until you merge it.
- A checkpoint is not a commit. Commit before an agent session.
