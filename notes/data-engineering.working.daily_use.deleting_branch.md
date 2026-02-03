---
id: jn2ken3cr3mfdqyx32optt2
title: Deleting_branch
desc: ''
updated: 1769487330787
created: 1769487114573
---
- ## this is use for deleting branch skip master


```bush
git branch | Where-Object { $_ -notmatch "master" } | ForEach-Object { git branch -D $_.Trim() }

```