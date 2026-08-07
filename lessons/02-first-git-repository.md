# 02. First Git Repository

## Goal

This lesson turns a normal folder into a Git repository and records the first real snapshot. I want learners to understand what Git is doing before they learn more commands.

## Start Inside the Project Folder

From the practice folder created in the first lesson:

```shell
cd git-playground
```

Check the files:

```shell
dir
type README.md
type todo.txt
```

At this point, the folder has files, but Git is not tracking them yet.

## Initialize Git

Run:

```shell
git init
```

`init` means initialize. Git creates a hidden folder named `.git`.

That `.git` folder is the repository database. It stores commits, branch pointers, staging data, and other Git metadata. If `.git` is deleted, the files may remain, but the Git history is gone from that folder.

## Check Status

Run:

```shell
git status
```

The first useful idea is `untracked files`.

An untracked file is a file Git can see, but Git has not been told to include it in any commit yet.

I tell learners to run `git status` often:

- before staging
- after staging
- after committing
- before switching branches
- before pushing

`git status` is the safest way to ask Git, "What do you think is happening right now?"

## Set Commit Identity

Git records an author name and email address on each commit.

For one repository only:

```shell
git config user.name "ImanM02"
git config user.email "you@example.com"
```

For all repositories on the same machine:

```shell
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

Use the local version during a workshop if learners are sharing a classroom machine. Use the global version on a personal machine.

Check the values:

```shell
git config user.name
git config user.email
```

## Stage Files

Run:

```shell
git add README.md todo.txt
```

`git add` does not create a commit. It copies the current version of each named file into the staging area.

The staging area is the list of file versions that will go into the next commit.

Check it:

```shell
git status
```

The files should now appear under `Changes to be committed`.

## Commit the Snapshot

Run:

```shell
git commit -m "Initialize project files"
```

`commit` records a snapshot from the staging area into history.

The message after `-m` should explain what changed. I prefer messages that sound like an action:

```text
Initialize project files
Add help note
Fix todo text
```

Avoid vague messages:

```text
stuff
changes
final final
```

## Read the History

Run:

```shell
git log --oneline
```

`log` shows commits. `--oneline` makes each commit fit on one line by showing a short hash and the message.

Example:

```text
7ca1625 Initialize project files
```

The hash is the commit identifier. Learners do not need to memorize it. They only need to know that Git uses it to point to a specific commit.

## Change, Stage, Commit Again

Append a line:

```shell
>> README.md echo Run make help to see commands
```

Now check:

```shell
git status
```

Because `README.md` was already committed once, Git describes it as modified instead of untracked.

Stage and commit:

```shell
git add README.md
git commit -m "Add help note"
```

Now inspect the short history:

```shell
git log --oneline
```

The newest commit appears at the top.

## What Learners Should Remember

- `git init` starts tracking history in a folder.
- `.git` is where the history lives.
- `git status` explains the current state.
- `git add` prepares file versions for the next commit.
- `git commit` records the staged versions.
- `git log --oneline` shows the commit list in a compact form.
