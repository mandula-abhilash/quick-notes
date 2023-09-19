### Git commands [refer](https://www.nobledesktop.com/learn/git/git-branches)

#### Create feature branch from develop

```
git checkout -b feature/new-branch develop

git commit -m "New feature: Label planning applications"

git push origin feature/user-labels
```


#### Rename branch name

```
git checkout old-branch

git branch -m new_branch

git push origin --delete old-branch

git push -u origin new-branch
```

#### Merge develop into master branch 

```
git checkout master

git merge develop  # develop -> master

git push origin master
```

#### Merge feature into develop branch 

```
git checkout develop

git merge feature  # feature -> develop

git push origin develop
```

#### Keep feature branch up to date by merging develop branch into feature

```
git checkout develop

git pull origin develop

git checkout feature

git merge develop

git push origin feature
```

#### Save temporary changes
```
git stash

git stash pop

```

#### Git commands with alternate ssh key

Use `GIT_SSH_COMMAND="ssh -i ~/.ssh/rdc_id_ed25519"` as prefix before each command (Git Bash) 

```
GIT_SSH_COMMAND="ssh -i ~/.ssh/rdc_id_ed25519" git clone git@github.com:realdreamchronicles/dreams.git

GIT_SSH_COMMAND="ssh -i ~/.ssh/rdc_id_ed25519" git pull origin main

GIT_SSH_COMMAND="ssh -i ~/.ssh/rdc_id_ed25519" git clone git@github.com:realdreamchronicles/dreams.git

GIT_SSH_COMMAND="ssh -i ~/.ssh/rdc_id_ed25519" git pull origin main

```
