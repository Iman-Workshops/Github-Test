# Lab 01. Local Git From Zero

## Outcome

You will create a folder, add files, initialize Git, make two commits, and inspect the history.

## 1. Create the Folder

```shell
mkdir git-workshop-lab
cd git-workshop-lab
```

Check your location:

```shell
cd
```

## 2. Create Starter Files

```shell
> README.md echo # Todo App
> todo.txt echo - [ ] Learn the command line
> notes.txt echo TEAM NOTE: use Python 3.11
```

Check the files:

```shell
dir
type README.md
type todo.txt
type notes.txt
```

## 3. Initialize Git

```shell
git init
git branch -M main
```

Check the state:

```shell
git status
```

Expected idea: Git sees untracked files.

## 4. Set Identity for This Repo

```shell
git config user.name "Your Name"
git config user.email "you@example.com"
```

Check:

```shell
git config user.name
git config user.email
```

## 5. Stage and Commit

```shell
git add README.md todo.txt notes.txt
git status
git commit -m "Initialize workshop files"
```

Check history:

```shell
git log --oneline
```

## 6. Make a Second Change

Append to `README.md`:

```shell
>> README.md echo Run make help to see commands
```

Inspect the unstaged change:

```shell
git diff
```

Stage it:

```shell
git add README.md
```

Inspect the staged change:

```shell
git diff --staged
```

Commit:

```shell
git commit -m "Add help note"
```

## 7. Check Your Work

```shell
git status
git log --oneline
```

Expected result:

- the working tree is clean
- there are at least two commits
- the newest commit is at the top

## Reflection

Answer these in your own words:

- What did `git add` do?
- What did `git commit` do?
- Why did `git diff` show output before staging?
- Why did `git diff --staged` show output after staging?
