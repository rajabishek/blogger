---
title: Mastering Vim
tags:
---
## Introduction
Vim is an extension of the Vi editor. Vi has been in existence since a very long time. Vim however is much more recent. It was created by ** Bram Moolenaar**.

I use vim for almost everything today programming, writing articles, writing notes etc. In fact this blog article was itself written using the vim editor. I must state here very early that vim does have a huge learning curve, but with a little bit of patience and practice you will be able to master this wonderful tool.

If you don't like vim, its perfectly fine, after all we use all these tools just to feel more comfortable and be more productive. If you feel vim is disturbing your workflow and it doesn't suit your need, its absolutely ok.

## Modes
Vim works with the concept of modes. We can start writing code or text in the file in the insert mode. Then we also have the command mode in which we enter command for the vim editor to perform some action. We will be changing between these two modes a lot. The default mode in vim is the command mode. So to enter into insert mode you need to enter the command `i`. To get back to the command mode we simple press the `Esc` key.

Now to save the file from the command mode you can press `:`  which will open a mini buffer in which we can type commands. To save the file in the buffer type `w filename.txt` and press enter key. `w` is the short form for `write`. To quit the vim program you can open the mini buffer and type `q` and click enter. `q` is the short form for `quit`.
