---
title: "C Code: An Unreadable One-Liner"
date: 2026-04-06
draft: false
showReadingTime: true
showHeadingAnchors: false
showSummary: true
summary: "Exploring legacy C features, octal literals, and program startup mechanics through a deliberately unreadable one-line program."
---

C is a fascinating languange for many reasons. Some of the most intriguing are the ways it exposes how software actually interacts with the computer. Many of its conventions that feel strange today were originally implemented for very practical historical reasons!

When you combine those features with an understanding of C runtime and standard library behavior, you can write programs that are technically valid, but completely unreadable!

One example is this:
```c
void exit(int status);int printf(const char *, ...);int _start()<%exit(!printf("%s",(char [])<%0103,040,0151,0163,040,0143,0157,0157,0154%>));%>
```

## Running the Program
On Unix-based systems, you can run the above code with the following command:
```bash
gcc -nostartfiles -g program.c && ./a.out
```

## Alternative Ways to Write This
The above code can also be written like this:
```c
void exit(int status);
int printf(const char *, ...);

int _start(){
    exit(!printf("%s",(char []){'C',' ','i','s',' ','c','o','o','l'}));
}
```
Or even simpler, like this:
```c
#include <stdio.h>
#include <stdlib.h>

int maini(){
    printf("%s","C is cool");
    exit(0);
}
```
(Technically, this second one is not the same program from a functional standpoint, but it produces the same output)

# Breakdown
So, how does that first unreadable line of code produce the same output? We will walk step by step through the line to decipher it:

### Prototypes
```c
void exit(int status);int printf(const char *, ...);
```
If we include header files, then they will all need their own respective lines, but we want this as unreadable as possible, so we cannot have that.

So, we can just do what the header file would be included for, and prototype the functions ourselves. 
- The "exit" function is included in the "stdlib.h" system header file
- The "printf" function is included in the "stdio.h" system header file

### Program Entry
```c
int _start()
```
This function is what C programs first enter, and it is this function that calls the "main" function. 

Normally, the "_start" function is used to set up memory allocations and initialize some standard libraries, however, we can preempt that behavior by defining "_start()" ourselves. This is why we need the "-nostartfiles" flag in our compile statement, so that the compiler will not use the default "_start()" function.

This serves no functional purpose aside from making our code less readable and demonstrating that we can run a valid C program without using "main"!

### Digraphs
```c
<% ... %>
```
Any "<%" can be read as "{", and any "%>" can be read as "}". These characters combinations are called "digraphs", and they are legacy notation left over from when some computers did not have the curly brace keys.

There are also such things as "trigraphs" (namely "??<" and ">??") which represent curly braces too!

### Program Exit
```c
exit(...)
```
The "exit" function is what allows us to exit from the "_start" function.

You may notice that it would be shorter to replace the "exit" call with a "return" statement, since that would eliminate the need for a prototype of the "exit" function earlier in the line. However, we cannot do this, as there is no place for the code to return to.

The "_start" function normally calls "main", so using a "return" statement inside "main" returns you to the "_start" function. However, since we overloaded the "_start" function, there is no place for the code execution to return to. This means that we are required to use the "exit" function.

### Return Value Negation
```c
!printf(...)
```
Here, the "!" seems unnecessary, but it actually serves a specific purpose. When we call "exit", we pass an integer into the function, which tells it if the program execution failed or succeeded.

If we pass a "0", or a false value, then "exit" believes that the program execution was a success. If we pass any other integer, or a true value, then "exit" believes the program did not succeed. 

So, why the negation? Well, the "printf" function returns the number of characters that it printed, which the "exit" function would interpret as execution failure. So, if we put a "!" in front of the "printf", it will negate the output, returning a false value and telling the "exit" function that the program succeeded.

### Type Casting
```c
(char[])
```
This section just casts the following array of numbers into an array of characters, using the numbers as ASCII codes for letters and allowing it to be printed as a string, since a string is really just an array of characters in C.

### Array of Digits
```c
<%0143,040,0151,0163,040,0143,0157,0157,0154%>
```
Finally, the digits in the array! If you have ever seen jokes about how "010 == '8'" in Javascript returns true, this is actually where that came from, and that statement would return true in C too!

We are familiar with base 10 numbers being represented as normal numbers in coding, and likely we are all familiar with many languages using "0x" as a prefix to denote base 16, or hexidecimal, numbers. Similarly, C has a prefix for base 8, or octal, that just happens to be "0", without the "x"!

Since Javascript is a combination of many different programming ideas and language conventions, it inherited this prefix notation from C, which can lead to confusion if you accidentally have a leading zero on a number.

This means that each of those numbers in the array is just an octal number that is being cast to a character, which in turn are their ASCII table values!

# Conclusion
Now, this specific program very obviously does not follow proper coding practices, breaks convention, and there is little reason to ever write code like this.

However, it is really fun sometimes to do this with code just because you can! And messing around with silly coding usually leads you to discover things about the language and your computer that you would not otherwise come across!

Happy coding!
