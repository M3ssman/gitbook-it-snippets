## Dev Tools Git

### General

Install latest Version on Ubuntu \(not distro default, which might be pretty outdated\)

```
sudo apt-add-repository ppa:git-core/ppa
sudo apt-get update
sudo apt-get install git
```

Global Setup

```
git config --global user.email <mail>
git config --global user.name <name>
# read settings
git config -l
```

Repository clone local

```
git clone <uri> <optional-local-path>
```

* Informations about local Repository via bash State: `git log -<latest commits>` or `gitk`
* Add Remote to brand new local Repository  
  `git remote add origin <uri>.git`

* Check Remote

  * `git config --get remote.origin.url` OR `git remote show origin`
  * `git remote set-url origin <uri>.git`

* git log  
  `git log -3 # fetch 3 latest commits + message`

### Branches

* new from current one
  `git checkout -b development`
* create new master

* ```
  git checkout not_yet_master
  git merge -s ours master
  git checkout master
  git merge not_yet_master
  ```
* compare branches  
  `git diff master feature/<x>`

* rename  
  `git branch -m <newname> # if inside to rename branch                                  
   git branch -m <old-name> <new-name> # when not inside branch to rename`

* delete  
  `git branch -d the_deleted_branch # local repository                            
   git push origin :the_deleted_branch # push delete to remote origin`

* copy files between branches  
  `git checkout <des-branch>`  
  `git checkout <src-branch> <file/package>`  
  `git commit -m "added file/package from src to des"`

### Commits

* checkout file with version from a specific past commit
  `git checkout fb2bfd12aec34f6c77e6c236a359c5e35d802d54 <project>/src/main/java/<path/to>.java`
* pick a specific commit \(cherry-pick\)
  `git cherry-pick -x b18f616dbe410e590714f0e2c91ed1f4cb9ede34 # -x keep source branch name in commit message` 

### Tags

create  
`git tag -a v3.6.13 -m "first tag ref#39046 1min"`

push to origin  
`git push origin master --tags  # pushed all local tags                
 git push origin v2.0.4         # pushed only tag v2.0.4`

delete  
`git tag --delete v1.5.7 # delete local              
 git push origin :v1.5.7 # push delete action to origin`

### Reverts

Re-checkout over local changed work copy  
`git checkout -- <project>/src/main/java/<path/to>.java # reset specific file          
 git checkout -- . # try to re-checkout anything`

Re-set hard \(remove any local changes and additions\) local working copy to latest repo version  
`git reset --hard origin/webcat-webgui                            
 git reset --hard HEAD # latest commit of current branch                            
 git reset --hard 61237694001ef1ef26e0c7d9e7c57e2f442cbeb6 # to a specific commit`

amed stuff  
`git commit --amend # edit latest HEAD commit message` 

### Stash

`git stash pop # remove last stash from stack and returns it  
git stash list # list all stashed commits` 





