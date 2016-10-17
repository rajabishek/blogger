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
