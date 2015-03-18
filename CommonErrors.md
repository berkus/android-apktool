# Basic Errors / Fixes #

## Error retrieving parent for item: No resource found that matches the given name `TextAppearance` ##

This error usually has to do with the increasing restrictive-ness of AAPT and the `styles.xml` file, this problem is due to the fact that implicit parenting now requires a parent. `SDK Tools r6` would let this slide, but newer AAPT does not. First lets learn a little about implicit parenting.

If you have this style.

```
<style name="TextAppearance.DialogWindowTitle">
        <item name="android:textSize">22.0sp</item>
        <item name="android:textColor">@color/holo_blue_light</item>
    </style>
```

(You might be unaware to know that `.DialogWindowTitle` isn't public). So extending a non public resource won't work on all devices. This is because that resource is assigned an integer, and only public resources in the framework are guaranteed not to change, thus this style will reference a parent that **might / might not** exist on a device. This is a problem.

Your first thought may be to revert to a older AAPT or perform a hacky `@*android:style fix`. Let me quote an AOSP Developer:

> "Reverting to an older aapt that lets you do this or using  `@*android:style/xxxx` is basically similar to using a private Java API.

> Our stance on this has been clear since 1.0: Don't do it. It may be   convenient for a bit, but it'll break on devices, all of them in this   case too, and it's not good for anyone."

So to fix this. We need to find the parent and insert it into the file. To fix the above example, we simply add.

```
<style name="TextAppearance"></style>
```

If you have a lot of errors. I would just import the entire `styles.xml` into your local application's `styles.xml`. It may be overkill, but it'll solve your problems :)