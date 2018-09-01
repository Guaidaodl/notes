# Simpliying Conditional Expressions

条件判断在代码里非常常见, 但是条件判断经常会导致代码变得难以理解. 可以使用本章里的重构方法来简化相关的代码.


## Decompose Conditional <p id="4-1"/>

分解条件表达式. 条件表达式的条件和分支可能都比较比较杂. 可以使用 extract method 的方法将条件
判断或者分支放到一个方法中. 这样可以减少代码的行数, 降低代码的复杂度, 提高可读性.

### 相关方法:
- [Extract Method](1-ComposingMethod.md#1-1)


## Consolidate Conditional Expression  <p id="4-2"/>

如果有两个分支的行为是一致的, 可以考虑合并两个分支. 如果合并后条件过于复杂可以使用 Decompose 
Conditional 方法来简化判断.


## Consolidate Duplicate Condistional Fragments  <p id="4-3"/>

如果所有的分支都有相同的代码. 应该将相同的代码提取出来, 放到分支判断的外面.


## Remove Constrol Flag  <p id="4-4"/>

使用 break, coutinue 和 return 来代替 Control Flag.


## Replace Nested Conditional with Guard Clauses  <p id="4-5"/>

嵌套的条件表达式导致代码层次过多, 写出火箭型的代码. 还可能导致正常情况的处理路径被错误处理路径掩盖,
导致代码不好理解. 应该使用 Guard Clause 尽快处理错误请并返回.

Before:
```java
if (aaa) {
    if (bbb) {
        if (ccc) {
            if (ddd) {
                // do something
                return;
            }
        }
    }
}
```

After:
```java
if (!aaa) return;
if (!bbb) return;
if (!ccc) return;
if (!ddd) return;

// do something
```


## Replace Conditional with Polymorphism  <p id="4-6"/>

根据 Type Code 来执行不同行为的代码最好使用多态的方式重新实现.

相关方法:
- [Replace Type Code with Enum](3-OrganizingData.md#3-13)
- [Replace Type Code with Subclass](3-OrganizingData.md#3-14)
- [Replace Type Code with Stragety](3-OrganizingData.md#3-15)


## Introduce Null Object  <p id="4-7"/>

不要使用 null 来代码没有, 而是使用一个特殊的对象来表示空. 通过 Null Object 可以减少很多判空的操作,
让代码的逻辑更清晰. 

不过现在很多语言都支持类型 optional 的类型, optional 类型可以取代一部分 Null Object 的作用.

<span id="4-8"></span>
## Introduce Assertion  

使用 assertion 来检查条件. 可以让错误今早被发现, 也有利于方法被理解.

Assertion 是用代码来表达一些隐含的限制. 跟 assertion 有类似功能还有 Annotation 和 Precondition.
Anotation 主要是在编译阶段进行一些检查, 比如 Android 里常用的 @NonNull 和 @Nullable. 
Precondition 与 Assertion 类似, 不过 Assertion 只有在 debug 版中存在, Precondition 
在 release 版也会存在.

NPE 是 Java 开发中最常见的一种错误. 在开发中, 我一直都会尽可能给每个函数的返回值和参数都加上
@NonNull 或者 @Nullable 约束. 然后在函数的内部利用 Precondition 来确保参数满足约束.

很明显在在没有函数中加入 Precondition 会显得代码比较冗余. 我的原则是确保错误不会扩散, 尽早地失败,
保留第一现场(调用栈). 比如下面的代码:
```java
void foo(@NonNull String s) {
    int l = s.length();

    //....
}
``` 
foo 函数即使不加 Precondition 也没有关系, 因为如果 s 为空, 那么在执行 s.length() 的时候程序
就会崩溃. 通过调用栈可以很清晰的知道是谁给 foo 函数一个非法参数.

有时错误则会扩散. 比如下面的代码:
``` java
class Bar {
    @NonNull A a;

    public Bar(@NonNull A a) {
        this.a =a;
    }

    public void setA(@NonNull A a) {
        this.a = a;
    }
}
```
Bar 得构造函数和 setA 方法都约束了参数 a 不能为空, 但是即使调用者传了一个为 null 的参数, 
程序也可以正常运行. 只用等到后续使用 a 时才会导致代码崩溃, 这时的从调用栈里就看不出来始作俑者是谁了.
所以应该给这两个方法加上 Precondition.
``` java
class Bar {
    @NonNull A a;

    public Bar(@NonNull A a) {
        this.a = Precondition.checkNotNull(a);
    }

    public void setA(@NonNull A a) {
        this.a = Precondition.checkNotNull(a);
    }
}
```
这样代码就会及时崩溃, 不会导致错误扩散.
