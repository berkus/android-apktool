# Introduction #

Confused about some of the commands Apktool can do?


## Utility Options ##

**`-version, --version`**
> Outputs current version. (Ex: 1.5.2)

**`-v, --verbose`**
> Verbose output. Needed before all other commands.

**`-q, --quiet`**
> Quiets output. Needed before all other commands.

**`-advance, --advanced`**
> Prints advance options

## Decompile Options ##

**`--api <API>`**
> The numeric api-level of the smali files to generate (eg 14 for ICS).

**`-b, --no-debug-info`**
> Prevents baksmali from writing out debug info (.local, .param, .line, etc). Preferred to use if you are comparing smali from the same APK of different versions. The line numbers and debug will change among versions, which can make DIFF reports a pain.

**`-d, --debug`**
> Decodes in Debug Mode. Check SmaliDebugging

**`--debug-line-prefix <prefix>`**
> Smali line prefix when decoding in debug mode. Default "a=0;//"

**`-f, --force`**
> Force delete destination directory. Use if trying to decompile to a folder that already exists.

**`--keep-broken-res`**
> If there is an error like "Invalid Config Flags Detected. Dropping Resources...". This means that APK has a different structure then Apktool can handle. This might be a newer Android version or a random APK that doesn't match standards. Running this will allow the decode, but then you have to manually fix the folders with -ERR in them.

**`-m, --match-original`**
> Keeps files closest as possible to original. Prevents rebuilding, used for analysis"

**`-o, --output <dir>`**
> The name of the folder that gets written.

**`-p, --frame-path <dir>`**
> The location where framework files are loaded from / placed.

**`-r, --no-res`**
> This will prevent the decompile of resources. This keeps the resources.arsc intact without any decompile. If only editing Java (smali) then this is the recommend for faster decompile & rebuild.

**`-s, --no src`**
> This will prevent the decompile of the java source. This keeps the APK classes.dex file and simply moves it during re-compile. If your only editing the resources. This is recommended for faster decompile & rebuild.

**`-t, --frame-tag <tag>`**
> Uses framework files tagged by `<tag>`.

## How to Decompile? ##

Prior to Decompile, you must have frameworks installed. Please read this wiki: FrameworkFiles for more information. Once complete run

```
apktool d name_of_apk.apk
```

With any configurations noted above.

## Recompile Options ##

**`-a, --aapt <file>`**
> Loads aapt from the specified file location, instead of relying on path. Falls back to PATH loading, if no file found.

**`-c, --copy-original`**
> Copies original `AndroidManifest.xml` and `META-INF` folder into built apk.

**`-d, --debug`**
> Builds in Debug Mode, see SmaliDebugging

**-f, --force-all**
> This overwrites an existing file during rebuild.

**`-o, --output <dir>`**
> The name of the folder that gets written.

**`-p, --frame-path <dir>`**
> The location where framework files are loaded from / placed.

## How to Recompile? ##

Prior to Recompile, you must have a decompiled application installed. Once complete run

```
apktool b folder_of_decoded_apk
```

With any configurations noted above.