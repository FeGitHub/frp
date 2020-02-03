## frp内网穿透
### 参考资料及工具
https://gitee.com/yijicai/frp

### 首先你得有一个公网ip的服务器

### 修改服务端  ubantu
wget https://github.com/fatedier/frp/releases/download/v0.20.0/frp_0.20.0_linux_amd64.tar.gz

如果提示：
-bash: wget: command not found

yum -y install wget

使用tar指令解压tar.gz文件
tar -zxvf frp_0.20.0_linux_amd64.tar.gz

cd frp_0.20.0_linux_amd64

vi frps.ini


[common]
bind_port = 7000
dashboard_port = 7500
dashboard_user = admin
dashboard_pwd = admin
vhost_http_port = 80
vhost_https_port = 443
token = Ddsf43FGERsdfdsf
---

临时启动
./frps -c ./frps.ini

后台保持启动
nohup ./frps -c frps.ini >/dev/null 2>&1 &

### 修改客户端 windows

修改 frpc.ini
---
[common]
server_addr = 你的公网ip，如：XXX.XXX.XXX.XXX
server_port = 用于frp的端口，如:700X
token = 秘钥（服务端和客户端保持一致），如：Ddsf43FGERsdfdsf

[ssh]
type = tcp
local_ip = 内网的ip，如:127.0.0.1  
local_port = 内网要映射的端口，如：8080
remote_port = 公网对外访问内网的端口，如：8888
---

cmd 启动

./frpc -c ./frpc.ini
