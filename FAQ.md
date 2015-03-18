# FAQ #


---


## What about "-j" switch from your video on YouTube? ##

[Issue 88](https://code.google.com/p/android-apktool/issues/detail?id=88) - In other words. It doesn't exist.


---


## Is it possible to run apktool on a device? ##

Not yet. Let's talk about it: [Running apktool on a device @ Google Groups](http://groups.google.com/group/apktool/browse_thread/thread/952c51ed1b2ff0f2). If you don't have a Google account (and you are using Android device? I don't believe you ;-P), then you could at least read that thread and write to me on XDA or somewhere.


---


## Where can I download sources of apktool? ##

[Source (Googlecode)](https://code.google.com/p/android-apktool/source/checkout), [Source (Github)](https://github.com/iBotPeaches/Apktool)


---


## Resulting apk file is much smaller than original! Is there something missing? ##

First: compression of resources.arsc file. Sometimes this file is compressed in original apk, sometimes not and apktool always compress it. Second: lack of META-INF dir. Apktool builds unsigned apks, so they lack signatures stored in this dir. Third: apktool uses newest Android SDK, so it could optimize files better, especially if original app is old. So: unpack both original and resulting apk, remove META-INF from original and then compare sizes. If they're still much different, then you could report on XDA or somewhere.


---


## There is no META-INF dir in resulting apk. Is this ok? ##

Yes. META-INF contains apk signatures mostly and after modifying apk in no longer signed, so there are no signatures in it. You have to sign resulting apk and then META-INF dir will be created.


---


## What do you call "magic apks"? ##

Sometimes there are some apks which (for my current knowledge) are invalid, broken, theoretically they shouldn't exist. There may be many reasons of their existence: my lack of understanding of Android resources; some non-public, maybe future SDK tools or custom modifications of these; manual hacking of binaries, etc. Usually I can't do anything about it, but you could at least try to replace broken parts by something valid. Actually it's quite likely that they aren't even used, because if they would, then application would crash.


---


## Could I integrate apktool into my own tool? Could I modify apktool sources? Do I have to credit you then? ##

Actually Apache License, which apktool uses, answers all these questions: yes, you could redistribute and/or modify apktool without my permission to do that. If you have credits section in your tool/app, then it would be nice to add me and others (JesusFreke, etc.) there, but I don't require that.


---


## My recompiled apk Force Closes (FCs). What gives? ##

There is a lot to understand when decompiling APKs. First: Is it a system apk? If so then you are going to have to be careful when putting it back on your device. Apktool rebuilds the apk without a signature. Pushing that new apk to your phone will result in an FC. You have 3 options at this point. 1) Re-inject the resources from the modified rebuilt apk (resources.arsc, classes.dex & any /res file you changed) back into the original apk using 7zip or some packer. 2) Find the keys that were used to sign those system apks and resign that modified apk with the same signature. 3) Sign the apk with some debug key and build an entire new ROM with that modified apk.

If the app is a regular data (non-system) APK. Your best bet is still to re-inject the resources (resources.arsc, classes.dex & and /res file changed) back into the original apk (to retain the signature). This will result in the lowest amount of modified app (except for what you changed).


---


## I get "Invalid Directory Errors". What happened? ##

This is simple. Your aapt is out of date. Please download a new aapt which is provided via Downloads. If you continue to get this error, even after updating aapt, then you didn't update it. So try again. Unfortunately, aapt has been at v0.2 for the past 3 years. It seems they don't increment the version. So checking `aapt v` doesn't help.