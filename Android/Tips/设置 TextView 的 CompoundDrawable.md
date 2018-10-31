### 问题
直接调用 `TextView#setCompoundDrawables` 没有效果

### 原因

从文档中可知如果在调用 `setCompoundDrawables` 方法之前需要调用 `Drawable#setBounds` 才能生效.

### 解决方案

1. 先调用 `Drawable#setBounds`
2. 调用 `TextView#setCompoundDrawablesWithIntrinsicBounds`