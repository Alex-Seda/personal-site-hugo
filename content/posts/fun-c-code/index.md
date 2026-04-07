---
title: "C Code: An Unreadable One-Liner"
showDate: false
draft: false
showReadingTime: false
showHeadingAnchors: false
summary: "Exploring legacy C features, octal literals, and program startup mechanics through a deliberately unreadable one-line program."
---

C is a fascinating languange for many reasons. Some of the most intriguing are the ways it exposes how software actually interacts with the computer. Many of its conventions that feel strange today were originally implemented for very practical historical reasons!

When you combine those features with an understanding of C runtime and standard library behavior, you can write programs that are technically valid, but completely unreadable!

One example is this:
```c
void exit(int status);int printf(const char *, ...);int _start()<%exit(!printf("%s",(char [])<%0143,040,0151,0163,040,0143,0157,0157,0154%>));%>
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
    exit(!print("%s",(char []){'C',' ','i','s',' ','c','o','o','l'}));
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
If we include header files, then they will all need their own respective lines. So, we can just do what the header file would be included for, and prototype the functions ourselves. 
- The "exit" function is included in the "stdlib.h" system header file
- The "printf" function is included in the "stdio.h" system header file

This is why we can replace those prototypes with imports in the cleanest code implementation block.

### Program Entry
```c
int _start()
```
This is what C programs enter before they enter the "main" function. It is normally used to set up memory allocations and initialize some standard libraries.

However, we can preempt that behavior by defining "_start()" ourselves. This is why we need the "-nostartfiles" flag in our compile statement, so that the compiler will not use the default "_start()" function.

This serves no functional purpose aside from making our code less readable.

### Code Organization
```c
<% ... %>
```
Any "<%" can be read as "{", and any "%>" can be read as "}". These characters combinations are called "digraphs", and they are legacy notation left over from when some computers did not have the curly brace keys.

There are actually such things as "trigraphs" (namely "??<" and ">??") which represent the same characters!

### Program Exit

### Return Value Negation

### Type Casting

### Array of Digits

# Conclusion
