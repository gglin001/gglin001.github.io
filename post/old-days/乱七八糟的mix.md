## GET POST... in shell
just install libwww-perl package
```
 sudo apt install libwww-perl
```
U can use GET in shell for HTTP


## linux下Java程序字体美化
In
```
~/.bashrc
```
add 
```
-Dawt.useSystemAAFontSettings=on
```

## Nutstore Startup
startup:
```
sh -c "nohup ~/.nutstore/dist/bin/nutstore-pydaemon.py >/dev/null 2>&1 &"
```

## glxgears 老是60
In terminal run:
```
vblank_mode=0 glxgears 
```
## opencv conpile Mat fail
When conpile, output error:

```
/tmp/ccoaA7tl.o: In function `cv::Mat::~Mat()':
test1.cpp:(.text._ZN2cv3MatD2Ev[_ZN2cv3MatD5Ev]+0x39): undefined reference to `cv::fastFree(void*)'
/tmp/ccoaA7tl.o: In function `cv::Mat::release()':
test1.cpp:(.text._ZN2cv3Mat7releaseEv[_ZN2cv3Mat7releaseEv]+0x47): undefined reference to `cv::Mat::deallocate()'
collect2: error: ld returned 1 exit status
```

do

```
g++ `pkg-config --cflags opencv` test1.cpp `pkg-config --libs opencv`
```

## underscore is not displayed in URxvt terminal
添加设置:

``` shell
URxvt.lineSpace: 1
```

## 解决/lib/libc.so.6: not found  
For 64 bit:
```
sudo ln -s /lib64/x86_64-linux-gnu/libc-2.13.so /lib64/libc.so.6   
```
For 32 bit:
```
sudo ln -s /lib/i386-linux-gnu/libc-2.13.so /lib/libc.so.6 
```
