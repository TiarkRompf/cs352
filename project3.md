---
title: "Project 3: Type Checking - Functions - Heap Allocation"
usetable: true
layout: template
---

> Due 11:59pm Monday Feb 5 (two weeks project)

## Useful Links

-   [x86_64 cheat
    sheet](https://cs.brown.edu/courses/cs033/docs/guides/x64_cheatsheet.pdf){:target="_blank"}

## Introduction

In this project, we will enrich the language we defined in the first two
projects.

At the end of the project, we will be able to parse full programs,
including functions and arrays. Our parser will generate an intermediate
representation in the form of an Abstract Syntax Tree (AST), and our
Semantic Analyzer will be able to verify that the typing rules are being
enforced.

With functions now in our language, we can add a little bit of I/O. When
writing code in our programming language, the programmer will have
access to two primitives:

-   **getchar** of type () =\> Int.
    [doc](https://en.wikibooks.org/wiki/C_Programming/stdio.h/getchar){:target="_blank"}
-   **putchar** of type Int =\> Unit.
    [doc](https://en.wikibooks.org/wiki/C_Programming/stdio.h/putchar){:target="_blank"}
    (we do not return the character)

Using these functions may lead to some issues when the code is launched
from sbt. In order to test, launch the **out** binary generated in the
folder **gen/**.

## Step 1: Getting Started

The project has been designed and tested for Linux/Mac OS. If you only
have Windows installed on your personal laptop, consider running Linux
in a VM or using the lab machines for the project.

If you use remote access to work on your project, please use one of the
lab machines pod1-1 to pod1-20 with the suffix cs.purdue.edu (e.g.
pod1-1.cs.purdue.edu)

Download the skeleton file
[here](https://www.cs.purdue.edu/homes/gao606/cs352/proj3.zip){:target="_blank"}.

    unzip proj3.zip
    cd proj3

## Step 2: Project Structure

### Browse the Files

A description of the different files is provided below. The files you
need to complete are **Parser.scala**, **SemanticAnalyzer.scala**,
**Interpreter.scala**, and **Compiler.scala**. Following the path of the
first project, we are going to implement the parser step by step. Follow
the comments in the code and find the **TODOs**. The parts are
independent and can be develop separately. In order to implement the new
features more easily, we have changed some of the previous
class/function definition we had. You can search for the string CHANGE
into the source code to see these modifications.

### src/main/scala/project3/Util.scala

This file defines multiple classes that are used to generate the code
and run it on your machine. Nothing needs to be modified, but it is
recommended to read it and have an idea of what is happening behind the
scenes.

### gen/bootstrap.c

As we are generating assembly code which is OS dependent, we are using
GCC to do the heavy lifting for us. The bootstrap file is a generic C
file that is allocation a chunk of memory called **heap**. This memory
region is sent to our program through an argument of the function
**entry_point**. The exit code of our program is then printed on the
screen. Our compiler will generate the file **gen/gen.s** and will be
assembled and bootstrapped by gcc:

    gcc bootstrap.c gen.s -o out

**out** will then execute our program.

### src/main/scala/project3/Main.scala

The main function is defined in this file. The data flow in this file
can be seen as:

    Read from File / Read from Command Line -> Parser -> Semantic Analyzer -> Interpreter or Compiler

You will be implementing many different parsers in order to test them
through the main function.

The AST generated will then go through the semantic analyzer. If there
are no errors, then the code is going to be interpreted or compiled. We
provide you with one interpreter. You will have to write one interpreter
and one compiler.

As our language becomes more complex, it will become more useful to read
the code from a source file. A folder with sample files **examples/**
has been provided. Here some examples how to run the code:

    sbt
    > run
    Usage: run PROG [OPTION]
       or: run FILE [OPTION]
    OPTION: intStack
    > run examples/valid_arithm.scala           ---> interpret with the provided interpreter, and x86 compiler
    > run examples/valid_arithm.scala intStack    ---> stack interpreter (your code), and x86 compiler

However, it is still possible to run code from the command line, as in
project 1:

    sbt
    > run "val x = 5; x"
    > run "val x = 5; x" intStack

### src/main/scala/project3/Parser.scala

This class contains the definition of our intermediate language.

As we discussed in class, we are introducing types in our language. In
addition to Integer, we will also have the types Boolean and Unit. You
will need to modify the **Scanner** class in order to tokenize the
constants of type Boolean correctly. There is a single Unit constant:
(). Because this construct can be used for other reasons (e.g. a
function without parameters), the () will still be parsed into two
delimiters: \'(\' and \')\'. The function **parseAtom** will be handling
the Unit literal.

The rest of the file is the definition of each parser we are building,
starting from a base parser that is an implementation of the parser we
implemented in project 2. What you have to do for this project is
highlighted with TODOs in the code. We encourage you to read the
comments and code carefully before proceeding.

### src/main/scala/project3/SemanticAnalyzer.scala

While the parser is in charge of verifying that the input string follows
the defined syntax, the semantic analyzer verifies that the program
described is meaningful and follows the rules. The skeleton code already
contains the semantic checks we implemented in project 2.

However as we have seen in class, we are upgrading our semantic analyzer
into a type checker. Your job is to complete the **typeInfer** function
using the rules we have seen in class.

### src/main/scala/project3/Interpreter.scala

As we have seen in class, now that our programing language accepts more
than just mathematical expressions, we need to define the required
behavior of our language. An interpreter can be used to define this
meaning.

We provide you with an interpreter that is fully functional. Your job is
to complete the **Stack-based** interpreter.

### src/main/scala/project3/Compiler.scala

The x86_64 compiler handling all features up to loops is already
implemented for you. You need to complete the compiler with the new
features.

### src/test/scala/project3/\*Test.scala

These files contain some unit tests for the first parsers. <mark>You will
have to write your own tests for the others. Every task should have at
least 2 tests otherwise points will be deducted.</mark> There are some
functions given to you in order to make the implementation easier.

## Extra Credit

### Char

The programmer can use two functions to interact with the console:
**getchar** and **putchar**. However, we do not have characters, so in
order to print hello world, we would have to write the code:

    putchar(72); putchar(101); putchar(108); putchar(108); putchar(111); ...

This is not really convenient; we would rather do:

    putchar(toInt('H')); putchar(toInt('e')); putchar(toInt('l')); putchar(toInt('l'))...

(much better isn\'t it?)

We are therefore going to add a new type in the language: Char. All
letters, numbers, punctuation signs and spaces should be handled, e.g.
you don\'t have to handle the escaping characters \'\\n\', \'\\r\'\...
In the program, a programmer will be able to use the single quote
notation to enter a character e.g. \'H\'. You will also provide two
primitives operations:

-   toInt: of type Char =\> Int
-   toChar: of type Int =\> Char

You can use the example of the Array look up transformation into
primitive. In the skeleton this is done in the semantic analyzer in the
App case. The x86 implementation: toInt will be a no-op and toChar:

    mov loc, %rax
    movzbq %al, loc

### Functions as value

In the **Compiler.scala** file, there are some places marked as Extra
Credit. These are the places where we need to generate code for
functions used as arguments, stored into variables, or returned from a
function. While you are required to parse this kind of code correctly
and be able to type check it, you are not required to generate the
corresponding x86 code. Implementing such generation correctly will be
counted as extra credit.

## Turnin

You should turn in the **proj3** directory. Please run an \'sbt clean\'
and \'./cleanall.sh\' before submitting.

To turn in your project create a ZIP file named
`<purdueemailusername>-proj<N>.zip` of the `proj3` directory for
example `axhebraj-proj3.zip` and upload it to the corresponding
assignment on Brightspace.

**No other file formats or naming conventions will be accepted as
submissions. Verify your submission by downloading the ZIP file you
uploaded on Brightspace and extracting its content. The uncompressed
content should be the `proj3` folder containing the code.**

## Grading

Your project will be tested against a set of unit tests. The weights of
each task will be distributed as follow:

  Task                     | Weight
  -------------------------|---------
  Scanner: Boolean         | 2.5%
  BaseParser: parse types  | 2.5%
  Syntactic Sugar          | 5%
  FunctionParser           | 15%
  ArrayParser              | 10%
  Semantic Analyzer        | 30%
  StackInterpreter         | 10%
  X86Compiler              | 25%
  Extra Credit             | 10%
