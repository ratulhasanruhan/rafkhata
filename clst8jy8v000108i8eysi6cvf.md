---
title: "Automated support chat with Firebase and Flutter"
datePublished: Mon Feb 19 2024 17:53:58 GMT+0000 (Coordinated Universal Time)
cuid: clst8jy8v000108i8eysi6cvf
slug: automated-support-chat-with-firebase-and-flutter
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1708365080208/7de89a85-335f-46bf-88d6-4259696bea0d.png
tags: firebase, flutter, firestore, support-chat

---

1. Connect your app to Firebase. Here we use Cloud Firestore for the database.
    
2. Our project requires these packages:-
    

```dart
firebase_core: ^2.14.0
cloud_firestore: ^4.0.4
flutter_chat_bubble: ^2.0.2
```

3\. Make a stateful widget on your chat page dart file. The basic setup is finished.

4\. Make a data model for chat data. Here are 2 variables. The first string chat is for the message. The second one bool isUser for who the sender is: user or Server.

```dart
class LearnChatModel {
  String chat;
  bool isUser;

LearnChatModel({
    required this.chat,
    required this.isUser,
  });
}
```

Now the main part is our chat screen.

![](https://miro.medium.com/v2/resize:fit:700/1*pYXm7vGdG6WXU0y3KXebQQ.png align="left")

5\. Inside the scaffold design your appBar. I Design like this

```dart
AppBar(
        backgroundColor: Colors.red,
        title: const Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Text(
              "Support",
              style: TextStyle(
                color: Colors.white,
                fontSize: 20,
              ),
            ),
            Text(
              "Get 24/7 support from our team",
              style: TextStyle(
                color: Colors.white,
                fontSize: 12,
              ),
            ),
          ],
        ),
        leadingWidth: 72.w,
        leading: Row(
          children: [
            IconButton(
              onPressed: () {
                Navigator.pop(context);
              },
              icon: Icon(
                Icons.arrow_back,
                color: Colors.white,
              ),
            ),
            CircleAvatar(
              radius: 15,
              backgroundColor: Colors.white,
              backgroundImage: NetworkImage(
                  "https://lh3.googleusercontent.com/CmH_wma2nqnYeVYoGoyD_O0sp-ySSH5uoczhgORsSwMYxw60_hDdyujFyydgZasasw",
              ),
            )
          ],
        ),
      )
```

6\. Add some variables. **scrollController** for scrolling to last when the message is sent. **messageList** is a chat model list. Here we store all our messages. **isLoaded** for CircularProgressIndicator when data is loading from the cloud.

```dart
final ScrollController scrollController = ScrollController();
TextEditingController writeController = TextEditingController();
List<LearnChatModel> messageList = [];

bool isLoaded = false;
```

7\. Add the message typing section in the bottom bar. That floats with keyboard appearance. Must use **Padding media query viewInsets.**

Send button function: First, is true our loading for loading UI.

Second, add user message to the list.

Third, check whether the question exists or not. If exists go to the fourth neither add the sorry message nor else to the **Same** messageList.

Fourth, check which doc contains this question. And add the answer to the messageList.

Fifth, loading false, textEditingController clear and Scroll to the last point.

```dart
bottomNavigationBar: Padding(
        padding: MediaQuery.of(context).viewInsets,
        child: Container(
          color: Colors.white,
          padding: EdgeInsets.symmetric(
            horizontal: 10,
            vertical: 5,
          ),
          child: TextField(
            controller: writeController,
            decoration: InputDecoration(
              hintText: "Ask a question...",
              border: OutlineInputBorder(
                borderSide: BorderSide(
                  color: Colors.red,
                  width: 2,
                ),
                borderRadius: BorderRadius.circular(20),
              ),
              enabledBorder: OutlineInputBorder(
                borderSide: BorderSide(
                  color: Colors.red,
                  width: 2,
                ),
                borderRadius: BorderRadius.circular(20),
              ),
              focusedBorder: OutlineInputBorder(
                borderSide: BorderSide(
                  color: Colors.red,
                  width: 2,
                ),
                borderRadius: BorderRadius.circular(20),
              ),
              suffixIcon: IconButton(
                onPressed: () async{
                  setState(() {
                    isLoaded = true;
                  });
                  messageList.add(
                    LearnChatModel(
                      chat: writeController.text.trim(),
                      isUser: true,
                    ),
                  );

               await FirebaseFirestore.instance.collection('english').get().then((value) {
                    if(value.docs.where((element) => element['q'] == writeController.text.trim()).toList().isEmpty){
                      messageList.add(
                        LearnChatModel(
                          chat: "Sorry, Your grammar is not correct. Please try again.",
                          isUser: false,
                        ),
                      );
                    }
                    value.docs.where((element) => element['q'] == writeController.text.trim()).forEach((element) {
                      messageList.add(
                        LearnChatModel(
                          chat: element['a'],
                          isUser: false,
                        ),
                      );
                    });
                  });
                  setState(() {
                    isLoaded = false;
                  });
                  writeController.clear();
                  scrollController.animateTo(
                    scrollController.position.maxScrollExtent + 100,
                    duration: const Duration(milliseconds: 300),
                    curve: Curves.easeOut,
                  );
                },
                icon: isLoaded ? CircularProgressIndicator(
                  backgroundColor: Colors.red.withOpacity(0.6),
                ) :
                Icon(
                  Icons.send,
                  color: Colors.red,
                ),
              ),
            ),
          ),
        ),
      ),
```

8\. Inside body — Message list view

If messageList has no data it shows no data or Start chat message.

Either show all messages inside a Listview.builder . With the ternary operator just check the message from the user or server. And change all the Colors and others. The ChatBubble has a feature called BubbleType it’s determines the message notch alignment.

```dart
body: messageList.isEmpty
      ? Center(
        child: Container(
          child: Column(
            crossAxisAlignment: CrossAxisAlignment.center,
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              Icon(
                Icons.chat_bubble_outline_rounded,
                size: 100,
                color: Colors.grey,
              ),
              Text(
                "Start Chatting",
                style: TextStyle(
                  color: Colors.grey,
                  fontSize: 24,
                ),
              ),
            ],
          ),
        ),
      )
      : ListView.builder(
        shrinkWrap: true,
        controller: scrollController,
        padding: EdgeInsets.symmetric(
          horizontal: 10,
          vertical: 10,
        ),
        itemCount: messageList.length,
        itemBuilder: (context, index) {
          return ChatBubble(
            clipper: messageList[index].isUser ? ChatBubbleClipper5(type: BubbleType.sendBubble) : ChatBubbleClipper5(type: BubbleType.receiverBubble),
            alignment: messageList[index].isUser ? Alignment.topRight : Alignment.topLeft,
            margin: EdgeInsets.only(
              bottom: 10,
            ),
            backGroundColor: messageList[index].isUser ? Colors.red : Colors.grey[200],
            child: Container(
              constraints: BoxConstraints(
                maxWidth: MediaQuery.of(context).size.width * 0.7,
              ),
              child: Text(
                messageList[index].chat,
                style: TextStyle(
                  color: messageList[index].isUser ? Colors.white : Colors.black,
                ),
              ),
            ),
          );
        },
      ),
```

# **Thank you!**