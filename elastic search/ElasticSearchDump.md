## 要通过 yum 安装nodejs 和 npm 

####  添加 epel 源 

```
rpm -ivh http://download.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
```

####        导入 key:  

```
    rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-6
```

####       添加 remi 源 

```
rpm -ivh http://rpms.famillecollet.com/enterprise/remi-release-6.rpm
rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-remi
```

####      安装完成后,执行 

```
    curl --silent --location https://rpm.nodesource.com/setup_5.x | bash -
    yum -y install nodejs
```

## node 升级**

####  首先安装n模块

```
   npm install -g n 
```

####  升级node.js到最新稳定版 

```
 n stable 
```

## 安装elasticdump

```
 npm install elasticdump
```

```
 cd /node_modules/elasticdump/bin 
```

执行索引移植命令

```
./elasticdump --input=http://192.168.1.55:9201/intention_20180420 --output=http://192.168.2.126:9201 /intention_20180531 --type=data
```

