# 01 · The Mental Model

Understanding *where* changes live is 80% of "getting" Git.

## The 3 places (+ GitHub)

```
edit files   →   git add   →   git commit   →   git push
(working dir)    (staged)       (local repo)     (GitHub / remote)
```

1. **Working directory** — the actual files on disk I edit.
2. **Staging area** — a holding pen where I pick *exactly* what goes into the next commit.
3. **Local repository** — my commit history, saved on my machine.
4. **Remote (GitHub)** — a copy on a server, for backup + sharing.

Most Git commands just move changes between these places.

## What a commit is

A **commit** is a *snapshot* of the whole project at a moment, with a message and a unique
id (hash like `6582308`). Each commit points to its parent → commits form a chain = history.

> A commit is local until I `push`. Pushing is what backs it up to GitHub.

## What a branch is

A **branch** is just a movable label pointing at one commit. `main` is the default branch.
Making a new branch = making a new label I can move independently, so I can work without
touching `main`.

## File states I'll see in `git status`

- **Untracked** — Git has never recorded this file. (`git add` to start tracking.)
- **Modified** — tracked file I changed but haven't staged.
- **Staged** ("Changes to be committed") — ready for the next commit.
- **Clean** — nothing changed since the last commit.
