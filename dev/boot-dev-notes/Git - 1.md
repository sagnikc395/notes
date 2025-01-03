---
title: Git Fundamentals
tags:
  - boot-dev
  - git
  - basic-programming
date: 3/1/25
---
### Git:
- [Git](https://git-scm.com/) is _the_ distributed [version control system](https://git-scm.com/book/en/v2/Getting-Started-About-Version-Control) (VCS). Nearly every developer in the world uses it to manage their code. It has quite a monopoly on VCS. Developers use Git to:
	- Keep a history of their code changes
	- Revert mistakes made in their code
	- Collaborate with other developers
	- Make backups of their code
	- And much more
- First, check and see if you already have Git installed. Open a terminal and type:

```bash
git --version
```
### Porcelain and Plumbing:
- In Git, commands are divided into high-level ("porcelain") commands and low-level ("plumbing") commands. The porcelain commands are the ones that you will use most often as a developer to interact with your code. Some porcelain commands are:
	- `git status`
	- `git add`
	- `git commit`
	- `git push`
	- `git pull`
	- `git log`
- Don't worry about what they do yet, we'll cover them in detail soon. Some examples of plumbing commands are:
	- `git apply`
	- `git commit-tree`
	- `git hash-object`
### git config:
- Whenever code changes, Git tracks _who_ made the change. To ensure you get proper credit (or more likely, blame) for all the code you write, you need to set your name and email.
- Git comes with a [configuration](https://git-scm.com/docs/git-config) both at the global and the repo (project) level. Most of the time, you'll just use the global config.
```bash 
git config --global user.name
```
```bash 
git config --global user.email 
```
- Finally, let's set a default branch (we'll talk more about configs and branches later) so that we're all on the same page. Run:
```bash
git config --global init.defaultBranch master
```
- Your `~/.gitconfig` file is the file that stores your global Git configuration. View it:
```bash
cat ~/.gitconfig
```

### Repositories:
- A Git "repository" (or "repo") represents a single project. You'll typically have one repository for each project you work on.
- A repo is essentially just a directory that contains a project (other directories and files). The only difference is that it _also_ contains a hidden `.git` directory. That [hidden directory](https://en.wikipedia.org/wiki/Hidden_file_and_hidden_directory) is where Git stores all of its internal tracking and versioning information for the project.
### Status:
- A file can be in one of [several states](https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository#_the_very_basics) in a Git repository. Here are a few important ones:
	- `untracked`: Not being tracked by Git
	- `staged`: Marked for inclusion in the next commit
	- `committed`: Saved to the repository's history
- The `git status` command shows you the current state of your repo. It will tell you which files are untracked, staged, and committed.
### Staging:
- The `contents.md` file has been created, but as we saw, it's _untracked_. We need to stage it (add it to the "index") with the [git add](https://git-scm.com/docs/git-add) command before committing it later.
- Without staging, every file in the repository would be included in every commit, but that's often not what you want.
- Here's the command:
		`git add <path-to-file | pattern>`
### Commit:
- After staging a file, we can [commit](https://docs.github.com/en/pull-requests/committing-changes-to-your-project/creating-and-editing-commits/about-commits) it.
- A commit is a snapshot of the repository at a given point in time. It's a way to save the state of the repository, and it's how Git keeps track of changes to the project. A commit comes with a message that describes the changes made in the commit.
- Here's how to [commit](https://git-scm.com/docs/git-commit) all of your staged files:
```bash
git commit -m "your message here"
```

### Git Log:
- A Git repo is a (potentially very long) list of commits, where each commit represents the _full state of the repository_ at a given point in time.
- The [git log](https://git-scm.com/docs/git-log) command shows a history of the commits in a repository. This is what makes Git a version control system. You can see:
	- Who made a commit
	- When the commit was made
	- What was changed
- Each commit has a unique identifier called a "commit hash". This is a long string of characters that uniquely identifies the commit. Here's an example of mine:
```
5ba786fcc93e8092831c01e71444b9baa2228a4f
```
- You may have noticed that even though we (you and I) both have the **same content** in our repositories, we have **different commit hashes**. While commit hashes _are_ derived from their content changes, there's [also some other stuff](https://git-scm.com/book/en/v2/Git-Internals-Git-Objects#_git_commit_objects) that affects the end hash. For example:	
	- The commit message
	- The author's name and email
	- The date and time
	- Parent (previous) commit hashes
- All this to say that hashes are (almost) always unique, and because they're generated automatically for you, you don't need to worry too much about what goes into them right now.
- Git uses a cryptographic hash function called [SHA-1](https://en.wikipedia.org/wiki/SHA-1) to generate commit hashes. We won't go into the details of how SHA-1 works in this course, but it's important to know because you might also hear commit hashes referred to as "SHAs".
### The Plumbing:
- All the data in a Git repository is stored directly in the (hidden) `.git` directory. That includes all the commits, branches, tags, and other objects we'll learn about later.
- Git is made up of [objects](https://git-scm.com/book/en/v2/Git-Internals-Git-Objects) that are stored in the `.git/objects` directory. A commit is just a type of object.
- 

