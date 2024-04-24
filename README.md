# This repo will have all info about Git that we learned

### 20 Git Basic Commands Every QA Engineer Should Know

#### Setting your username in Git

The username is needed to bind commits to your name. This is not the same as the GitHub account username used to log in to the GitHub profile. You can set or change the username using the **git config** command. The new name will automatically show up in subsequent commits pushed via the command line.

> git config --global user.name "Michael Scott"

You can also change the email address associated with your git commits with the **git config** command. The new email address will automatically show up on all future commits submitted to GitHub via the command line.

> git config --global user.email "michael.scott@dundermifflin.com"

#### Credential caching

Credentials can be cached using the **config** option with the **--global** flag. This helps you with no need to manually enter a username and password when creating a new commit. Helps to temporarily store passwords in memory.

> git config --global credential.helper cache

#### Setting up a repository

Create an empty Git repository or reinitialize an existing one. Executing **git init** creates a .git subdirectory in the current working directory, which contains all of the necessary Git metadata for the new repository. This metadata includes subdirectories for objects, refs, and template files.

> git init

#### Add files to stagging area

The **git add** command adds new or changed files in your working directory to the Git staging area.
Add somefile:

> git add somefile.js

Add all files:

> git add .

#### Repo status check

The **git status** command displays the state of the working directory and the staging area. It lets you see which changes have been staged, which haven’t, and which files aren’t being tracked by Git.

> git status

#### Take a snapshot of changes

Record changes to the repository. This command is used to save your changes to the local repository. Can be used with some git keys, like:

> - m to add message to your commit
> - a to stage all files to your commit
>   --amend to rewrite last commit with any currently staged changes or new commit message
>   git commit -m "Commit message"
>   git commit --amend
>   git commit --amend -m "New message"

#### Check git history

Show commit logs. Also as a git user you can use **git log** command in more advanced way, just adding some keys to your git log command.

> git log

Oneline flag, display each commit to a single line:

> git log --oneline
> Shortlog groups each commit by author and displays the first line of each commit message:

> git shortlog

The **--graph** option draws an ASCII graph representing the branch structure of the commit history. This is commonly used in conjunction with the **–oneline** and **–decorate** commands to make it easier to see which commit belongs to which branch:

> git log --graph --oneline --decorate

Also you can limit the number of commits to log ouput:

**git log -5**
Soporting filtering git history, for example by date, by author, by file, by message:

> git log --after="yesterday" --before="2022-10-10"
> git log --author="Michael"
> git log -- somefile.js
> git log -S "fix"

#### Display changes

**git diff** show changes between commits, commit and working tree.

> git diff
> Specify filename to display ongoing changes of its file:

**git diff somefile.js**
Displays changes between the branches master and develop:

**git diff master..develop**

#### Files renaming

You can rename a file or folder with the mv command. You should specify a source and a destination paths. The source is an actual file or folder, and the destination is an existing folder.

> git mv directory1/somefile.js directory

#### Branching feature

A branch represents an independent line of development. Branches serve as an abstraction for the edit/stage/commit process. The git branch command lets you create, list, rename, and delete branches.
To create new branch:

> git branch branch_name

Also you can pass some keys to git branch command:

**git branch -m <branch>** to rename current branch
**git branch -d <branch>** to delete branch locally
**git push origin --delete <branch>** to push changes to remote informing of deleting branch to the remote origin repository (require use with previously command)
**git branch -a** to show list of all branches

#### Undo file changes

**git restore** command helps to unstage or even discard uncommitted local changes. The command can be used to undo the effects of git add and unstage changes you have previously added, also can also be used to discard local changes in a file, thereby restoring its last committed state.

> git restore somefile.js
> git restore --staged index.js

#### Working with remote commands

**git remote** manage set of tracked remote repositories.
To show list of all remote connections:

> git remote -v

To change remote url:

> git remote set-url <url> <new_url>

To rename current connections, next command can be used:

> git remote rename <old_name> <new_name>

To delete connection:

> git remote remove <remote_name>

#### Save changes to clipboard

**git stash** Stash the changes in a dirty working directory away. This command takes your uncommitted changes (both staged and unstaged), saves them away for later use.

> git stash

Several keys can be added to command:

**git stash** to stash tracked files
**git stash -u** to stash untracked files
**git stash -a** to stash all files (including ignored files)
Stash command saves your changes to some kind of list of changes, you can access to this just using:

> git stash list

Also you can add message to your stash, annotate them using git stash save "message" command:

> git stash save "some comment"

Also it supports viewing stash diffs:

> git stash show

To apply stash saved changes (it will apply the last stash from stash list):

> git stash apply

And to be able to clear all stashes:

> git stash clear

#### Tagging

**git tag** tag specific points in a repository’s history.

> git tag v1.1

To access to list of tags use **git tag -l.** To delete just pass specific key **git tag -d v1.0.** To list remote tags: **git ls-remote --tags.** To retag (renaming of existing tag) just send with force key: **git tag -f v1 v1.1** , in this case we renaming v1 with new v.1.1.

#### Get latest remote changes

To get the latest changes to your local there are 2 git commands: **git pull** and **git fetch.** The main difference between them is that **git fetch** will download the remote content but not update your local repo’s working state, leaving your current work intact. I personal using a **git fetch** command with **--prune key**, which is the best utility for cleaning outdated branches. Before fetching, remove any remote-tracking references that no longer exist on the remote. **git pull** instead will download the remote content for the active local branch and immediately execute merge onto your files. Also **git pull** can be used with rebase common key: **git pull -r to pull and rebase.**

Undoing changes and restoring lost commits
**git cherry-pick** is used for this purpose. Cherry-picking in git means that you choose a commit from one branch and apply it onto another. Normally in dev teams used for quick bug fixes (hotfixes) under release stages, or when there are needs to apply not merged commits. To use this command you should pass commit sha.

#### Undo last commits

In git existing two ways to undo last changes: **git revert** and **git reset.** **git revert** command creates a new commit that undoes the changes from a previous commit. This command adds new history to the project. **git reset** is used to undo changes in your working directory that haven’t been comitted yet. Reset command can be used with arguments **--soft,** **--mixed,** **--hard.** By default git uses reset with --mixedkey (uncommit + unstage changes). Frequently used by developers is **--hard** option (uncommit + unstage + delete changes). When passed **--hard** commit history ref pointers are updated to the specified commit. And the **--soft** is more accurate way if you want to uncommit changes, in this case changes are left staged.
For example to hard reset files to HEAD on git:

> git reset --hard HEAD

#### Switching between commits or branches

**git checkout** command is used. You can switch between commits and branches, just passing branch_name/commit_sha to git checkout command. Also you can create new no-existing branch using checkout command, it will create new branch and switching onto it:

> git checkout -b new_branch

To checkout some commit, where 5939515 is commit sha:

> git checkout 5939515

#### Find the commit that broke something

**git bisect** is your friend. Very powerful command in git which helps a lot. Used to point two commits as an edge cases and then repass all commits history between this two points (and mark commit by commit if there was some specific fail). To use, first of all you should start to initialise with tool:

> git bisect start

Then we should mark two edge cases as bad and good points:

> git bisect bad
> git checkout commit
> git bisect good

Going through commits you can easily find bad commit, were possible introduced some error/bug.

#### Show who made changes to selected file

**git blame** command is used for this. The main purpose is ti show log of selected file, showing who and when made a changes to this file.

> git blame somefile.js

Will show a list of commit made to this file, authors, date and commit messages. Command can be used passing some keys like -e to show email address of authors in log, -L 1-7 to limit and display just 7 output lines. The main difference between **git blame** and **git log** is that blame can tell you who was the last person to modify each line of code and when.
