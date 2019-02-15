## final solution
first install lxde-core, the lightest one
```
sudo apt install lxde-core
``` 
then u can step into lxde, just run:
```
startx
```
or
```
xinit
```

then maybe u wang to use ibus-*(for example I use ibus-rime)
u need to install some softwares like
```
sudo apt install ibus ibus-rime ibus-gtk ibus-gtk3 ibus-qt4 
```
well, u are very happy, because u can input chinese in your Linux OS
even in Chrome or Chromium-browser
But when u want to switch to one more light WM, just like ##i3-wm##
u just find that there are some unhappy issues...
when u cannot input chinese(use ibus) in your modern Broswers like Chrome, but u can use it in lxde, then u can borrow somethings frome LXDE, not just input essue.
## Replace
 just edit the startup file of LXDE
```
sudo vim `which startlxde`
```
just replace the last line:
```
# Start the LXDE session
exec /usr/bin/lxsession -s LXDE -e LXDE
```
to
```
# Start the i3 session
exec i3
```
## bingo
 







