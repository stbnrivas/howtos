# configuration

```bash
sudo apt install git tig # Text-mode interface for the git revision control system
sudo dnf install git tig
```



```bash
git config --global user.name "stbn"
git config --global user.email "stbnrivas@gmail.com"
git config --global color.ui auto

git config --global core.editor "vim"

git config --global format.pretty oneline
git config --global core.pager 'less'

# git completion into ~/.bash_profile
updatedb
locate git-completion.bash
source /usr/share/doc/git-1.7.4.4/contrib/completion/git-completion.bash

# set diff tool and merge tool meld
git config --global diff.tool meld
git config --global difftool.meld.path "/usr/bin/meld"
git config --global difftool.meld.path "/usr/bin/tig"
git config --global difftool.prompt false

git config --global merge.conflictstyle diff3
```


## alias at file: .gitconfig

[alias]
  co = checkout
  ci = commit
  st = status
  br = branch
  hist = log --pretty=format:'%h %ad | %s%d [%an]' --graph --date=short
  hist = log --pretty=format:'%C(yellow)%h %C(cyan)%ad | %C(green)%s%d %C(blue)[%an]' --graph --date=short

  hist2 = log --pretty=format:"%C(yellow)%h %Cblue%>(12)%ad %Cgreen%<(7)%aN%Cred%d %Creset%s" --date=short

  hist2 = log --pretty=format:"%C(yellow)%h %Cblue%>(12)%ad %Cgreen%<(7)%aN%Cred%d %Creset%s" --date=short
  type = cat-file -t
  dump = cat-file -p





# inicialization repository

```bash
git init $repo
git init --bare $repo.git

git clone <url>
git clone --bare $repo $repo.git


git pull --allow-unrelated-histories
```


now you can: ignore file, add file, modify file, delete file, rename file, move file location

# ignore file

git has a .gitignore file to specify

# forcing ignore files which are .gitignore and it on track files

```bash
# If you wanna stop tracking changes to a file that's already tracked in the repository like .env .secrets
git update-index --assume-unchanged <file>
# If you wanna start tracking changes again
git update-index --no-assume-unchanged <file>

# also for folders
git update-index --skip-worktree <path-name>
```


# working at the repo

* show diff

```bash
git diff    # diff between current status and last commit
git diff --ignore-space-at-eol
git diff --cached # between add to stage and last commit
git diff --staged #

git difftool

# show files changes
git diff --name-status
git diff $file
# show diferences between branches
git diff mybranch master > file.diff
git diff mybranch master -- specific-file-to-see-diff.ext
```

* store changes into stage

```bash
git add -A # stages All
git add --all

git add .  # stages new and modified, without deleted
git add -u # stages modified and updated, without new
```

* delete file and stop tracking

```bash
git rm --cached <file>
```

* reset the working directory and stage to last commit, but unstaged all changes keeping untracked files

```bash


git reset --hard HEAD
```

* remove untracked files from the working tree

```bash
# CAUTION FILES REMOVE FOREVER
git clean -n  # to show what will be removed
git clean -f  # delete untracked files
git clean -fx # delete non-ignored files
git clean -fX # delete ignored files
git clean -d  # delete untracked directories


# RECOMMENDED
git clean -nfd  # simulate
git clean -fd   # do it
```

* undoing individual files to the last commit

```bash
  git checkout HEAD <file>
```

* unstage something undoing in the staging area

```bash
# unstage all
git reset

git reset HEAD <file> # unstage file
git checkout HEAD <file> to discard
```

* forgot something in that commit

```bash
  git reset --soft HEAD^   # undo last commit, put changes into stage

  git add <file>
  git commit --amend -m "Message"
```
* adding hunks of coden within of CLI

```bash
# Interactively choose hunks of patch between the index and the work tree and add them
# to the index. This gives the user a chance to review the difference before adding
# modified contents to the index.

# for all modified files
git add -p
git add --patch

# for specified file

git add $file -p
git add $file --patch


# y - stage this hunk
# n - do not stage this hunk
# q - quit; do not stage this hunk or any of the remaining ones
# a - stage this hunk and all later hunks in the file
# d - do not stage this hunk or any of the later hunks in the file
# g - select a hunk to go to
# / - search for a hunk matching the given regex
# j - leave this hunk undecided, see next undecided hunk
# J - leave this hunk undecided, see next hunk
# k - leave this hunk undecided, see previous undecided hunk
# K - leave this hunk undecided, see previous hunk
# s - split the current hunk into smaller hunks
#
# e - manually edit the current hunk
#
# ? - print help
```



* commit one command

```bash
git commit -a		# like git add . ; git commit
```

* saving your changes between branches

```bash
git add ...
git stash
git checkout branch_destination
git stash pop

git stash list
git stash apply --index 0
git stash apply --index 2
```

```bash
git stash
# now you can
git stash pop: unstash and merge stored changes.
# or apply without remove off stack of stashes
git stash apply
# also you later remove  with
git stash drop
# see last stash diff
git stash show -p
# see arbitrary stash diff
git stash show -p stash@{1}
# see changes with other branch
git diff stash@{0} master
```

stash single file

```bash
git stash push -m saving_only_this_file project/path/to/file.c
git stash pop
```







# checking the log of repo

```bash
git log
```

--pretty="..." defines the format of the output.
%h is the abbreviated hash of the commit
%d are any decorations on that commit (e.g. branch heads or tags)
%ad is the author date
%s is the comment
%an is the author name
--graph informs git to display the commit tree in an ASCII graph layout
--date=short keeps the date format nice and short


```bash
git log --graph
git log --oneline
git log --pretty=full
git log -4
git log --date=short
git log --decorate
git log --simplify-by-decoration

git log --pretty=format:"%C(yellow)%h %Cblue%>(12)%ad %Cgreen%<(7)%aN%Cred%d %Creset%s"

git reflog
git diff --ignore-space-at-eol: ignore spaces (workaround for Atom formatter).
git diff --cached: changes in files that you’ve already added.
git diff mybranch master -- file.ext: compare file between branches.
```

```bash
git log --grep $string
git log <since>..<until>
git log  git log --since="2019-08-15"
git log --since=$(date --date="15 day ago" +"%Y-%m-%d")
git log --stat
git log --author=stbnrivas
git show # show changes
```



# manipulating branches

* list branch

```bash
git branch
```

* delete branch

```bash
git branch -d <name> #only delete this branch if changes are merged
git branch -D <name> #to force deletetion with unmerged commit
```

* create new branch and jump to that

```bash
git branch testing ; git checkout testing
git checkout -b new_branch_name
```

* create new branch from another

```bash
git branch master <new-branch>
```

* change to branch:

```bash
git checkout branch_to_jump
```

* change to rigth branch and mixed branchs

```bash
git checkout master
git merge hotfixgit
git branch -d hotfix
```

* how see conflicts after merge operation

```bash
git diff --name-only --diff-filter=U

git mergetool
```



* if there is problem at merge
```bash
git status
```

* update branch with changes from master

```bash
git checkout <branch>
git rebase master
```

## rename branch

```bash
git checkout $old-name
git branch -m $new-name

git branch -m $old-name $new-name
```

## moving into same branch differents commits (detach mode)


```bash
git log
git branch <branch-name>

git checkout <commit> # this will enter into detach mode
git log               # commit after <commit> wont be shown
git reflog            # this will show lost commits (commit after <commit>)

git checkout <branch> #  this will exit from detach mode

```





## workflow merge branches using `git merge`

```bash
git checkout -b hotfix
# ... changes
git add ...
git commit
git checkout master
git merge hotfix

git merge --abort
git branch -d hotfix
```

```bash
git status # First normal step, as a double-check for files not added to the repo or unwanted changes
git checkout -b my_new_branch # Let's begin
git add file_1 file_2
git commit -a -m "Message" # If no long explanation is required, or ...
git commit -a # ... if a long comment is convenient (see later)
git fetch master
git rebase master # If it's safe or ...
git merge master # ... if it's not and
git push # If there's no history rewrite or ...
git push --force-with-lease # ... if it's not (see later)
```


## workflow merge branches with git rebase

when devs work in paralel it posible that you branch must be merged into another and newer head that exist into your repo, for than have git rebase

```bash
git checkout -b hotfix
#... changes
git add ...
git commit
git checkout master
git rebase hotfix  # apply all changes of hotfix branch to a master
```


## merge a specific commit

```bash
git ckeckout experimental
git log --graph
# commit id =

git checkout master

```


# remote and locals repos

change remote from http to ssh

````bash
git remote -v
origin  https://github.com/${OWNER}/${REPO_NAME} (fetch)
origin  https://github.com/${OWNER}/${REPO_NAME} (push)

git remote set-url origin git@github.com/${OWNER}/${REPO_NAME}.git
git remote -v
origin  git@github.com/${OWNER}/${REPO_NAME}.git (fetch)
origin  git@github.com/${OWNER}/${REPO_NAME}.git (push)


```




```bash
git branch -r   # show remotes branch
git branch -a   # show all branch

# download only one branch
git fetch origin <remote-branch>
git checkout <remote-branch>

git switch <remote-branch>

# download  all remote branches
git fetch --all
git checkout <remote-branch>

# download all changes without do merge
git fetch <remote> <branch>

# duplicate the remote branch into local
git branch --all
# master
# develop
# origin/remote_develop
git fetch origin remote_develop
git checkout -b remote_develop origin/remote_develop
git checkout -b other_name     origin/remote_develop


# download all changes and merge into local repo
git pull <remote> <branch>
git merge <remote> <branch>

# Set a new remote
git remote add origin https://github.com/user/repo.git

# Verify new remote
git remote -v
  origin  https://github.com/user/repo.git (fetch)
  origin  https://github.com/user/repo.git (push)

# put changes on repo with privileges

# check remotes available
git remote
--> origin
# check branch to upload
git branch
--> master
# upload changes
git push <remote> <branch>
git push origin master


# something wrong undo last commit in github
# you'll find the changes as uncommitted local modifications in your working copy.
git reset --soft HEAD~1

# something wrong undo last commit in github
# all changes will LOST FOREVER!!...
git reset --hard HEAD~1


git log
git reset --hard <SHA-1 last right commig>
git log

git push <remote> <branch> --force
git push -f <remote> <branch>

# or
git reset --soft HEAD~1

# get another remote branch to local
git fetch origin [remote-branch]:[new-local-branch]
```

```bash
git remote update --dry-run
git remote update --prune [--dry-run]
```

# pull a new remote branch

```bash
git fetch origin

git branch -a

#  local_one
#  local_two
#  master
#  remotes/origin/HEAD -> origin/master
#  remotes/origin/local_one
#  remotes/origin/local_two
#
#  remotes/origin/new_remote_branch_to_pull


git checkout -b new_remote_branch_to_pull origin/new_remote_branch_to_pull

git branch
#  master
#  local_one
#  local_two
#* new_remote_branch_to_pull
```




# creating and apply patches

```bash
git checkout fix-branch
# generate one patch for every commit
git format-patch  master
# generate single patch file for all commits
git format-patch master --stdout > branch_name.patch

# apply patch
git apply --stat filename.patch
# reverse apply patch
git apply -R  filename.patch
```


# download a pull request

```bash
git fetch origin pull/3344/head:pull_3344
```



# rewriting the history of the repo

there are several ways:

* amending commits
```bash
git add .
git commit --amend
```
* create new commit that reverse

```bash
git revert HEAD


git revert $SHA_1

git revert HEAD^2

git revert SHA-1
```

* removing commits from a branch (tag commit, reset before)
```bash
git checkout $commit
git tag $tag
git tag $tag -a   # If you want to include a description with your tag
git reset --hard $tag

git hist --all
```

```bash
git push origin --tags
```

* If we hadn’t tagged them, they would still be in the repository, but there would be no way to reference them other than using their hash names. Commits that are unreferenced remain in the repository until the system runs the garbage collection software.


* removing tags
```bash
git tag -d oops
git hist --all
```

once tag is removed that commit is not longe listed in the repo

```bash
# undo last commit the changes of last commit changes persist as stage
git reset --soft HEAD^

# undo last commit the changes of last commit are unstage
git reset --mixed HEAD^

# undo last commit the changes of lasta commit are lost completely
git reset --hard HEAD^
```

send tag to github
```bash
git tag -a v1.01 -m 'release 1 fix #12312'

git push origin --tags
```



# contribution (upstream)

```bash
git clone <url>
git checkout -b branch_some_feature
#... do some
git add ...
git commit
git push <remote> <branch_some_feature>
git request-pull origin/master
```

How to keep your fork update with its origin
error: This branch is X commits behind $USER:master

```bash
git remote add upstream git://github.com/ORIGINAL-DEV-USERNAME/REPO-YOU-FORKED-FROM.git
git fetch upstream

git pull upstream master
git push origin master
```

```bash
git remote add upstream git://gitlab.com/ORIGINAL-DEV-USERNAME/REPO-YOU-FORKED-FROM.git
git fetch upstream

git pull upstream master
git push origin master
```

and for gitlab




# nested repo with git submodule


```bash
  git submodule add https://github.com/twbs/bootstrap
  # to update
  cd submodule_repo
  git pull origin master
```

if a repos has multiples git submodules to download all

```bash
git clone $repo --recurse-submodules
```


# issues

1.  problem with \r\n and phantom changes...

```
git config --local core.autocrlf input
```

or

```
rm .gitatributtes
```





# working with Github

## configuration


* Imagine that now i have got a key for deployment server called id_rsa
* Or generate another id_rsa for github...

```bash
cd ~/.ssh
ssh-keygen -t rsa -C "your_email@youremail.com"

Generating public/private rsa key pair.
# Enter file in which to save the key (/home/you/.ssh/id_rsa): id_rsa_github
# Enter same passphrase again: [Type passphrase again]
# copy to clipboard id_rsa_github
xclip -sel clip < ~/.ssh/id_rsa.pub
# Add your SSH key to GitHub website

# test your that works
ssh -i ~/.ssh/id_rsa_github -T git@github.com
```

* configure ssh for use git with custom identify file id_rsa.pub
```bash
vi ~/home/.ssh/config

Host github.com
  Hostname github.com
  PreferredAuthentications publickey
  User git
  IdentityFile ~/.ssh/id_rsa_github

# to see
git remote show origin

# and change for this
git remote set-url origin git@github.com:my_user_name/my_repo.git
git remote set-url origin git@github.com:stbnrivas/sinatra-static-assets.git

# Pushes commits to your remote repo stored on GitHub
git push origin HEAD:master
```

## remove sensible data files

```bash
git filter-branch --force --index-filter "git rm --cached --ignore-unmatch ./FUCK-FILE" --prune-empty --tag-name-filter cat -- --all
```



### PROBLEMS

PROBLEMS

* sign_and_send_pubkey: signing failed for RSA  from agent: agent refused operation
```bash
chmod 600 ~/.ssh/id_rsa
```




* debug the configuration
```bash
ssh -vT git@github.com
```
* Bad owner or permissions on /home/serg/.ssh/config
fatal: The remote end hung up unexpectedly

```bash
cd ~/.ssh
chmod 600 *
```

* work with github without password needed for every repo

always check that you have cloned from url like "git@github.com:<Username>/<Project>.git" this way git can use ssh key. If it is asking you for a username and password, your origin remote is pointing at the https url rather than the ssh url. Change it to ssh. For example, a github project like Git will have https url

problematic url: https://github.com/<Username>/<Project>.git

use one like this: git@github.com:<Username>/<Project>.git

```bash
git remote set-url origin git@github.com:<Username>/<Project>.git
```


* mixin githup repo and local repo

```
cd repo
git remote add origin git@github.com:<Username>/<Project>.git
# ERROR
# There is no tracking information for the current branch. Please specify which branch you want to merge with. See git-pull(1) for details.
# EXPLANATION: remote:master:SHA-1 != local:master:SHA-1 point with:
git remote set-url origin git@github.com:<Username>/<Project>.git
git push origin master
# ERROR
# fatal: refusing to merge unrelated histories
git pull origin master --allow-unrelated-histories

# resolve conflicts

git push origin master


```


# working for Bitbucket


```bash
cd ~/.ssh
ssh-keygen -t rsa -C "your_email@youremail.com"

Generating public/private rsa key pair.
# Enter file in which to save the key (/home/you/.ssh/id_rsa): id_rsa_bitbucket
# Enter same passphrase again: [Type passphrase again]
# copy to clipboard id_rsa_bitbucket
xclip -sel clip < ~/.ssh/id_rsa_bitbucket.pub
# Add your SSH key to Bitbucket website

# test your that works
ssh -i ~/.ssh/id_rsa_bitbucket -T git@github.com
```


Return to the terminal window and verify your configuration by entering the following command.
ssh -T git@bitbucket.org

$ cat .git/config
[core]
  repositoryformatversion = 0
  filemode = true
  bare = false
  logallrefupdates = true
  ignorecase = true
[remote "origin"]
  fetch = +refs/heads/*:refs/remotes/origin/*
  url = https://newuserme@bitbucket.org/newuserme/bb101repo.git
[branch "master"]
  remote = origin
  merge = refs/heads/master

