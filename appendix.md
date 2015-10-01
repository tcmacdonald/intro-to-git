## An Introduction to Bash (pt. 1)

> A Unix "shell" is a command-line interpreter that provides a traditional user interface for the Unix operating system and for Unix-like systems.

* There are a bunch of different shells... Bourne shell, C shell, Korn shell, Z shell, etc.
* The first major shell was the Bourne Shell, developed in the late 70's.
* We're going to focus on the "Bourne again shell" or Bash (default shell for OSX and Linux)

_Hint: You can install Bash bindings in Windows via [Git for Windows](https://git-for-windows.github.io/)_


## An Introduction to Bash (pt. 2)

`ls` - List directory contents
> *Optional flags:*  
> &nbsp;&nbsp;Long listing (with details)... `ls -l`  
> &nbsp;&nbsp;List all files... `ls -a`

`pwd` - Present working directory  

`cd` - Change directory
> *Special characters:*  
> &nbsp;&nbsp;Root of filesystem... `cd /`  
> &nbsp;&nbsp;Your home directory... `cd ~`  
> &nbsp;&nbsp;Go up a directory... `cd ..`  
> &nbsp;&nbsp;Return to last directory... `cd -`

`mkdir` - Make directory  
> *Optional flags:*  
> &nbsp;&nbsp;Create intermediate directories as required. ... `mkdir -p`  

`mv` - Move (or rename) a file or directory  

`rm` - Remove files and directories  
> *Optional flags:*  
> &nbsp;&nbsp;Remove recursively (directories)... `rm -r`  

`cp` - Copy a file or directory  
> *Optional flags:*  
> &nbsp;&nbsp;Copy recursively (directories)... `cp -R`  

`touch` - Change timestamp (or create a file)  
`which` - Show the path to command  
`history` - Show command history  
> *Special characters:*  
> &nbsp;&nbsp;Recall previous command... `!!`  
> &nbsp;&nbsp;Repeat command in your history... `!<linenumber>`  

`cat` - Concatenate and print files  
`less` - Paged output; the opposite of more  
`git` - Version control

## Git Workflow

The typical workflow for Git looks like this...

1. Add or edit some files in your project directory.
2. Add the files to a temporary staging area.
3. Commit the staged changes to the repository.

## Introduce Yourself

First, let's personalize Git by setting some configuration values...

    $ git config --global user.name "Your Name"
    $ git config --global user.email "your_email@whatever.com"

## Configuring Git

You should now have a file in your home directory called `.gitconfig`. Let's take a look...

    $ cat ~/.gitconfig
      [user]
        email = tcmacdonald@gmail.com
        name = Taylor C. MacDonald
      [core]
        editor = /usr/bin/vim

You can add new configuration values, aliases, etc. here if needed.

## Setting Your Editor

Let's tell Git to use an editor of our choice, such as *Sublime Text*...

**Mac Users:**

    $ ln -s "/Applications/Sublime Text.app/Contents/SharedSupport/bin" /usr/local/sbin/subl
    $ git config --global core.editor "subl -n -w"

**Windows Users:** Something like... this?

    $ git config --global core.editor "'c:/program files/sublime text 3/subl.exe' -w"

...or this?

    $ git config --global core.editor "'C:\\Program Files\\Sublime Text 3\\subl.exe' -w"

...or this?

    $ git config --global core.editor "subl.exe -w"

More here... [http://stackoverflow.com/questions/8951275/how-can-i-make-sublime-text-the-default-editor-for-git](http://stackoverflow.com/questions/8951275/how-can-i-make-sublime-text-the-default-editor-for-git)

## Initializing a New Repository

You can track any directory you want with Git by initializing a new repository.

    $ cd /path/to/some/directory
    $ git init
      Initialized empty Git repository in /path/to/some/directory/.git/  

What just happened? Git created a new, hidden directory called `.git` which it uses to track changes.

    $ ls -la
      total 0
      drwxr-xr-x   3 tcmacdonald  staff   102 Sep 21 22:57 .
      drwxr-xr-x  34 tcmacdonald  staff  1156 Sep 21 22:57 ..
      drwxr-xr-x  10 tcmacdonald  staff   340 Sep 21 22:57 .git

Now when we add new files (and folders) we can use Git to keep track of everything.

## Cloning a Remote Repository

Let's clone a repository from Github to learn a little more about how Git works...

    $ git clone https://github.com/tcmacdonald/intro-to-git-starter-kit.git
      Cloning into 'intro-to-git-starter-kit'...
      remote: Counting objects: 17, done.
      remote: Compressing objects: 100% (10/10), done.
      remote: Total 17 (delta 3), reused 17 (delta 3), pack-reused 0
      Unpacking objects: 100% (17/17), done.
      Checking connectivity... done.

Git just created a new directory called `intro-to-git-starter-kit` containing all the project files. Let's inspect...

    $ cd intro-to-git-starter-kit/
    $ ls -la
      total 24
      drwxr-xr-x   7 tcmacdonald  staff   238 Sep 24 23:00 .
      drwxr-xr-x  36 tcmacdonald  staff  1224 Sep 24 23:00 ..
      drwxr-xr-x  13 tcmacdonald  staff   442 Sep 24 23:00 .git
      -rw-r--r--   1 tcmacdonald  staff    10 Sep 24 23:00 .gitignore
      -rw-r--r--   1 tcmacdonald  staff   583 Sep 24 23:00 about.html
      drwxr-xr-x   3 tcmacdonald  staff   102 Sep 24 23:00 images
      -rw-r--r--   1 tcmacdonald  staff    13 Sep 24 23:00 index.html

## Checking the Status

The status tells you what changed since the last commit.

    $ git status
      On branch master
      Your branch is up-to-date with 'origin/master'.
      nothing to commit, working directory clean

Say you made some changes...

    $ git status
      On branch master
      Your branch is up-to-date with 'origin/master'.
      Changes not staged for commit:
        (use "git add <file>..." to update what will be committed)
        (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   index.html

      no changes added to commit (use "git add" and/or "git commit -a")

You can change the format of the command's output by passing the `-s` flag...

    $ git status -s
      M index.html

## Uncommitted Changes

You can use `git diff` to see what changed ...

    $ git diff
      diff --git a/index.html b/index.html
      index cd08755..e4a5346 100644
      --- a/index.html
      +++ b/index.html
      @@ -1 +1,2 @@
      Hello world!
      +Is anybody out there?
      (END)

## Committing Changes

Commiting a revision is a 2-step process...

    $ git add index.html
    $ git commit -m "Update index.html"
      [master 80c520c] Update index.html
      1 file changed, 1 insertion(+)

## The Stage

With the `git add` command, you are "staging" files in preparation for commit. This is a convention designed to help you *organize your commits*.

Imagine you've edited the copy in a couple files and added something new...

    $ git status
      On branch master
      Your branch is ahead of 'origin/master' by 1 commit.
        (use "git push" to publish your local commits)
      Changes not staged for commit:
        (use "git add <file>..." to update what will be committed)
        (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   about.html
        modified:   index.html

      Untracked files:
        (use "git add <file>..." to include in what will be committed)

        news.html

Lets split these changes into a couple commits. First, lets add `news.html` to the stage...

    $ git add news.html

Now we can see that file is ready to be committed...

    $ git status
      On branch master
      Your branch is ahead of 'origin/master' by 1 commit.
        (use "git push" to publish your local commits)
      Changes to be committed:
        (use "git reset HEAD <file>..." to unstage)

        new file:   news.html

      Changes not staged for commit:
        (use "git add <file>..." to update what will be committed)
        (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   about.html
        modified:   index.html


Once a file has been staged, you can commit it to the repo...

    $ git commit -m "Added new file."
      [master (root-commit) 5d47818] Added new file.
      1 file changed, 1 insertion(+)
      create mode 100644 index.html

In this example, we passed an inline commit message with the `-m` flag. 

If you don't specify a commit message like this, you'll be prompted to enter one in a text editor of your choice. More on that later.

## Undoing a Commit

Made a mistake? You can undo your last commit with the `git reset` command, like so...

    $ git reset HEAD~1
      Unstaged changes after reset:
      M   about.html
      M   index.html

Git responds by telling you all the unstaged commits in the current directory. You can see that our last commit was indeed reverted by looking at status...

    $ git status -s
       M about.html
       M index.html
      ?? news.html

## Staging Everything

Sometimes you want to commit all the latest changes and staging individual files one by one can be a pain.

You can add everything to the stage by passing the `-A` flag...

    $ git add -A
      M  about.html
      M  index.html
      A  news.html

## Unstaging Changes

Let's say you changed your mind and want to unstage a particular file.

You can do this by passing a file to the `git reset` command...

    $ git reset index.html
      Unstaged changes after reset:
      M   index.html

    $ git status
      On branch master
      Your branch is up-to-date with 'origin/master'.
      Changes to be committed:
        (use "git reset HEAD <file>..." to unstage)

        modified:   about.html
        new file:   news.html

      Changes not staged for commit:
        (use "git add <file>..." to update what will be committed)
        (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   index.html

Want to unstage everything? Just call `git reset` with no arguments...

    $ git reset
    Unstaged changes after reset:
    M	about.html
    M	index.html

Check the status to ensure nothing is left on the stage...

    $ git status
      On branch master
      Your branch is up-to-date with 'origin/master'.
      Changes not staged for commit:
        (use "git add <file>..." to update what will be committed)
        (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   about.html
        modified:   index.html

      Untracked files:
        (use "git add <file>..." to include in what will be committed)

        news.html

      no changes added to commit (use "git add" and/or "git commit -a")

## Discarding Changes

Now you can discard all your local changes with `git checkout`...

    $ git checkout -- index.html
    $ git status
      On branch master
      Your branch is up-to-date with 'origin/master'.
      Changes not staged for commit:
        (use "git add <file>..." to update what will be committed)
        (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   about.html

      Untracked files:
        (use "git add <file>..." to include in what will be committed)

        news.html

      no changes added to commit (use "git add" and/or "git commit -a")

Now the contents of `index.html` is back to where it was.

## Cleaning Up

At this point, our project folder has a couple uncommited files so let's stage and commit those.

    $ git add -A
    $ git status
      On branch master
      Your branch is up-to-date with 'origin/master'.
      Changes to be committed:
        (use "git reset HEAD <file>..." to unstage)

        modified:   about.html
        new file:   news.html

Now, we commit...

    $ git commit -m "Leftovers."
      [master 0b2b1f9] Add uncommitted files.
      2 files changed, 7 insertions(+), 1 deletion(-)
      create mode 100644 news.html

## History

You can view all the commits with `git log`...



    $ git log
      commit 0b2b1f9a8fe2e836d300ac9e711429d01cbca0e7
      Author: Taylor C. MacDonald <tcmacdonald@gmail.com>
      Date:   Sun Sep 27 21:58:59 2015 -0400

          Add uncommitted files.

      commit 5466ecf3271990817904e3f48dea166bf0af4605
      Author: Taylor C. MacDonald <tcmacdonald@gmail.com>
      Date:   Tue Sep 22 08:57:59 2015 -0400

          Cleanup punctuation.

      commit 61e70075e6d77bf3e6513c07253dabb9d8c1239b
      Author: Taylor C. MacDonald <tcmacdonald@gmail.com>
      Date:   Mon Sep 21 23:19:33 2015 -0400

          Remove hidden .DS_Store files. :boom:

      commit a1f9b3e92585015c9ee6a4e2bc59205554438325
      Author: Taylor C. MacDonald <tcmacdonald@gmail.com>
      Date:   Mon Sep 21 23:12:26 2015 -0400

          Add about page.

      commit 7b16c0cbad5caa44f62de31a51ec03cf6bb3ce44
      Author: Taylor C. MacDonald <tcmacdonald@gmail.com>
      Date:   Mon Sep 21 23:06:35 2015 -0400

          Initial commit.
      (END) 

Each commit has a unique, 40-digit identifier called a SHA.

You can view the details of an individual commit by passing the commit SHA to the `git show` command...

    $ git show 5466ecf3271990817904e3f48dea166bf0af4605
      commit 5466ecf3271990817904e3f48dea166bf0af4605
      Author: Taylor C. MacDonald <tcmacdonald@gmail.com>
      Date:   Tue Sep 22 08:57:59 2015 -0400

          Cleanup punctuation.

      diff --git a/about.html b/about.html
      index 2e5af6b..006caec 100644
      --- a/about.html
      +++ b/about.html
      @@ -1,5 +1,5 @@
      <h1>Sollicitudin Pharetra Nullam</h1>
      -<img src="images/gdi.png" alt="Girl, Develop It" />
      +<img src="images/gdi.png" alt="Girl Develop It" />
      (END) 

Conveniently, you can abbreviate the SHA value and get the same output...

    $ git show 5466ecf
      # same output as above...

## Adding Remotes & Github

So far, we've done everything locally but Git is a powerful remote collaboration tool by allowing us to "push" and "pull" updates to/from remote endpoints.

Since we cloned this repository from Github, we already have a remote endpoint that points to Github.

    $ git remote -v
      origin	https://github.com/tcmacdonald/intro-to-git-starter-kit.git (fetch)
      origin	https://github.com/tcmacdonald/intro-to-git-starter-kit.git (push)

Adding a remote server your repository is easy too. In the example below, you'd replace &lt;name&gt; with the name of your remote (eg. "origin") and &lt;server&gt; with the address of your remote.

    $ git remote add <name> <server>


Then "pushing" all your files and your commit history to a remote is as easy as executing the following (where "master" is your branch name)...

    $ git push origin master
      Counting objects: 4, done.
      Delta compression using up to 8 threads.
      Compressing objects: 100% (4/4), done.
      Writing objects: 100% (4/4), 430 bytes | 0 bytes/s, done.
      Total 4 (delta 2), reused 0 (delta 0)
      To git@github.com:tcmacdonald/intro-to-git-starter-kit.git
        5466ecf..0b2b1f9  master -> master

"Pulling" updates from your remote endpoint is also easy...

    $ git pull origin master
      From github.com:tcmacdonald/intro-to-git-starter-kit
      * branch            master     -> FETCH_HEAD
      Already up-to-date.

## Branches

Often, you or your team will be working on different features simultaneously. You can use branches to keep each feature seperate until development is complete and then merge everything together.

To see a list of all the branches in your repo, do this...

    $ git branch
      * master

The default branch when you create a new repository is `master`.

You can create a new branch like this...

    $ git branch some-branch

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
    $ git commit -m "Update index.html"

Now if we cat the contents of index.html, we can see that the file has indeed changed...

    $ cat index.html
      Hello cruel world!

Now if we checkout the master branch and cat the same file, you'll see those changes are not persisted...

    $ git checkout master
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
      commit d89e6fc154c300e1d09872e78d83489fd3ed0d2a
      Author: Taylor C. MacDonald <tcmacdonald@gmail.com>
      Date:   Sun Sep 27 22:27:52 2015 -0400

          Update index.html

      commit 5466ecf3271990817904e3f48dea166bf0af4605
      Author: Taylor C. MacDonald <tcmacdonald@gmail.com>
      Date:   Tue Sep 22 08:57:59 2015 -0400

          Cleanup punctuation.

      commit 61e70075e6d77bf3e6513c07253dabb9d8c1239b
      Author: Taylor C. MacDonald <tcmacdonald@gmail.com>
      Date:   Mon Sep 21 23:19:33 2015 -0400

          Remove hidden .DS_Store files. :boom:

      commit a1f9b3e92585015c9ee6a4e2bc59205554438325
      Author: Taylor C. MacDonald <tcmacdonald@gmail.com>
      Date:   Mon Sep 21 23:12:26 2015 -0400

          Add about page.

      commit 7b16c0cbad5caa44f62de31a51ec03cf6bb3ce44
      Author: Taylor C. MacDonald <tcmacdonald@gmail.com>
      Date:   Mon Sep 21 23:06:35 2015 -0400

          Initial commit.
      (END) 

## Resolving Conflicts

When working with teams of developers, you will occasionally run into conflicts when pulling down updates. A conflict takes place when there was a change to a particular line in a file, both locally and remotely, and Git was unable to determine which version is the keeper.

    $ git pull origin master 
      remote: Counting objects: 3, done.
      remote: Compressing objects: 100% (1/1), done.
      remote: Total 3 (delta 1), reused 3 (delta 1), pack-reused 0
      Unpacking objects: 100% (3/3), done.
      From github.com:tcmacdonald/intro-to-git-starter-kit
      * branch            master     -> FETCH_HEAD
        5466ecf..e5be2a2  master     -> origin/master
      Auto-merging index.html
      CONFLICT (content): Merge conflict in index.html
      Automatic merge failed; fix conflicts and then commit the result.

When you run into a conflict, you'll need to resolve it manually by opening the file and inspecting the conflicting code.

    $ git status
      On branch master
      Your branch and 'origin/master' have diverged,
      and have 1 and 1 different commit each, respectively.
        (use "git pull" to merge the remote branch into yours)
      You have unmerged paths.
        (fix conflicts and run "git commit")

      Unmerged paths:
        (use "git add <file>..." to mark resolution)

        both modified:   index.html

      no changes added to commit (use "git add" and/or "git commit -a")

If you inspect the index.html file you might see something like this...

    <<<<<<< HEAD
    Hello cruel world!
    =======
    Goodbye world!
    >>>>>>> e5be2a2a442cecf18082d5438742abd06c22cbe3

This notation is Git telling you that there was a conflict it could not resolve automatically.

After editing the file manually, it looks like this...

    Hello cruel world!

We can now commit our update to the repo, thus resolving the conflict.

    $ git add index.html
    $ git commit -m "Resolve conflict."

## Forking a Repository

Even though you can clone and view details of any public repository, you'll need permissions to push your updates to them.

Thus, a more appropriate workflow for commiting your changes back to somebody else's repository is to "fork" the repo, commit your changes to the fork and then submit a "pull request" back to the original repository.

When you "fork" a repository in Github, you are copying the entire contents (including all commit data) to your own account. You don't have to submit a pull-request unless you want to. 

Since forking is super fast in Github and public repo's are free, this is an extremely useful way to track incremental changes or bug fixes to open-source projects. Likewise, it's trivial to pull in "upstream" changes applied to the original repo, keeping your copy in sync with the ongoing development of the project.

## Pull Requests

A "pull request" (PR) is a method of submitting changes for consideration to a software project.

Technically, PR's are a workflow method and not a feature of the version control system itself.

Github makes this really easy.

## Forks and PR's in Practice

Let's do this together so we can get an idea of how this workflow operates in the real world.

1. Go to [https://github.com/tcmacdonald/intro-to-git-starter-kit](https://github.com/tcmacdonald/intro-to-git-starter-kit) and fork the repository to your own account.
1. Create a new fork of the Starter Kit respository.
1. Add your fork as a new remote.
1. Make some changes locally– add some files, edit some files, etc. and commit them to your repo.
1. Push those changes back to your fork.
1. Submit a pull-request back to the original repository with all your changes.

## Questions?
