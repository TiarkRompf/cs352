---
layout: template
title: "Compilers: Principles And Practice"
homepage: true
---

Spring 2026, 3 credits. Instructor: Prof. Tiark Rompf

Announcements will be posted on [Piazza](https://piazza.com/purdue/spring2026/cs352){:target="_blank"}.
Homework submission and grading will be done through [Brightspace](https://purdue.brightspace.com/){:target="_blank"}.

> Lectures are Monday, Wednesday, and Friday, 12:30-1:20pm in LWSN B155.
>
> Teaching assistants are:
>
> - Songlin Jia [(jia137 at purdue.edu)]()
> - Ran Guo [(guo543 at purdue.edu)]()
> - Dongmin Lee [(lee4818 at purdue.edu)]()
>
> PSO sessions are:
>
> - Tuesday 3:30-4:20pm, HAAS 257
> - Tuesday 4:30-5:20pm, HAAS 257
> - Wednesday 10:30-11:20am, HAAS 257
> - Wednesday 11:30am-12:20pm, HAAS 257

<!--
> Final will be held on Wednesday May 1st, 1:00pm to 3:00pm, HORT 117.
-->

# About the Course <a id="about"></a>

**In a nutshell:**
The theory and practice of programming language translation, compilation, and run-time systems, organized around a significant programming project to build a compiler for a simple but non-trivial programming language.

Parts of the class are based on the [Advanced Compiler Construction](https://edu.epfl.ch/coursebook/en/advanced-compiler-construction-CS-420){:target="_blank"} class taught by Michel Schinz at EPFL. The corresponding class materials (lecture slides, programming assignments, etc) are used with permission.

**Grades:** Final grades will be based on results for the programming assignments (30%), midterm (30%), and final exam (40%).
Achieving a minimum of 20% in each of the three components is necessary (but not sufficient!) for a passing grade.

**Late Work Policy:** No late submissions will be accepted. Any travel, including interview trips, load from work or other classes, or simply not being able to get your program to run will not be grounds for extensions or exceptions.

**Academic integrity:**
For general policies about academic integrity etc. Please see [here](http://spaf.cerias.purdue.edu/cpolicy.html){:target="_blank"}.
You are expected to read that page and will be held accountable according to its contents.

**Attendance:**
This is an in-person class. Attendance is encouraged but not required. Most students profit from in-class discussions. But if you prefer to learn on your own that's fine, too.
Lectures won't be recorded but slides will be made available online. You're welcome to take notes in class, but ***strictly no audio or video recordings***.

<!--
# Textbook { #textbook }

- [*Modern compiler implementation in Java*](http://www.cs.princeton.edu/%7Eappel/modern/java), Second Edition, Andrew W. Appel, Cambridge University Press, 1998.

## Supplementary Resources { #textbook }

- [*Compilers: Principles, Techniques, and Tools*](http://dragonbook.stanford.edu), Aho, Lam, Sethi, Ullman, Addison-Wesley, 2007
- [*The Java Language Specification*](http://java.sun.com/docs/books/jls)
- [*The Java programming language*](http://java.sun.com/docs/books/javaprog), Ken Arnold, James Gosling and David Holmes, Addison-Wesley, 2000
- [*Computer Organization and Design: The Hardware/Software Interface*](http://books.elsevier.com/us/mk/us/subindex.asp?isbn=9780123706065&country=United+States&community=mk&ref=&mscssid=C9TPQXSQGMC69MDPB7HVBN4GMSHT0EB5), David Patterson and John Hennessy, Morgan Kaufmann, 1998
- [*The Java Tutorial*](http://java.sun.com/docs/books/tutorial)
- [Generics for Java](http://java.sun.com/developer/earlyAccess/adding_generics/)
- [Java Documentation](http://java.sun.com/docs)
- [Java APIs](http://java.sun.com/apis.html)
- [JavaCC](../javacc/doc)
- [*SPIM: A MIPS R2000 Simulator*](http://www.cs.wisc.edu/%7Elarus/spim.html) <br> [Documentation](spim.pdf)
- PowerPC
    * [Beginner's guide to PowerPC assembly language](http://www.lightsoft.co.uk/Fantasm/Beginners/begin1.html)
    * [Mac OS X Developer Tools](http://developer.apple.com/reference/DeveloperTools)
    * [Mac OS X Assembler Guide](http://developer.apple.com/documentation/DeveloperTools/Reference/Assembler)
    * [Mac OS X ABI Function Call Guide](http://developer.apple.com/documentation/DeveloperTools/Conceptual/LowLevelABI)
    * [Mac OS X ABI Mach-O File Format Reference](http://developer.apple.com/documentation/DeveloperTools/Conceptual/MachORuntime)
-->


# Recommended Books <a id="textbook"></a>

- [*Modern compiler implementation in Java*](http://www.cs.princeton.edu/%7Eappel/modern/java){:target="_blank"}, Second Edition, Andrew W. Appel, Cambridge University Press, 1998.
- [*An Incremental Approach to Compiler Construction*](http://scheme2006.cs.uchicago.edu/11-ghuloum.pdf){:target="_blank"}, Abdulaziz Ghuloum, 2006.
- [*Engineering a Compiler*](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=3&ved=0ahUKEwip386f9drVAhXB34MKHRLPCokQFggyMAI&url=http%3A%2F%2Fbank.engzenon.com%2Fdownload%2F560e72f1-0a74-4507-8385-12aec0feb99b%2FEngineering_a_Compiler_2nd_edition_by_Cooper_and_Torczon.pdf&usg=AFQjCNFSp0DjfX-AzwUnRl-eiBq8RxlHLA){:target="_blank"}, Second Edition, Keith D. Cooper, Linda Torczon, 2007.
- [*Compilers: Principles, Techniques, and Tools*](http://dragonbook.stanford.edu){:target="_blank"}, Aho, Lam, Sethi, Ullman, Addison-Wesley, 2007.

## Supplementary Resources

- [Scala Cheatsheet](https://docs.scala-lang.org/cheatsheets/index.html){:target="_blank"}
- [x86_64 Cheatsheet](https://cs.brown.edu/courses/cs033/docs/guides/x64_cheatsheet.pdf){:target="_blank"}

# Lecture Notes

A set of lecture notes is available here:

- [Post-Modern Compiler Design](https://www.cs.purdue.edu/homes/rompf/pmca/){:target="_blank"}

# Slides <a id="schedule"></a>

Week 1

- Introduction to Compilers [(pdf)](https://www.cs.purdue.edu/homes/jia137/cs352/week1-1.pdf){:target="_blank"}
- Operator precedence and Tokenization  [(pdf)](https://www.cs.purdue.edu/homes/jia137/cs352/week1-2.pdf){:target="_blank"}

Week 2

- Error handling - Semantics - Branches [(pdf)](https://www.cs.purdue.edu/homes/jia137/cs352/week2-1.pdf){:target="_blank"}
- Variables - Loops - Type Checking [(pdf)](https://www.cs.purdue.edu/homes/jia137/cs352/week2-2.pdf){:target="_blank"}

<!--
Week 3

- Type Checking/Inference - Functions [(pdf)](https://www.cs.purdue.edu/homes/huan1464/cs352/week3-1.pdf){:target="_blank"}
- Functions - Arrays [(pdf)](https://www.cs.purdue.edu/homes/huan1464/cs352/week3-2.pdf){:target="_blank"}

Week 4-5

- Intermediate Representations [(pdf)](https://www.cs.purdue.edu/homes/huan1464/cs352/week4-1.pdf){:target="_blank"}
- Values Representation [(pdf)](https://www.cs.purdue.edu/homes/huan1464/cs352/week5-1.pdf){:target="_blank"}

Week 6-7

- Closure Conversion [(pdf)](https://www.cs.purdue.edu/homes/huan1464/cs352/week6-1.pdf){:target="_blank"}

Week 8

- Optimizations [(pdf)](https://www.cs.purdue.edu/homes/huan1464/cs352/week7-1.pdf){:target="_blank"}

Week 9

- Dataflow Analysis [(pdf)](https://www.cs.purdue.edu/homes/huan1464/cs352/week8-1.pdf){:target="_blank"}


Week 12-14

- Register Allocation [(pdf)](https://www.cs.purdue.edu/homes/huan1464/cs352/week10-2.pdf){:target="_blank"}
- Instruction Scheduling [(pdf)](https://www.cs.purdue.edu/homes/huan1464/cs352/week11-2.pdf){:target="_blank"}
- Tail Call [(pdf)](https://www.cs.purdue.edu/homes/huan1464/cs352/week12-1.pdf){:target="_blank"}

Week 15-16

- Interpreters And Virtual Machines [(pdf)](https://www.cs.purdue.edu/homes/huan1464/cs352/week12-2.pdf){:target="_blank"}
- Memory Management [(pdf)](https://www.cs.purdue.edu/homes/huan1464/cs352/week13-1.pdf){:target="_blank"}

Week 17

- Object-Oriented Languages [(pdf)](https://www.cs.purdue.edu/homes/huan1464/cs352/week14-1.pdf){:target="_blank"} -->


<!-- - TurboFan JIT Design [(link)](https://docs.google.com/presentation/d/1sOEF4MlF7LeO7uq-uThJSulJlTh--wgLeaVibsbb3tc/htmlpresent) -->

<!--
Extra material:
- [Dataflow Analysis](http://lamp.epfl.ch/files/content/sites/lamp/files/teaching/advanced-compiler-construction/spring-2015/slides/acc15_07_dataflow-analysis.pdf)
- [Register Allocation](http://lamp.epfl.ch/files/content/sites/lamp/files/teaching/advanced-compiler-construction/spring-2015/slides/acc15_08_register-allocation.pdf)
- [Instruction Scheduling](http://lamp.epfl.ch/files/content/sites/lamp/files/teaching/advanced-compiler-construction/spring-2015/slides/acc15_13_instruction-scheduling.pdf)
- [Memory Management](http://lamp.epfl.ch/files/content/sites/lamp/files/teaching/advanced-compiler-construction/spring-2015/slides/acc15_11_memory-management.pdf)
- [CS352 Liveness Analysis Slides](https://www.cs.purdue.edu/homes/ehanau/cs352/supplemental/registerliveness.pdf)
- [CS352 Reaching Definition Slides](https://www.cs.purdue.edu/homes/ehanau/cs352/supplemental/reachdef.pdf)
-->

# Projects <a id="project"></a>

- [Project 1: Arithmetic](project1.html) (due 11:59pm Sunday Jan 18)
- [Project 2: Branches, Loops, and Error Handling](project2.html) (due 11:59pm Sunday Jan 25)
- [Project 3: Type Checking - Functions - Heap Allocation](project3.html) (due 11:59pm Sunday Feb 8)

<!--
- [Project 4: CMScala to CPS Translation](project4.html) (due 11:59pm Sunday Feb 23)
- [Project 5: Value Representation](project5.html) (due 11:59pm Sunday Mar 9)
- [Project 6: Optimization](project6.html) (due 11:59pm Sunday Apr 6)
- [Project 7: Garbage Collection](project7.html) (due 11:59pm Sunday Apr 27) -->
