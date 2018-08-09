# Composing methods. 重组函数

## Extract Method (提炼方法)

编号: 1-1

将一部分代码提炼成一个函数.

### 好处:
- 缩短函数长度. 让函数更容易理解.
- 将代码提炼成一个函数, 可以让代码的目的和作用更清晰.

### 重构的难点:
- 处理临时变量.

### 相关联的方法:

- Replace Temp with Query. 用户减少临时变量.

- Split Temporary Variable. 让临时变量更容易被取代.

- Replace Method with Method Object. 临时变量太过复杂无法提炼时可以采用.

