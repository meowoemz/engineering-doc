# GitHub Command
## Create New Branch
```
git checkout -b your_branch_name
```
## Push things to your branch
```
git add .
git commit -m "the note you want to show"
git push origin your_branch_name
```
## Merge other branch to your branch
Here is an example for merge develop to your branch, First go to develop branch
```
git checkout develop
git pull origin develop
```
Go back to your own branch
```
git checkout your_branch_name
git merge develop
```
Sometimes you will have conflicts, you can see the files that have conflicts on command line. Go to each file and resolve the conflicts
Then push the changes to your own branch
```
git add .
git commit -m "resolve conflict"
git push origin your_branch_name
```

