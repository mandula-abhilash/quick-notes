### Git commands

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
