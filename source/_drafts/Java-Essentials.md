---
title: Java Essentials
tags:
---
## Introduction
Java is a general-purpose high-level computer programming language originally developed by Sun Microsystems and released in 1995 that is concurrent, class-based, object-oriented.

It is intended to let application developers "write once, run anywhere", meaning that compiled Java code can run on all platforms that support Java without the need for recompilation.

<!-- more -->

## Principles of Java
- Simple & familiar
- Object oriented
- Robust
- Secure
- Architecture neutral & portable
- High performance
- Interpreted (Byte code is interpreted at runtime by the JVM)
- Threaded and dynamic 

## Strongly Typed Language
- Every variable has a type. Every expression has a type. Every type is strictly defined.
- Whenever an assignment is made whether explicit or via parameter passing in method calls, Java checks for type compatibility.
- Whenever Java encounters conflicting types it does not perform any automatic coercions or conversions.

This strongly typed nature of Java is what makes is highly robust and secure. Any type mismatches are reported as errors and can be identified during compile time itself.

## Primitive Types
In any programming language you need a way to represent these 3 basic values. A way to represent numbers. A way to represent characters. A way to represent truthy/falsy values. Java has eight primitive types of data: `byte`, `short`, `int`, `long`, `char`, `float`, `double`, and `boolean`. Primitive types are also known as simple types. These can be categorized into 4 groups.
1. **Integers** - This includes `byte`, `short`, `int`, and `long`, which are for whole valued signed numbers.
1. **Floating point numbers** - This includes `float` and `double`, which represent numbers with fractional precision.
1. **Characters** - The `char` datatype is used to represent characters that represents symbols in a character set, like letters and numbers.
1. **Boolean**- The `boolean` datatype is used to represent true/false values.

Any type that we define are also is built up using these basic primitive types. Thus they form the basis for all other types of data that you can create. Although Java is otherwise completely object-oriented, the primitive types are not. They represent single values and are not objects. The reason for not modeling the primitive types as classes is for performance. Making the primitive types into classes would have degraded performance very much.

The primitive types in Java having an explicit size. In C and C++ the size of an integer varies based upon the platform in the program is compiled, but because of Java’s portability requirement, all data types have a strictly defined range. For example, an `int` is always 32 bits in Java, regardless of the particular platform.

## Integers
There are four integer types - `byte`, `short`, `int`, and `long`. All of these are signed(positive and negative), Java does not support unsigned, positive-only integers. Java’s designers felt that unsigned integers were unnecessary.
- `long` - Has a width of 64 bits and values can range from –9,223,372,036,854,775,808 to 9,223,372,036,854,775,807
- `int` - Has a width of 32 bits and values can range from –2,147,483,648 to 2,147,483,647
- `short` - Has a width of 16 bits and value can range from –32,768 to 32,767
- `byte` - Has a width of 8 bits and values can range from –128 to 127

Width must not be interpreted as the amount of storage consumed. It should be seen as the behavior that is defined for variables and expressions of that type. The Java run-time environment is free to use whatever size it wants, as long as the types behave as you declared them.