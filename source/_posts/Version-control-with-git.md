---
title: Version control with git
date: 2016-08-15 09:00:00
tags:
---

## What is version control ?
It is a system that records and stores the changes made to the project over time thereby allowing us to go back to a previous state at any time.

<!-- more -->

## Why do we need version control ?
Think about the days when we used to have folder names for our projects like project-start, project-final, project-final2, project-last-final etc. We used to duplicate the project folder every time we needed a backup. Version control solves this problem. Developers have been using this method for a long time (it exists from the 70s) and it is now unthinkable to write software without this technology.

With a good version control system you should get the below features for a very little overhead.

- Revert files back to a previous state.
- Revert the entire project back to a previous state.
- Compare changes over time.
- See who last modified something that might be causing a problem.
- Who introduced an issue and when.
- Recover files when you screw up things or lose files

## Local Version Control Systems
The technique that developers used back then was to duplicate project folders. This approach is very simple but highly error prone. It is easy to forget which directory you’re in and accidentally write to the wrong file or copy over files you don’t mean to. To deal with these problems programmers developed local version control systems that had a simple database that stored the changes made over time. One of the most popular local version control systems back then was a system called RCS.

![Screenshot 1](/img/version-control-git/local-version-control.png)

RCS works by keeping patch sets (i.e the differences between files) in a special format on disk. If you asked RCS for a file at a particular point in time, it would recreate that file by adding up all the patches stored in the database.

## Centralized Version Control Systems
Next developers started working with centralized version control systems that allowed them to collaborate with their peers working on other systems. The idea is to have a single server that contains all the versioned files and a number of clients check out files from this central place. Systems such as CVS, Subversion and Perforce were based on this idea. This system was better than local version control system because team members to a certain extent know what others are working on and now administrators have better control over who can do what.

![Screenshot 1](/img/version-control-git/central-version-control.png)

But there are some down sides too. If the server goes down for sometime, then during that period nobody can collaborate and save versioned changes to anything they’re working on. But even worse what if the hard disk on the server gets corrupted ? You absolutely loose everything except for whatever single snapshots people happen to have kept on their local machines.

Both local version control system and centralized version control system suffers from this problem. Whenever you have the entire history of the project in a single place you have the risk of losing everything.

## Distributed Version Control Systems
In a distributed version control system such as Git, Mercurial, Bazaar or Darcs, the clients fully clone the repository, they don’t just check out the latest snapshot of the files. Every clone is really a full backup of all the data. Every clone consists of both the latest code files and the information about the different versions and how to generate them. Thus if the central server dies then any of the client repositories can be copied back to the server to restore it.

## Little bit of history
Git is the most popular version control system used today. The history of git is pretty interesting since it started in a controversy. The Linux kernel is a fairly large open source project. In 2002 the Linux kernel project began using **BitKeeper** for version control which was a proprietary DVCS. In 2005 the relationship between the commercial company that developed BitKeeper and the community that developed the Linux kernel broke down, and thus no more the Linux kernel community could use the tool for free of charge. This provoked the Linux community and especially the creator of Linux kernel(Linus Torvalds) to develop their own version control tool keeping in mind the lessons they had learned while using BitKeeper. Some of the goals for designing the new system that they had in mind was:
- Free & open source
- Fast
- Simple design
- Efficient with large projects
- Strong support for non-linear development
- Fully distributed

Git project was completed with the above features in 2005. Since inception it has been in wide adoption. It is extremely fast and can handle large projects efficiently. Its branching system which we will look into later provides strong support for non linear development.

## Installation
Before installing git you might want to check whether git is already installed. You can open the terminal and type `git --version` to check the exact version that you have or you could do `which git` to find the location of git.
If you are on a Linux machine you can use the package manager that comes with your installation. If you’re on Fedora for example, you can use yum:
```sh
sudo yum install git-all
```
If you’re on a Debian-based distribution like Ubuntu, try apt-get:
```sh
sudo apt-get install git-all
```
If you are on mac then the easiest way to install git is to install command line tools from Xcode. If you want a more updated version of git then you can head over to the downloads section of the [official git website](https://git-scm.com/downloads) and download the git installer. The installation process is pretty simple and the installer will guide you through.

## Snapshots, Not Differences
Other version control systems(CVS, Subversion, Perforce, Bazaar, and so on) store information as a list of file based changes. The information they keep and store is the changes made to each file over time.

Git handles data in a completely different way. Git thinks of its data more like a set of snapshots of a miniature filesystem. Whenever you save the state of your project in Git, it basically takes a snapshot. It takes a picture of what all your files look like at that moment and stores a reference to that snapshot. To be efficient, if files have not changed, Git doesn’t store the file again, just a link to the previous identical file it has already stored.

## Almost everything is done locally
Most of the operations done in Git is performed locally, no information is needed from another computer on your network. This is possible because the entire history of the project is right there on the local disk. This is why almost every operation seems instantaneous(no network latency overhead).

For example, to browse the history of the project, Git doesn’t need to go out to the server to get the history and display it for you, it simply reads it directly the your local database.

## Initial Configuration
Before we start using git for our projects we need to configure git to suit our needs, just like how we would configure a text editor before we start writing code. You should have to do these things only once on any given computer and they’ll even stick around between upgrades. Its important to note here that git allows us to provide configuration at 3 different levels.
- **System** - Configurations at this level apply to all the users of the system
- **User** - Configurations at this level apply to a specific user of the system
- **Project** - Configurations at this level apply to a specific project

The system level configurations are stored at `/etc/gitconfig`, the user level configurations are stored at `~/.gitconfig` or `~/.config/git/config`, the project level configurations are stored at `project-root/.git/config`. Each level overrides values in the previous level, so values in `.git/config` trump those in `/etc/gitconfig`. These configuration files are just plain text files. To change the configuration at any particular level we could very well just go and edit the corresponding file manually, but the issue here is that we should also know the format in which we must write the configurations. To simplify this process git provides us with some commands to add/remove configurations at any level.

We run the command `git config --system <configuration>` for a system wide configuration, or `git config --global <configuration>` for a user level configuration, and `git config <configuration>` for a project level configuration.

Lets add a few user level configurations to start with. The first thing is, you need to tell git about yourself i.e your name and email address. When you are working on a project with multiple team members and when you make a change, git marks that change with your identity. In this way any team member can know the person who was responsible behind writing/changing a particular piece of code.

You can also tell git the default text editor that you want it to use. Git uses that text editor to open files when it wants you to enter some message. If not configured, git uses your system’s default editor. Along with the text editor we also provide it with 2 options `w` meaning telling unix to wait till we complete entering the message(if we don't do this unix will not wait till we complete writing the message and it will keep going with what it needs to do) and `l1` means put the cursor at line number 1. Another configuration that we can add is to tell git to use colors when outputing things to the command line, if we don't add this configuration it will just give us plain monochromatic text.
```sh
git config --global user.name "Raj Abishek"
git config --global user.email "rajabishek@hotmail.com"
git config --global core.editor "sublime -wl1"
git config --global color.ui true
git config --global --list #Show all the configurations
git config --global user.name #Show's the name
git config --global user.email #Show's the email address
```

After running the above command git will automatically write these configurations to the `~/.gitconfig` file. Infact if you look at the contents of the configuration file by running `cat ~/.gitconfig` we can indeed see the configurations added. The contents of the configuration file are show below. As you can see below git expects the configurations in a specific format. Thanks to the `git config` command, we need not worry about any of this.

```
[user]
       	email = rajabishek@hotmail.com
       	name = Raj Abishek
[core]
       	editor = sublime -wl1
[color]
        ui = true
```
When you run the `git config --list` command it shows the settings the are applicable for the project. Git starts reading the settings from the system level downwards. As a result you may see keys more than once, because git is reading the same key from different files (/etc/gitconfig and ~/.gitconfig, and then <project-root>/.git/config). First it reads from the system level, then it reads from the user level and then it reads from the project level. Git uses the last value for each unique key it sees.

## Getting help from git
You can use the `git help` command to get help from git. This will list the commonly used commands that git provides along with a short note on each one of them. To know more about how to use a specific command we can do `git help <verb>` or `git <verb> --help`. It actually brings out the git manual page for that command, the page has the description about that command and the options that we can use along with it. Use can use `f` key to move forward and `b` to move backward in the git man page.

When you are finally done you can hit `q` to come out. Now unix users will recognize that the manual page that was opened looked something similar to the unix man page.  In fact its was the very same thing, you could have also opened it using `man git-log`. Git just gives you an easier way to look at those manual pages through its command line tool.

## Initializing a repository
Before we start using git for a project we need to initialize a repository, what I mean is that we need to tell git which is the folder that it needs to keep track of. The first step that we do is we navigate to the project's root folder and run the `git init` command there. This tell git to do the initialization process, i.e we are essentially telling it to start doing what it needs to do, to track this folder.

What git internally does is that it creates a `.git` folder in the project's root where it stores all the information for tracking purpose. Its important to note here that this `.git` folder is the only place where git stores all the information, unlike other version control systems like SVN it doesn't include a tracking file in every single directory down the line (To remove SVN we would have to go through every sub directory in the project and pull out the tracking file present in it). Since this is the only place where git stores all the information for tracking, in future if we needed to remove version control from our project, all that we need to do is remove this folder by running `sudo rm -rf .git`.

## Basic git workflow
Now that we have initialized git, the basic work flow that one would follow is shown below.
1. Make the changes in files
1. Add the changes ( Adds the files to the staging area - more on this later )
1. Commit changes to the repository with a message

To add the changes we use the git add command, we run `git add <path>`. Once the files are added to the staging area we commit them with a message. You can think of commit as taking a photograph or capturing a screen shot. Commits are what that allows us to get a previous version of file. Every time you commit you are creating a backup of the files. To commit with a message we run `git commit -m "Commit message"`.

The commit message is very important and it needs to be descriptive. In the commit message you write what that change set does and not what you did or what you were asked to do. For example if you are asked animate a screen in a mobile app. Then first you write code for the animation. You add those files to the staging area. And then you commit this change set with a message like "Animates the login screen before presenting it". As you can see here, the commit message describes what the change set is and not what you actually did("I added the animation for the login screen"). If someone else pulls in this change set in their project, commit message should let them know what will happen.

## Looking through the commits made
The git log command allows us to see the commits that have been made so far. For example to see the recent 5 commits we run `git log -n 5` to get the last 5 commits that have been made. `git log --since=2016-08-1` will show the commits that have been made after 1st of August 2016.(This is exclusive doesn't include commits made on 1st of August). Similarly the command `git log --until/before=2016-08-1` will show commits that have been made before 1st August 2016.(This is inclusive, includes the commits made on 1st of August). You can also pass something interesting values for the dates. You can do something like `git log --since="2 weeks ago"` to get the commits from the last 2 weeks. You can even combine since and util options in the git log command. `git log --since="2 weeks ago" --until="3 days ago"` shows the commits that have happened since 3 weeks ago and it will show the results only till 3 days ago, the commits made during the last 3 days wont be shown. And another way you can write this command is `git log --since=2.weeks --until=3.days`.

You also look for commits that have been made by a specific author, you need not search by the full name, you can just provide git a part of the author's name and git will search for you. `git log --author="Raj"` will search for all commits that have been made by authors who's name contains the word "Raj". We can also search the commits by the commit message, `git log --grep="hello"` will bring out all commits that have the word hello in the commit message. `grep` stands for global regular expression.

## Three tree architecture
Git uses a three tree architecture, i.e we have 3 trees the **working copy**, **staging area**, and the **repository**. We call each one of them a tree because each one of them represents a folder structure. When we run the git add command we are adding files to the staging area. From there we commit to the repository. It is also possible to go ahead and commit directly to the repository and skip the staging step, we will look into that in a moment.

The whole point of having a staging area is to make and get things ready, lets say we have 10 files that haves changes in our project(working copy), now if we don't want to commit all these changes at once as a single change set(a commit), then this is where the staging area comes in handy. We can just add those files to the staging area that we want to be a part of the next commit and commit them alone. Next we can take the remaining changes from the working copy and do the same.

The staging area acts like a workplace where we can arrange and group things that we want to be a part of one change set. When we commit only the changes present in the staging area will be recorded. Now we also have the option to pull changes from the repository to the staging index, and then from there to the working copy, buts that's not usually the way we work. Whenever we are pulling changes from the repository we pull it directly into the working copy.

The `.git` directory is where git stores the metadata and object database for your project. This is the most important part of git, and it is what is copied when you clone a repository from another computer. The working directory is a single checkout of one version of the project. These files are pulled out of the compressed database from the `.git` directory and placed on disk for you to use or modify. If a particular version of a file is in the `.git` directory, it’s considered committed. If it has been modified and was added to the staging area, it is staged. And if it was changed since it was checked out but has not been staged, it is modified.

## How git refers to the change sets ?
Git generates a checksum for each change set. Checksum algorithms convert data into a simple number called as a checksum. How many ever times you feed in the data to the checksum algorithm, the same data always generates the same checksum. Changing the data would result in a different checksum. Git uses SHA-1 hash algorithm for generating the checksum. It is a 40 character hexadecimal string.

We have seen this checksum before if you remember, when we do git log we see this checksum that is generated for each commit. Therefore every commit has a meta information attached to it which includes the checksum, the author details and a reference to the checksum of the previous commit(parent). In fact we can use these checksums for searching a particular commit.

## Demystifying the HEAD pointer
We also have something called as the HEAD pointer in git. HEAD always points to the tip of the current branch in the repository. It is the last state of the repository, what was last checked out. Or you can visualize HEAD as a pointer that is pointing to the parent of the next commit, i.e where the writing will start taking place. Its the place where we left off, its the place from where we are going to make any further changes.

Inside the `.git` folder there is a file called HEAD and that is what git uses to know where the HEAD is pointing. If you see the contents of the file you find a path, if you follow that path, you would actually lead to the SHA value of the most recent commit made in the current branch. When we are doing `git log` its the same thing as doing `git log HEAD` i.e we are telling git to log the commits starting from the HEAD going backwards. Instead if we do `git log <sha-value-of-a-commit>` then it would log all the commits previous to that commit.

## Revisiting some basic git commands
One of the most important commands in git is the `git status` command, it reports us the difference between the three trees in git. Whenever you don't know what to do while working with git, this command will help you with the available options that you have. It shows the difference between the working area, staging area and the repository. Its also shows the current branch that we are on. Lets say that you add 2 new files, now when you run `git status` it says that you have 2 untracked files. All that it is trying to tell you is that it knows about the repository and it has found 2 new files in the working copy that are not there in the repository. Working copy has new things that git is not currently tracking.

Now to add files to the staging index we do `git add <path-to-file>` or we can add all files in a folder by running `git add <path-to-folder>`. This will add all the files in the path to the staging area from where we can make a commit. Now when we do `git status` the things under the changes to be committed section are the files that are there in the staging area.

Now to commit the changes in the staging area we run `git commit -m "This is the commit message"` the `-m` option is used to provide a message along with a commit. When you do a commit you are essentially taking a snapshot of the changes that you have made to files present in the staging area. Lets say you have 5 files ready to be committed in the staging area, when you do a commit you are taking a snapshot of the changes that you have made to these 5 files and giving a message that describes the change.

There is another git command to add the files to the staging area and then commit it in a single step. You can do that by `git commit -am "This is the message"`. This command is equivalent to running the following command from the root folder `git add . && git commit -m "This is the message"`. There are some caveats here, first this adds all the files in the working directory, so if there are some changes that you didn't want to include in the first change set that you are commiting, then this might not be the best option that you are looking for. Secondly, the files that are deleted and the files that are not tracked(new files) doesn't get included in this. This only works well for files that have been modified.

## Show the differences
Lets say you have made some changes in the working copy. Now we can use the `git diff` command for showing the changes that you have made. It shows us the difference between the working copy and the staging index. By the way staging area and staging index is the same, the terms are used interchangeably. It just reports the changes that we have in the working copy, i.e what is unique is the working copy, how is the working copy different from the staging index and the repository. It tells on a line by line basis on what was changed. `git diff <path-to-file>` will just report that changes that have occurred to the particular file. `git diff --staged` command compares the staging area with repository, i.e how is the staging are different from the repository. `git diff --cached` is the equivalent to the `git diff --staged` command. There is also another option called as `--color-words` that you can use with the git diff command to show the changes side by side on the same line and to use color to differentiate the changes, instead of the changes on different lines. We run the command `git diff --color-words <path-to-file>`.

## Deleting a file
Lets say your working copy is in sync with the repository. Now lets say you are removing a file from the working copy, let say you are removing sample.text file. First you delete the file on disk. Now when you run git status, git tells you that I knew a file that I was tracking called as sample.txt but its not present in the working area now. Now as usual to add the file to the staging index you can do `git rm/add sample.txt`. Now if you do git status it shows you that the file that was deleted. Next to commit this change you can do a git commit.

Now you also have another way to do it. Instead of you deleting the file manually on disk, git can take care of that work for you. You can do `git rm sample.txt` this will essentially do `rm sample.txt && git add sample.txt`, i.e its does a Unix delete on the file and adds the change to the staging area. What is happening here is that the file is removed from the staging area and removed from your working copy. Now you can just do git commit to capture this change set. If you modified the file and added it to the index already, you must force the removal with the -f option. This is a safety feature to prevent accidental removal of data that hasn’t yet been recorded in a snapshot and that can’t be recovered from git. When it comes to deleting files I would suggest the 2nd approach, let git handle the work for you. Its more easy and quick way to achieve the result. But of course if you are removing multiple files and would like to capture that change you can use the first method.


## Moving or Renaming a file
If you think about it renaming is essentially moving a file. Its like deleting the old file and adding the new file. So when you move a file in the working copy you have to do this `git rm/add <old-path>` and then `git add <new-path>`, i.e delete the old file and add the new untracked file. Now if you do git status it shows that the file has be moved. To commit this change you can do a git commit as usual.

Instead of doing these work manually there is another way in which git can help you in this process. You can do `git mv <old-path> <new-path>` and git will move the file on disk and add the changes to the staging area. Now to can just git commit to complete the process. When it comes to moving files I would suggest the 2nd approach, let git handle the work for you. Its more easy and quick way to achieve the result.

## Undoing changes made to the working copy
This is the most useful feature in git, in fact this is the reason why we use version control at all. The ease to move back to any previous state is what makes this tool very popular. Lets take a look at how we can undo changes in git. The changes that you made in the working directory, changes that you made staged in the staging index or changes that you have even committed in the repository. First lets take a look at how we can undo changes that we have made in the working directory. Lets say we have a file called sample.txt and we make some change in it and save it. But we didn't do it on purpose, now we want the backup version of sample.txt that is in our repository, we want the saved version that git has stored for us in the backup. So we want git to essentially go to the repository checkout the sample.txt file from there and replace what we have in the working directory with it. To do that we use the following command `git checkout sample.txt`.

The git checkout command is used for more that one purpose, its also used along with branches that we will see later. What checkout does is that goes to the repository and gets the named thing that we give it and makes our working directory look like that. So if that named thing is a branch it brings a branch down, if the named thing is a file it brings the file down.

Lets say we have a folder called sample in our working directory in which we have changes in many files, now if we do `git checkout sample` it will checkout the sample folder from the repository and replace the sample folder in the working copy with it. Which means that now all changes that we made in the sample folder are lost. This is all great, but what if we also had a branch called sample. Then its difficult for git to decided whether we mean a branch or a folder, so git decides to give us the branch by default. Thats why its a good practice to use the `--` option while not checking out a branch. So the best way to checkout the sample folder here would be to `git checkout -- sample`. The `--` option is just to indicate git that we are not checking out a branch, we are just talking about a file or folder in the current branch.

## Undoing changes made to the staging index
Lets say we have a sample.txt file in which we have made some changes and now we have added that file to the staging index. Now how do we unstage this file, i.e how do we remove this file from the staging index. We don't want to loose the changes that we made to this file, we still want the changes to be present in the working directory, all that we want to do it remove this file from the staging index, i.e make the sample.txt file in the staging index look the same as the sample.txt file from the repository.

The time when you most often will be doing this is when you are trying to put files together for a commit and you have accidentally added a file to the staging index that you didn't want to a part of the change set that you will be commiting. The way to unstage a folder/file is `git reset HEAD <path>`. What we are telling is go and look at the HEAD pointer, the HEAD pointer points to the last commit in the current branch, go look at that commit and reset the file to the same as what that has.

## Undoing changes made to the repository
Now how do we go about undoing changes made to the repository itself. This is not as easy as you might think, it gets a bit trickier here. Because if you think about it, it makes sense. Lets say we have some commit x in the history that we would like to change, now if you remember if we change the data the the checksum will change(checksum depends on the changes made in the files, the commit message, date, author details, parent value of the commit), but checksums are what used to identify commits in git. If checksum of x changes then the parent of the next commit following x needs to change, if the parent value changes then checksum for it must also be changed, and therefore the checksum of every commit following x in the commit history needs the change. All the way down the chain from x every single commit object will need to be changed, we have completely broken the integrity of data thats in git. Git doesn't allow us to do that. However it is possible for us to just change the last commit because there are not commits following that. So the most recent commit, the commit that HEAD points to alone has the ability to change.

So lets say we make a change to the sample.txt file and commit that, but thats not how we wanted the change set to be, so what we can do is make the rework on how we want the changes to be in our working copy and add that to the staging index and then do `git commit --amend -m "This is the message for the commit"`. Doing this removes the last commit and adds this new one. We can also use this if we would like to just change the commit message alone, lets say we have a spelling error in the last commit message that we made the we can just do `git commit --amend -m "This is the new message for the commit"`.

## Retrieving old versions
Previously as we have seen that its difficult to amend older commits since it would violate the data integrity in git. But what we can do is we can make a new commit to revert the changes made in a commit. Lets say we have a commit x, but we are not happy with the change set that in creates, now what we can do is we can checkout the file from the commit previous to commit x(lets say commit y) and make the changes as we want and commit the changes as a new commit, when we commit this its a good practice to mention that this commits reverts the commit x, so that other people can understand the purpose of this commit. By default when do a `git checkout -- <path>` were actually doing `git checkout HEAD -- <path>` i.e getting the file from the latest commit, instead we could also get a version of file from a previous commit. In our case we need to checkout the file from the commit y, because in commit x the file actually changed. Now to checkout files from the commit y we do the following `git checkout <part-of-sha-value-of-commit-y> -- <path>`. Now when we do this i.e get the version of a file from previous commit the file gets added to the staging area, making it ready for us to commit.

Git also has a revert command that make it easy for us to revert a particular commit lets say as we wanted here we need to revert the commit y, then when we do `git revert <part-of-sha-value-of-commit-y>` it will take all the changes made during commit y and flip it around, it will do exact opposite of the changes anything added will be deleted and anything deleted will be added back again, anything that was modified will be changed back to the previous state. When we execute this command, it going to make that commit. It will pop up the default text editor that we gave and give us an option to change the commit message if we want. Now you can pass the `-n` option with revert and it won't actually do the commit, it will just stage it, wait for you to commit by yourself. Now git revert works really well when things are simple, but if in the mean time other things have changes files have moved perhaps, things were renamed, then it would be harder to make an exact mirror image revert. Now to deal with it git will use a complex set of rules for how to deal with those changes, and the set of the rules that we use is the rules for merging. But if you revert something very complex you are essentially gonna find yourself doing a merge between the current branch and the new set of changes that you are trying to merge into it.

## Undoing many commits
Git reset command is a very powerful tool to undo multiple commits. Always remember that more powerful a tool is the more careful and responsible we have to be while using it. With great power comes great responsibility. Git reset always moves the HEAD pointer. But there are 3 different options that we can use with git reset.
- **soft** - Doesn't change the staging area or the working directory
- **mixed**(default) - Changes staging index to match repository, doesn't change the working directory
- **hard** - Changes the staging index and the working directory to match the repository

## Soft reset
Whenever you are working with git reset, its a good idea to take a screen shot of the git log before you proceed any further. Noting down the SHA values can be helpful if you mess up with anything. Lets say we have b as the most recent commit and commit c was made before commit b. Now the HEAD points to the SHA value of commit b. You can check that with `cat .git/refs/heads/master`. Now if you do `git reset --soft <part-of-sha-value-of-commit-c>`, then HEAD will point to the commit c. You can check that with `cat .git/refs/heads/master`, that the value would have changed. Now in fact if you do `git log` you won't find commit b. c will be like the last commit that was made. The working directory will have the changes that we made after commit c. The changes will be ready in the staging area for us to make a commit.

## Mixed reset(Default)
With this type of git reset the staging area will match the repository after the HEAD pointer was made to point to a different one. Just like the previous example lets say we have b as the most recent commit and commit c was made before commit b. Now the HEAD points to the SHA value of commit b. You can check that with `cat .git/refs/heads/master`. Now if you do `git reset --mixed <part-of-sha-value-of-commit-c>`, then HEAD will point to the commit c. You can check that with `cat .git/refs/heads/master`, that the value would have changed. Now in fact if you do `git log` you won't find commit b. c will be like the last commit that was made. The working directory alone will have the changes that we made after commit c. The staging index will not have the changes, it will be identical to the repository. The changes will be ready in the working area for us to stage and make a commit.

In fact if you remember when you need to unstage a file from the staging index you do `git reset HEAD <filename>`, what is essentially happening here is a mixed reset. Since mixed is the default reset you don't actually need the --mixed option if you want to do a mixed reset. Here we are reseting the HEAD pointer to HEAD itself and making the staging area's file match with the repository's version of the file. This is what happens when we additionally give a filename. Not the entire staging area is made to match the repository, only that particular file that was provided is checked out from the repository to the staging index.

## Hard reset
With this type of git reset the staging area and the working directory will match the repository after the HEAD pointer was made to point to a different one. Just like the previous example lets say we have b as the most recent commit and commit c was made before commit b. Now the HEAD points to the SHA value of commit b. You can check that with `cat .git/refs/heads/master`. Now if you do `git reset --hard <part-of-sha-value-of-commit-c>`, then HEAD will point to the commit c. You can check that with `cat .git/refs/heads/master`, that the value would have changed. Now in fact if you do `git log` you won't find commit b. c will be like the last commit that was made. Use this with caution because you will loose all the changes that you made after commit c, there is no place in which we will have the changes that we made after commit c.

## Removing untracked files
This is where the git clean command comes in handy. Lets say you have a bunch of new files that you have added to the project and you would like to remove them, then you could do it manually, but git clean simplifies this process. You cannot use the git clean option as such you have to use it with either the `-n` or the `-f` option. When you do `git clean -n` it will show you the list of new files that git will remove. When you do `git clean -f` git would actually remove the new file from the working copy. Its important to note here that git clean only removes the untracked files, i.e lets say you have added 3 new files sample1.txt, sample2.txt and sample3.txt then let says you add sample3.txt to the staging area. Now when you run `git clean -f` git will remove only the sample1.txt and the sample2.txt file. So git clean removes the untracked files that are there in your working directory.

## Ignoring files
Lets say we are working on a project and we don't want git to track a particular file or a folder. It may be a log file thats constantly changing, or a temporary file, or a folder that contains the project dependencies which is something that we don't wanna be a part of version control. We need a way to tell git to ignore certain files all together. To tell the list of these files and folders that we want git ignore we create a `.gitignore` file in the project root. We can even use very basic regular expressions in the gitignore file. We can negate expression using the `!` character. The following rules means that ignore all html files except the index.html file. The order of writing the rules is important. Git reads the file from top to bottom and keeps overwriting the rules which are already there.
```
*.html
!index.html
```
You can also tell git to ignore all files in a directory by just having a trailing slash. The following rules says git to ignore all files in the photos directory, which is inside of the assets directory.
```
assets/photos/
```
In the gitignore file comments should start with # character, and blank lines in the gitignore files are skipped. Make sure that you commit the gitignore file to the repository. This is a file that we want git to track and maintain, it is as important as any other project files or folders.
```
assets/*.png
```
The above rules will only ignore the png files in the assets folder, if the assets folder has a folder that contains some other png files, those png files will not be ignored, i.e * only applies to the filenames.

## What to ignore ?
- Compiled source code
- Packages & compressed files
- Logs & Databases
- Operating system generated files
- User uploaded assets (images, PDFs, videos)

To start writing gitignore files for your project you can visit [this website](https://www.gitignore.io/) and type a programming language, or operating system as tags to get started with some boilerplate code. They even have a consistent endpoint naming system allowing developers to even access it via APIs. You way also wanna look at github [article](https://help.github.com/articles/ignoring-files/) on ignoring files and the gitignore [project](https://github.com/github/gitignore) created by github.

## Ignoring files globally
If find yourself ignoring certain files over and over for every project, for example like the operating system files then you can configure git globally to ignore certain files. Doing this will allow to ignore files in all repositories. The settings that we add for configuring to ignore files globally will not live inside of our project, its gonna be outside. Since it wont be a part of the repository, any other person who is working, when they download our project it will not have this configuration. What we are doing is instead or repository specific ignores we have create user specific ignores. Thats good because having things like .DS_Store in the gitgnore is not good if not every team member is using a mac based operating system. Each person in team can have their own gitignore file specific to their operating system on their machines. There are 2 steps that needs to be done to globally ignore files.
1. Make a global gitignore file in some location
1. Tell git where to look for the global gitignore file

Lets say we create a new file in the home folder called as .gitignore_global that represents the global gitignore file. Next to tell git about that we add the following user level configuration `git config --global core.excludesfile ~/.gitignore_global`.

## Ignoring tracked files
If you want to ignore files that are already being tracked, then what can we do ? First step would be to add it to the list in the gitignore file. But doing this alone will not help. Git will still keep track of the changes. One option is that you can do `git rm <filename>` which would remove the file from the working copy and add the changes to the staging index ready for us to commit. Now we can also add the .gitignore file to the staging area, if we commit now, the file would be removed from the working copy and the repository, and even if we add that file again to the project git will not track it.

But what if we do not want to loose the working copy that we had. Well you can delete that file from the staging index alone with the command `git rm --cached <filename>`, now add the .gitgnore file to the staging area and make a commit. Now the file would be delete from the repository also. The only place where the file would be present in the working copy, but again it will not show as an untracked file because now we have git ignored it.

## Tracking empty directories
By default git does not track empty directories. That is because git was designed to be a file tracking system, its purpose is to track files and content in those files. So it tracks files and tracks the directories that it takes to get to those files. But it ignores directories that have no files at all. Now lets say we have an empty folder, but we want git to track that folder, how do we tell git to do that. So the trick that we use here to keep track of empty directories in so put a file in them. By convention the filename that is used for this purpose is a `.gitgnore` or a `.gitkeep` file. `.gitkeep` is the most widely used conventions, you can think of it has a way of telling git to track that folder.

Now you can just add that folder to staging index and commit this change set. There is nothing magical happening here we could have named that file anything we want, we just followed a method that everyone uses. The idea behind doing all this is to add a dummy file in the empty folder which git can track (in turn tracking the folder it takes to read that dummy file).

## Looking through commit history
Before we proceed lets look at the ways in which we can reference commits in git. In the git documentation you often see the reference to the word tree-ish. What does this mean ? We know that tree is a folder structure in a git repository. In git tree-ish means something that references a part of the tree. Its ish because that something can vary widely. In simpler terms a tree-ish is a reference to a commit. Because that commit in turn references the tree, git repository and the files in there at that point. So if you hard time thinking about all the things a tree-ish can be, the simplest version is that its just something that points at a commit. So lets look at the ways in which we can reference a commit.
- full SHA-1 hash of a commit
- part of SHA-1 hash of a commit (at least 4 characters)
- HEAD pointer ( to reference the latest commit )
- Branch reference ( to point to the tip of the branch )
- Tag reference
- Ancestry

In ancestry we have 2 options. One is that we can use the `^` as a suffix character to refer to a parent of a reference.
Like `HEAD^`,`master^`,`acf9339^`. To get the parent of parent we can use the `^` symbol twice. Second option is we can use the `~` as suffix with number of generations to go up. Like `HEAD~1`, `master~`. If there is no number after ~ it is assumed to be 1, so we can leave off number 1 i.e `HEAD~` is equivalent to `HEAD~1`.
```sh
HEAD^ == HEAD~1 == HEAD~ # refers to the 2nd last commit
HEAD^ == HEAD~1 == HEAD~ == master^ == master~  == master~1 # if the currently checked out branch is master

HEAD^^ == HEAD~2 # refers # refers to the 3rd last commit
HEAD^ == HEAD~2 == master^^  == master~2 # if the currently checked out branch is master
```

## Exploring the commit tree
We can use the git ls-tree command to look at a tree-ish. We use the command like this `git ls-tree <tree-ish>`. So when we do `git ls-tree HEAD`, since HEAD points to the tip of the currently checked out branch, it will return the list of files at that point. In the left you can see that we see blob or tree. A blob is a simple file whereas a tree is nothing but a folder. If were we checked out these are the files that we would get from the repository. We can also tell git to show us the file structure from inside a particular path alone, we can do `git ls-tree HEAD^ assets/`, this means that show me the file structure inside the assets folder before making the last commit.

## Navigating the commit log
We have already seen the basics of git log. You should take a look at the git help pages for log because there are so many options there, and you can exactly fine tune the information that you are looking for. Let me walk you through some of the important ones. `git log --online` gives a one line information about every commit. The command `git log --format=oneline` is also equivalent to the previous one but the only difference is that it returns the full SHA instead of partial. There are other formats also `short`, `medium`(default), `full`, `fuller`,`email`,`raw`. `git log -3` can be used to the number of the recent commits to show. Since every commit has a SHA value we can even provide a range of commits. `git log j8129dh..r3919fh` will show the commits in this range, this range is exclusive of the first and inclusive of the second. We can leave the second SHA value, then it would mean all the way till end i.e it will use HEAD as the default for 2nd one.

We can also provide a path here `git log j8129dh.. index.html` would mean show me all the commits in which index.html file was changes since the commit with SHA value j8129dh was made. We can also provide the `-p` meaning patch option to the git log command to show is the details as to what changes in every commit. It will show the diff in each commit. Similarly the `--stat` will give you some statistics on each commit like the number of lines changes etc and the `--summary` will give a summary on each commit, i.e the number of deletions, additions, and the files changed. There is also a `--graph` option that we can use with the git log command which shows a graphical view of each one of the commits, when we start working with branches this will be very useful, cause it will show the places where we branched out and did the merges. A good combination for the graphical view would be `git log --online --graph --all --decorate` which is worth remembering cause this will show the tip of every branch and also where the HEAD currently points to.

## Looking at a specific commit
Git show command it used to look a a specific commit, what changes we made in a particular commit. `git show <commit-reference>` is used to show details about a particular commit. Its shows the full SHA value of the commit, the author details, the date, the commit message, the diff i.e the changes in the file. As discussed previously we can pass the `--format` option here along with the git show command. Git show can actually show various types of objects, it can show blobs, trees, tags and commits. We were working with commits here, but if we passed in a tree it would show the names of the files and folders inside it, it is equivalent to doing `git ls-tree --only-names <tree>`. For blobs i.e files it shows plain contents. Remember that we can't do `git show index.html` to show the contents of the index.html file. Because index.html is not a tree-ish, it is not a reference what we have to do to see the contents with the git show command is first do `git ls-tree HEAD` and in that get the SHA value of the reference of the index.html file and then do `git show <sha-of-index.html-file>`.

## Comparing commits
When we are comparing commits x and y what we are essentially doing is comparing the file trees at x and y, i.e the state of the project at commit x and the state of the project at commit y, thats what we are essentially comparing, we are not actually comparing the files that changed during commit x and during commit y, this is very important to understand and remember. So comparing the latest commit with the commit made 1 week before will show us all the changes to the project that happened during the past 1 week. When we take a look at what branches are we can even compare two different branches.

To compare commits we again use the git diff command in a different way. Lets say HEAD~10 refers to the commit that was made before 1 week, then running `git diff HEAD~10` would show us the all the differences between the directory 1 week ago and now. We can also be specific about what the git diff command reports. We can do `git diff HEAD~10 assets` means that show the changes that happened in the assets folder since the past 1 week. We can also pass in a range lets say HEAD~5 refers to the commit made 2 days ago then running `git diff HEAD~10..HEAD~5` will show the differences between the directories at 1 week ago and 2 days before, i,e what all changes happened in between that period of 5 days.

The `--stat` and the `--summary` command can be used as options along with this command. We can also use the `-b/--ignore-space-change` options which means ignore showing changes where there was a single space as a change and the `-w/--ignore-all-space` option means ignore showing changes where spaces were changed. These are useful because space changes are not somethings that you care about most often and its a way of telling git to not show those changes to you while running the diff command. With the git diff command you can use the `--color-words` options to show the changes on the same line, but with the changes highlighted with different colors.

## Branching
Getting the most of git means using branches more often and effectively. In git branches are cheap, they don't cause a lot of headaches, its not a overhead at all when you create branches, they don't take a lot of processing power, not a lot of storage space, they are easy to create, delete and work with. The main purpose of using a branch is that they allow you to try out new ideas.

Lets say that you would like to try out a new idea, instead of doing it in the master branch and undoing commits if the new idea did not go out well, you can create a new branch and work on that. If the idea doesn't come out well then you can throw away that branch. If it did come out well then you can merge the new branch in which you were working with the master branch, meanwhile other people can be working on the master branch. This is the kind of flexibility that you get when you start using branches. When working with branches we just have one working copy, when we switch branches git will do fast context switching its going to take all of the files and folders in the working directory and match with the branch.

## Creating & showing branches
Running the command `git branch` will list all the branches of the project that are there in the local machine. The `*` character indicates which is the current branch that we are on. Its referred to as the current branch or the currently checked out branch. The point where HEAD points to can be found at `cat ~/.git/HEAD` which will show `ref: refs/heads/master`. What this file contains is reference to one of the branches, the master branch in this case. The output above means that I am pointing right now to the tip of the master branch. When we do `ls -alh ~/.git/refs/heads` we see a file listing of all the branches listed there. Every time you create a branch a new file in created in this folder and the contents of the file is the SHA value of the last commit in that branch. To create a new branch you do `git branch <branch-name>`. Some companies using hyphens to separate the words of the branch name and some use underscores. Creating a branch doesn't mean that you will automatically switch to that branch.

## Switching branches
To switch to the new branch that we create we have to do `git checkout <branch-name>`. Once you switch to the new branch the HEAD will point to the tip of this new branch. So when we do `cat ~/.git/HEAD` it will show `ref: refs/heads/<new-branch>`. If you follow that file and see the contents the SHA value will be the same because till now the tip of master branch and the new branch is the same, since we haven't added any new commits in the new branch of the master branch.

You're working directory must be mostly clean before you switch to a new branch. If your working directory has some changes that have not be commited yet the got will not allow you to switch branches. Because if you think about it lets say you have the master branch and a branch called sample, and you are currently in the sample branch and you have one file called index.html which has some changes. Now if you do `git checkout master` you are telling git to make your working directory look like the master branch, by which you will loose all the changes that you have made to the index.html file. You have got three options here.
- Discard the changes to the index.html file by `git checkout -- index.html`
- Commit the changes made to the index.html file to the current branch `git add index.html && git commit -m "Commit message"`
- You can stash the changes - we will talk about this later, it is like a pocket were we can put things in until later needed.

As I told you the working directory only needs to be mostly clean, because it doesn't have to be completely clean. It should be clean enough that there are no conflicts. For example lets say you are adding a new file in the current branch and you are switching to a new branch that wouldn't be a problem at all. Git won't allow the switching to happen if there is a possibility of loosing data.

## Creating & switching simultaneously
We have seen how to create a new branch and then switch to the new branch. In this we will take a look at how we can create and switch to that new branch simultaneously. To do this we run `git checkout -b <new-branch-name>` which will create and checkout to that new branch in a single step. You can think of the `-b` option as saying check this out as a new branch, its like put this stuff in my directory as a new branch. Its important to note here that whenever you create a new branch you are always creating from the branch that you are currently on. We can create branches from new branches that we create. So lets say you are on the master branch and you checkout to a new branch called x then you make 5 commits in the branch x, now after that you create a new branch from the branch x called y and make 5 more commits in the branch y. Now if you checkout to the master branch neither of the 10 changes will be there, if you checkout to the branch x then the last 5 changes will not be there. If you checkout to the branch y then all the changes will be there. So just remember that its important when creating a branch to see which branch you are currently working on, cause the new branch always branches out from the current branch.

## Comparing branches
If you remember we can use the git diff command to compare the two tree-ishes. A branch is also a tree-ish. So we can use the same command to compare two branches. Running the command `git diff master..new-branch` will just us the file changes between the tip of the master branch and the tip of the new-branch. Remember that we can pass any tree-ish this would also work `git diff master..new-branch^` which would give us the file changes between the tip of the master branch and the 2nd last commit of the new branch. Now we can also find whether one branch completely contains another branch or not. So when we run `git branch --merged` which will all branches that are completely included in the current branch we are on. So when we are in the new branch and execute the command it will show the master branch and the new branch (every branch is completely contained in itself). So lets say we have a master branch and we branch out of it called as x and we make 5 commits, then we branch out of x called as y and make 5 commits in it. Now when we run `git branch --merged` this will list master,x and y. If we checkout to the branch x and run the command it will list master and x. If we checkout to master and run the command it will list the master branch alone. While listing it will also indicate the current branch we are in with the `*` character.

The `--merged` is an option to the git branch command, git branch by default will list all the branches in the current working copy and the merged option restricts the results to just show the branches which are contained in the current branch. We can delete any branch that is contained by the current branch and the current branch won't be affected because it have all the commits of the branches that it contains, i.e when we are in branch y deleting x will not affect y because branch y contains all the commits that are in branch x. So the way how `git branch --merged` works is that it goes the way up the ancestor chain and sees which all branch tip is present, those branches alone are the branches that the current branch contains.

## Renaming branches
To rename a branch you use the git branch command with the `-m` or the `--move` option. Lets say we have the master branch from which we are branching out to a branch called new-feature and then we make 5 commits to clean the code. Well new-feature is really not a good name for a branch, we have to be descriptive about why we created a branch. To rename a branch `git branch -m <old-name> <new-name>`.

## Deleting branches
To delete a branch 1st you have to move to a different branch. Then you have to use the `-d` or the `--delete` option. Running the command `git branch -d <branch-name>` will delete the branch entirely. Its just like how you have to move to a different branch in a tree before you cut the branch that you are currently sitting on. Another things is that lets say we are in the master branch and we branch out to a new one called as x. Now lets say we make 5 commits here. Now lets say we checkout to the master branch and if we try to delete the branch x from here git will fail and it will tell you that you have made some changes in the branch x (those 5 commits) and those changes are not yet merged in the current branch, so you would loose the data of you delete that branch.

So if you really wanted to destroy those 5 change sets that you made and want to delete the branch x then git wants you to explicitly tell that by using the `-D` option instead of the `-d` option. You can think of the `-D` as the force delete option. The `-d` option will only work if the branch you are deleting is fully merged with the current branch you are on and the `-D` option doesn't require this condition. Its pretty easy to delete branches as you see in git, the only thing is that git gives you certain checks so that you don't do something dumb.

## Merging branches
Its good to make branches and try out new ideas, but now its time to learn how to merge the changes made in one branch to another. Lets say we have the master branch and to try out a new idea we branch out to a new branch called as branch x and lets say we work on our new feature there and we are committing the changes that we make along the way. Now we are done with this feature and we would like to merge the changes that we made in the branch x to the master branch. The first step is you must checkout to the branch in which you would like to bring in the changes. In this case we would like to bring in the changes made in the branch x to the master branch. So first we checkout to the master branch with `git checkout master`. To to merge the branch x into it we run the command `git merge x`. Now the branch x in merged into the branch master. We can check that by doing `git diff master..x` there will be no output, or we can also check that by running `git branch --merged` and we will see the branch x in the listing. Now if we want to we can completely delete the branch x by running `git branch -b x`.

Now in this case merging was easy actually, but merging can be a bit complicated and we should know how to deal with them. Because of this always make sure that you run git merge in a clean working directory, make sure you don't have any uncommitted changes before you run git merge, you can even stash them (we will see this a bit later), but always make sure you have a clean working directory which will give you a good clean workplace where you can sort out any problems which you might have while merging.

## Fast-forward merge
Before we proceed any further we need to understand the difference between a fast forward merge and a real merge. In the last example we looked at when we did a merge what actually happened was a fast forward merge. When merging the new branch back to master, the master branch did not have any commits after the point from where we branched out to the new branch. Master branch was just idle, we did not commit any changes to the master branch at all, as a result what we ended up with a fast forward merge. What git does is that when we merge a new branch into the current branch git starts from the tip of the new branch and goes up the ancestor chain to see if anywhere it can find the HEAD pointer. If it finds the HEAD pointer along the way the merge that happens is called as a fast forward merge, it is the safest of all, there are no problems that we need to deal with.

In a fast forward merge what happens that the HEAD pointer now is just made to point to the tip of last commit of the new branch. In other type of merges this is not actually the case, what actually happens is that git uses a set of merging rules and makes a commit called as the merge commit. In a fast forward merge there is no need to make a new commit.

When you know that a fast forward merge is what is going to happen, you can pass a couple of options to the git merge command. The `--no-ff` option meaning no fast forward tells forces git to make a merge commit anyway. You would run it like `git merge --no-ff <branch-name>`, which prevents a fast forward and make a merge commit anyway. The main reason why you wanna do is that if needed some kind of documentation in the git history that you in fact did do a merge. You have another `--ff-only` which means that do the merge only if you are able to do a fast forward merge. So if you are unsure whether or not a fast forward will happen or not and you want the merge to happen only if fast forwarding is possible then you can use this option.

## Real merge
A real merge is that kind of merge that happens when git is not able to find the HEAD pointer when it looks up the ancestor chain from the tip of the branch that we are trying to merge. In these cases git creates a new commit called as a merge commit and it does a really good job on choosing the best strategy for merging the changes. But sometimes in spite of its best efforts git fails. In these cases we will have to help git out to resolve the merge conflicts.

Lets say we have a master branch from which we branched out to a branch called as x. Now in branch x we make a change to the index.html file at the top and commit this change, now we checkout to the master branch and change the index.html file somewhere at the bottom and then commit this change, now if we try to merge the branch x into master branch git will not have any problems in merging them and it will do the real merge by itself. Conflicts only occurs when the code has changed in two branches in the same line numbers, because in this case git can't decide which one to use and we will have to help it. This is called as resolving a merge conflict. This is one issue that we have to take care when merging branches.

## Resolving merge conflicts
Whenever you trying merging and there is a merge conflict git reports the files in which the merge conflict occurred. Now when you run `git status` it will show you the unmerged paths. We are now in the middle of a merge, the merge is not yet completed, git needs some help to complete this real merge. So we need to open the file and fix the problem. Lets say you are trying to merge the sample branch into the master branch and there was a merge conflict in the index.html file. Now in the index.html file the contents would look like this after you run `git merge sample` from the master branch.

There are choices that you have when you need to resolve a merge
- Abort the merge (I don't want the merge to happen, I wasn't not anticipating these problems get me out of here)
- Resolve the conflicts manually (Initially when  you are learning I suggest you to start out with this)
- Use a merge tool to resolve the conflicts

To abort the merge you just run the command `git merge --abort`. You will go back to the state before you ran the git merge command, the merge will be aborted. You can resolve the conflicts manually by opening the index.html file and the editing the way it needs to look. Now save the file and add index.html file to the staging index `git add index.html`. If you have 10 files with merge conflict then you have to manually change all the 10 files and then add all of them to the staging area before you make a commit. Normally when you commit you give it a message, here also you can give a message but you don't need to, when you are in the middle of a merge git has a standard default message that it would use. So just run `git commit`, it might pop up the default text editor and ask give you an option if you would like to change the commit message, you can just click save and close for the merge to complete. The merge was successful you can check that by running `git branch --merged` and see that the sample branch is there in the list. Now you can remove the sample branch if you want to.

You could also use a merge tool to resolve conflicts instead of doing it manually. To see the list of merge tools available you can run `git mergetool` to see the list of merge tools available. When you are in the middle o a merge and you want to use the merge tool for the merge you can run `git mergetool --tool=<tool-name>`. You can also add a merge toll to your git config file if you want to always use a certain tool.

## Strategies to reduce conflicts
The following strategies can be helpful to reduce the possibility of a merge conflict and also make it easier to resolve a merge conflict.
1. Keep lines short
1. Keep commits small and focused
1. Beware stray edits to white space
1. Merge often
1. Track changes to master - as changes happen in master, keep bringing those changes into your branch

The last technique is very important when you are working with a lot of team members. When you are working in a new branch and other are changing the master branch, its a good idea to merge the master branch into the new branch and keep in in sync with the master branch, this will help to reduce the merge conflicts when you merge the new branch into the master branch. Since the new branch has most of the changes that are incorporated in the master already and it will reduce the number of conflicts you when you merge back the new branch in master.

## Saving in the stash
The stash is a place where we can store changes temporarily without having to commit them to the repository. Its a lot like putting something in a locker to save it for a later. The stash is not a part of the working area, staging index or the repository, its a separate full area in git separate from others. The things that we put into it aren't commits, bu they are a lot like commits. They work in a very similar way. There are still a snapshot of the changes but they don't have a SHA value associated with them. Lets try making a change and storing it in the stash.

One typical use case of when stashing would come in handy would be when you needs to switch to a different branch but you have some changes that you are not quite ready to turn into a commit yet, so you can stash them instead. You run the following command to add the changes to the stash `git stash save "This is the message"`, note here that you need not provide the `-m` option for the message you can give it directly. After it puts the changes into the stash git does a `git reset --hard HEAD` to take whatever is in the repo and put it in the staging index and the working area. If you had untracked file to stash them also you need to pass the `--include-untracked` option, but you rarely you this options because having untracked files doesn't prevent you from switching branches.

## Looking at the stash
To see the list of things in the stash you can run `git stash list` to see the changes added to the stash. You see the message that you added while saving to the stash in the listing. In the listing every stash has an identifier that we need to use to refer to a stash. The identifier have a naming rule they follow the pattern `stash@{index}` where index in the number starting from 0.

Next it also shows the name of the branch from which we saved the changes to the stash, because stash is available in all branches. This is very handy because lets say you start working on a branch and you realize that this isn't the branch in which you wanna make the commit then you can add the changes to the stash, checkout to a new branch and pull the changes from the stash there, and then make a commit in that branch. This is another use case of when you would use a stash. To know more about a stash run the command `git stash show <stash-identifier>`, and by default it comes and shows whats called as a diff stat, i.e shows only statistics on what was changed. To see more information about the stash you can use the `-p` patch option.

## Pulling from the stash
Now lets take a look at how we can pull the change set from the stash. Now in whichever branch we are on pulling the changes set from the stash is going to bring the changes to the working directory. It will try to bring in the files from the stash and apply it in the working directory, just like merges there may be conflicts. There are two commands that we can use to pull items from the stash, we can use the `git stash pop <stash-identifier>` or the `git stash apply <stash-identifier>` command, both of them will pull whats in the stash and put it in the working directory.

The differences between these two commands is the stash pop will also pull the change set out from the stash and stash apply will leave the copy of change set there in the stash. If we don't give a stash identifier by default git is going to use the first one. Git stash apply is used in places where we would like a change set to be applied to multiple branches so we switch between branches and apply it in one by one, or in places where you would like at apply a change some after doing some commits and then again after doing some commits and so on, but mostly these uses cases are very rare and you will be only using `git stash pop <stash-identifier>` command.

## Deleting from the stash
To remove a change set from the stash we run the command `git stash drop <stash-identifier>`. Clearing everything in the stash would be useful in certain cases like, lets say you are working on a feature and you stashed that, but someone else on the team has already completed that feature and you no longer have to work on that anymore. We can delete everything in the stash all at once simply by running the command `git stash clear`.

## Remotes
Remote repositories in git are also called as remotes. Everything that we have worked on so far is on our local computer, we don't require network connection. We can just do version control locally and not share it with anyone, its perfectly fine and git allows us to do that. But it becomes even more powerful when we start collaborating with others and thats what remotes allow us to do. The basic concept it that we have a remote server in which we will put our changes so that others can see them. They can the download the changes that we have made to their repositories make changes on theirs and upload them to the remote server and we can pull those changes down to our repository to get their changes. The remote repository if just a git repository, nothing magical is going on here. Git is distributed version control there is no real difference between different repositories. It makes the remote repository as a sort of the central clearing house for all the changes that are going on.

So lets say we have our master branch with us in our local copy. So when we do a push the remote server creates the same master branch with the same commits. At the same time git also makes a branch called `origin/<branch-name>` (called as a remote branch) in our local working copy, this is by default we can change that name it doesn't need to be origin, this new branch references the remote server branch. It always tries to stay in sync with that. So every time when we do a push the local copy makes a note of the change in the remote server and syncs the remote branch with it. When other people push their changes to the remote server we need to know about them and pull that down in our working copy. This is called as a fetch, when we do this the new changes comes in the remote branch.

Fetch is essentially telling git sync my remote branch with the remote server, but it does not bring it into our master branch. We have to manually do a merge to bring the changes into our master branch. The remote branch is not duplicated, the commit objects are not duplicated by git, git is always smart enough to use pointer effectively instead of duplication. The remote branch is just like other branch, the only thing is that whenever you do a push or a fetch it tries to stay in sync with the remote branch. This is the usual work flow when you are working with a remote repository.
1. Do the changes locally
1. Fetch the latest from the remote server - gets the remote branch in sync
1. Merge any work you did with just what came down from the server
1. Push the result back up to the remote server

## Adding remotes
You can run the `git remote` command to get the list of remotes that git knows about. To add a remote we run the following command `git remote add <alias> <url>`, the alias is what name we wanna give the remote and the url is the endopint where git can find that remote. So if we give the alias as origin then this name `origin` will be the way in which we reference the remote repository, because since we have have many remotes we don't want to keep giving the full url to identify a remote every time we want to use it. By convention we call the primary remote as `origin`, this is just convention. Once you have run this command of adding a remote, when you run the `git remote` command you can find the alias in the listing to confirm it.

You can also the `-v` option to get more information while listing the remotes, it will show the url that its going to use for fetching and url that it will use for pushing, typically these are going to be the same urls but it doesn't have to be, we can even have them as different endpoints, git is so much flexible and powerful. For example we could have a read only remote that we are fetching from and for pushing we can link to the endpoint with write access.

When you do `cat ~/.git/config` it will show the list of remotes there. To remove a remote all that you do is `git remote rm <alias>`. Adding a remote is just to let the local repository know about the presence of the remote repository, adding a remote does not pull or push the changes. So far all that we have done is just create a way in which the local repository has the ability to communicate with the remote repository.

## Creating a remote branch
When you run the command `git push -u origin master`, this means that push the master branch to the remote called origin. It compresses the master branch and pushes it to the remote, and then writes the objects on the remote server and once its done with all of these it creates a new branch locally. When you do `cat ~/.git/config` these is a branch definition here and the branch has a remote which is origin. When you do `ls -alh ~/.git/refs/remotes` you can see that there is a directory create for every remote you create. We see the branches normally with `git branch` command, you can use the `-r` option to see the remote branches, to see all the branches you can use the `-a` option.

## Cloning a remote
Earlier we already has a project that were working on and we added a remote in that. Now lets say we are a new team member joining a company and we want to start contributing so how to we pull down the existing project first. We would run the `git clone <url> <folder-name>`, the folder name argument is optional and if we don't give that git will automatically use the project name as the folder name. By default git will pull down only the default branch that is set on the remote, github sets the default branch as the master branch, which we can change if we want. To bring down specific branches from the remote we can use the `-b` option and specify the branches while doing git clone.
