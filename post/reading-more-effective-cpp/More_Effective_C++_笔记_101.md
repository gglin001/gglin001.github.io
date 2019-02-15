# 基础议题

## 条款01
## 仔细区别 pointer 和 reference
当你需要指向某个东西, 而且确保绝不会改变指向其他东西, 或是当你实现一个操作符而其语法需求 (如 T[x]) 无法由 pointer 达成, 你就应该选择 reference. 其他任何时候, 请采用 pointer.

## 条款02
## 最好使用 C++ 转型操作符
旧式转型(C式)是为 C 设计的, 而非 C++.
应使用 static_cast, const_cast, dynamic_cast, reinterpret_cast 替代. 

## 条款03
## 绝对不要以多态方式处理数组
因为子类往往会对父类进行扩展, 在数组中利用父类指针而实际对象为子类类型时往往发生意想不到的事情.

## 条款04
## 非必要不提供 default constructor.
default constructor 即不给任何自变量就可对对象进行初始化.
这个是个两难的问题, 添加或不添加 default constructor 都会有一些讨论.
若 default constructor 不能够使得对象所有字段都会被正确初始化, 就避免出现它.
