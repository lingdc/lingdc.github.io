## 虚拟机准备

1.防火墙关闭
service iptables stop//服务关闭
chkconfig iptables off//关闭开机自启

连接xshell

同步时间

date -s "2019-06-25 20:13:00"

2.创建一个一般用户 lingdc
useradd lingdc

![image-20200526162444480](C:\Users\yaoe\AppData\Roaming\Typora\typora-user-images\image-20200526162444480.png)

passwd 
3.在/opt目录下创建 software module文件夹
mkdir /opt/software /opt/module
chown lingdc:lingdc /opt/software /opt/module
4.把这个用户加到sudoers
vim /etc/sudoers
lingdc ALL=(ALL)              NOPASSWD:ALL

:wq!

5.改 Hosts
vim /etc/hosts
在文件后追加
192.168.1.100 master
192.168.1.101 node1
192.168.1.102 node2

6.改静态IP*每克隆一台都需要做一遍
vim-/etc/sysconfig/network-scripts/ifcfg-eth0

DEVICE=eth0
TYPE=Ethernet
ONBOOT=yes
BOOTPROTO=static
IPADDR=192.168.1.100
PREFIX=24
GATEWAY=192.168.1.2
DNS1=11.168.1.2
NAME=eth0

(通过虚拟网络编辑器修改网关等地址)

7.改主机名*每克隆一台都需要做一遍
vim /etc/sysconfig/network
改 HOSTNAME字段
改成 HOSTNAME= hadoop100
拍快照(在此克隆)

//新虚拟机，不用第八步
8.改网卡脚本文件*每克隆一台都需要做一遍
vim /etc/udev/rules.d/70-persistent-net.rules
第一行删

第二行
最后NAME="eth1"改成NAME="etho”



## JAVA准备(master)



hadoop-2.7.2.tar.gz 

jdk-8u144-linux-x64.tar.gz 

导入/opt/software

解压：tar-zxvf jdk-8u144-linux-x64.tar.gz -C /opt/module

至/opt/module



#JAVA_HOME
export JAVA_HOME=/opt/module/jdk1.8.0_144
export PATH=$PATH:$JAVA_HOME/bin
#HADOOP_HOME
export HADOOP_HOME=/opt/module/hadoop-2.7.2
export PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin