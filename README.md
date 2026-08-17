# 🌿 Git & GitHub — Course Notes

> Personal summary from a Git & GitHub course, organized around the actual local → branch → merge → remote workflow.

---

## 📑 Table of Contents

- [1. Foundations](#1-foundations)
- [2. The Local Workflow](#2-the-local-workflow)
- [3. Branching](#3-branching)
- [4. Merging](#4-merging)
- [5. GitHub & Remotes](#5-github--remotes)

---

## 1. Foundations

### What is version control?

A system that tracks every change made to a project's files — **what** changed, **when**, and **where** the copies live (your machine, or the version control system itself).

### What is Git?

Git is a **distributed** version control system used to track and manage changes in a software project, and to collaborate with a team. It lets you create copies of a project (**branches**) and merge changes between them securely.

Other version control tools exist too: `CVS`, `SVN`, `Perforce`, `Bazaar` — but Git's branching/merging model is why it's the most widely used today.

### Git vs. GitHub

| | Git | GitHub |
|---|---|---|
| **What it is** | The version-control tool | A cloud platform for hosting Git repos |
| **Runs** | Locally, on your machine | Online, accessible from any device |
| **Job** | Tracks and manages changes | Lets you share, edit, and collaborate on projects |

---

## 2. The Local Workflow

| Command | What it does |
|---|---|
| `git init` | Creates a new repository. Sets up the hidden folder Git uses to store the project's history. |
| `git add <file>` | Stages a file — marks it to be included in the next commit. |
| `git commit -m "message"` | Permanently saves staged changes to the repo, with a description. |
| `git log` | Shows the commit history: hash, author, date, and message for each commit. |

```bash
git add file1.txt file2.txt
git commit -m "Added new files"
```

> 📌 A commit is permanent — you can always come back to it to restore that exact state of the project.

### `.gitignore`

A file listing what Git should **never track** — config files, secrets, temp files, build artifacts. Anything listed here stays out of history entirely.

---

## 3. Branching

A **branch** is an independent line of work — a full copy of the project you can safely change without affecting the main line. Once the work is verified, you merge it back in.

| Command | What it does |
|---|---|
| `git branch new-feature` | Creates a new branch (copy of current files + full commit history). |
| `git checkout new-feature` | Switches your active branch. |
| `git switch -c new-feature` | Modern shortcut — combines `branch` + `checkout` in one step. |
| `git revert abc123` | Doesn't delete history — adds a **new** commit that undoes a previous one's changes. |
| `git branch -d branchname` | Deletes a branch. ⚠️ Be careful not to delete the one you're actively on. |

---

## 4. Merging

`git merge branchname` folds another branch's changes into your current branch, creating a new commit that contains both histories. Always check out the target branch first (`git checkout main`) before merging into it.

### Fast-forward vs. 3-way merge

| Type | When it happens | Result |
|---|---|---|
| **Fast-forward** | Main branch has no new changes | Feature commits are just appended — no new merge commit |
| **3-way merge** | Main branch *has* moved on | Git creates a dedicated merge commit reconciling both sides |

### Squash merge

Compresses every commit on a branch into a single, clean commit before merging. Keeps history short and readable — as long as the squashed message actually describes the change.

### Merge conflicts ⚠️

Happen when the same lines are changed differently on two branches. Git flags the conflict and waits for it to be resolved — manually, by picking one side, or with a merge tool — before finishing the merge.

### Merge vs. Rebase

| | ✅ Merge | ⚡ Rebase |
|---|---|---|
| **Pros** | Preserves true history · doesn't rewrite commits · simple to reason about | Clean, linear history · fewer conflicts overall |
| **Cons** | Can get messy with many branches · extra merge commits | Rewrites history · risky on shared branches · can complicate collaboration |
| **Best for** | Shared/team branches | Solo/local cleanup before sharing |

---

## 5. GitHub & Remotes

Code you write is local by default — invisible to anyone else. GitHub gives a repository a home in the cloud so it can be shared by link and edited collaboratively.

### Uploading a project to GitHub

```bash
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/userName/repoName.git
git push -u origin main
```

| Step | Purpose |
|---|---|
| `git init` | Start tracking the project |
| `git add README.md` | Stage the file |
| `git commit -m "first commit"` | Save the staged snapshot |
| `git branch -M main` | Rename the default branch to `main` |
| `git remote add origin <url>` | Link the local repo to a remote named `origin` |
| `git push -u origin main` | Push commits and link local ↔ remote branches |

### `git fetch` vs. `git pull`

| | `git fetch` | `git pull` |
|---|---|---|
| Downloads new remote commits | ✅ | ✅ |
| Merges them automatically | ❌ (manual `git merge` needed) | ✅ |
| Use when | You want to review changes before merging | You want updates merged in immediately |

### Fork vs. Clone

| | 🍴 Fork | 💻 Clone |
|---|---|---|
| **Copies to** | Your own GitHub account | Your local machine |
| **Use case** | Propose changes to someone else's project via a pull request | Get a working local copy of any repo |

---

<p align="center"><sub>✅ merged into <code>main</code> — course complete</sub></p>