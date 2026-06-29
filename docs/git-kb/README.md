# Git Knowledge Base

My personal Git playbook for working on this repo. Written in plain words, grown as I
learn. Each file is one topic. Start at the top, add a new file whenever I learn something
new worth keeping.

> **How to use this KB:** when I hit a Git situation I don't remember, I search here first
> (`grep -ri "keyword" docs/git-kb/`). If the answer isn't here, I solve it, then write it
> down so future-me doesn't have to relearn it.

## Index

| File | What it covers |
|------|----------------|
| [01-mental-model.md](01-mental-model.md) | The 3 places a file lives; what a commit/branch really is |
| [02-daily-workflow.md](02-daily-workflow.md) | The everyday loop: `add → commit → push` |
| [03-branching.md](03-branching.md) | Feature branches + Pull Requests |
| [04-troubleshooting.md](04-troubleshooting.md) | Real problems I hit and how I fixed them |

## The one rule

Run `git status` after every step. It always tells me what's going on and what to do next.

## Cheat sheet (the 90% commands)

```bash
git status                 # what changed, and where it sits
git add <file>             # stage a file (pick what to save)
git commit -m "message"    # save a snapshot locally
git push                   # upload to GitHub
git pull                   # download others' changes from GitHub
git log --oneline -5       # see recent history
```
