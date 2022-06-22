---
description: Most used commands when working with the terminal
---

# Terminal Basics

### Navigation

#### List files and folders

<mark style="color:red;">`ls`</mark> : List the content of the current directory

<mark style="color:red;">`ls`</mark>` ```` `<mark style="color:orange;">`<folder/subfolder>`</mark> : List the content of a given folder

<mark style="color:red;">`ls`</mark>` ```` `<mark style="color:blue;">`-a`</mark> : Show hidden files and folders

#### Change Directory

<mark style="color:red;">`cd`</mark>` ```` `<mark style="color:orange;">`<folder>`</mark> : Change directory to folder

<mark style="color:red;">`cd ..`</mark> : Back up one directory

#### Misc

<mark style="color:red;">`clear`</mark> : clear terminal

<mark style="color:red;">`pwd`</mark> : Print working directory

<mark style="color:red;">`start .`</mark> : Open Explorer on current directory (Windows)

<mark style="color:red;">`start`</mark>` ```` `<mark style="color:orange;">`<folder>`</mark> : Open Explorer on folder (Windows)



{% hint style="info" %}
The meaning of `~` in your terminal is that your current directory is Home .
{% endhint %}

{% hint style="success" %}
TIP : You can press `TAB` to autocomplete the path.
{% endhint %}

### Working with files and folders

#### Create

<mark style="color:red;">`touch`</mark>` ```` `<mark style="color:orange;">`<file1> <file2>`</mark>` ``...`  : Create new file(s) in the current directory.

<mark style="color:red;">`touch`</mark>` ```` `<mark style="color:orange;">`<path1> <path2>`</mark>` ``...`  : Create new file(s) in the given path(s).

{% hint style="warning" %}
Touching an existing file just change the _modified time_ of a file.
{% endhint %}

<mark style="color:red;">`mkdir`</mark>` ```` `<mark style="color:orange;">`<folder1> <folder2>`</mark>` ``...` : Create new folder(s) in the current directory.

#### Remove

<mark style="color:red;">`rm`</mark>` ```` `<mark style="color:orange;">`<file1> <file2>`</mark>` ``...` : Delete file(s) from the current directory.

<mark style="color:red;">`rm`</mark>` ```` `<mark style="color:orange;">`<file-path1> <file-path2>`</mark>` ``...` : Delete file(s) from the given path(s).

<mark style="color:red;">`rm -rf`</mark>` ```` `<mark style="color:orange;">`<folder1> <folder2>`</mark>` ``...` : Delete folder(s) from the current directory.&#x20;

{% hint style="danger" %}
The delete actions **cannot** be undone.
{% endhint %}

