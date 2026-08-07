# Facilitator Guide

I use this guide when I teach the workshop live. It keeps the session practical and helps me notice when learners need a slower explanation.

## Teaching Goal

The goal is not to make everyone memorize every command. The goal is to help learners understand the loop:

```text
change files
check status
stage the right changes
commit with a clear message
share through GitHub when needed
```

Once that loop feels normal, branches, merges, conflicts, and remotes become much easier.

## Room Setup

Before the session, ask learners to install:

- Git for Windows
- a text editor
- a GitHub account

Ask them to check:

```shell
git --version
```

If Git is missing, fix that before teaching commands. A beginner who starts with broken setup will often think they are the problem.

## Session Plan

| Time | Topic | What I watch for |
| --- | --- | --- |
| 0 to 10 minutes | What the terminal is | Learners know commands are programs. |
| 10 to 25 minutes | Files and folders | Learners can create, read, and edit files. |
| 25 to 50 minutes | `git init`, `status`, `add`, `commit` | Learners can explain staging in plain words. |
| 50 to 70 minutes | `log`, `diff`, `show` | Learners can read what changed. |
| 70 to 100 minutes | Branch and merge | Learners understand branch names as pointers. |
| 100 to 125 minutes | Conflict practice | Learners can remove markers and commit the result. |
| 125 to 150 minutes | GitHub remote | Learners can push, edit remotely, and pull. |

## How I Explain Core Ideas

### Terminal

The terminal runs commands. If a command is unknown, the shell says it cannot find it.

I ask:

```text
Did the command fail because Git failed, or because the shell could not find any program with that name?
```

That question helps learners separate shell problems from Git problems.

### Repository

A Git repository is a folder with a `.git` database inside it.

The visible project files are the working tree. The hidden `.git` folder stores history.

### Staging

The staging area is the set of file versions that will be recorded in the next commit.

My favorite explanation:

```text
git add chooses what goes into the photo.
git commit takes the photo.
```

### Commit

A commit is a named point in history. It has an author, date, message, parent commit, and file snapshot.

I ask learners to write messages that answer:

```text
What did this commit do?
```

### Branch

A branch is a name pointing to a commit. It is not a copy of the project folder.

When the active branch gets a new commit, that branch name moves.

### Merge

A merge brings one line of work into another. If the target branch has not moved, Git can fast-forward. If both branches moved, Git may create a merge commit or stop for a conflict.

### Conflict

A conflict means Git needs a human choice. It does not mean the repo is ruined.

I slow down here and ask learners to identify:

- current branch side
- incoming branch side
- final text they actually want

## Common Instructor Moves

- Ask learners to read `git status` out loud.
- Draw branch pointers with commit letters on a board.
- Make one mistake on purpose, such as typing a fake command.
- Show that a typo in a filename creates a different file.
- Pause before each commit and ask what should be included.
- Use `git diff --staged` before committing.

## Common Learner Mistakes

`git command not found`

Git is not installed or is not in `PATH`. Reopen the terminal after installing Git.

`remote origin already exists`

The repo already has a remote called `origin`. Run `git remote -v`, then keep it or change the URL.

Committed conflict markers

Open the file, remove marker lines, commit a real fix. Use `git show` to explain what happened.

Changed the wrong branch

Use `git branch`, `git log --oneline --graph --decorate --all`, and `git status` to rebuild the picture.

Pushed to the wrong repo

Run `git remote -v` and fix the URL with `git remote set-url origin <url>`.

## Closing Prompt

At the end, I ask learners to explain this sentence in their own words:

```text
Git tracks snapshots of files, GitHub stores a shared copy, and branches are names that move through history.
```

If they can explain that, they have the foundation they need for real project work.
