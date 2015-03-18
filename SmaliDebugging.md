# Overview #

Apktool makes possible to debug smali code step by step, watch variables, set breakpoints, etc.

# General informations #

Generally we need several things to run Java debugging session:

  * debugger server (usually Java VM)
  * debugger client (usually IDE like IntelliJ, Eclipse or Netbeans)
  * client must have sources of debugged application
  * server must have binaries compiled with debugging symbols referencing these sources
  * sources must be java files with at least package and class definitions, to properly connect them with debugging symbols

In our particular situation we have:

  * server: Monitor (Previously DDMS), part of Android SDK, standard for debugging Android applications - explained here: http://developer.android.com/guide/developing/tools/ddms.html
  * client: any JPDA client - most of decent IDEs have support for this protocol.
  * sources: smali code modified by apktool v2 to satisfy above requirements (".java" extension, class declaration, etc.). Apktool modifies them when decoding apk in debug mode.
  * binaries: when building apk in debug mode, apktool removes original symbols and adds new, which are referencing smali code (line numbers, registers/variables, etc.)

To successfully run debugging session apk must be both decoded and built in debug mode.

# General instructions #

Above information is enough to debug smali code using apktool, but if you aren't familiar with DDMS and Java debugging, then you probably still don't know, how to do it. Below are simple instructions for doing it using Netbeans.

  1. Decode apk in debug mode: $ apktool d -d -o out app.apk
  1. Build new apk in debug mode: $ apktool b -d out
  1. Sign, install and run new apk.
  1. Follow sub-instructions below depending on IDE.

## IntelliJ (Android Studio) instructions ##

  1. In IntelliJ add new Java Module Project selecting the "out" directory as project location and the "smali" subdirectory as content root dir.
  1. Run Monitor (Android SDK /tools folder), find your application on a list and click it. Note port information in last column - it should be something like "86xx / 8700".
  1. In IntelliJ: Debug -> Edit Configurations. Since this is a new project, you will have to create a Debugger.
  1. Create a Remote Debugger, with the settings on "Attach" and setting the Port to 8700 (Or whatever Monitor said). The rest of fields should be ok, click "Ok".
  1. Start the debugging sesion. You will see some info in a log and debugging buttons will show up in top panel.
  1. Set breakpoint. You must select line with some instruction, you can't set breakpoint on lines starting with ".", ":" or "#".
  1. Trigger some action in application. If you run at breakpoint, then thread should stop and you will be able to debug step by step, watch variables, etc.

## Netbeans instructions ##

  1. In Netbeans add new Java Project with Existing Sources, select "out" directory as project root and "smali" subdirectory as sources dir.
  1. Run DDMS, find your application on a list and click it. Note port information in last column - it should be something like "86xx / 8700".
  1. In Netbeans: Debug -> Attach Debugger -> select JPDA and set Port to 8700 (or whatever you saw in previous step). Rest of fields should be ok, click "Ok".
  1. Debugging session should start: you will see some info in a log and debugging buttons will show up in top panel.
  1. Set breakpoint. You must select line with some instruction, you can't set breakpoint on lines starting with ".", ":" or "#".
  1. Trigger some action in application. If you run at breakpoint, then thread should stop and you will be able to debug step by step, watch variables, etc.

# Limitations/Issues #

  * Because IDE doesn't have full sources, it doesn't know about classes members and such. Variables watching works because most of data could be read from memory (objects in Java know about their types), but if, for example, you will watch object and it will have some nulled member, then you won't see, what type is this member.