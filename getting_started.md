---
title: Getting Started
layout: template
---

This page will explain how to setup the tools necessary for development.
The tools necessary for development are:

- **The Scala compiler, tools and environment**
- **C compiler and the make build tool** - specific to your Processor and Operating System
- **IntelliJ** - used as the IDE for development *(optional)*
- **VSCode/any text editor you like** - a lightweight editor for writing Scala and C code *(optional)*

### Setting up the development tools on your machine

The tools you will need to install and configure are:

-   [Java Virtual Machine, Scala REPL (Read, Eval, Print Loop) and sbt](#local-scala)
-   [a C compiler and the make utility](#local-c)
-   git for keeping versions of your files *(optional)*
-   [IDE or text editor](#local-ide)

Please don't hesitate to ask for help on the course Piazza if you have
any problems setting up the environment.

As the projects are to generate code in x86_64 assembly, the projects
will be tested on an x86_64 Linux server. Thus, developing on non-x86_64
non-Unix-like platform is possible but **not** recommended. Consider
[using a LWSN server](#remote-dev) if that is your case.

## <a id="local-scala">Installing Scala</a>

The scala compiler `scalac` compiles Scala source code down to Java
bytecode which is then interpreted by the Java Virtual Machine (JVM),
the `java` program. Additionally, `sbt` (the Simple Build
Tool) is often used to manage and build the projects. For this course,
we are using the following versions,

- Java (openjdk 17)
- sbt (1.10.5)
- Scala (2.12.18, optional)

Note that Scala 3.x or Scala 2.13.x will **not** work for this course. However, `sbt` manages the
Scala version for each project individually, so it is optional to ensure the
correct version of Scala installed. Using other versions of `java` or `sbt` may
work, but does not guarantee passing the tests when grading.
Installation instructions for these tools are as follows.

<!-- ### SDKMAN!

[SDKMAN!](https://sdkman.io/){:target="_blank"} is a package management tool for
JVM-related environments. Before using it, follow the instructions
[here](https://sdkman.io/install){:target="_blank"} to install it. Next, type

    $ sdk install java 17.0.13-tem
    ...
    $ sdk install scala 2.12.18
    ...
    $ sdk install sbt 1.10.5
    ...

and then you will be able to check the versions of `java` and `sbt` as specified in
the previous section. Additionally, you can check 

To test that the installation succeeded write a file like
`HelloWorld.scala` with the following content.

```scala
object HelloWorld {
    def main(args: Array[String]) = {
    println("Hello World!")
    }
}
```

From the directory you've created the file in, run

    $ scala HelloWorld.scala
    Hello World!
-->

### Coursier

[Coursier](https://get-coursier.io/docs/overview) is a tool for getting Scala applications and artifacts.
The following command works on x86-64 Linux and
will install JDK 17, the Scala REPL `scala` and `sbt`.

    curl -fL "https://github.com/coursier/launchers/raw/master/cs-x86_64-pc-linux.gz" | gzip -d > cs
    chmod +x cs
    # Remove `--jvm openjdk:17` if you already have a system-level JDK 17.
    ./cs setup --jvm openjdk:17 -y --apps sbt:1.10.5,scala:2.12.18,cs
    rm cs

If you are using macOS or a different architecture, you need [different links](https://get-coursier.io/docs/cli-installation#launcher-urls)
for downloading Coursier. Please note that the first three projects require
a x86-64 platform for testing.

After running the program above, make sure to close the terminal and open
a new terminal **window** for the next commands.
You should be able to invoke the
java virtual machine in a Terminal (or Command Prompt):

    $ java -version
    openjdk version "17.0.0" 
    ...

and also the standalone `scala`:

    $ scala -version
    Scala code runner version 2.12.18 -- Copyright 2002-2019, LAMP/EPFL and Lightbend, Inc.

You should be able to invoke `sbt`. To test, run the `sbt` command
in a project folder (e.g. `proj1/`). After some downloads, the sbt repl should
start

    $ cd proj1
    $ sbt
    [info] [launcher] getting org.scala-sbt sbt 1.10.5  (this may take some time)...
    # ......
    [info] Set current project to root (in build file:/)
    [info] sbt server started at local:///root/.sbt/1.0/server/e656f0eb572233bacf5f/sock
    sbt:root>

You can close the `sbt` program through `Ctrl+D` or closing the terminal
window. The command above will generate the `target` and `project`
directories. It is safe to delete both directories.

As an alternative to Coursier, you may also use [SDKMAN!](https://sdkman.io/){:target="_blank"}
to manage JVM-related environments. We recommend using `java 17.0.13-tem`
from SDKMAN.

### Structure of a Scala Project

Although it would be possible to compile projects manually using the
`scalac` command, scala projects use the `sbt` tool and have the
following directory structure.

    my-app
    ├── build.sbt
    └── src
        ├── main
        │   └── scala
        │       ├── util_package
        │       │   └── Lib.scala
        │       └── Main.scala
        └── test
            └── scala
                └── util_package

The `build.sbt` file is a configuration file for `sbt` that describes
the scala version used, dependencies etc. Source files are usually found
under `src/main/scala`. This directory denotes that the source files are
Scala code. Similarly to Java, package hierarchy is reflected in the
directory structure.

## <a id="local-c">Installing a C Compiler, a debugger and the make build tool</a>

These tools depend on the operating system you will be using. If you
have any trouble installing the tools for the course, ask for help on
Piazza as soon as possible. TAs or other students might help
troubleshoot and solve your issue. If all suggestions fail, setup your
machine for remote development as described in [Remote development with VSCode on LWSN servers](#remote-dev)

### Debian-based Linux distribution

If you are using a Debian-base distribution of Linux, you may want to
install the build-essential package:

    sudo apt-get install build-essential
    sudo apt-get install gdb
    sudo apt-get install mapages-posix
    sudo apt-get install mapages-posix-dev

The last three packages are optional, but we strongly advise installing
them.

### RedHat-based Linux distribution

For RedHat-based distributions use the yum installer:

    yum groupinstall "Development Tools"

### MacOSX

For MacOSX use homebrew:

      brew install gcc
      brew install gdb

### Windows

Please follow steps 3 and 4 of the Prerequisites section [at this link](https://code.visualstudio.com/docs/cpp/config-mingw#_prerequisites){:target="_blank"}
and install gcc, gdb, make and bash. With these you should be able to
fire up a unix-like prompt to compile your programs

Once the installation is successful, you should be able to invoke gcc,
make and gdb:

## <a id="local-ide">Installing an IDE</a>

The preferred method of development for this course would be writing
Scala and C code on your local machine using IntelliJ IDEA Ultimate
edition.

### Installing and configuring IntelliJ

A popular IDE for Scala is IntelliJ, which you can find
[here](https://www.jetbrains.com/idea/download/){:target="_blank"}. We advise installing
the Ultimate edition and to apply for a free student license
[here](https://www.jetbrains.com/student/){:target="_blank"}. Always make sure to have the
latest version installed. Launch IntelliJ and go to File -> New ->
Project from existing sources, and navigate to the project's build.sbt
file. Choose the Java 17 as the project's SDK. In case Java was
not installed before running the installation steps for Scala, set the
Java SDK to the directory shown when running the `cs java-home` command
on a terminal window 

The simplest way is to import the project as an 'sbt project'. Be sure
to check 'sbt shell' in the import settings.

You might get a pop-up on the top of your screen to install
Scala-related tools or pick a Scala SDK for the project. Make sure to
configure them and you're good to go.

### VS Code/Vim/Emacs/\<insert your favorite editor\>

IntelliJ might be slow on machines with few resources. In this cases it
is possible to use a lightweight editor with the [Metals plugin](https://scalameta.org/metals/docs/){:target="_blank"}.
Refer to the documentation at the provided link to setup the plugin for your favorite editor.

## <a id="remote-dev">Remote development with VSCode on LWSN servers</a>

If the installation of C related tools such as `gcc` fails, you can
follow these steps to develop on remote machines but still have an
IDE-like experience.

- [Connect](https://www.cs.purdue.edu/resources/instructional/teaching-remotely/ssh-scp.html){:target="_blank"}
  to one of the [LWSN servers](https://www.cs.purdue.edu/resources/facilities/lwsnservers.html){:target="_blank"}
  and perform the commands shown in section [Installing Scala](#local-scala).
-   Install [VSCode](https://code.visualstudio.com/){:target="_blank"}
-   From the extension tab on VSCode install the [Remote Development](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack){:target="_blank"}
    extension
-   From VSCode, connect to the remote host as shown in the [Connect to a remote host](https://code.visualstudio.com/docs/remote/ssh#_connect-to-a-remote-host){:target="_blank"}
    section on their guide
-   From the extension tab on VSCode install the
    [Metals](https://marketplace.visualstudio.com/items?itemName=scalameta.metals){:target="_blank"}
    extension on the remote machine (tips on how to use it at [the documentation](https://scalameta.org/metals/docs/){:target="_blank"})

Congratulations, you've set up the tools you will use for CS352!
