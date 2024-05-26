## Git Hidden Folder (ls-la)

There is a hidden folder called `.git` which tells you that our project is a git repo 

If we want to create a git repo in a new project we' create the folder and initialize that repo using `git init`.

```sh
mkdir /workspace/tmp/new-project
cd /workspace/tmp/new-project
git init
touch Readme.md 
code Readme.md 
git status
git add Readme.md

# make changes to Readme.md
git commit -m "add readme file"
```

## Cloning 

3 ways to clone: HTTPs, SSH, Github CLI


```sh
mkdir /workspace/tmp
cd /workspace/tmp
```

### HTTPS (Public no need credentials to clone)
```sh
git clone https://github.com/Ben-Tay/GitHub-Examples.git
cd GitHub-Examples
```

## Commits
Commit code using git commit which will open up the commit edit message in the editor of choice 

```sh
git commit 

# Make commit without having to open editor
git commit -m "Add another exclamation"

```
Set the global commit editor (typically required for local machine for commit)

## Gitconfig file

Gitconfig file stores your global configuration for git such as email, name, editor and more 

Showing the contents of our .gitconfig file
```
git config --global core.editor emacs
git config --list --show-origin
```

When you first install Git on a machine you are suppose to set up your name and email

```sh
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com
```


## Branches


## Remotes


## Stashing


## Merging



## Add 
When we want to stage changes that will be included in the committed, 
We can use the . to add all possible files

```
git add Readme.md
git add .
``` 
## Reset
Reset allows you to move Staged changes to be unstaged
This is useful when you want to revert all files not to be committed 

```sh 
git add . 
git reset
```

## Status
Git status shows you what files will or will not be committed.

```
git status
```

## Log
`git log` will show recent commits to the git tree

## Push
When we want to push a repo to our remote origin (Github)

```
git push 
```