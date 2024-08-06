# Introduction

- The *command line* is a text interface for the computer’s operating system. To access the command line, we use the terminal.
- A *filesystem* organizes a computer’s files and directories into a tree structure. It starts with the *root directory*. Each parent directory can contain more child directories and files.
- From the command line, you can navigate through files and folders on your computer:
    - `pwd` outputs the name of the current working directory.
    - `ls` lists all files and directories in the working directory.
    - `cd` switches you into the directory you specify.
    - `mkdir` creates a new directory in the working directory.
    - `touch` creates a new file inside the working directory.

---

The command line is a powerful tool used by developers to find, create, and manipulate files and folders. This short tutorial will walk you through the steps for setting up the command line application on your computer.

Command Line Interfaces (CLIs) come in many forms.

A common CLI is Bash.

## **What is Bash?**

**Bash**, or the __B__ourne-__A__gain __SH__ell, is a CLI that was created in 1989 by Brian Fox as a free software replacement for the Bourne Shell.

A **shell** is a specific kind of CLI.

Bash is “open source,” which means that anyone can read the code and suggest changes.

Since its beginning, it has been supported by a large community of engineers who have worked to make it an incredible tool.

Bash is the default shell for Linux and Mac up through macOS 10.14 (Mojave).

For these reasons, Bash is the most used and widely distributed shell.

---

### Summary

- Options modify the behavior of commands:
    - `ls -a` lists all contents of a directory, including hidden files and directories
    - `ls -l` lists all contents in long format
    - `ls -t` orders files and directories by the time they were last modified
    - Multiple options can be used together, like `ls -alt`
- From the command line, you can also copy, move, and remove files and directories:
    - `cp` copies files
    - `mv` moves and renames files
    - `rm` removes files
    - `rm -r` removes directories
- Wildcards are useful for selecting groups of files and directories (see *)