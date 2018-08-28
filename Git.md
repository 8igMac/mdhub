Git
===
If you want to look up any command, there are good documentation on manual page and good example too.
```
$ man git command
```
# Reset
- From staging area to unstage
```
$ git reset 
```
- From commit to staging area
```
$ git reset --soft HEAD^
```
- Discard the entire commit (if you have branch on current commit, the content will be kept in the branch in stead of discard)
```
$ git reset --hard HEAD^
```

# Merging
1. Checkout to target branch
2. Merge desire branch (no fast forward merge)
```
$ git merge --no-ff topic_branch
```
