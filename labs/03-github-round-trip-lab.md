# Lab 03. GitHub Round Trip

## Outcome

You will connect the local repo to GitHub, push it, make a remote edit, pull that edit, and inspect the history.

Start from the repository created in Lab 02.

## 1. Create an Empty GitHub Repo

On GitHub, create a new empty repository.

Do not add a README from GitHub if your local repo already has one. The local repo is the source for the first push.

Copy the repository URL. It will look like this:

```text
https://github.com/OWNER/REPO.git
```

## 2. Add the Remote

Replace the example URL with your real repo URL:

```shell
git remote add origin https://github.com/OWNER/REPO.git
git remote -v
```

If `origin` already exists, check it:

```shell
git remote -v
```

If it points to the wrong repo, change it:

```shell
git remote set-url origin https://github.com/OWNER/REPO.git
```

## 3. Push Main

```shell
git branch -M main
git push -u origin main
```

After this, refresh GitHub in the browser. You should see your files.

## 4. Make a Remote Edit

On GitHub:

1. Open `README.md`.
2. Edit the file.
3. Add one line, such as `Edited once from GitHub`.
4. Commit the change.

## 5. Pull the Remote Change

Back in the terminal:

```shell
git pull
```

If Git opens an editor for a merge commit message, save and close it. If Git reports a conflict, use the conflict steps from Lab 02.

## 6. Inspect History

```shell
git log --oneline --graph --decorate
type README.md
```

Expected result:

- the GitHub edit appears in `README.md`
- the history includes the remote commit
- local `main` and `origin/main` point to the same recent history after the pull

## 7. Push One More Local Change

Append a local line:

```shell
>> todo.txt echo - [ ] Practice git pull
git add todo.txt
git commit -m "Add pull practice item"
git push
```

Refresh GitHub. The pushed commit should appear there.

## Reflection

Answer these in your own words:

- What did `origin` point to?
- What did `-u` set during the first push?
- What did `git pull` bring into your local repo?
- Why can GitHub and your local repo have different commits for a while?
