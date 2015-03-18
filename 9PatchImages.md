There are docs about this topic on Android main site: http://d.android.com/guide/topics/graphics/2d-graphics.html#nine-patch , http://d.android.com/guide/developing/tools/draw9patch.html (read them first, if you didn't), but these docs are for developers of apps only, not for people, who works with 3rd party apps. There you can find what 9patch images are and how to create them, but you won't find any technical info on how this actually works. And 9patch thing is quite tricky and confusing, many people are WTFing, why their images got screwed up after simple modification, etc. I decided to explain this here.

Most important thing, totally ignored by official docs: 9patch images have two forms: source and compiled one. They differ in the way, how 9patch data is written in them:

  * source - you probably know these ones, you can find them in sources of an app. 9patch data is written in the form of black borders around the image, so you can easily see and modify it using any image editor.
  * compiled - mysterious form found in apk files. There are no borders, 9patch data is written in special binary chunk named as: npTc. You can't see or modify it easily, but it's much easier for Android OS to use it, so it's faster.

There are some problems caused by above:

  * You can't move 9patch images between both types without converting them. If you try to unpack `*`.9.png file from apk and use it in sources of other app, then you will get error during build, cause `*`.9.png without borders are invalid at build time. And vice versa: if you replace `*`.9.png file in apk by png with borders, then this image won't be recognized as 9patch image - it will look weird and borders will be visible at runtime.
  * 9patch binary chunk isn't recognized by image processing tools, so if you try to do anything with compiled 9patch image, then it's possible you will break its npTc chunk and image will look weird on a device. You can't use optipng on compiled 9patch image, also many image editors will break it even if you just open & save file without doing any changes.

There is only one good solution to these problems: make possible to easily convert between both types of 9patch images. Encoder (source -> compiled) is built into aapt tool and it's automatically used during app build. Decoder is built into apktool since v1.3.0. I believe there are no other tools to convert 9patch images.

So if you want to modify `*`.9.png files in 3rd party app, don't do that directly - most probably you will run into problems. Use apktool to decode this app, then modify images and build apk back. If you want to use `*`.9.png images from one 3rd apk in another, but don't modify them, you could try to just copy these files without converting, cause both apps are in compiled form. But if you have decoded one of these apps using apktool, then you have to decode second one as well.

Also I know many people don't want to decode and build whole apk, but selected files only. There is an issue for that: [Issue 92](https://code.google.com/p/android-apktool/issues/detail?id=92) .