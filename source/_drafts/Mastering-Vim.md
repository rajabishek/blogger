---
title: Mastering Vim
tags:
---
## Introduction
Vim is an extension of the Vi editor. Vi has been in existence since a very long time. Vim however is much more recent. It was created by ** Bram Moolenaar**.

I use vim for almost everything today, from programming to writing articles, writing notes etc. In fact this blog article was itself written using the vim editor. I must state here very early that vim does have a huge learning curve, but with a little bit of patience and practice you will be able to master this wonderful tool.

<!-- more -->

If you don't like vim, its perfectly fine. After all these tools were discovered only to make us more productive and feel comfortable. If vim is disturbing your workflow and doesn't suit your needs, its absolutely fine.

## Modes
Vim works with the concept of modes. We can start writing code or text in the file in the **insert mode**. Then we also have the **command mode** which allows us to type commands that acts over the underlying text. We will be changing between these two modes a lot. The default mode in vim is the command mode. So to enter into insert mode you need to enter the command `i`. To get back to the command mode we simple press the `Esc` key.

Now to save the file, you can press `:` from the command mode which will open a mini buffer in which we can type commands. To save the file in the buffer type `w filename.txt` and press enter key. `w` is the short form for `write`. To quit the vim program you can open the mini buffer and type `q` and click enter. `q` is the short form for `quit`. You can also type `wq` and press enter that will write and quit at the same time. If you try to quit from a file that is not yet saved vim will prevent you from quitting, but if you are very sure about quitting and not saving the file you can type `q!` and press enter which means quit without saving.

## Faster Movement
When in the command mode you can press the `h` key to move left. `l` key to move right. `j` key to move down and `k` key to move up in the file. If you are comfortable with the arrow keys you can use that to navigate in the file itself. If you would like to know more about why these specific keys were chosen for navigation have a look at this [article](http://www.catonmat.net/blog/why-vim-uses-hjkl-as-arrow-keys).

When in command mode we can press the `w` key to move from word to word, a period is also considered as a word. To go back a word you type the `b` key. If you want to jump full words i.e sequences separated by spaces then you can use the `W` key and for moving back full word you can use the `B` key.

You can press the `$` key to move to the end of the line and you can hit the `^` key to move the 1st non space letter on the line and you can hit the `0` key to move to the real beginning of the line. In vim you can hit `gg` from the command mode to go to the beginning of the line and you can hit `G` to move to the end of the file. You can use the `}` key to move to the next paragraph and `{` key to move to the previous paragraph.

You can press the `f<character>` to move forward to the first occurrence of the character in the line. You can press the `F<character>` to move backward to the first occurrence of the character in the line. You have 3 different way to move to a specific line number in vim. To show the line numbers open the mini buffer in command mode by pressing `:` and type `set number` and press enter. Now to move to a specific line number you can type `n gg` or `n G` from the command mode, or you can open the mini buffer and type `n` and press enter. In fact this applies for all commands you can type a number n followed by the command to repeat the command n times.

## Basic Editing
From the command mode you can enter into the mini buffer and type `e <filepath>` to open the file in vim. There is a special file called as `.vimrc` in the home folder. The `.vimrc` is a configuration file that persists you preferences for using the vim editor. Any command that you enter in the mini buffer can be put in this `.vimrc` file. For example the configuration `set number` will make sure that vim shows you the line number in the file.

If you press the `x` key from the command mode it will delete the character under the cursor. You can hit `dw` to delete the following word and `db` is used to delete the previous word in vim. You can hit `u` to undo an action in vim. If you type `cw` you will delete the word and enter into insert mode this is helpful for replacing a word in vim.

You can hit `dd` to delete the whole line in vim and hit `cc` to delete the whole line and enter into insert mode. This can be applied with the repeater technique mentioned previously. If you press `2dd` it will delete 2 lines and similarly pressing `2cc` will delete 2 line and get into insert mode.
