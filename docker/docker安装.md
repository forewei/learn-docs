### **Docker** **安装**

Docker 提供了两个版本：社区版 (CE) 和企业版 (EE)。

### **操作系统要求** 

以Centos7为例，且Docker 要求操作系统必须为64位，且centos内核版本为3.1及以上。 

查看系统内核版本信息： 

```
uname -r
```

#### **一、准备**

卸载旧版本： 

```
yum remove docker docker-common docker-selinux docker-engine 

yum remove docker-ce 
```

卸载后将保留 /var/lib/docker 的内容（镜像、容器、存储卷和网络等）。 

```
rm -rf /var/lib/docker 
```

##### 1.安装依赖软件包 

```
yum install -y yum-utils device-mapper-persistent-data lvm2 
```

\#安装前可查看device-mapper-persistent-data和lvm2是否已经安装 

```
rpm -qa|grep device-mapper-persistent-data 

rpm -qa|grep lvm2 
```

##### 2.设置yum源 

```
yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo 
```

##### 3.更新yum软件包索引 

```
yum makecache fast
```

#### **二、安装** 

安装最新版本docker-ce

```
yum install docker-ce -y 

\#安装指定版本docker-ce可使用以下命令查看 

yum list docker-ce.x86_64 --showduplicates | sort -r 

\# 安装完成之后可以使用命令查看 

docker version 
```

#### **三、配置镜像加速** 

这里使用阿里云的免费镜像加速服务，也可以使用其他如时速云、网易云等 

##### 1.注册登录开通阿里云容器镜像服务 

##### 2.查看控制台，招到镜像加速器并复制自己的加速器地址 

##### 3.找到/etc/docker目录下的daemon.json文件，没有则直接 vi daemon.json 

##### 4.加入以下配置

```
#填写自己的加速器地址 
{
"registry-mirrors": ["https://zfzbet67.mirror.aliyuncs.com"] 
}
```

##### 5.通知systemd重载此配置文件； 

```
systemctl daemon-reload 
```

##### 6.重启docker服务 

```
systemctl restart docker
```

### **Docker常用操作**

输入 docker 可以查看Docker的命令用法，输入 docker COMMAND --help 查看指定命令详细用法。

### **镜像常用操作** 

#### 查找镜像 

```
docker search 关键词
#搜索docker hub网站镜像的详细信息
```

#### 下载镜像

```
docker pull 镜像名:TAG 
\# Tag表示版本，有些镜像的版本显示latest，为最新版本
```

#### 查看镜像

```
docker images 
\# 查看本地所有镜像
```

#### 删除镜像

```
docker rmi -f 镜像ID或者镜像名:TAG 
\# 删除指定本地镜像 
\# -f 表示强制删除
```

#### 获取元信息

```
docker inspect 镜像ID或者镜像名:TAG 
\# 获取镜像的元信息，详细信息 
```

### **容器常用操作**

运行： 

```
docker run --name 容器名 -i -t -p 主机端口:容器端口 -d -v 主机目录:容器目录:ro 镜像ID或镜像名:TAG 
\# --name 指定容器名，可自定义，不指定自动命名 
\# -i 以交互模式运行容器 
\# -t 分配一个伪终端，即命令行，通常-it组合来使用 
\# -p 指定映射端口，讲主机端口映射到容器内的端口 
\# -d 后台运行容器 
\# -v 指定挂载主机目录到容器目录，默认为rw读写模式，ro表示只读
```

容器列表： 

```
docker ps -a -q 
\# docker ps查看正在运行的容器 
\# -a 查看所有容器（运行中、未运行） 
\# -q 只查看容器的ID 
```

启动容器：

```
docker start 容器ID或容器名
```

停止容器： 

```
docker stop 容器ID或容器名 
```

删除容器： 

```
docker rm -f 容器ID或容器名 
\# -f 表示强制删除
```

查看日志：

```
docker logs 容器ID或容器名 
```

进入正在运行容器：

```
docker exec -it 容器ID或者容器名 /bin/bash 
\# 进入正在运行的容器并且开启交互模式终端 
\# /bin/bash是固有写法，作用是因为docker后台必须运行一个进程，否则容器就会退出，在这里表示启动容器后启动 
bash。 
\# 也可以用docker exec在运行中的容器执行命令
```

拷贝文件： 

```
docker cp 主机文件路径 容器ID或容器名:容器路径 #主机中文件拷贝到容器中 
docker cp 容器ID或容器名:容器路径 主机文件路径 #容器中文件拷贝到主机中
```

获取容器元信息：

```
docker inspect 容器ID或容器名
```

### **实战：****mysql**

```
docker pull mysql:5.7 
\#创建三个要挂载的目录 
mkdir -p /my/mysql/conf 
mkdir -p /my/mysql/data 
mkdir -p /my/mysql/logs
\#复制文件 并修改字符 
docker cp mysql:/etc/mysql/mysql.conf.d/mysqld.cnf /my/mysql/conf/ 
vi /my/mysql/conf/mysqld.conf
character-set-server=utf8 
\#最终启动命令
docker run \ 
--name mysql \ 
-p 3306:3306 \ 
-v /my/mysql/conf:/etc/mysql/mysql.conf.d/ \ 
-v /my/mysql/data:/var/lib/mysql \ 
-v /my/mysql/logs:/logs \
-e MYSQL_ROOT_PASSWORD=root \ 
-d mysql:5.7
```

