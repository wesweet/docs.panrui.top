<!--
 * @Author: panr99 1547177202@qq.com
 * @Date: 2024-06-24 14:24:04
 * @LastEditors: panrui 1547177202@qq.com
 * @LastEditTime: 2024-09-27 19:34:36
 * @FilePath: \docs.panrui.top\docs\1panel\README.md
 * @Description:
-->

# pve

pve 虚拟机平台入口：https://192.168.31.48:8006
账号：root 密码：Pr338535
账号:panrui 密码：Pr338535

## ws2022

1. 登录密码 Pr338535

## debian

#### 1panel

1panel 登录入口：http://192.168.31.188:38639/ 账号:panrui 密码：Pr338535

###### ddns

登录入口：http://192.168.31.188:38640 账号:root 密码：Pr338535

###### phpMyAdmin

登录入口： http://192.168.31.188:38643 服务器：1Panel-mysql-rIip 用户名：root 密码：Pr338535

# 域名管理

panrui.top
dhan.top
prlovedh.top

网络配置：
1panel
{
"Name": "1panel-network",
"Id": "c1d24b6ed67450a9cde9cadecdc7266a02f3b71dabfcb9047d4b4f3f1d1367dd",
"Created": "2024-06-22T21:18:12.657921359+08:00",
"Scope": "local",
"Driver": "bridge",
"EnableIPv6": false,
"IPAM": {
"Driver": "default",
"Options": null,
"Config": [
{
"Subnet": "172.18.0.0/16",
"Gateway": "172.18.0.1"
}
]
},
"Internal": false,
"Attachable": false,
"Ingress": false,
"ConfigFrom": {
"Network": ""
},
"ConfigOnly": false,
"Containers": {},
"Options": {},
"Labels": {}
}

{
"Name": "phpmyadmin_default",
"Id": "726e2ecfd9df0aac2c40eb574ba540acf17389d85a20fb96e6ed31c1d7e02d23",
"Created": "2024-06-22T21:47:15.148120824+08:00",
"Scope": "local",
"Driver": "bridge",
"EnableIPv6": false,
"IPAM": {
"Driver": "default",
"Options": null,
"Config": [
{
"Subnet": "172.20.0.0/16",
"Gateway": "172.20.0.1"
}
]
},
"Internal": false,
"Attachable": false,
"Ingress": false,
"ConfigFrom": {
"Network": ""
},
"ConfigOnly": false,
"Containers": {},
"Options": {},
"Labels": {
"com.docker.compose.network": "default",
"com.docker.compose.project": "phpmyadmin",
"com.docker.compose.version": "2.26.1"
}
}

{
"Name": "nest_default",
"Id": "c05c33ed914ff53cc76f15e65c309dc9f5116cd247c8bc1d00359912768af851",
"Created": "2024-06-23T09:13:51.682856912+08:00",
"Scope": "local",
"Driver": "bridge",
"EnableIPv6": false,
"IPAM": {
"Driver": "default",
"Options": null,
"Config": [
{
"Subnet": "172.24.0.0/16",
"Gateway": "172.24.0.1"
}
]
},
"Internal": false,
"Attachable": false,
"Ingress": false,
"ConfigFrom": {
"Network": ""
},
"ConfigOnly": false,
"Containers": {},
"Options": {},
"Labels": {
"com.docker.compose.network": "default",
"com.docker.compose.project": "nest",
"com.docker.compose.version": "2.26.1"
}
}

{
"Name": "mariadb-link",
"Id": "853d401a3f1f8cc59098c83f4a6ffced3a7d00ed65a17026ca7b4a84e173bdb3",
"Created": "2024-06-23T23:34:35.400388104+08:00",
"Scope": "local",
"Driver": "bridge",
"EnableIPv6": false,
"IPAM": {
"Driver": "default",
"Options": null,
"Config": [
{
"Subnet": "172.30.0.0/16",
"Gateway": "172.30.0.1"
}
]
},
"Internal": false,
"Attachable": false,
"Ingress": false,
"ConfigFrom": {
"Network": ""
},
"ConfigOnly": false,
"Containers": {},
"Options": {},
"Labels": {}
}

{
"Name": "db_net-mariadb",
"Id": "21eff5da40173938a1c3ac141d35047a225ff9c97b02422d41d9da09d931cd8b",
"Created": "2024-06-23T23:47:42.582450831+08:00",
"Scope": "local",
"Driver": "bridge",
"EnableIPv6": false,
"IPAM": {
"Driver": "default",
"Options": null,
"Config": [
{
"Subnet": "192.168.32.0/20",
"Gateway": "192.168.32.1"
}
]
},
"Internal": false,
"Attachable": false,
"Ingress": false,
"ConfigFrom": {
"Network": ""
},
"ConfigOnly": false,
"Containers": {},
"Options": {},
"Labels": {
"com.docker.compose.network": "net-mariadb",
"com.docker.compose.project": "db",
"com.docker.compose.version": "2.26.1"
}
}

网站配置文件：
server {
listen 8043 default_server;
listen [::]:8043 default_server;
server_name default.panrui.top;
index index.php index.html index.htm default.php default.htm default.html;
proxy_set_header Host $host;
proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
proxy_set_header X-Forwarded-Host $server_name;
proxy_set_header X-Real-IP $remote_addr;
proxy_http_version 1.1;
proxy_set_header Upgrade $http_upgrade;
proxy_set_header Connection "upgrade";
access_log /www/sites/default.panrui.top/log/access.log main;
error_log /www/sites/default.panrui.top/log/error.log;
location ^~ /.well-known/acme-challenge {
allow all;
root /usr/share/nginx/html;
}
include /www/sites/default.panrui.top/proxy/\*.conf;
}
