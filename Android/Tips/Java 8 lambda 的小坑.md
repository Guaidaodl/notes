今天在写代码的时候发现了一个 Java 8 里面的 lambda 的小坑. 在一个自定义的 EditText 里写了以下的代码:

```java
getViewTreeObserver().addOnPreDrawListener(() -> {
    doSomething();    
    getViewTreeObserver().removeOnPreDrawListener(this);
    return true;
});
```

然后就发现 doSomething() 被不停的调用, remove 没有生效.

原因在于 lambda 是不能用 this 引用的, 所以这里的 this 引用的其实是我自定义的 EditText. 而 EditText 
又刚好继承了 ViewTreeObserver.OnPreDrawListener. 所以这一段代码不会报错, 但是效果跟预期的不符.

所以 lambda 和匿名内部类不是完全等效的, 如果需要用 this 引用自己的时候一定要使用内部类. 

另外看了一下 Android Studio 的 lint. 如果匿名内部里引用了 this 的话是不会有可以转成 lambda 的警告, 在
修改的时候可以放心使用自动转换的功能.

