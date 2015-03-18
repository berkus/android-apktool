## 2.0.0 ##
2014.xx.xx

MigrationInstructions

## 1.5.2 ##
2013.02.02

  * Fixed ([issue #299](https://code.google.com/p/android-apktool/issues/detail?id=#299)) - output smali filename errors to screen during rebuild instead of filestream
  * Only show the --aapt / -a info in verbose mode.
  * Fixed ([issue #392](https://code.google.com/p/android-apktool/issues/detail?id=#392)) - Don't crash out if .git folder isn't present. Use SNAPSHOT-DEV instead.
  * Fixed ([issue #67](https://code.google.com/p/android-apktool/issues/detail?id=#67)) - Only store compressed resources.arsc if original was compressed, otherwise STORE.
  * Moved build.gradle files to each sub-project, more organization :)
  * Fixed ([issue #394](https://code.google.com/p/android-apktool/issues/detail?id=#394)) - Prevented duplicated files in final jar which saved around 1.2mb.
  * Added Proguard to drop final jar size from 6.2mb to 2.6mb.
  * Fixed ([issue #395](https://code.google.com/p/android-apktool/issues/detail?id=#395)) - Added check for "aapt" in unit-tests.
  * Added ability to use "--frame-path" on [if|install-framework]
  * Fixed renaming of ".r.9.png" images -> ".9.png".
  * Added ability to use --version to print out Apktool version
## 1.5.1 ##
2012.12.28

MigrationInstructions

  * **Android 4.2 support**
  * Added -a / -aapt command on rebuild to specify location of aapt
  * Updated unit tests for 4.2 support
  * Closed file-handler when writing frameworks to file system.
  * Updated to Gradle 1.3
  * Properly deleted tmp files after building apk ([issue #365](https://code.google.com/p/android-apktool/issues/detail?id=#365))
  * Added support for renamed packages via --renamed-manifest-package ([issue #252](https://code.google.com/p/android-apktool/issues/detail?id=#252))
  * Option to specify framework folder ([issue #175](https://code.google.com/p/android-apktool/issues/detail?id=#175))
  * Prevents removal of configChanges in AndroidManifest ([issue #304](https://code.google.com/p/android-apktool/issues/detail?id=#304))
  * Updated snakeyaml to 1.11  to fix "unacceptable character" errors. ([issue #360](https://code.google.com/p/android-apktool/issues/detail?id=#360))
  * Updated smali/baksmali to v1.4.1
  * Fixed reference-array problem ( pull request [#53](https://github.com/iBotPeaches/Apktool/pull/53)))
  * Fixed bad spacing issue on Mac OS X (pull request [#49](https://github.com/iBotPeaches/Apktool/pull/49))
  * Removed maven in favor of gradle
  * Removed Maven REPOs that were used if local projects didn’t exist.
  * Merged brut.j.dir,brut.j.common,brut.j.util & brut.apktool.smali (Fork of JesusFreke’s smali) into one repo.
  * Fix –verbose mode to actually work
  * Added SDK API 17 framework
## 1.5.0 ##
2012.09.02

  * Fix for colours being decompiled with wrong hex code
  * Fix for `<string-array>` being treated as `<array>`
  * Support for Mac OS X user:home instead of /home
  * updated builtin framework to SDK API16
  * Added `<user-sdk>` into apktool.yml for future aapt changes
  * Half fixed -d mode
  * Added --verbose commands to output contents from aapt (help with debugging)
  * Ignore bootclasspath on debug mode

## 1.4.10 ##
2012.08.21

  * Fix for bad whitespace in manifest
  * Fix for bad decompilation of some apks (Credit: KOJAN)

## 1.4.9 ##
2012.07.28

  * Fix for plurals.xml (Credit: MIUIRussia)
  * Added xhdpi configurations
  * Added uimodes configurations - miui roms
  * Fixed problem escaping chars like ' /

## 1.4.8 ##
2012.07.08

  * Revert greyscale fix due to errors
  * Skip extra com.htc package in some apks.
  * Some fixes from yyj inserted

## 1.4.7 ##
2012.07.05

  * updated to baksmali/smali to public v1.3.3
  * Fix for grayscaled images (Credit: Charles)
  * Adjusted resources/configurations for API13

## 1.4.6 ##
2012.02.14

  * Fixed reading of xlif data to correctly insert formatted="false"
  * Fixed `<item>` being read incorrectly and placed as attr type

## 1.4.5 ##
2012.01.07

  * updated builtin framework to SDK API15
  * updated baksmali/smali to v1.3.3dev

## 1.4.4 ##
2011.12.11

  * updated baksmali/smali to v1.3.3
  * New developer: iBotPeaches

## 1.4.3 ##
2011.12.08

  * updated builtin framework to SDK API14
  * fixed some "Multiple substitutions (...)" errors ([Issue 254](https://code.google.com/p/android-apktool/issues/detail?id=254))

## 1.4.2 ##
2011.12.02

  * added support for API14 (Android 4.0) resources
  * updated smali to v1.3.0
  * added --quiet option
  * fixed decoding error when string ends with '%' ([Issue 169](https://code.google.com/p/android-apktool/issues/detail?id=169))
  * fixed decoding error when `<plurals>` contains a reference ([Issue 234](https://code.google.com/p/android-apktool/issues/detail?id=234))
  * fixed a broken res when decoding `<array>` with positional substitutions ([Issue 222](https://code.google.com/p/android-apktool/issues/detail?id=222))

## 1.4.1 ##
2011.05.15

  * fixed builtin framework. See changelog and migration instructions of v1.4.0 below.

## 1.4.0 ##
2011.05.15

**Major changes**:

  * added Honeycomb support (3.1, API 12). See migration instructions below.
    * support for mipmaps and xlarge, xhdpi resource qualifiers
    * updated builtin framework to 3.1 (API 12) <font color='red'>broken</font>
  * completely rewritten mechanism of enclosing/escaping strings in XML files:
    * fixed legendary [Issue 100](https://code.google.com/p/android-apktool/issues/detail?id=100)
    * fixed a lot of other bugs discovered when writting integration tests
    * string format is simpler and more compact now: '"  "' instead of '\u0020 ', '\"' instead of '\&quot;', etc.
  * fixed incompatibilities between newer aapt and apks built by older one. New aapt is more restrictive, some apps can't be built using it, even if you would have sources. Apktool tries to convert/fix these incompatibilities: it adds formatted="false" for `<string />` tags and enumerates substitutions for plurals.
  * updated smali to v1.2.6
  * added automatic integration tests for resource decoding and building
  * first official release of apktool built using Maven from open source

**Minor changes**

  * sort framework ids before storing them in apktool.yml. aapt command requires you to include frameworks in order.
  * zero-padding of MCC resource qualifier
  * prefer to use raw values when decoding XML attrs. This could make decoded XMLs a little more similar to original ones.
  * close apktool.yml file handler after generating it
  * added error message about missing input file when decoding
  * added more info messages during decoding.
  * do not decode res-references as `<item />`. Now they're decoded as e.g. `<string name="test">@android:string/ok</string>` instead of `<item type="string" name="test">@android:string/ok</item>`.
  * changed encoding of generated XML files from UTF-8 to utf-8 - it's more consistent with Android SDK.
  * add new line at the end of generated XML files.

### Migration to 1.4.0 ###

In order to get full Honeycomb/Gingerbread (3.1, API 12) support you have to:

  * update apktool to v1.4.0
  * update install package to [r04](https://code.google.com/p/android-apktool/source/detail?r=04)-brut1 or update your aapt manually
  * then remove $HOME/apktool/framework/1.apk or install your own framework from Honeycomb/Gingerbread

## 1.3.2 ##
2010.09.03

  * <font color='red'>contains critical bug: <a href='https://code.google.com/p/android-apktool/issues/detail?id=100'>Issue 100</a>.</font>
  * updated smali to v1.2.4
  * added support for API Level 8 resource qualifiers: night, car, etc. ([Issue 65](https://code.google.com/p/android-apktool/issues/detail?id=65))
  * added support for broken file-resources ([Issue 91](https://code.google.com/p/android-apktool/issues/detail?id=91))
  * don't generate sdkVersion ("-v") resource qualifiers if they're "natural" ([Issue 85](https://code.google.com/p/android-apktool/issues/detail?id=85))
  * always compress resources.arsc file ([Issue 67](https://code.google.com/p/android-apktool/issues/detail?id=67))
  * throw warnings instead of exceptions on unknown files inside smali dir ([Issue 77](https://code.google.com/p/android-apktool/issues/detail?id=77))
  * added support for resources using invalid/unknown config flags, e.g. from future APIs or added by manufacturer ([Issue 65](https://code.google.com/p/android-apktool/issues/detail?id=65))
  * added an option to keep broken resources to fix them manually ([Issue 65](https://code.google.com/p/android-apktool/issues/detail?id=65))
  * fixed case-sensitivity problems ([Issue 86](https://code.google.com/p/android-apktool/issues/detail?id=86))
  * fixed an issue when `*`.9.png doesn't have 9patch chunk in it ([Issue 59](https://code.google.com/p/android-apktool/issues/detail?id=59))
  * fixed NPE when there is a file without extension in drawable dir ([Issue 62](https://code.google.com/p/android-apktool/issues/detail?id=62))
  * fixed escaping of chars in XML style tags ([Issue 64](https://code.google.com/p/android-apktool/issues/detail?id=64))
  * fixed an error, when there are missing resources in a type, which does not have default config (http://forum.xda-developers.com/showthread.php?p=7949440#post7949440)
  * try to use original value of XML attribute - instead of parsed one. Fixes an issue when apktool was decoding e.g. "01" as "1" ([Issue 76](https://code.google.com/p/android-apktool/issues/detail?id=76))
  * added more debugging info when omitting unknown config flags ("Config size > 32" message)

## 1.3.1 ##
2010.06.14

  * added decoding of XML tags in res strings ([Issue 15](http://code.google.com/p/android-apktool/issues/detail?id=15))
  * fixed some issues ([Issue 45](http://code.google.com/p/android-apktool/issues/detail?id=45)), ([Issue 46](http://code.google.com/p/android-apktool/issues/detail?id=46)), ([Issue 48](http://code.google.com/p/android-apktool/issues/detail?id=48)), ([Issue 56](http://code.google.com/p/android-apktool/issues/detail?id=56))

## 1.3.0 ##
2010.06.12

  * added 9patch images (`*`.9.png) decoding ([Issue 2](http://code.google.com/p/android-apktool/issues/detail?id=2))
  * fixed support for apks lacking res dir or resources.arsc file ([Issue 44](http://code.google.com/p/android-apktool/issues/detail?id=44), [Issue 50](http://code.google.com/p/android-apktool/issues/detail?id=50))
  * changed default name of built file from out.apk to <original\_name.apk>
  * added possibility to choose location of output apk when building

## 1.2.0 ##
2010.06.03

  * added feature for installing and using custom framework files - pulled from a device. See FrameworkFiles ([Issue 27](http://code.google.com/p/android-apktool/issues/detail?id=27))
  * Froyo support ([Issue 37](http://code.google.com/p/android-apktool/issues/detail?id=37))
  * updated Android framework to 2.2r1
  * removed HTC framework
  * no need to use -s/-r switch, when apk doesn't contain sources/resources
  * added protection against accidental remove of important files when decoding ([Issue 36](http://code.google.com/p/android-apktool/issues/detail?id=36))
  * made outdir argument optional when decoding
  * fix: adding dummy resources if some of them are missing ([Issue 40](http://code.google.com/p/android-apktool/issues/detail?id=40))
  * fix: better recognition of AXML files ([Issue 41](http://code.google.com/p/android-apktool/issues/detail?id=41))

## 1.1.1 ##
2010.04.29

  * much better recognition of register types when debugging ([Issue 24](http://code.google.com/p/android-apktool/issues/detail?id=24))
  * fixed SIGSEGV error, which usually occured after several steps when debugging ([Issue 26](http://code.google.com/p/android-apktool/issues/detail?id=26))

## 1.1.0 ##
2010.04.28

  * added smali debugging! For more info, see: SmaliDebugging
  * added HTC resources ([Issue 17](http://code.google.com/p/android-apktool/issues/detail?id=17))
  * made all framework resources public ([Issue 16](http://code.google.com/p/android-apktool/issues/detail?id=16))
  * proper escaping of whitespaces in resource strings ([Issue 14](http://code.google.com/p/android-apktool/issues/detail?id=14))
  * updated (bak)smali to 1.2.2
  * fixed "Building resources..." freeze bug ([Issue 13](http://code.google.com/p/android-apktool/issues/detail?id=13))

## 1.0.0 ##
2010.04.02

  * it is now pure-Java, so should work on any platform
  * added support for decoding and rebuilding framework-res.apk file
  * added support for many new resources features and apks
  * included automatic workaround for 9-patch images issue
  * added possibility to decode sources or resources only
  * automatic detecting, whether there is a need for rebuilding files
  * added some info messages
  * it is less invasive, cause res ids in built file are identical as in original apk
  * it is much faster
  * fixed a lot of bugs

## 0.9.2 ##
2010.03.13

  * many, many new apps supported. I've tested it on 85 random apps pulled from my device: 0.9.1 gave me 28 failures, 0.9.2 only 2. This does not mean all 83 apps are perfectly fine, but it is quite probably that they are.
  * smali, baksmali and android resources are now builtin, so it is much simplier to install apktool. Still you need aapt in a PATH.
  * much better error reporting
  * added simple usage help
  * new "bs" command

## 0.9.1 ##
2010.03.02

  * [#1](http://code.google.com/p/android-apktool/issues/detail?id=1) fixed
  * fixed support for many apps