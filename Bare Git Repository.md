---
title : Bare Git Repository
notetype : feed
date : 18-12-2021
---

A bare [[Git]] repository is a repository without a working tree. If you create a bare repository, you'll get just the contents that you'd normally find within `.git` directory.

Since it doesn't have a working tree, the bare repository does not hold your files directly as you'd expect from a normal repository. If you add a file like `main.go` to a non-bare repo, the file will exist within the repository itself and will be visible to you like you'd expect.

In case of a bare git repository, git only keeps track of it's internal git object representation of your `main.go` file, not the actual file. 

For example, when Github hosts your repository, it hosts it as a bare repo, and uses git object data to show you the files in the browser (even though the real files don't exist in that form on their servers). Once you do a git clone of this (bare) repo from github, git translates it into a non-bare repo and "materializes" the actual files on your machine. 

-----

Status: #💡 

