# Profile Layout

## 参考文章:
- [Understanding the performance benefits of ConstraintLayout](https://android-developers.googleblog.com/2017/08/understanding-performance-benefits-of.html)

- [Debug Your layout with Layout Inspector](https://developer.android.com/studio/debug/layout-inspector)

- [systrace](https://developer.android.com/studio/command-line/systrace)

## 性能测试工具

### Layout Inspector
Hierarchy Viewer 已经被从 SDK 中移除. 现在 Google 推荐使用 [Layout Inspector](https://developer.android.com/studio/debug/layout-inspector)
可以更方便地查看View 的层次结构.

### systrace
用于进行性能分析. 需要 Python 2. 位于 SDK/platform-tools/systrace 文件下.

可以通过运行命令:
``` bash
python ./systrace.py view -t 10
```
就可以检测绘制的情况. 可以分析每一帧的时间是否正常.

#### systrace 自定义Tag
systrace 默认只会分析系统调用, 如果你想要分析自己代码的性能. 需要使用 Trace 接口.

Trace 接口的使用方法如下:
``` Java
Trace.beginSection("Label")
// other code
Trace.endSection()
```

同时在运行 systrace 需要通过 --app 或者 -a 来指定进程名.

## 其他工具

systrace 主要是分析系统调用的时间. 如果想要具体的数据可以使用 Android Studio 自带的工具获.






