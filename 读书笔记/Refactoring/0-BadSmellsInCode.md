# 坏代码的味道

## Deplicated (重复的代码)

DRY 原则。尽量不要用重复的代码。

相关的重构方法：
- [Extract Method](1-ComposingMethod.md#1-1)
- Pull up Field
- Form Template Method
- Substitute Algorithm
- [Extract Class](2-MovingFeaturesBetweenClasses.md#2-3)

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
- [Extract Class](2-MovingFeaturesBetweenClasses.md#2-3)
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

## Divergent Change (发散式改变)

一个类可能因为多种不同的原因被改变, 证明该类应该被拆分成多个类.

相关重构方法:
- [Extract Class](2-MovingFeaturesBetweenClasses.md#2-3)

## Shotgun Surgery (散弹式修改)

跟 Divergent Change 相反, 同一个变化会造成多个类的改变.

相关重构方法:
- [Move Method](2-MovingFeaturesBetweenClasses.md#2-1)
- [Move Field](2-MovingFeaturesBetweenClasses.md#2-2)
- [Inline Class](2-MovingFeaturesBetweenClasses.md#2-4)

## Feature Envy (依恋情结)

一个类的方法里过多的依赖另外一个类, 比如大量调用另一个类的 getter 来进行计算. 
这样的类显然更适合放到另一个类中.

有一些设计模式违背了这个原则, 比如 Strategy 和 Visitor 模式. 
所以遇到时需要确定不是特意做成这样的, 如果不是再进行重构.

相关重构方法:
- [Move Method](2-MovingFeaturesBetweenClasses.md#2-1)
- [Extract Method](1-ComposingMethod.md#1-1)

## Data Clumps (数据泥团)

如果某些数据总是一起出现. 比如一起作为某个类的成员变量, 作为函数的参数. 这时应该将这些
数据包装成一个类.

包装成一个类以后会减少一些坏味道, 但是还会造成其他的*坏味道*. 比如 Feature Envy, Data Class,
Inappropriate Imaticy 等. 所以分析这些数据的使用方式来继续优化.

相关重构方法:
- [Extract Class](2-MovingFeaturesBetweenClasses.md#2-3)
- Introduce Parameter Object
- Perserve Whole Object

## Primitive Obsession (基本类型偏执)

偏爱基本类型, 抗拒使用一些简单的类. 这应该也是造成数据泥团的重要原因.

相关重构方法:
- Replace Data Value with Object
- [Replace Type Code with Enum](3-OrganizingData.md#3-13)
- [Replace Type Code with Subclass](3-OrganizingData.md#3-14)
- [Replace Type Code with Stragety](3-OrganizingData.md#3-15)
- [Extact Class](2-MovingFeaturesBetweenClasses.md#2-3)
- Introduct Parameter Object

## Switch Statements

大部分的 Switch 语句都可以利用多态以更优雅的形式来实现. 
如果只有一两个方法需要用到大量的 Switch 语句则没有必要进行重构.

## Parallel Inheritance Hierarchies (平行继承体系)

Shotgun Surgery 的一种, 当你为某个类创建一个子类时, 也需要为另一个创建一个子类.

相关重构方法:
- [Move Method](2-MovingFeaturesBetweenClasses.md#2-1)
- [Move Field](2-MovingFeaturesBetweenClasses.md#2-2)

## Lazy Class (冗赘类)

一些类如果不能起到足够的作用, 那就应该被删除, 减少维护的成本.

相关重构方法:
- Collapse Hierarchy
- [Inline Class](2-MovingFeaturesBetweenClasses.md#2-4)

## Speculative Generality (夸夸奇谈的未来性)

为了某些不确定的需求和变化增加了代码复杂度. 简单来说就是过度设计.

相关重构方法:
- Collapse Hierarchy
- [Inline Class](2-MovingFeaturesBetweenClasses.md#2-4)
- Remove Parameter
- Rename Method

## Temporary Field (临时属性)

一些类的成员变量只是用来记住一些临时的属性. 比如一个初始化的参数.

相关重构方法:
- [Extract Class](2-MovingFeaturesBetweenClasses.md#2-3)
- Introduce Null Object

## Message Chains (过度耦合的消息链)

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
- **[Hide Delegate](2-MovingFeaturesBetweenClasses.md#2-5)**
- [Extract Method](1-ComposingMethod.md#1-1)
- [Move Method](2-MovingFeaturesBetweenClasses.md#2-1)

## Middle Man (中间人)

有些类只是充当中间人的作用, 将请求委托给另一个类.

Middle Man 和 Message Chains 相关联. 改进一个问题可能会造成另外一个问题. 
二者的度需要好好把握.

相关重构方法:
- [Remove Middle Man](2-MovingFeaturesBetweenClasses.md#2-6)
- Inline Method
- Replace Delegate with Inheritance

## Inappropriate Intimacy (狎昵关系)

一个类知道另一个类的过多实现细节, 有时候是互相. 这样是破坏了类的封装性. 在继承关系中, 
子类就经常知道过多父类的实现细节.

相关的重构方法:
- [Move Method](2-MovingFeaturesBetweenClasses.md#2-1)
- [Move Field](2-MovingFeaturesBetweenClasses.md#2-2)
- [Extract Class](2-MovingFeaturesBetweenClasses.md#2-3)
- [Hide Delegate](2-MovingFeaturesBetweenClasses.md#2-5)
- Change Bidirectional Association to Unidirectional
- Replace Delegation with Inheritance 

## Alternative Classes with Different Interfaces (异曲同工类)

两个类做同样的事情却没有实现同一个接口. 甚至连函数签名也不同.

相关的重构方法:
- Rename Method
- [Move Method](2-MovingFeaturesBetweenClasses.md#2-1)
- Extract Superclass

## Incomplete Library Class (不完美的库类)

类库很难做到完美, 我们可以利用一些方法来让增加库的方法.

- [Introduce Foreign Method](2-MovingFeaturesBetweenClasses.md#2-7)
- [Introduce Local Extension](2-MovingFeaturesBetweenClasses.md#2-8)

## Data Class (纯粹的数据类)

纯数据的对象通常意味着:
1. 该类没有任何职责
2. 该类的使用者知道了过多的细节.

相关的重构方法:
- Encapsulate Field
- Encasulate Collection
- Remove setting method
- [Move Method](2-MovingFeaturesBetweenClasses.md#2-1)
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
