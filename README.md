anycore
=======

This contains the RTL for Anycore and associated simulation and synthesis framework for the latest RISCV based development of AnyCore

1. [Quickstart](#quickstart)
2. [Tour of The Sources](#tour)
3. [Commit Changes in Submodules](#commit-submodules)


# <a name="quickstart"></a>Quickstart

Check the version your git by using:

	% git --version

#####If your git version is above 1.7.9

	% git clone --recursive https://github.ncsu.edu/AnyCore/anycore-synth.git

#####If you are using git version before 1.7.9, you must specify your username for  ghttps://github.ncsu.edu

######Note: 
You can add the line "unsetenv SSH_ASKPASS"  in your ~/mycshrc or "unset SSH_ASKPASS"  in ~/.bashrc to preven git from popping up a graphical password prompt. This is useful if you are using terminal programs such as PuTTY.

######If using C-Shell:

	% set GIT_USER_NAME=<username>    
	% git clone https://`echo $GIT_USER_NAME`@github.ncsu.edu/AnyCore/anycore-synth.git
	% cd anycore-synth/
	% sed -i -- 's/github\.ncsu/'`echo $GIT_USER_NAME`'@github\.ncsu/g' .gitmodules 
	% git submodule update --init --recursive
	
######If using Bash:	

	$ export GIT_USER_NAME=<username>    
	$ git clone https://`echo $GIT_USER_NAME`@github.ncsu.edu/AnyCore/anycore-synth.git
	$ cd anycore-synth/
	$ sed -i -- 's/github\.ncsu/'`echo $GIT_USER_NAME`'@github\.ncsu/g' .gitmodules 
	$ git submodule update --init --recursive


#####WARNING:
If you just want to use the codebase to run tests, you are all set to move on to [Build The Tools.]#build-tools). However, if you think that you might need to modify code in any of the submodules and want to commit them back to upstream repo, read the section on [Committing Submodules](#commit-submodules) very carefully. You have been warned!


# <a name="commit-submodules"></a>Commit Changes in Submodules

When you clone a repo and recursively init all its submodules, each submodule remains
in a state called "Detached HEAD State". What this basically means is that the submodule
repo is "branchless". It does not track any local or remote branches. In this state, you 
can use everything in the repo, play around, modify and even commit your changes. What you
can't do however is push your commits to a remote as your HEAD is not tracking any branch.
There are at least two simple ways to get around this issue:

## Checkout a branch and then start modifying
	% cd <submodule_directory>
	% git checkout <branch_you_want_to_use>
	...
	..
	Make all modifications
	..
	% git add <Stuff you want to commit>
	% git commit -m"Made bunch of modifications"
	% git push
	% cd <parent repo>
	% git status        ## This will show you changes in the submodule
	% git add <submodule_directory>
	% git commit -m"Modified a submodule"
	% git push

## If you didn't checkout before modifying, create a new branch with your latest commit and merge

	% cd <submodule_directory>
	...
	..
	Make all modifications
	..
	% git add <Stuff you want to commit>
	% git commit -m"Made bunch of modifications"
	% git branch temp_commit_branch <##Commit hash>
	% git checkout <branch_you_want_to_actually_commit_to>
	% git merge temp_commit_branch <branch_you_want_to_actually_commit_to>
	% git push
	% cd <parent repo>
	% git status        ## This will show you changes in the submodule
	% git add <submodule_directory>
	% git commit -m"Modified a submodule"
	% git push


[Return to top.](#quickstart)
