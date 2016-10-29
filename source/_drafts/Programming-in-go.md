---
title: Programming in go
tags:
---
## Introduction
Go is an open source programming language that makes it easy to build simple, reliable, and efficient software. It is widely available on a number of platforms and has a robust well documented common library and focuses on good software engineering principles.

Go was created in 2007 at Google by **Robert Griesemer**, **Rob Pike**, and **Ken Thompson** as an experimental project. Go combines the development speed of working in a dynamic language like Python with the performance and safety of a compiled language like C or C++.

## Go toolset
We need to install the Go toolset before we begin working in Go. Before installing the Go toolset lets do some preparation work. The Go toolset uses an environment variable called `GOPATH` to find the Go source code. We can set the `GOPATH` to anything we want, but to make things a little bit easier let set it to our home directory. If you are on a mac open the terminal and enter the following.
```sh
echo 'export GOPATH=$HOME\n' >> ~/.zshrc
```
Close the terminal, reopen it and enter `env` to the list of environment variables. You should see an entry for `GOPATH`. Now head over to the official [downloads](golang.org/dl) page and run the installer for your platform. To confirm the installation run `go version` from the command line. The Go toolset is made up of several different commands and subcommands. You can pull up a list of those commands by `go help`.

Mac users can also install Go from the command line using homebrew by running `brew install go`. I have personally installed Go in my machine through homebrew as it will easily allow me to upgrade to a newer version by just running `brew upgrade go`.

## First program
Lets write the typical first hello world program in Go.
```go
package main

import "fmt"

func main() {
    fmt.Println("Hello world from Raj Abishek")
}
```
You can save the code in a file called `code.go` and then we can execute the file by running `go run code.go`. Ok, I see no compiled binary then is Go an interpreted language ? No, the `go run` command takes the subsequent files (separated by spaces), compiles them into an executable saved in a temporary directory, and then runs the program. Its like Javascript, every time we run the program the code is compiled.

If you had made some mistake somewhere while typing the program, the compiler will give you hints about where the mistake lies. Like most compilers, the Go compiler is extremely scrupulous and does not tolerate any mistakes.

## Understanding Hello world
```go
package main

import "fmt"

func main() {
    fmt.Println("Hello world from Raj Abishek")
}
```
The `package main` at the top is a package declaration. Packages are Go’s way of organizing and reusing code. For now, just make sure to include this line in any program you write.

Go doesn’t care about whitespace. We use whitespaces to make programs more readable. The `import "fmt"` imports the `fmt` package(short for format). The import keyword is how we include code from other packages to use with our program. The `fmt` package implements formatting for input and output. The `fmt` package’s files would contain `package fmt` at the top of them.

It is important to remember here that when we import a package we always provide a string literal. Notice that `fmt` is surrounded by double quotes. Anything surrounded in double quotes is known as a string literal, which is a type of expression.

We define functions in Go with the `func` keyword followed by the name of the function(main, in this case), a list of zero or more parameters surrounded by parentheses, an optional return type, and a body which is surrounded by curly braces. The main function we defined above has no parameters, doesn’t return anything, and has only one statement.

We had to name the function as `main` because that is the first function that gets called when you execute the Go program. To print the contents out to the console we do `fmt.Println("Output to console")`. We are accessing the Println function inside the fmt package and invoking it using one string argument.

To find documentation details about a specific function in a package run the command `godoc <package-name> <function-name>`. If we deliberately read out the program that we just wrote out loud, it would go like this.
> Create a new Go program that references the fmt library and contains one function called main. That function takes no arguments and doesn’t return anything. It accesses the Println function from the fmt package and invokes it using one string argument.

## Data Types
Go is a statically typed programming language. Variables always have a specific type and that type cannot change. In every programming language you need some way to represent numbers(integers and floating point numbers), strings or characters, and booleans. Lets see how Go deals with these type of data.

### Integers
Generally, we split numbers into two different kinds integers and floating-point numbers. Go’s integer types are `uint8`, `uint16`, `uint32`, `uint64`, `int8`, `int16`, `int32`, and `int64`. The number at the end of each type tells us how many bits each of the types use. uint means **unsigned integer** while int means **signed integer**. In addition, there two alias types `byte`(which is the same as `uint8`) and `rune`(which is the same as `int32`).

There are also three machine dependent integer types `uint`, `int`, and `uintptr`. They are machine dependent because their size depends on the type of architecture you are using. Generally, if you are working with integers, you should just use the `int` datatype type.

## Floating point numbers
Floating-point numbers are numbers that contain a decimal component. Go has two floating point types `float32` and `float64` (also often referred to as single precision and double precision, respectively).

It also has two additional types for representing complex numbers (numbers with imaginary parts) `complex64` and `complex128`. Generally, we should stick with `float64` when working with floating point numbers.

## Strings
A string is a sequence of characters with a definite length used to represent text. String literals can be created using double quotes `"Raj Abishek"` or backticks `Raj Abishek`. The difference between these is that double quoted version cannot contain newlines but they allow special escape sequences to be used like `\n` for new line and `\t` for a tab.
```go
package main
import "fmt"
func main() {
    fmt.Println(len("Raj Abishek")) // gets the length of the string
    fmt.Println("Raj Abishek"[0]) // accesses the first character in the string
    fmt.Println("Raj " + "Abishek") // concatenates the two strings together
}
```
Notice that you see 82 instead of R when you run this program. This is because the character is represented by a byte (remember a byte is an integer).

## Booleans
A boolean value (named after George Boole) is a special 1-bit integer type used to represent `true` and `false` (or on and off). Three logical operators are used with boolean values `&&`, `||` and `!`.
