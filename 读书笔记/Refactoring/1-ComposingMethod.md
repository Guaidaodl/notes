# Composing methods. 重组函数

## Extract Method (提炼函数) <p id="1-1"></p>

将一部分代码提炼成一个函数.

### 作用:
- 缩短函数长度. 让函数更容易理解.
- 将代码提炼成一个函数, 可以让代码的目的和作用更清晰.

### 重构的难点:
- 处理临时变量.

### 相关联的方法:

- [Replace Temp with Query](#1-4) 用户减少临时变量.

- [Split Temporary Variable](#1-6) 让临时变量更容易被取代.

- [Replace Method with Method Object](#1-8) 临时变量太过复杂无法提炼时可以采用.

## Inline Method (内联函数) <p id="1-2"></p>

去到方法, 直接调用. 如果代码本身足够清晰与简单, 那就不要特地使用一个函数.因为函数调用是
一种简介的过程, 会增加理解的负担.

还有一种使用方式是觉得方法的结构比较糟糕, 可以先 inline 再重新 extract.


## Inline Temp (内联临时变量) <p id="1-3"></p> 
去到临时变量, 直接使用表达式.

### 作用：
- 辅助其他的重构方式,比如 Replace Temp With Query 和
Extract Method. 

### 相关联的方法:
- [Replace Temp with Query](#1-4)
- [Extract Method](#1-1)


## Replace Temp with Query (以查询取代临时变量) <p id="1-4"></p>
临时变量通常是为了保存一个表达式的值. 可以尝试将此表达式放入一个方法中, 对临时变量的访问
就可以变成对方法的调用了.

### 适用范围:
临时变量只被赋值一次且表达式没有副作用.

### 作用
- 减少临时变量的数量. 临时变量只能在方法调用, 可能导致方法过长. 而方法则可以在各种地方调
用, 有利于构建清晰的代码结构.
- 辅助 Extract Method 方法.

### 相关联的方法:
- [Split Temporaty Variable](#1-6) 解决临时变量被引用多次的问题
- [Separate Query from Modifier](5-MakingMethodCallSimple.md#5-4) 解决表达式用副作用的问题
- [Extract Method](#1-1) 进一步优化


## Introduce Explaining Variable <p id="1-5"></p>


## Split Temporary Variable <p id="1-6"></p>

如果有一个临时变量被重复赋值, 且该变量并不是循环变量或者用来迭代的变量时, 应该在每次赋值
的时候都采用一个单独的临时变量.(从 Java 的角度就是尽量将临时变量定义成 final)

### 原因:
如果一个临时变量被赋值多次, 说明该变量有多个职责. 这个是不应该出现的, 所以每次赋值应该使
用一个新的变量.

## Remove Assignments to Parameters <p id="1-7"/>

删除对参数的赋值, 用临时变量代替.

### 原因:
可以让对参数的使用保持一致性.

## Replace Method with Method Object <p id="1-8"/>



