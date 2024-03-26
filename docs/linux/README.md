<!--
 * @Description: linux系统使用规范
 * @Author: panrui
 * @Date: 2023-05-13 11:32:31
 * @LastEditTime: 2023-09-14 09:24:50
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->

# linux 最后更新时间: 2023-09-14 08-50-58

- [linux 命令大全](https://www.linuxcool.com/)

#### 其他命令

```
查询linux系统的版本信息
cat /etc/*release

查看端口占用情况
ss -lntup

查看nginx进程
ps -aux | grep nginx

查看指定端口占用情况
netstat -tuln | grep 80

显示往前电脑的ipv6地址
ip -6 addr show
```

#### Rocky Linux 系统命令

```
dnf是一款软件包管理器与之类似的还有yum

查看安装的软件包
dnf list installed(仅显示已安装的软件包列表。这将显示所有已安装的软件包，但不包括未安装的软件包。)
dnf repolist all( 命令显示所有已安装和未安装软件包的列表，以及每个软件包所属的仓库。这将显示所有可用的软件包，包括已安装和未安装的。)

更新软件包
dnf update

安装软件包
dnf install bind-utils
```

#### 修改 ddns 查看域名配置情况

```
vim /etc/ddns/config.json

cat /var/log/cron_log/ddns_cron.log

// 重启服务
使用绝对路径执行 run.sh 文件：在命令行中输入 "/path/to/run.sh"（其中 "/path/to/" 是 run.sh 文件的完整路径）。
使用相对路径执行 run.sh 文件：如果 run.sh 文件和你的命令行在同一目录下，你可以输入 "./run.sh" 来执行该文件。
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
