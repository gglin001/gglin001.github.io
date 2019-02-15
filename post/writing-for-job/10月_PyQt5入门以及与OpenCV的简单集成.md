## PyQt5与OpenCV简介

### PyQt

PyQt是Python语言的GUI编程解决方案之一。可以用来代替Python内置的Tkinter。其它替代者还有PyGTK、wxPython等。与Qt一样，PyQt是一个自由软件。

PyQt的开发者是英国的“Riverbank Computing”公司。它提供了GPL与商业协议两种授权方式，因此它可以免费地用于自由软件的开发。PyQt可以运行于Microsoft Windows、Mac OS X、Linux以及Unix的多数变种上。

pyqt5是一套Python绑定QT5应用的框架。它可用于Python 2和3。pyqt5的官方网站
[http://www.riverbankcomputing.co.uk/news](http://www.riverbankcomputing.co.uk/news)

pyqt5做为Python的一个模块，它有620多个类和6000个函数和方法。
pyqt5的类别分为几个模块，包括以下：

QtCore
QtGui
QtWidgets
QtMultimedia
QtBluetooth
QtNetwork
QtPositioning
Enginio
QtWebSockets
QtWebKit
QtWebKitWidgets
QtXml
QtSvg
QtSql
QtTest

QtCore:包含了核心的非GUI功能。此模块用于处理时间、文件和目录、各种数据类型、流、URL、MIME类型、线程或进程。
QtGui包含类窗口系统集成、事件处理、二维图形、基本成像、字体和文本。
qtwidgets模块包含创造经典桌面风格的用户界面提供了一套UI元素的类。
QtMultimedia包含的类来处理多媒体内容和API来访问相机和收音机的功能。
Qtbluetooth模块包含类的扫描设备和连接并与他们互动。描述模块包含了网络编程的类。这些类便于TCP和IP和UDP客户端和服务器的编码，使网络编程更容易和更便携。
Qtpositioning包含类的利用各种可能的来源，确定位置，包括卫星、Wi-Fi、或一个文本文件。
Enginio模块实现了客户端库访问Qt云服务托管的应用程序运行时。
Qtwebsockets模块包含实现WebSocket协议类。
QtWebKit包含一个基于Webkit2图书馆Web浏览器实现类。
Qtwebkitwidgets包含的类的基础webkit1一用于qtwidgets应用Web浏览器的实现。
QtXml包含与XML文件的类。这个模块为SAX和DOM API提供了实现。
QtSvg模块提供了显示SVG文件内容的类。可伸缩矢量图形（SVG）是一种描述二维图形和图形应用的语言。
QtSql模块提供操作数据库的类。
QtTest包含的功能，使pyqt5应用程序的单元测试

PyQt5不兼容PyQt4。PyQt5有一些巨大的改进。但是，迁移并不是很难，两者的区别如下：
重新组合模块，一些模块已经被废弃(QtScript)，有些被分为两个子模块(QtGui, QtWebKit)。
添加了新的模块，比如QtBluetooth, QtPositioning，和Enginio。
废弃了SINGAL()和SLOT()的调用方式，使用了新的信号和xx处理方式。
不再支持所有被标记为废弃的或不建议使用的Qt API

OpenCV的全称是Open Source Computer Vision Library，是一个跨平台的计算机视觉库。OpenCV是由英特尔公司发起并参与开发，以BSD许可证授权发行，可以在商业和研究领域中免费使用。OpenCV可用于开发实时的图像处理、计算机视觉以及模式识别程序。该程序库也可以使用英特尔公司的IPP进行加速处理。

## PyQt5 demo 3个

### demo1, 简单的GUI

``` python
#!/usr/bin/python3
# -*- coding: utf-8 -*-

"""
PyQt5 demo 1
"""

import sys
from PyQt5.QtWidgets import QApplication, QWidget, QPushButton

# demo1继承自QWidget
class demo1(QWidget):

    # 构造函数
    def __init__(self):
        # 父类初始化
        super().__init__()
        self.init_show()

    def init_show(self):
        btn = QPushButton('Hello, PyQt5', self)
        btn.move(300, 200)
        btn.resize(100, 40)

        self.setWindowTitle('demo1')
        self.resize(800, 600)

# 运行
if __name__ == '__main__':
    app = QApplication(sys.argv)
    w = demo1()
    w.show()
    app.exec()

```

### demo2, 简单的signal与slot

``` python

#!/usr/bin/python3
# -*- coding: utf-8 -*-

"""
simple signal
"""
import sys
from PyQt5.QtWidgets import QApplication, QDialog, QPushButton

app = QApplication(sys.argv)
dlg = QDialog()
dlg.setWindowTitle('just close it')
dlg.resize(300, 200)

btn = QPushButton(dlg)
btn.resize(100, 50)
btn.setText('click it!')
btn.move(100, 100)

# 将btn的clicked信号与dlg的close槽连接
btn.clicked.connect(dlg.close)

dlg.show()
sys.exit(app.exec())
```

### demo3, 简单的串口通信

``` python

#!/usr/bin/python3
# -*- coding: utf-8 -*-

"""
PyQt5 demo 2
"""
# 导入QSerialPort库
from PyQt5.QtSerialPort import QSerialPort
from PyQt5.QtCore import QIODevice, QByteArray

port = QSerialPort('COM1')

# QSerialPort的一些通信设定
port.setBaudRate(QSerialPort.Baud9600)
port.setFlowControl(QSerialPort.FlowControl(0))
port.setParity(QSerialPort.Parity(7))
port.setStopBits(QSerialPort.StopBits(1))

# 实际代码中应判断是否打开成功
port.open(QIODevice.ReadWrite)

byte = QByteArray()
byte.resize(6)
byte.fill('0')

port.write(byte)
port.flush()
port.close()
```

## OpenCV demo

### demo1, 简单读取一个image

``` python
import cv2

"""
simple opencv snippet
"""
# 读取图像
img = cv2.imread('D:/wuhan.jpg')

# 显示图像
cv2.imshow('wuhan', img)

# 等待键盘输入事件
cv2.waitKey(0)

#销毁所有window
cv2.destroyAllWindows()
```

### demo2, 简单的图像处理

``` python
import cv2

"""
simple opencv snippet 02
"""
# 读取图像
img = cv2.imread('D:/lena.jpg', 0)

# 对图像做直方图均衡处理
equ = cv2.equalizeHist(img)

# 采用cancy算子进行边缘检测
edge = cv2.Canny(img, 50, 50)

# 显示图像
cv2.imshow('img', img)
cv2.imshow('equ', equ)
cv2.imshow('edge', edge)

cv2.waitKey(0)
cv2.destroyAllWindows()

```

![simple opencv snippet 02](https://upload-images.jianshu.io/upload_images/1711028-5096c1e3e07830fe.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


## PyQt5与OpenCV的简单集成

``` python
#!/usr/bin/python3
# -*- coding: utf-8 -*-

import sys
import cv2 as cv
import numpy as np
from PyQt5.QtGui import QImage, QPixmap
from PyQt5.QtWidgets import (QApplication, QDialog, QFileDialog, QGridLayout,
                             QLabel, QPushButton)


class win(QDialog):
    def __init__(self):

        # 初始化一个img的ndarray, 用于存储图像
        self.img = np.ndarray(())

        super().__init__()
        self.initUI()

    def initUI(self):
        self.resize(400, 300)
        self.btnOpen = QPushButton('Open', self)
        self.btnSave = QPushButton('Save', self)
        self.btnProcess = QPushButton('Process', self)
        self.btnQuit = QPushButton('Quit', self)
        self.label = QLabel()

        # 布局设定
        layout = QGridLayout(self)
        layout.addWidget(self.label, 0, 1, 3, 4)
        layout.addWidget(self.btnOpen, 4, 1, 1, 1)
        layout.addWidget(self.btnSave, 4, 2, 1, 1)
        layout.addWidget(self.btnProcess, 4, 3, 1, 1)
        layout.addWidget(self.btnQuit, 4, 4, 1, 1)

        # 信号与槽连接, PyQt5与Qt5相同, 信号可绑定普通成员函数
        self.btnOpen.clicked.connect(self.openSlot)
        self.btnSave.clicked.connect(self.saveSlot)
        self.btnProcess.clicked.connect(self.processSlot)
        self.btnQuit.clicked.connect(self.close)

    def openSlot(self):
        # 调用打开文件diglog
        fileName, tmp = QFileDialog.getOpenFileName(
            self, 'Open Image', './__data', '*.png *.jpg *.bmp')

        if fileName is '':
            return

        # 采用opencv函数读取数据
        self.img = cv.imread(fileName, -1)

        if self.img.size == 1:
            return

        self.refreshShow()

    def saveSlot(self):
        # 调用存储文件dialog
        fileName, tmp = QFileDialog.getSaveFileName(
            self, 'Save Image', './__data', '*.png *.jpg *.bmp', '*.png')

        if fileName is '':
            return
        if self.img.size == 1:
            return

        # 调用opencv写入图像
        cv.imwrite(fileName, self.img)

    def processSlot(self):
        if self.img.size == 1:
            return

        # 对图像做模糊处理, 窗口设定为5x5
        self.img = cv.blur(self.img, (5, 5))

        self.refreshShow()

    def refreshShow(self):
        # 提取图像的尺寸和通道, 用于将opencv下的image转换成Qimage
        height, width, channel = self.img.shape
        bytesPerLine = 3 * width
        self.qImg = QImage(self.img.data, width, height, bytesPerLine,
                           QImage.Format_RGB888).rgbSwapped()

        # 将Qimage显示出来
        self.label.setPixmap(QPixmap.fromImage(self.qImg))


if __name__ == '__main__':
    a = QApplication(sys.argv)
    w = win()
    w.show()
    sys.exit(a.exec_())
```
![PyQt5与OpenCV的简单集成](https://upload-images.jianshu.io/upload_images/1711028-0934f0fc0d9c0aa0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 结语

PyQt将Qt强大的界面开发功能带入到Python语言中,结合Python语言的特性,可方便快捷地实现编程人员的想法,更可以结合OpenCV库包含的种种算法实现对图像和视频的处理.
