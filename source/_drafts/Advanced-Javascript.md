---
title: Advanced Javascript
tags:
---
## Javascript compiler
Does javascript have a compiler ? Yes. Javascript is actually a compiled language. Understanding about the javascript compiler can be helpful in analyzing how javascript handles scope internally. 

<!-- more -->

Its not quite the same as how we would compile C++/Java programs. We don't distribute the binary compiled form of the program. In javascript the program is compiled every single time it is run. So then what would be an interpreted language ? The difference between a compiled language and interpreted language is that in a interpreted language the interpreter has no idea about the next line when it is evaluating the current line(eg bash scripting), i.e when it is running line 6 it has no idea on what to expect on line 7. It has not even looked at line 7 yet. So an interpreter literary goes from top to bottom of the program line by line. In javascript however the compiler does an initial pass through the code to compile it and it does atleast one more pass through the code and then only in its final pass ot will perform the execution, so it has looked at line 7 when it is running line 6.

