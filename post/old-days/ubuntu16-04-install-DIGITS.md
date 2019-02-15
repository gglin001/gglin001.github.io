## 0x01 What Is DIGITS
> Deep Learning GPU Training System [https://developer.nvidia.com/digits](https://developer.nvidia.com/digits)

Github address: https://github.com/NVIDIA/DIGITS
## 0x02 install 
存在多种安装方法：
1. 一步步编译：Nvidia driver+cuda(Optional)+caffe([BVLC/caffe](https://github.com/BVLC/caffe)
 or  [NVIDIA/caffe](https://github.com/NVIDIA/caffe))+DIGITS+tensorflow(Optional)

2. For Ubuntu14.04 and Ubuntu16.04, Nvidia提供了仓库
[cuda/repos](http://developer.download.nvidia.com/compute/cuda/repos/)
and
[machine-learning/repos](http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1604/x86_64/)
install *repo*.deb, add to apt source list

3. Use Docker *recommand way*

官方参考：
https://github.com/NVIDIA/DIGITS/blob/master/docs/BuildDigits.md
测试机器：
```
~  uname -a
Linux ubuntu-server 4.13.0-36-generic #40~16.04.1-Ubuntu SMP Fri Feb 16 23:25:58 UTC 2018 x86_64 x86_64 x86_64 GNU/Linux
---
GPU：amd hd7850
```

由于未知的问题（疑因cuda驱动），安装成功后不能使用caffe，tensorflow可用
这里采用nvidia官方的仓库进行安装，步骤如下：
1. 添加deb源
2. apt安装
3. 安装一些依赖
4. 成功

## 0x03 测试：
