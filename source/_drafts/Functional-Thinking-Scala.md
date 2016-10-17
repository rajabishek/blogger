---
title: Functional Thinking - Scala
tags:
---
## Introduction
- Stands for **scalable language** - Named so because it was designed to grow with the demands of developers.
- Can be used for building large systems and frameworks of reusable components.
- Runs on the standard Java platform
- Interoperable with all Java libraries.
- Blend of object-oriented and functional programming.
- Statically typed with Type Inference

## Installation
To get the official Scala installation, you can visit the official [downloads](http://www.scala-lang.org/downloads) page  and follow the directions for your platform. You can also use a Scala plug-in for Eclipse, IntelliJ, or NetBeans. To check if Scala is installed correctly you can run `scala -version` on the command line to check the version installed.

## Overview
All of Java’s primitive types have corresponding classes in the `scala` package. For instance `scala.Boolean` corresponds to Java’s boolean. `scala.Float` corresponds to Java’s float. When we compile the Scala code to Java bytecodes, the Scala compiler will use Java’s primitive types where possible to give you the performance benefits of the primitive types.

Scala has two kinds of variables, vals and vars. A val is like a constant which once initialized can never be reassigned. A var, by contrast, is a normal variable that can be reassigned throughout its lifetime.
```scala
val message = "Helloworld from Raj Abishek"
```
The type of message is `java.lang.String`, because Scala strings are implemented by Java’s String class. But if you notice above we never mentioned the type while creating message. This is called as type inference. The Scala interpreter (or compiler) can infer types based on the initial value that we assign while declaring the variable. In fact it is often best to let the compiler do so rather than specifying a type explicitly using type annotations.
```scala
val name: java.lang.String = "Raj Abishek"
val friend: String = "Sailesh Dev" //using the simple name for type annotation
```
As you see above here we have used type annotations to explicitly explicitly the type of name. The `java.lang` types are visible with their simple names in Scala. The simple name of `java.lang.String` is `String`. As I had mentioned earlier what we can’t do with message or name or friend, given that it is a val, not a var, is reassign it.
```scala
var greeting = "Good morning!"
greeting = "Good evening!" //Perfectly valid since greeting is a var
```

We start function definitions with the `def` keyword. The function’s name as shown above is max and it is followed by a comma separated list of parameters in parentheses with type annotations for every parameter. After the close parenthesis of max’s parameter list we type annotate the result type of the function. In Scala the type of value returned from a function is called as result type(In Java we call it return type). Following the function’s result type is an equals sign and pair of curly braces which contains the function body.
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

While executing the Scala file we can pass command line arguments which are in the `args` array. Arrays are zero based and can be positionally indexed with parentheses. So the ith element in a Scala array named data is `data(i-1)`, not `data[0]`, as in Java.
```Scala
println("Helloword from " + args(0)) //get the command line argument
```
In all of the above shown sample code we never wrapped the code within a main method of a class like how we do it in Java. Thats because even though Scala is designed to help developers build very large-scale systems, it also scales down nicely to scripting. A script is just a sequence of statements in a file that will be executed sequentially.

Just like comments behave the same way in Scala. The Scala compiler will ignore characters between `//` and the next end of line and any characters between `/*` and `*/`.
