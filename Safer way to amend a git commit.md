---
title : Safer way to git commit amend
notetype : feed
date : 14-02-2023
---

When you amend a [[Public/Git]] commit, you will have to force push it to remote, which can cause you to overwrite someone's commit which was pushed in the meantime.

Using push flag `--force-with-lease` instead of `--force` will not allow you to force push your amended commit if it would overwrite a commit on the remote. You will get an error, pull the remote changes and just repeat the push command.

```
git commit --amend
git push --force-with-lease
```

You can go a step further and create a git alias 
```bash
git config --global alias.kindly "push --force-with-lease"
```

Which allows you to run `git kindly` next time you need to "kindly" force push things. 

-----

Status: #💡 

Part of [[Public/Git Runbooks]]
