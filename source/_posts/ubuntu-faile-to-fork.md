---
title: Ubuntu apt get faile to fork解决方法 
date: 2016-11-04 10:42:42
categories: 
tags: 一些问题 
---


在Ubuntu14.04LTS上面安装东西，忽然发现不可以用了，具体表现为
>apt-get  install git
No packages will be installed, upgraded, or removed.
0 packages upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
Need to get 0 B of archives. After unpacking 0 B will be used.
FATAL -> Failed to fork.


google 搜索到
http://serverfault.com/questions/401862/debian-fatal-failed-to-fork

发现第二个人回答的可以解决，意思是swap空间不够了（好像支持的人很少），只要运行 
```
curl -sSL https://manageacloud.com/api/cm/configuration/activate_swap/ubuntu/manageacloud-production-script.sh | bash
```
就可以继续越快的apt-get了。



脚本备份
```shell
#!/bin/bash
mkdir -p /tmp/manageacloud/
PREFIX='';
if [ `id -u` != 0 ] ; then
    PREFIX='sudo -E ';
fi
apt_timeout="0"
until which git || (( "$apt_timeout" > 10 ))
do
    if [ "$apt_timeout" != "0"  ]; then
        sleep 10
    fi
    $PREFIX apt-get install -q git -y || $PREFIX apt-get -q update | cat && $PREFIX apt-get -q install git -y | cat
    apt_timeout=$[$apt_timeout+1]
done

cat > /tmp/manageacloud/.manageacloud.sh << 'MACEOL'
#!/bin/bash
set -ue

dd if=/dev/zero of=/swapfile bs=1024 count=512k
mkswap /swapfile

echo vm.swappiness = 10 | sudo tee -a /etc/sysctl.conf
echo 10 | sudo tee /proc/sys/vm/swappiness

chown root:root /swapfile
chmod 0600 /swapfile

echo " /swapfile       none    swap    sw      0       0 " >> /etc/fstab

swapon /swapfile



MACEOL

#!/bin/bash
set +u
export DEBIAN_FRONTEND=noninteractive
shopt -s xpg_echo
unset PATH JAVA_HOME LD_LIBRARY_PATH
function abort {
   echo "aborting: $@" 1>&2
   exit 1
}
export PATH=/usr/ucb/bin:/bin:/sbin:/usr/bin:/usr/sbin
cat > /etc/motd <<EOL

=================================================
To debug Manageacloud

Bootstrap script:
    cd /tmp/manageacloud/vcs/
    bash .manageacloud.sh

Environment variables:
    cat /tmp/manageacloud/env.log

Git repository (if applicable):
    cd /tmp/manageacloud/vcs/

Any questions support@manageacloud.com
=================================================
 
EOL


env > /tmp/manageacloud/env.log
PREFIX=''
if [ `id -u` != 0 ] ; then
    PREFIX='sudo -E ';
fi
echo 'Host * 
         StrictHostKeyChecking no' >> ~/.ssh/config
rm -rf /tmp/manageacloud/vcs/
mkdir -p /tmp/manageacloud/vcs/
CLONE=""
BRANCH=""
PRIV_KEY=""
if [ "$PRIV_KEY" != "" ]; then
PREFIX='';
if [ `id -u` != 0 ] ; then
    PREFIX='sudo -E ';
fi

apt_timeout="0"
until which git || (( "$apt_timeout" > 10 ))
do
    if [ "$apt_timeout" != "0"  ]; then
        sleep 10
    fi
    $PREFIX apt-get install -q git -y || $PREFIX apt-get -q update | cat && $PREFIX apt-get -q install git -y | cat
    apt_timeout=$[$apt_timeout+1]
done
   cd /tmp/manageacloud/
   echo '#!/bin/sh
   if [ -z "$PKEY" ]; then
       ssh "$@"
   else
       ssh -i "$PKEY" "$@"
   fi' > git_patch.sh
   chmod +x git_patch.sh
   echo "$PRIV_KEY" > ~/.ssh/mac_private
   chmod 600 ~/.ssh/mac_private
   if [ "$BRANCH" != "" ]; then
       set -x
       cd /tmp/manageacloud/vcs/ && GIT_SSH=../git_patch.sh PKEY=~/.ssh/mac_private git clone -q $CLONE . | cat && git checkout $BRANCH
       set +x
   fi
else
PREFIX='';
if [ `id -u` != 0 ] ; then
    PREFIX='sudo -E ';
fi

apt_timeout="0"
until which git || (( "$apt_timeout" > 10 ))
do
    if [ "$apt_timeout" != "0"  ]; then
        sleep 10
    fi
    $PREFIX apt-get install -q git -y || $PREFIX apt-get -q update | cat && $PREFIX apt-get -q install git -y | cat
    apt_timeout=$[$apt_timeout+1]
done
   if [ "$BRANCH" != "" ]; then
       set -x
       cd /tmp/manageacloud/vcs/ && git clone $CLONE .| cat && git checkout $BRANCH
       set +x
   fi
fi
cp /tmp/manageacloud/.manageacloud.sh /tmp/manageacloud/vcs/
cd /tmp/manageacloud/vcs/ && $PREFIX bash ./.manageacloud.sh | cat 
test ${PIPESTATUS[0]} -eq 0
exit $?
```