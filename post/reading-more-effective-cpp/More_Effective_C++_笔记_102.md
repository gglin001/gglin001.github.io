# 操作符

## 条款05
##   对定制的"类型转换函数"保持警惕
具有隐式类型转换的函数: 单自变量 constructors 和隐式类型转换符(opearator xx 函数).
解决办法, 对于单自变量 constructors 应使用 explicit 关键词(推荐)或采用一个 proxy class 禁止隐式转换调用; 不要声明隐式类型转换符

## 条款06
 ## 区别 increment/decrement 操作符的前置(prefix)和后置(postfix)形式
前置式, 累加然后取出, 返回对象引用.
后置式, 取出然后累加, 返回 const 对象, 因返回旧值, 且不能允许(i++++)合法.

## 条款07
## 千万不要重载 &&, || 和 , 操作符
因为对于这些操作符, 无论你多努力, 也无法令其行为和它们该有的行为一样.
对于 , 操作符, 逗号左边的先被评估, 然后右边的被评估, 逗号表达式的结果以右侧的值为代表(即返回值), 如用在 for 循环第三个参数里面.
ps: 何必要自虐搞这些操作符的重载呢.

## 条款08
## 了解各种不同意义的 new 和 delete
new operator (new expression) 即平常用法, 做了两件事, 1. 分配足够的内存; 2. 调用一个 constructor.
operator new 返回一个指针, 指向一块原始的内存. 用法如:
```
void *rawMem = operator new (sizeof(string))
```
placement new 用于在已分配的内存中构造对象. 如:
```
widget * constructWidgetinBuffer(void *buff, int widgetSize){
    return new (buff) widget(widgetSize);
}
```

与 new 相似, 存在 delete operator 和 operator delete
delete operator 即常用的 delete 形式, 如:
```
string *ps;
...
delete ps;
```
近似于:
```
ps->~string();
operator delete(ps);
```
即 operator delete 只处理原始的内存.
ps: 说来说去只要抓住内存的获取和释放以及对象的创建与析构即可理清这些.
当然, 对于数组(array), 应使用类似于下面的形式:
```
string *ps = new string[10];
delete [] ps;
```

