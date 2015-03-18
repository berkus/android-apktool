# Dreams about the future #

These are my thoughts/plans/dreams/vision about the future of apktool and omnipatcher.

Let's assume we have some apk file or group of apk files and want to modify them. We will go through whole process and all possibilities from the beginning to the end.

## Decode ##

First we need to decode it. This is one-line command, creates directory with Android-project-like structure. We can choose method to decode:

  * sources:
    * none: there will be a classes.dex file in an output directory
    * baksmali: `*`.smali files in a smali subdirectory
    * java: `*`.java files in a src subdirectory
  * resources:
    * none: original resources.arsc, AndroidManifest.xml and res subdirectory
    * XMLs: like none, but all XMLs in textual form
    * resources.arsc: like none, but res/values`*`/`*`.xml files generated, resources.arsc file replaced by resources.map - a textual file containing resourceId`<->`resourceName mappings
    * full: both above

Default is java/full and there are little advantage to changing it: faster decoding and building mainly.

Also there will be a build.xml file - this will simplify integration with some IDEs, etc.

## Edit ##

Depends on what you have decoded and what you want to do. You can replace/add/delete images, sounds, etc., modify layouts, string values, Manifest and other XMLs, make some changes to code of an app, etc., etc. If you have chosen java/full, you can even open it in Eclipse as any other Android project and get ADT plugin support: edit layouts graphically, etc.

## Build ##

You can use apktool CLI interface or ant tool. Commands are similar to that from Android project:

  * build apk
  * build, sign, zipalign
  * build, sign, zipalign, install
  * build, sign, zipalign, install, run
  * build, sign, zipalign, package as update.zip file

Signing can use:

  * builtin "debug" key
  * yours key, defined in some config file, so you will have to enter password to keystore only
  * testkey

## Patches ##

There are many reasons, why you may want to create one:

  * don't want to distribute proprietary stuff
  * want to easily port changes to other versions of an apk
  * want to distribute smaller files
  * want to distribute packages of several modified apks
  * want to make possible to join yours and others changes of the same apk

Changes contained in a patch may be of different types and forms:

| | **diff** | **bindiff** | **replacement** |
|:|:---------|:------------|:----------------|
| **new bin file** |  |  | X |
| **changed bin file** |  | X | X |
| **deleted bin file** | X |  |  |
| **smali code changes** | X | X | X |
| **java code changes** | X | X | X |
| **res XML changes** | X | X | X |

**Diffs** are textual differeneces between text assets, decoded sources or XML resources. They are smallest, reversable, most portable, free of proprietary stuff, joinable with others patches and generally most useful for developers, but also technically hardest to apply.

**Bindiffs** are binary diffs between binary assets, undecoded XMLs, classes.dex or resources.arsc files. They are most specific to single one version of an app, potentially possible to join with other patches, somewhat proprietary-free and easy to apply, but not always possible to generate. They are probably the best ones for a distribution.

**Replacements** are just a new versions of files. They are least joinable with other patches, may contain a lot of proprietary stuff and if applied to other version of an app, for which they are built, they may broke it and you won't know about it at apply time. They should be used for situations, where bindiff fails, mainly for binary resources (images, sounds, etc.).

Diffs are generally the best one, give most possibilities, but it is quite probable, that we won't be able to apply them directly on a device.

### Create ###

You can use apktool to create a patch by differenting two versions of an app. Apps can be in a binary or decoded format.

### Apply ###

You can apply patch on a PC using apktool or directly on a device using Omnipatcher. It is quite probable that not every patch will be appliable by Omnipatcher (diff format may be a problem).

### Convert ###

You can convert patch to other format using apktool. To do this you must have an app, which could by patched by this patch.

## Examples ##

  * App was abandoned by its author or he is not known - there are only binaries and no sources. Someone has modified it and put apk on his website to download. He also released diff patch to show to other developers, what was changed.
  * App is proprietary and this is not a good idea to put modified version onto website. Developer releases bindiff, so every noob can apply it easily using omnipatcher. He could also release diff patch for other developers.
  * There are many simple modifications to a single app. They are released in separate bindiffs, so one can easily apply only these modifications, which he want.
  * Same as above, but some changes are related to same objects, so bindiffs are not appliable one after another. One can download conflicting bindiffs and try to join them as diff patches using apktool. Then he can release changes as one bindiff.
  * Developer has added new features to some actively developed app. He stores his changes in a diff patch, so he can easily generate bindiffs for each new official release of this app.

I think you get an idea.

## Ending words ##

That is a hell of lot of work to do, but we have time. Android will be more and more popular and app structure assumptions are not likely to change too soon, so what we will do, will be useful for years, I think. Really nice thing is that all these ideas above were my dreams just a few months ago, now some of them are reality and others became my goals. It makes me feel good about the future :-)

I wanna open source my works, cause we need more developers to work on it. I have started this project and I hope I showed others that there are possibilities to greatly enhance apps modding process.