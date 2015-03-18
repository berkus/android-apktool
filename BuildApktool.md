# Introduction #
Apktool is a collection of 1 project, containing 5 sub-projects.

  * brut.apktool.lib - (Main, all the Library code)
  * brut.apktool.cli - The cli interface of the program
  * brut.apktool.smali - fork of [JesusFreke's smali](http://code.google.com/p/smali)  tool
  * brut.j.dir - Utility project
  * brut.j.util - Utility project
  * brut.j.common - Utility project

The main project can be found below

https://github.com/iBotPeaches/Apktool

### Requirements ###
  * Java JDK (1.7)
  * aapt in $PATH (Android Asset Packaging Tool)

### Build Steps ###
We use gradle to build. Its pretty easy. First clone the repository.

```
git clone git://github.com/iBotPeaches/Apktool.git
```

Move into the directory.

```
cd Apktool
```

Issue the build. `./gradlew` for unix based systems. `gradlew.bat` for windows.

```
[./gradlew][gradlew.bat] build fatJar
```

You may also build a Proguard jar
```
[./gradlew][gradlew.bat] build fatJar proguard
```

Then look in

```
./brut.apktool/apktool-cli/build/libs/apktool-xxxxx.jar
```