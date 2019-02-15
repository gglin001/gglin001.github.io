## 问题
when u start into X envirement, 可以run 
`startx`
but u find that in 
`chrome`
cannot use ibus for chinese input(BTW, I use `ibus-rime`, It is really good) However, When u run 
`xinit` 
into X, ibus is OK (but WHY??)
sometimes, `xinit` returns false, message as:
```
...
cannot open /dev/tty0  // or /dev/tty*

```

## 解决方案
# A1
修改
```
/etc/X11/Xwrapper.config
```
add
```
needs_root_rights=yes
```

# A2
修改
 ```
/etc/X11/xinit/xserverrc  //for all users
```
or
```
$HOME/.xerverrc // for the $USER
```
to
```
...
exec /usr/bin/X -nolisten tcp "$@" vt$XDG_VTNR
```
In which `vt$XDG_VTNR` is the key to solve the problem.

## 效果
ok
