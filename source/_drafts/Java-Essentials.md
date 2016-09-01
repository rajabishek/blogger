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

## Integer Values
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

Any whole number value is an integer literal and by default they are all decimal values, meaning they are describing a base 10 number. Octal values are denoted in Java by a leading zero. Hexadecimal values are denoted in Java by a leading zero-x, (0x or 0X). Binary values are denoted in Java by a leading zero-b, (0b or 0B).

If all integer literals create a `int` value then how it is possible to assign an integer literal to one of Java’s other integer types, such as byte or long, without causing a type mismatch error. That's because in Java when a literal value is assigned to a `byte` or `short` variable, no error is generated if the literal value is within the range of the target type.

Beginning with JDK 7, you can embed one or more underscores in an integer literal. Doing so makes it easier to read large integer literals. When the literal is compiled, the underscores are discarded. The underscores will be ignored. Underscores can only be used to separate digits. They cannot come at the beginning or the end of a literal. However it is permissible for more than one underscore to be used between two digits.
```java
int x = 123_456_789;
int x = 123___456___789;
int x = 0b1101_0101_0001_1010;
```

## Long
Has a width of 64 bits and values can range from -2<sup>63</sup> to 2<sup>63</sup> - 1. This type is useful in those occasions where an `int` is not large enough to hold the desired value. Since `long` gives a larger range it is suitable for containing bigger whole numbers. Use this data type when you need a range of values wider than those provided by `int`. An integer literal can always be assigned to a long variable. However to specify a long literal, you will need to explicitly tell the compiler that the literal value is of type long. It is done by appending an upper or lowercase L to the literal.
```java
long x1 = 12; //OK
long x2 = 2147483648; // not OK! That's not a valid int literal
long x3 = 2147483648L; // OK
```
Note that while integer literals will be auto-widened to `long` when assigning to a `long` variable but you will need to use an explicit long literal when expressing a value. Here 2147483648 is interpreted as a literal integer but can't fit in a 32-bit int type. It needs to be a literal long value, so it needs an l or L at the end. Use the upper case L always as the upper case L is less easy to confuse with a numeral 1 than the lower case l.

## Floating Point Values
Floating point values are real numbers. They are used for numbers that require fractional precision. There are two kinds of floating-point types, `float` and `double`, which represent single and double precision floating point values, respectively. Floating point literals can be expresses in Standard notation or Scientific notation.

## Float
The `float` data type is a single precision 32 bit IEEE 754 floating point. This type can be used (instead of `double`) if you need to save memory in large arrays of floating point numbers. The advantage of using a `float` type is that they are faster on some processors and takes half as much space as double precision.

Variables of type `float` are useful when you need a fractional component, but don’t require a large degree of precision. This data type should never be used for precise values, such as currency. When dealing with currency values use the the `java.math.BigDecimal` class instead.

Floating-point literals in Java default to double precision. To specify a float literal, you must append an F or f to the constant. Beginning with JDK 7, you can embed one or more underscores in a floating-point literal. This feature works the same as it does for integer literals. The same rules apply here. They cannot come at the beginning or the end of a literal. It is, however, permissible for more than one underscore to be used between two digits. It is also permissible to use underscores in the fractional portion of the number.
```java
double num = 9_423_497_862.0;
double num = 9_423_497.1_0_9;
```

## Double
The double data type is a double-precision 64 bit IEEE 754 floating point. For decimal values, this data type is generally the default choice. This type is useful when you are manipulating large valued numbers and when you need to maintain accuracy over many iterative calculations.

Again this type must not be used for precise values like currency use the `java.math.BigDecimal` class instead. Double precision is actually faster than single precision on some modern processors that have been optimized for high-speed mathematical calculations.

By default, Java uses `double` to represent its floating point numerals (so a literal 3.14 is typed `double`). It's also the data type that will give you a much larger number range, so I would strongly encourage its use over `float`. Unless you can guarantee that your result will be small enough to fit in float's prescribed range, then it's best to opt with `double`. A `float` gives you approx. 6-7 decimal digits precision while a `double` gives you approx. 15-16.

As mentioned earlier floating-point literals in Java default to double precision. You can also explicitly specify a double literal by appending a D or d. Doing so is, of course, redundant.

## Characters
Java uses Unicode to represent characters. Java `char` is a 16 bit type. The range of a char is 0 to 65,536. Unicode defines a fully international character set that can represent all of the characters found in all human languages.

Characters in languages such as English, German, Spanish, or French can easily be contained within 8 bits. The use of 16 bits here is inefficient in these cases( as just 8 bits are needed) but such is the price that must be paid for global portability. 

ASCII character set occupies the first 127 values in the Unicode character set. Although char is designed to hold Unicode characters, it can also be used as an integer type on which you can perform arithmetic operations.
```java
class Test {
	public static void main(String args[]) {
		char ch1, ch2, ch3;
		ch1 = 88; // code for X
		ch2 = 'Y';
		ch3 = ch1 + 1;
		System.out.print("ch1 and ch2 and ch3: ");
		System.out.println(ch1 + " " + ch2 + " " + ch3);
	}
}
```
The output of the above code is `ch1 and ch2 and ch3: X Y Y`. A literal character is represented inside a pair of single quotes. All of the visible ASCII characters can be directly entered inside the quotes, such as 'a', 'z', and '@. String literals in Java are specified like they are in most other languages—by enclosing a sequence of characters between a pair of double quotes.

## Boolean
The boolean data type has only two possible values: true and false. Use this data type for simple flags that track true/false conditions. This is the type returned by all relational operators. This is also the type required by the conditional expressions.

The values of true and false do not convert into any numerical representation. The true literal in Java does not equal 1, nor does the false literal equal 0.

## Variables & Scope
- A variable cannot be used prior to its declaration.
- A variable cannot be used after its declaration if its not initialized.
- Variables are created when their scope is entered, and destroyed when their scope is left. Lifetime of a variable is confined to its scope.
- You cannot declare a variable in an inner scope.
- Simply creating { } creates a new scope in Java.

## Type Conversion and Casting
- The two types are compatible and if the destination type is larger than the source type then Java does automatic type promotion.
- Explicit casting is required for conversion between two incompatible types.
- When there is an overflow during casting the resulting value is remainder of the division of size of destination type.
- Java automatically promotes each byte, short, or char operand to int when evaluating an expression.
- If one operand is a long, the whole expression is promoted to long.
- If one operand is a float, the entire expression is promoted to float.
- If any of the operands are double, the result is double.

## Arrays
- In Java all arrays are dynamically allocated.
- Declare array using `type var-name[ ];` this just declares the array variable. No array actually exists.
- To create actual array use `array-var = new type [size];`. Only now memory is allocated for the array and linked to the array-var variable.
- The elements in the array allocated by new will automatically be initialized to zero (for numeric types), false (for boolean), or null (for reference types, which are described in a later chapter).
- An array initializer is a list of comma-separated expressions surrounded by curly braces. The array will automatically be created large enough to hold the number of elements you specify in the array initializer. There is no need to use new.
```java
int month_days[] = { 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31 };
```
- If you try to access elements outside the range of the array (negative numbers or numbers greater than the length of the array), you will cause a run-time error.
- Multidimensional arrays are actually arrays of arrays. To declare a multidimensional array variable, specify each additional index using another set of square brackets.
```java
int twoD[][] = new int[4][5];
```
- When you allocate memory for a multidimensional array, you need only specify the memory for the first (leftmost) dimension.
```java
int twoD[][] = new int[4][];
twoD[0] = new int[1];
twoD[1] = new int[2];
twoD[2] = new int[4];
twoD[3] = new int[3];
```
- It is possible to initialize multidimensional arrays. To do so, simply enclose each dimension’s initializer within its own set of curly braces.
```java
int data[][] = {{1,2,3}, {4,5}};
```
- You can also declare array like `type[ ] var-name;`Both syntax are equivalent as shown below. But this syntax is especially useful while declaring array as a return type from a function.
```java
char twod1[][] = new char[3][4]; <=> char[][] twod2 = new char[3][4];
int[] nums, nums2, nums3; <=> int nums[], nums2[], nums3[];
```

## Hashtable
- You declare a hash table instance using `Hashtable<Character, Integer> store = new Hashtable<>();`. 
- To store the value for a key you use the put method on the instance `store.put(character, count);`. 
- And to get the value for the key you use the get method `int count  = store.get(character) == null ? 1 : store.get(character) + 1;`, i.e if the value for the key is not there it returns null or else it returns the value.
- To get the keys in the hash table you can do `Set<Character> keys = store.keySet();`. Now we can loop through the key set using a simple for in loop.
```java
package com.rajabishek;

import java.util.Hashtable;
import java.util.Scanner;
import java.util.Set;

public class Main {

    public static void main(String[] args) {
        Scanner reader = new Scanner(System.in);
        System.out.println("Enter the input string: ");
        String input = reader.nextLine();

        Hashtable<Character, Integer> store = new Hashtable<>();

        char[] characters = input.toCharArray();
        for(char character : characters) {
            int count  = store.get(character) == null ? 1 : store.get(character) + 1;
            store.put(character, count);
        }

        Set<Character> keys = store.keySet();
        int maxCount = -1;
        char maxCharacter = 'a';
        for(Character key: keys) {
            int count = store.get(key);
            if(count > maxCount) {
                maxCount = count;
                maxCharacter = key;
            }
        }

        System.out.println("The maximum occuring character is " + maxCharacter + " and its maximum count is: " + maxCount);
    }
}
```
The above is the code for getting the maximum occurring character in a string.