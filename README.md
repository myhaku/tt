# START

|[Tintin++](https://tintin.sourceforge.io/)
|[Termux](https://github.com/termux/termux-app)|
</br>
|[Tintin++中文手册](./Wiki.md)|
</br>
|[北侠官网](http://pkuxkx.net/)
|[北侠Wiki](http://pkuxkx.net/wiki/)
|[北侠论坛](http://pkuxkx.net/forum/)
|[紫溪涧](http://zixijian.xyz)|

### 这是做什么的？

本仓库用于存储xgg@pkuxkx的游戏配置，</br>
以及部分相关脚本和文档。

北大侠客行是一个MUDs文字游戏，</br>
Termux是一个安卓系统上的终端模拟器，</br>
Tintin++ 是一个跨平台的MUDs客户端。</br>

北大侠客行可使用 Tintin++ 客户端连接，</br>
Tinin++可以运行在Termux上。

So：tintin++ on termux for pkuxkx。

注：客户端用法与其他平台一致。

### 怎么进入MUDs游戏？

- 1.安装Termux

style插件非必选，可配置字体和主题风格。

- 2.在Termux中安装必须软件及一些必要配置

Termux本身不能运行MUDs游戏，必须安装mud客户端，比如tintin++、Go-Mud，
环境配置可以帮助更好的游戏(比如解决乱码和快速进入游戏)。

- 3.配置文件管理

机器人脚本则是必须的，尤其是没有图形界面的客户端，建议先使用xgg@pkuxkx的机器人熟悉一下。

- 4.启动游戏客户端

这时候启动游戏即可。

```
写给小白的话(老白们跳过)：

不会只是暂时的，
没有人天生什么就都懂，
请细致地阅读文中内容，
请合理地使用搜索引擎，
请合理地联想相同的方法和规律，
有些内容不会在文中重复出现。
```

## 0。Termux

### Termux 简介

> 安卓系统高级终端模拟器。</br>
 使用bash 和 zsh。</br>
 使用nano 和 vim编辑文件。</br>
 通过ssh访问服务器。</br>
 使用gcc和clang编译代码。</br>
 使用python控制台来作为掌上电脑。</br>
 使用git 和 subversion管理项目。</br>
 使用frotz运行基于文本的游戏。</br>
 双指捏合缩放界面。
 
### 下载安装 Termux

- 应用商店内搜索安装

- 访问[Termux](https://github.com/termux/termux-app)获取

### 安装vim git screen tintin++

打开Termux输入如下指令安装**必须**软件：
> pkg up -y
</br>pkg install vim git screen tintin++ -y

**按行复制命令后按回车执行！！！**

安装完毕后，可直接跳转到screen转码。</br>
速度慢可更换国内清华开源镜像站的源。

注：Linux deploy是一款能在安卓手机上利用chroot部署任意linux发行版的app（需要root权限、比Termux更强大），使用linuxdeploy在手机上部署的chroot环境，比如Debian，使用apt(相当于pkg)指令安装完 tintin++ 的路径在`/usr/games/tt++`。

由于Debian上tt版本比较老旧</br>
也可以使用源码进行编译。</br>
Termux不用看此段内容。
```
Debian9编译安装tt++

1.安装编译环境
apt install gcc libgnutls-dev zlib1g-dev libpcre3-dev make cmake -y
2.下载源码到本地
mkdir tintin
cd tintin
[beta]版本
wget https://tintin.sourceforge.io/download/tintin-beta.tar.gz
3.解压、配置、编译
tar -zxf tintin-beta.tar.gz
cd tt/src/
./configure
make
4.复制可执行文件到/bin目录
cp tt++ /bin
```
Termux一般不用编译，仅列出方法。
```
Termux编译安装tt++

1.安装环境
pkg install make cmake libgnutls-dev zlib-dev pcre-dev wget -y
2.获取代码
mkdir tintin
cd tintin
wget https://tintin.sourceforge.io/download/tintin-beta.tar.gz
tar -zxvf tintin-beta.tar.gz
3.进行编译并拷贝二进制文件到bin目录
cd /tt/src
./configure
make
cp tt++ /data/data/com.termux/files/usr/bin/
或
cp tt++ $PREFIX/usr/bin/
```


## 1。Termux相关

**++此步骤非必要++**

个人使用Termux0.72版本(大于0.66版）

如果使用style样式插件则签名必须一致

建议使用apk编辑器签名后安装。

**++配置文件编辑方法如下++**

使用vim文本编辑器编辑：

> vim ~/.termux/termux.properties

按字母i键开启插入模式，方向键控制光标：

```
extra-keys = [['ESC','+','-','HOME','UP','END','PGUP'],['TAB','CTRL','ALT','LEFT','DOWN','RIGHT','PGDN']]
```
将以上内容复制粘贴到文本中，</br>
修改完毕后按ESC键退出编辑模式：

- 输入:wq保存
- 或大写模式按两下ZZ键

回到原版二行工具条。

注：根据[官网](https://tintin.sourceforge.io/android.php)介绍，termux可以使用组合宏键。

**++可根据需求对工具条进行定制++**

以下是xgg@pkuxkx使用的工具条：

```
extra-keys = [['ESC','ALT','PGUP','HOME','UP','END','chat ','ENTER'],['CTRL','TAB','PGDN','LEFT','DOWN','RIGHT','orz','BACKSPACE']]
```

**++初始脚本使用++**

> vim ~/.bashrc

可将常用命令进行别名设置，</br>
开启新窗口配置立即生效。</br>
善用别名可大幅简化操作。

```
export LS_OPTIONS='--color=auto'
eval "`dircolors`"
alias ls='ls $LS_OPTIONS'
alias ll='ls $LS_OPTIONS -l'
alias l='ls $LS_OPTIONS -lA'
alias tt='cd ~/tt && screen tt++ init.tt'
alias ck='vim ~/.termux/termux.properties'
```
此处tt命令就可以快速进入游戏。

## 2。screen、vim中文乱码

**tintin++原生不支持中文GBK编码</br>
使用screen进行转码**

### 利用screen给tt++转码

使用vim文本编辑器编辑：

> vim ~/.screenrc

按字母i键开启插入模式，方向键控制光标</br>
添加如下内容后保存：
```
defencoding GBK
```
将以上内容复制粘贴到文本中，</br>
修改完毕后按ESC键退出编辑模式：

- 输入:wq保存
- 或大写模式按两下ZZ键

只玩游戏做到这一步即可。

### vim编辑脚本时中文乱码

> vim ~/.vimrc

添加如下内容后保存：
```
set fileencodings=utf-8,ucs-bom,gb18030,gbk,gb2312,cp936
set termencoding=utf-8
set encoding=utf-8
```

### 手写脚本中文乱码转换编码

按ESC键退出编辑模式后输入下列命令：

> :set fileencoding=gb18030

## 3。初始init.tt脚本

### 利用screen启动tintin++客户端
> screen tt++

连接服务端使用#ses命令</br>
可选填账号密码参数，使用 ; 间隔
```
例:
#ses pku mud.pkuxkx.com 8080;username;password;
```
### 分屏

> #split

**最新的tt++2.01.8需要添加event
</br>
防止收回键盘后`screen redraw`异常**

> #event {SCREEN RESIZE} {#split}

**注**：另可将配置先写入到文件，</br>
然后使用配置文件启动游戏。
```
1.新建文件
vim init.tt
2.添加如下内容后保存
#split
#config charset big5
#event {SCREEN RESIZE} {#split}
#ses pku mud.pkuxkx.com 8080
```
### 进入游戏
> screen tt++ init.tt

### 管理配置文件

- 此处可将配置文件使用git上传至github，</br>
这样更换环境后克隆仓库即可快速使用配置。

- 或者安装ssh使用sftp或scp传输。

- tintin++官网提供了从电脑端`wintin++`使用chat传输配置的方法。

- Termux内建的termux-setup-storage接口可以在$home创建一个对内部存储的符号链接，我们可以直接访问内存卡或者建立相应目录的符号链接。
```
使用Termux管理的流程（本地推荐）：

1.建立符号链接
输入：termux-setup-storage
在弹出的权限要求中点击允许。
2.访问内存卡中的tt目录
cd $home/storage/shared/tt
3.内存卡中tt目录的符号链接到$home目录
ln -s storage/shared/tt $home/tt
4.通过符号链接进入内存卡的tt目录
cd tt
```
```
使用git管理的流程（远程推荐）：

1.克隆仓库
git clone https://github.com/zixijian/tt.git tt
2.进入仓库
cd tt
3.启动游戏
screen tt++ init.tt

更新新仓库内容输入指令（未启动游戏时）：
git pull

注：这里是xgg@pkuxkx的机器人脚本。
```

### screen 管理进程

- 组合键ctrl+a+d后台运行；
- screen -list 显示后台列表；
- screen -r <进程id或名称> 恢复进程到前台；

**注**：screen还能指定名称管理。

```
按组合键ctrl+a后，输入：
:sessionname xgg
回车确定，
按顺序按组合键ctrl+a+d进入后台，
screen -r xgg
返回游戏。
```

## 4。游戏指南

**Termux使用MXP验证fullme时**
</br>
**长按屏幕提取url再长按跳转到浏览器**

Termux可以直接调用浏览器访问链接

> termux-open-url <链接>

tintin++可以写触发器获取链接
```
#alias {fm} {fullme};
#alias {slink} {#showme $link};
#alias {mxp} {#sys termux-open-url $link};
#act {http://pkuxkx.com/antirobot/robot.php?filename=%1}
{
    #var link {http://pkuxkx.com/antirobot/robot.php?filename=%1};
    #sys termux-open-url $link;
}
#act {http://pkuxkx.net/antirobot/robot.php?filename=%1}
{
    #var link {http://pkuxkx.net/antirobot/robot.php?filename=%1};
    #sys termux-open-url $link;
}
```
**++新手推荐丐帮++**

丐帮拜师从扬州广场开始

> enter shudong;bai qiu

福利别忘了领哦

更多游戏信息访问|[北侠Wiki](http://pkuxkx.net/wiki/)|[北侠论坛](http://pkuxkx.net/forum/)|

## 5。机器人使用

### 逍遥行(城际公交)

**大部分地区可直接触发定位**

命令`gt`查看逍遥行帮助

命令`gt list`查看可去地点信息

命令`inquire list`查看地标房间信息

**Termux的xterm终端使用</br>PGDW PGUP上下翻页查看信息**

### 机器人实例：

**详见**|[TinTin++中文手册](./Wiki.md)|

## 6。天高任鸟飞

> 挂到你天~荒地也老。    --- by 鲁迅。

# END