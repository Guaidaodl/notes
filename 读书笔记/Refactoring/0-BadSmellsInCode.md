# 坏代码的味道

## Deplicated 重复的代码.

DRY 原则。尽量不要用重复的代码。

相关的重构方法：
- [Extract Method](1-ComposingMethod.md#1-1)
- Pull up Field
- Form Template Method
- Substitute Algorithm
- Extract Class

## Long Method

单个方法太长。 太长的方法会变得特别难理解。我的个人标准是最好是一个屏幕就可以显示整儿方法， 方法的嵌套层次最高不要超过 3 个。

相关重构方法：
- [Extract Method](1-ComposingMethod.md#1-1)
- Replace Temp with Query
- Instroduce Parameter Object
- Preserve Whole Object
- Replace Method with Method Object
- Decompose Conditional

## Large Class

## Long Parameter List

## Divergent Change

## Shotgun Surgery

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

一个类知道另一个类的过多实现细节, 有时候是互相. 这样是破坏了类的封装性. 在继承关系中, 子类就经常知道过多父类的实现细节.

相关的重构方法:
- Move Method
- Move Field
- Extract Class
- Hide Delegate
- Change Bidirectional Association to Unidirectional
- Replace Delegation with Inheritance 

## Alternative Classes with Different Interfaces

## Incomplete Library Class

## Data Class

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

## Refused Bequest

## Comments