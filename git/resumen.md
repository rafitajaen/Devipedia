# Resumen

### Git Configuration

#### **Set name and email** account

They will be attached to your commits and tags

```bash
git config --global user.name "Rafael"
git config --global user.email "you@example.com"
```

#### **Enable colorization** of Git output

```bash
git config --global color.ui auto
```

### Git Initialization

**Create new local repository**

* If **\[project name]** is provided, git will create a new directory and will initialize a repo inside it.
* If it is not provided, git will initialized in the current directory.

```bash
git init [project name]
```

#### Clone from remote repository

```bash
git clone [project url]
```

### Git Browse

#### List staged, unstaged and untracked files

```bash
git status
```

