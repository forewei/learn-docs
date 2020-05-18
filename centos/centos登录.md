### 设置证书登录 

####  生成公私玥

 使用ssh-kegen命令生成公私钥 生成的文件路径在/root/.ssh/

```
ssh-keygen
```

#### 配置公玥

把公玥写入 /root/.ssh/authorized_keys

```
cat id_rsa.pub >> authorized_keys
```

最后把私玥发送到自己要链接的客户端

### 关闭用户密码登录方式

#### 编辑ssh 配置文件

```
 vim /etc/ssh/sshd_config 
```

#### 修改配置

yes打开密码登录 no关闭密码登录

```
PasswordAuthentication yes/no 
```

#### 重启服务

```
 service sshd restart 
```
#### 修改hostname
hostnamectl set-hostname forewei
