最近转到i3wm桌面下, 发现调用xfce4-terminal有些慢,索性卸载掉一切所谓高级的终端,使用xterm,其实这个才是更牛的家伙.
## 安装
```
sudo apt install xterm
```
in i3-wm, you can type `modx+enter` 进入终端,会有一个默认的终端排序,但是删除了其他终端之后就只有xterm可以用来了

## 配置
其实主要是字体的问题,因为默认的字体太小了,而且中文显示有问题,这里有两种方式配置xerm
- ~/.Xresources或者~/.Xdefault文件,其实都是一样的,因为做了修改后需要run
```
xrdb -merge ~/.Xresources
```
发现这样子在系统重启后设置不能保存,因此选择下一种
- /etc/X11/app-defaults/XTerm
at the last, add
```
xterm*ScrollBar: true
xterm*faceName: DejaVu Sans Mono Book
xterm*faceNameDoublesize: WenQuanYi Micro Hei
xterm*faceSize: 11
xterm*allowBoldFonts: false
xterm*foreground: grey100 
xterm*background: rgb:30/10/10
!xterm*background: black
```
rgb说明可见`cat /etc/X11/rgb.txt` 
这样,所有用户都可以采用修改后的配置了, 需要注意的是,要install ttfs

## 使用
 ctrl+鼠标三键出现设置菜单,左键双击选中后,用右键点击其他区域,自动扩展选中,这个太吊.
ibus无法在xterm输入中文

## 效果
