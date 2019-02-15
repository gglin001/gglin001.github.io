## 0
常用ss开代理，但由于ss是socks5协议的，偶尔会有些问题，polipo可以将socks5转换成http
## install
```
sudo apt install polipo
```
## configure
```
abc@kali:~/ss$ cat /etc/polipo/config
# This file only needs to list configuration variables that deviate
# from the default values.  See /usr/share/doc/polipo/examples/config.sample
# and "polipo -v" for variables you can tweak and further information.

logSyslog = true
logFile = /var/log/polipo/polipo.log
## ss config
socksParentProxy = "127.0.0.1:1080"
socksProxyType = socks5
```
默认代理端口为8123
