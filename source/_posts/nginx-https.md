---
title: nginx配置https，Let'sEncrypt证书
date: 2016-08-20 10:13:27
categories: Linux
tags: 
---

https的好处，不会被运营商插入广告，网站更加安全，chrome下有绿锁，高大上。



## 安装certbot
certbot是Let's官方推荐使用的证书制作工具
```
wget https://dl.eff.org/certbot-auto#下载
chmod a+x ./certbot-auto#加权限
./certbot-auto -n#安装依赖
./certbot-auto certonly --standalone --email test@example.com -d www.test.site #单域名单证书
./certbot-auto certonly --standalone --email test@example.com -d www.test.site -d blog.test.site#多域名单证书
```
`需要注意的是，验证的时候保证80/443端口对外开放，且不被占用，如果这些端口实现被nginx占用，先停掉nginx`

## 查看证书
`ls /etc/letsencrypt/live/`
如果需要备份到本地可以使用scp命令
`scp -r root@ip:/etc/letsencrypt /Users/test`

## 配置nginx
在

> server {
        server_name example.com;
        listen 443 ssl;
        省略
>}

后加上
```
ssl_certificate /etc/letsencrypt/live/www.test.site/fullchain.pem;
ssl_certificate_key /etc/letsencrypt/live/www.test.site/privkey.pem;
ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
```

##  自动续签
证书的默认有效期是三个月，所有三个月后需要重新签署证书
可以在crontab加入如下规则`0 3 */5 * * /root/certbot-auto renew`这样每五天就会执行一次续期操作。当然时间也可以自行进行调整，建议别太频繁，因为他们都有请求次数的限制。


参考(http://blog.just4fun.site/https-note.html)
参考(http://www.vpser.net/build/letsencrypt-certbot.html#comment-103155)