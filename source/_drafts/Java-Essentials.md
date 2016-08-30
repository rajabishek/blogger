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
- `long` - Has a width of 64 bits and values can range from -2<sup>63</sup> to 2<sup>63</sup> - 1
- `int` - Has a width of 32 bits and values can range from –2<sup>31</sup> to 2<sup>31</sup> - 1
- `short` - Has a width of 16 bits and value can range from –32,768 to 32,767
- `byte` - Has a width of 8 bits and values can range from –128 to 127

Width must not be interpreted as the amount of storage consumed. It should be seen as the behavior that is defined for variables and expressions of that type. The Java run-time environment is free to use whatever size it wants, as long as the types behave as you declared them.

## Byte
This is the smallest integer type with a width of 8 bits and values ranging from -128 to 127. Variables of this type are useful while working with a stream of data from a network or file. While dealing with a stream of data from a network or a file we fetch/write in chunks, with each chunk of a byte size. They are also useful while working with raw binary data that may not be directly compatible with Java’s other built-in types. The byte data type can also be useful for saving memory in large arrays, where the memory savings actually matters.

## Short
Has a width of 16 bits and values ranging from –32,768 to 32,767. This is the least used type in Java. As with byte, you can use a short to save memory in large arrays, in situations where the memory savings actually matters.

## Int
Has a width of 32 bits and values can range from –2<sup>31</sup> to 2<sup>31</sup> - 1. Variables of type `int` are commonly used in control loops and to index arrays. By why not use a `byte` or `short` to be more efficient and save space in cases where larger number is not required. This shouldn't be done because when byte and short values are used in an expression, they are promoted to `int` when the expression is evaluated. This is called as type promotion. There `int` is often the best choice when an integer is needed. Use the `byte` and `short` only when the requirement explicitly demands it.

## Long
Has a width of 64 bits and values can range from -2<sup>63</sup> to 2<sup>63</sup> - 1. This type is useful in those occasions where an `int` is not large enough to hold the desired value. Since `long` gives a larger range it is suitable for containing bigger whole numbers. Use this data type when you need a range of values wider than those provided by `int`.

## Floating-Point Types
Floating point values are real numbers. They are used for numbers that require fractional precision. There are two kinds of floating-point types, `float` and `double`, which represent single and double precision floating point values, respectively.

## Float
The `float` data type is a single precision 32 bit IEEE 754 floating point. This type can be used (instead of `double`) if you need to save memory in large arrays of floating point numbers. The advantage of using a `float` type is that they are faster on some processors and takes half as much space as double precision.

Variables of type `float` are useful when you need a fractional component, but don’t require a large degree of precision. This data type should never be used for precise values, such as currency. When dealing with currency values use the the `java.math.BigDecimal` class instead.

## Double
The double data type is a double-precision 64 bit IEEE 754 floating point. For decimal values, this data type is generally the default choice. This type is useful when you are manipulating large valued numbers and when you need to maintain accuracy over many iterative calculations.

Again this type must not be used for precise values like currency use the `java.math.BigDecimal` class instead. Double precision is actually faster than single precision on some modern processors that have been optimized for high-speed mathematical calculations.

By default, Java uses `double` to represent its floating point numerals (so a literal 3.14 is typed `double`). It's also the data type that will give you a much larger number range, so I would strongly encourage its use over `float`. Unless you can guarantee that your result will be small enough to fit in float's prescribed range, then it's best to opt with `double`. A `float` gives you approx. 6-7 decimal digits precision while a `double` gives you approx. 15-16.