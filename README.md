## The Problem

* Software projects have lots of files.
* Lots of people making changes.
* Easy to overwrite somebody's work.

## Enter Version Control

> Version control is a system that records changes to a file or set of files over time so that you can recall specific versions later.

* Track every change to every file.
* Manage multiple versions of file(s).
* Who added/edited/deleted what?
* Attach descriptive messages to each change.

## Landscape

Two classes of modern version control... 

* **Centralized**  
  Assumes a single "central" copy of your project somewhere (probably on a server), and programmers will "commit" their changes to this central copy.  
  _Subversion (SVN), CVS, SourceSafe_
* **Distributed**  
  Doesn't rely on a central server. Every developer "clones" a copy of a repository and has the full history of the project on their own hard drive.  
  _Bazaar, Mercurial, Git_

## Why Git?

* Free and open source distributed version control system.
* Created by Linus Torvalds in 2005 for Linux Kernel Development.
* Popularized by Github.

## Getting Git

* **OSX:**  
  You probably already have Git installed. If not, use [Homebrew](http://brew.sh/)
* **Windows**  
  Download [Git for Windows](https://git-for-windows.github.io/)
* **Linux**  
  Install via relevant package manager (apt-get, yum, etc.)

There are also some GUIs for Git...

* [Github for Mac and Windows](https://desktop.github.com/)
* [and many more...](https://git.wiki.kernel.org/index.php/InterfacesFrontendsAndTools#Graphical_Interfaces)

## An Introduction to Bash (pt. 1)

> A Unix "shell" is a command-line interpreter that provides a traditional user interface for the Unix operating system and for Unix-like systems.

* There are a bunch of different shells... Bourne shell, C shell, Korn shell, Z shell, etc.
* The first major shell was the Bourne Shell, developed in the late 70's.
* We're going to focus on the "Bourne again shell" or Bash (default shell for OSX and Linux)

_Hint: You can install Bash bindings in Windows via [Git for Windows](https://git-for-windows.github.io/)_

## An Introduction to Bash (pt. 2)

`ls` - List directory contents  
`pwd` - Present working directory  
`cd` - Change directory  
`mkdir` - Make directory  
`mv` - Move (or rename) a file or directory  
`rm` - Remove files and directories  
`cp` - Copy a file or directory  
`touch` - Change timestamp (or create a file)  
`history` - Show command history  
`cat` - Concatenate and print files  
`less` - Paged output; the opposite of more  

## Git Workflow

The typical workflow for Git looks like this...

1. Add or edit some files in your project directory.
2. Add the files to a temporary staging area.
3. Commit the staged changes to the repository.

## Initializing a New Repository

Imagine we have a directory with a couple HTML files and an image that we want to track with Git.

First we have to initialize a new repository...

    $ cd /path/to/some/directory
    $ git init
      Initialized empty Git repository in /path/to/some/directory/.git/  

## Checking the Status

The status of a repository tells you what changed since the last commit.

    $ git status
      On branch master

      Initial commit

      Untracked files:
        (use "git add <file>..." to include in what will be committed)

        about.html
        index.html
        logo.png

      nothing added to commit but untracked files present (use "git add" to track)

## Staging Changes

In order to track these files with Git, we have to...

1. Add them to the stage with `git add`
2. Commit them to the repository with `git commit`

For example...

    $ git add index.html
    $ git status
      On branch master

      Initial commit

      Changes to be committed:
        (use "git rm --cached <file>..." to unstage)

        new file:   index.html

      Untracked files:
        (use "git add <file>..." to include in what will be committed)

        about.html
        logo.png

## Committing Changes

Once a file has been staged, you can commit it to the repo...

    $ git commit -m "Added new file."
      [master (root-commit) 5d47818] Added new file.
      1 file changed, 1 insertion(+)
      create mode 100644 index.html

## Diff'ing Changes

Let's assume that we've made some edits to index.html, which is now under revision control...

    $ git diff
      diff --git a/index.html b/index.html
      index cd08755..e4a5346 100644
      --- a/index.html
      +++ b/index.html
      @@ -1 +1,2 @@
      Hello world!
      +Is anybody out there?
      (END)

Looks good, let's add it to the stage.

    $ git add index.html
    $ git status
      On branch master
      Changes to be committed:
        (use "git reset HEAD <file>..." to unstage)

        modified:   index.html

      Untracked files:
        (use "git add <file>..." to include in what will be committed)

        about.html
        logo.png

## Unstaging Changes

    $ git reset HEAD index.html
      Unstaged changes after reset:
      M   index.html

    $ git status
      On branch master
      Changes not staged for commit:
        (use "git add <file>..." to update what will be committed)
        (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   index.html

      Untracked files:
        (use "git add <file>..." to include in what will be committed)

        about.html
        logo.png


## Discarding Changes

## History

## Adding Remotes & Github

## Branches

## Merging

## Workflow & Pull Requests

