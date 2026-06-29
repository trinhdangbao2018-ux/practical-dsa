# 02 · Daily Workflow

The loop I repeat for every change: **edit → add → commit → push.**

## One-time setup (per machine)

```bash
git config --global user.name "Trinh Dang Bao"
git config --global user.email "huong.le@monterro.com"
git config --global --list        # verify
```

## The loop, step by step

```bash
git status                            # 1. see what changed
git add <file>                        # 2. stage what I want to save
git status                            # 3. confirm it moved to "to be committed"
git diff --staged                     # 4. review exactly what I'm about to commit
git commit -m "week-01: solve two-sum"  # 5. save the snapshot locally
git push                              # 6. upload to GitHub
git status                            # 7. confirm "working tree clean"
```

## Commit message rules (from this repo's CONTRIBUTING)

- Short, **imperative** mood: `Add…`, `Fix…`, `Solve…` (not "Added" / "Adding").
- Week-scoped for problems: `week-01: solve two-sum with hash map`.
- **One logical change per commit.** This repo's rule: commit per problem.

## Handy partial-staging

```bash
git add .                  # stage everything changed (use carefully)
git add path/to/file.c     # stage just one file (preferred — keeps commits focused)
git restore --staged <f>   # un-stage a file (undo an `add`), keeps my edits
git restore <file>         # discard unstaged edits to a file (CAREFUL: can't undo)
```
