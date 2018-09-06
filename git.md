Git
===

If you want to look up any command, there are good documentation on manual page and good example too.
```
$ man git command
```

# Begining a repository
1. Init git.
```
$ git init
```
2. User name and email setting locally, otherwise use global setting.
```
$ git config user.name "Mona Lisa"
```
```
$ git config user.email "xxx@gmail.com"
```
- note:
Use command `git config user.name` or `git config user.email` to check current config.
3. Add all files in the current dir form **working area** to **staging area**.
```
$ git add .
```
4. Commit: add all the files from **staging area** to **local repo**.
```
$ git commit -m "YOUR COMMIT MESSAGE"
```
5. Set up remote repo.
```
$ git remote add origin REMOTE_REPO_URL
```
- note:
Use command `git remote -v` to check current remote setting. (fetch: download, push: upload).
6. Add files from **local repo** to **remote repo**.
```
$ git push origin master
```

# Developing workflow
1. Before you start working, sync your **local repo** to the **remote repo**.
```
$ git pull origin master
```
2. Check git status
```
$ git status
```
3. Add file to **staging area**.
```
$ git add FILE_NAME
```
4. Commit
```
$ git commit -m "COMMIT MESSAGE"
```
5. Push to **remote repo**
```
$ git push origin master
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
1. Checkout to main branch
```
$ git chekcout main_branch
```
2. Merge topic branch into main branch (no fast forward merge)
```
$ git merge --no-ff topic_branch
```

# Handling a merge(pull) request
1. Fetch and check out the branch for this merge request
```
$ git fetch origin
$ git checkout -b target_branch origin/target_branch
```
2. Review the change locally
3. Merge the branch and fix any conflict that come up
```
$ git chekcout master
$ git merge --no-ff target_branch
```
4. Push the result of merge to remote repo
```
$ git push origin master
```

# Merge develop branch to master branch
On local, before sending merge(pull) request
1. Checkout to master
2. Create topic branch on master
3. Chekcout to develop 
4. Merge topic branch into develp and resolve conflict
5. Make sure unit test pass
6. Push develop branch to origin/develop
7. Send merge(pull) request on remote repo

# Squash two commit or edit old commit message
```
$ git rebase -i HEAD~3  # view last 3 commit
```
