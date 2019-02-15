最近碰上了这个问题，很奇特，稍微修改下配置文件就可以了。

##0x01
~/.xinitrc
```
#!/bin/sh

# /etc/X11/xinit/xinitrc
#
# global xinitrc file, used by all X sessions started by xinit (startx)

# invoke global X session script
#. /etc/X11/Xsession
exec i3

```
## 0x02
~/.xserverrc
```
#!/bin/sh

exec /usr/bin/Xorg -nolisten tcp "$@" vt$XDG_VTNR 
```
## 0x03
~/.config/i3/config
add
```
## input method
###
exec --no-startup-id ibus-daemon -xdr
####
exec --no-startup-id export GTK_IM_MODULE=ibus
exec --no-startup-id export XMODIFIERS=@im=ibus
exec --no-startup-id export QT_IM_MODULE=ibus

##########
# for sound control  
bindsym XF86AudioRaiseVolume exec amixer set Master playback 5000+  
bindsym XF86AudioLowerVolume exec amixer set Master playback 5000-  
bindsym XF86AudioMute exec amixer set Master toggle
###################
#exec --no-startup-id feh --bg-scale /home/abc/.config/i3/dream.png
exec --no-startup-id feh --bg-scale /home/abc/.config/i3/moon.jpeg

```
reboot x window , ok
