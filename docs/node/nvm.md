<!--
 * @Description:
 * @Author: panrui
 * @Date: 2023-05-13 10:46:35
 * @LastEditTime: 2023-05-22 15:46:19
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->

## 最后更新时间：2023-05-13 10-56-04

#### 下载路径

> [下载](https://github.com/coreybutler/nvm-windows/releases)

#### linux 安装 nvm 报错

```
curl: (7) Failed to connect to raw.githubusercontent.com port 443: 拒绝连接

解决方案：添加域名解析ip
vim /etc/hosts
199.232.28.133 raw.githubusercontent.com

查看配置文件
cat /root/.bashrc

配置生效
source /root/.bashrc

激活nvm
source ~/.nvm/nvm.sh
```
