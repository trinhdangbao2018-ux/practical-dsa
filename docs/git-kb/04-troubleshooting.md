# 04 · Troubleshooting (real situations I hit)

A growing log of problems and their fixes. Add a new entry each time I get stuck.

---

## Push rejected: "Updates were rejected (fetch first)"

**What I saw:**
```
! [rejected]        main -> main (fetch first)
error: failed to push some refs ...
hint: the remote contains work that you do not have locally
```

**Why:** GitHub's `main` had commits my local `main` didn't have. The two had **diverged**
(split from a common commit). Git refuses to push because it would lose the remote work.

**Fix — pull (rebasing my commit on top), then push:**
```bash
git fetch origin
git log --oneline main..origin/main   # see what THEY have that I lack
git log --oneline origin/main..main   # see what I have that THEY lack
git pull --rebase origin main         # replay my commit on top of their work
git push                              # now it works
```

**`--rebase` vs plain pull:** `--rebase` replays my commits on top → clean straight-line
history (best when I have a small local commit). Plain `git pull` makes an extra "merge
commit" instead. For solo work, prefer `--rebase`.

**Note:** after a rebase my commit's hash changes (it's a *new* replayed commit). Normal.

---

## I staged the wrong file

```bash
git restore --staged <file>    # un-stage it, keeps my edits intact
```

## I want to undo my last commit (but keep the changes)

```bash
git reset --soft HEAD~1        # commit undone, changes back in staging
```

## I messed up the last commit message

```bash
git commit --amend -m "the correct message"   # only if NOT pushed yet
```

## I need to throw away ALL my uncommitted changes

```bash
git restore .                  # CAREFUL: discards every unstaged edit, no undo
```

---

> Template for new entries:
>
> ## Short title of the problem
> **What I saw:** <error / symptom>
> **Why:** <cause in plain words>
> **Fix:** <the commands that worked>
