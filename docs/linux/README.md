<!--
 * @Description:
 * @Author: panrui
 * @Date: 2023-05-13 11:32:31
 * @LastEditTime: 2023-05-19 08:50:02
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->

# linux 最后更新时间: 2023-05-19 08-50-02

- [linux 命令大全](https://www.linuxcool.com/)

#### 其他命令

```
查询linux系统的版本信息
cat /etc/*release

查看端口占用情况
ss -lntup

查看指定端口占用情况
netstat -tuln | grep 80
```

#### Rocky Linux 系统命令

```
更新软件包
dnf update

安装软件包
dnf install bind-utils
```

#### 修改 ddns

```
vim /etc/ddns/config.json
```

#### 防火墙

```
查看防火墙状态
sudo systemctl status firewalld

sudo systemctl start firewalld
sudo systemctl stop firewalld
sudo systemctl restart firewalld

查看端口开放情况
sudo firewall-cmd --list-ports

添加或者删除端口
其中 <port> 表示端口号，<protocol> 表示协议，可以是 tcp、udp 或 icmp。如果使用 --permanent 选项，则修改将永久生效
sudo firewall-cmd --add-port=<port>/<protocol> [--permanent]
sudo firewall-cmd --remove-port=<port>/<protocol> [--permanent]

```

#### 计划任务

```
查看所有计划任务
sudo crontab -l

查看任务执行日志
sudo tail -f /var/log/cron.log

添加计划任务
```

#### 查看域名配置情况

> 1. cat /etc/ddns/config.json
