---
title: linux服务器安全防范
date: 2016-12-11 06:44:52
categories: Linux
tags: 
---

本文适合debian系服务器。
## 安装系统更新
apt-get update
apt-get upgrade
## 禁止密码登陆

sed -i 's/^#PasswordAuthentication yes/PasswordAuthentication no/g' \
      /etc/ssh/sshd_config
sed -i 's/PasswordAuthentication yes/PasswordAuthentication no/g' \
     /etc/ssh/sshd_config
grep PasswordAuthentication /etc/ssh/sshd_config
## 新建用户加入root组
useradd deploy
mkdir /home/deploy
mkdir /home/deploy/.ssh
chmod 700 /home/deploy/.ssh

vim /home/deploy/.ssh/authorized_keys

chmod 400 /home/deploy/.ssh/authorized_keys
chown deploy:deploy /home/deploy -R
## 生产密钥
ssh-keygen
## 更改shh端口
sshd_port="2702"
sed -i "s/^Port 22/Port $sshd_port/g" /etc/ssh/sshd_config
grep "^Port " /etc/ssh/sshd_config
## 更改防火墙
iptables -F; iptables -X
echo 'y' | ufw reset
echo 'y' | ufw enable
ufw default deny incoming
ufw default deny forward

ufw allow 22,80,443/tcp
(iptable根据系统管理员编写的一系列规则筛选网络数据包。对于初学者来说，iptable 可能比较复杂，所以UFW 将其进行了简化。)

ufw allow 2702/tcp
service ssh restart
##　监视登陆事件
apt-get install fail2ban
Fail2ban是一个守护进程，监视对服务器的登录尝试，并阻止可疑活动发生。 它很好配置开箱即用
## 安全检查工具
apt-get install -y lynis
lynis -c

## 查看用户在何时运行了什么命令
echo export HISTTIMEFORMAT=\"%h %d %H:%M:%S \" >> /root/.bashrc

## 修改主机名
echo "my-hostname" > /etc/hostname
hostname -F /etc/hostname

## 经常看日志文件
/var/log/kern.log
/var/log/syslog
/var/log/ufw.log
/var/log/auth.log
/var/log/dpkg.log
/var/log/aptitude
/var/log/boot.log
/var/log/cron.log
/var/log/mailog

如果你配置好了邮件，还可以
vim /etc/cron.daily/00logwatch
/usr/sbin/logwatch --output mail --mailto test@gmail.com --detail high
参考
http://www.dennyzhang.com/linux_security/