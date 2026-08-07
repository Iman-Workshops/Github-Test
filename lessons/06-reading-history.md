# 06. Reading History

## Goal

This lesson teaches learners how to inspect what changed, when it changed, and who authored each line. These commands turn Git history into a tool for understanding the project.

## Start With Status

Before reading history, check the current state:

```shell
git status
```

If the working tree is clean, history commands are easier to read because there are no local edits mixed into the picture.

## See Recent Commits

Run:

```shell
git log --oneline
```

This shows each commit as:

```text
short-hash Commit message
```

Use it when you need a quick list.

## See the Shape of Branches

Run:

```shell
git log --oneline --graph --decorate --all
```

The flags mean:

- `--oneline` keeps each commit short.
- `--graph` draws branch and merge shape with text characters.
- `--decorate` shows branch and tag names.
- `--all` includes all local branches and remote-tracking branches.

This is the command I use when learners ask, "Where did my branch go?"

## See One Commit

Copy a short hash from the log, then run:

```shell
git show d7fd425
```

Replace `d7fd425` with a real hash from your repo.

`git show` displays:

- the full commit hash
- the author
- the date
- the commit message
- the file changes recorded by that commit

Use `git show --stat` for a shorter file summary:

```shell
git show --stat d7fd425
```

## See Uncommitted Changes

Before staging:

```shell
git diff
```

After staging:

```shell
git diff --staged
```

This distinction matters. `git diff` shows unstaged changes. `git diff --staged` shows what is ready for the next commit.

## Read Diff Output

A diff often begins with lines like:

```text
diff --git a/README.md b/README.md
index 1234567..89abcde 100644
--- a/README.md
+++ b/README.md
@@ -1,3 +1,4 @@
```

For a beginner workshop, I focus on these parts:

- `a/README.md` is the old side.
- `b/README.md` is the new side.
- lines with `-` were removed from the old side.
- lines with `+` were added to the new side.
- lines with no marker are context.

The `@@` line shows the nearby line numbers. It is helpful, but learners do not need to master it on day one.

## See Who Last Changed Each Line

Run:

```shell
git blame README.md
```

The name is harsh, but the command is useful. It shows the latest commit that touched each line.

I explain it as "line history," not as a way to accuse someone.

Use it when:

- you need to know when a line appeared
- you want the commit that explains a line
- you are about to edit code and want context

After finding a commit hash in blame, inspect it:

```shell
git show <hash>
```

## Compare Two Branch Tips

Run:

```shell
git diff main..feature/add-help
```

This compares the file tree at `main` with the file tree at `feature/add-help`.

Run:

```shell
git log --oneline main..feature/add-help
```

This shows commits reachable from `feature/add-help` that are not reachable from `main`.

The same two-dot syntax can appear in both commands, but each command asks a different kind of question. `diff` compares file content. `log` compares commit reachability.

## What Learners Should Remember

- `git log --oneline` shows a compact commit list.
- `git log --graph --decorate --all` shows branch shape.
- `git show <hash>` opens one commit.
- `git diff` shows unstaged edits.
- `git diff --staged` shows staged edits.
- `git blame <file>` shows the latest commit for each line.
- The same syntax can mean slightly different things depending on the command.
