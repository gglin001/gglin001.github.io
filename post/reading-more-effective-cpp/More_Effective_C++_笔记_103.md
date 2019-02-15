# 异常(exception)

## 条款09
##  利用 destructors 避免泄漏资源
即避免裸指针的使用, 将指针包装进对象里面, 即使用智能指针.

## 条款10
## 在 constructors 内阻止资源泄漏
请铭记: 对于"仅部分构造完成"的对象, C++ 拒绝调用其 destructor;
请以智能指针替代原始指针成员; 

## 条款11
## 禁止异常流出 destructors 之外
这里要考虑到栈展开(stack-unwinding)机制, 即一个函数抛出异常后, 首先在寻找本身的catch字句, 若不能处理, 就会退出当前函数(释放函数内存, 销毁局部对象, 但不处理 new 出的对象), 寻找上层的异常处理代码, 直到找到 catch 字句. 若没有找到, 就会调用 terminate 结束程序, 终端输出类似下面的信息:
```
terminate called after throwing an instance of 'int'
```
所以. 共有两种情况会调用 destructor, 1. 对象离开生存空间, 正常析构. 2. 栈展开过程中调用. 对于情况2, 应在 destructor 中捕捉任何异常, 但 catch 字块为空, 阻止了异常流出 destructor, terminate 也不会被调用.

## 条款12
## 了解"抛出一个异常"与"传递一个参数"或"调用一个虚函数"之间的差异


## 条款13
##

## 条款14
##

## 条款15
##

