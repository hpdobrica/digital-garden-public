---
title : Git Cherry Pit
notetype : feed
date : 18-12-2021
---

To completely delete a commit from a [[Git]] branch you can use the following command:

```bash

CURRENT_OS=$(uname -s)


if [ "$CURRENT_OS" = "Linux" ]; then
  git rebase --rebase-merges --onto $1^ $1
fi

if [ "$CURRENT_OS" = "Darwin" ]; then
  git rebase --rebase-merges --onto $1~ $1
fi



```

The `$1` in the above command would be the commit sha of the commit you want to remove. Packing this into a zfunc named `git-cherry-pit`, you'd use it like so:

```bash

git-cherry-pit 8b5515fdf49feea83ad6fe9c0ad4a9e81abe9f86

```

-----

Status: #🌲 

