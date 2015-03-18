# Known and frequent issues #

People very often report some issues that aren't actually issues or they just don't know what to do. Below list is some kind of a FAQ, but for specific issues:


---


## "error: Error: Resource is not public." ##

The correct fix is to move the "private extended" styles into that applications styles.xml. You can look at AOSP styles.xml to get the list of those styles which are private. Then simply add them into that APKs styles and all should work. This was tested and worked with the problematic apks.

Apktool isn't met to "fix" apks. As AAPT becomes more restrictive, Apktool will become more difficult to use. These APKs that have this problem were obviously built with an older AAPT before this was enforced. So this actually is NOT an apktool problem. Just a problem building old vs new aapt.

I am writing a good deal of documentation to explain stuff like this for 2.0, but this bug in particular is not really a bug, but a feature request to somehow automatically re-map privately extended styles automatically into the local styles.


---


## "error: Public symbol aaa/bbb declared here is not defined." ##

Usually this isn't an issue by itself, but it's a symptom of other issue. It's general error which may be caused by various specific ones. If you are building an application and there is an error in one of files, this file is ignored and building procedure goes on. Then you get plenty of above errors cause of missing files.

Just look above these errors, there you should find another, real ones. This is general rule for reading error messages: earlier messages are always more important, they might cause later ones.

If error messages are bigger than console/window buffer, so you can't read first lines of output, you will have to increase buffer size. Search for this in console properties.


---


## INSTALL\_PARSE\_FAILED\_NO\_CERTIFICATES ##

This means: "you have tried to install apk which wasn't signed". Just sign this file - as you does when you build apk from sources (did I told you working with apktool'd application is very similar to working with sources?).


---


## Some APKs won't decompile ##

I've found that some APKs don't conform to regular Android standards. They were probably built using a modified aapt, which makes decompiling near impossible. These APKs are called "Magic" apks and probably won't be supported.


---


## "java.lang.UnsupportedClassVersionError: brut/apktool/Main : Unsupported major.minor version 51.0" ##

You need to update to Java7. Also setting PATH variables correctly so that executing `java -version` on command line / command prompt results in Java7.


---
