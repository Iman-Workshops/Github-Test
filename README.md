# Git, GitHub, and the Command Line Workshop

I wrote this workshop after teaching a first session on Git, GitHub, and the Windows command line. My goal is to help learners build a real mental model for everyday project work, not memorize a random list of commands.

By the end, learners should be able to:

- move through folders from the terminal
- create and inspect files
- start a Git repository
- stage and commit changes
- read project history
- create a branch
- merge a branch
- resolve a text conflict
- connect a local repository to GitHub
- pull and push with confidence

This version uses `main` as the branch name. Some older notes and older Git repositories use `master`. If your repository uses `master`, replace `main` with `master` in the commands.

## How I Teach It

The workshop is built around one small project: a todo app folder with a README, a todo list, and a team note. The files stay simple so learners can focus on what Git is tracking and why each command matters.

I teach the commands in this order:

| Step | Topic | Main idea |
| --- | --- | --- |
| 1 | Command line basics | The terminal runs programs and reports errors when a program cannot be found. |
| 2 | Folders and files | `mkdir`, `cd`, `dir`, `type`, `echo`, and `notepad` are enough for the first practice loop. |
| 3 | First Git repository | `git init` creates `.git`, the hidden database where Git stores history. |
| 4 | Identity | `git config user.name` and `git config user.email` tell Git who authored a commit. |
| 5 | Staging and commits | `git add` prepares a change, and `git commit` records it. |
| 6 | History | `git log`, `git show`, and `git blame` answer different history questions. |
| 7 | Branches | A branch lets you work on a change without moving the main line yet. |
| 8 | Merge | A merge brings branch work back together. |
| 9 | Conflicts | Git asks for a human decision when two branches change the same line differently. |
| 10 | GitHub remote | `git remote`, `git push`, and `git pull` connect the local repo to GitHub. |

## Repo Map

- `lessons/` contains the teaching notes in the order I would present them.
- `labs/` contains hands-on exercises for learners.
- `reference/` contains command notes for quick review after the workshop.
- `examples/workshop-state/` contains small files from the original workshop practice.

## Suggested Session Flow

1. Start with the command line, because Git is much less scary when the terminal feels normal.
2. Create a fresh folder and initialize Git inside it.
3. Make the first commit with a README and a todo file.
4. Create a feature branch, edit a file, commit, and merge it back.
5. Build a conflict on purpose, resolve it, and explain each conflict marker.
6. Connect to GitHub and push the final state.
7. Pull a remote change and inspect the history with graph commands.

## Ground Rules I Emphasize

- Run `git status` before and after important steps.
- Commit small, meaningful changes.
- Write commit messages in the present tense, like `Add help text`.
- Do not commit credentials or private local files.
- Read conflict markers carefully before deleting them.
- Pull before pushing when a shared branch may have changed.

## Before You Teach

Install Git, open a terminal, and confirm these commands work:

```shell
git --version
git config --global user.name
git config --global user.email
```

If the name or email commands return nothing, set them:

```shell
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

For the workshop itself, use a local folder you can delete later. The point is to practice without fear.
