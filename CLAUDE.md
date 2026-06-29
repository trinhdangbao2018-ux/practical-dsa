# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

This is **not a software product** — it's a 12-week self-study curriculum for learning Data Structures & Algorithms by implementing them from scratch. The "code" is teaching material: reference implementations and solved practice problems. Optimize edits for *pedagogical clarity and correctness*, not for production abstraction. Each source file is standalone and self-testing; there is no shared library, build graph, or package.

**Language strategy:** C for fundamentals (weeks 1–7), C++ for advanced topics (weeks 8–12). Data structures are built in raw C first (manual memory, pointers, no STL) so the internals are understood before STL containers are used later.

## Build & run

Every file compiles and runs on its own. There is no top-level build system in use (see caveat below).

```bash
# C (weeks 1–7) — always with warnings + AddressSanitizer:
gcc -Wall -Wextra -std=c11 -g -fsanitize=address <file>.c -o out && ./out

# C++ (weeks 8–12):
g++ -Wall -Wextra -std=c++17 -g -fsanitize=address <file>.cpp -o out && ./out
```

- `impl/` files and most `problems/` files contain their own `main()` that runs `assert()`-based self-tests and prints `OK`. Compiling + running a file *is* its test suite.
- Multi-file `impl/` (e.g. a `.c` + its `.h`): compile the `.c`; it `#include`s the header. Some impl files guard `main()` with `#ifndef DA_NO_MAIN` so they can be reused as a translation unit — define that macro to compile without the self-test driver.
- **Zero warnings is the standard.** Treat any warning as a bug to fix before moving on.

**CI caveat:** `.github/workflows/cmake-single-platform.yml` runs `cmake`/`ctest`, but there is **no `CMakeLists.txt` in the repo** — so CI currently fails/no-ops. If a build target is needed, either add a `CMakeLists.txt` or adjust the workflow to invoke the per-file `gcc`/`g++` pattern above.

## Repository structure

```
phase-N-<topic>/week-MM-<topic>/
├── notes.md       theory in the learner's own words (starts as a stub)
├── impl/          reference data-structure implementations, one concept per file
├── problems/      solved problems, one file per problem (01_two_sum.c, …)
└── exercises.md   the curated to-do list of problems for the week
```

- Phases 1–6 map to weeks 1–12 (see `README.md` table and `ROADMAP.md` for the week-by-week plan).
- **Week 1 (`phase-1-foundations/week-01-complexity-arrays/`) is the fully-seeded reference example** of every file's intended shape. Use it as the template when filling in any later week. All other weeks start as `.gitkeep` stubs.
- `templates/` holds the starting skeletons: `problem-template.c`, `problem-template.cpp`, `notes-template.md`.
- `docs/guidelines.md` is the authoritative spec for *how* a week is worked (the 7-step per-problem workflow, definition-of-done). `docs/progress.md` is the running journal.

## Conventions (from CONTRIBUTING.md and docs/guidelines.md)

- **Standards:** C11, C++17. Must compile clean under `-Wall -Wextra`.
- **Required header banner** on every `problems/` solution file — problem name, source link, approach (plain English), `Time: O(?)`, `Space: O(?)`, `Notes:`. The plan goes in the header *before* the code is written. See `templates/problem-template.c`.
- **`impl/` files** carry a comment documenting invariants (e.g. `0 ≤ len ≤ cap; data != NULL iff cap > 0`) and include a `main()` that asserts edge cases (empty, single element, after-resize, after-clear).
- **Naming:** `snake_case` in C; `snake_case` functions + `PascalCase` types in C++. No magic numbers (`#define`/`const`). One concept per `impl/` file.
- **Problem file naming:** leading number matches the `exercises.md` order — `01_two_sum.c`, `02_remove_duplicates.c`, …
- **Commits:** short, imperative, week-scoped — e.g. `week-01: add dynamic array reference impl`, `week-04: solve n-queens with iterative backtracking`. Commit per problem.

## Alternative-solution layout

Community/alternative solutions live beside the canonical one:

```
problems/<problem-name>/
├── solution.c            canonical
└── solutions/<handle>/   alternative solutions
    └── solution.cpp
```
