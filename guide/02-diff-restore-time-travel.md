# 2. See changes, undo them, time travel

**Video:** 7:28 to 11:07
**What you'll do:** change your files and see exactly what changed, stage and commit it, break a file and restore it, then jump back in time to your first commit and come home.

## Step 1: Change both files

Add a line to the story and take something away (the video deletes a comma):

```bash
nano zombiestory.md
```

```
It was a dark, stormy night in Resident Evil land.
Hey it's a zombie story
```

Save (**Ctrl+X**, **Y**, **Enter**). Do the same to the web page:

```bash
nano index.html
```

```
This is a website about why we love zombies.
Hey it's a website
```

## Step 2: See exactly what changed with `git diff`

```bash
git diff
```

```diff
diff --git a/zombiestory.md b/zombiestory.md
--- a/zombiestory.md
+++ b/zombiestory.md
@@ -1 +1,2 @@
-Hey, it's a zombie story
+It was a dark, stormy night in Resident Evil land.
+Hey it's a zombie story
```

Read it by the first character of each line:

- A line starting with **`-`** was removed (the old line with the comma).
- A line starting with **`+`** was added.

Git knows about these changes, but they only live in your files right now. They aren't saved.

## Step 3: Stage it, and watch `git diff` go quiet

```bash
git add .
git diff
```

Nothing prints. Your changes didn't disappear: they moved to staging, and plain `git diff` only shows changes that are **not** staged yet. To see what's staged:

```bash
git diff --staged
```

There they are again.

## Step 4: Commit it

```bash
git commit -m "our first change"
git log --oneline
```

```
15271c9 (HEAD -> main) our first change
6933913 my first commit
```

Two save points. Newest on top.

**What's `HEAD -> main`?** It's the "you are here" dot on the mall map. It tells you which commit you're standing on right now. The short codes on the left are each commit's hash (its ID). You'll use one in step 7.

## Step 5: Break something

Open the story and delete a line on purpose:

```bash
nano zombiestory.md
```

Delete `It was a dark, stormy night...`, then save. Your story is broken.

## Step 6: Restore it from the last save point

```bash
git restore zombiestory.md
cat zombiestory.md
```

The deleted line is back. `git restore` throws away your unsaved edits to that file and puts back the version from your last commit.

> [!WARNING]
> `git restore` is permanent for those edits. Anything you changed since your last commit, in that file, is gone. That's the point, so use it on purpose.

## Step 7: Make one more commit (one you'll hate)

Add `I hate this change` to the end of both files, then:

```bash
git add .
git commit -m "I hate this change"
git log --oneline
```

```
0f5861c (HEAD -> main) I hate this change
15271c9 our first change
6933913 my first commit
```

Three save points, and you're on the newest.

## Step 8: Time travel to your first commit

Copy the hash of your **first** commit (the one at the bottom, `6933913` here; yours is different) and check it out:

```bash
git checkout 6933913
```

```
Note: switching to '6933913'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.
...
HEAD is now at 6933913 my first commit
```

Lots of words. The line that matters is the last one: **HEAD is now at your first commit**. You're in the DeLorean. Prove it:

```bash
git log --oneline
cat zombiestory.md
```

Only one commit shows, and the story is back to its first version.

**"Detached HEAD"** sounds scary but isn't. It means you're looking at an old save point instead of standing on a branch. Nothing is broken and nothing is lost.

## Step 9: Back to the present

```bash
git switch main
```

```
Previous HEAD position was 6933913 my first commit
Switched to branch 'main'
```

All three commits are back. `main` is your main branch, the real timeline. More on branches next.

## Step 10: Where all of this actually lives

```bash
ls -la .git
```

Every commit, every save point, all the time-travel data is in this one hidden folder on your computer. No cloud, no GitHub. That's all Git.

**Next:** [3. Branches](03-branches.md)
