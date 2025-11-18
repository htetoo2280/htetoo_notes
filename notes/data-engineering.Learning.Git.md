---
id: acjnq5fxl1e8j1cv6cresp8
title: Git_learning
desc: ''
updated: 1761276469432
created: 1747205099323
---

## Modified -> Staging -> Commited

- Modified - any modified
- Staging - git add .
- Commited - git commit -m "xxxx"

--------------------------------------

- checking commit git - git log --oneline


--------------------------------------

## commit

there are three types of commit , checkout commit , 
revert commit , reset commit

- git revert id (before)
- git reset id --hard (delete and go after)

-----------------

## reamrk
```bash
- git remote -v (where origin)
- git push origin --delete dev1 (delete branch from github)
- git stash (temp drop modified files)
- git stash --include-untracked (also untracked fiels)
```

## merge

```bash
- git checkout "branch_name" (to switch branch)
- git commit -m "comment" 

```

## branch deleting

- delete all branch skip master

```bush

git branch --merged master | ForEach-Object {
    $branch = $_.Trim()
    if ($branch -ne 'master' -and $branch -ne '* master') {
        git branch -d $branch
    }
}

```
