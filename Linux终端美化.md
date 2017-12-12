# Linux终端美化

在linux终端内安装美化，在xshell中调整，并显示一个漂亮的操作环境
* **系统**
    * Centos7 x86_64

* **工具**

    * zsh
    * oh my zsh
    * xshell
    * Monofur for Powerline.ttf（Powerline字体）
    * Powerlevel9k （oh my zsh主题）

* **美化前的样子**

![未美化前]()

### xshell美化

* 下载字体

链接：[github Powerline字体](https://github.com/powerline/fonts)

下载好字体后安装，xshell即可选用

* xshell美化

选择合适的字体，然后将xshell设置为透明，具体请参考其他资料

### linux终端美化

* 安装zsh

```shell
yum -y install zsh
```
* 修改shell为zsh

```shell
chsh -s /bin/zsh
```
返回如下结果
> Changing shell for root.

> Shell changed.

* 安装oh-my-zsh

```shell
wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | sh
```
![安装完oh-my-zsh]()

断开与服务器的连接，并重新连接服务器

![重新连接服务器]()

* 配置oh-my-zsh主题

```shell
git clone https://github.com/bhilburn/powerlevel9k.git ~/.oh-my-zsh/custom/themes/powerlevel9k
```
编辑zsh配置文件

ZSH_THEME一行改为

ZSH_THEME="powerlevel9k/powerlevel9k"

```shell
source ~/.zshrc
```
调整xshell的配色方案，让配色看起来更舒服一些

调整后的效果如下

![powerlevel9k效果]()

可以对powerlevel9k进行更进一步的配置，参考github powerlevel9k

链接：[github powerlevel9k](https://github.com/bhilburn/powerlevel9k)

* 最终效果如下

![最终效果]()
