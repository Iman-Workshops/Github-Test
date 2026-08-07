# Lab 02. Branch, Merge, and Conflict

## Outcome

You will create a feature branch, merge it back into `main`, then create and resolve a text conflict.

Start from the repository created in Lab 01.

## 1. Create a Feature Branch

```shell
git status
git checkout -b feature/add-help
```

Confirm the current branch:

```shell
git branch
```

## 2. Change README on the Branch

```shell
>> README.md echo Use git status before each commit
git add README.md
git commit -m "Add status reminder"
```

Compare the branch with `main`:

```shell
git diff main..feature/add-help
git log --oneline main..feature/add-help
```

## 3. Merge the Feature Branch

```shell
git checkout main
git merge feature/add-help
```

Check the result:

```shell
git status
git log --oneline --graph --decorate
type README.md
```

Expected idea: if `main` did not move while the branch existed, Git can fast-forward.

## 4. Create a Conflict on Purpose

Create a new branch:

```shell
git checkout -b feature/python-313
```

Change the team note:

```shell
> notes.txt echo TEAM NOTE: use Python 3.13
git add notes.txt
git commit -m "Use Python 3.13 in note"
```

Return to `main`:

```shell
git checkout main
```

Change the same line differently:

```shell
> notes.txt echo TEAM NOTE: use Python 3.12
git add notes.txt
git commit -m "Use Python 3.12 in note"
```

Now merge:

```shell
git merge feature/python-313
```

Git should report a conflict.

## 5. Resolve the Conflict

Inspect the file:

```shell
type notes.txt
```

You should see markers like:

```text
<<<<<<< HEAD
TEAM NOTE: use Python 3.12
=======
TEAM NOTE: use Python 3.13
>>>>>>> feature/python-313
```

Open the file:

```shell
notepad notes.txt
```

Choose the final line:

```text
TEAM NOTE: use Python 3.13
```

Remove the marker lines, save, and return to the terminal.

Finish:

```shell
git add notes.txt
git commit -m "Resolve Python note conflict"
```

## 6. Check Your Work

```shell
git status
git log --oneline --graph --decorate
type notes.txt
```

Expected result:

- the working tree is clean
- `notes.txt` contains no conflict markers
- the history shows the conflict resolution commit

## Reflection

Answer these in your own words:

- Which side was `HEAD`?
- Which side was incoming?
- Why did Git need a human decision?
- What did `git add notes.txt` mean after the edit?
