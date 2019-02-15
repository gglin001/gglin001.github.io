## 0x0

在使用Qt4做串口通信时,存在以下几种第三方库可以使用:

- QextSerialPort

- QtSerialPort

其中QtSerialPort可以看做时Qt”官方”生产的串口通信库,其在Qt5上已是正式的一员,但由于其出现较晚,在Qt4上QextSerialPort库应用较多.UniSYS2软件的串口通信部分也是以其为基础实现的.现对该库进行简要介绍. QtSerialPort库从1.2beta版本开始以MIT协议开发布. 最新版本为1.2RC,目前开发貌似已经停滞.

官方自我介绍:

QextSerialPort provides an interface to old fashioned serial ports for Qt-based applications. It currently supports Mac OS X, Windows, Linux, FreeBSD.

## 1 结构

### 1.1 包含两个类

- QextSerialPort 包括了可以应用在POSIX平台和Windows平台的串口.

- QextSerialEnumerator 可以获取系统中可用的端口.(使用getPorts()方法返回一个QextPortInfo结构体保存了相关信息)

重点介绍QextSerialPort类,其结构如图1所示.其中QextBaseType仅仅是一个宏定义,用于区别win和POSIX平台.

![图1 QextSerialPort类结构](https://upload-images.jianshu.io/upload_images/1711028-76aab4016a38b8ff.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 2 使用方式

### 2.1 直接使用源码

将源码下载后,目录里存在一个qextserialport.pro工程文件,将该文件包含在项目中即可使用.

windows下使用到的文件是:

- qextserialbase.cpp

- qextserialbase.h

- qextserialport.cpp

- qextserialport.h

- win_qextserialport.cpp

- win_qextserialport.h

linux等POSIX平台下则需将win_qextserialport.cpp和win_qextserialport.h 换为 posix_qextserialport.cpp和posix_qextserialport.h。

### 2.2 编译成动态库调用

    1. 下载源码,解压

    2. 运行qmake命令,生成makefile后使用make或nmake命令编译

    3. 使用时在工程文件中加入:

``` null
 CONFIG += extserialport // Qt4
```

    4. 使用

aa

### 2.3编译成静态库调用

    1. 在qextserialport.pro文件中加入

``` null
 CONFIG += qesp_static
```

    2. 运行qmake命令,生成makefile后使用make或nmake命令编译

    3. 使用时在工程文件中加入:

``` null
 CONFIG += extserialport //Qt4
```

### 2.4 构建文档

运行命令:

``` null
make docs //POSIX平台
```

## 3 简单使用

### 3.1 QextSerialEnumerator类

引自
[https://qextserialport.github.io/1.2/examples-enumerator-main-cpp.html](https://qextserialport.github.io/1.2/examples-enumerator-main-cpp.html)

``` C++
 #include "qextserialenumerator.h"

 #include <QtCore/QList>

 #include <QtCore/QDebug>

 int main()

 {

 QList<QextPortInfo> ports = QextSerialEnumerator::getPorts(); //获取到端口信息

 qDebug() << "List of ports:";

 foreach (QextPortInfo info, ports) {

 qDebug() << "port name:" << info.portName;

 qDebug() << "friendly name:" << info.friendName;

 qDebug() << "physical name:" << info.physName;

 qDebug() << "enumerator name:" << info.enumName;

 qDebug() << "vendor ID:" << info.vendorID;

 qDebug() << "product ID:" << info.productID;

 qDebug() << "===================================";

 }

 return 0;

}

```

### 3.2 QextSerialPort类

``` C++

//代码片段

 //构造QextSerialPort类

QextSerialPort *port = new QextSerialPort("COM4", QextSerialPort::EventDriven); port->open(QIODevice::ReadWrite ); //打开端口

 port->setBaudRate(BAUD9600); //设置波特率

 port->setFlowControl(FLOW_OFF); //设置流量控制

 port->setParity(PAR_NONE); //设置校验

 port->setDataBits(DATA_8); //设置数据位

 port->setStopBits(STOP_1); //设置停止位

 port->write("hello"); //向串口写入数据

port->close(); //关闭串口
```

## 4 注意事项

- QextSerialPort类所有成员列表:

[https://qextserialport.github.io/1.2/qextserialport-members.html](https://qextserialport.github.io/1.2/qextserialport-members.html)

- 串口设置时需要先将串口打开，然后将串口的设置参数传入。

- 包含两种轮询模式:

    QextSerialPort::Polling //异步读写
    QextSerialPort::EventDriven //同步读写

- 关于对不同波特率的支持,win平台和POSIX平台有所区别.详见:

[https://qextserialport.github.io/1.2/qextserialport.html#details](https://qextserialport.github.io/1.2/qextserialport.html#details)

- 数据位可设置为5, 6, 7,或8,但存在一些限制:

    5 data bits cannot be used with 2 stop bits.

    1.5 stop bits can only be used with 5 data bits.

    8 data bits cannot be used with space parity on POSIX systems.

- 校验位支持Space, Mark, None, Even, Odd.(其中Mark只能用于win平台)

- 停止位有1, 1.5, 2三种,但存在一些限制:

    2 stop bits cannot be used with 5 data bits.

    1.5 stop bits cannot be used with 6 or more data bits.

    POSIX does not support 1.5 stop bits.

- setTimeout(long millisec)函数POSIX平台和win平台上有不同的表现,该函数在QextSerialPort::EventDriven模式下不起作用.

- 可用PortSettings结构体定义串口类,该结构体定义如下:

``` C++
struct PortSettings

{

 BaudRateType BaudRate;

 DataBitsType DataBits;

 ParityType Parity;

 StopBitsType StopBits;

 FlowType FlowControl;

 long Timeout_Millisec;

};
```
