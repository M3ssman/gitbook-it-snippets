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

### Tags

### Reverts

Re-checkout over local changed work copy  
`git checkout -- <project>/src/main/java/<path/to>.java`

Re-set hard \(remove any local changes and additions\) local working copy to latest repo version  
`git reset --hard origin/webcat-webgui          
 git reset --hard HEAD # latest commit of current branch          
 git reset --hard 61237694001ef1ef26e0c7d9e7c57e2f442cbeb6 # to a specific commit`

