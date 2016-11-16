### Setup

1. Download starter kit... http://bit.ly/intro-to-git-starter-kit
2. Open a new Bash window and `cd` in to the starter kit's directory

First, let's personalize Git by setting some configuration values...

`git config --global user.name "Your Name"`  
`git config --global user.email "your_email@whatever.com"`

<br>

### Local Workflow

Git will track the contents of every file within a directory.

* What changed?
* When did it change?
* Who changed it?

As you're working on the files, you can create "save-points" (aka "revisions"; aka "commmits").  

If you ever make a mistake, you can recover a previous state of a file.

---

`git init`

* Initializes a new "repository"
* Tells git to keep track of changes in your current directory
* `ls -la .git`

`git status`

* Shows what has changed since our last commit.
* Use this command constantly.
* Top of your “how do I figure out what happened” tools
* `git status -s`

---

> **_Creating a save-point is a two-step process..._**  

> * You "stage" your changes before "committing" your changes.
> * Staged files will be included in the next save-point.
> * Helps with organizing your files.

---

`git add`

* Adds the specified files to the stage<br>(i.e. tell Git to incude this file in the next save-point).
* `git add .`

`git commit -m "initial commit."`

* Create a new save-point by commiting our changes to the repository.
* Use the `-m` flag to pass commit message inline.

`git log`

* See all the save-points over the lifetime of this repository.
* It's your safety net– you can always get back to anything.

---

> **_Demo_:**  
> 1. Add new `README.md` and update `index.html`  
2. Make two seperate commits to illustrate staging area.

> _(Checkout `git log -p`)_

---

`git reset <filename>`

* Remove a file from the stage.

`git diff`

* Displays changes since the last save-point

---

> **_In-class Exercise (5 minutes)_:**  
> 1. Edit some files  
> 2. Stage your changes  
> 3. Commit your changes

---

Undoing the last commit:

`git reset HEAD~1`

Discarding local changes:

`git checkout .`

<br>

### Remote Workflow

Why would you use remote repos?

* Collaboration
* Backups
* Deployment
* Automated Services

Each repository can have multiple "remotes", you refer to them with aliases.  
_(Github is just another remote repository.)_

---

> **_In-Class Exercise (5-minutes)_:** Create a New Github Repo

> 1. Login to Github.
2. Create a new public repository.
3. Follow on-screen instructions to add remote to your local repository.
4. Push changes to Github.
5. Checkout how you can clone.

---

`git clone`

* Creates a "clone" of a remote repository.
* Copies the entire commit history to your computer.

`git push <remote-alias> <branch-name>`

* Push code on specific branch to a remote repository.
* Copies your entire commit history to the remote.

---

> **_Demo_:**  
> 1. Edit a file on Github.
2. Pull it's changes down.

---

`git pull <remote-alias> <branch-name>`

* Copies updates from a remote repository to your computer.
* Git will try to automatically merge your code.

---

> **_Did You Know?_**  
> There are three ways to start a new project... 
1. `git init` 
2. `git clone`
3. Fork a repository and `git clone`

---

<br>

### Branches

* Git automatically calls the main branch “master”.

---

> **_Demo_:**  
1. Draw a linear-picture of what branches look like.

---

Create a new branch:

`git branch <branch-name>`

See all the branches:

`git branch`

Checkout a specific branch:

`git checkout <branch-name>`

Delete a branch:

`git branch -D <branch-name>`

<br>

### Merging

`git merge <branch-name>`

* Merging combines the histories of two branches.
* Git will try to automatically merge your code.

Conflicts happen when Git doesn't know how to merge your code.

They look like this... 

    <<<<<<< HEAD
    This was once a test, but is no longer.
    =======
    This is a test.
    >>>>>>> some-branch-name

When you encounter a conflict, you need to edit the file by hand.

---

> **_In-Class Exercise_:**  
> 1. Create a merge conflict by editing the same file on two branches.
2. Merge the branches.
3. Resolve the conflict.

---

<br>

### Forks and Pull-Requests

These are Github specific terms (though other platforms have adopted them).

* A "fork" is clone of a repository to your Github account.
* A "pull-request" is a formal request to merge forked code back into the original repo.

---

> **_In-Class Exercise_:**  
> 1. Create a new fork of... [girldevelopitcincinnati/memehub](https://github.com/girldevelopitcincinnati/memehub)
2. Clone the fork and add new animated gif the respository.
3. Submit a pull-request.

---

<br>

