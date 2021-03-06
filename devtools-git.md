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
git config --global --unset <property>
# create alias
git config --global alias.lg "log --graph --pretty=format:'%C(bold red)%H%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold yellow)<%an>%Creset' --abbrev-commit --date=relative"
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

* logs format  
  `git config --global format.pretty oneline`

* enhance log level for sh  
  `GIT_SSH_COMMAND="ssh -v" git clone <url>`

* merge-tool  
  `git config --global merge.tool WinMerge          
   git config --global diff.tool WinMerge`

### Read

`git fetch --tags # fetch all in local clone, even tags`

### Branches

* new branch development from current one
  `git checkout -b development`
* create new branch from commit  
  `git checkout -b old/stage 99fdf81bf44dc889ac4db283a909ec44d83ed04e`

* create new master

* ```
  git checkout not_yet_master
  git merge -s ours master
  git checkout master
  git merge not_yet_master
  ```
* compare branches  
  `git diff master feature/<x>`

* compare files between branches  
  `git diff release/vhk_rp master -- routes\vhk.ts    
   git difftool release/vhk_rp master -- routes\vhk.ts`

* rename  
  `git branch -m <newname> # if inside to rename branch                                                                          
   git branch -m <old-name> <new-name> # when not inside branch to rename`

* delete  
  `git branch -d the_deletedbranch # local repository                                                                    
   git push origin :thedeletedbranch # push delete to remote origin                                
   git push origin --delete thedeletedbranch # or like this                              
   git fetch origin --prune # remove local refs to branches that dont exists remote anymore`

* copy files between branches  
  `git checkout <des-branch>`  
  `git checkout <src-branch> <file/package>`  
  `git commit -m "added file/package from src to des"`

### Commits

* checkout file with version from a specific past commit
  `git checkout fb2bfd12aec34f6c77e6c236a359c5e35d802d54 <project>/src/main/java/<path/to>.java`
* pick a specific commit \(cherry-pick\)
  `git cherry-pick -x b18f616dbe410e590714f0e2c91ed1f4cb9ede34 # -x keep source branch name in commit message` 
* compare a file between 2 branches
  ```
  git diff release/vhk_rp master -- routes\vhk.ts
  git difftool release/vhk_rp master -- routes\vhk.ts
  ```

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

amend stuff  
`git commit --amend # edit latest HEAD commit message`

amend even all message back from specific commit \(argh!\)

```
git rebase -i <commit-hash>
git commit --amend --author="Uwe Hartwig <uwe.hartwig@bitsrc.info>"
git rebase --continue
```

revert to specific commit  
`git revert --strategy resolve 398c2c1826133c18deecdf16e3db9df2ff11bcc4`

### Stashes

`git stash # add current commit stage to stash`  
`git stash pop # remove last stash from stack and returns it                                          
 git stash list # list all stashed commits`

### Git-Hooks

* Location: &lt;folder&gt;.git/hooks
* rename desired one, prepare-commit-msg.sample =&gt; prepare-commit-msg
* check if executable 
* Prepare-commit-ms Hook for Gitlab - Pivotaltracker URL creation from \#\#123 ID at the end of commit message append below
  `PT_STORY_URL=$(cat ${1} | sed -rn 's/.*##([0-9]+)$/http:\/\/www.pivotaltracker.com\/story\/show\/\1/p')`
  ``echo "${PT_STORY_URL}" >> "$1"` ``

### Submodules

* clone with existing modules  
  `git clone --recursive <url>`

* add  
  `git submodule add git@<host>:<repo>.git localrepofolder`

* remove submodule in folder lib  
  `git submodule deinit lib`

* fetch changes from submodule

```
cd <submodul-folder>
git fetch
git merge origin/master
cd ..
git diff --submodule
 # list change-log
```

### Split Repositories

Split existing Git-Repository via subtree

```
git subtree split -P <folder> -b <new-folder-branch>
cd .. 
mkdir <new-repo> 
cd <new-repo> 
git init
git pull /absolute/path/to/old/repo <new-folder-branch>
mkdir <folder>
git mv <file-1 ... file-n> <folder>
git commit -m "merged <folder> and moved to subfolder"
```

afterwards, if desired paths are extracted, filter them from original repo  
`git filter-branch -f --tree-filter 'rm -rf <folder>' HEAD`

### Troubleshooting

* "Permissions 0777 for ' /etc/gitlab/ssh\_host\_ed25519\_key' are too open."
  Solution: `chmod 600 /home/me/.ssh/id_rsa_targethost` 



