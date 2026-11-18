# 8. Troubleshooting

The problems hit while filming come first, then the ones people hit most often.

| You see | Why | Fix |
|---------|-----|-----|
| `git push` asks for a **username and password** even though `gh auth login` worked | Git isn't using the GitHub CLI to log in | `gh auth setup-git`, then push again. Happened in the video |
| `gh issue create --label feature` fails | That label doesn't exist in the repo yet | Use a built-in label (`bug`, `documentation`, `enhancement`), or create it first: `gh label create feature`. List them: `gh label list` |
| `fatal: destination path 'gitgood' already exists` on `git clone` | A folder with that name is already there | Clone inside a new folder (`mkdir testgitgood && cd testgitgood`), or give the clone a new name: `git clone <url> gitgood-copy` |
| `gh pr merge` says the pull request **is not mergeable** | A merge conflict | [Chapter 7](07-conflicts-and-revert.md), step 5 |
| `git branch` doesn't show the agent's branch | It's a remote branch you haven't fetched, and plain `git branch` only shows local ones | `git fetch`, then `git branch -a` |
| `You are in 'detached HEAD' state` | You checked out an old commit instead of a branch | Nothing's broken. `git switch main` to come back |
| `git diff` shows nothing, but you changed files | The changes are already staged | `git diff --staged` |
| `Author identity unknown` / `Please tell me who you are` when committing | You skipped the `git config` step | Chapter 1, step 3 |
| `git status` says `On branch master`, not `main` | The repo was made before you set `init.defaultBranch` | Rename it: `git branch -m master main` |
| `error: failed to push some refs ... the remote contains work that you do not have locally` | Someone (or your agent, or you on the website) pushed first | `git pull`, then `git push` |
| `nothing to commit, working tree clean` | There are no changes to save | Change a file first, or you already committed it |
| `fatal: not a git repository` | You're not inside the repo folder | `cd ~/gitgood` |
| `CONFLICT (content): Merge conflict in ...` after `git pull` or `git merge` | You and someone else changed the same lines | [Chapter 7 bonus](07-conflicts-and-revert.md#bonus-do-it-all-from-the-terminal), or back out with `git merge --abort` |
| `nano: command not found` | No nano installed (common on Windows) | Use any editor you like: `notepad index.html`, VS Code, vim |
| You committed a password or key by accident | `.gitignore` only stops files that were never committed | Change that password or key **now**. Deleting the file afterward doesn't remove it from history |

## Still stuck?

- `git status` tells you where you are and usually what to do next. Read the hints in parentheses.
- `git <command> --help` opens the manual for any command.
- The free Pro Git book: [git-scm.com/book](https://git-scm.com/book).
