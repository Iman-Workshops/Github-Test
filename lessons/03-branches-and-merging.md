# 03. Branches and Merging

## Goal

This lesson explains how to make a change on a separate branch, compare it with `main`, and bring it back with a merge.

## Branch Mental Model

A branch is a name that points to a commit.

`HEAD` points to the branch you are currently working on. When you create a commit, the current branch moves forward to that new commit.

I draw it like this:

```text
main
  |
  v
A
```

After one new commit on `main`:

```text
main
  |
  v
B
|
A
```

When you create a feature branch, Git creates another name that points to the current commit:

```text
main
feature/add-help
  |
  v
B
|
A
```

If you commit on the feature branch, only that branch moves:

```text
feature/add-help
  |
  v
C
|
B <- main
|
A
```

That picture is the main idea. A branch is not a folder copy. It is a movable name for a commit.

## Create a Branch

From `main`:

```shell
git checkout -b feature/add-help
```

`checkout -b` means create a branch and switch to it.

Newer Git also supports:

```shell
git switch -c feature/add-help
```

I teach `checkout -b` because many projects still show it in older notes, blog posts, and workshop material. I also mention `switch -c` so learners recognize it later.

Check the current branch:

```shell
git branch
```

The current branch has `*` next to it.

## Change a File on the Branch

Append a line:

```shell
>> README.md echo Run make help to see commands
```

Stage and commit:

```shell
git add README.md
git commit -m "Add help note"
```

The new commit belongs to `feature/add-help`, not `main`, because that is the branch currently checked out.

## Compare Branches

Run:

```shell
git diff main..feature/add-help
```

For this form of `git diff`, Git compares the file tree at the tip of `main` with the file tree at the tip of `feature/add-help`.

In the output:

- lines beginning with `-` exist in the first side and not the second side
- lines beginning with `+` exist in the second side and not the first side
- lines with no marker are context lines that help you see where the change happened

For a compact commit list:

```shell
git log --oneline main..feature/add-help
```

That asks for commits reachable from `feature/add-help` that are not reachable from `main`.

## Merge Back to Main

Switch to `main`:

```shell
git checkout main
```

Merge the feature branch:

```shell
git merge feature/add-help
```

If `main` has not moved since the feature branch was created, Git can do a fast-forward merge. That means Git only moves the `main` branch name forward to the feature commit.

If both branches have new commits, Git may create a merge commit. A merge commit has more than one parent, so it records the join point in history.

## Inspect the Result

Run:

```shell
git status
git log --oneline --graph --decorate
type README.md
```

I want learners to see three things:

- the working tree is clean
- the graph shows where the branch work went
- the file content now includes the merged line

## Clean Up the Branch Name

After the merge, the branch name can be deleted if it is no longer needed:

```shell
git branch --merged
git branch -d feature/add-help
```

`-d` refuses to delete a branch if Git thinks it has unmerged work. That makes it safer than `-D`.

## What Learners Should Remember

- A branch is a name that points to a commit.
- `HEAD` tells Git which branch is active.
- New commits move the active branch forward.
- `git diff main..branch-name` compares file content between two branch tips.
- A fast-forward merge moves a branch pointer.
- A merge commit records a join between lines of work.
