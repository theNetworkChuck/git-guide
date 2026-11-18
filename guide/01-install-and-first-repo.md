# 1. Install Git and make your first repo

**Video:** 3:01 to 7:28
**What you'll do:** install Git, build a tiny project, turn it into a Git repo, and make your first save point.

## Step 1: Check if you already have Git

Git comes preinstalled on a lot of systems. Check first:

```bash
git --version
```

If you see something like `git version 2.50.1`, you're good. Skip to step 2.

If you get "command not found", install it:

| You're on | Run this |
|-----------|----------|
| **Mac** | `xcode-select --install` (or `brew install git` if you use Homebrew) |
| **Ubuntu / Debian / WSL2** | `sudo apt update && sudo apt install git` |
| **Fedora** | `sudo dnf install git` |
| **Windows** | `winget install --id Git.Git -e`, or the installer from [git-scm.com/downloads](https://git-scm.com/downloads) |

Then run `git --version` again.

## Step 2: Make a project to track

Make a folder and jump in:

```bash
mkdir gitgood
cd gitgood
```

Create two files. First a basic web page:

```bash
nano index.html
```

Type anything, like `Hey, it's a website`, then save: **Ctrl+X**, then **Y**, then **Enter**.

Then a story:

```bash
nano zombiestory.md
```

Type `Hey, it's a zombie story`, and save the same way (**Ctrl+X**, **Y**, **Enter**).

```bash
ls
```

```
index.html  zombiestory.md
```

> [!TIP]
> What you type doesn't matter. If you'd rather copy the exact starter files, they're in [`examples/`](../examples).

## Step 3: Tell Git who you are

Three settings, set once per computer. The first two sign your name on every save point you make. The third names your first branch `main` (you'll see why in chapter 3).

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --global init.defaultBranch main
```

Nothing prints when they work. That's normal.

## Step 4: Turn the folder into a Git repo

One command:

```bash
git init
```

```
Initialized empty Git repository in /Users/you/gitgood/.git/
```

"Empty" because Git isn't tracking anything yet. List everything, hidden files included:

```bash
ls -la
```

There's a new hidden folder called `.git`. That folder **is** the repo. Every save point you make lives in there, on your computer.

## Step 5: Get your bearings

```bash
git status
```

```
On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	index.html
	zombiestory.md
```

Three things to notice:

1. You're on a branch called `main`.
2. There are no commits (save points) yet.
3. Your two files are **untracked**. They live in the folder, but Git isn't watching them.

## Step 6: Stage your files with `git add`

You can add one file at a time:

```bash
git add index.html
```

Or everything in the folder at once (that's a space and a dot):

```bash
git add .
```

Check again:

```bash
git status
```

```
Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   index.html
	new file:   zombiestory.md
```

Your files are now **staged**. They're not saved yet. Staging is Git's waiting room: think of a letter that's written, in the envelope and stamped, but not in the mailbox yet.

## Step 7: Your first commit

Put the letter in the mailbox:

```bash
git commit -m "my first commit"
```

```
[main (root-commit) 6933913] my first commit
 2 files changed, 2 insertions(+)
 create mode 100644 index.html
 create mode 100644 zombiestory.md
```

`-m` is your message: a short note about what this save point is. All the output means is your two files are now part of the repo. That's your first save point.

## Step 8: Look at your history

```bash
git log
```

```
commit 693391359ee1f6fe44574dc59dda615620757214 (HEAD -> main)
Author: Your Name <you@example.com>
Date:   Wed Nov 18 08:32:52 2026 -0600

    my first commit
```

Who made it, when, and your message. The long string of letters and numbers is the commit's **hash**, its ID. Your hash will be different from this one.

For a quick one-line-per-commit view:

```bash
git log --oneline
```

```
6933913 (HEAD -> main) my first commit
```

You'll use `git log --oneline` constantly from here on.

## The three places a change can live

| Where | What it means | How it gets there |
|-------|---------------|-------------------|
| **Your folder** | You edited the file. Only the file knows. | You type and save |
| **Staging** | Git has it ready to save, but hasn't saved it | `git add` |
| **A commit** | Saved for good. A save point you can go back to | `git commit` |

**Next:** [2. See changes, undo them, time travel](02-diff-restore-time-travel.md)
