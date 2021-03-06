# 模拟位置

因为要进行国际化的测试, 所以需要模拟一些国外的位置. 进行了一些调研, 可行的方案主要有三种:

1. 采用模拟器来模拟位置
2. 利用一些第三方的应用来模拟位置
3. 利用开发者选项来模拟应用

## 利用模拟器模拟位置

Google 官方自带的模拟器可以通过直接输入经纬度的方法模拟位置.

具体位置的经纬度可以通过 Google Map 获得.

## 利用第三方的应用来模拟位置

对于己经 Root 的手机可以通过一些第三方的应用或者 Xposed 模块来修改位置. 

看起来这个是最方便的方法, 不过这些应用可能都不太稳定. 一部分的应用需要付费.

## 利用开发者选项来模拟应用

Android 的开发者选项中有模拟位置的选项. 不过这个需要应用自己提供一个设置位置的页面. 需要一定的开发量.

具体使用方法可以参考[这篇文章](https://blog.csdn.net/ucxiii/article/details/52293025)

