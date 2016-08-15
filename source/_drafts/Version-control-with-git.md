---
title: Version control with git
tags:
---

## Why do I need version control?
Thinks about the day when we used to have folder names like project, project-final, project-final2, project-last-final etc.
We used to duplicate project every time to backup a previous version for safety. Version control solves this problem. It is a system which records and stores every changes made to a project, with the flexibility of allowing you to go back to a previous state at any time. Developers have been using this method for a long time (trust me it exists from the 70s) and it is now unthinkable to seriously write software without one.

<!-- more -->

## Installation
Git is the most popular version control tool used today, so we will be taking a look at how we can make use of this powerful tool to make our lives easier. Before installing git you might want to check whether git is already installed. You can open the terminal and type `git --version` to check the exact version that you have or you could do `which git` to find the location of git. If you don't have git installed, then you can head over to the downloads section of the official git [website](https://git-scm.com/downloads) and download the git installer based on your operating system to install it on your computer. The installation process is pretty simple and the installer will guide you through.

## Initial Configuration
Before we start using git for our projects, we need to configure git to suit our needs, just like how we would configure a text editor before we start writing code.Its important to note her that git allows us to provide configuration at 3 different levels.
> System - Configurations at this level apply to all the users of the system
> User - Configurations at this level apply to a specific users of the system
> Project - Configurations at this level apply to the project alone

The system level configurations are stored at `/etc/gitconfig`, the user level configurations are stored at `~/.gitconfig`, the project level configurations are stored at `project_root_folder/.git/config`. These are just plain text files, to change the configurations at any particular level we could very well just go and edit these file manually, but the issue here is that we have to also understand the format in which we must write the configuration in these file. Git simplifies this process by providing us some commands to edit these configurations.

Using the git command we edit the configuration like this. `git config --system #the configuartion goes here` for a system wide configuration, or `git config --global #the configuartion goes here` for a user level configuration, and `git config #the configuartion goes here` for a project level configuration.

Lets add a few user level configurations to get us started with git. The first thing is, you need to tell git about yourself i.e your name and email address. Because when you are working on a project with multiple team members and when you make a change with git, it marks that change with your identity so that others can know the person who was responsible behind writing that piece of code. You can also tell git the default text editor that you want it to use. Git uses that text editor to open files when it wants you to enter some message. Along with the text editor we also provide it with 2 options `w` meaning telling unix to wait till we complete entering the message(if we don't do this unix will not wait till we complete writing the message and it will keep going with what it needs to do) and `l1` means put the cursor at line number 1. Another configuration that we can add is to tell git to use colors when outputing things to the command line, if we don't add this configuration it will just give us monochromatic text. 
```
git config --global user.name "Raj Abishek"
git config --global user.email "rajabishek@hotmail.com"
git config --global core.editor "sublime -wl1"
git config --global color.ui true
git config --global --list //Show all the configurations
git config --global user.name //Show's the name
git config --global user.email //Show's the email address
```

## Getting help from git
You can use the `git help` command to get help from git. This will list all the commonly used commands that git provides along with a short note on each one of them. To know more about how to use a specific command we can do `git help <command>` to get details about using that git command, it actually brings out the git manual page for that command, the page has the description about that command and the options that we can use along with it. Use can use f key to move forward and b to move backward while reading the documentation in the git man page. When you are finally done you can hot q to quit out. Unix users will recognize that the manual page that was opened was a typical Unix man page.  In fact its was the very same thing, you could have also opened it using `man git-log`. Git help just gives you an easier way to look at those manual pages through its command line tool.

## Initializing a repository
Before we start using git for a project we need to initialize a repository, what I mean is that we need to tell git which is the folder that it needs to keep track of. The first step that we do is we navigation to the project's root folder and run the `git init` command there. This tell git to do the initialization process, i.e start doing what you need to do, to track this folder. What git internally does is that it create a .git folder in the project's root where it store all the git related information. Its important to note here that this .git folder is that only place where git stores all the information, unlike other version control systems like SVN it doesn't include a tracking file in every single directory down the line ( To remove SVN you will have to go through all pull out all the tracking file present in every directory). Since this is the only place where git stores all of the git related information for the project, if we needed to remove version control from the project, all that we need to do is remove this folder `sudo rm -rf .git`.

## Basic git workflow
> Make the changes
> Add the changes ( Adds the files to the staging area - more on this later )
> Commit changes to the repository with a message

## Looking through the commit made
`git log` command allows us to see the commits that have been made so far. For example to see the recent 5 commits what we do `git log -n 5` to get the last 5 commits that have been made. `git log --since=2016-08-1` will should the commits that have been made after 1st of August 2016.(This is exclusive doesn't include commits made on 1st of August). Similarly the command `git log --until=2016-08-1` will show commits that have been made before 1st August 2016.( This is inclusive, includes the commits made on 1st of August). You also look for commits that have been made by a specific author, you need not search by the full name, you can just provide git a part of the author's name and git will search for you. `git log --author="Raj"` will search for all commits that have been made by authors who's name has the word "Raj". We can also search the commits by the commit message, `git log --grep="hello"` will bring out all commits that have the word hello in the commit message. `grep` stands for gllbalk regular expression.

## The three-tree architecture
Git uses a three tree architecture, i.e we have 3 trees the working copy, staging area, and the repository. We call each one of them a tree because each one them represents a folder structure. In fact when we did an add we are actually adding file to the staging area. From there we commit to the repository. It is possible to go ahead and commit directly to the repository and skip the staging step, we will look into that in a moment. The whole point of having a staging area is to make and get things ready, lets say we have 10 files that have changed in our project( working copy), now if we don't want to commit all these changes at once as a single change set(a commit), then this is where the staging area comes in handy. We can just add those files that we want to a part of the first change set to the staging area and commit them alone. Next we can take the remaining changes from the working copy and do that same. The staging area acts like a workplace where we can arrange and group things that we want to be a part of one change set. Now we also have the option to pull changes from the repository to the staging index, and then from there to the working copy, buts that's not usually the way we work. Whenever we are pulling changes from the repository we pull it directly to the working copy.

## How git refers to the change sets ?
Git generates a checksum for each change set. Checksum algorithms convert data into a simple number called as the checksum. How many ever times you feed the same data the checksum algorithm always generates the same checksum. Changing the data would change the checksum. Git uses SHA-1 hash algorithm to generate the checksum. Its a 40 character hexadecimal string. We have seen this checksum before if you remember, when we do a git log we see this checksum that is generated for each commit there. Therefore every commit has this meta information the checksum, the author details and a reference to the checksum of the previous commit called as parent. In fact we can use these checksums to search for the commits also. 

## What the hell is the HEAD pointer ?
We also have something called as the HEAD pointer in git. HEAD always points to the tip of the current branch in the repository, it's the last state of the repository, what was last checkout out. Or you can visualize as HEAD pointing to the parent of the next commit, i.e where the writing will start taking place. Its the place where we left off, its the place from where we are going to make any further changes.

Lets take a look at how git keep track of HEAD. Inside the .git folder there is a file called HEAD and that what git uses to know where the head is pointing. If you see the contents of the file you find a path, if you follow that path, you would actually lead to the SHA value of the most recent commit made in the current branch. When we are doing `git log` its the same thing as `git log HEAD` starting from the HEAD go backwards and show me the log.