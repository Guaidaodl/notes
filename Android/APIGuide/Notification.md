# 通知基础知识

## 笔记来源
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

- Group: 可以把通知分组. 系统可以把通知按组折叠.
  
  Anroid 7.0 以上系统可用.

- Channel: 同一个应用的通知可以再被细分到不同的 Channel 中, 用户可以根据 Channel 来管理通知.
  比如禁止特定 Channel 的通知或在勿扰貌似下允许特定的通知. 总而言之是为了细化通知管理的粒度.

  Android 8.0 及以上的系统可用.

- Importance: 通知的重要性, 共有四个等级: Urgent, Hight, Medium, Low. Android 8.0 
  及以上的系统通知的重要性取决于其所属的 Channel 的重要性. 7.1 及以下的系统由 
  priority 属性决定. 
  
  手机根据不同的重要性选择不同的提示方式. 比如只在通知栏, 要不要显示顶部的通知等. 不过用户可以
  更改提示方式.Channel 和 Importance 两个属性大大增强了用户对通知的管理能力.

## 如何发送通知

- 注册 Notification Channel (API 27+)

  Android 8.0 以后的手机上发送通知需要指定通知所属的 Channel. 需要在程序启动时调用. 创建 Channel
  时要指定 Channel 的 Importance.

  关键的类: `NotificationManager`, `NotificationChannel`

- 创建通知
  
  主要使用 NotificationCompat.Build 类, 设置一些属性.

- 发送通知
  
  使用 NotificationManager 的 notify 方法. 需要指定 notification id.

