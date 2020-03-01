### 关闭阿里云盾

CentOS推荐用这个，使用

```
chkconfig --list
```

查看开机启动里面这个软件的服务名是什么，然后替换掉xxx然后执行就可以了；

如果想开机不启动的话，chkconfig –del xxxx这个xxxx就是你找出来aliyundun的后台服务。

```
service aegis stop  #停止服务
chkconfig --del aegis  # 删除服务
```

### 安装shadowsocks-all

```
$ wget --no-check-certificate -O shadowsocks-all.sh https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks-all.sh
$ chmod +x shadowsocks-all.sh
$ ./shadowsocks-all.sh 2>&1 | tee shadowsocks-all.log
```

三行代码一行一行的执行即可，然后填写账号密码。

执行后，会提示输入源码语言，密码、端口、及加密方式等。（端口使用8989；源码选择的是go语言；加密方式我这里选择aes-256-cfb；）

最终显示你得账号密码则为成功！

### 卸载

```
./shadowsocks-all.sh uninstall
```

### 安装锐速

因为 CentOS7 X64 系统的内核版本太高，所以没办法直接安装锐速，我们需要对系统内核进行降级操作。按照下图提示，我们首先复制下列命名：

```
wget --no-check-certificate -O rskernel.sh https://raw.githubusercontent.com/hombo125/doubi/master/rskernel.sh && bash rskernel.sh
```

等待内核更换完毕后系统会自动重启并断开连接。然后重新连接，执行下面命令。

```
yum install net-tools -y && wget --no-check-certificate -O appex.sh https://raw.githubusercontent.com/0oVicero0/serverSpeeder_Install/master/appex.sh && bash appex.sh install
```

按回车键继续，系统会自动安装锐速，同时会先后要求我们设置锐速的三项信息。按照下图提示，我们每次都直接回车继续即可。

出现以下就以为启动成功 

```
ServerSpeeder is running!
```

### 锐速相关命令

```
#查看运行状态
/appex/bin/serverSpeeder.sh status

#启动锐速
/appex/bin/serverSpeeder.sh start

#停止锐速
/appex/bin/serverSpeeder.sh stop

#重启锐速
/appex/bin/serverSpeeder.sh restart

#卸载锐速
/appex/bin/serverSpeeder.sh uninstall


```

如果以上安装烦锁，可以考虑v2ray意见安装

### 后续工作

阿里云得防火墙打开8989，通过客户端shadownsocks连接即可用



## v2ray一键安装

#### 安装 Curl 方法:

```
apt-get update -y && apt-get install curl -y
```



####   安装脚本

```
bash <(curl -s -L https://git.io/v2ray.sh)
```

#### 	相关命令

`v2ray info` 查看 V2Ray 配置信息
`v2ray config` 修改 V2Ray 配置
`v2ray link` 生成 V2Ray 配置文件链接
`v2ray infolink` 生成 V2Ray 配置信息链接
`v2ray qr` 生成 V2Ray 配置二维码链接
`v2ray ss` 修改 Shadowsocks 配置
`v2ray ssinfo` 查看 Shadowsocks 配置信息
`v2ray ssqr` 生成 Shadowsocks 配置二维码链接
`v2ray status` 查看 V2Ray 运行状态
`v2ray start` 启动 V2Ray
`v2ray stop` 停止 V2Ray
`v2ray restart` 重启 V2Ray
`v2ray log` 查看 V2Ray 运行日志
`v2ray update` 更新 V2Ray
`v2ray update.sh` 更新 V2Ray 管理脚本
`v2ray uninstall` 卸载 V2Ray

#### github地址

```
https://github.com/233boy/v2ray/
```

## 端口不可用（手动添加端口）

### 查看firewall状态

```
systemctl status firewalld.service
firewall-cmd --state
```

### 查看开放端口

```
firewall-cmd --zone=public --list-ports
```

### 添加端口

```
firewall-cmd --zone=public --add-port=80/tcp --permanent
```

### 务必要重载才能生效开放的端口

```
firewall-cmd --reload
```

### 询问端口状态和移除端口

```
firewall-cmd --zone=public --query-port=80/tcp
firewall-cmd --zone=public --remove-port=80/tcp --permanent
```



### trojan安装脚本

```
curl -O https://raw.githubusercontent.com/atrandys/trojan/master/trojan_centos7.sh && chmod +x trojan_centos7.sh && ./trojan_centos7.sh
```

