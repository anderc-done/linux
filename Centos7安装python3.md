# Centos6安装Python3

## 第1步 - 准备系统

我们首先通过运行这个命令来确保yum是最新的：

```shell
sudo yum -y update
```

接下来，我们将安装`yum-utils`，这是一个扩展和补充yum的实用程序和插件的集合

```shell
sudo yum -y install yum-utils
```

最后，我们将安装CentOS开发工具，这些工具用于允许您从源代码构建和编译软件：

```shell
sudo yum -y groupinstall development
```

## 第2步 - 安装和设置Python 3

因为我们想要安装Python 3的最新上游稳定版本，我们需要安装**IUS**，代表Inline with Upstream Stable。作为一个社区项目，IUS为选择软件的一些更新版本提供了红帽软件包管理器（RPM）软件包。

```shell
sudo yum -y install https://centos7.iuscommunity.org/ius-release.rpm
```

IUS完成安装，我们可以安装最新版本的Python：

```shell
sudo yum -y install python36u
```

当Python的安装过程完成后，我们可以通过以下`python3.6`命令检查其安装是否成功：

```shell
python3.6 -V
```

接下来我们将安装`pip`，它将管理Python的软件包：

```shell
sudo yum -y install python36u-pip
```

一个用于Python的工具，我们将使用**pip**来安装和管理我们可能想在我们的开发项目中使用的编程包。你可以通过键入以下命令来安装Python包

```shell
sudo pip3.6 install package_name
```

在这里，`package_name`可以参考任何Python包或者库，比如用于Web开发的Django或者用于科学计算的NumPy。所以如果你想安装NumPy，你可以用命令来完成`pip3.6 install numpy`。

最后，我们将需要安装IUS软件包**python36u-devel**，它为我们提供了Python 3开发所需的库和头文件：

```shell
sudo yum -y install python36u-devel
```

安装完成后我们可以在/usr/bin下找到python3的运行文件

输入命令可进入python3

```shell
python3.6
```

