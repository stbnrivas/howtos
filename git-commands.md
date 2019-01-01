###########################################################
# configuration
###########################################################

git config --global user.name "stbn"
git config --global user.email "stbnrivas@gmail.com"
git config --global color.ui auto

git config --global format.pretty oneline
git config --global core.pager 'less'


# git completion into ~/.bash_profile
updatedb
locate git-completion.bash
source /usr/share/doc/git-1.7.4.4/contrib/completion/git-completion.bash


# alias at file: .gitconfig

[alias]
  co = checkout
  ci = commit
  st = status
  br = branch
  hist = log --pretty=format:'%h %ad | %s%d [%an]' --graph --date=short
  type = cat-file -t
  dump = cat-file -p



###########################################################
# inicialization
###########################################################

  git init $repo
  git init --bare $repo.git

  git clone <url>
  git clone --bare $repo $repo.git


###########################################################
# adding, saving, undoing changes
###########################################################



# show diff 
  
  git diff		# diff between current status last commit
  git diff --cached	#
  git diff --staged	#

# store changes into stage

  git add -A # stages All
  git add --all

  git add .  # stages new and modified, without deleted
  git add -u # stages modified and updated, without new

# delete file and stop tracking

  git rm --cached <file>

# reset the working directory and stage to last commit, but unstaged all changes keeping untracked files

  git reset --hard HEAD 

# remove untracked files from the working tree
  
  git clean -n # to show what will be removed
  git clean -f # to remove untracked files
  git clean -d # to remove untracked directories
  
  git clean -fd # 

# undoing individual files to the last commit

  git checkout HEAD <file>

# unstage something undoing in the staging area

  git reset HEAD <file> # unstage file
  git checkout HEAD <file> to discard

# forgot something in that commit

  git reset --soft HEAD^   # undo last commit, put changes into stage

  git add <file>
  git commit --amend -m "Message"

# commit one command

  git commit -a		# like git add . ; git commit

###########################################################
# moving stash between branches
###########################################################

  git add ...
  git stash
  git checkout branch_dest
  git stash pop

  git stash list
  git stash apply --index 0
  git stash apply --index 2

###########################################################
#   log
###########################################################

git log --graph
git log --pretty=oneline
git log --pretty=full


    --pretty="..." defines the format of the output.
    %h is the abbreviated hash of the commit
    %d are any decorations on that commit (e.g. branch heads or tags)
    %ad is the author date
    %s is the comment
    %an is the author name
    --graph informs git to display the commit tree in an ASCII graph layout
    --date=short keeps the date format nice and short


###########################################################
#   manipulating branches
###########################################################
# list branch

  git branch

# delete branch

  git branch -d <name> #only delete this branch if changes are merged
  git branch -D <name> #to force deletetion with unmerged commit

# create new branch and jump to that

  git branch testing ; git checkout testing
  git checkout -b new_branch_name

# create new branch from another

  git branch master <new-branch>

# change to branch:

  git checkout branch_to_jump

# change to rigth branch and mixed branchs

  git checkout master
  git merge hotfixgit
  git branch -d hotfix

# if there is problem at merge

  git status


# delete all un-stages changes

  $ git clean -df

# delete all stages changes

  $ git checkout

# remove file from stage

###########################################################
#   Get changes from master into branch in Git
###########################################################
Check out the aq branch, and rebase from master.

$ git checkout aq
$ git rebase master



###########################################################
# workflow merge branches with git merge
###########################################################

  git checkout -b hotfix
  ... changes
  git add ...
  git commit 
  git checkout master
  git merge hotfix
  git branch -d hotfix


###########################################################
# workflow merge branche with git rebase
###########################################################
when devs work in paralel it posible that you branch must be merged into another
and newer head that exist into your repo, for than have git rebase

  git checkout -b hotfix
  ... changes
  git add ...
  git commit
  git checkout master
  git rebase hotfix  # apply all changes of hotfix branch to a master



###########################################################
# remote and locals repos 
###########################################################

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


  # get another remote branch to local
  git fetch origin [remote-branch]:[new-local-branch]


###########################################################
# creating and apply patches 
###########################################################

  # generate patch file
  git format--patch master --stdout > branch_name.patch

  # apply patch
  git apply --stat filename.patch
  # reverse apply patch
  git apply -R  filename.patch



###########################################################
# history of repo
###########################################################

  git log <since>..<until>
  git log --stat

  git show # show changes

###########################################################
# undo history of repo
###########################################################

  there are several ways:

  - amending commits

   

  - create new commit that reverse
  git revert HEAD


  - removing commits from a branch (tag commit, reset before)
  git checkout $commit
  git tag $tag
  git reset --hard $tag

  git hist --all 

If we hadn’t tagged them, they would still be in the repository, but there would be no way to reference them other than using their hash names. Commits that are unreferenced remain in the repository until the system runs the garbage collection software.


  -removing tags

  git tag -d oops
  git hist --all

once tag is removed that commit is not longe listed in the repo


###########################################################
# contribution 
###########################################################

  git clone <url>
  git checkout -b branch_some_feature
  ... do some
  git add ...
  git commit
  git push <remote> <branch_some_feature>
  git request-pull origin/master
  




###########################################################
# nested repo with git submodule
###########################################################


  git submodule add https://github.com/twbs/bootstrap

  # to update

  git pull origin master



###########################################################
# work with github without password needed for every repo
###########################################################

If it is asking you for a username and password, your origin remote is pointing at the https url rather than the ssh url. Change it to ssh. For example, a github project like Git will have https url

https://github.com/<Username>/<Project>.git

and the ssh one:

git@github.com:<Username>/<Project>.git

You can do:

git remote set-url origin git@github.com:<Username>/<Project>.git











///////////////////////////////////////////////
// configuration for github...
///////////////////////////////////////////////

#Imagine that now i have got a key for deployment server called id_rsa

#Generate another id_rsa for github...
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


#configure ssh for use git with custom identify file id_rsa.pub

# ~/home/.ssh/config
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

PROBLEMS

# debug
ssh -vT git@github.com

#
Initialized empty Git repository in /home/serg/projects/GameServer/.git/
Bad owner or permissions on /home/serg/.ssh/config
fatal: The remote end hung up unexpectedly

$ cd ~/.ssh
$ chmod 600 *

#
error: src refspec head does not match any.
error: failed to push some refs to 'git@github.com:stbnrivas/sinatra-static-assets.git'




# if you already have your SSH keys set up and are still getting the password prompt, make sure your repo URL is in the form

  git+ssh://git@github.com/username/reponame.git

as opposed to

https://github.com/username/reponame.git

To see your repo URL, run:

  git remote show origin

You can change the URL with git remote set-url like so:

  git remote set-url origin git+ssh://git@github.com/username/reponame.git



//////////////////////////////////////////////////////7
configuration for Bitbucket
//////////////////////////////////////////////////////7

ssh-keygen

  -- id_rsa_bitbucket
  -- enter paraphrase


restart bash


xclip -sel clip < ~/.ssh/id_rsa_bitbucket.pub


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






//////////////////////////////////////////////////////
create a public repo into github
//////////////////////////////////////////////////////

create repo into github


echo "# testing-orm" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/stbnrivas/testing-orm.git
git push -u origin master


