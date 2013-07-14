git-cheat-sheet
===============

A cheat sheet of useful git commands.

## Assumptions

This cheat sheet assumes that:

1. You are using GitHub. Because GitHub is **awesome**.
1. You are working with the command line. Because the command line is the only way to fly.

## Install git
A list of Git clients can be found here http://git-scm.com/downloads, but below are some common install methods.

### Mac 
The GitHub for Mac can be found here http://mac.github.com/

The command line tools can be added from the Preferences menu after installation.

### Windows
The GitHub for Windows client includes a copy of the git commandline tool and can be found here http://windows.github.com/

### Linux

If you're using the `apt` package manager that is common to Debian-based distributions such as Ubuntu:

	apt-get install git

If you're using the `yum` package manager that is common to Red Hat-based distributions such as Fedora:

	yum install git-core

## Configure git

	git config --global user.name {your-name}

	git config --global user.email {the-email-address-you-use-for-github}

These commands are part of what's called *identifying yourself*. They tell git who you are so that git and GitHub can tell what modifications were made by you.

## Make a copy of a repository on your local machine

	git clone https://github.com/{your-github-handle}/{repository-you-want-to-work-on}.git

This command is called *cloning a repository*. It will make a copy of the specified repository to your local machine. You need to clone a repository before you can start working on that repository and do cool things.

## Link your fork to the original repository that you have forked

	git remote add upstream https://github.com/{someone-else's-github-handle}/{repository-that-you-have-forked}.git

This command is called *adding the upstream remote*. It will allow you to keep your fork up to date with all the cool things other people have contributed to the original repository using *fetch and merge from upstream*.

## Find out where you are

	git status

This command is called *finding out where you are*. It will tell you which branch you're currently on and what changes you have made that haven't been recorded.

Before you start working on anything, you want this command to reply:

	# On branch master
	nothing to commit (working directory clean)

After you have made some changes, you want this command to reply:

	# On branch {the-branch-you-are-working-on}
	# Changes not staged for commit:
	#   (use "git add/rm <file>..." to update what will be committed)
	#   (use "git checkout -- <file>..." to discard changes in working directory)
	#
	#	modified:   {a-file-you-have-modified}
	#	added:		{a-file-you-added}
	#	deleted:	{a-file-you-deleted}
	#
	no changes added to commit (use "git add/rm" and/or "git commit -a")

## Update your local copy of the repository with all the changes from the original repository that you have forked

	git fetch upstream && git merge upstream/master

This command is called *fetching and merging from upstream* and depends on *adding the upstream remote*. It gets all the changes that other people have contributed to the original repository since you last updated your local copy.

You will want to run this command anytime you're about to start working on something. This will ensure that you're working from the latest code and eliminate problems down the road.

## Create a branch for you to do cool things safely

	git checkout -b {a-descriptive-name-for-what-you-will-work-on}

This command is called *branching a safety net*. It will create a workspace for you to do cool things in without any risk of [fecking up](http://www.urbandictionary.com/define.php?term=feck) anything.

After *branching a safety net*, *finding out where you are* should return:

	# On branch {a-descriptive-name-for-what-you-will-work-on}
	nothing to commit (working directory clean)

At this point, you can start making changes. Once you're done making your changes, *find out where you are* again.

## Tell git which files contain the cool things you did

	git add {file-you-added-or-changed}

	git rm {file-you-deleted}

These commands is part of what's called *staging for commit*. They will tell `git` which files it needs to update with your changes. For each file you added or modified, use `git add`; for each file you deleted, use 'git rm`.

After *staging changes for commit*, you should *find out where you are* to make sure all the changes you want to record are staged. You want the command to reply:

	# On branch {the-branch-you-are-working-on}
	# Changes to be committed:
	#   (use "git reset HEAD <file>..." to unstage)
	#
	#	modified:   {a-file-you-have-modified}
	#	added:		{a-file-you-added}
	#	deleted:	{a-file-you-deleted}
	#

## Tell git to record the cool things you did

	git commit -m "{description-of-the-changes-you-are-committing}"

This command is called *committing a change*. It tells `git` to record all the changes you made to the files you specified with *staging for commit* so that you don't lose the cool things you did.

## Make sure you have all the latest changes

	git checkout master
	
	git fetch upstream && git merge upstream/master

	git checkout {the-branch-you-are-working-on}

	git rebase master

These commands are part of what is called *rebasing from master*. They update your branch with all the changes that have been made to the master branch since you created your branch. This helps avoid complications when you submit a pull request to bring your changes into the master branch of the original repository that you have forked.

## Tell the world about the cool things you did

	git push origin {the-branch-you-are-working-on}

This command is called *pushing your changes*. It takes all the changes you committed using *committing a change* and records them on GitHub for the world to see.

## Clean up when you're done

	git branch -D {the-branch-you-no-longer-need}

	git push origin --delete {the-branch-you-no-longer-need}

These commands are part of what is called *cleaning up*. The first one deletes your branch locally, the second one deletes your branch on GitHub.

Make sure you really are done with your branch before deleting it though.
