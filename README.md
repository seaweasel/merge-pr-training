# GitHub PR & Merge Training

A practical training repo for learning how to orchestrate open-source collaboration using GitHub pull requests, forks, branches, reviews, and merges.

This workflow simulates a real maintainer/contributor setup using two GitHub accounts and two browsers.

- Chrome account → maintainer
- Firefox account → contributor

The goal is to build operational fluency with:

- forks
- branches
- pull requests (PRs)
- code review
- merge conflicts
- upstream syncing
- collaborative iteration

---

# Mental Model

GitHub collaboration is fundamentally:

```text
base repository
    ↓
contributors create branches/forks
    ↓
contributors propose changes via PRs
    ↓
maintainers review and merge
```

A pull request is not “sending code.”

It is:
- a proposed merge
- attached to discussion
- attached to review
- attached to a diff
- attached to history

This allows maintainers to stabilize systems over time while still permitting experimentation.

---

# Repository Roles

## Maintainer (Chrome account)

Responsibilities:
- owns canonical repository
- reviews PRs
- manages `main`
- merges approved changes
- coordinates contributors

## Contributor (Firefox account)

Responsibilities:
- forks repository
- creates feature branches
- submits PRs
- rebases/syncs fork
- responds to review feedback

---

# Training Exercises

---

# Exercise 1 — Create the Base Repository

Using the maintainer account:

1. Create repository:
   ```text
   merge-pr-training
   ```

2. Add:
   - `README.md`
   - `.gitignore`

3. Keep:
   ```text
   main
   ```
   as the default branch.

---

# Exercise 2 — Fork Workflow

Using the contributor account:

1. Open maintainer repo
2. Click:
   ```text
   Fork
   ```

3. Edit:
   ```text
   README.md
   ```

4. Add a small section:
   ```md
   ## Contributor Note
   Training PR from contributor account.
   ```

5. Commit to:
   ```text
   firefox-readme-edit
   ```

6. Open a pull request.

---

# Exercise 3 — Review & Merge

Using the maintainer account:

1. Open:
   ```text
   Pull Requests
   ```

2. Review:
   - commits
   - changed files
   - diff

3. Leave a comment.

Example:

```text
Looks good. Please add one more line.
```

4. Contributor pushes another commit.

5. Maintainer merges PR.

---

# Exercise 4 — Local Git Workflow

Contributor local workflow:

```zsh
git clone git@github.com:YOUR_USER/merge-pr-training.git

cd merge-pr-training

git remote add upstream \
git@github.com:MAINTAINER_USER/merge-pr-training.git

git checkout -b feature/add-notes

echo "Contributor note" >> README.md

git add README.md

git commit -m "Add contributor note"

git push origin feature/add-notes
```

Then open the PR on GitHub.

---

# Exercise 5 — Syncing a Fork

Contributor sync workflow:

```zsh
git checkout main

git fetch upstream

git merge upstream/main

git push origin main
```

This keeps the fork aligned with the canonical repository.

---

# Exercise 6 — Merge Conflict Training

Purpose:
Learn conflict resolution under competing edits.

## Setup

Maintainer:
- edits a line in `README.md`
- commits directly to `main`

Contributor:
- edits the same line
- pushes PR

GitHub should now report:

```text
This branch has conflicts that must be resolved.
```

---

# Resolving Conflicts Locally

Contributor:

```zsh
git fetch upstream

git checkout feature/add-notes

git merge upstream/main
```

Git will stop and mark conflicts.

Open conflicted files and look for:

```text
<<<<<<< HEAD
your code
=======
incoming code
>>>>>>> upstream/main
```

Manually choose the final version.

Then:

```zsh
git add README.md

git commit

git push origin feature/add-notes
```

The PR updates automatically.

---

# Core Git Commands

## Status

```zsh
git status
```

## Create branch

```zsh
git checkout -b feature/my-change
```

## Stage files

```zsh
git add .
```

## Commit

```zsh
git commit -m "Describe change"
```

## Push branch

```zsh
git push origin feature/my-change
```

## Pull latest

```zsh
git pull
```

## Fetch remotes

```zsh
git fetch --all
```

## View remotes

```zsh
git remote -v
```

---

# Recommended Branch Naming

```text
feature/add-auth
feature/fix-navbar
bugfix/mobile-layout
docs/update-readme
refactor/api-client
```

Keep names:
- short
- descriptive
- stable

---

# Recommended PR Practices

Good PRs are:
- small
- focused
- reviewable
- reversible

Avoid:
- giant unrelated changes
- formatting noise
- mixed concerns

A PR should ideally answer:
1. What changed?
2. Why?
3. What are the risks?
4. How was it tested?

---

# Suggested Repository Protections

Later, as projects mature:

Enable:
- required PR review
- CI checks
- branch protection
- squash merge rules
- CODEOWNERS

These increase coordination quality as project concreteness rises.

---

# Operational Philosophy

Early projects benefit from:
- fast iteration
- low ceremony
- frequent merges

As systems become more load-bearing:
- review depth increases
- migration planning matters more
- compatibility matters more
- change cost rises

This repo exists to practice that transition deliberately.

---

# Canonical Collaboration Loop

```text
fork
  ↓
branch
  ↓
commit
  ↓
push
  ↓
pull request
  ↓
review
  ↓
merge
  ↓
sync fork
```

Repeat until fluent.
