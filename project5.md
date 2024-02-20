---
title: "Project 5: Value Representation"
usetable: true
layout: template
---

> Due 11:59pm Monday Mar 4 (two weeks project)

Your task in this assignment is to implement a compiler phase for the
CPS value representation transformation, including closure conversion.
In the skeleton code, you will find a template for this compiler phase
in class `miniscala.CPSValueRepresenter`. You can (and are
encouraged to) use the helper methods in class
`CPSValueRepresenter`, `CPSTreeModule.Tree`, and object
`BitTwiddling`. Please note that the the following aspects will be
taken into consideration while grading:

-   Correctness of the implementation.
-   The time and memory efficiency of the implementation.

For instance, transforming a primitive operation *x op y* by naively
decoding the arguments *(x,y)* and encoding the result back will fetch
you fewer points if there exists a better translation that avoids,
either completely or partially, some encodings/decodings. Note: To that
end, make sure to use left shift (`<<`) and right shift (`>>`) operations
to implement multiplication and division by 2 as described in the lectures.

For the closure conversion part, you can choose to implement either the
\"simple\" or the optimized version. Correctly implementing the
simplified one will give you 90% of the grade for this assignment,
whereas a correct implementation of the optimized transformation will
give you 110% of the grade. An optimized version that works without
supporting recursive/mutually recursive calls will give you 100% (you
can still have function calls if they are not recursive). The extra 10%
will be given if recursive and mutually recursive function calls can be
handled properly.

Notice, however, that by submitting an incorrect version of the
optimized transformation you may lose a lot of points depending on the
mistakes. Therefore, we recommend that you start by implementing the
basic closure conversion procedure and, if you are successful and still
have time, to extend it to the optimized procedure.

NOTE: many functions have an implicit argument **worker**. This argument
should not be useful in the non-optimized version, therefore you are
free to pass the value **Map.empty** to a function call.

## CPS Low Level

The value representation phase of the MiniScala compiler takes as input
a CPS program where all values and primitives are \"high-level,\" in
that they have the semantics which the MiniScala language gives them. It
produces a \"low-level\" version of that program as output, in which all
values are either integers or pointers and primitives correspond
directly to instructions of a typical microprocessor.

This means that the primitive operations used in the CPSLow code
(defined in `CPSPrimitives`) are only executing operations on
integers (or pointers for block operations). All primitives are
performing the operation that you could be expecting based on the name.
The CPSByteWrite primitive returns the unit value. You can
checkout the `CPSLowInterpreter` in the **CPSInterpreter.scala**
file and make sure you understand the CPSLow semantics.

## Testing

From this assignment on, you will choose the shapes for the trees you
generate. You should inspect them visually and decide whether or not
they are correct and optimal. The application in the given skeleton code
will not have whitebox tests, but it will still have an extensive
blackbox test suite to ensure the correctness of the programs you
generate.

Although we will not test tree shapes, we still encourage you to do so
for every transformation rule you write. You have the necessary
infrastructure in `miniscala.test.CPSValueRepresentation_Whitebox`
so it\'s a matter of just writing the source code and the resulting
tree. It is usually an effort that pays off.

<mark>You should write 10 tests otherwise points will be deducted.</mark>

## Road Map

-   Spend the time to understand the task that has to be accomplished.
    This means reading the material and the lectures carefully. A good
    idea to make sure you understand is to manually transform some piece
    of code. While doing that, write this as a test case! Two birds, one
    stone.
-   Implement the actual value transformation function, keep the closure
    conversion for last. Test every cases! Of course the best way is to
    write at least one test case for it, but if you are not willing to
    write tests then verify that you can generate code that produces a
    correct result for simple programs. **Do not use** sbt test
    everytime you add a case to see if you pass more tests! Many of the
    Blackbox tests will fail unless the closure conversion has been
    implemented.

Tips:

-   The implementation can be very technical in some cases, so make sure
    that you are making good use of the helping function to avoid
    clustered code!
-   When creating fresh variable names, you can try to add some
    information that will help you to debug. For example, when creating
    a name for the worker of the function \"test\" you may prefer to use
    `Symbol.fresh("test_worker")` rather than
    `Symbol.fresh("w")`.

The skeleton code for the assignment is available
[here](https://www.cs.purdue.edu/homes/gao606/cs352/proj5.zip){:target="_blank"}.

This assignment relies on the correct implementation of the previous one
(the `CMScalaToCPSTranslator` class). If you are confident that
your implementation of `CMScalaToCPSTranslator` is correct, feel
free to use your implementation. You are also free to use the reference
implementation that is part of the skeleton for Project 5.

## Turnin

You should turn in the **proj5** directory. Please run an \'sbt clean\'
and \'./cleanall.sh\' before submitting.

To turn in your project create a ZIP file named
`<purdueemailusername>-proj<N>.zip` of the `proj5` directory for
example `axhebraj-proj5.zip` and upload it to the corresponding
assignment on Brightspace.

**No other file formats or naming conventions will be accepted as
submissions. Verify your submission by downloading the ZIP file you
uploaded on Brightspace and extracting its content. The uncompressed
content should be the `proj5` folder containing the code.**
