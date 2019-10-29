# nginx 反向代理

```
首先在nginx.conf中定义自定义配置文件目录（eg:/usr/local/nginx/server/*.conf）
意思是在server目录下新建的.conf文件为你的配置文件
```

## 需求

> 有个服务端和后台管理端，在本地情况下分别需要配置域名映射

### 比如（以 node 服务来说）服务端起了个服务为：127.0.0.1:5000，后台管理端起了个服务为 127.0.0.1:3000。现在要分别为他们配置域名为：api.wei.top 和 m.wei.com。

配置方式如下:

> 首先在之前说的 server 目录下新建一个 cast.conf(名字可自己定义)，配置内容

```
server {
    listen       80;
    server_name api.wei.top;
    charset utf-8;

    access_log  /var/log/nginx/pod-access.log;
    error_log   /var/log/nginx/pod-error.log;

    location / {
        proxy_pass   http://server5000;
    }
}

server {
  listen      80;
  server_name m.wei.com;
  charset utf-8;
  access_log  /var/log/nginx/pod-access.log;
  error_log   /var/log/nginx/pod-error.log;

  location / {
    proxy_pass http://server3000;
  }

}

upstream server3000 {

  server 127.0.0.1:3000;
}

upstream server5000 {

  server 127.0.0.1:5000;
}
```

这样就完成了反向代理。

### 现在需求又有变动，对服务端增加 https，首先要生成 ssl_certificate 和 ssl_certificate_key，引入到配置中即可，具体配置如下：

```
server {
    listen      443 ssl ;
    listen       80;
    server_name api.wei.top;
    charset utf-8;

    ssl_certificate    server.crt;
    ssl_certificate_key server.key;
    ssl_protocols       TLSv1 TLSv1.1 TLSv1.2;
    ssl_prefer_server_ciphers on;

    keepalive_timeout   5m;

    access_log  /var/log/nginx/pod-access.log;
    error_log   /var/log/nginx/pod-error.log;

    location / {
        proxy_pass   http://server5000;
    }
}

server {
  listen      80;
  server_name m.wei.com;
  charset utf-8;
  access_log  /var/log/nginx/pod-access.log;
  error_log   /var/log/nginx/pod-error.log;

  location / {
    proxy_pass http://server3000;
  }

}

upstream server3000 {

  server 127.0.0.1:3000;
}

upstream server5000 {

  server 127.0.0.1:5000;
}
```
