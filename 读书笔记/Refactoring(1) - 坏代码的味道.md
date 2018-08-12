# 坏代码的味道

## Deplicated 重复的代码.

DRY 原则。尽量不要用重复的代码。

相关的重构方法：
- Extract Method
- Pull up Field
- Form Template Method
- Substitute Algorithm
- Extract Class

## Long Method

单个方法太长。 太长的方法会变得特别难理解。我的个人标准是最好是一个屏幕就可以显示整儿方法， 方法的嵌套层次最高不要超过 3 个。

相关重构方法：
- Extract Method
- Replace Temp with Query
- Instroduce Parameter Object
- Preserve Whole Object
- Replace Method with Method Object
- Decompose Conditional
