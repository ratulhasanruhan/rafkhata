---
title: "Flutter easy onboarding"
seoTitle: "Optimize User Onboarding: 'gone_board' Flutter Package"
seoDescription: "Enhance User Onboarding in Flutter Apps with 'gone_board' by Ratul Hasan Ruhan: A Comprehensive Guide and Tutorial"
datePublished: Fri Mar 22 2024 01:07:21 GMT+0000 (Coordinated Universal Time)
cuid: clu1yopfb000309l9gqfqb7ja
slug: flutter-easy-onboarding
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1711069222175/e2156d2d-a13b-4af5-b99b-49389161f311.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1711069375843/a6b94b4c-ce73-4888-a0de-8498dc39176e.png
tags: flutter, flutter-packages

---

**Why need an onboarding screen in the app?**

Onboarding screens in apps introduce features, familiarize users, set expectations, promote engagement, personalize experiences, build trust, and reduce churn.

---

![](https://media.licdn.com/dms/image/D5612AQFU8y0gRU4BVw/article-inline_image-shrink_1000_1488/0/1711068287945?e=1716422400&v=beta&t=ONIFgRdWfGkqWqATAoce-uk5Q9EA6BWx3BxyqlPPW_0 align="left")

gone\_board

%[https://pub.dev/packages/gone_board] 

---

Easily add On-Boarding with some lines of code:-

Add this package:

```yaml
dependencies:
  gone_board: ^1.0.5
```

And here is the screen-

```dart
Scaffold(
        body: GoneBoard(
            pageController: pageController,
            onFinishedPage: DemoHome(),
            items: [
              GonePage(
                image: 'assets/1.png',
                text: 'Welcome to GoneBoard',
                color: Colors.blue,
                context: context,
              ),
              GonePage(
                image: 'assets/2.png',
                text: 'GoneBoard is a Flutter package',
                color: Colors.red,
                context: context,
              ),
              GonePage(
                image: 'assets/3.png',
                text: 'For simplify the task.',
                color: Colors.green,
                context: context,
              ),
            ]),
      ),
    );
```

And that's all...