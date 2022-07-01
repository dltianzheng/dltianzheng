# centos

## 设置IP以及联网

```shell
#版本
[root@bsa10026 ~]# cat /etc/redhat-release 
CentOS Linux release 7.9.2009 (Core)
```

```shell
#设置静态IP
#需要编辑网卡的配置
vim /etc/sysconfig/network-scripts/ifcfg-ens192

cat /etc/sysconfig/network-scripts/ifcfg-ens192
```

```txt
#网卡配置内容
BOOTPROTO="none"
DEFROUTE="yes"
IPV4_FAILURE_FATAL="no"
IPV6INIT="yes"
IPV6_AUTOCONF="yes"
IPV6_DEFROUTE="yes"
IPV6_FAILURE_FATAL="no"
IPV6_ADDR_GEN_MODE="stable-privacy"
NAME="ens192"
UUID="b1606870-3436-4863-8d95-bc3bee9047b2"
DEVICE="ens192"
ONBOOT="yes"
IPADDR="10.8.100.28"
PREFIX="16"
GATEWAY="10.8.255.254"
DNS1="114.114.114.114"
DOMAIN="8.8.8.8"
IPV6_PRIVACY="no"
```

```shell
#重启网卡
/etc/init.d/network restart
```

```shell
#配置hostname
vim /etc/hostname
reboot
#重启后生效
```

## service | 服务

```shell
# 查看服务log
journalctl -xe
```

## 包管理yum

