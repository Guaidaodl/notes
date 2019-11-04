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