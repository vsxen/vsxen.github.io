---
title: 用ngrok刺破内网，开启本地调试
date: 2016-10-18 10:44:33
categories: Linux
tags:
---
ngrok是一个内网映射工具，可以给没有分配公网ip的电脑提供外部访问，可以用于开我的世界私服，或者远程登录家里的电脑。1.x版本开源，2.x之后不再开源。
本文用的是qydev.com,对应的ngrok版本是1.x,和2.0之后有一定的区别，不能通用，下面介绍下使用方法。
## 下载
下载ngrok的二进制文件，网站提供的都有，直接解压就行。
## 命令
```
./ngrok  help
Options:
  -authtoken string（认证，可选）
    	Authentication token for identifying an ngrok.com account
  -config string  （指定配置文件位置）
    	Path to ngrok configuration file. (default: $HOME/.ngrok)
  -hostname string （使用自己的域名首先配置好CNAME）
    	Request a custom hostname from the ngrok server. (HTTP only) (requires CNAME of your DNS)
  -httpauth string
    	username:password HTTP basic auth creds protecting the public tunnel endpoint
  -log string  （日志 感觉我用不到）
    	Write log messages to this file. 'stdout' and 'none' have special meanings (default "none")
  -log-level string （同上）
    	The level of messages to log. One of: DEBUG, INFO, WARNING, ERROR (default "DEBUG")
  -proto string  （协议类型）
    	The protocol of the traffic over the tunnel {'http', 'https', 'tcp'} (default: 'http+https') (default "http+https")
  -subdomain string （指定域名前缀）
    	Request a custom subdomain from the ngrok server. (HTTP only)

Examples:
	ngrok 80
	ngrok -subdomain=example 8080
	ngrok -proto=tcp 22
	ngrok -hostname="example.com" -httpauth="user:password" 10.0.0.1


Advanced usage: ngrok [OPTIONS] <command> [command args] [...]
Commands:
	ngrok start [tunnel] [...]    Start tunnels by name from config file
	ngrok list                    List tunnel names from config file
	ngrok help                    Print help
	ngrok version                 Print ngrok version

Examples:
	ngrok start www api blog pubsub
	ngrok -log=stdout -config=ngrok.yml start ssh
	ngrok version
```


## 配置
配置文件中尽量不要有中文，必须是UTF_8编码（不是会报错），
下面的配置文件，第一个隧道是一个有认证的只转发 https 的隧道。第二个隧道转发我们自己机器的 22 端口以便让我可以通过隧道连接到自己的电脑，是一个http隧道，client和weixin指定域名前缀（subdomain）
```
server_addr: "tunnel.qydev.com:4443"#可以改成别的网站
trust_host_root_certs: falsetunnels
tunnels:
  client:
    auth: "user:password"
    proto:
      https: 8080
  ssh:
    proto: 
      tcp: 22
  test.tunnel.qydev.com:
    proto:
      http: 4000
  weixin2: 
    proto: 
      http: 80 
```
##  运行
执行`./ngrok -config ngrok.cfg  list `可以看到
weixin2
client
ssh
test.tunnel.qydev.com
已经成功添加了四个隧道
运行./ngrok -config ngrok.cfg start ssh client ，可以开启指定的端口隧道。

注意
配置文件每一项冒号后面必须有空格，必须有空格，必须有空格
1.x配置和2.x不同


其他类似服务（注意看好ngrok版本）
 https://ngrok.cc/
本文参考https://imlonghao.com/28.html
