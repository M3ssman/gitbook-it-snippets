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
* Check Remote
  * `git config --get remote.origin.url` OR `git remote show origin`
  * reset:`git remote set-url origin <uri>.git`

### Branches

* new from current one: `git checkout -b development`
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

  * local:`git branch -d the_deleted_branch`
  * push:`git push origin :the_deleted_branch`

* copy files between branches
  `git checkout <des-branch>`
  `git checkout <src-branch> <file/package>`
  `git commit -m "added file/package from src to des"`

### Commits



