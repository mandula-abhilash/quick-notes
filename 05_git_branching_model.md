# Git Branching model  [source](https://nvie.com/posts/a-successful-git-branching-model/)

<img src="https://user-images.githubusercontent.com/77572066/132303731-1d3ed70b-2ac9-4769-ac5c-1d4938361257.png" height="400"></img>
<!-- ![image](https://user-images.githubusercontent.com/77572066/132303731-1d3ed70b-2ac9-4769-ac5c-1d4938361257.png) -->

<br></br>

## The main branches
<img src="https://user-images.githubusercontent.com/77572066/132305656-657bcbac-ac99-4443-a0cb-8e9bfce7140e.png" height="300"></img>
<!-- ![image](https://user-images.githubusercontent.com/77572066/132305656-657bcbac-ac99-4443-a0cb-8e9bfce7140e.png) -->
- We consider *origin/master* to be the main branch where the source code of HEAD always reflects a production-ready state.
- We consider *origin/develop* to be the main branch where the source code of HEAD always reflects a state with the latest delivered development changes for the next release.

<br></br>

## Supporting branches
<img src="https://user-images.githubusercontent.com/77572066/132306587-8f45606b-a46a-4593-a466-90683bc85731.png" height="300"></img> 
<!-- ![image](https://user-images.githubusercontent.com/77572066/132305656-657bcbac-ac99-4443-a0cb-8e9bfce7140e.png) -->

### Feature branches

> - May branch off from :
>   - *develop*
> - Must merge back into :
>   - *develop*
> - Branch naming convention : 
>   - anything except master, develop, release-*, or hotfix-*
>   
> #### Creating a feature branch :
> When starting work on a new feature, branch off from the develop branch.
> ```
> $ git checkout -b myfeature develop
> Switched to a new branch 'myfeature'
> ```
> #### Incorporating a finished feature on develop :
> Finished features may be merged into the *develop* branch to definitely add them to the upcoming release.
> ```
> $ git checkout develop
> Switched to branch 'develop'
> 
> $ git merge --no-ff myfeature
> Updating ea1b82a..05e9557
> (Summary of changes)
>   
> $ git branch -d myfeature
> Deleted branch myfeature (was 05e9557).
> 
> $ git push origin develop
> ```
> _Note: The --no-ff flag causes the merge to always create a new commit object, even if the merge could be performed with a fast-forward. [refer](https://user-images.githubusercontent.com/77572066/132309596-7d02c187-f2cf-4574-9ac4-ec75305e3ddb.png)_

<br></br>
### Release branches

> - May branch off from :
>   - *develop*
> - Must merge back into :
>   - *develop and master*
> - Branch naming convention : 
>   - release-*
>   
> #### Creating a release branch :
> Release branches are created from the *develop* branch. 
> ```
> $ git checkout -b release-1.2 develop
> Switched to a new branch "release-1.2"
>
> $ git commit -a -m "Bumped version number to 1.2"
> [release-1.2 74d9424] Bumped version number to 1.2
> 1 files changed, 1 insertions(+), 1 deletions(-)
> ```
> #### Finishing a release branch :
> ```
> $ git checkout master
> Switched to branch 'master'
> 
> $ git merge --no-ff release-1.2
> Merge made by recursive.
> (Summary of changes)
>
> $ git tag -a 1.2
>   
> $ git checkout develop
> Switched to branch 'develop'
>
> $ git merge --no-ff release-1.2
> Merge made by recursive.
> (Summary of changes)
> 
> $ git branch -d release-1.2
> Deleted branch release-1.2 (was ff452fe).
> ```
> 

<br></br>
### Hotfix branches
Hotfix branches are very much like release branches in that they are also meant to prepare for a new production release, albeit unplanned.

> - May branch off from :
>   - *master*
> - Must merge back into :
>   - *develop and master*
> - Branch naming convention : 
>   - hotfix-*
>   
> #### Creating the hotfix branch :
> Hotfix branches are created from the master branch.
> ```
> $ git checkout -b hotfix-1.2.1 master
> Switched to a new branch "hotfix-1.2.1"
>
> $ git commit -a -m "Bumped version number to 1.2.1"
> [hotfix-1.2.1 41e61bb] Bumped version number to 1.2.1
> 1 files changed, 1 insertions(+), 1 deletions(-)
> ```
> Fix the bug and commit the fix in one or more separate commits.
> ```
> $ git commit -m "Fixed severe production problem"
> [hotfix-1.2.1 abbe5d6] Fixed severe production problem
> 5 files changed, 32 insertions(+), 17 deletions(-)
> ```
> #### Finishing a hotfix branch :
> ```
> $ git checkout master
> Switched to branch 'master'
> 
> $ git merge --no-ff hotfix-1.2.1
> Merge made by recursive.
> (Summary of changes)
>
> $ git tag -a 1.2.1
>   
> $ git checkout develop
> Switched to branch 'develop'
>
> $ git merge --no-ff hotfix-1.2.1
> Merge made by recursive.
> (Summary of changes)
> 
> $ git branch -d hotfix-1.2.1
> Deleted branch hotfix-1.2.1 (was abbe5d6).
> ```
> 

