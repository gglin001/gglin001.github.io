# 模板与范型编程
C++ template 演变:
type-safe(类型安全, 主要指容器) -> generic programing(范型编程, 如 STL 算法) -> template metaprograming(模板元编程, 即利用编译期生成代码, 或称为代码运行在编译期内的方式)

## 条款41
## 了解隐式接口和编译期多态
隐式接口就是让表示式必须成立(成立即可)所满足的条件, 并非依靠函数签名式(包含函数名称, 参数类型和返回类型).
编译期多态指在编译期"以不同的 template 参数具现化 function templates".
classes 和 templates 都支持接口(interface)和多态(polymorphism).
对于classes, 接口是显式的, 以函数签名为中心, 多态则是通过 virtual 函数发生于运行期.
对于templates, 接口是隐式的, 基于有效表达式, 多态则是通过 template 具现化和函数重载解析发生于编译期.

## 条款42
## 了解 typename 的双重意义
声明 template 参数时, class 和 typename 可以互换.
请使用关键字 typename 标识嵌套从属类型(目的)名称, 但不得在 base classes lists(基类列)或 member initialization list(成员初值列)内以它作为 base class 修饰符.

## 条款43
## 学习处理模板化基类内的名称

## 条款44
## 

## 条款45
## 

## 条款46
## 

## 条款47
## 

## 条款48
## 
