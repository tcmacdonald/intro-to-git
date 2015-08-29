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

In this example, we passed an inline commit message with the `-m` flag. 

If you don't specify a commit message like this, you'll be prompted to enter one in a text editor of your choice. More on that later.

## Diff'ing Changes

Let's assume that we've made some edits to index.html, which is now under revision control.

We can check what changed by using `git diff` like so...

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

Let's say you changed your mind and want undo the changes you just made.

First you have unstage the changes with the `git reset` command...

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

Now you can discard the changes with `git checkout`...

    $ git checkout -- index.html
    $ git status
      On branch master
      Untracked files:
        (use "git add <file>..." to include in what will be committed)

        about.html
        logo.png

Now the contents of `index.html` is back to where it was.

## Cleaning Up

At this point, our project folder has a couple uncommited files so let's stage and commit those.

    $ git add -A

The `-A` flag tells git that you want to stage every file.

    $ git status
      On branch master
      Changes to be committed:
        (use "git reset HEAD <file>..." to unstage)

        new file:   about.html
        new file:   logo.png

Now, we commit...

    $ git commit -am "Add uncommited files."
      [master 16ac13f] Add uncommited files.
      2 files changed, 0 insertions(+), 0 deletions(-)
      create mode 100644 about.html
      create mode 100644 logo.png

## History

You can view all the old commits with `git log`...

    $ git log
      commit 16ac13fa31202ffb88433f279468212d27df8a21
      Author: Taylor C. MacDonald <tcmacdonald@gmail.com>
      Date:   Mon Aug 24 23:58:22 2015 -0400

          Add uncommited files.

      commit 5d4781847e5c4460467a0eb8bc7a02f5dac79c56
      Author: Taylor C. MacDonald <tcmacdonald@gmail.com>
      Date:   Sun Aug 23 22:53:49 2015 -0400

          Added new file.
      (END)

Each commit has a unique, 40-digit identifier called a SHA.

You can view the details of an individual commit by passing the commit SHA to the `git show` command...

    $ git show 5d4781847e5c4460467a0eb8bc7a02f5dac79c56
      commit 5d4781847e5c4460467a0eb8bc7a02f5dac79c56
      Author: Taylor C. MacDonald <tcmacdonald@gmail.com>
      Date:   Sun Aug 23 22:53:49 2015 -0400

          Added new file.

      diff --git a/index.html b/index.html
      new file mode 100644
      index 0000000..cd08755
      --- /dev/null
      +++ b/index.html
      @@ -0,0 +1 @@
      +Hello world!
      (END) 

Conveniently, you can abbreviate the SHA value (7 or more characters) and get the same output...

    $ git show 5d47818
      # same output as above...

## Adding Remotes & Github

So far, we've done everything locally but Git is a powerful remote collaboration tool.

You can add a remote server to your repository and then "push" all your files and your commit history to that server.

    $ git remote add origin <server>
    $ git push origin master

Enter Github: a remote repository you can push to and pull from.

Github lets you visualize the commit history and diff output from your repository. It also supports issue tracking, wikis, etc. and has some really nice utilities for managing branches and pull-requests.

Interacting with Github is just like any remote...

    $ git remote add origin https://github.com/tcmacdonald/intro-to-git.git
    $ git pull origin master

## Branches

Often, you or your team will be working on different features simultaneously. You can use branches to keep each feature seperate until development is complete and then merge everything together.

To see a list of all the branches in your repo, do this...

    $ git branch
      * master

The default branch when you create a new repository is `master`.

You can create a new branch like this...

    $ git branch another-branch

And then switch to it, like so...

    $ git checkout some-branch

Or do both at the same time by passing the `-b` flag 

    $ git checkout -b testing
      Switched to branch 'testing'

    $ git branch
        master
        some-branch
      * testing

Now that we're on a new branch, we can change files and commit those changes to that branch without affecting the other branches.

Consider the following...

    $ cat index.html
      Hello world!

Now let's edit that file to say "Hello cruel world!" and then commit that update to the testing branch...

    $ git diff
      diff --git a/index.html b/index.html
      index cd08755..f6e8705 100644
      --- a/index.html
      +++ b/index.html
      @@ -1 +1 @@
      -Hello world!
      +Hello cruel world!
      (END) 

    $ git add index.html
    $ git commit -am "Update index.html"

Now if we cat the contents of index.html, we can see that the file has indeed changed...

    $ cat index.html
      Hello cruel world!

Now if we checkout the master branch and cat the same file, you'll see those changes are not persisted...

    $ cat index.html
      Hello world!

## Merging

Now that we can seperate our code into individual branches each with distinct commit histories, we can talk about merging branches together.

Assume we're satisfied with the changes in our testing branch and now want to bring those updates into the master branch.

First, let's make sure we're on master...

    $ git branch
      * master
        some-branch
        testing

Now we can use `git merge` to copy the updates in testing over to master...

    $ git merge testing
      Updating 16ac13f..cdc34cf
      Fast-forward
      index.html | 2 +-
      1 file changed, 1 insertion(+), 1 deletion(-)

Now the updates to index.html are reflected in the master branch...

    $ cat index.html
      Hello cruel world!

    $ git log
      commit cdc34cf998268ad44557e09da9edadef75a7ff25
      Author: Taylor C. MacDonald <tcmacdonald@gmail.com>
      Date:   Fri Aug 28 21:34:32 2015 -0400

          Update index.html

      commit 16ac13fa31202ffb88433f279468212d27df8a21
      Author: Taylor C. MacDonald <tcmacdonald@gmail.com>
      Date:   Mon Aug 24 23:58:22 2015 -0400

          Add uncommited files.

      commit 5d4781847e5c4460467a0eb8bc7a02f5dac79c56
      Author: Taylor C. MacDonald <tcmacdonald@gmail.com>
      Date:   Sun Aug 23 22:53:49 2015 -0400

          Added new file.
      (END) 

## Resolving Conflicts

When working with teams of developers, you will occasionally run into conflicts when pulling down updates. A conflict takes place when there was a change to a particular line in a file, both locally and remotely, and Git was unable to determine which version is the keeper 

    $ git pull origin master 
      remote: Counting objects: 3, done.
      remote: Compressing objects: 100% (2/2), done.
      remote: Total 3 (delta 1), reused 0 (delta 0)
      Unpacking objects: 100% (3/3), done.
      From ../test
      * branch            master     -> FETCH_HEAD
        b4c9014..2423465  master     -> origin/master
      Auto-merging planets.md
      CONFLICT (content): Merge conflict in planets.md
      Automatic merge failed; fix conflicts and then commit the result.

When you run into a conflict, you'll need to resolve it manually by opening the file and inspecting the conflicting code.

    $ git status
      On branch branch-b
      You have unmerged paths.
        (fix conflicts and run "git commit")

      Unmerged paths:
        (use "git add ..." to mark resolution)

      both modified:      planets.md

If you inspect the planets.md file you might see something like this...

    the number of planets is
    <<<<<<< HEAD
    nine
    =======
    eight
    >>>>>>> 24234654d3e9678f6f0e802a07974070cf77cdcc

This notation is Git telling you that there was a conflict it could not resolve automatically.

After editing the file manually, it looks like this...

    the number of planets is eight

We can now commit our update to the repo, thus resolving the conflict.

    $ git add planets.md
    $ git commit -m "Resolve conflict."

## Pull Requests

A "pull request" (PR) is a method of submitting changes for consideration to a software project.

Technically, PR's are a workflow method and not a feature of the revision control system itself.

Github makes this really easy.
