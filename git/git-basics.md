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

