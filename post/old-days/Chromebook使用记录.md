Taobao买的Thinkpad 11e chromebook,评价:键盘还行吧,(比不上当下价格更低的Thinkpad x200,情理之中的事情),待机超强,电池健康80%,能干掉我周围的所有笔记本,当然,副作用就是性能孱弱.

## 开机,登录...
这个恐怕是所有用google产品的人的第一步难题,哈哈,也是走了许多弯路,解决方案如下
- 早期可以手机用fqrouter(donot remember)as a proxy server
- on line pac address,之前有个还能用,现在都挂了
- 用同一局域网的台式机开proxy,如wproxy等软件作代理,台式机需要vpn可连接到google
- 手机上有个server ultrama(忘了名字,想用的终归可以查得到),可以开代理,但不提供fq,配合shadowsocks可用,ss应该是需要全局代理
- 经测试,手机fq,再用数据线开usb共享不能用

## 开启开发模式
引用自贴吧：
>开发者模式 : 在关机状态下，按住Esc+F3+电源键，启动Chromebook，看到ChromeOS系统损坏的界面以后（顺带一提，按方向键可以切换成不同的语音；需要重装ChromeOS的话就在这个界面里插入ChromeOS恢复U盘）按Ctrl+D，系统提示是否确认要进入开发者模式，回车确认。然后等待系统重启，第一次重启会显示修复系统，耐心等待就可以了，从此系统就进入开发者模式。注意一旦开启开发者模式，开机界面都会显示一个警告界面。要么等待30秒后系统自动启动，要么按Ctrl+D跳过等待时间。切记不可以按空格键，否则ChromeOS就自动关闭开发者模式了。

## 安装各类插件
这个可以单独写一篇了,放个图在这

## 安装crouton cli
安装crouton
（https://github.com/dnschneid/crouton）
crosh下进入shell
解压crouton在installer目录下
```
sudo sh ./main.sh -r list
sudo sh ./main.sh -t list
sudo sh ./main.sh -r kali-rolling -t cli-extra -m http://mirrors.ustc.edu.cn/debian
```
安装cli,此时没有gui,只安装cli不需要fq

## 安装crouton gui
问题：audio模块需要fq下载

解决:在crouton下安装shadowsocks或者shadowsocks-libev,有sslocal,ss-local命令连接ss,下载相应audio文件,在crouton安装包下target目录下修改audio文件,把下载地址设为127.0.0.1:8888,可用插件web server开文件服务器下载,或者在crouton下安装nginx或者apache2,(需配置目录),run
```
sudo sh ./main.sh -r kali-rolling -t cli-extra,xiwi,xorg
#桌面环境
sudo sh ./main.sh -r kali-rolling -t cli-extra,xiwi,xorg,lxde
```
xiwi 需要配合crouton插件运行,会很爽,但是速度比纯xorg慢
## 使用crouton
in crosh 进入 shell
```
sudo enter-chroot
xiwi -t xterm
#需要安装相应软件
xiwi -t stratlxde
#启动桌面
```
直接启动桌面
```
sudo startlxde
```
enjoy
