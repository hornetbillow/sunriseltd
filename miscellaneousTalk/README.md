# 杂谈笔记

### 谷歌翻墙笔记

>在阿里云后台,购买 1核CPU 1GB内存 的服务器, 操作系统选择的是 CentOS 7.2

### 安装Shdowsocks服务端

登录阿里云服务器, 执行以下命令

1. 安装pip
    - yum install python-pip

2. 使用pip安装shadowsocks
    - pip install shadowsocks

3. 配置Shdowsocks服务,并启动

>新建 /etc/shadowsocks.json 文件, 并写入以下内容

```
{
	"server":"remote-shadowsocks-server-ip-addr",
	"server_port":443,
	"local_address":"127.0.0.1",
	"local_port":1080,
	"password":"your-passwd",
	"timeout":300,
	"method":"aes-256-cfb",
	"fast_open":false,
	"workers":5
}
```
注意修改 server 和 password, workers 表示启动的进程数量。

然后使用以下命令启动: ssserver -c /etc/shadowsocks.json -d start