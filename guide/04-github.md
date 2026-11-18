# 4. Put it on GitHub

**Video:** 15:13 to 22:06
**What you'll do:** install the GitHub CLI, log in, make a private repo on GitHub, keep a secrets file off it, push your repo up, clone a second copy, and pull down a change made on the website.

Everything so far has lived in one folder on your computer. GitHub gives your repo a home in the cloud: a backup, a place to share it, and a place for other people (and agents) to work on it with you. In Git terms, GitHub is your **remote**.

GitHub isn't the only option. GitLab and Bitbucket are cloud services too, and you can self-host your own Git server. This guide sticks with GitHub because almost everyone uses it.

## Step 1: Install the GitHub CLI

You can do all of this on the website, but we're staying in the terminal. Install `gh`:

| You're on | Run this |
|-----------|----------|
| **Mac** | `brew install gh` |
| **Windows** | `winget install --id GitHub.cli` |
| **Linux / WSL2** | Follow the steps for your distro at [cli.github.com](https://cli.github.com) |

Check it:

```bash
gh --version
```

You also need a GitHub account. It's free: [github.com](https://github.com).

## Step 2: Log in

```bash
gh auth login
```

Answer the prompts like this:

| Prompt | Pick |
|--------|------|
| Where do you use GitHub? | **GitHub.com** |
| What is your preferred protocol for Git operations? | **HTTPS** |
| Authenticate Git with your GitHub credentials? | **Yes** |
| How would you like to authenticate GitHub CLI? | **Login with a web browser** |

It prints a one-time code and opens github.com in your browser (or copy the link it prints). Paste the code, approve, and the terminal says you're logged in.

## Step 3: Create an empty repo on GitHub

Make sure you're still in your project folder (`cd ~/gitgood`), then:

```bash
gh repo create gitgood --private
```

`--private` means only you can see it. It prints the new repo's web address, like `https://github.com/YOUR-USERNAME/gitgood`. Open it in your browser: an empty repo, waiting for you.

## Step 4: Keep secrets off GitHub with `.gitignore`

Projects often have files you never want uploaded: passwords, API keys, tokens. Make a fake one:

```bash
nano .env
```

```
password123
```

Save it. Now tell Git to ignore it. Create a file named `.gitignore`:

```bash
nano .gitignore
```

```
.env
```

Save. Every line in `.gitignore` is a file (or pattern) Git will pretend doesn't exist. Check:

```bash
git status
```

```
Untracked files:
	.gitignore
```

`.gitignore` shows up as a new file. `.env` doesn't show up at all. Git will never stage it, so it can never reach GitHub.

> [!TIP]
> `.gitignore` is a normal file, so commit it too. In the video it rides along with the next `git add .` in step 8. If you'd rather commit it now: `git add .gitignore && git commit -m "ignore secrets"`.

> [!WARNING]
> `.gitignore` only works **before** a file is committed. If a secret is ever committed, deleting the file later doesn't remove it: it's still in your history. Change that password or key right away.

## Step 5: Connect your repo to GitHub

Tell your local repo where its remote lives. The name `origin` is the standard nickname for "my main remote":

```bash
git remote add origin https://github.com/YOUR-USERNAME/gitgood.git
git remote -v
```

```
origin	https://github.com/YOUR-USERNAME/gitgood.git (fetch)
origin	https://github.com/YOUR-USERNAME/gitgood.git (push)
```

Use your own username. The URL ends in **`.git`**.

## Step 6: Push it up

```bash
git push -u origin main
```

Read it as: **push** my **main** branch to **origin**. The `-u` makes Git remember that link, so from now on you only type `git push`.

```
To https://github.com/YOUR-USERNAME/gitgood.git
 * [new branch]      main -> main
branch 'main' set up to track 'origin/main'.
```

> [!NOTE]
> If it asks for a username and password even though you logged in, run `gh auth setup-git` and push again. That happened while filming. See [troubleshooting](08-troubleshooting.md).

Refresh the repo in your browser. Your files and your commits are there. Notice what's **not** there: `.env`.

## Step 7: Clone a second copy

`git clone` downloads a whole repo, history and all, into a new folder. Your home folder already has a `gitgood`, so clone into a new folder to avoid a name clash:

```bash
cd ~
mkdir testgitgood
cd testgitgood
git clone https://github.com/YOUR-USERNAME/gitgood.git
ls
cd gitgood
git log --oneline
```

Same commits, same files, its own `.git` folder. It's a complete, separate copy. **Keep this folder.** In chapter 5 it becomes your AI agent's computer.

## Step 8: Change, commit, push

Back to your main folder:

```bash
cd ~/gitgood
nano zombiestory.md
```

Add a line, save, then:

```bash
git diff
git add .
git commit -m "Chuck pulls a coffee out of his beard"
git push
```

The commit lives on your computer first. GitHub doesn't know about it until you `git push`. Refresh GitHub and your new line is there.

## Step 9: Change it on GitHub, pull it down

Now the other direction. On GitHub, open `zombiestory.md`, click the **pencil icon** to edit, add a line, click **Commit changes**, and commit directly to `main`.

Your computer doesn't have that change yet. Pull it:

```bash
git pull
git log --oneline
```

```
Updating c907907..3735d57
Fast-forward
 zombiestory.md | 1 +
```

```
3735d57 (HEAD -> main, origin/main) Edited on GitHub
c907907 Chuck pulls a coffee out of his beard
...
```

`origin/main` is where GitHub's `main` is. `HEAD -> main` is where you are. They match: you're up to date.

| Command | Direction |
|---------|-----------|
| `git push` | Your computer **up to** GitHub |
| `git pull` | GitHub **down to** your computer, merged into your branch |
| `git clone` | A full copy of a GitHub repo into a new folder |

Your AI agent does most of this for you. Now you know what it's doing.

**Next:** [5. Hand issues to an AI agent](05-issues-and-your-agent.md)
