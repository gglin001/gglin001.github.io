## 前言
本人笔记本用Kali Linux，因课程需要，要在Linux下运行Labview，找到了2010的iso，但只支持redhat系列的发行版，用rpm转化deb的方案不可行，尝试了在virtualbox下运行winxp跑labview2012和fedora跑labview2010，但机器太老了，不流畅，想到了利用docker跑gui的方式，尝试了下，感觉不错。

## install docker
download frome docker.io or ustc mirror 
get docker_ce.deb 
```
sudo dpkg -i docker_ce.deb
```
## install docker container
```
abc@kali:~$ docker search fedora32
NAME                             DESCRIPTION                        STARS     OFFICIAL   AUTOMATED
hugodby/fedora32                 Images of fedora i386 / 32 bits    0                    
savoirfairelinux/ring-fedora32   Images of fedora i386 / 32 bits    0                    
abc@kali:~$ docker pull hugodby/fedora32
...
```
plug in usb soundcard as `/dev/dsp1`,then 
mount labview.iso to `host:/home/abc/labview/`
```
docker run -ti -v /tmp/.X11-unix:/tmp/.X11-unix -v /home/abc/labview:/mnt  -e DISPLAY=$DISPLAY --device /dev/dsp1  hugodby/fedora32 bash
```
install labview in docker `/mnt`
## run labview
in docker container fedora32
```
labview &
```
提示缺乏组件，用yum命令安装，OK！

注：这里可能会出现主机上没有`/dev/dsp*`,用下面的命令解决
```
apt install alsa-oss
sudo modprobe snd_pcm_oss
sudo modprobe snd_mixer_oss 
```
or add to `/etc/modules`(`/etc/modules-load.d/modules.conf `)
```
abc@kali:~$ cat  /etc/modules-load.d/modules.conf 
# /etc/modules: kernel modules to load at boot time.
# This file contains the names of kernel modules that should be loaded
# at boot time, one per line. Lines beginning with "#" are ignored.
snd_pcm_oss
snd_mixer_oss
```
若提示无法连接xserver,在主机上运行
```
xhost+
```

效果:

![labview on docker](http://upload-images.jianshu.io/upload_images/1711028-5ed7379105aa556e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
