# Command Reference

This reference is for review after the workshop. I grouped the commands by the moment where learners usually need them.

## Terminal Basics

| Command | Meaning | Use it when |
| --- | --- | --- |
| `HiToAll` | Example of an invalid command | You want to show how the shell reports an unknown program. |
| `mkdir git-playground` | Make a directory | You need a new folder for practice or a project. |
| `cd git-playground` | Change directory | You want the terminal to work inside another folder. |
| `cd` | Print current folder in Command Prompt | You want to check your location. |
| `dir` | List files and folders | You want to see what exists in the current folder. |
| `type README.md` | Print file content | You want to read a file in the terminal. |
| `notepad README.md` | Open a file in Notepad | You want to edit a text file from the terminal. |

## Writing Text From Command Prompt

| Command | Meaning |
| --- | --- |
| `> README.md echo # Todo App` | Write one line into `README.md`, replacing old content. |
| `>> README.md echo New line` | Append one line to the end of `README.md`. |

Remember:

- `>` replaces file content.
- `>>` appends file content.
- In Command Prompt, quotes passed to `echo` are written into the file.
- In PowerShell, quotes group strings and are not written by default.

## Starting Git

| Command | Meaning | Use it when |
| --- | --- | --- |
| `git init` | Create a Git repository in the current folder | You want Git to start tracking history. |
| `git branch -M main` | Rename current branch to `main` | You want branch naming to match modern GitHub defaults. |
| `git status` | Show current Git state | You want to know what changed, what is staged, and what is untracked. |

## Identity

| Command | Meaning |
| --- | --- |
| `git config user.name "Your Name"` | Set author name for this repo. |
| `git config user.email "you@example.com"` | Set author email for this repo. |
| `git config --global user.name "Your Name"` | Set author name for all repos on this machine. |
| `git config --global user.email "you@example.com"` | Set author email for all repos on this machine. |

Use local config for shared workshop machines. Use global config for a personal machine.

## Staging and Committing

| Command | Meaning | Use it when |
| --- | --- | --- |
| `git add README.md` | Stage one file | You want that file version in the next commit. |
| `git add README.md todo.txt` | Stage selected files | You want to commit a specific set of files. |
| `git commit -m "Add help note"` | Create a commit | You want to record staged changes in history. |
| `git diff` | Show unstaged changes | You edited files and want to inspect them before staging. |
| `git diff --staged` | Show staged changes | You want to inspect what will go into the next commit. |

Short rule:

```text
git add prepares the snapshot.
git commit records the snapshot.
```

## History

| Command | Meaning | Use it when |
| --- | --- | --- |
| `git log --oneline` | Show compact commit history | You want a quick commit list. |
| `git log --oneline --graph --decorate --all` | Show branch shape | You want to understand how branches relate. |
| `git show <hash>` | Show one commit | You want the details for a specific commit. |
| `git show --stat <hash>` | Show a shorter commit summary | You want file names and change counts. |
| `git blame README.md` | Show the latest commit for each line | You want line history for a file. |

## Branches

| Command | Meaning | Use it when |
| --- | --- | --- |
| `git branch` | List local branches | You want to see the active branch. |
| `git checkout -b feature/add-help` | Create and switch to a new branch | You want to work away from `main`. |
| `git switch -c feature/add-help` | Newer form for create and switch | You prefer the newer branch command. |
| `git checkout main` | Switch to `main` | You want to return to the main line. |
| `git branch --merged` | List branches merged into the current branch | You want to know what is safe to clean up. |
| `git branch -d feature/add-help` | Delete a merged local branch | You no longer need that branch name. |

## Comparing Branches

| Command | Meaning |
| --- | --- |
| `git diff main..feature/add-help` | Compare file content between branch tips. |
| `git log --oneline main..feature/add-help` | Show commits on the feature branch that are not on `main`. |

`diff` asks about files. `log` asks about commits.

## Merging

| Command | Meaning |
| --- | --- |
| `git merge feature/add-help` | Merge the named branch into the current branch. |
| `git merge --abort` | Stop an unfinished merge and return to the pre-merge state when Git can do it cleanly. |

Run `git status` after a merge. It tells you whether the merge is done or needs a conflict fix.

## Conflict Markers

```text
<<<<<<< HEAD
current branch text
=======
incoming branch text
>>>>>>> branch-name
```

Resolve by editing the file into the final text, removing all marker lines, then running:

```shell
git add conflicted-file.txt
git commit -m "Resolve text conflict"
```

## Remotes and GitHub

| Command | Meaning | Use it when |
| --- | --- | --- |
| `git remote -v` | Show remote names and URLs | You want to confirm where Git will fetch and push. |
| `git remote add origin <url>` | Add a remote named `origin` | You are connecting a local repo to GitHub for the first time. |
| `git remote set-url origin <url>` | Change the URL for `origin` | The remote points to the wrong repo. |
| `git push -u origin main` | Push `main` and set upstream tracking | You are pushing a branch to GitHub for the first time. |
| `git push` | Push commits to the tracked remote branch | Upstream tracking is already set. |
| `git fetch` | Update remote-tracking branches | You want remote data without merging yet. |
| `git pull` | Fetch and integrate remote commits | You want to bring remote work into the current branch. |

## Quick Debug Order

When something feels wrong, run these first:

```shell
git status
git branch
git remote -v
git log --oneline --graph --decorate --all
```

Those four commands usually show where you are, what changed, which remote is connected, and how the history is shaped.
