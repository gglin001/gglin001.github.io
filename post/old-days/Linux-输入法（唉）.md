很久就发现所用ibus在wps、retext等qt应用不能使用，今天特意研究下能否解决，结果，呵呵
## ibus安装
```
sudo apt install ibus ibus-gtk ibus-gtk3 ibus-qt4 ibus-sunpinyin
```
run`im-config`设置为ibus，gtk应用没有问题
## qt4的设置
```
sudo apt install qt4-qtconfig
```
run`qtconfig-qt4`可以设置qt4应用的输入法为ibus，然而，并没有什么卵用，依然不能使用
## 00
有人说是qtx下plugins文件夹的一个动态库的问题，搞了搞，好像只能解决qt开发时的输入问题
## 思路
之前用lxde桌面时貌似wps是可以用ibus输入中文的，问题的根源应该还是环境的问题
已设置
```
## i3wm配置文件
## input method
###
exec --no-startup-id ibus-daemon -xdr
####
exec --no-startup-id export GTK_IM_MODULE=ibus
exec --no-startup-id export XMODIFIERS=@im=ibus
exec --no-startup-id export QT_IM_MODULE=ibus
```
不知何解，还是继续用着英文输入吧
## 更新，在wps、wpp、ed执行的脚本开始处加入
```
export GTK_IM_MODULE=ibus
export XMODIFIERS=@im=ibus
export QT_IM_MODULE=ibus
```
即可在wps中使用ibus-pinyin
