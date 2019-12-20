# 通知基础知识

## 笔记来源
- Notification
  - [Overview](https://developer.android.com/guide/topics/ui/notifiers/notifications)
  - [Create Notification](https://developer.android.com/training/notify-user/build-notification)

## 通知的结构

![通知的结构](https://wx4.sinaimg.cn/large/6abde139ly1fv9ez3r940j20ny06zgmr.jpg)

1. Small Icon: 24* 24 dp, 是唯一一个必须要提供的部件.
2. App Name (由系统提供)
3. TimeStamp (可隐藏)
4. Large Icon
5. Title. API: `setContentTitle()`
6. Content. API: `setContentText()`

## 关键的概念:

- Group: 可以把通知分组. 系统可以把通知按组折叠.
  
  Android 7.0 以上系统可用.

- Channel: 同一个应用的通知可以再被细分到不同的 Channel 中, 用户可以根据 Channel 来管理通知.
  比如禁止特定 Channel 的通知或在勿扰貌似下允许特定的通知. 总而言之是为了细化通知管理的粒度.

  Android 8.0 及以上的系统可用.

- Importance: 通知的重要性, 共有四个等级: Urgent, Hight, Medium, Low. Android 8.0 
  及以上的系统通知的重要性取决于其所属的 Channel 的重要性. 7.1 及以下的系统由 
  priority 属性决定. 
  
  手机根据不同的重要性选择不同的提示方式. 比如只在通知栏, 要不要显示顶部的通知等. 不过用户可以
  更改提示方式.Channel 和 Importance 两个属性大大增强了用户对通知的管理能力.

## 如何使用通知相关的 API

### 发送简单通知
- 注册 Notification Channel (API 27+)

  Android 8.0 以后的手机上发送通知需要指定通知所属的 Channel. 需要在程序启动时调用. 创建 Channel
  时要指定 Channel 的 Importance.

  关键的类: `NotificationManager`, `NotificationChannel`

- 创建通知
  
  主要使用 `NotificationCompat.Build` 类, 设置一些属性.

- 发送通知
  
  使用 `NotificationManager` 的 notify 方法. 需要指定 notification id.

比如以下的代码:
```kotlin
val nt = NotificationCompat.Builder(this, CHANNEL_ID)
                .setSmallIcon(R.drawable.ic_nt_small)
                .setContentTitle("Simple Notification")
                .setContentTitle("This is a simple notification, the id is ${id.get()}, " +
                        "the channel id is ${CHANNEL_ID}")
                .build()
val m = NotificationManagerCompat.from(this)
m.notify(id.getAndIncrement(), nt)
```

### 处理点击通知的事件

Android 可以利用 PendingIntent 机制来处理通知的点击事件. 在创建好 PendingIntent 后使用 Builder
的 `setContentIntent` 方法即可.

### 点击后隐藏.
`builder.setAutoCancel(true)`

### 添加一个 Action
可以通过 `builder.addAction()` 方法添加一个 Action. 需要指定图标, 标签和一个 PendingIntent

### 添加直接回复
1. 使用 `RemoteInput.Builder` 来创建一个 `RemoteInput`.
2. 创建一个 `PendingIntent` 了进行回复.
3. 创建一个 `NotificationCompat.Action`, 并通过 `setRemoteInput` 来设置 Action 的 `RemoteInput`
4. 将 Action 和通知绑定.
5. **获取用户回复的信息**. 调用`RemoteInput.getResultFromIntent()`可以获得.
6. 使用 `NotificationCompat.notify()` 更新对应的通知.

想到一个小点子, 可以用该 API 来做一个通知栏翻译的小插件.

### MessagingStyle
对于聊天型的通知可以通过 MessagingStyle 来显示多条聊天信息. 通过 `NotificationCompat.MessageStyle`
可以构建一个聊天的信息流. 

Android P(API 28, 9.0) 后增加了 Person 类, 可以更方便地管理通知.