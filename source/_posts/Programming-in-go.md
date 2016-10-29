---
title: Programming in go
date: 2016-10-29 16:17:32
tags:
---

## Introduction
Go is an open source programming language that makes it easy to build simple, reliable, and efficient software. It is widely available on a number of platforms and has a robust well documented common library and focuses on good software engineering principles.

<!-- more -->

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
Floating-point numbers are numbers that contain a decimal component. Go has two floating point types `float32` and `float64` (also often referred to as single precision and double precision, respectively). Generally, we should stick with `float64` when working with floating point numbers.

Go also has two additional types for representing complex numbers(numbers with imaginary parts) `complex64` and `complex128`.

## Strings
A string is a sequence of characters with a definite length used to represent textual data. String literals can be created using double quotes `"Raj Abishek"` or backticks `Raj Abishek`. The difference between these is that double quoted version cannot contain newlines but they allow special escape sequences to be used like `\n` for new line and `\t` for a tab.
```go
package main
import "fmt"
func main() {
    fmt.Println(len("Raj Abishek")) // gets the length of the string
    fmt.Println("Raj Abishek"[0]) // accesses the first character in the string
    fmt.Println("Raj " + "Abishek") // concatenates the two strings together
}
```
Notice that in the output for the second print statement you see `82` instead of `R`. This is because the character is represented by a byte in Go (byte is an integer).

## Booleans
A boolean value is a special 1-bit integer type used to represent `true` and `false` (or on and off). Three logical operators are used with boolean values `&&`, `||` and `!` which currespond to the boolean operation `AND`, `OR` and `NEGATION` respectively.

## Variables
A variable is a storage location, with a specific type and an associated name. Variables in Go are created by first using the var keyword, then specifying the variable name(message) and the type(string), and finally, assigning a literal value to the variable.
```go
package main
import "fmt"
func main() {
    var message string = "Hello world from Raj Abishek"
    fmt.Println(message)
}
```
Assigning a value is optional. As shown below we can split into two statements, one that declares the variable and another that assigns a value. Variables can change their value throughout the lifetime of a program.
```go
package main
import "fmt"
func main() {
    var message string //Declare a variable called message that can hold string values
    message = "Hello world" //Assigns a value to the message variable
    fmt.Println(message)

    message = message + " from Raj Abishek" //Re assign a new value to the message variable
    fmt.Println(message)
}
```
Because creating a new variable with a starting value is so common, Go also supports a shorter statement.
```go
message := "Raj Abishek"
```
`:` is required before the `=`, this is how Go compiler knows that this is a variable declaration and not an assignment expression. Also observe that no type was specified, the type is not necessary because the Go compiler can infer the type based on the literal value you assign the variable.

Because we are assigning a string literal, message is given the type string. This is called as type inference. This is present in many other modern programming languages like Scala, Swift also. The compiler can also do type inference with the var statement:
```go
var message = "Raj Abishek"
```
Generally you should use the `:=` shorter form whenever possible since as it is seen as the idiomatic usage of the language. It is important to remember that type inference will work only if you provide an initial value, because the only way for the compiler to infer the data type in from the initial value. The following Go code is invalid an will not compile.
```go
var message
```
Variable names must start with a letter and may contain letters, numbers, or the underscore symbol. camelCase is the preferred way to name the variables in Go.
```go
name := "Raj Abishek"
fmt.Println("My name is", name)
```

## Constants
Constants are essentially variables whose values cannot be changed later. You use the `const` keyword instead of the `var` keyword for creating them.
```go
package main
import "fmt"
func main() {
    const name string = "Raj Abishek"
    fmt.Println(name)
}
```
If you try to re assign a constant then it results in a compile time error. Constants are a good way to reuse common values in a program without writing out each time. For example, `Pi` in the `math` package is defined as a constant.

Go also has another shorthand when you need to define multiple variables. Use the keyword `var`(or `const`) followed by parentheses with each variable on its own line as shown below.
```go
var (
    name = "Raj Abishek"
    message = "Hello world"
    age = 20
)
```

## Scope
The range of places where you are allowed to use a variable is called the scope of the variable. Like Java, C and C++, Go is **lexically scoped using blocks**. This means that the variable exists within the nearest curly braces ({}), or block, including any nested curly braces (blocks), but not outside of them.
```go
package main
import "fmt"

message := "Hello world"

func main() {
  name := "Raj Abishek"
  fmt.Println(name)
  fmt.Println(message)
}

func another() {
    fmt.Println(message)
    fmt.Println(name) //This statement will result in a compile time error
}
```

## Iteration & Loops
The for statement allows us to repeat a list of statements (a block) multiple times. The following is equivalent to while loops present in other programming languages.
```go
package main
import "fmt"
func main() {
    i := 1
    for i <= 10 {
        fmt.Println(i)
        i = i + 1
    }
}
```
The above code prints the numbers from 1 to 10 in ascending order. Other programming languages have a lot of different types of loops (while, do, until, foreach, ...) but Go only has one that can be used in a variety of different ways. The previous program could also have been written like this. This is equivalent to the for loop present in other languages.
```go
package main
import "fmt"
func main() {
    for i := 1; i<=10; i++ {
        fmt.Println(i)
    }
}
```

## The if statement
We can choose to do different things based on a condition. For that, we use the if statement. The else part is optional like in other programming languages. If the condition in the if evaluates to true, then the block after the condition is run; otherwise, either the block is skipped, or if the else block is present then that block is run.
```go
if i % 2 == 0 {
    // even
} else {
    // odd
}
```
If statements can also have else if parts as shown below.
```go
if i % 2 == 0 {
    // divisible by 2
} else if i % 3 == 0 {
    // divisible by 3
} else if i % 4 == 0 {
    // divisible by 4
}
```
Like in other languages the conditions are checked top down and the first one to result in true will have its associated block executed and none of the other blocks will execute. A sample program to print only the even number from 1 to 10 is shown below.
```go
package main
import "fmt"
func main() {
    for i:=1; i <= 10; i++ {
        if i % 2 == 0 {
            fmt.Println(i, " ")
        }
    }
}
```

## Switch statement
To write a program that printed the English names for numbers from 1 to 5 if we used if statements then we would have a clumsy code. We would have a lot of else if statements and the program would like hard to maintain and make it is less readable. Instead we could use the switch statement in Go. We would write the program like this:
```go
switch i {
    case 0: fmt.Println("Zero")
    case 1: fmt.Println("One")
    case 2: fmt.Println("Two")
    case 3: fmt.Println("Three")
    case 4: fmt.Println("Four")
    case 5: fmt.Println("Five")
    default: fmt.Println("Unknown Number")
}
```
Like an if statement, each case is checked top down and the first one to succeed is chosen. A switch also supports a default case that will happen if none of the cases matches the value (similar to how the else works in an if statement).

Go's switch statement is also considerably more powerful than its counterpart in many C-like languages. Because the cases of a switch statement do not fall through to the next case in Go, it avoids common C errors caused by missing break statements.

## Arrays
An array is a ordered sequence of items of a single type with a fixed length.
```go
package main
import "fmt"
func main() {
    var data [5]int //declares an array called data of 5 integers
    data[4] = 100
    fmt.Println(data)
}
```
You should see the output `[0 0 0 0 100]`. Array elements can be accessed using their indexes. The index starts from zero. To access the nth element we use `data[n-1]`. A sample program to get the average of the elements of an integer array is shown below.
```go
package main
import "fmt"
func main() {
    var data [4]float64
    data[0] = 10
    data[1] = 20
    data[2] = 30
    data[3] = 40
    var total float64 = 0 //Or we could do total := 0.0
    length := len(data)
    for i:=0; i < length; i++ {
            total += data[i] //#1
    }
    fmt.Println(total / float64(length)) //#2
}
```
There are some important observations to make in the above code. Firstly we did not declare the variable using shorthand `total := 0` in the above code because then `total` would have inferred to be of the type `int`. Since we want total to be of type `float64` so that we can add the `data[i]` while totaling and divide by `float64(length)` while computing the average, we explicitly mentioned its type as `float64` using the var statement. If we wrote the code as `total := 0` then  we would get compile time error due to line 1 and line 2 due to mismatched types `int` and `float64`.

But what we can do is `total := 0.0`. In this way the Go compiler would infer the type of total as `float64` since `0.0` literal is seen as a double precision value. Next we have the `len` function that returns the length of the array as an `int`. But since `total` is of type `float64` we cannot directly divide by `length`. Go doesn't allow us to operate between two mismatching data types. We need to convert length into a `float64` which is done by `float64(length)`. This is called as type conversion. In general, to convert between types, you use the type name like a function.

We can also use a special form of a for loop with array in Go.
```go
total := 0.0
for i, value := range data {
    total += value
}
fmt.Println(total / float64(len(data)))
```
As you can see above with this variation of the loop `i` and `value` represents the index and the value of each iteration. At every iteration `i` is the index and `value` in data[index]. We use the keyword `range` followed by the name of the variable we want to loop over. But when we compile the above program and run it will result in a compile time error because Go doesn't allow us to create variables that we never use. The `i` was never used inside of the for loop and therefore we have to replace it with a single underscore to tell the compiler that we don’t need this. The modified program would be:
```go
total := 0.0
for _, value := range data {
    total += value
}
fmt.Println(total / float64(len(data)))
```
As we had a shorthand syntax to create variables with initial values, we can also in a similar way create array variables with initial values.
```go
data := [4]float64{ 10, 20, 30, 40 }
collection := [4]float64 {
    100,
    200,
    300,
    400,
}
```
As you can see above we need not force the declaration on a single line. We can break up into multiple line however the extra trailing `,` after 400 is required by Go. It allows us to easily remove an element from the array by commenting out the line.

As you can see above while declaring the array we have to hardcode the length of the array. We cannot change the size of an array once it is declared. Because of this and other limitations, you rarely see arrays used directly in Go code. Instead we usually use something called as a slice, which is data type build on top of an array.

## Slices
A slice is a segment of an array. Like arrays, slices are indexable and have a length. Unlike arrays, this length is allowed to change. We declare a slice as follows. We do not put the length or the number of elements inside the square brackets.
```go
var data []float64
```
As you can see above we have created a slice called data with a length of zero. To create a size with a length we use the built in make function.
```go
data := make([]float64, 5)
```
As you can see above we have created a slice that is associated with an underlying `float64` array of length `5`. Slices are always associated with some array, and although they can never be longer than the array, they can be smaller. The make function also allows a third parameter that represents the capacity of the underlying array that the slice points to.
```go
data := make([]float64, 5, 10)
```
In the above code we have create a slice of length `5` that is associated with an underlying `float64` array of length `10`. Another way to create slices is to use the ``[low:high]`` expression from an existing array. The `low` is the index of where to start the slice and `high` is the index of where to end it(but not including the index itself). It is similar to slicing sequences in Python except that we don't have negative indexing here.
```go
array := [5]float64{ 1, 2, 3, 4, 5 }
slice := array[0:5]
```
When we do `array[0:5]` returns `[1, 2, 3, 4, 5]`, `array[1:4]` returns `[2, 3, 4]`. For convenience, we are also allowed to omit low, high, or even both low and high. `array[0:]` is the same as `array[0:len(array)]`, `array[:n]` is the same as `array[0:n]`, and `array[:]` is the same as `array[0:len(arr)]`. In addition to indexing Go includes two built in functions to assist with slices: `append` and `copy`.

To append elements to the end of slice we use the `append` function. If there is space in the underlying array the element is added after the last element and the length of the slice is incremented. If there is no space in the underlying array then a new array is created and the existing elements are copied over to the new array, the new element is added to the end and then the new slice is returned.
```go
func main() {
    slice1 := []int{1, 2, 3} //shorthand form to create a new slice from initial values
    slice2 := append(slice1, 4, 5)
    fmt.Println(slice1, slice2)
}
```
As you can see from the above code if you omit the length of the elements inside the square bracket that is the shorthand from for creating a new slice with initial values. `slice1` has `[1, 2, 3]` and `slice2` has `[1, 2, 3, 4, 5]`. The `append` function creates a new slice by taking an existing slice(the first argument) and appending all the following arguments to it.

The `copy` function in Go takes two arguments `dst` and `src`. All of the entries in `src` are copied into `dst` overwriting whatever is there. If the lengths of the two slices are not the same, the smaller of the two will be used.
```go
func main() {
    slice1 := []int{1, 2, 3}
    slice2 := make([]int, 2)
    copy(slice2, slice1)
    fmt.Println(slice1, slice2)
}
```
On running the above program `slice1` has `[1, 2, 3]` and `slice2` has `[1, 2]`. The contents of `slice1` are copied into `slice2`, but because `slice2` has room for only two elements, only the first two elements of `slice1` are copied.

## Maps
A map is an unordered collection of key value pairs (maps are also sometimes called associative arrays, hash tables, or dictionaries). Maps are used to look up a value by its associated key. Here’s an example of a map in Go. To create a map in Go we have to provide the datatype of both the key and the value.
```go
var data map[string]int
```
The above code create a map with the type of keys as `string` and the type of values as `int`. Maps have to be initialized before they are used in the program, or else we would get a run time error.
```go
data := make(map[string]int)
data["key"] = 10
fmt.Println(data["key"])
```
The length of a map(found by doing len(data)) can change as we add new items to it. We can use the `delete` function to delete items from a map.
```go
delete(data, "key")
```
Suppose we tried to look up an element that doesn’t exist then a map returns the zero value for the value type(which for strings is the empty string). The zero value for integer type is 0. Although we could check for the zero value in a condition (data["jsjsjs"] == 0), Go provides a better way.
```go
number, ok := data["jsjsjs"]
fmt.Println(number, ok)
```
The first value is the result of the lookup, the second tells us whether or not the lookup was successful. Here since we have no key called `jsjsjs` `number` will be zero and `ok` will be false. In Go programs we would often see code like this.
```go
if number, ok := data["jsjsjs"]; ok {
    fmt.Println(number, ok)
}
```
We try to get the value from the map, if successful then we execute the code block. The shorthand form to create map in Go is like this.
```go
numbers := map[int]string{
    1: "One",
    2: "Two",
    3: "Three",
    4: "Four",
    5:  "Five",
}
```
Go supports nesting of maps as well. To nest maps we could do the following.
```go
func main() {
    data := map[string]map[string]string{
        "13bce1106": map[string]string{
            "name":"Raj Abishek",
            "state":"Tamil Nadu",
        },
        "13bce1118": map[string]string{
            "name":"Sailesh Dev",
            "state":"Tamil Nadu",
        },
    }
    if student, ok := data["13bce1106"]; ok {
        fmt.Println(student["name"], student["state"])
    }
}
```

## Functions
Function definition starts with the `func` keyword, followed by the function’s name followed by the parameters followed by the return type. Collectively, the parameters and the return type are known as the function’s signature. The following code defines a function called average that takes takes in a slice of type `float64` and returns one `float64`.
```go
func average(data []float64) float64 {
    total := 0.0
    for _, value := range data {
        total += value
    }
    return total / float64(len(data))
}

func main() {
    slice := []float64{ 1, 2, 3, 4, 5}
    fmt.Println(average(slice))
}
```
In Go the return type of functions can have names.
```go
func sample() (number int) {
    number = 10
    return
}
```
In Go we can also return multiple values from a function.
```go
func getFullName() (string, string) {
  return "Raj", "Abishek"
}
func main() {
  firstName, lastName := getFullName()
}
```
Multiple value returning functions are commonly used in code to return the error value along with the result, or sometimes a boolean value to indicate the success of the operation.

## Variadic Parameters
The last parameter of a function in Go can be a variadic parameter.
```go
func add(args ...int) int {
    total := 0
    for _, v := range args {
        total += v
    }
    return total
}
func main() {
    fmt.Println(add(1,2,3))
}
```
As you can see in the above code the args parameter is a variadic parameter meaning while calling the functions we can pass multiple arguments zero or more to the `add` function and all of those will be available in the `args` array. The `...` called as ellips is used before the type name of the last parameter to identify it as a variadic parameter.

Do you remember the `Println` function from the `fmt` package we can pass any number of variable to output the values right, internally it uses a variadic parameter. The `Println` function takes any number of values of any type(the special interface{} type). This is precisely how the fmt.Println function is implemented.
```go
func Println(a ...interface{}) (n int, err error)
```

We can also pass a slice followed by ellipsis while calling a function with a variadic parameter as shown below.
```go
func main() {
    data := []int{1, 2, 3}
    fmt.Println(add(data...))
}
```

Functions can also be defined recursively in Go. Here is one way to compute the factorial of a number.
```go
func factorial(x uint) uint {
    if x== 0 {
        return 1
    }
    return x * factorial(x-1)
}
```

## Closures
A closure can capture constants and variables from the surrounding context in which it is defined. The closure can then refer to and modify the values of those constants and variables from within its body, even if the original scope that defined the constants and variables no longer exists.

In Go, the simplest form of a closure that can capture values is a nested function, written within the body of another function. A nested function can capture any of its outer function’s arguments and can also capture any constants and variables defined within the outer function.

Here’s an example of a function called `makeIncrementer`, which contains a nested function called `incrementer`. The nested `incrementer` function captures two values, `runningTotal` and `amount`, from its surrounding context. After capturing these values, `incrementer` is returned by `makeIncrementer` as a closure that increments `runningTotal` by `amount` each time it is called.
```go
package main
import "fmt"

func makeIncrementer(amount int) func() int {
    runningTotal := 0
    incrementer := func() int {
        runningTotal += amount
        return runningTotal
    }
    return incrementer
}

func main() {
    incrementByTen := makeIncrementer(10)
    fmt.Println(incrementByTen()) // returns a value of 10
    fmt.Println(incrementByTen()) // returns a value of 20
    fmt.Println(incrementByTen()) // returns a value of 30

    incrementBySeven := makeIncrementer(7)
    fmt.Println(incrementBySeven()) // returns a value of 7

    fmt.Println(incrementByTen()) // returns a value of 40
}
```
The return type of `makeIncrementer` is `func() int`. This means that it returns a function, rather than a simple value. The function it returns has no parameters, and returns an `int` value each time it is called. When considered in isolation, the nested `incrementer` function might seem unusual.
```Go
incrementer := func() int {
    runningTotal += amount
    return runningTotal
}
```
The `incrementer` function doesn’t have any parameters, and yet it refers to `runningTotal` and `amount` from within its function body. It does this by **capturing a reference** to `runningTotal` and `amount` from the surrounding function and using them within its own function body.

Capturing by reference ensures that `runningTotal` and `amount` do not disappear when the call to `makeIncrementer` ends, and also ensures that `runningTotal` is available the next time the `incrementer` function is called. Closure and recursion are powerful programming techniques that form the basis of a paradigm known as **functional programming**.

## Pointers
When we pass a variable to a function it is passed by copy.
```go
package main
import "fmt"

func sample(a int) {
    a = 10
}
func main() {
    b := 5
    sample(b)
    fmt.Println(b) // b is still 5
}
```
As we can see above even though the sample function will not modify the original b variable in the main function. But what if we wanted to ? One way to accomplish this is through pointers.
```go
package main
import "fmt"

func swap(a, b *int) {
  temp := *a
  *a = *b
  *b = temp
}
func main() {
    a := 5
    b := 10
    swap(&a, &b)
    fmt.Println(a, b) // a is 10 and b is 5
}
```
In Go if the parameters of a function are of same data type then we need not mention the data type along with every parameter name, instead we can add the data type at the end of the parameter list as shown above. Pointers reference a location in memory where a value is stored rather than the value itself. By using a pointer `*int` the swap function is able to modify the original variables.
