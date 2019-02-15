## install ss
```
apt search shadowsocks
shadowsocks/kali-rolling,kali-rolling,now 2.9.0-2 all [installed]
  Fast tunnel proxy that helps you bypass firewalls
shadowsocks-libev/kali-rolling,now 2.6.3+ds-3 amd64 [installed]
  lightweight and secure socks5 proxy
sudo apt install shadowsocks shadowsocks-libev
```
`shadowsocks-libev` is a c++ version of shadowsocks, may more faster than the python version
we got 2 command `ss-local`and `ss-server`
## set up a shadowsocks server
port:888888

## set up ss clients
configure file`s`
```
{       
        "server":"xx.xx.xx.xx",
        "server_port":xx,
        "password":"xxxx",
        "local_port":1080,
        "method":"aes-256-cfb"
}
```
boot file`start_s`
```
#!/bin/bash
# cd /home/abc
ss-local -c ~/s > ss-local.log 2>&1 &
echo "s-local starts"
```
## use kcptun
Download https://github.com/xtaci/kcptun/releases
`server.json`
```
{
        "listen": "xx.xx.xx.xx:28800",
        "target": "xx.xx.xx.xx:888888",
        "key": "xxxx",
        "crypt": "aes",
        "mode": "fast2",
        "autoexpire": 60
}
```
`start_server`
```
#!/bin/bash
cd /root/kcptun
./kcptun_server -c /root/kcptun/server.json 
echo "kcptun starts"
```
`client.json `
```
{
    "localaddr": ":28800",
    "remoteaddr": "xx.xx.xx.xx:28800",
    "key": "xxxx",
    "crypt": "aes",
    "mode": "fast2",
    "autoexpire": 60
}
```
`start_client`
```
#!/bin/bash
cd /home/abc/kcptun
./kcp_client -c ~/client.json > kcptun.log 2>&1 &
echo "kcptun_client starts"
```
need new ss-local file
`ss`
```
{       
        "server":"127.0.0.1",
        "server_port":28800,
        "password":"ss`s passwd",
        "local_port":1080,
        "method":"aes-256-cfb"
}
```
` start_ss`
```
#!/bin/bash
#cd /home/abc/ss
ss-local -c ~/ss > ss-local.log 2>&1 &
echo "ss-local srtarts"
#cd /home/abc/ss/kcptun
./kcp_client -c ~/client.json > kcptun.log 2>&1 &
echo "kcptun_client starts"
```
note:`xx.xx.xx.xx` is your vps ip
ok ! now u have a socks5 proxy address:`127.0.0.1:1080`






