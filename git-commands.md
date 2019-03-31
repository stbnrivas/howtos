# configuration

```bash
git config --global user.name "stbn"
git config --global user.email "stbnrivas@gmail.com"
git config --global color.ui auto

git config --global format.pretty oneline
git config --global core.pager 'less'

# git completion into ~/.bash_profile
updatedb
locate git-completion.bash
source /usr/share/doc/git-1.7.4.4/contrib/completion/git-completion.bash
```


## alias at file: .gitconfig

[alias]
  co = checkout
  ci = commit
  st = status
  br = branch
  hist = log --pretty=format:'%h %ad | %s%d [%an]' --graph --date=short
  type = cat-file -t
  dump = cat-file -p




# inicialization repository

```bash
git init $repo
git init --bare $repo.git

git clone <url>
git clone --bare $repo $repo.git
```


now you can: add file, modify file, delete file, rename file, move file location



# working at the repo

* show diff 

```bash  
git diff    # diff between current status and last commit
git diff --cached # between add to stage and last commit
git diff --staged #
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
git clean -n # to show what will be removed
git clean -f # to remove untracked files
git clean -d # to remove untracked directories

git clean -fd # 
```

* undoing individual files to the last commit

```bash
  git checkout HEAD <file>
```

* unstage something undoing in the staging area

```bash
git reset HEAD <file> # unstage file
git checkout HEAD <file> to discard
```

* forgot something in that commit

```bash
  git reset --soft HEAD^   # undo last commit, put changes into stage

  git add <file>
  git commit --amend -m "Message"
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
```

```bash
git log --grep $string
git log <since>..<until>
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

* if there is problem at merge
```bash
git status
```

* update branch with changes from master

```bash
git checkout <branch>
git rebase master
```



## workflow merge branches with git merge

```bash
git checkout -b hotfix
# ... changes
git add ...
git commit 
git checkout master
git merge hotfix
git branch -d hotfix
```


## workflow merge branche with git rebase

when devs work in paralel it posible that you branch must be merged into another and newer head that exist into your repo, for than have git rebase

```bash
git checkout -b hotfix
#... changes
git add ...
git commit
git checkout master
git rebase hotfix  # apply all changes of hotfix branch to a master
```





# remote and locals repos 

```bash
# download all changes without do merge
git fetch <remote> <branch>
git merge <remote> <branch>

# download all changes and merge into local repo
git pull <remote> <branch> 

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



# creating and apply patches 

```bash
# generate patch file
git format--patch master --stdout > branch_name.patch

# apply patch
git apply --stat filename.patch
# reverse apply patch
git apply -R  filename.patch
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
```

* removing commits from a branch (tag commit, reset before)
```bash
  git checkout $commit
  git tag $tag
  git reset --hard $tag

  git hist --all 
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


# contribution 

```bash
git clone <url>
git checkout -b branch_some_feature
#... do some
git add ...
git commit
git push <remote> <branch_some_feature>
git request-pull origin/master
```

keep a fork up to date 
error: This branch is X commits behind $USER:master

```bash
git remote add upstream git://github.com/ORIGINAL-DEV-USERNAME/REPO-YOU-FORKED-FROM.git
git fetch upstream

git pull upstream master
git push origin master
```



# nested repo with git submodule


```bash
  git submodule add https://github.com/twbs/bootstrap
  # to update
  cd submodule_repo
  git pull origin master
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

### PROBLEMS

PROBLEMS

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

