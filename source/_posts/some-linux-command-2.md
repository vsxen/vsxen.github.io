---
title: Linux命令之二--sed
date: 2016-10-12 17:52:15
categories:
tags:
---
sed -i -e  's/PermitRootLogin no/PermitRootLogin yes/g' ssh_config 
sed -i 's/,scandir//g' /usr/local/php/etc/php.ini