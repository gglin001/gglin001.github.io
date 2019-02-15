今天尝试下采用Qt Designer设计界面,设计完成后保存为一个dlg.ui文件,这个文件该怎样使用呢?
首先要理解ui文件在编译时的处理,qmake和uic工具将ui文件转换成可符合C++认可的结构,包含:

- Pointers to the form's widgets, layouts, layout items, button groups, and actions.
- A member function called setupUi() to build the widget tree on the parent widget.
- A member function called retranslateUi() that handles the translation of the string properties of the form. 

对于ui文件,一般有以下几种使用方法:

## 0x01 Compile Time Form Processing
3种使用方法
- The Direct Approach: you construct a widget to use as a placeholder for the component, and set up the user interface inside it.
(直接使用生成的ui_*.h文件)

- The Single Inheritance Approach: you subclass the form's base class (QWidget or QDialog, for example), and include a private instance of the form's user interface object.
(单继承方法)

- The Multiple Inheritance Approach: you subclass both the form's base class and the form's user interface object. This allows the widgets defined in the form to be used directly from within the scope of the subclass.
(多继承方法)

当然,首先要做的是在工程中加入ui文件
```
FORMS       = dlg.ui
```

### 直接使用
加入
```
#include "ui_dlg.h"
```
即可使用
```
// ...
QWidget *w = new QWidget;
Ui::dlg ui;  //注意在Ui namespace中,定义在ui_dlg.h中
ui.setupUi(w);  //setupUi函数
w->show();
// ...
```
这样的方式简单直接,但若是想要dlg窗口的元素与自己的代码集成,还是要用到下面的方式;

### 单继承方法
存在两种方式:
- dlg作为成员变量;
- dlg作为成员指针变量;

#### member variable
新建一个widget类,其头文件像这样:
```
#include "ui_calculatorform.h"  //注意与下面的区别

class widget : public QWidget
{
    Q_OBJECT

public:
    widget(QWidget *parent = 0);
private:
    Ui::dlg ui;
// ...
};
```

构造函数:
```
widget::widget(QWidget *parent)
    : QWidget(parent)
{
    ui.setupUi(this);
}
```
由于Ui::dlg是作为成员变量使用的,因此可以在一个QWidget中添加多个界面,也可十分方便的进行自定义signal与slot的处理.

#### Pointer Member Variable
新建一个widget类,其头文件像这样:
```
namespace Ui {
    class dlg;  //前置声明
}

class widget : public QWidget
{
widget();
virtual ~widget();
private:
    Ui::dlg *ui;
// ...
}
```
cpp文件:
```
#include "ui_dlg.h"  //包含ui_*.h

widget::widget(QWidget *parent) :
    QWidget(parent), 
    ui(new Ui::dlg)  // new出新的dlg
{
    ui->setupUi(this);  //setupUi
}

widget::~widget()
{
    delete ui;  //析构时要删除ui
}
```
这种方式有利于二进制兼容性的实现;(此处不太懂)

### 多继承方法
新建一个widget类,其头文件像这样:
```
#include "ui_dlg.h"

class widget : public QWidget, private Ui::dlg  //多继承
{
    Q_OBJECT

public:
    widget(QWidget *parent = 0);

//...
};
```
构造函数:
```
widget::widget(QWidget *parent)
    : QWidget(parent)
{
    setupUi(this);
}
```


## 0x02 Reacting to Language Changes

对于上面的widget,reimplement QWidget::changeEvent()
```
void widget::changeEvent(QEvent *e)
{
    QWidget::changeEvent(e);
    switch (e->type()) {
    case QEvent::LanguageChange:
        ui->retranslateUi(this);  //retranslateUi函数
        break;
    default:
        break;
   }
}
``` 

## Run Time Form Processing

借助 QtUiTools模块实现
工程中要添加
```
CONFIG += uitools
```
头文件:
```
#include <QtUiTools>
```
使用:
```
QUiLoader loader;
QFile file(":/dlg.ui");
file.open(QFile::ReadOnly);
QWidget *w = loader.load(&file, this);
file.close();
```
本文基本是照着文献1来写的,推荐看下原文;

## 参考文献
[http://doc.qt.io/archives/qt-4.8/designer-using-a-ui-file.html](http://doc.qt.io/archives/qt-4.8/designer-using-a-ui-file.html)
[https://blog.csdn.net/zzwdkxx/article/details/25823363](https://blog.csdn.net/zzwdkxx/article/details/25823363)
