---
title: Programming in go
tags:
---
## Introduction
Go is an open source general purpose programming language that makes it easy to build simple, reliable, and efficient software. It is a language with advanced features and a clean syntax. It is widely available on a number of platforms and has a robust well documented common library and focuses on good software engineering principles.

## Installing Go
We need to install the Go toolset before we begin working in Go. Before installing the Go toolset lets do some preparation work. The Go toolset uses an environment variable called GOPATH to find Go source code. We can set the GOPATH to anything we want, but to make things a little bit easier let set it to our home directory. If you are on a mac open the terminal and enter the following.
```sh
echo 'export GOPATH=$HOME\n' >> ~/.zshrc
```
Close the terminal, reopen it and enter `env` to the list of environment variables. You should see an entry for GOPATH. Now head over to the official [downloads](golang.org/dl) page and run the installer for your platform. To confirm the installation run `go version` from the command line. The Go toolset is made up of several different commands and subcommands. You can pull up a list of those commands by `go help`. Mac users can also install Go from the command line using the brew package manager `brew install go`. I have personally installed Go in my machine through homebrew as it will allow me to easily upgrade to a newer version by just running `brew upgrade go`.
