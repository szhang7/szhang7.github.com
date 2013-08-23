---
layout: post
title: "Git Handbook"
description: "Git Handbook"
category: java
tags: [git, handbook, github]
---
{% include JB/setup %}

## Introduction
In software development, Git is a distributed version control and source code management (SCM) system with an emphasis on speed. Initially designed and developed by Linus Torvalds for Linux kernel development, Git has since been adopted by many other projects.

Every Git working directory is a full-fledged repository with complete history and full version tracking capabilities, not dependent on network access or a central server.

Git is free software distributed under the terms of the GNU General Public License version 2.

## Installation instructions

###Windows 2000/XP/Win7

###Unix-based Operating Systems(Linux, Solaris and Mac OS X)
    $ sudo apt-get install git git-core git-gui git-doc     # Install git

## Configuring git

###Configuring ssh key
    $ ssh-keygen -t rsa -C "your_email@example.com"
    # Create a new ssh key (press Enter while need to type a passphrase)

    $ sudo apt-get install xclip
    # Install xclip

    $ xclip -sel clip < ~/.ssh/id_rsa.pub
    # Copy the contents to clipboard, add to github account setting.

    $ ssh -T git@github.com
    # Showing 'Hi username!' means you've successfully authenticated.

###Set up git

####Username
    $ git config --global user.name "Your Name Here"
    # Set the default name for git to use when you commit

####Email
    $ git config --global user.email "your_email@example.com"
    # Set the email associated with your GitHub account

####Password caching
    $ git config --global credential.helper cache
    # Set git to use the credential memory cache

    $ git config --global credential.helper 'cache --timeout=3600'
    # Set the cache to timeout after 1 hour (setting is in seconds)
    
    Tip: You need git 1.7.10 or newer to use the credential helper

## Common commands
    $ git init
    $ git clone
    
    $ git add
    $ git status
    $ git diff
    $ git commit
    $ git reset
    $ git rm, mv
    $ git stash
    
    $ git branch
    $ git checkout
    $ git merge
    $ git log
    $ git tag
    
    $ git fetch, pull
    $ git push
    $ git remote
    
    $ git log
    $ git diff

###Getting and Creating Projects
In order to do anything in Git, you have to have a Git repository. This is where Git stores the data for the snapshots you are saving.

There are two main ways to get a Git repository. One way is to simply initialize a new one from an existing directory, such as a new project or a project new to source control. The second way is to clone one from a public Git repository, as you would do if you wanted a copy or wanted to work with someone on a project. We will cover both of these here.

####git init
Initializes a directory as a Git repository

    $ mkdir cbay
    $ cd cbay
    $ git init      #initialized empty Git repository in cbay/.git/

In a nutshell, you use `git init` to make an existing directory of content into a new Git repository. You can do this in any directory at any time, completely locally.

####git clone
Copy a git repository so you can add to it

    $ git clone [url]
    
    $ git cone git://github.com/szhang7/Hello-World.git

In a nutshell, you use `git clone` to get a local copy of a Git repository so you can look at it or start modifying it.

###Basic Snapshotting
Git is all about composing and saving snapshots of your project and then working with and comparing those snapshots. This section will explain the commands needed to compose and commit snapshots of your project.

####git add
Adds file contents to the staging area

    $ git status -s
    ?? README
    
    $ git add README
    
    $ git status -s
    A README
    
    $ vim README
    $ git status -s
    AM README
    
    $ git add .
    $ git add -A
    #add changes from all tracked and untracked files

In a nutshell, you run `git add` on a file when you want to include whatever changes you've made to it in your next commit snapshot.

####git status
View the status of your files in the working directory and staging area

    $ git status -s
    $ git status

In a nutshell, you run `git status` to see if anything has been modified and/or staged since your last commit so you can decide if you want to commit a new snapshot and what will be recorded in it.

####git diff
Shows diff of what is staged and what is modified but unstaged

    $ git diff              #show diff of unstaged changes
    $ git diff --cached     #show diff of staged changes
    $ git diff HEAD         #show diff of all staged or unstaged changes
    $ git diff --stat       #show summary of changes instead of a full diff

In a nutshell, you run `git diff` to see details of the `git status` command - how files have been modified or staged on a line by line basis.

####git commit
Records a snapshot of the staging area

    $ git commit -a         #automatically stage all tracked, modified files before the commit
    $ git commit -m 'changes to hello file'
    $ git commit -am 'changes to hello file'

In a nutshell, you run `git commit` to record the snapshot of your staged content.

####git reset
Undo changes and commits

    $ git reset HEAD        #undo the last commit and unstage the files
    $ git reset --soft      #undo the last commit
    $ git reset --hard      #undo the last commit, unstage files and undo any changes in the working directory

In a nutshell, you run `git reset HEAD` to undo the last commit, unstage files that you previously ran `git add` on and wish to not include in the next commit snapshot.

####git rm
Remove files from the staging area

    $ git rm file           #remove the file from the staging area entirely and also of your disk
    $ git rm file --cached  #remove the file from the staging area, but leave the file in the working directory.
    $ git mv                #git rm --cached orig; mv orig new; git add new

In a nutshell, you run `git rm` to remove files from being tracked in Git. It will also remove them from your working directory.

####git stash
Save changes made in the current index and working directory for later

    $ git stash             #add current changes to the stack
    $ git stash list        #view stashed currently on the stack
    $ git stash apply       #grab the item from the stash list and apply to current working directory
    $ git stash drop        #remove an item from the stash list

In a nutshell, run `git stash` to quickly save some changes that you're not ready to commit or save, but want to come back to while you work on something else.

###Branching and Merging 

####git branch
List, create and manage working contexts

    $ git branch                        #list your available branches
    $ git branch (branchname)           #create a new branch
    $ git branch -v                     #see the last commit on each branch
    $ git branch -d (branchname)        #delete a branch

In a nutshell, you use `git branch` to list your current branches, create new branches and delete unnecessary or already merged branches.

####git checkout
Switch to a new branch context

    $ git checkout -b (branchname)      #create and immediately switch to a branch
    $ git checkout master               #switch to branch 'master'
    
    $ git push (remote-name) :(branchname) #delete a branch
    $ git push remote-name --delete branchname
    # git push remote-name local-branch:remote-branch
    
####git merge
Merge a branch context into your current one

#####simple merges
    $ git branch removals
    $ git checkout -b removals
    $ git rm test.txt
    $ git commit -am 'removed test.txt'
    $ git checkout master
    $ git merge removals            #merge master with branch removals

#####more complex merges
    $ git branch change_class
    $ git checkout -b change_class
    $ vim hello.rb                  #modify hello.rb
    $ git commit -am 'changed the class name'
    
    $ git checkout master
    $ git mv hello.rb ruby.rb       #rename hello.rb-->ruby.rb
    $ vim ruby.rb                   #modify ruby.rb
    $ git diff                      #diff --git a/ruby.rb b/ruby.rb
    $ git commit -am 'added from ruby'
    $ git merge change_class

#####merge conflicts
    $ git branch fix_readme
    $ git checkout -b fix_readme
    $ vim README
    $ git commit -am 'fixed readme title'
    
    $ git checkout master
    $ vim README
    $ git commit -am 'fixed readme title differently'
    
    $ git merge fix_readme
    Auto-merging README
    CONFLICT (content): Merge conflict in README
    Automatic merge failed; fix conflicts and then commit the result.
    
    $ vim README        #here I'm fixing the conflict
    $ git diff          #show you both sides of the conflict and how you've resolved it as shown here.
    
    $ git status -s
    $ git add README
    $ git status 0s
    $ git commit

In a nutshell, you use `git merge` to combine another branch context into your current branch.

####git log
Show commit history of a branch

    $ git log                       #we'll see all the commit messages that we've done.
    $ git log --oneline             #see a more compact version of the same history.
    $ git log --oneline --graph     #see when the history was branched and merged
    
    $ git branch erlang
    $ git checkout -b erlang
    $ vim erlang_hw.erl
    $ git add erlang_hw.erl
    $ git commit -m 'added erlang'
    
    $ vim haskell.hs
    $ git add haskell.hs
    $ git commit -m 'added haskell'
    
    $ git checkout master
    $ vim ruby.rb
    $ git commit -am 'reverted to old class name'
    
    $ git log --oneline erlang
    
    # which commits are unique to a branch in comparison to another. 
    $ git log --oneline erlang ^master
    $ git log --oneline master ^erlang

    If we are interested in merging in the 'erlang' branch we want to see what commits are going to effect our snapshot when we do that merge. The way we tell Git that is by putting a ^ in front of the branch that we don't want to see.Note that the Windows command-line treats ^ as a special character, in which case you'll need to surround ^master in quotes. 

In a nutshell, you use `git log` to list out the commit history or list of changes people have made that lead to the snapshot at the tip of the branch.

####git tag
Tag a point in history as important

    $ git tag -a v1.0
    $ git log --oneline --decorate --graph
    
    $ git tag -a v0.9 558151a
    $ git log --oneline --decorate --graph
    
    $ git fetch origin --tags                   #fetch all tags from a remote repository
    $ git fetch <remote> tag <tag-name>         #want a single tag
    
    $ git push <remote> --tags                  #push tags to a remote repository

In a nutshell, you use `git tag` to mark a commit or point in your repo as important.

###Sharing and Updating Projects
Git doesn't have a central server like Subversion. All of the commands so far have been done locally, just updating a local database. To collaborate with other developers in Git, you have to put all that data on a server that the other developers have access to. The way Git does this is to synchronize your data with another repository. There is no real difference between a server and a client - a Git repository is a Git repository and you can synchronize between any two easily.

####git remote
List, add and delete remote repository aliases

    $ git remote            #list your remote aliases
    $ git remote -v         #see the actual URL for each alias
    
    $ git remote add        #add a new remote repository of your project
    #git remote add [alias] [url]
    
    $ git remote rm         #remove an existing remote alias
    #git remote rm [alias]
    
    $ git remote rename [old-alias] [new-alias] #rename remote aliases
    #git remote rename [old-alias] [new-alias]
    
    $ git remote set-url        #update an existing remoete URL
    $ git config remote.origin git://github.com/szhang7/HelloWorld.git

####git fetch
Download new branches and data from a remote repository

    $ git fetch [alias]         #synchronize you with another repo

In a nutshell, you run `git fetch [alias]` to synchronize your repository with a remote repository, fetching all the data it has that you do not into branch references locally for merging and whatnot.

####git pull
Fetch from a remote repo and try to merge into the current branch

    $ git pull
    #run a [git fetch] immediately followed by a [git merge]

####git push
Push your new branches and data to a remote repository

    $ git push [alias] [branch]         #make your [branch] the new [branch] on the [alias]
    $ git push github master            #push our 'master' branch to the new 'github' remote

#####Q&A
    $ git push github master
    To git@github.com:schacon/hw.git
     ! [rejected]        master -> master (non-fast-forward)
    error: failed to push some refs to 'git@github.com:schacon/hw.git'
    
    The solution:
    $ git fetch github
    $ git merge github/master
    #and then pushing again

In a nutshell, you run `git push [alias] [branch]` to update a remote repository with the changes you've made locally.

###Inspection and Comparison
In a nutshell you can use `git log` to find specific commits in your project history - by author, date, content or history. You can use `git diff` to compare two different points in your history - generally to see how two branches differ or what has changed from one version of your software to another.

####git log
Filter your commit history

    $ git log --author                  #look for only commits from a specific author
    $ git log --author=Linus --oneline -5
    #-[number] option will limit the results to the last [number] commits.
    
    $ git log --since --before          #filter commits by date committed
    $ git log --until --after
    $ git log --oneline --before={3.weeks.ago} --after={2010-04-18} --no-merges
    #--no-merges remove merge commits
    
    $ git log --grep                    #filter commits by commit message
    $ git log --grep=P4EDITOR --no-merges
    #commit messages including P4EDITOR
    
    $ git log --grep='p4 depo' --format="%h %an %s"
    #use --format option, so we can see who the author of each commit was.
    
    $ git log --grep="p4 depo" --format="%h %an %s" --author="Hausmann"
    #show all commits by Simmon OR commits with "p4 depo" in the message.
    
    $ git log --grep="p4 depo" --format="%h %an %s" --author="Hausmann" --all-match
    #show all commits by Simon and commits with "p4 depo" in the message.
    
    $ git log -S                    #filter by introduced diff
    $ git log -Suserformat_find_requirements
    #find which commits modified anything that looked like the function name 'userformat_find_requirements'
    
    $ git log -p                    #show patch introduced at each commit
    $ git log -p --no-merges -2
    #tells Git to put the patch after each commit
    
    $ git log --stat                #show diffstat of changes introduced at each commit
    $ git log --stat --no-merges -2
    #summarize the changes

####git diff
See the absolute changes between any two commit snapshots

    $ git diff [version]            #see what has changed since the last release
    $ git diff v0.9
    #see what has changed in our project since the v0.9 release
    
    $ git diff v0.9 --stat
    #summarize the changes
    
    $ git diff --stat master erlang         #wrong way
    
    $ git diff --stat 8d585ea erlang
    $ git diff --stat master...erlang       #recommended strongly 
    $ git diff --stat $(git merge-base master erlang) erlang
    #see what is on the "erlang" branch compared to the "master" branch.

In a nutshell, you can use `git diff` to see how a project has changed since a known point in the past or to see what unique work is in one branch since it diverged from another. Always use `git diff branchA...branchB` to inspect branchB relative to branchA to make things easier.

###git api思维导图
![1.jpg]({{ site.img_url }}/2013-08-16.png)

## REFERENCES
- [Set Up Git](https://help.github.com/articles/set-up-git)
- [Generating SSH Keys](https://help.github.com/articles/generating-ssh-keys)
- [Git Reference](http://gitref.org/index.html)
- [Git 常用命令](http://www.cnblogs.com/1-2-3/archive/2010/07/18/git-commands.html)


