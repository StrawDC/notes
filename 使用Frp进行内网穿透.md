# 使用 Frp 进行内网穿透

## 下载 Frp

首先,去 Frp 的 Github 下载最新的服务端文件,将其解压,放到服务器目录中并解压

https://github.com/fatedier/frp/releases

## 配置服务端

服务端,也就是公网 IP 机器

编辑`frps.ini`配置文件,frps 代表服务端配置

```
[common]
# frp监听的端口，默认是7000，可以改成其他的
bind_port = 7000
# token，可以更复杂
token = 52010

# frp管理后台端口，请按自己需求更改
dashboard_port = 7500
# frp管理后台用户名和密码，请改成自己的
dashboard_user = admin
dashboard_pwd = admin
enable_prometheus = true

```

### 启动服务端 Frp

```
./frps -c frps.ini
# 或者后台运行（说明：>/dev/null 2>&1 &，表示丢弃）
nohup ./frps -c frps.ini >/dev/null 2>&1 &
```

## 配置客户端

客户端就是需要内网穿透的机器

配置`frpc.ini`,客户端配置文件

```
[common]
#公网IP
server_addr = 124.221.244.19
 # 与frps.ini的bind_port一致
server_port = 7000
# 与frps.ini的token一致
token = 52010
login_fail_exit = false
tls_enable=true

[http]
type = tcp
#自定义的远程服务器端口，例如8080
remote_port = 8899
 #要映射的内网IP地址
local_ip = 127.0.0.1
#映射的内网IP端口
local_port = 80

```

### 启动客户端

```
./frpc -c frpc.ini
```
