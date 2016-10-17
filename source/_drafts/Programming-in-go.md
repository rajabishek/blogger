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

## First program
Lets write the typical first hello world program in Go.
```go
package main

import "fmt"

func main() {
    fmt.Println("Hello world from Raj Abishek")
}
```
You can save the code in a file called code.go and then we can execute the file by running `go run code.go`. Ok the where is the compiler binary ? Is Go an interpreted programming language ? No, the go run command takes the subsequent files (separated by spaces), compiles them into an executable saved in a temporary directory, and then runs the program. Its like Javascript, every time we run the program the code is compiled. If you had made some mistake somewhere while typing the Go compiler will give you hints about where the mistake lies. Like most compilers, the Go compiler is extremely pedantic and has no tolerance for mistakes.

## Understanding Hello world
```go
package main

import "fmt"

func main() {
    fmt.Println("Hello world from Raj Abishek")
}
```
The `package main` at the top is a package declaration. Packages are Go’s way of organizing and reusing code. For now, just make sure to include this line in any program you write. Go doesn’t care about whitespace we use it to make programs easier to read. The `import "fmt"` imports the `fmt` package. The import keyword is how we include code from other packages to use with our program. The `fmt` package (shorthand for format) implements formatting for input and output. The `fmt` package’s files would contain `package fmt` at the top of them. It is important to remember here that when we import a package we always provide a string literal. Notice that `fmt` is surrounded by double quotes.

Function definitions in Go start with the `func` keyword followed by the name of the function (main, in this case), a list of zero or more parameters surrounded by parentheses, an optional return type, and a body which is surrounded by curly braces. This function has no parameters, doesn’t return anything, and has only one statement. We had to name the function as `main` because that is the first function that gets called when you execute the program. To print the contents onto the console we do `fmt.Println("Ouput to console")`. We are accessing the Println function inside the fmt package and invoking it using one string argument.

To find documentation details about a specific function in a package run the command `godoc <package-name> <function-name>`.
