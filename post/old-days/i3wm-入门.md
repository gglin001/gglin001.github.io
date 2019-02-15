## 安装
所用Linux版本为kali-rolling，直接安装
``` 
sudo apt install i3 
```

## 设置为xinit的启动对像
~/.xserverrc
```
#!/bin/sh
exec /usr/bin/Xorg -nolisten tcp "$@" vt$XDG_VTNR
```
～/.xinintrc
```
#!/bin/sh
# /etc/X11/xinit/xinitrc
# global xinitrc file, used by all X sessions started by xinit (startx)
# invoke global X session script
#. /etc/X11/Xsession
######################################
exec i3
```
键入
```
startx
```
or 
```
xinit 
```
可进入i3
注：这里有个奇怪的问题，sartx进入后chrome不能用中文，xinit进入时则可以使用中文。

## i3配置
~/.config/i3/config 
加入
```
##################################
exec --no-startup-id export GTK_IM_MODULE=ibus
exec --no-startup-id export XMODIFIERS=@im=ibus
exec --no-startup-id export QT_IM_MODULE=ibus
###########################
exec --no-startup-id feh --bg-scale /home/abc/.config/i3/bgp.jpg
exec --no-startup-id ibus-daemon --xim -d -r
```
注：1.这里使用ibus输入法. 2.feh软件用来设置桌面

~/.config/i3status/config
加入温度显示
```
#order += "ipv6"
order += "cpu_temperature 0"
order += "disk /"
order += "wireless _first_"
order += "ethernet _first_"
order += "battery all"
order += "load"
order += "tztime local"
cpu_temperature 0 {
                   format = "T: %degrees °C"
                   path = "/sys/devices/platform/coretemp.0/hwmon/hwmon2/temp2_input"
           }
```
## 安装配套应用
dmenu（应用菜单）
xbacklight（亮度调节）
feh（壁纸）
conky（显示系统信息）
以上未完全测试

效果：
![desktop](http://upload-images.jianshu.io/upload_images/1711028-d5d035a8837dd604.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## i3wm菜单提速
 抛弃
```
i3-dmenu-desktop
```
投入到
```
j4-demu-desktop
```
速度超快

## i3wm 调节音量
### Configure
i3wm，设置调节音量的快捷键
~/.config/i3/config
添加
```
# for sound control  
bindsym XF86AudioRaiseVolume exec amixer set Master playback 5+  
bindsym XF86AudioLowerVolume exec amixer set Master playback 5-  
bindsym XF86AudioMute exec amixer set Master toggle  
```
x200上静音键可用,调节大小的按键没有作用

### 修改
原来是数值太小,修改为
```
# for sound control  
bindsym XF86AudioRaiseVolume exec amixer set Master playback 5000+  
bindsym XF86AudioLowerVolume exec amixer set Master playback 5000-  
bindsym XF86AudioMute exec amixer set Master toggle  
```
可以使用, 可用
```
amixer
```
查看设置的值

## i3wm 搭配lxpanel
在i3配置文件中加入
```
exec --no-startup-id lxpanel
```
可以使用lxpanel,调节位置到top,用者也不错

##i3wm 关闭焦点鼠标跟随

```
focus_follows_mouse no
```
reference:
https://i3wm.org/docs/userguide.html#_focus_follows_mouse
