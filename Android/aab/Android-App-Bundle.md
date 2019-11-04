# Android App Bundle

## 相关资料:
1. [App Bundle](https://developer.android.com/platform/technology/app-bundle)
2. [Dynamic Delivery](https://item.taobao.com/item.htm?id=590221409485)
3. [Your First Dynamic App](https://codelabs.developers.google.com/codelabs/your-first-dynamic-app/index.html#0)

## split APK 机制
spilt APK 机制是 dynamic delivery 的基础组件. 该机制可以把同一个应该拆成不同的 APK, 分次安装.

### APK 的类型
1. Base APK 
   基本的 APK, 包含所有 APK 都可以访问的代码和资源.
2. Configuration APK
   主要包含了特定机型(架构, 语言, 屏幕密度)的 native 库和资源.
3. Dynamic feature APK
   包含了特定模块的代码和资源.

![典型结构](../asset/apk_splits_tree.png)
#### 4.4(19) 以下的兼容.
因为 4.4 以下的系统不支持 split APK 机制, 不能使用动态分发. 所以 Google Play 提供了兼容的方案
multi-APK. Google Play 会根据设备的架构和屏幕密度等配置声生成一个只包含必要资源的 APK.

## 动态模块的下发方式.
对于 AAB 来说, 通常一个动态模块对应一个 Dynamic Feature APK. 对于不太的功能模块可以选择不同的下载策略.
- At-install delivery
  不动态下发, 跟随主应用下发. 但是可以卸载.
- On demand delivery
  按需下发. 只有在需求的时候才下载.
- Conditional delivery
  可以根据设备属性(local, api, 硬件特性)来选择要不要跟随主应用下发.
- Instant delivery
  即时应用使用.

## 创建一个 Android App Bundle
1. 创建普通的应用.
2. 在 build.gradle 的 android {} 模块里添加以下的配置
   ``` groovy
   bundle {
       language {
           enableSplit = true
       }
       density {
           enableSplit = true
       }
       abi {
           enableSplit = true
       }
   }
   ```
3. 通过 Android Studio 创建一个动态模块.
   关键点:
   * 模块的 plugin 为 'com.android.dynamic-feature'.
   * 在主模块的 android {} 里 dynamicFeatures 的值.
     ``` grovvy
     dynamicFeature = [":payments"]
     ```
   * 设置一个下发策略



# 疑问?
1. 如果我已经下载了一个 onDemand 的模块, 那我更新应用时是否也会更新这个模块
2. 动态模块中 implementation 和 api 依赖有什么区别