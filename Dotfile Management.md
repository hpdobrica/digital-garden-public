---
title : Dotfile Management
notetype : feed
date : 18-12-2021
---

I switch machines i work on often, and its important to me that my configuration is up-to-date on all of them.

I needed a solution which would address the following topics:
- dotfiles should be backed up in one place which will be the source of truth
- i should be able to easily make changes to this source of truth from any machine
- all my machines should be able to easily sync with this source of truth

In short, I should be able to use one machine for days, make config changes on it, and then when i move to another machine, all of my config changes should be applied to the other machine as well.

To accomplish this, I found a pretty nice solution using a [[Bare Git Repository]].

## Initial setup

Lets create a new [[Git]] repo to store our config:

```bash

git init --bare $HOME/.cfg

```

To control the repo neatly with a dedicated command, we can create a `config` alias like so:

```bash

# make sure to save it to wherever you keep your aliases, e.g. `.zshrc`
alias config='/usr/bin/git --git-dir=$HOME/.cfg/ --work-tree=$HOME'

```

Notice that even though repository is in `.cfg`, the work tree is your home directory. This allows us to add any files in your home directory to this repository. Test the alias and set up the repository by configuring it to only track the files we've explicitly added:

```bash

# instead of git config
config config --local status.showUntrackedFiles no

```

The last step is to add your config files and push them:

```bash

config add .zshrc
config add .config/nvim/init.vim
# ...
# add anything else you are using
# ...
config commit -m 'add initial configuration'
config push


```

## Setup once repo exists

Every other time you are setting up (e.g. on a new machine), your repository will already exist, so the procedure is somewhat different:

```bash

git clone --bare $YOUR_GIT_REPO $HOME/.cfg

# make sure to save it to wherever you keep your aliases, e.g. `.zshrc`
alias config='/usr/bin/git --git-dir=$HOME/.cfg/ --work-tree=$HOME'


```

Now that config command is ready and repo is cloned, you can execute `config checkout` to get your config files. 

There might be trouble with conflicts if you already have some config files on your machine. Its best you back them up and then do a reconciliation to see if what you currently have needs to go into your main configuration. 

A neat script to automatically back up your current files if they are conflicting:

```bash

BACKUP_DIR="~/.config-backup"

if config checkout; then  
	echo "No conflicts, checkout succesful.";  
else  
	echo "Backing up pre-existing config files to $BACKUP_DIR";  
	mkdir $BACKUP_DIR 
	config checkout 2>&1 | egrep "\s+\." | awk {'print $1'} | xargs -I{} mv {} $BACKUP_DIR/{}  
	echo "Repeating checkout now that pre-existing files are moved."
	config checkout
fi



```

The only thing left to do now is to disable showing untracked files (just like we did before), and reconcile your conflicting configuration. Make the changes to your main files based on what you have in your `.config-backup` directory, execute a `config add / config commit / config push` of the changes (if any) and you are good to go!

Just dont forget to do `config pull` on your other machines to sync back your changes.

-----

Status: #🌲 

References:
- https://www.atlassian.com/git/tutorials/dotfiles
