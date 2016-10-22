---
title: Diving deep into python
tags:
---
## Object object everywhere
Everything is an object in a Python script. Any data we deal with in python code is essentially a object, either a built in object that Python provides or objects we create using Python classes or external language tools such as C extension libraries.

<!-- more -->

## Built in object types
| Object type        | Example literals/creation        |
|--------------------|----------------------------------|
| Numbers            | 296, 2.345, 2+3j                 |
| Strings            | 'cool', "Raj's"                  |
| Lists              | [1, 2, 'three'], list(range(10)) |
| Dictionaries       | {'name': 'Raj', 'role': 'dev'}   |
| Tuples             | (True, False)                    |
| Files              | open('sample.txt')               |
| Sets               | {'a', 'b', 'c'}                  |
| Boolean            | True, False                      |
| None               | None                             |
| Type               | type('hello'), type(1)           |
| Program unit types | Functions, modules, classes      |
As you can see above program units such as functions, modules and classes are also objects in Python. The above table is not fully complete as I had mentioned earlier that everything that we manipulate and process in Python is an object of some kind. For instance, we use socket objects when we write scripts for networking and we create pattern objects when we perform text pattern matching in Python. The syntax of the expressions you run determines the types of objects you create and use. An expression wrapped in square brackets makes a list, one in curly braces makes a dictionary, and so on.
