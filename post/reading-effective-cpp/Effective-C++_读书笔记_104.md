# 设计与声明
"让接口容易使用,让接口不容易被误用"

## 条款18
## 让接口容易使用,不容易被误用
接口包括function接口,class接口,template接口...
"正确使用"要尽力做到接口的一致性,与内置类型的行为兼容;
"阻止误用"包括建立新类型,限制类型上的操作,束缚对象值,以及消除客户的资源管理任务;
shared_ptr支持定制deleter,这可以防范DLL问题(对象在不同的DLL中被new和delete),可被用来自动解除mutex;

## 条款19
## 设计class犹如设计type
设计类之前问自己以下问题:
1. 新type的对象应如何被创建和销毁?
涉及到了构造函数和析构函数的设计.
2. 对象的初始化和对象的赋值该有怎样的差别?(初始化发生于构造函数作用之前)
决定了构造函数和赋值操作符的行为和他俩的差异.
3. 新type若被passed by value,意味着什么?
即copy构造函数的设计.
4. 什么是新type的"合法值"?
决定了成员函数(特别是setter函数,如构造函数,赋值operator)必须进行的错误检查工作,以及异常处理等.
5. 新type需要配合某个继承图系吗?
作为子类要考虑父类成员的成员是否是virtual,作为父亲会影响到声明的函数,尤其是析构函数是否应是virtual.
6. 新type需要什么样的转换?
涉及到单成员构造函数是否为explicit,是否需要添加类型转换成员函数/操作符(条款15有案例).
7. 什么样的操作符和函数对此新typr是合理的?
决定了为新type添加哪些函数,包括menmber函数和非menber函数.
8. 什么样的标准函数应该驳回?
声明到private中.
9. 谁该取用新type的成员?
决定哪个成员成为public,protect,private,以及friend函数/class,以及类的嵌套.
10. 新type有多一般化?
对于有types家族需要的情况,也许class template更合适.
11. 你真的需要一个新type吗?
如只是定义新的derived class以便为既有class增加功能,也许你只需要一个或多个普通函数/模板函数罢了.

记住,class设计就是type设计!

## 条款20
## 宁以pass-by-reference-to-const 替换pass-by-value
一般来说,pass-by-reference-to-const比pass-by-value节省了至少(class没有父亲)一次构造和一次析构;reference在编译器中以指针实现,pass-by-reference本质上就是指针传递.
尽量以pass-by-reference-to-const替代pass-by-value,前者通常比较高效,并可以避免切割问题.
以上规则并不适用于内置类型,以及STL的迭代器和函数对象,对于这些,pass-by-value更适当.

## 条款21
## 必须返回对象时,别妄想返回其reference
注意:reference不可指向不存在的对象(特别注意不要用到local对象上),他只是个别名;
绝不要返回pointer或reference指向一个local stack对象,或返回reference指向一个heap-allocate对象,或返回pointer或reference指向一个local static对象而有可能同时需要多个这样的对象(单例模式只有一个对象).

## 条款22
## 将成员变量声明为private
切记将成员变量声明为private,这有诸多好处;
protected并不比public更具封装性;

## 条款23
## 宁以non-member,non-friend替代member函数
不要误解了封装性,封装性高指的是对外界暴露的机会更少.
宁可拿non-member non-friend函数替代member函数,这样可以增加封装性,包裹弹性和机能扩充性.

## 条款24
## 若所有参数皆需类型转换,请为此采用non-memer函数
member函数的反面是non-menber函数,与friend无关.
如果你需要为某个函数(包含operator)的所有参数进行类型转换,那么这个函数必须是个non-member.

## 条款25
## 考虑写出一个不抛异常的swap函数
当std::swap对你的类型效率不高时,提供一个swap成员函数,并确定该函数不爬出异常.
若你提供了一个member swap,也应提供一个non-member swap用来调用前者,对于class(非template),也应特化std::swap.
为"用户定义类型"进行std template全特化是好的,但千万不要尝试在std中加入某些对std而言全新的东西.
