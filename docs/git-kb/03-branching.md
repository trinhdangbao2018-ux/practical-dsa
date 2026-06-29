# 03 · Branching & Pull Requests

Working on `main` directly is fine when learning solo. The professional habit — and what
this repo already uses (see the many `Two_Sum`, `Linked_List_Cycle`, … branches on GitHub)
— is **one branch per piece of work**, merged via a Pull Request.

```
main:     A───B───C─────────────M      ← stable, always working
                   \           /
feature:            D───E───F─┘         ← my work-in-progress
```

## The branch workflow

```bash
# 1. Start fresh from an up-to-date main
git switch main
git pull

# 2. Create + switch to a new branch (one per problem/topic)
git switch -c week-01-two-sum

# 3. Do the work — write code, compile, test
#    gcc -Wall -Wextra -std=c11 -g -fsanitize=address file.c -o out && ./out

# 4. Stage + commit
git add phase-1-foundations/week-01-complexity-arrays/problems/01_two_sum.c
git commit -m "week-01: solve two-sum with hash map"

# 5. Push the branch (first push needs -u to link local↔remote)
git push -u origin week-01-two-sum
```

Then on GitHub: open a **Pull Request** (PR) from `week-01-two-sum` → `main`. A PR is a
request to merge, where review/CI happens. After it's merged:

```bash
git switch main
git pull                          # bring merged work into local main
git branch -d week-01-two-sum     # delete the local branch (work is in main now)
```

## Notes

- `git switch -c name` = create + switch. Older syntax: `git checkout -b name` (same thing).
- `git switch name` = move to an existing branch.
- `git branch` = list local branches; `git branch -a` = include remote ones.
- Even working solo, PRs are worth doing here — this repo runs CI checks on PRs.
