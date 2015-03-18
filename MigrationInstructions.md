# Introduction #

Upgrades between Apktool versions that include an update to the internal framework, means that the Android framework has updated and new frameworks are needed.


# Details #

# v1.5.x -> v2.0.0 #
  * **Java JRE 1.7 is required!**
  * Update apktool to v2.0.0
  * aapt is now included inside the apktool binary. Its not required to maintain your own aapt install under $PATH. (However, features like `-a / --aapt` are still used and can override the internal aapt).
  * The addition of aapt replaces the need for separate aapt download packages. Helper Scripts may be found [here](https://github.com/iBotPeaches/Apktool/tree/master/scripts).
  * Remove framework `$HOME/apktool/framework/1.apk` or manually update via (FrameworkFiles)
  * Eagle eye users will notice resources are now decoded before sources now. This is because we need to know the API version via the manifest for decoding the sources.
**Parameter Changes**
  * Smali/baksmali 2.0 are included. This is a big change from 1.4.2. Please read the smali updates [here](https://code.google.com/p/smali/wiki/SmaliBaksmali20) for more information.
  * `-o / --output` is now used for the output of apk/directory.
  * `-t / --tag` is required for tagging framework files
  * `-advance / --advanced` will launch advance parameters and information on the usage output.
  * `-m / --match-original` is a new feature for apk analysis. This retains the apk is nearly original format, but will make rebuild more than likely not work due to ignoring the changes that newer aapt requires.
  * After `[d]ecode`, there will be new folders (original / unknown) in the decoded apk folder.
    * `original/` = `META-INF folder` / `AndroidManifest.xml`, which are needed to retain the signature of APKs to prevent resigning. Used with `-c / --copy-original` on `[b]uild`.
    * `unknown/` = Files / folders that are not part of the standard AOSP build procedure. These files will be injected back into the rebuilt APK.
  * `apktool.yml` collects more information than before
    * `SdkInfo` = Used to re-populate the sdk information in `AndroidManifest.xml` since aapt requires it to be passed at runtime.
    * `packageInfo` = Used to help support Android 4.2 due to renamed manifest packages. Automatically detects difference between manifest and resources and performs automatic `--rename-manifest-package` on `[b]uild`.
    * `versionInfo` = Used to re-populate the version information in the `AndroidManifest.xml` since aapt requires it to be passed at runtime.
    * `compressionType` = Used to determine the compression that `resources.arsc` had on the original apk to duplicate on `[b]uild`.
    * `unknownFiles` = Used to record the name/location/compression type of non-standard files in Apk.

**Examples of new usage**

| **Apktool 1.5.x** | **Apktool 2.0.x** |
|:------------------|:------------------|
| `apktool if framework-res.apk tag` | `apktool if framework-res.apk -t tag` |
| `apktool d framework-res.apk output` | `apktool d framework.res.apk -o output` |
| `apktool b output new.apk` | `apktool b output -o new.apk` |


# v1.4.x -> v1.5.1 #
  * Update apktool to v1.5.1
  * Update aapt manually or use package `r05-ibot` via [Downloads](http://code.google.com/p/android-apktool/downloads/list)
  * Remove framework `$HOME/apktool/framework/1.apk` or manually update via (FrameworkFiles)