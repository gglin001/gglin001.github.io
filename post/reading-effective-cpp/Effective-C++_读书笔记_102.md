# 构造/析构/赋值运算

## 条款05
### 了解C++默默编写并调用了哪些函数
编译器可以暗自创建default构造函数,copy构造函数,copy assignment操作符以及析构函数(C++11后添加了默认移动构造函数和默认移动操作符);
即:
```
class Empty { } ;
```
经编译器处理后等价于(只有这些函数被调用时才创建):
```
class Empty {
public:  //注意是public
  Empty () { ... }  //只处理非静态成员
  Empty (const Empty& rhs) { ... }
  ~Empty () { ... }
  
  Empty& operator=(const Empty& rhs) { ... }
};

```

## 条款06
## 若不想使用编译器自动生成的函数,就应明确拒绝
可以将相应成员函数声明为private并且不予实现即可达到目的;(调用会引起linkage error)
C++11中存在更好的解决方案,即还函数声明后添加 `= delete`

## 条款07
## 为多态基类声明virtual析构函数
带多态性质的base class应声明一个virtual析构函数;如果class带有任何virtual函数,它都应具有一个virtual析构函数;
含有virtual函数的对象在体积上上会有明显的增加,所以,若class的设计不是作为base class或不是为了具有多态性,析构函数就不要成为virtual;
对于C++11,要用好final,override等关键字

## 条款08
## 别让异常逃离析构函数
C++不喜欢析构函数吐出异常;
若要对耨个操作函数运行期间抛出的异常做出反应,class应该提供一个普通函数(而非在析构函数中)执行该操作;

## 条款09
## 决不在构造函数和析构函数中调用virtual函数
原因是这类调用从不会下降到derived class;
要确保构造函数和析构函数都没有调用virtual函数,而它们调用的所有函数也都服从同一约束;

## 条款10
## 令operator= 返回一个reference to *this
该条款同样适用于operator+=等所有赋值相关运算;
即写成
```
...
className& operator=(const className& rhs){
...
  return *this;
}
...
```

## 条款11
## 在operator= 中处理"自我赋值"
"自我赋值"指的是对象赋值给自己时;实现"异常安全性"可自然获得"自我赋值安全性",所以可直接关注异常安全的处理;
达到"自我赋值安全性"的技术包括:比较双方地址(认同测试,这可能会有效率问题), 精心周到的语句顺序(先保持原有数据的指针,new操作异常时会保持原状),copy-and-swap(两种方式,1传引用,制作副本,swap;2传值,swap);
要确保任何函数如果操作一个以上的对象,而其中的多个对象是同一对象时,其行为依然安全.

## 条款12
## 复制对象时勿忘其每一个成分
copying函数指的是copy构造函数和copy assignment操作符;
Copying函数应确保复制"对象内的所有成员变量"和"所有base class 成分";
不要尝试以某个copying 函数实现另一个copying函数,应将共同机能放进某个函数中,并由两个copying函数共同调用;
