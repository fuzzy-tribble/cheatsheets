# Git Cheatsheet

## Conventions / Notes

* **[Git Sandbox for Learning/Experimenting](https://learngitbranching.js.org/)**

* `origin` is a shorthand name for the *remote repository* that a project was originally cloned from; original remote reference

* `master` is a shortand name for the *main branch*

* `HEAD` is the *pointer to the current branch reference* (which is in turn a pointer to the last commit made on that branch); is the symbolic name for the currently checked out commit (essentially what commit you're working on top of).

* `index` is the *staging area*; where you place files to be committed; staged files are said to be in the "index"

* **Relative Refs:** 
(`^` and `~`) refers to parent. For example when traversing the git tree (eg `git reset HEAD^` or `git reset HEAD^^` or `git reset HEAD~2`, etc) will take you to parents, grandparents, etc; number of times to move upwards

* **Branches:** 
are just *pointers to specific commits*; `master` is created by default; `stable` is another common one; "branch early, branch often"

## Setup and Configs

| Command | Description |
| ------- | ----------- |
| `git config --list` | List all configs (add `--global` for global configs) |
| `git config user.email “[email]”` | Configure local user email |
| `git config user.email` | Show config user email |
---

## Setup and Init

| Command | Description |
| ------- | ----------- |
| `git init` | Initialize a local Git repository |
| `git clone [url]` | Create a local copy of a remote repository |
| **Forking** | Use GitHub interface; copies someone else's repo to your dev accnt so you can then clone and work on it |
---

## Stage and Snapshot

| Command | Description |
| ------- | ----------- |
| `git add [file]` | Stage a file; add to staging area |
| `git commit -m "[msg]"` | Commit/snapshot staged changes |
| `git reset [file]` | Unstage (while retaining the changes in working directory) |
| `git reset HEAD~` | Undo last commit |
---

***Types of Reset**: Three types of resets all of which reset HEAD to specified state: `--soft` resets `HEAD` to `[commit]` but does not touch the index file or the working tree; `--mixed` (default) resets index, not working tree; `--hard` resets index and working tree.*

***Reverting vs. Reseting**: The `git reset` command will move a branch backwards as if the commit had never been made in the first place. Resetting works great for local branches on your own machine however to get the change to show up on remote you would need to use `git push --force origin master` (force replaces remote history with your local history). Generally its better to use `git revert` however which will reverse changes and share the reversed changes remotely.*

## Inspecting and Comparing

| Command | Description |
| ------- | ----------- |
| `git log --graph --all` | Show commit log graphically; use `--branches` to show specific branches; use `-n 3` to show last three commit messages |
| `git status` | Check working tree status |
| `git diff` | Detailed `git status`; Diff of what is changed but not staged |
| `git diff --staged` | Diff of what is staged but not yet commited |
| `git diff [source branch] [target branch]` | Preview changes bt branched before merging |
---

## Moving Around The Git Tree
| Command | Description |
| ------- | ----------- |
| `git branch -f master HEAD~3` | Branch forcing; move branches around; moves (by force) the master branch ref to three parents behind HEAD |
| `git checkout [commit-hash]` | Move around the git tree using commit hashes (or any valid ref) |
| `git checkout HEAD~3`<br>`git checkout HEAD^^^` | Move around the git tree using relative refs |
---

## Undoing and Rewriting History
| Command | Description |
| ------- | ----------- |
| `git revert [commit-hash]` | Revert the commit hash (or any valid ref); safe undo |
| `git reset --soft HEAD^` | Moves HEAD one commit back |
| `git reset HEAD^` <br> `git reset --mixed HEAD^` | Undo last commit; unsafe/rewrites history; doesn't change working dir |
| `git reset --hard` | Undo last commit; unsafe/rewrites history; changes working dir |
| `git commit --amend -m "an updated commit message"` | Ammend commit message; most recent commit |
| `git push --force [remote] [branch]` or `git push --force-with-lease [remote] [branch]` | `--force` rewrites remote banch with local branch; `--force with lease` rewrites remote with local safely? |
---

## Branching

| Command | Description |
| ------- | ----------- |
| `git branch -a` | List branches (asterisk denotes current; `-a` for local and remote |
| `git [branch name]` | Create a new branch |
| `git checkout -b [branch name]` | Create a new branch and switch to it (`-b`) |
| `git branch -d [branch name]` | Delete a branch |
| `git push origin --delete [branch name]` | Delete a remote branch |
| `git stash` | Stash changes in a dirty working directory |
| `git stash list` | List stack-order of stashed file changes |
| `git stash pop` | Write working from top of stash stack |
| `git stash drop` | Discard the changes from top of stash stack |
| `git stash clear` | Remove all stashed entries |
---

## Merging / Combining Work

| Command | Description |
| ------- | ----------- |
| `git merge [feature]` | Merge a branch (eg. feature) into the active branch (eg. master) |
| `git merge [source branch] [target branch]` | Merge a branch into a target branch (target branch will default to active branch if not specified) |
| `git rebase [base]` | Rebases the current branch onto base |
| `git rebase -i` | Run rebase interactively to select specific commits, etc |
| `git cherry-pick [commit-hash]` | Pick specific commit(s) to apply to a branch |
---

***Merging vs Rebasing**: Merging is non-destructive bc existing branches are not changed. Instead, it creates a special commit that has two unique parents; rebasing takes a set of commits, "copies" them, and plops them down somewhere else..(nice b/c it gives you a nice linear sequence of commits).*

## Sharing & Updating Projects

| Command | Description |
| ------- | ----------- |
| `git push origin [branch name]` | Push a branch to your remote repository |
| `git push -u origin [branch name]` | Push changes to remote repository (and remember the branch) |
| `git push` | Push to remote repository (remembered branch) |
| `git config --local credential.helper ""` | To push as another user run this first and it will prompt you for username and password |
| `git push origin --delete [branch name]` | Delete a remote branch |
| `git fetch [remote] [branch]` | Download object and refs from repo |
| `git pull [remote] [branch]` | Pull changes from remote branch (`git fetch` + `git merge`) |
| `git remote add origin [url]` | Add a remote repository |
| `git remote set-url origin [url]` | Set a repository's origin branch |
---

***Making a Pull Request vs `git pull`**: Using the `git pull` command you are pulling changes from remote to your local; making a "pull request" is requesting another repo's maintainers to pull your changes into their repo.*

## Misc (tagging, describe, etc)
| Command | Description |
| ------- | ----------- |
| `git tag` | List tags |
| `git tag [tag name]` | Create tag  |
| `git describe` | TODO |
---

********************************************

# Common Workflows

## Contribute to existing repo

*Assumption: You have ownership of the repo or are listed as a contributor*

```bash
# clone repo
git clone [url]
cd repo

# create new branch; switch to it
git branch my-branch
git checkout my-branch

# make and commit changes
git add [files]
git commit -m "detailed snapshot msg"

# push changes to github
git push --set-upstream origin my-branch
```

## Start a new repository and publish it to GitHub

```bash
# init new repo; cd into it
git init my-repo
cd my-repo

# create file; add it; commit it
touch README.md
git add README.md
git commit -m "add README to initial commit"

# add the 'origin' ref url
git remote add origin [url]

# push changes to github
# use --set-upstream to set default push remote and branch
git push origin master
```

## Start a project based off of someone else's project / Contribute to someone else's project

```bash
# fork the project
git clone [url]

# make changes; stage; commit; push
# consider making your changes in a branch if 
# you plan to make a pull request later
git add .
git commit -m "my changes"
git push origin master

# (OPTIONAL) keep up with original project changes
# ie. keep your git fork up to date

# add upstread ref
git remote add upstream [original url you forked from]

# make sure your see the origin (yours) and upstream (forked/theirs)
git remote -v

# keep upstream updated (pull, fetch/merge, or rebase...you choose)
# git pull upstream

# git fetch upstream
# git merge upstream/master master

git rebase upstream/master

# (OPTIONAL) make a pull request (req they pull in your work)
# Click the Compare & pull request button
# Click Create pull request to open a new pull request
```

## Contribute to an existing branch on GitHub

*Assumption: a project called `repo` already exists in local working dir; a new branch has been pushed to GitHub since the last time changes were made locally*

```bash
# change into the `repo` directory; update all remote branches
cd repo
git pull

# change into branch of interest
git checkout [branch of interest]

# make changes; stage; commit/snapshot; push
git add .
git commit -m [commit message]
git push
```

### Inspect Work from Prev Commits/Snapshots

```bash
# figure out what commit you want to get back to
git log --graph -n 5

# checkout that commit
git checkout [commit-hash]
```

### Merge two branches into one sequential commit history

*Assumption: Two branches: `bugFix`, `master`; We would like to move our work from `bugFix` directly onto the work from `master`. That way it would look like these two features were developed sequentially, when in reality they were developed in parallel.*

```bash
# OPTION-1
git checkout bugFix   # make bugifx active
git rebase master     # rebase active (bugFix) onto master 
git checkout master   # make master active
git rebase bugFix     # move master ref up to bugFix

# OPTION-2 (same outcome as option-1 but shorter)
git rebase master bugFix   # rb bugFix onto master
git rebase bugFix master   # rb master onto bugFix (move ref up)
```