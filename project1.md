---
title: "Project 1: Arithmetic Expressions"
usetable: true
layout: template
---

> Due 11:59pm Sunday Jan 14

## Useful Links

- [x86_64 cheat sheet (up to page 3 for this project)](https://cs.brown.edu/courses/cs033/docs/guides/x64_cheatsheet.pdf){:target="_blank"}

## Introduction

The goal of this project is to setup the environment and to learn how to
parse and translate mathematical expressions into x86_64 assembly code.
Our approach will be simple and the objective is to highlight some of
the key aspects and ideas behind a compiler.

For this first project, we are going to keep things very simple and take
very small steps. Make sure that you understand everything correctly
before going to the next step.

At the end of the project, we will be able to parse mathematical
expressions with single digit numbers, addition, substraction,
multiplication, division, and parentheses. Our parser will generate an
intermediate representation in the form of an Abstract Syntax Tree
(AST). The definition of the AST is the one used during the lecture.

In parallel, we will implement a generator that converts the AST into
x86_64 code.

Here is a small example of what we will be able to generate by the end
of the project:

    [info] Running project1.Runner 2+3
    ============= AST ================
        Plus(Lit(2),Lit(3))
    ==================================

    ============ OUTPUT ==============
    .text
        .global entry_point

    entry_point:
        push %rbp   # save stack frame for C convention
        mov %rsp, %rbp

        # beginning generated code
        movq $2, %rbx
        movq $3, %rcx
        addq %rcx, %rbx
        movq %rbx, %rax
        # end generated code
        # %rax contains the result

        mov %rbp, %rsp  # reset frame
        pop %rbp
        ret



    ==================================
    Result: 5

## Step 1: Getting Started

The first step of this assignment is to set up your environment as
described in the [Getting Started - Tools page](getting_started.html).
If you have any trouble installing the tools for the course, ask the for
help on Piazza as soon as possible. TAs or other students might help
troubleshoot and solve your issue.

You can do the project on your own machine or lab machines and then
upload your submission on Brightspace.

The project has been designed and tested for Linux/Mac OS. If you have
only Windows installed on your laptop consider running Linux in a VM, or
use the lab machines for the project. (However it should be working on
Windows as well)

If you use remote access to work on your project, please use one of the
lab machines data/pod1-1 to pod1-20 with the suffix cs.purdue.edu (e.g.
pod1-1.cs.purdue.edu, data.cs.purdue.edu)

Download the skeleton file
[proj1.zip](https://www.cs.purdue.edu/homes/gao606/cs352/proj1.zip){:target="_blank"}.

    unzip proj1.zip
    cd proj1

## Step 2: Project Structure

### Open Project in Your Favorite Scala IDE

### Browse the Files

A description of the different files is provided below. The two files
you need to complete are **Parser.scala** and **Generator.scala**. Each
parser that we are going to implement builds on top of another, so you
need to implements them in order by following the comments in the code.
We will implement two different generators using two different
strategies. It is recommended to implement the **StackASMGenerator**
class when it is suggested in the **Parser.scala** file, and implement
the **RegASMGenerator** at the end.

### build.sbt and project/plugin.sbt

The Scala Build Tool (sbt) is an open source build tool for Scala and
Java projects. These files contain the information necessary to compile
this project. You should not have to modify them.

To use sbt, launch a terminal and go to the project directory (proj1)
and enter `sbt`. It will lauch an sbt console. You can run the program
from there:

    run "arg1" "arg2" // run main program with arguments arg1 and arg2
    run "1+3*(5-8)"
    test              // run all the tests application (in src/test)

### src/main/scala/project1/Util.scala

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

NOTE: the assembly/compilation and running steps are executed through
the code. (see Util.scala#L88 and Main.scala#L39)

### src/main/scala/project1/Main.scala

The main function is defined in this file. During this project, you will
be implementing many different parsers in order to test them through the
main function. You will need to modify the parser or generator you want
to use.

### src/main/scala/project1/Parser.scala

This class contains the definition of our intermediate language. This is
the language we are using in class; please refer to the lecture for more
information.

The class **SimpleParser** defined in this file is the basic parser that
we are going to use for this project. It is reading a stream of
characters one at a time and can extract a single digit number
**getNum** or a single letter name **getName**. It does not handle
whitespace.

We are keeping the parser very simple at the beginning to focus on the
important concepts. Later on, we will improve it to handle multiple
digits numbers and more expressions. We will also support whitespace.

The rest of the file is the definition of each parser we are building,
starting from single number expressions to the full language we want to
target. What you have to do for this project is highlighted with TODOs
in the code. We encourage you to read the comments and code carefully
before proceeding.

### src/main/scala/project1/Generator.scala

In this file, we are defining some generators that can convert our AST
into x86_64 code.

We consider two different ways of generating the assmbly code, each of
which has pros and cons: **Stack-based** code, which is not very
efficient but can handle arbitrarily complex expressions; and
**Register-based** code, which is efficient but can not handle
arbitrarily complex expressions. We will see later that compilers use a
hybrid approach.

### src/test/scala/project1/test/\*Test.scala

These files contain some unit tests for the first parsers. You will have
to write your own tests for the others. There are some functions given
to you in order to make the implementation easier.

## Turnin

You should turn in the **proj1** directory. Please run an 'sbt clean'
and './cleanall.sh' before submitting.

To turn in your project create a ZIP file named
`<purdueemailusername>-proj<N>.zip` of the `proj1` directory for
example `axhebraj-proj1.zip` and upload it to the corresponding
assignment on Brightspace.

**No other file formats or naming conventions will be accepted as
submissions. Verify your submission by downloading the ZIP file you
uploaded on Brightspace and extracting its content. The uncompressed
content should be the `proj1` folder containing the code.**

## Grading

Your project will be tested against a set of unit tests. The weights of
each task will be distributed as follow:

  Task               | Weight
  -------------------|--------
  parseTerm          | 20%
  parseFactor        | 20%
  StackASMGenerator  | 30%
  RegASMGenerator    | 30%