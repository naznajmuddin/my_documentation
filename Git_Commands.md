## Overview

These are notes on common Git commands used with GitHub and VS Code.

**1. Create a new `Pull Request (PR)`**

From `main/master/development` branch,
```
git checkout -b <your-branch-name>
```

Finish your code/changes,

```
git add .
git commit -s -m "<your-message>"
git push -u origin <your-branch-name> 
```

Realistic Example:
```
git checkout -b feat/add/branch
git add .
git commit -s -m "feat : add : new branches"
git push -u origin feat/add/branch
```

Then, go to your remote repository and click `New Pull Request`.

**2. To edit in the same commit:**

```
git reset --soft HEAD~1
git add . # this will push all your changes
git add <file-name> # specific changes to push
git commit --reuse-message=HEAD@{1}
git push -f <your-branch-name>
```

**3. To update the remote branch with remote main branch**

From your branch,

```
git fetch
git rebase origin/development
```
Alternative way:
```
git checkout <your-branch-name>
git merge origin/development
```

Push the updated code to the remote branch,

```
git push origin <your-branch-name>
```

**4. To update your local branch with remote branch**

From your branch,
```
git fetch
git status
git pull
```
Check if it is the `same commit` as remote branch,
```
git log
```

**5. Saving your changes to use later using `git stash`**

Tutorial: https://opensource.com/article/21/4/git-stash