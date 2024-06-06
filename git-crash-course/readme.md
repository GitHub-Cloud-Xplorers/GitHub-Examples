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
 
> Require a Personal Access Token (PAT)
when cloning from local development

1. Generate a PAT first:
https://github.com/settings/tokens?type=beta

2. Set the PAT permissions as follows (expiry time, permissions etc)
3. Use PAT as the pasword when you login

### SSH 
Cloning is possible if it is a public repository, else credentials are required 

```ssh
git clone git@github.com:Ben-Tay/GitHub-Examples.git
```
> Generating an ssh private/public key for pushing (Linux command)
```s
ssh-keygen -t rsa
## Save private key in a file (use full path)
github-alt_id_rsa.pub

## Enter passphrase (for more security but optional)

## Public key will be auto generated 
```
### Cat the file path to the public key (in linux) and add its contents to our github account
https://github.com/settings/keys

> For WSL users and if create non default key might need to add it 
```
ssh-add privatekeypath
eval `ssh-agent`

# Debug if authentication connection works (if ssh-add doesnt work)
ssh-T git@github.com 
```

### Github CLI
Install the CLI 

eg: Linux(Ubuntu)
https://cli.github.com/

```
gh auth login
gh repo clone Ben-Tay/GitHub-Examples

Can Choose to clone via ssh/https
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
List of branches
```
git branch 
```

Create a new branch

```
git branch branch-name
```

Checkout the branch (Switches to that branch)

```
git checkout dev
```

Pushing new branch to remote (needs to be done if remote does not have this branch yet)

```
git push -u origin dev

## If done in forked repository, only affects fork, need to do pull request to upload to original repo
```

## Remotes


## Stashing


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



