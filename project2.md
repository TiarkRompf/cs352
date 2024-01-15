---
title: "Project 2: Branches - Loops - Error handling"
usetable: true
layout: template
---

> Due 11:59pm Monday Jan 22

## Useful Links

-   [x86_64 cheat sheet (up to page 4 for this
    project)](https://cs.brown.edu/courses/cs033/docs/guides/x64_cheatsheet.pdf){:target="_blank"}

## Introduction

In this project, we will enrich the simple arithmetic expression
language we defined in the first project.

At the end of the project, we will be able to parse full programs; the
only things missing will be functions and arrays. Our parser will
generate an intermediate representation in the form of an Abstract
Syntax Tree (AST).

## Step 1: Getting Started

The project has been designed and tested for Linux/Mac OS. If you only
have Windows installed on your personal laptop, consider running Linux
in a VM or using the lab machines for the project.

If you use remote access to work on your project, please use one of the
lab machines pod1-1 to pod1-20 with the suffix cs.purdue.edu (e.g.
pod1-1.cs.purdue.edu)

Download the skeleton file
[here](https://www.cs.purdue.edu/homes/gao606/cs352/proj2.zip){:target="_blank"}.

    unzip proj2.zip
    cd proj2

## Step 2: Project Structure

### Browse the Files

A description of the different files is provided below. The files you
need to complete are **Parser.scala**, **SemanticAnalyzer.scala**,
**Interpreter.scala**, and **Compiler.scala**. Following the path of the
first project, we are going to implement the parser step by step. Follow
the comments in the code and find the **TODOs**. The other part are also
independent and can be develop separately.

### src/main/scala/project2/Util.scala

This file defines multiple classes that are used to generate the code
and run it on your machine. Nothing needs to be modified, but it is
recommanded to read it and have an idea of what is happening behind the
scenes.

### gen/bootstrap.c

As we are generating assembly code which is OS dependent, we are using
GCC to do the heavy lifting for us. The boostrap file is a generic C
file that is calling a function **entry_point** and is printing the
result in **stdout**. Our compiler will generate the file **gen/gen.s**
and will be assembled and bootstrapped by gcc:

    gcc bootstrap.c gen.s -o out

**out** will then print the result of our compiled expression.

### src/main/scala/project2/Main.scala

The main function is defined in this file. The data flow in this file
can be seen as:

> Read from File / Read from Command Line -> Parser -> Semantic Analyzer -> Interpreter **or** Compiler

You will be implementing many different parsers in order to test them
through the main function.

The AST generated will then go through the semantic analyzer. If there
are no errors, then the code is going to be interpreted or compiled. We
provide you with one interpreter and one compiler. You will have to
write one of each yourself.

As our language becomes more complex, it will become more useful to read
the code from a source file. A folder with sample files **examples/**
has been provided. Here some examples how to run the code:

    sbt
    > run
    Usage: run PROG [OPTION]
       or: run FILE [OPTION]
    OPTION: compX86, intStack, intValue (default)
    > run examples/valid_arithm.scala              ---> interpreter with the provided interpreter
    > run examples/valid_arithm.scala compX86      ---> x86 compiler (your code)
    > run examples/valid_arithm.scala intStack     ---> stack interpreter (your code)

However, it is still possible to run code from the command line, as in
project 1:

    sbt
    > run "val x = 5; x"
    > run "val x = 5; x" compX86
    > run "val x = 5; x" intStack

### src/main/scala/project2/Parser.scala

This class contains the definition of our intermediate language.

As we discussed in class, parsing the file one character at a time is
not enough when we introduce more complex constructs. Also, our single
digit numbers were a little bit limiting. The **Scanner** class defined
in this file tokenizes the code. You will have to implement the
**getNum** method. Check out the other methods implemented there, as
they are going to be useful for the next part.

The rest of the file is the definition of each parser we are building,
starting from a generic precedence arithmetic parser to the full
language we want to target, including variables, if statements, and
loops. What you have to do for this project is highlighted with TODOs in
the code. We encourage you to read the comments and code carefully
before proceeding.

### src/main/scala/project2/SemanticAnalyzer.scala

While the parser is in charge of verifying that the input string follows
the defined syntax, the semantic analyzer verifies that the program
described is meaningful and follows the rules. For example:

    val x = 2; x = 5

has a valid syntax. However \'val\' is immutable: it is not allowed to
be reassigned to.

Using the functions **error** and **warn**, enforce the following
semantic rules:

-   unary operators supported \"+\", \"-\". Raise: undefined unary
    operator
-   binary operators supported \"+\", \"-\", \"/\", \"\*\". Raise:
    undefined binary operator
-   boolean operators supported \"==\", \"!=\", \"\<=\", \"\>=\",
    \"\<\", \"\>\". Raise: undefined boolean operator
-   \'val\' can not be assigned. Raise: reassignment to val
-   identifier needs to be defined in the current scope before being
    used. Raise: undefined identifier

Note that we allow a variable to be declared multiple times. The last
definition will be used when a reference to it is found. In this case
only a warning is raised.

### src/main/scala/project2/Interpreter.scala

As we have seen in class, now that our programing language accepts more
than just mathematical expressions, we need to define the required
behavior of our language. An interpreter can be used to define this
meaning.

We provide you with an interpreter that is fully functional. Your job is
to complete the **Stack-based** interpreter.

### src/main/scala/project2/Compiler.scala

In this file, one compiler emitting Scala-like code has already been
implemented. You need to implement a second compiler that can convert
our AST into x86_64 code.

In the previous project, we considered two different ways of generating
the assembly code, each of which has pros and cons: **Stack-based**
code, which is not very efficient, but can handle arbitrarily complex
expressions; and **Register-based** code, which is efficient, but can
not handle arbitrarily complex expressions. **For this assignment, we
will use a register-based approach.**

### Tests src/test/scala/project2/\*Test.scala

These files contain some unit tests for the first parsers. <mark>You will
have to write your own tests for the others. Every task should have at
least 2 tests otherwise points will be deducted.</mark> There are some
functions given to you in order to make the implementation easier.

## Turnin

You should turn in the **proj2** directory. Please run an \'sbt clean\'
and \'./cleanall.sh\' before submitting.

To turn in your project create a ZIP file named
`<purdueemailusername>-proj<N>.zip` of the `proj2` directory for
example `axhebraj-proj2.zip` and upload it to the corresponding
assignment on Brightspace.

**No other file formats or naming conventions will be accepted as
submissions. Verify your submission by downloading the ZIP file you
uploaded on Brightspace and extracting its content. The uncompressed
content should be the `proj2` folder containing the code.**

## Grading

Your project will be tested against a set of unit tests. The weights of
each task will be distributed as follow:

  Task              | Weight
  ------------------|---------
  Scanner.getNum    | 5%
  ArithParser       | 10%
  LetParser         | 5%
  BranchParser      | 10%
  VariableParser    | 15%
  LoopParser        | 5%
  SemanticAnalyzer  | 10%
  StackInterpreter  | 15%
  X86Compiler       | 25%
