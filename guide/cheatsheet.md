# Git cheat sheet

Every command from the video, in the order you meet them.

## Set up (once per computer)

```bash
git --version                                     # do I have Git?
git config --global user.name "Your Name"         # sign your save points
git config --global user.email "you@example.com"
git config --global init.defaultBranch main       # first branch is called main
```

## Save points

```bash
git init                         # turn this folder into a repo
git status                       # where am I, what changed?
git add index.html               # stage one file
git add .                        # stage everything
git commit -m "my first commit"  # save the game
git log                          # full history
git log --oneline                # short history
```

## See and undo changes

```bash
git diff                         # unstaged changes (+ added, - removed)
git diff --staged                # staged changes
git restore zombiestory.md       # throw away unsaved edits to a file
git checkout <hash>              # time travel to an old commit (detached HEAD)
git switch main                  # back to the present
```

## Branches

```bash
git branch                       # list branches (* = where you are)
git branch zombieattack          # make a branch
git switch zombieattack          # move to it
git switch -c zombieattack       # make it and move to it in one go
git merge zombieattack           # merge it into the branch you're on
git branch -d zombieattack       # delete it
```

## GitHub

```bash
gh auth login                                          # log the GitHub CLI in
gh auth setup-git                                      # fix push asking for a password
gh repo create gitgood --private                       # empty private repo on GitHub
git remote add origin https://github.com/YOU/gitgood.git
git remote -v                                          # show your remotes
git push -u origin main                                # first push
git push                                               # every push after that
git clone https://github.com/YOU/gitgood.git           # download a full copy
git pull                                               # download and merge the latest
git fetch                                              # download, don't merge
git branch -a                                          # local AND remote branches
```

Keep secrets off GitHub: put file names (like `.env`) in a file called `.gitignore`.

## Issues and pull requests

```bash
gh issue create --title "Add a line" --body "Add one more line to zombiestory.md"
gh issue list
gh label list                     # labels you can use with --label
gh pr list
gh pr view 3
gh pr checkout 3                  # fetch a PR's branch and switch to it
gh pr merge 4 --merge             # merge a PR from the terminal
```

## When things go wrong

```bash
git merge --abort                 # back out of a conflicted merge
git revert -m 1 <merge-hash>      # undo a merge with a new commit
```

On GitHub: **Resolve conflicts** on the PR page fixes a conflict. **Revert** on a merged PR undoes it.
