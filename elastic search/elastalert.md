1.python setup.py install 错误处理

​    解决办法：

```
wget https://pypi.python.org/packages/source/s/setuptools/setuptools-0.6c11.tar.gz
tar zxvf setuptools-0.6c11.tar.gz
cd setuptools-0.6c11
python setup.py install
```



2.pip安装

```
$ curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py   # 下载安装脚本
$ sudo python get-pip.py    # 运行安装脚本
```

**注意：**用哪个版本的 Python 运行安装脚本，pip 就被关联到哪个版本，如果是 Python3 则执行以下命令：

```
pip3 ython get-pip.py
```

部分 Linux 发行版可直接用包管理器安装 pip，如 Debian 和 Ubuntu：

```
sudo apt-get install python-pip
```