---
title: "A common error for Flutter build apk"
seoTitle: "A common error for Flutter build apk"
seoDescription: "Flutter JDK error"
datePublished: Sun Oct 20 2024 20:43:11 GMT+0000 (Coordinated Universal Time)
cuid: cm2i21f3i000008mf7pm9elfk
slug: a-common-error-for-flutter-build-apk
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1730323126540/611b0396-e639-4e99-98c3-d6dc84ceac05.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1730323078253/68683c1f-a3ee-4a4f-a459-534eb5d90590.png
tags: flutter, jdk

---

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1730323152073/292e98a6-4420-46b5-9ae0-7b4cb0c6d8e2.avif align="center")

#### Causes:

Many plugins, like share\_plus, connectivity\_plus, etc., now need JDK 17. You get this type of error if you don't have JDK 17.

#### Solutions:

[Download JDK 17](https://download.oracle.com/java/17/archive/jdk-17.0.12_windows-x64_bin.exe). Put any directory. (You can also add the path to the environment variable.)

Add the JDK path to your project [gradle.properties](http://gradle.properties). Like this:

![image](https://res.cloudinary.com/daily-now/image/upload/s--pFKQOGsa--/f_auto/v1729456706/ugc/content_74d137c1-f0bf-46ab-acee-6b217a6f0529 align="left")

[`org.gradle.java`](http://org.gradle.java)`.home=C://Program Files//Java//jdk-17`

That's all.