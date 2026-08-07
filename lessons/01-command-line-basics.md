# 01. Command Line Basics

## Goal

Before I teach Git, I want learners to feel safe in the terminal. Git commands are just programs we run from a shell, so the first lesson is about how the shell reads text and how the operating system answers.

## The Mental Model

When you type a command and press Enter, the shell does a few things:

1. It reads the command name.
2. It reads the extra words after the command name as arguments.
3. It checks whether the command is built into the shell.
4. If not, it searches folders listed in the `PATH` environment variable.
5. If it finds a program, it runs it.
6. If it does not find a program, it prints an error.

That is why this command fails:

```text
HiToAll
```

In Windows Command Prompt, the error usually looks like this:

```text
'HiToAll' is not recognized as an internal or external command,
operable program or batch file.
```

The lesson here is important: the terminal is not magic. It only runs commands it knows how to find.

## Folders

Create a practice folder:

```shell
mkdir git-playground
```

`mkdir` means make directory. A directory is a folder.

Move into it:

```shell
cd git-playground
```

`cd` means change directory. I explain it as "put the terminal inside this folder."

Check where you are:

```shell
cd
```

In Windows Command Prompt, `cd` with no path prints the current folder.

## Listing Files

In Windows Command Prompt:

```shell
dir
```

In PowerShell, `dir` also works, but it is an alias for another command:

```shell
Get-ChildItem
```

For this workshop, `dir` is enough.

## Creating Files With Text

In Command Prompt, quotes are written into the file if you put them inside `echo`. To avoid that, I use this form:

```shell
> README.md echo # Todo App
> todo.txt echo - [ ] Learn CLI
```

The `>` symbol writes output into a file. If the file already exists, it replaces the old content.

Use `>>` to append to the end of a file:

```shell
>> README.md echo Run make help to see commands
```

That line adds new text without deleting the first line.

## Reading Files

In Command Prompt:

```shell
type README.md
type todo.txt
```

`type` prints file content.

In PowerShell, this also works:

```shell
Get-Content README.md
```

## Editing Files

Open a file in Notepad:

```shell
notepad README.md
```

If the file does not exist, Notepad asks whether it should create it. That is useful for beginners because they can still edit text in a familiar window.

## Redirection Rules

I repeat these rules several times:

- `>` replaces the file content.
- `>>` appends to the file.
- In Command Prompt, quoted text passed to `echo` keeps the quote marks.
- In PowerShell, quotes group the string and are not written by default.

## Practice Loop

Run this from an empty practice folder:

```shell
mkdir git-playground
cd git-playground
> README.md echo # Todo App
> todo.txt echo - [ ] Learn CLI
dir
type README.md
type todo.txt
notepad todo.txt
```

The learner should be able to answer:

- What folder am I in?
- What files exist here?
- What is inside each file?
- Did I replace a file or append to it?

Those questions become the base for `git status` in the next lesson.
