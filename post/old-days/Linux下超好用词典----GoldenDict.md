## install
```
abc@kali:~$ apt search goldendict
Sorting... Done
Full Text Search... Done
goldendict/kali-rolling,now 1.5.0~git20160508.g92b5485-1.1+b2 amd64 [installed]
  feature-rich dictionary lookup program

goldendict-wordnet/kali-rolling,kali-rolling,now 1:3.0-33 all [installed]
  electronic lexical database of English language (goldendict)
```
`goldendict` 是本体,`goldendict-wordnet`是一个en-en离线词典,按需安装
```
sudo apt install goldendict goldendict-wordnet
```
## set up 
设置可调节语言为简中
在词典-网站内添加
有道源
```
http://dict.youdao.com/search?q=%GDWORD%&ue=utf8
```
尝试过google的,没搞定
自带英文维基,可用
## 离线词典
#### 下载
http://download.huzheng.org/zh_CN/
感谢该网站!!
#### 安装
解压后
在词典-文件添加路径即可
令可单独下载构词法文件,安装也很简单
可以设置屏幕取词,方便的不要不要的
## 后记

尝试使用bing搜索的dic搜索,效果不错,网络词典添加地址
```
https://cn.bing.com/dict/search?q=%GDWORD%
```
