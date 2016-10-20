---
title: Functional Thinking - Scala
date: 2016-10-17 20:30:49
tags:
---

## Introduction
Scala stands for "Scalable Language". Its a language that is meant to grow with its users. It can be used for building large systems and frameworks of reusable components. It runs on the standard Java platform and is interoperable with all Java libraries. It is statically typed with a blend of object-oriented and functional programming.

<!-- more -->
## Installation
To get the official Scala installation, you can visit the official [downloads](http://www.scala-lang.org/downloads) page and follow the directions for your platform. You can also use a Scala plug-in for Eclipse, IntelliJ, or NetBeans. To check if Scala is installed correctly you can run `scala -version` on the command line to check the version installed.

## Overview
All of Java’s primitive types have corresponding classes in the `scala` package. For instance `scala.Boolean` corresponds to Java’s boolean. `scala.Float` corresponds to Java’s float. When we compile the Scala code to Java bytecodes, the Scala compiler will use Java’s primitive types where possible to give you the performance benefits of the primitive types.

Scala has two kinds of variables, vals and vars. A val is like a constant which once initialized can never be reassigned. A var, by contrast, is a normal variable that can be reassigned throughout its lifetime.
```scala
val message = "Helloworld from Raj Abishek"
```
The type of message is `java.lang.String`, because Scala strings are implemented by Java’s String class. But if you notice above we never mentioned the type while creating the message val. This is called as type inference. The Scala interpreter(or compiler) can infer types based on the initial value that we assign while declaring the variable. In fact it is often best to let the compiler do so rather than specifying a type explicitly using type annotation.
```scala
val name: java.lang.String = "Raj Abishek"
val friend: String = "Sailesh Dev" //using the simple name for type annotation
```
As you see above here we have used type annotations to explicitly explicitly the type of name. The `java.lang` types are visible with their simple names in Scala. The simple name of `java.lang.String` is `String`. As I had mentioned earlier what we can’t do with message or name or friend, given that it is a val, not a var, is reassign it.
```scala
var greeting = "Good morning!"
greeting = "Good evening!" //Perfectly valid since greeting is a var
```

We start function definitions with the `def` keyword. The function’s name as shown below is minimum and it is followed by a comma separated list of parameters in parentheses with type annotations for every parameter. After the close parenthesis of minimum's parameter list we type annotate the result type of the function. In Scala the type of value returned from a function is called as result type(In Java we call it return type). Following the function’s result type is an equals sign and pair of curly braces which contains the function body.
```scala
def minimum(x: Int, y: Int): Int = {
  if (x < y)
    x
  else
    y
}
```
Scala’s if expression can result in a value, just like Java’s ternary operator. The `if(x < y) x else y` expression in Scala behaves similarly to `(x < y) ? x : y` in Java. The result type of the function is not always required to be mentioned. If we leave the result type off and the compiler can infer it. But in some cases like recursive functions the Scala compiler will require you to explicitly specify the result type of a function. In Scala if the function consists of just one statement, you can leave off the curly braces.
```scala
def minimum(x: Int, y: Int) = if (x < y) x else y
```
As you can see above the result type of the function is omitted and the curly brace is removed since function body just has a single if statement.
Nevertheless, it is often a good idea to indicate function result types explicitly, even when the compiler doesn’t require it. Such type annotations can make the code easier to read. Another developer working on the project need not study the function body to figure out the inferred result type.
```scala
def greet() = println("Helloworld from Raj Abishek")
```
The above is an example of function declaration the accepts no parameters and returns nothing. The result type of greet function is `Unit`. Scala’s Unit type is similar to Java’s void type. Every `void` returning method in Java is mapped to a `Unit` returning method in Scala.
As we will see later the above `greet` function is not pure. A pure function is a function where the result value is only determined by its input values, without observable side effects. Its takes input through parameters, processes the input and returns a value. As we will see later a pure function always gives the same output for a given input, it produces no side effects and does not rely on any external state. In simpler term if you think about it a function is impure is if it makes sense to call it without using its return value. Methods with the result type of Unit, therefore, are only executed for their side effects. In the case of `greet` function, the side effect is a friendly greeting printed to the standard output.

While executing the Scala file we can pass command line arguments which are in the `args` array. Arrays are zero based and can be positionally indexed with parentheses. So the ith element in a Scala array named data is `data(i-1)`, not `data[0]`, as in Java.
```Scala
println("Helloword from " + args(0)) //get the command line argument
```
In all of the above shown sample code we never wrapped the code within a main method of a class like how we do it in Java. Thats because even though Scala is designed to help developers build very large-scale systems, it also scales down nicely to scripting. A script is just a sequence of statements in a file that will be executed sequentially.

Just like comments behave the same way in Scala. The Scala compiler will ignore characters between `//` and the next end of line and any characters between `/*` and `*/`.

To loop through the elements of the array using a while loop we do the following.
```scala
//Non idiomatic code
var i = 0
while (i < args.length) {
  println(args(i))
  i += 1
}
```
You should understand here that although while loops are explained here, they do not demonstrate the best Scala style. Later we shall see better approaches that avoid iterating through arrays with indexes. The above code that loops through the array through positional indexing via a while loop is not seen as the natural way of lopping through an array in Scala. Note here that Java’s ++i and i++ don’t work in Scala, to increment in Scala we either do i = i + 1 or i += 1. There is also a `print` function in Scala that prints out a string without a line break. So to print out the command line arguments on the same line we can do the following.
```scala
var i = 0
  while (i < args.length) {
    if (i != 0)
    print(" ")
    print(args(i))
    i += 1
  }
println()
```
Like Java, in Scala you must put the boolean expression for a while or an if in parentheses.(You can't do things like if i < 10 as you can in a languages such as Python, Ruby). Another similarity to Java is that if a block has only one statement, you can optionally leave off the curly braces. Also in Scala adding semicolons at the end of a line is optional(Scala won't complain if you prefer adding semicolons). But semicolons are required if you want to write multiple statements on a single line.

When we wrote the while loops above we were programming in an imperative style. In languages such a Java, C, C++ we give one imperative command at a time, iterate with loops, and often mutate state shared between different functions. One of the main characteristics of a functional language is that functions are first class constructs. Although Scala allows us to program in imperative style as we saw above(positional indexing with while), we will find ourselves using functional style more as we dive deeper into Scala.
```scala
args.foreach(arg => println(arg))
```
The above code is how we would achieve the same result functionally. We call the `foreach` method on the `args` array and pass in a function. Here we are passing a function literal that takes one parameter names `arg`. The body of the function is the single statement `println(arg)`. The syntax for a function literal is a list of named parameters, in parentheses, a right arrow, and then the body of the function. As you can see above the Scala interpreter infers the type of `arg` as `String`, since `String` is the element type of the array on which we called the foreach.
But if you would like be verbose we can explicitly type annotate the `arg` parameter as a `String`. And remember to add the parentheses when you explicitly type the parameter.
```scala
args.foreach((arg: String) => println(arg))
```
If you would like to be concise and not explicit, you can use a shorthand form called as partially applied function. If a function literal consists of one statement that takes a single argument, you need not explicitly name and specify the argument.
```scala
args.foreach(println)
```
Ok but now you may think, what about the very famous imperative style for loops that we use in Java or C++. In an effort to guide Scala programmers in a functional direction, only a functional relative of the imperative for(called as for expression) is available in Scala.
```scala
for(arg <- args)
    println(arg)
```
The `arg` is a val and not a var here. Although `arg` may seem to be a var, it gets a new value on each iteration, it really is a val. `arg` can’t be reassigned inside the body of the for expression. A new `arg` val will be created and initialized to the element value during every iteration.
