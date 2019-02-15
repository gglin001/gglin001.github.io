# 继承与面向对象设计
OOP不是一项用来划分语言特性的仪典, 而是可以让你通过它说出你对软件系统的想法.
永远铭记 80-20 原则.
分析类的声明与定义, 一是接口在何处, 二是 实现在何处, 接口与实现的关系体现着设计模式的运用.

## 条款32
## 确定你的 public 继承塑模出 is-a 关系
public 继承意味着 is-a 关系. 适用于 base class 身上的每一件东西也一定适用于 derived classes 身上, 因为每个 derived class 对象也是一个 base class 对象.

## 条款33
## 避免遮掩继承而来的名称
简单来说就是不同作用域的问题.
derived class 内的名称会遮掩 base class 内的名称. 在 public 继承下从来没有人希望如此. (这样违反了条款32).

## 条款34
## 区分接口继承和实现继承
纯虚函数也可以有默认实现, 但只能实现接口继承;
接口继承和实现继承不同, 在 public 继承下, derived classes 总是继承 base class 的接口.
pure vitual 函数只具体指定接口继承.
impure virtual 函数具体指定接口继承和缺省实现继承.
non-pure 函数具体指定接口继承以及强制性实现继承.

## 条款35
## 考虑 virtual 函数以外的其他选择
virtual 函数的替代方案包括 NVI (Non-virtual interface) 手法和 Strategy 设计模式的多种形式, NVI 手法自身是一个特殊(一般)形式的 Template Method 设计模式.
NVI 手法用public non-virtual 成员函数包裹访问性较低的 virtual 成员函数.
将 virtual 函数替换为"函数指针成员变量", 这是 Strategy 设计模式的一种分解表现形式.
以tr1::function(C++11已加入std)成员变量替换 virtual 函数, 因而允许使用任何可调用物搭配一个兼容于需求的表达式, 这也是 Strategy 设计模式的体现.
将继承体系内的 virtual 函数替换为另一个继承体系内的 virtual 函数, 这是 Stategy 设计模式的传统手法.

## 条款36
## 绝不重新定义继承而来的 non-virtual 函数
为了防止出现面对同一对象, 不同类型的指针调用 non-virtual 函数表现不同的问题, 同时错误的做法也违背了条款32.
(面对自己写的代码, 惭愧...)

## 条款37
## 绝不重新定义继承而来的缺省参数值
绝对不要重新定义一个继承而来的缺省参数值, 因为缺省参数值都是静态绑定, 而 virtual 函数 - 你唯一应该覆盖的东西, 是动态绑定的.

## 条款38
## 通过复合塑模出 has-a 或 "根据某物实现出"
复合(composition)的意义与 public 继承完全不同
在应用域, 复合意味着 has-a (有一个), 在实现域, 复合意味着 is-implemented-in-terms-of (根据某物实现出) .

## 条款39
## 明智而审慎地使用 private 继承
private 继承意味着 is-implemented-in-terms-of. 它通常比复合的级别低. 但是当 derived class 需要访问 protect base class 的成员. 或者需要重定义继承而来的 virtual 函数时, 这么设计是合理的.
和复合不同, private 继承可以造成 empty  base 最优化, 对于库开发来说可达到"对象尺寸最小化".

## 条款40
## 明智而审慎地使用多重继承
多重继承比单一继承复杂, 它可能导致新的歧义性, 以及对 virtual 继承的需要.
virtual 继承一般只用在多重继承上面, 对于单继承体系, 会徒增成本.
virtual 继承会增加大小, 速度, 初始化复杂度增加等成本, 若 virtual base class 不带有任何数据, 将是最具实用价值的情况.
多重继承有正当的用途. 如"public 继承某个 Interface class" 和 "private 继承某个协助实现的 class" 的组合. (即接口内方法采用协助类实现).
