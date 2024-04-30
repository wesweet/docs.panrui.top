<!--
 * @Description:
 * @Author: prui
 * @Date: 2024-04-29 15:28:39
 * @LastEditTime: 2024-04-30 10:02:52
 * @LastEditors: prui
 * 不忘初心,不负梦想
-->

## nvm

#### 下载路径

- [下载](https://github.com/coreybutler/nvm-windows/releases)

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

最后更新时间：2024-4-28 16:15:29
