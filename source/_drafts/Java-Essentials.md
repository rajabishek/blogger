---
title: Java Essentials
tags:
---
## Introduction
Java is a general-purpose high-level computer programming language originally developed by Sun Microsystems and released in 1995 that is concurrent, class-based, object-oriented, and specifically designed to have as few implementation dependencies as possible. 

It is intended to let application developers "write once, run anywhere" (WORA), meaning that compiled Java code can run on all platforms that support Java without the need for recompilation.

<!-- more -->

## Principles of Java
- Simple & familiar
- Object oriented
- Robust
- Secure
- Architecture neutral & portable
- High performance
- Interpreted (Byte code is interpreted at runtime by the Java virtual machine)
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