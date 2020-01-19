# AAB 常见问题

## 如何设置动态模块的下发方式
可以通过设置动态的模块的 AndroidManifest.xml 文件来设置
``` xml
<dist:module>
  <dist:delivery>
    <dist:on-demand/>
  </dist:delivery>
</dist:module>
```
除了 on-demand 外, 还有 install-time

## 动态模块中依赖会打包在哪里? 应该用哪一种依赖?
根据测试结果来看, 同一个依赖不会再 base 和 dynamic module 中同时存在.


## 如果我已经下载了一个 onDemand 的模块, 那我更新应用时是否也会更新这个模块
会