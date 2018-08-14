# 坏代码的味道

## Deplicated 重复的代码.

DRY 原则。尽量不要用重复的代码。

相关的重构方法：
- [Extract Method](1-ComposingMethod.md#1-1)
- Pull up Field
- Form Template Method
- Substitute Algorithm
- Extract Class

## Long Method (长方法)

单个方法太长。 太长的方法会变得特别难理解。我的个人标准是最好是一个屏幕就可以显示整儿方法， 
方法的嵌套层次最高不要超过 3 层.

相关重构方法：
- [Extract Method](1-ComposingMethod.md#1-1)
- Replace Temp with Query
- Instroduce Parameter Object
- Preserve Whole Object
- Replace Method with Method Object
- Decompose Conditional

## Large Class (巨大的类)

一个类的太大通常意味着这个类承担了过多的职责. 判断一个类是否太大的一个很重要的方法就是看
该类拥有的变量的个数. 

相关的重构方法:
- Extract Class
- Extract Subclass
- Extract Interface
- Duplicate Observed Data

## Long Parameter List (长参数列表)

参数列表太长会让函数变得比较难理解, 出错的可能性会上升. 而且如果参数中含有多个同类型的参数
则更容易混淆.

当然, 在一些支持命名参数的语言, 如 Kotlin 和 Swift 多个参数造成的问题会被减弱. 但是过多
的参数依然不可取.

相关的重构方法:
- Replace Parameter with Method
- Preverse Whole Object
- Introduce Parameter Object

## Divergent Change(发散式改变)

## Shotgun Surgery(散弹式修改)

## Feature Envy

## Data Clumps

## Primitive Obsession

## Switch Statements

## Parallel Inheritance Hierarchies

## Lazy Class

## Speculative Generality

## Temporary Field

## Message Chains(过度耦合的消息链)

调用者会连续使用 get 方法来获得一个信息. 比如:
```java
xxx.getYY().getZZ().getWW();
// or:
y = xxx.getYY();
z = y.getZZ();
w = z.getWW();
```
Message Chains 会导致调用者和多个对象耦合. 任意一个对象的修改都会影响到调用者.

相关的重构方法:
- **Hide Delegate**
- [Extract Method](1-ComposingMethod.md#1-1)
- Move Method

## Middle Man (中间人)

有些类只是充当中间人的作用, 将请求委托给另一个类.

Middle Man 和 Message Chains 相关联. 改进一个问题可能会造成另外一个问题. 
二者的度需要好好把握.

相关重构方法:
- Remove Middle Man
- Inline Method
- Replace Delegate with Inheritance

## Inappropriate Intimacy (狎昵关系)

一个类知道另一个类的过多实现细节, 有时候是互相. 这样是破坏了类的封装性. 在继承关系中, 
子类就经常知道过多父类的实现细节.

相关的重构方法:
- Move Method
- Move Field
- Extract Class
- Hide Delegate
- Change Bidirectional Association to Unidirectional
- Replace Delegation with Inheritance 

## Alternative Classes with Different Interfaces (异曲同工类)

两个类做同样的事情却没有实现同一个接口. 甚至连函数签名也不同.

相关的重构方法:
- Rename Method
- Move Method
- Extract Superclass

## Incomplete Library Class (不完美的库类)

类库很难做的完美, 我们可以利用一些方法来让增加库的方法.

- Introduce Foreign Method
- Introduce Local Extension

## Data Class (纯粹的数据类)

纯数据的对象通常意味着:
1. 该类没有任何职责
2. 该类的使用者知道了过多的细节.

相关的重构方法:
- Encapsulate Field
- Encasulate Collection
- Remove setting method
- Move Method
- Extact Method
- Hide Method

## Refused Bequest (拒绝馈赠)

子类有可能不需要继承父类所有的方法. 大部分情况下不值得为了这种简单的情况去重构. 如果这种现象造成了问题与困惑, 
可以考虑抽象出一个更小父类. 

但是如果子类不想支持父类的接口, 那就不要使用继承的方式.


## Comments

注释本身是必要的, 但是很多信息可以通过代码本身获得, 对于这些信息没有必要在写在注释中. 比如解释代码块的作用的代码
可以变成函数名.

同时还有很多人利用注释来掩盖代码结构不清晰的问题.

相关的重构方法:
- Extract Method
- Rename Method
- Introduce Assersion