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

## Github CLI
> Command Line interface to interact with Github Account
Allows performing common Github actions without leaving developer environment

Documentation: https://cli.github.com/manual/
#### Example CLI commands 
```sh
gh auth login
gh repo create github-examples --public
gh repo set-default #selects default repo to use in the current directory
gh issue create --title "Issue title" --body "Issue body"
gh pr review --comment -b "interesting"
gh label list
gh label create bug --description "Something isn't working" --color E99695

# Use generated PAT instead of default one in github
export GH_TOKEN = "PAT_token link"
 # Check if environment variable for token is set
 env | grep GH_

# Can Choose to clone via ssh/https
gh repo clone Ben-Tay/GitHub-Examples
```
#### Installation (CLI) installable on Windows/Linux/MacOs
```sh
# MacOs
brew install gh
# Install CLI for Codespaces via Features
"features": {
    "ghcr.io/devcontainers/features/github-cli:1": {}
}
```

## Commits (only the changes)
> Contains additions/modifications/deletions of files and its file contents but not the whole files themselves (reduces the file size)

> Commits represent incremental changes to a codebase represented with a git tree (graph at specific time) tagged with a SHA Hash ID used to checkout specific commits
```sh
git commit # commits without message will be opened in text editor of choice

# Commits staged changes with a message
git commit -m "Commit message"

# Automatically stages all tracked changes before the commit 
git commit -a -m "Commit message"

# Modifies most recent commit that is not yet pushed
git commit --amend

# Empty commit (for placeholder)
git commit -m "Initial commit" --allow-empty

# Commits with specified author
git commit -m "Message" --author="Author Name <email@example.com>"

# Checkout to specified commit based on SHA Hash
git checkout SHA-HASH
```
Set the global commit editor (typically required for local machine for commit)

Components of a Git Commit
> Hash (SHA-1), Author Info, Message, Timestamp of commit, Parent Commit (Hashes) and Snapshot of content (staged changes snapshot)
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

## Branches (Main vs Production)
> It is basically a divergence of the state of the repository, Can be seen as  copies at a point in time modified to be different

> Production: Push from main using some CI/CD tool. CI/CD systems gets triggered when tag is applied

Branches can be used for multiple purposes:
> Environments - staging/development/production

> Specific branches by developer name/bugs/features

```sh
# Lists all local branches
git branch
# Lists both remote & local branches
git branch -a
# creates a new branch
git branch [branchname]
# switch to a new branch
git checkout [branchname]
# creates and switches to that branch
git checkout -b [branchname]
# deletes a branch
git branch -d [branchname]
# renames a branch
git branch -m [oldname] [newname]
```

## Github Workflow
> Original Workflow
1. Clone/pull  from develop branch into feature branches
2. Any changes done in feature branches ready to be tested out will be merged back into develop branches 
3. Develop branches ready for testing would be pushed into CI/CD pipeline environment into staging/release branches (aka Deploy)
4. Test changes in production environment (deploy) and once changes are verified, merge them into the main/amaster branch
5. Any issues that arise from merging into main will be pulled from master branch into hotfixes (to fix them and remerge in)
> `NOTE THAT release branches are not common much these days, and people tend to push directly from development into master (production)`

> Push feature branch upstream to remote origin (if branch not yet in remote)
```sh
git add .
git commit -m 'mychanges'
git push -u origin [branchname]

# If done in forked repository, only affects fork, need to do pull request to upload to original repo
```

## Remotes
> Represents a reference to the remote location where a copy of your repository is hosted

> Can have multiple remote entries where `origin` is a remote name for a repo

> Remote names can be referenced,
remote stored in git/config file

We can add remote but often you will just add remote via upstream when adding a new branch

Remote Commands
```sh
# Lists all remote repositories with their URLs
git remote -v 
# Add a remote
git remote add [name] [URL]
# Remove remote
git remote remove [name]
# Rename a remote branch
git remote rename [old-name] [new-name]
# Pushes a branch and its commit to the specific remote
git push [remote-name] [branch]
git push origin main 
# Pulls updates from a remote branch (combination of git fetch + git merge)
git pull [remote-name] [branch]
# Retrieves changes from remote into current local branch but does not merge it into local branch
git fetch [remote-name] # Updates remote tracking branches in local development
```

## Remote Upstream & Downstream
Upstream  (Push request)
> Push changes from local development into remote repository
```
git branch -u origin new-feature
```
Downstream (Pull request)
> Clones/pulls from other repository into remote 

## Stashing (Local development)
When you wish to save your changes in a stash after adding (not directly committing)
```
git add .
git stash
git stash list # check stash list
git stash save my-name 
git stash apply 
git stash pop # remove from stash list
```

## Merging
> Takes the changes from the specified branch into the current branch and merges it
* Typically performed after a git fetch to integrate the fetched changes
```
git checkout dev
git merge main
```

## Add 
When we want to stage changes that will be included in the committed, 
We can use the . to add all possible files

```sh
git add Readme.md
git add .
git rm my-other file # remove a specific file
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
> Makes our local changes available to others in the cloud
```
git push [remote-name]
```



