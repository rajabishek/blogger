---
title: Version control with git
tags:
---

## Why do I need version control?
Version control is a system which records and stores every change made to a set of files, so that you can go back to a previous state at any time. Developers have been using this method for a long time (the first kind of version control system was developed in the 70s) and it is now unthinkable to seriously write software without one.

<!-- more -->

## Installation
Before installing git you might want to check whether git is already installed. You can open the terminal and type `git --version` to check the exact version that you have or you could do `which git` to find the location of git. If you don't have git installed, then you can head over to the downloads section of the official git [website](https://git-scm.com/downloads) and download the git installer based on your operating system to install git on your computer.

## Initial Configuration
Before we configure git to suit our needs we need to know that git allows us to provide configuration at 3 different levels.
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
