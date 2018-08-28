# Organnizing Data

这一章节的重构方法都是为了让对数据的处理变得更简单. 这里的方法有些看起来是相反的, 
设计是一个取舍的过程, 一切都为了让代码变得更容易理解.

## Self Encapsulate Field

## Replace Data Value with Object

## Change Value to Reference

## Change Reference to Value

## Replace Array with Object

## Duplicate Observed Data

## Change Unidirectional Asssociation to Bidirectional

## Change Bidirectional Association to Unidiectional

## Replace Magic Number with Symbolic Constant

## Encapsulate Field

## Encapsulate Collection

## Replace Record with Data Class
用一个数据类来取代原始的记录. 比如一个 JSONObject.


## Replace Type Code with Enum
原书该方法的名字是 Replace Type Code with Class. 可能是因为书出的时间比较早, Java 还没有 Enum类型.
从书上给的例子来看, 显然使用 enum 会更加方便.

如果一个类里有用数字来表示类型的域, 那么最好使用 enum 类型来代替. 使用 int 时, 编译器无法检查用户使用的值是否正确.
但是使用 enum 可以保证值都是在确定的范围内.

使用该重构方法的前提是 Type Code 并不会影响类的行为, 如果会影响应该考虑使用下面两种重构方法.


## Replace Type Code with Subclass
如果该类的 Type Code 是**不可变的**且**会影响类的行为**, 这时应该使用子类来代替 Type Code.


## Replace Type Code with State/Strategy
如果类当中的 Type Code 会是可变的, 那就不能简单地使用子类来代替. 而是应该使用 State 或者 
Strategy 两种模式, 用一个状态类来代替 Type Code.

这里其实依然可以使用 enum 类型来实现这个状态类. 因为 Java 的 enum 可以带状态, 也可以重写父类的方法.

## Replace Subclass with Fields
如果子类和父类之间的区别只有一些 constant mehtod 返回的值不同, 那应该尝试在父类中添加一个代表该属性的域,
并移除子类.