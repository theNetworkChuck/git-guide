# 5. Hand issues to an AI agent

**Video:** 22:06 to 27:05
**What you'll do:** create issues (a to-do list on GitHub), have your AI agent work one on its own branch from "another computer", and grab its branch with `git fetch` so you can look at the work before it touches `main`.

## What issues are

An **issue** is a to-do item attached to a repo: a feature to add, a bug to fix, a question. Issues are a **GitHub** feature, not a Git feature. Git has never heard of them. GitLab, Bitbucket and Gitea all have their own version.

Developers have always used issues as a to-do list. Now they're one of the best ways to hand work to an AI agent: the task is written down, numbered, and tied to the code that fixes it.

## Step 1: Create your first issue

From your main folder (`~/gitgood`):

```bash
gh issue create --title "Add a line" --body "Add one more line to our scary story in zombiestory.md"
```

It prints the issue's web address. List your issues:

```bash
gh issue list
```

Issue **#1**. You've got issues.

## Step 2: Create a second one

```bash
gh issue create --title "Japanese" --body "Translate zombiestory.md into Japanese in another file"
gh issue list
```

Two more options you'll want later:

| Option | What it does |
|--------|--------------|
| `--label bug` | Tags the issue. The label has to **already exist** in the repo |
| `--assignee "@me"` | Assigns it to someone. If an agent watches your repo, assigning it can start the work automatically |
| `--web` | Opens the issue form in your browser instead |

> [!WARNING]
> In the video, `--label feature` failed because new repos don't come with a `feature` label. New repos start with labels like `bug`, `documentation` and `enhancement`. Use one of those (`--label enhancement`), or make your own first with `gh label create feature`. See them all with `gh label list`.

## Step 3: Go to the agent's computer

Pretend your agent works on a different computer. The second copy you cloned in chapter 4 plays that part:

```bash
cd ~/testgitgood/gitgood
git pull
```

`git pull` makes sure this copy has the latest from GitHub before the agent starts.

## Step 4: Hand the issue to your agent

Start your AI coding agent in this folder (Claude Code, Codex, whatever you use) and tell it:

> Work issue #1 on a new branch, then push that branch to GitHub. Don't open a pull request yet.

Watch what it runs. It reads the issue with `gh issue view`, makes a branch, edits the story, and commits, using the same commands you've been typing.

> [!NOTE]
> Your agent runs in your terminal, so it uses **your** Git and **your** GitHub login. Anything you can do, it can do. Read its commands before you approve them.

When it's done, check from this folder:

```bash
git branch
```

There's a new branch (in the video it was named after the issue). That's the agent's alternate timeline. If your agent forgot to push it, tell it to push.

On GitHub, the repo's branch dropdown (top left, says `main`) now shows the agent's branch too.

## Step 5: Go back to your computer

```bash
cd ~/gitgood
git branch
```

```
* main
```

The agent's branch isn't here. It's on GitHub and on the agent's computer, not yours.

## Step 6: `git fetch` the agent's work

```bash
git fetch
```

```
 * [new branch]      issue-1-add-a-line -> origin/issue-1-add-a-line
```

Like a dog: go get it. `git fetch` downloads new branches and commits from GitHub but **doesn't change your files or merge anything**. It's "let me look first."

Your agent's branch name will be different from `issue-1-add-a-line`. Use the one your terminal prints.

## Step 7: Find it with `git branch -a`

```bash
git branch
```

Still just `main`. Plain `git branch` only lists your local branches. Add `-a` for **all**:

```bash
git branch -a
```

```
* main
  remotes/origin/issue-1-add-a-line
  remotes/origin/main
```

There it is, under `remotes/origin/`.

## Step 8: Step into the agent's timeline

First, what the story looks like on `main`:

```bash
cat zombiestory.md
```

Now switch to the agent's branch, using the name **without** `remotes/origin/`:

```bash
git switch issue-1-add-a-line
```

```
Switched to a new branch 'issue-1-add-a-line'
branch 'issue-1-add-a-line' set up to track 'origin/issue-1-add-a-line'.
```

Git saw there's no local branch by that name, found it on `origin`, and made a local copy that tracks it.

```bash
cat zombiestory.md
git log --oneline
```

The agent's new line is there, and its commit is on top. You're ahead of `main`, in the agent's dimension. You've checked its work without touching the sacred timeline.

Head back:

```bash
git switch main
```

The work looks good. Next you'll get it into `main` the way most teams (and agents) do it: a pull request.

**Next:** [6. Pull requests](06-pull-requests.md)
