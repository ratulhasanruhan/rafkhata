---
title: "Flutter AAPT: error: resource android:attr/lStar not found. Solutions"
datePublished: Wed Oct 30 2024 21:21:16 GMT+0000 (Coordinated Universal Time)
cuid: cm2wdsx2k00020al6grdg0hvg
slug: flutter-aapt-error-resource
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1730323218657/72e6ccc5-1b22-4957-97a4-fc8c5c93d0fb.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1730323270028/5470d9ba-9ff8-4bbe-929a-e1c2e149f71a.png
tags: flutter, package

---

**Cause:** Some packages use compileSdkVersion:30. In this SDK version, there are no attribute names lStar.

**Solutions:**

![](https://miro.medium.com/v2/resize:fit:700/1*LDUpIFw0y-eWEU8jFZaF6Q.png align="left")

You get a package name in the error message where the attribute lStar is not found. Find the package name. In my case, that was flutter\_sound.

Go to external libraries then find the package.

![](https://miro.medium.com/v2/resize:fit:560/1*Tu5isUgLuJSqm2ICgK3CNg.png align="left")

Then go to build.gradle. And change to compileSdkVersion to latest.

![](https://miro.medium.com/v2/resize:fit:700/1*wPWPzHspzQm6wHsC42IJ3Q.png align="left")

And Done…….