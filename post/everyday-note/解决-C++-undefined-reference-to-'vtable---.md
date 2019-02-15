## 问题
C++ 工程编译时(g++)遇到了令人烦恼的 error: 
```
undefined reference to 'vtable...
```
莫名其妙的错误提示.

## 解决
这一问题法人出现多半是由于实现文件未参与到工程编译工程中, 首先确认 make 类工具(如 cmake, automake, makefile, qmake 等等)的配置文件是否漏掉存在问题的文件, 其次重新编译包含出现问题 class 的工程(组件). 即可解决问题. 


## 参考
[http://gcc.gnu.org/faq.html#vtables](http://gcc.gnu.org/faq.html#vtables)
[https://stackoverflow.com/questions/3065154/undefined-reference-to-vtable](https://stackoverflow.com/questions/3065154/undefined-reference-to-vtable)

