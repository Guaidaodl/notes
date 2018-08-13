# Composing methods. 重组函数

## Extract Method (提炼函数) <p id="1-1"></p>

将一部分代码提炼成一个函数.

### 好处:
- 缩短函数长度. 让函数更容易理解.
- 将代码提炼成一个函数, 可以让代码的目的和作用更清晰.

### 重构的难点:
- 处理临时变量.

### 相关联的方法:

- [Replace Temp with Query](#1-4) 用户减少临时变量.

- [Split Temporary Variable](#1-6) 让临时变量更容易被取代.

- [Replace Method with Method Object](#1-8) 临时变量太过复杂无法提炼时可以采用.

## Inline Method (内联函数) <p id="1-2"></p>

## Inline Temp (内联临时变量) <p id="1-3"></p> 

## Replace Temp with Query (以查询取代临时变量) <p id="1-4"></p>

## Introduce Explaining Variable <p id="1-5"></p>

## Split Temporary Variable <p id="1-6"></p>

如果有一个临时变量被重复赋值, 且该变量并不是循环变量或者用来迭代的变量时, 应该在每次赋值的时候都采用一个单独的临时变量.
(从 Java 的角度就是尽量将临时变量定义成 final)

### 原因:
如果一个临时变量被赋值多次, 说明该变量有多个职责. 这个是不应该出现的, 所以每次赋值应该使用一个新的变量.

## Remove Assignments to Parameters <p id="1-7"/>

删除对参数的赋值, 用临时变量代替.

### 原因:
可以让对参数的使用保持一致性.

## Replace Method with Method Object <p id="1-8"/>



