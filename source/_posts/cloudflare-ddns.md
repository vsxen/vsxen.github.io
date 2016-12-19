---
title: cloudflare动态DDNS
date: 2016-12-18 08:54:05
categories:
tags:
---


1、Linux系统支持shell脚本。
2、注册一个cloudflare账户并在账户设置页面取得Global API Key。
3、添加一个域名并设置好解析。
3、设置以下脚本。

1、获得记录ID

curl https://www.cloudflare.com/api_json.html -d 'a=rec_load_all' \
  -d 'tkn=CloudFlare_API_Key' \
  -d 'email=CloudFlare_Email_Address' \
  -d 'z=holin.net'
把返回的数据使用json解析后方便查看
或者使用在线解析工具http://json.parser.online.fr/ 解析查看

解析后大概是这样

{
"rec_id":"499268485",
"rec_hash":"ac4735d1f3443e8b85efef54ad8bd8b6",
"zone_name":"holin.net",
"name":"test.holin.net",
"display_name":"test",
"type":"A",
"prio":null,
"content":"1.1.1.1",
"display_content":"1.1.1.1",
"ttl":"1",
"ttl_ceil":86400,
"ssl_id":"2133576",
"ssl_status":"V",
"ssl_expires_on":null,
"auto_ttl":1,
"service_mode":"0",
"props":{
"proxiable":1,
"cloud_on":0,
"cf_open":1,
"vanity_lock":0,
"ssl":1,
"expired_ssl":0,
"expiring_ssl":0,
"pending_ssl":0
}
}
添加动态ip脚本

mkdir -p 
vi /scripts/dyndns.sh
写以入下内容

#!/bin/sh
mkdir -p /var/tmp/
NEW_IP=`wget -O - -q http://api.holin.net/getip/`
CURRENT_IP=`cat /var/tmp/current_ip.txt`

if [ "$NEW_IP" = "$CURRENT_IP" ]
then
        echo "No Change in IP Adddress"
else
        curl https://www.cloudflare.com/api_json.html \
          -d 'a=rec_edit' \
          -d 'tkn=CloudFlare_API_Key' \
          -d 'email=CloudFlare_Email_Address' \
          -d 'z=techjourney.net' \
          -d 'id=CloudFlare_Record_ID' \
          -d 'type=CloudFlare_Record_Type' \
          -d 'name=CloudFlare_Record_Name' \
          -d 'ttl=1' \
          -d "content=$NEW_IP"
        echo $NEW_IP > /var/tmp/current_ip.txt
fi
上面需要修改相信的参数

1、tkn为cloudflare账户并在账户设置页面取得Global API Key。
2、email为你cloudflare账户的邮箱。
3、z为你的域名
4、id为上步获取到的”rec_id”:”你的ID”。
5、type一般为A。
6、name为您的主机名如果是主域名一般为@或者www，我这测试为test即test.holin.net
保存好后设置一下权限

chmod 755 /scripts/dyndns.sh
现在设置定时检测IP变化后更新

进入cron任务设置

crontab -e
添加一行任务30秒检测一次，如果ip发生变化就更新解析记录。

* * * * * sleep 30; /bin/date >>/scripts/dyndns.sh
你要以运行以下命令来监控脚本运行情况

tail -f /var/log/cron


参考
https://zh.holin.net/topic/02163858520/
http://lesca.me/archives/ddns-with-cloudflare-on-windows.html