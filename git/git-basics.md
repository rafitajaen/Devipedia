# Git Basics

### Version control

Git is a version control software. It tracks and manages changes to files over time, and allow to:&#x20;

* Revisit earlier versions of the files.
* Compare changes between versions.
* Undo changes and rever previuos versions.
* Collaborate on share changes.
* Combine changes.

### Configuring Git User

<mark style="color:red;">`git config`</mark>` ```` `<mark style="color:orange;">`user.name`</mark> : Show actual user name.

<mark style="color:red;">`git config`</mark>` ```` `<mark style="color:orange;">`user.email`</mark> : Show actual user email.

<mark style="color:red;">`git config`</mark>` ```` `<mark style="color:purple;">`--global`</mark>` `<mark style="color:orange;">`user.name "UserName"`</mark> : Set user name.

<mark style="color:red;">`git config`</mark>` ```` `<mark style="color:purple;">`--global`</mark>` ```` `<mark style="color:orange;">`user.email "email@email.com"`</mark> : Set user email.

### Ignoring Files `.gitignore`

Files you never want to commit:

* Secrets, API Keys, credentials, etc.
* Operating System Files (.DS\_Store)
* Log files (because you can regenerate the easily)
* Dependencies & packages (you can import them whenever you want)

```bash
# You can prepend a pattern with a double asterisk to match directories anywhere in the repository.
**/logs

# An asterisk is a wildcard that matches zero or more characters.
*.log

# Appending a slash indicates the pattern is a directory. The entire contents of any directory in the repository matching that name – including all of its files and subdirectories – will be ignored
logs/
```

### First Commands

{% hint style="info" %}
A Git _"repo"_ is a workspace wich tracks and manage files within a folder.
{% endhint %}

#### Initialize a repository

<mark style="color:red;">`git init`</mark> : Initialize a get repo in the current directory.

#### Get information of a repository

<mark style="color:red;">`git status`</mark> : Gives info on the current status of a git repo and its content.

<mark style="color:red;">`git log`</mark> : A log of the commits for a given repo.

### Basic Git Workflow

![](../.gitbook/assets/basic-git-workflow.JPG)

{% hint style="info" %}
A _commit_ is a checkpoint in a repo. It takes a snapshot of your project in that moment.
{% endhint %}

<mark style="color:red;">`git add`</mark>` ```` `<mark style="color:orange;">`<file1> <file2>`</mark>` ``...` : Add file(s) to the staging area.

<mark style="color:red;">`git add .`</mark> : Add all changes to the staging area.

<mark style="color:red;">`git commit`</mark>` ```` `<mark style="color:purple;">`-m`</mark>` ```` `<mark style="color:orange;">`"A short message"`</mark> : Commit changes from the staging area.

{% hint style="success" %}
**TIP: Atomic Commits**

Try to keep each commit focused on a single thing (_feature, change, fix_). This makes it much easier to undo or rollback changes later on.

It also makes your project easier to be reviewed.
{% endhint %}

#### Discard changes in staging area

<mark style="color:red;">`git restore`</mark>` `<mark style="color:orange;">`<file>`</mark> : Discard changes in working directory

<mark style="color:red;">`git restore`</mark>` ```` `<mark style="color:purple;">`--staged`</mark>` ```` `<mark style="color:orange;">`<file>`</mark> : Unstage file(s)

<mark style="color:red;">`git rm`</mark>` ```` `<mark style="color:purple;">`-cached`</mark>` ```` `<mark style="color:orange;">`<file>`</mark> : Unstage file(s)

#### Amending Commits

```bash
# How to redo the previous commit

> git commit -m "a random message"
> git add forgotten_file
> git commit --amend
```

### Branches

The default branch name in Git is `master`. In GitHub is `main`.

HEAD is simply a pointer that refers to the current location in your repository. It points to the reference of the lastest commit you made in a branch.

#### Create branches

<mark style="color:red;">`git branch`</mark> : to view existing branches.

<mark style="color:red;">`git branch`</mark>` ```` `<mark style="color:orange;">`<name>`</mark> : Make a new branch based upon the current HEAD.

#### Switch between branches

<mark style="color:red;">`git switch`</mark>` ```` `<mark style="color:orange;">`<branch>`</mark> : Switch HEAD to a existing branch.

<mark style="color:red;">`git switch`</mark>` ```` `<mark style="color:purple;">`-c`</mark>` ```` `<mark style="color:orange;">`<new-branch>`</mark> : Create a new branch and switch it.

#### Switching branches with unstaged changes

If yours unstaged changes have conflicts with other branches, you only can:

* commit changes, or
* stash changes

Else, if yours unstaged changes don't have conflicts with other branches, you can switch branches and still preserve yours unstaged changes.

**Alternative commands for switch branches**

<mark style="color:red;">`git checkout`</mark>` ```` `<mark style="color:orange;">`<branch>`</mark> : (Old) Switch HEAD to a existing branch.

<mark style="color:red;">`git checkout`</mark>` ```` `<mark style="color:purple;">`-b`</mark>` ```` `<mark style="color:orange;">`<new-branch>`</mark> : (Old) Create a new branch and switch it.

#### Delete branches

{% hint style="danger" %}
HEAD cannot reference the branch you want to remove.
{% endhint %}

<mark style="color:red;">`git branch`</mark>` ```` `<mark style="color:purple;">`-d`</mark>` ```` `<mark style="color:orange;">`<branch>`</mark> : Only remove an existing branch if it is fully merged.

<mark style="color:red;">`git branch`</mark>` ```` `<mark style="color:purple;">`-D`</mark>` ```` `<mark style="color:orange;">`<branch>`</mark> : Force to delete an existing branch, even it is not fully merged.

#### Rename branches

<mark style="color:red;">`git branch`</mark>` ```` `<mark style="color:purple;">`-m`</mark>` ```` `<mark style="color:orange;">`<new-branch-name>`</mark> : Rename the current branch.

#### Merging branches

{% hint style="info" %}
We merge branches, not specific commits.
{% endhint %}

{% hint style="warning" %}
We always merge to the current HEAD branch.
{% endhint %}

```bash
# Fast Forward Merge the bugfix branch into master

> git switch master
> git merge bugfix
```
