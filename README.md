# git-fur-alles

A repository for learning git.

## Git Resources

* [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)
* [Git Tutorial](https://www.atlassian.com/git/tutorials/what-is-version-control)
* [Git Branching](https://learngitbranching.js.org/)
* [Git Book](https://git-scm.com/book/en/v2)

## Vocabulary

* **Repository** - A repository is a directory which contains your project work, as well as a few files (hidden by default) which are the local git database. Repositories can exist either locally on your computer or as a remote copy on another computer. A repository is made up of commits.
* **Clone** - A clone is a copy of a repository that lives on your computer instead of remotely. With your clone you can edit the files in your preferred editor and use Git to keep track of your changes without having to be online. It is, however, connected to the remote version so that changes can be synced between the two. You can push your local changes to the remote to keep them synced when you're online.
* **Remote** - This is the version of something that is hosted on a server. It can be connected to local clones so that changes can be synced.
* **origin** - The default name that Git gives to your main remote. Your local clone of a repository originally copied from the remote is called origin.
* **Branch** - A branch is a parallel version of a repository. It is contained within the repository, but does not affect the primary or master branch allowing you to work freely without disrupting the "live" version. When you've made the changes you want to make, you can merge your branch back into the master branch to publish your changes.
* **Commit** - A commit, or "revision", is an individual change to a file (or set of files). It's like when you save a file, except with Git, every time you save it creates a unique ID (a.k.a. the "SHA" or "hash") that allows you to keep record of what changes were made when and by who. Commits usually contain a commit message which is a brief description of what changes were made.
* **Staging area** - The staging area is where you place files when you're ready to commit them. Unlike your working directory, in the staging area you can choose what files will be included in your next commit by git adding the specific files you want, instead of everything in your working directory.
* **Merge** - Merging takes the changes from one branch and applies them into another. This often happens as a pull request (which can be thought of as a request to merge), or via the command line.
* **Pull** - Pull refers to when you are fetching in changes from the remote and merging them. For instance, if someone has edited the remote file you're both working on, you'll want to pull in those changes to your local copy so that it's up to date.
* **Fork** - A fork is a personal clone of another user's repository that lives on your git server. Used in open source development.

## Git states and transitions

A local git repository has three main states that your files can reside in:

* **Modified** files exists only in the working directory.
* **Staged** files are files that have been added to the staging area.
* **Committed** files are files that have been committed to the local git repository database.
  
As a last step, committed files can be pushed to a remote repository.

The following diagram shows the possible transitions between the states.

```other

```other
                           +---------+
+----------+   +--------+  | Comitted|           +--------+
|  Working |   |Staging |  |  .git   |           | Remote |
| Directory|   |  area  |  |  local  |           +---+----+
+----+-----+   +--------+  +---------+               |
     |             |            |                    |
     |<-------------------------+<-------------------+
     |             |    clone   |                    |
     |             |            |                    |
     |             |            |                    |
     |<-------------------------+                    |
     |          checkout        |                    |
     |             |            |                    |
     |             |            |                    |
     +------------>|            |                    |
     |    add      |            |                    |
     |             +----------->|                    |
     |             |   commit   |                    |
     |             |            |                    |
     |             |            +------------------->|
     |             |            |       push         |
     |             |            |                    |
     |             |            |                    |
     |<-------------------------+<-------------------+
     |             |    pull    |                    |
     |             |            |                    |
     |             |            |                    |
     |             |            |<-------------------+
     |             |            |        fetch       |
     |             |            |                    |
     |             |            |                    |
```

## Git Cheat Sheet

* Setup
  * `git config --global user.name “[firstname lastname]”`
  * `git config --global user.email “[valid-email]”`
* Initialization
  * `git init` - initialize local git repository
  * `git clone [url]` - clone repo from url
* Stage & Commit
  * `git status` - view status of working directory and staging area
  * `git diff` - view unstaged changes since last commit
  * `git add [file]` - add file to staging area
  * `git add -a` - add all files
  * `git commit -m “[descriptive message]”` - commit staged changes
  * `git commit -am “[descriptive message]”` - add and commit
* Branch & Merge
  * `git branch` - list branches
  * `git branch [branch-name]` - create branch
  * `git switch [branch-name]` - switch to branch
  * `git switch -c [branch-name]` - create and switch to branch
  * `git fetch` - fetch changes from remote repo and get remote branches
  * `git pull` - fetch and merge changes from remote repo
  * `git pull origin master` - fetch and merge changes from origin (upstream) master branch into current branch
* Stash
  * `git stash` - stash changes from working directory
  * `git stash list` - list stashed changes
  * `git stash pop` - apply stashed changes to working directory
* Undo
  * `git reset [file]` - unstage file
  * `git reset --hard` - discard all changes (changes are lost)
  * `git checkout [file]` - discard changes in working directory
  * `git checkout [branch-name]` - discard changes in working directory and switch to branch
  * `git revert [commit]` - revert commit, create new commit with inverse changes

## Workflow & Commands

* Basic master merge workflow
  * `git switch master` - Switch to master branch
  * `git pull` - fetch remote changes
  * Work, work work
  * `git commit -am “Add banana split recipie”`
  * Work, work, work
  * `git commit -am “Apply new styling”`
  * `git pull` - fetch and merge changes from other authors
  * `git push` - push branch to remote repo

* Basic branch and merge workflow
  * `git switch master` - Switch to master branch
  * `git pull` - fetch remote changes
  * `git switch -c [branch-name]` - create and switch to branch
  * Work, work work
  * `git commit -am “Add banana split recipie”`
  * Work, work, work
  * `git commit -am “Apply new styling”`
  * `git push origin [branch-name]` - push branch to remote repo
  * Create PR, review
  * `git pull origin master` - fetch and merge changes from other authors
  * Work, work, work
  * `git commit -am “Changes after review”`
  * `git push`

* Fix commit to master that should have been in branch
  * `git switch -c [branch-name]` - create and switch to branch (including commit)
  * `git switch master`
  * `git reset --hard HEAD~1` - reset master to previous commit
  * `git switch [branch-name]`