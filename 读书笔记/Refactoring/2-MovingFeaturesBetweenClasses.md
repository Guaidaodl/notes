# Moving Features Between Class
确定类的职责是面向对象的设计的一个基本步骤, 但是一开始就可以做出正确的设计却很难.
所以当发现需要改动的时候需要使用合适的重构方法.

## Move Method <p id="2-1"/>
## Move Field <p id="2-2"/>
## Extract Class <p id="2-3"/>
## Inline Class <p id="2-4"/>
## Hide Delegate <p id="2-5"/>
## Remove Middle Man <p id="2-6"/>
## Introduce Foreign Method <p id="2-7"/>

想给一个类添加**一个**方法但是又不能修改该类时. 可以写一个方法将需要扩展的类作用参数.

感觉这个没有什么用.

## Introduce Local Extension <p id="2-8"/>

当你想给一个类添加一些方法但是你又不能修改该类时，可以新建一个该类的子类，或者新建一个该类的Wrapper,
然后在添加方法.

两者相比较, 子类的方法更方便一点. 但是最方便的还是语言本身支持扩展功能, 比如 Swift 和 Kotlin.