# 05. GitHub Remotes

## Goal

This lesson connects the local repository to GitHub, pushes commits, pulls remote changes, and explains the names Git uses for local and remote state.

## Local Repo and Remote Repo

A local repository is the Git repository on your machine.

A remote repository is another copy of the repository somewhere else, often on GitHub.

`origin` is only a short name for a remote URL. It is not a special server by itself. Git uses `origin` by convention because it is the default name created by `git clone`.

## Check Remotes

Run:

```shell
git remote -v
```

If no remote is configured, the command prints nothing.

Add GitHub as the remote:

```shell
git remote add origin https://github.com/Iman-Workshops/Github-Test.git
```

Check again:

```shell
git remote -v
```

You should see one fetch URL and one push URL.

If `origin` already exists and points to the wrong place, change it:

```shell
git remote set-url origin https://github.com/Iman-Workshops/Github-Test.git
```

## Use Main as the Branch Name

Set the current branch name to `main`:

```shell
git branch -M main
```

`-M` renames the branch even if a branch with the target name already exists locally. Use it carefully. In a workshop repo with one branch, it is a simple way to align with GitHub's common default branch name.

## Push the First Time

Run:

```shell
git push -u origin main
```

`push` sends local commits to the remote.

`-u` sets upstream tracking. After that, Git knows that local `main` is connected to `origin/main`, so later you can run:

```shell
git push
git pull
```

without typing the remote and branch every time.

## What Is origin/main?

`origin/main` is a remote-tracking branch.

It is your local record of where Git last saw the remote `main` branch. It updates when you run commands such as:

```shell
git fetch
git pull
git push
```

It is not a live connection. If someone pushed to GitHub five seconds ago, your local `origin/main` may not know until you fetch or pull.

## Pull Remote Changes

Run:

```shell
git pull
```

In the common default setup, `git pull` does two steps:

1. `git fetch`
2. `git merge`

Some machines are configured so `git pull` rebases instead of merging. You can see the current setting with:

```shell
git config pull.rebase
```

During this beginner workshop, I explain pull as "get the remote commits, then integrate them into my current branch."

## Practice a GitHub Round Trip

1. Push your local repository to GitHub.
2. Open the repository on GitHub.
3. Edit `README.md` from the GitHub web interface.
4. Commit that change on GitHub.
5. Return to the terminal.
6. Run `git pull`.
7. Run `git log --oneline --graph --decorate`.

This shows learners that local and remote history can move independently, then Git can bring them back together.

## Common Messages

`remote origin already exists`

This means the name `origin` is already used. Check it with:

```shell
git remote -v
```

Then decide whether to keep it or change it with `git remote set-url`.

`Updates were rejected`

This often means the remote branch has commits your local branch does not have yet. Start with:

```shell
git pull
```

Resolve any conflict if Git reports one, then push again.

`fatal: The current branch main has no upstream branch`

This means Git does not know which remote branch your local branch should push to by default. Fix it with:

```shell
git push -u origin main
```

## What Learners Should Remember

- `origin` is a remote nickname.
- `git remote -v` shows remote URLs.
- `git push -u origin main` sends commits and sets tracking.
- `origin/main` is a local record of the remote branch.
- `git fetch` updates remote-tracking branches.
- `git pull` fetches and integrates remote commits.
- A rejected push usually means you need to bring remote work into your local branch first.
