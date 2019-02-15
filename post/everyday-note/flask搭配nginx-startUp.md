## needed 
flask
```
pip install flask
```
uwsgi
```
pip install uwsgi
```
nginx
```
# see
https://docs.nginx.com/nginx/admin-guide/installing-nginx/installing-nginx-open-source/ 
```

## configure files
file tree
```
~/app1/
├── app1.py
└── uwsgi.ini

/etc/nginx/sites-enabled/
└── app1.conf -> /etc/nginx/sites-available/app1.conf

```

app1.py
```
from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello():
        return "<h1 style='color:blue'>Hello There!</h1>"

@app.route("/start")
def start():
    return "start"

if __name__ == "__main__":
    app.run(host='0.0.0.0')
```

uwsgi.ini
```
[uwsgi]
module = app1:app

master = true
processes = 3

socket = 127.0.0.1:10001
chmod-socket = 660
vacuum = true
die-on-term = true

uid = www-data
gid = www-data
```

app1.conf
```
server{
        listen 80;

        location / {
                include uwsgi_params;
                uwsgi_pass 127.0.0.1:10001;
        }
}
```

/etc/nginx/nginx.conf
```
...
http {
        ...
        include /etc/nginx/sites-enabled/*;
}
```

## run
start nginx
```
# run nginx test
sudo nginx -t

# for systemd based
sudo systemctl start nginx
```

start uwsgi
```
uwsgi --ini ~/app1/uwsgi.ini
```

当然也可以做成 systemd unit file, 不赘述

##  result
![bare ip address](https://upload-images.jianshu.io/upload_images/1711028-93db06c528b35c20.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![ip/start](https://upload-images.jianshu.io/upload_images/1711028-d6973f89efa05b5d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## attention
在测试过程中遇到了一个麻烦, uwsgi 老是出现奇怪的错误,检查一番后发现是由于采用了 pyenv 下 python 环境所致,重新采用系统的 python 环境(或通过 virtualenv 构建的环境)即可正常使用.

