# 04. Conflict Resolution

## Goal

This lesson teaches learners how to create a conflict on purpose, read the conflict markers, resolve the file by hand, and finish the merge.

A conflict is not a broken repository. It is Git pausing because two lines of work changed the same place in different ways.

## When Conflicts Happen

Git usually merges changes by itself when they touch different lines or different files.

A conflict can happen when two branches change the same line differently.

Example:

- `main` says `TEAM NOTE: use Python 3.12`
- `feature/python-note` says `TEAM NOTE: use Python 3.13`

Git cannot know which one the team wants. A person must decide.

## Build the Conflict

Start clean:

```shell
git status
```

Create a note:

```shell
> notes.txt echo TEAM NOTE: use Python 3.11
git add notes.txt
git commit -m "Add Python team note"
```

Create and switch to a branch:

```shell
git checkout -b feature/python-note
```

Change the note on the feature branch:

```shell
> notes.txt echo TEAM NOTE: use Python 3.13
git add notes.txt
git commit -m "Use Python 3.13 in note"
```

Switch back to `main`:

```shell
git checkout main
```

Change the same line differently:

```shell
> notes.txt echo TEAM NOTE: use Python 3.12
git add notes.txt
git commit -m "Use Python 3.12 in note"
```

Now merge the feature branch:

```shell
git merge feature/python-note
```

Git should stop and report a conflict in `notes.txt`.

## Read the Markers

Open the file:

```shell
type notes.txt
```

It will look similar to this:

```text
<<<<<<< HEAD
TEAM NOTE: use Python 3.12
=======
TEAM NOTE: use Python 3.13
>>>>>>> feature/python-note
```

The parts mean:

- `<<<<<<< HEAD` starts the current branch version.
- `=======` separates the two versions.
- `>>>>>>> feature/python-note` ends the incoming branch version.

In this example, `HEAD` is `main` because `main` was checked out when the merge started. The incoming side is `feature/python-note` because that is the branch being merged in.

## Resolve the File

Edit the file:

```shell
notepad notes.txt
```

Choose the final text and remove every marker line. For example:

```text
TEAM NOTE: use Python 3.13
```

Save the file.

Check status:

```shell
git status
```

Git should say the file is unmerged or needs resolution.

Stage the resolved file:

```shell
git add notes.txt
```

Finish the merge:

```shell
git commit -m "Resolve Python note conflict"
```

In many Git versions, the commit message editor opens automatically if you run `git commit` without `-m`. During the workshop, I use `-m` to keep the focus on the conflict itself.

## If You Need to Stop

Before finishing the merge, you can cancel it:

```shell
git merge --abort
```

This returns the working tree to the state before the merge attempt, as long as Git can do so cleanly.

## What Not to Do

- Do not commit conflict marker lines.
- Do not delete both versions without deciding what the final file should say.
- Do not panic when `git status` shows unmerged paths.
- Do not use `git add` until the file contains the final text.

## What Learners Should Remember

- A conflict is a request for a human decision.
- `HEAD` is the branch currently checked out.
- The other marker names the branch or commit being merged.
- Resolve by editing the file into its final state.
- `git add` tells Git the conflict is resolved.
- A commit finishes a normal merge conflict.
