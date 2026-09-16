# 02: Branching and Merging

## 1. Why Branches Exist

Branches let you isolate work without disturbing the main project line. In a club or team project, this is useful for:

- new features
- bug fixes
- experiments or model tuning attempts
- writing documentation
- testing new ideas safely

A good convention is to use prefixes like:

- `feat/` for features
- `fix/` for bug fixes
- `experiment/` for exploration
- `docs/` for documentation improvements

## 2. Basic Branch Commands

### List branches

```bash
git branch
```

Example output:

```text
* main
```

### Create a new branch

```bash
git checkout -b feat/data-cleaning
```

Modern Git equivalent:

```bash
git switch -c feat/data-cleaning
```

Example output:

```text
Switched to a new branch 'feat/data-cleaning'
```

### Switch branches

```bash
git switch main
```

### Delete a merged branch

```bash
git branch -d feat/data-cleaning
```

Example output:

```text
Deleted branch feat/data-cleaning (was 8d42d1a).
```

## 3. Example Feature Branch Workflow

```bash
git switch main
git pull origin main
git switch -c feat/eda-dashboard
# make changes to files
# inspect and stage them
git add .
git commit -m "feat: add exploratory dashboard notebook"
git push -u origin feat/eda-dashboard
```

This creates a clean branch for work that is not yet ready to be merged into the main project line.

## 4. Merge Strategies

### A. Fast-forward merge

A fast-forward happens when the target branch has not moved forward since the feature branch was created.

```text
main: A --- B --- C
feat:              D --- E
```

When merged, the branch pointer simply moves forward:

```text
main: A --- B --- C --- D --- E
```

This is the cleanest case.

### B. Three-way merge commit

This occurs when both branches have independent commits.

```text
main:    A --- B --- C
feat:    A --- B --- D --- E
```

Git creates a merge commit to combine both histories.

```bash
git switch main
git merge feat/data-cleaning
```

Example output:

```text
Merge made by the 'ort' strategy.
```

### C. Squash merge

A squash merge takes all changes from the feature branch and collapses them into one commit on the main branch.

```bash
git switch main
git merge --squash feat/data-cleaning
```

Then commit explicitly:

```bash
git commit -m "feat: add data cleaning workflow"
```

Squash merges are often preferred in student or research repos to keep history cleaner and easier to review.

## 5. Rebasing: When and Why

Rebasing moves commits from one branch onto another branch.

```bash
git switch feat/data-cleaning
git rebase main
```

This can produce a cleaner linear history, but it rewrites commit history. Be careful when the branch is already pushed to others or is shared.

### Rebase vs merge

- Use merge for shared or collaborative branch history.
- Use rebase when you want a clean local history before opening a PR.
- Do not rebase public/shared history unless your team agrees.

## 6. Merge Conflicts: A Real Workflow

Conflicts happen when two branches edit the same lines in the same file.

### Example

Start from a shared branch:

```bash
git switch main
git pull origin main
git switch -c feat/model-config
```

Edit a file, then switch back and edit the same lines:

```bash
git switch main
git switch -c fix/model-config
```

Now merge:

```bash
git merge feat/model-config
```

Git will report a conflict:

```text
Auto-merging config.yaml
CONFLICT (content): Merge conflict in config.yaml
Automatic merge failed; fix conflicts and then commit the result.
```

Open the file and Git will show markers like this:

```yaml
learning_rate: 0.01
<<<<<<< HEAD
batch_size: 32
=======
batch_size: 64
>>>>>>> feat/model-config
```

### Resolve the conflict

Decide which version is correct, then edit the file manually:

```yaml
learning_rate: 0.01
batch_size: 64
```

Then stage the resolved file:

```bash
git add config.yaml
```

Finish the merge:

```bash
git commit
```

Git opens an editor so you can write the merge commit message. If you want a short one:

```bash
git commit -m "merge: resolve model config conflict"
```

## 7. Conflict Resolution Checklist

- Read both versions carefully.
- Keep the correct final logic.
- Remove all conflict markers `<<<<<<<`, `=======`, `>>>>>>>`.
- Stage the resolved file.
- Commit the merge result.
- If unsure, ask a teammate for review.

## 8. Branching Best Practices

- Keep branches short-lived.
- Name branches clearly and consistently.
- Open a pull request once the branch is ready.
- Merge only after review and validation.
- Never merge without checking the diff.

## 9. Summary

Branching helps teams work in parallel safely. Understanding merge strategies and conflict resolution is essential because real collaborative development almost always includes at least one difficult merge. The right habit is to make small, reviewable changes, keep the main branch clean, and resolve conflicts deliberately instead of forcing a merge.

The next step is [03: Collaboration and PRs](./03-collaboration-and-pr.md).
