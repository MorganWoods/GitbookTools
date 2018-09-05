---
description: operations in Shell
---

# Shell

## mac 🌀

* 查看 xcode 版本:  `xcodebuild -version`
* 查看系统位数  `uname -a`    x86\_64 表示系统为64位;  i686 表示系统32位的
*  常用文件位置

```text
1.驱动所在位置 /Systme/Library/Extensions ；
2.桌面的位置 /User/用户名/Desktop ；
3.文件通配符为星号 *  # 用来模糊搜索文件的,主要有*或?,可以代替一个或多个真正字符.
4.在 Unix系统中是区别大小写字符的，A.txt 不等于 a.txt。根目录标志 / 不是可有可无，
cd /System 表示转到跟目录下的System中，而cd System 表示转到当前目录下的 System中 。

~  #home 目录,/Users/Menghao/
.  #隐藏文件,在 gui 和 ls 下默认不显示,使用 ls -a 显示.
```

* Normal commands

```ruby
defaults writecom.apple.finder _FXShowPosixPathInTitle -boolYES 
#在 finder 上显示路径位置

killallFinder
​
defaults writecom.apple.screencapture location 存放位置 #改变截屏图片保存位置
killallSystemUIServer
​
say 'hello'#让电脑说话
sleep10&& say "hello"#10s 后提醒我 hello
​
chflags hidden ~/Desktop/Hidden #隐藏文件
你也可以使用 nohidden 重新让该文件夹显示。如果你要显示全部文件，
推荐大家直接使用快捷键「Shift +Command +.」即可显示全部隐藏文件。
​
defaults writecom.apple.finder CreateDesktop -boolfalse; killallFinder 
#关闭桌面所有图标 true 为还原
​
open .  #用 Finder 打开当前目录 🌏
​
显示所有文件：defaults writecom.apple.finder AppleShowAllFiles -booltrue
仅显示可见文件：defaults writecom.apple.finder AppleShowAllFiles -boolfalse

which ..   显示路径 ⚽️
.. version  显示版本 这个可能不对.
```

* uninstallation

  mac 下安装程序有两种dmg 和 pkg . 对于 dmg 直接在应用程序中删除, 但是 pkg 需要用命令删除.

```text
pkgutil --pkgs  #list all pkgs
```

### ➡brew

**包管理工具**:提供对一系列软件包的安装卸载升级的自动化工具.包管理工具分为:1,管理预编译好的软件\(binary installation/ precomplied packages\)如 app store 或 windows installer; 2,基于源码的安装包,通过编译脚本来安装软件\(sourcecode-based installation/using compile scripts\),如 homebrew 和 apt-build.

brew 的原理:从远程仓库下载软件的源代码,解压后执行命令./configure && make install 进行安装,并自动下载好相关依赖并配置好各种环境变量.

需要提前安装 Xcode,其里面包含 gcc 编译器. 安装 ruby, homebrew 基于 ruby 写的.  
所有软件默认安装目录: /usr/local/Cellar; 部分可执行脚本文件通过软链接到/usr/loca/bin 目录下,这样就可以在 terminal 下使用;  
[Homebrew](http://mxcl.github.io/homebrew/)对于Formula的管理是基于git的。你可以在`/usr/local/`下发现有一个`.git`的文件夹。通过查看`.git`目录下的`config`文件，可以知道其实目录是被链接到github上的一个repository。

brew cask是一套建立在homebrew 基础上的 mac 软件安装命令行工具.一般用来安装有 GUI 的软件, 命令如: `brew cask install sublime-text skitch dropbox google-chrome`

```text
brew search/install/upgrade/uninstall/update
brew home [] 用浏览器打开相关包的页面
brew info [] 显示包信息
brew deps [] 显示包依赖
brew server 启动web服务器，可以通过浏览器访问http://localhost:4567/ 来同网页来管理包
brew -h brew帮助
brew list   —列出已安装的软件
brew update   —更新Homebrew
brew doctor  自己检查
brew outdated 列出需要更新的软件
brew upgrade [] 更新某软件
brew cleanup 清楚所有软件的所有老版本
brew cleanup [] 清楚指定软件老版本.
```

## Ubuntu 🌀

* 我的ubuntu系统信息:

```text
cat   /etc/issue  
    #输出版本号:  Ubuntu 16.04.4 LTS \n \l

df -hl  # df 命令是linux系统以磁盘分区为单位查看文件系统.
    #输出:
    Filesystem      Size  Used Avail Use% Mounted on
    udev            1,9G     0  1,9G   0% /dev
    tmpfs           387M  6,3M  380M   2% /run
    /dev/sda11       46G   11G   33G  25% /
    tmpfs           1,9G   80M  1,9G   5% /dev/shm
    tmpfs           5,0M  4,0K  5,0M   1% /run/lock
    tmpfs           1,9G     0  1,9G   0% /sys/fs/cgroup
    /dev/sda10      453M  401M   25M  95% /boot
    /dev/sda12       62G   28G   32G  47% /home
    tmpfs           387M   76K  387M   1% /run/user/1000

sudo fdisk -l  # 查看物理硬盘分区
    Device     Boot      Start        End    Sectors   Size Id Type
    /dev/sda1  *          2048  209719295  209717248   100G  7 HPFS/NT
    /dev/sda2        209721342 1953523711 1743802370 831,5G  f W95 Ext
    /dev/sda5        209721344  924852223  715130880   341G  7 HPFS/NT
    /dev/sda6        924854272 1387290623  462436352 220,5G  7 HPFS/NT
    /dev/sda7       1387292672 1393686527    6393856   3,1G  7 HPFS/NT
    /dev/sda8       1638950912 1953523711  314572800   150G  7 HPFS/NT
    /dev/sda9       1393688576 1409310719   15622144   7,5G 82 Linux s
    /dev/sda10      1409312768 1410287615     974848   476M 83 Linux
    /dev/sda11      1410289664 1507944447   97654784  46,6G 83 Linux
    /dev/sda12      1507946496 1638934527  130988032  62,5G 83 Linux

```

* 常用目录解释

```text
/boot 引导程序，内核等存放的目录;存放引导加载器 (bootstraploader)使用的文件，
      如lilo，核心映像也经常放在这里，而不是放在根目录中。
      但是如果有许多核心映像，这个目录就可能变得很大，这时使用单独的文件系统会更好一些。
      还有一点要注意的是，要确保核心映像必须在ide硬盘的前1024柱面内。  
/bin 包含了引导启动所需的命令或普通用户可能用的命令(可能在引导启动后)。
     这些命令都是二进制文件的可执行程序(bin是binary-二进制的简称)，
     多是系统中重要的系统文件。
/sbin 类似/bin，也用于存储二进制文件。因为其中的大部分文件多是系统管理员使用的
      基本的系统程序，所以虽然普通用户必要且允许时可以使用，但一般不给普通用户使用。
/lib 共享库目录,根文件系统上的程序所需的共享库，存放了根文件系统程序运行所需的
     共享文件。这些文件包含了可被许多程序共享的代码，以避免每个程序都包含有相同的
     子程序的副本，故可以使得可执行文件变得更小，节省空间。 
/lib/modules   包含系统核心可加载各种模块，尤其是那些在恢复损坏的系统时
               重新引导系统所需的模块(例如网络和文件系统驱动)。
/dev 存放了设备文件，即设备驱动程序，用户通过这些文件访问外部设备。
     比如，用户可以通过访问/dev/mouse来访问鼠标的输入，就像访问其他文件一样。
/root 用户root的home目录,超级用户的目录.
/etc 存放着各种系统配置文件，其中包括了用户信息文件/etc/passwd， 环境变量也在这里.
     系统初始化文件/etc/rc等。linux正是*这些文件才得以正常地运行。
     最早命名为 etcetra directory, 类似于其他目录
/mnt 目录是系统管理员临时装载(mount)文件系统的安装点。程序并不自动支持安装到/mnt。
     /mnt下面可以分为许多子目录，例如/mnt/dosa可能是使用msdos文件系统的软驱，
     而/mnt/exta可能是使用ext2文件系统的软驱，/mnt/cdrom光驱等等。
/proc 系统内部一些信息 
/var 某些大文件的溢出区，比方说各种服务的日志文件
/tmp 临时目录 系统断电 或许目录被会清空;存放程序在运行时产生的信息和数据 
/lost+found 当系统崩溃的时候，在系统修复过程中需要恢复的文件，
               可能就会在这里被找到了，这个目录一般为空

/usr 用户安装目录 
/usr/include C程序语言编译使用的头文件 
/usr/bin 应用程序
/usr/sbin 超级用户的一些管理程序
/usr/doc linux文档
/usr/lib 常用的动态链接库和软件包的配置文件
/usr/man 帮助文档 manual 的缩写;
/usr/src 源代码，linux内核的源代码就放在/usr/src/linux里
/usr/local/bin 本地增加的命令
/usr/local/lib 本地增加的库
```

### ➡ 常用命令

```r
su   #   Swith user  切换用户，切换到root用户
cat   # Concatenate  串联
uname   # Unix name  系统名称
df   # Disk free  空余硬盘
du   # Disk usage 硬盘使用率
chown   # Change owner 改变所有者
chgrp   # Change group 改变用户组
ps   # Process Status  进程状态
tar   # Tape archive 解压文件
chmod   # Change mode 改变模式
umount   # Unmount 卸载
ldd   # List dynamic dependencies 列出动态相依
insmod   # Install module 安装模块
rmmod   # Remove module 删除模块
lsmod   # List module 列表模块
alias    # Create your own name for a command
bash    # GNU Bourne-Again Shell  linux内核 
grep   # global regular expression print
httpd    # Start Apache
ipcalc    # Calculate IP information for a host
ping    # Send ICMP ECHO_Request to network hosts
reboot   #  Restart your computer
sudo   # Superuser do
cd/ #切换到根目录 change directory
ls参数 目录名 #列出文件列表  list
mkdir#建立新目录  make directory
cp参数 源文件 目标文件 #拷贝文件
rm参数 文件 #删除文件
rmdir文件夹#删除文件夹
mv文件 #移动文件
nano 文件名 #编辑文件
vim文件名 #编辑文件
pwd #显示路径名  Print Working Directory
cat文件名 #显示或链接文件; Concatenate 链接,串联
file 文件名 #显示文件类型
date #显示系统当前日期时间
cal #显示日历
time 程序文件 #统计程序执行时间
history #显示最近执行过的命令及编号
r -2#重复执行上命令列出的第二条命令
alias #给某个命令定义别名
unalias #取消定义的别名
uname #显示操作系统相关信息 
clear#清屏
who#显示当前所有设置过的环境变量
tty #显示终端或为终端的命长
w #显示当前系统活动的总信息

df -h 查看空间内存
uname -r 当前运行内核
sudo apt --fix-broken install

用make -j带一个参数，可以把项目在进行并行编译，比如在一台双核的机器上，完全可以用make -j4，让make最多允许4个编译命令同时执行，这样可以更有效的利用CPU资源。

touch 是 新建文件   
cp 是复制   cp 老文件 新文件   
mv 剪切
mkdir 创建文件夹
rmdir 移除空文件夹
rm 移除单个文件   -i 交互式的 interactive
rm -r 文件夹 移除文件夹可以为空   (r 是 recursively)
cat 显示文件内容  catenate
chmod 修改权限
ssh 远程控制,同一个路由下
dpkg -l | grep 安装包  找到当前安装的包, sudo aptget remove 
```

#### ➡ ➡  apt-get

* 常用命令 \[apt-get 是 ubuntu 系统的包管理命令, 在 mac os上对应的是 brew

```text
apt-cache show packagename              #获取包的相关信息，如说明、大小、版本等
apt-cache depends packagename           #了解使用依赖
apt-cache rdepends packagename          #是查看该包被哪些包依赖
apt-get install packagename             #安装包
apt-get install package=version         #指定安装版本
apt-get install packagename --reinstall #重新安装包
apt-get remove packagename --purge      #卸载程序，包括删除配置文件等
apt-get update                          #更新源,更新 /etc/apt/sources.list里的链接地址
apt-get upgrade -u                      #升级程序(不包括依赖关系改变的) -u 完整显示列表
apt-get dist-upgrade                    #升级程序(包括依赖关系改变的并且重新组织依赖关系)
apt-get clean                           #删除安装包(节约硬盘空间,下次安装需要重新下载包，软件包位置：/var/cache/apt/archives/)
apt-get autoclean                       #删除已卸载的安装包(Ubuntu14.04测试发现没起作用)
apt-get autoremove                      #卸载依赖的程序
```

* apt-get的安装位置 下载后的软件存放于 /var/cache/apt/archives  安装后软件默认存放 /usr/share  可执行文件位置    /usr/bin  lib 文件位置     /usr/lib

#### ➡ ➡  几种安装方法总结

```text
1.编译安装#
./configure#make#make install
2.python脚本#
python xxx.py
3.bin#
chmod +x xxx.bin#./xxx.bin
4.rpm包#
rpm -i xxx.rpm
5.deb包#
dpkg -i xxx.deb
6.apt#
apt-get install xxx
7.yum#
yum install xxx
建议：安装前先查看安装包内的安装手册，一般都会有详细的说明。
```

## General 🌀

### ➡通用命令

```text
echo  # 在终端显示文字,一般用来做提示用, 就是回音的意思.
export [-fnp][变量名称]=[变量设置值] #设置或显示环境变量; -f 代表变量名称是函数;   
                                  -n 删除指定的变量,实际未删除,只是后续操作中被删除
                                  -p 列出所有 shell 赋予的环境变量.
export $PATH="路径”(或“PATH=$PATH:路径”)   # 该命令只是单次有效,并未修改,所以 zsh 文件中是 export 的句子
touch #创建文件
```

#### ➡ ➡ ln

ln是linux中又一个非常重要命令，它的功能是为某一个文件在另外一个位置建立一个同步的链接.当我们需要在不同的目录，用到相同的文件时，我们不需要在每一个需要的目录下都放一个必须相同的文件，我们只要在某个固定的目录，放上该文件，然后在 其它的目录下用ln命令链接（link）它就可以，不必重复的占用磁盘空间。

命令格式：  
 ln \[参数\]\[源文件或目录\]\[目标文件或目录\]

2．命令功能：

Linux文件系统中，有所谓的链接\(link\)，我们可以将其视为档案的别名，而链接又可分为两种 : 硬链接\(hard link\)与软链接\(symbolic link\)，硬链接的意思是一个档案可以有多个名称，而软链接的方式则是产生一个特殊的档案，该档案的内容是指向另一个档案的位置。硬链接是存在同一个文件系统中，而软链接却可以跨越不同的文件系统。

软链接：

1.软链接，以路径的形式存在。类似于Windows操作系统中的快捷方式  
2.软链接可以 跨文件系统 ，硬链接不可以  
3.软链接可以对一个不存在的文件名进行链接  
4.软链接可以对目录进行链接

硬链接:

1.硬链接，以文件副本的形式存在。但不占用实际空间。  
2.不允许给目录创建硬链接  
3.硬链接只有在同一个文件系统中才能创建

  这里有两点要注意：

第一，ln命令会保持每一处链接文件的同步性，也就是说，不论你改动了哪一处，其它的文件都会发生相同的变化；

第二，ln的链接又分软链接和硬链接两种，软链接就是ln –s 源文件 目标文件，它只会在你选定的位置上生成一个文件的镜像，不会占用磁盘空间，硬链接 ln 源文件 目标文件，没有参数-s， 它会在你选定的位置上生成一个和源文件大小相同的文件，无论是软链接还是硬链接，文件都保持同步变化。

ln指令用在链接文件或目录，如同时指定两个以上的文件或目录，且最后的目的地是一个已经存在的目录，则会把前面指定的所有文件或目录复制到该目录中。若同时指定多个文件或目录，且最后的目的地并非是一个已存在的目录，则会出现错误信息。

3．命令参数：

必要参数:  
-b 删除，覆盖以前建立的链接  
-d 允许超级用户制作目录的硬链接  
-f 强制执行  
-i 交互模式，文件存在则提示用户是否覆盖  
-n 把符号链接视为一般目录  
-s 软链接\(符号链接\)  
-v 显示详细的处理过程

选择参数:  
-S “-S&lt;字尾备份字符串&gt; ”或 “--suffix=&lt;字尾备份字符串&gt;”  
-V “-V&lt;备份方式&gt;”或“--version-control=&lt;备份方式&gt;”  
--help 显示帮助信息  
--version 显示版本信息

### ➡ pip

> pip 是 python 的包管理工具,所以安装路径在 python 的路径下;

```text
pip list 列出当前环境下安装的所有包
pip help
安装python包
pip install <包名>
pip install <包名> -i http://pypi.mirrors.ustc.edu.cn/simple/
pip install -e < local project path>
pip install -r requirements.txt

pip show -f <包名>  #查看安装的包所在目录❤️
pip show
pip install –e ‘.[all]’进行完全安装。
git clone xxx.git
git clone xxx.git "指定目录"
python 的包有以 egg 命名的
pip install -v pycrypto==2.3   安装指定版本包
```

### ➡ conda

> 著名的开源 python 发行版本,包含 conda, python 等科学包依赖.  
> Anaconda 可以用于创建独立的 python 开发运行环境,每个环境中的 python 独立的.

* conda 常用命令

```text
conda create -npy35 python=3.5  #创建虚拟环境
source activate py35             #激活环境 ※
conda install numpy              #conda 安装
conda install anaconda    
conda info --envs               #查看当前活动的环境  ※
conda search python
conda install pandas=0.13.0
conda update conda
conda update ipython
conda list                       #查看当前环境下已安装的包
conda list -n python34           #查看某个指定环境的已安装包
conda search numpy               #查找package信息
# 安装package
conda install -npython34 numpy
# 如果不用-n指定环境名称，则被安装在当前活跃环境
# 也可以通过-c指定通过某个channel安装
conda update -npython34 numpy   # 更新package
conda remove -npython34 numpy   # 删除package
conda info -e #列出所有环境
```

### ➡ Docker

> 数据卷 volume ; 仓库 Repository ; 标签 tag ; registry 档案室,注册处 ;

#### ➡ ➡ 介绍

Docker 的项目代码在 github 上, 其属于系统层面的虚拟化技术.由于隔离的进程独立于宿主和其它的隔离的进程, 因此也称为容器. 容器比传统虚拟机更加轻便,因为他连内核都不用;

Docker 与传统虚拟化方式相比具有众多优势:  
高效利用系统资源: 速度,损耗,存储等都好与传统虚拟机技术.相比虚拟机技术,一个同配置主机能运行更多数量应用  
更快启动时间:容器中的应用运行于宿主内核,无需启动完整的操作系统,  
一致的运行环境.持续交付和部署,更轻松的迁移; 更轻松的维护和扩展.

* Docker 镜像 操作系统分为内核和用户空间, 对于 linux,内核启动后挂载 root 文件系统为其提供用户空间支持. 而 Docker Image 相当于是一个 root 文件系统. 除了提供容器运行时所需的程序.库,资源,配置文件外,还包含了一些为运行时准备的配置参数,如匿名卷,环境变量,用户等.
* 分层存储 分层存储架构.镜像构建时,会一层层构建,前一层是后一层的基础.每一层构建完不改变.后一层的任何改变只是发生在自己这层, 现在不影响过去, 比如当前删除前一层的操作,只是在当前层标记前一层操作被删除,但不是真的删除.在最终运行时,虽然不会看到这个文件,但是实际上该文件会一直跟随镜像.
* 容器 container

  Image 与 container 的关系如 类 和 实例 一样,镜像是静态的定义,容器是镜像运行时候的实体.容器可以被创建,启动,停止,删除,暂停等.  
  容器的实质是进程,但与直接在宿主执行的进程不同,容器进程运行于属于自己的命名空间中, 因此容器拥有自己的 root 文件系统,自己的网络配置,自己的进程空间,甚至自己的用户 id 空间.容器内的进程运行在一个隔离的环境中.使用起来就像完全独立的一样.具有隔离特性.  
  容器运行时, 是以镜像为基础层,在其上创建的一个当前容器的存储层.

* Docker registry 一个 Docker registry 中可以包含多个仓库 repository ; 每个repository 包含多个 tag, 每个 tag 对应一个镜像;
* 安装 Docker 分为 CE 和 EE 版本, CE 是社区版,免费,EE 是企业版付费;

#### ➡ ➡ 命令

```text
docker --version   ;   
docker-compose --version  ;  
docker-machine --version  ;
docker run  - 启动docker容器
--rm  - 一旦启动完成，删除容器
-e DOCKER_NET_HOST=172.17.0.1  
- 启动时告诉universe远程VNC连接到这个Docketr分配的IP
-v /var/run/docker.sock:/var/run/docker.sock 
- 使主机上的docker unix socket可用于容器。这功能常用于允许容器在其自身旁启动其他容器。
universe  - 使用上面构建的名为“Universe”的镜像
pytest  - 在容器中运行“pytest”，即运行所有测试
```

### ➡ Zsh

Zsh 和 bash 一样是功能强大的终端 shell 软件.bash 是大部分 linux 发行版默认的 shell, 而 Zsh 需要手动安装\(mac 默认安装\). 既可以作为交互式终端,也可以作为脚本解释器. zsh 兼容 bash 前者更好; 名字是耶鲁大学一个华人教授命名的 z shell , 简称 zsh; bash 的全称是Bourne-Again _SHell._  
shell 的命令历史记录保存在~/.zsh\_history 文件中,可用箭头查找; 可用 !! 执行上一条命令; 可用 ctrl-r 搜索命令历史记录.

* 启动过程 `/etc/zsh/zshenv`该文件应该包含用来设置[PATH 环境变量](https://wiki.archlinux.org/index.php/Zsh_%28%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87%29#Configuring_.24PATH)以及其他一些[环境变量](https://wiki.archlinux.org/index.php/Environment_variables)的命令；不应该包含那些可以产生输出结果或者假设终端已经附着到 tty 上的命令。 `~/.zshenv`该文件和 `/etc/zsh/zshenv` 相似，但是它是针对每个用户而言的。一般来说是用来设置一些有用的环境变量。 `/etc/zsh/zprofile`这是一个全局的配置文件，在用户登录的时候加载。一般是用来在登录的时候执行一些命令。请注意，在 Arch Linux 里该文件默认包含[一行配置](https://projects.archlinux.org/svntogit/packages.git/tree/trunk/zprofile?h=packages/zsh)，用来加载 `/etc/profile` 文件，详见 [\#全局配置文件](https://wiki.archlinux.org/index.php/Zsh_%28%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87%29#.E5.85.A8.E5.B1.80.E9.85.8D.E7.BD.AE.E6.96.87.E4.BB.B6)。 `/etc/profile`在登录时，该文件应该被所有和伯克利（Bourne）终端相兼容的终端加载：它在登录的的时候会加载应用相关的配置（`/etc/profile.d/*.sh`）。注意在 Arch Linux 里，Zsh 会默认加载该文件。 `~/.zprofile`该文件一般用来在登录的时候自动执行一些用户脚本。 `/etc/zsh/zshrc`当 Zsh 被作为交互式终端的时候，会加载这样一个全局配置文件。 `~/.zshrc`当 Zsh 被作为交互式终端的时候，会加载这样一个用户配置文件。⛳️ `/etc/zsh/zlogin`在登录完毕后加载的一个全局配置文件。 `~/.zlogin`和 `/etc/zsh/zlogin` 相似，但是它是针对每个用户而言的。 `/etc/zsh/zlogout`在注销的时候被加载的一个全局配置文件。 `~/.zlogout`和 `/etc/zsh/zlogout` 相似，但是它是针对每个用户而言的.
* oh my zsh

  体验很好的开源工具.

```text
echo $SHELL  #查看自己使用的是什么终端.
替换bash的方式：chsh -s /bin/zsh。关闭终端，再次打开即为zsh。
source ~/.zshrc 生效修改的配置.
```

### ➡ PATH

Environmental variable is a dynamic-named value affect the way running processes will behave on a computer.  
Linux 中环境变量包括系统级和用户级.  
.bash\_profile是用户登录会被读的 .bashrc是用户不登录也会被读的 .zshrc是用户登录、不登录都会被读的。

```text
# 软件名-版本号
PATH=$PATH:路径1:路径 2:...:路径n    #PATH 变量的分隔符是冒号,
echo $PATH #显示当前环境变量.
```

```text
系统级目录：
/etc/profile：该文件是用户登录时，操作系统定制用户环境时使用的第一个文件，
               应用于登录到系统的每一个用户。该文件一般是调用/etc/bash.bashrc文件。
/etc/bash.bashrc：系统级的bashrc文件。
/etc/environment:在登录时操作系统使用的第二个文件,系统在读取你自己的profile前,
               设置环境文件的环境变量。

用户级（这些文件处于home目录下）：
~/.profile:每个用户都可使用该文件输入专用于自己使用的shell信息,当用户登录时,该文件仅仅执行一次!
           默认情况下,他设置一些环境变量,执行用户的.bashrc文件。这里是推荐放置个人设置的地方
~/.bashrc:该文件包含专用于你的bash shell的bash信息,当登录时以及每次打开新的shell时,
          该该文件被读取。不推荐放到这儿，因为每开一个shell，这个文件会读取一次，效率肯定有影响。               
```

```text
常见的环境变量:
　　$PATH：决定了shell将到哪些目录中寻找命令或程序
　　$HOME：当前用户主目录
　　$MAIL：是指当前用户的邮件存放目录。
　　$SHELL：是指当前用户用的是哪种Shell。
　　$HISTSIZE：是指保存历史命令记录的条数
　　$LOGNAME：是指当前用户的登录名。
　　$HOSTNAME：是指主机的名称，许多应用程序如果要用到主机名的话，通常是从这个环境变量中来取得的。
　　$LANG/LANGUGE：是和语言相关的环境变量，使用多种语言的用户可以修改此环境变量。

使用 echo 可以显示环境变量内容.
使用 env 显示所有环境变量.
使用 set 显示所有本地定义的 Shell 变量

　　5.2 设置一个新的环境变量
　　$ export HELLO=“Hello!”
　　$ echo $HELLO
　　Hello!

```

### ➡ Make

makefile关系到了整个工程的编译规则。一个工程中的源文件不计数，其按类型、功能、模块分别放在若干个目录中，makefile定义了一系列的规则来指定，哪些文件需要先编译，哪些文件需要后编译，哪些文件需要重新编译，甚至于进行更复杂的功能操作，因为makefile就像一个Shell脚本一样，其中也可以执行操作系统的命令。

make 从 makefile 中读取指令,然后编译.  
make install 是用来安装的,也是从 makefile 中读取指令,安装到指定位置.

代码变成可执行文件叫做 **编译 compile**; 编译过程中的先后次序安排叫做 **构建 build**.   
Make 是最常用的 build 工具,1977年出生;主要用于 c 语言项目.但实际中,任何只要某个文件有变化就要重新构建的项目,都可以用 make 来 build.  
构建过程中需要的文件以及规则卸载 Makefile 中, make命令依赖这个文件进行工作; makefile 文件可以自己改名字, make 时候需要指出 如: make --file=rules.txt ;

#### ➡ ➡ Makefile 文件由一系列 rules 构成

```text
<target> : <prerequisites>  
[tab]  <commands>
```



#### ➡ ➡ configure

configure, 一般用来生成 makefile 的,为下一步的编译做准备.可以通过在 configure 后加上参数来对安装进行控制.

```text
./configure –prefix=/usr  #意思是将该软件安装在 /usr 下面,
        执行文件就会安装在 /usr/bin （而不是默认的 /usr/local/bin),
        资源文件就会安装在 /usr/share（而不是默认的/usr/local/share）。
        同时一些软件的配置文件你可以通过指定 –sys-config= 参数进行设定。
        有一些软件还可以加上 –with、–enable、–without、–disable 等等参数对编译加以控制，
        你可以通过允许 ./configure –help 察看详细的说明帮助。
        
./configure  #运行脚本
```

configure是一个shell脚本，它可以自动设定源程序以符合各种不同平台上Unix系统的特性，并且根据系统叁数及环境产生合适的Makefile文件或是C的头文件\(header file\)，让源程序可以很方便地在这些不同的平台上被编译连接。运行configure脚本，就可产生出符合GNU规范的Makefile文件了：

#### ➡ ➡ makefile 的选项 

```text
LDFLAGS 是选项,告诉连接器去哪找库文件，库的路径
        gcc 等编译器会用到的一些优化参数，也可以在里面指定库文件的位置。
        用法：LDFLAGS=-L/usr/lib -L/path/to/your/lib。每安装一个包都几乎一定的会在
        安装目录里建立一个lib目录。如果明明安装了某个包，而安装另一个包时，
        它愣是说找不到，可以抒那个包的lib路径加入的LDFALGS中试一下。
LIBS       告诉连接器都需要用哪个库。需要啥库 告诉链接器要链接哪些库文件.如LIBS = -lpthread -liconv
           都是喂给ld的，只不过一个是告诉ld怎么吃，一个是告诉ld要吃什么。
CFLAGS  表示用于 c 编译器的选项,制定头文件.h 的路径,如 , CFLAGS=-I/usr.../include. 
        同样的.安装一个包时会在安装路径下简历一个 include 目录.当安装过程中出现问题时，
        试着把以前安装的包的include目录加入到该变量中来。
CXXFLAGS 表示用于 C++ 编译器的选项。        

```

如果在执行./configure以前设置环境变量export LDFLAGS="-L/var/xxx/lib -L/opt/mysql/lib -Wl,R/var/xxx/lib -Wl,R/opt/mysql/lib" ，注意设置环境变量等号两边不可以有空格，而且要加上引号（shell的用法）。那么执行configure以后，Makefile将会设置这个选项，链接时会有这个参数，编译出来的可执行程序的库文件搜索路径就得到扩展了。

| 后缀 | 所对应的语言 |
| :--- | :--- |
| -S | 只是编译不汇编，生成汇编代码 |
| -E | 只进行预编译，不做其他处理 |
| -g | 在可执行程序中包含标准调试信息 |
| -o file | 把输出文件输出到file里 |
| -v | 打印出编译器内部编译各过程的命令行信息和编译器的版本 |
| -I dir | 在头文件的搜索路径列表中添加dir目录 |
| -L dir | 在库文件的搜索路径列表中添加dir目录 |
| -static | 链接静态库 |
| -llibrary | 连接名为library的库文件 |

#### ➡ ➡ CMake

由于 make 不支持跨平台,每当换了平台之后需要重新写 makefile 文件,非常麻烦.这时候出现了 CMake 工具.  
进化关系: gcc -&gt; make -&gt; Cmake

全称为 Cross platform make, 是一个开源的跨平台自动化构建系统.使用指定名为 CMakeLists.txt 的配置文件控制安装测试打包等流程. 类似的 make 工具有很多, Autocof, JAM, QMake, SCons, ANT 等. CMake 是一种跨平台编译工具,比 make 更为高级,使用起来更方便;   
工作流程: CMake 编写 CMakeLists 文件,然后用 cmake 命令将文件转化为 make 所需要的 makefile 文件,然后用 make 命令编译源码生成可执行程序或共享库.



### ➡ other terms

#### ➡ ➡ GCC

GNU **编译器**套装 GNU Compiler Collection. 一套编程语言编译器. 处理 C 和 C ++ 语言 之后扩展能处理更多语言; Unix 系统和 Linux 及BSD 家族都采用 GCC 作为标准编译器. GCC 是无所不在的.他是跨平台编译器;

当程序只有一个源文件时,就可以用 gcc 命令编译它;当有多个文件时,就要用 make 工具, **make 工具相当于批量化的 GCC 工具**. makefile 命令中包含调用 gcc 或别的编译器去编译和链接.

#### ➡ ➡ LLVM

是一个自由软件项目,一种编译器基础设施,以 c++写成.是为了任意一种编程语言写成的程序,利用虚拟技术创造出编译时期,链接时期,运行时期,及闲置时期的最优化.现在是 mac 开发工具的一部分.  
Low level Virtual Machine,底层虚拟机.

#### ➡ ➡ Clang

是 c 语言 c++等编译器前端,采用了 LLVM 底层虚拟技术作为其后端.他的目标是提供一个 GNU CC 的替代品.支持了 GCC 的大多数编译设置及非官方语言扩展.苹果公司支持.

#### ➡ ➡ GNU

GNU 是一个自由的操作系统;内容完全以 GPL 方式发布.名称是 GNU's not unix. 其类似 unix. 是个操作系统,但仍未完成.

#### ➡ ➡ BSD

Berkeley Software Distribution, 伯克利软件套件.是一个操作系统名称.衍生自 unix. 现在其被当做工作站级别的 Unix 系统.这归功于 BSD 用户许可证非常宽松.许多早期计算机公司都从中获益.

#### ➡ ➡ Go

Go 或 Golang, 是谷歌开发的编程语言,与2007年计划出生;2009年出生,称为开源项目,并在 linux 和 osx 上实现,后来追加到 windows 系统下的实现; 近似 c 语言,但对于变量的声明有些不同,go 支持垃圾回收♻️功能.其并行模型基于霍尔的通信顺序进程 SCP. 不同于 java,go 内嵌了关联数组,也称哈希表 hashes 或字典 dictionaries,像字符串类型一样.

### ➡ library

#### ➡ ➡ libjpeg-turbo

libjpeg-turbo, turbo 是涡轮机的意思; 是 ligjpeg 的一个复刻;它采用单指令多数据流\(SIMD\)指令来加速 JPEG 编码和解码基础效率.许多项目使用 turbo 版而不是原版;

#### ➡ ➡ go\_vncdriver

 是一个快速的 vnc driver, go 语言; vnc:可能是 virtual network console.

### ➡ commands form

* 横线 - 与 --

  - 与 -- 是两种不同的命令行选项风格,前者是传统 Unix 风格,后者是 GNU 风格; - 一般是选项 options, 如 横线后加单独字母:   -a 是 all, -c 是 command, -f 表示 file, -V 表示 version. 多个选项可以连写;  
  由于单独字母数量有限不够用,于是有了后来的 GNU 风格完善; 使用 -- 作为前缀加个单词: --version, --all, 这些选项自己的参数可以放在后面用空格或=隔开,如「--file foobar.out」等价于「--file=foobar.out」。这种GNU风格的选项常被称之为『长选项』（Long Options），而Unix风格的为『短选项』（Short Options）。通常来说短选项都有与之对应的长选项，如「-a，--all」、「-V，--version」。

### ➡ boost python

是boost 库的一部分.随着 boost 一起安装,实现 c++ 和 python 代码交互.

## Editor 🌀

### ➡ Vim

```text
'''打开文件'''
vim filename  # 打开文件
vim file1 file2 file3 #打开多个文件
​
'''vim 的三种模式'''
# 命令模式 (默认, 按 Esc, 按 Ctrl+[ ,进入) 左下角显示文件名或空
# 插入模式 (按 i 进入) 左下角显示 --INSERT-- ; Esc 关闭插入模式
# 可视模式 ()左下角显示 --VISUAL--
​
'''退出命令'''#在命令模式下操作
:wq , :x #保存并退出🌀
:w #保存
:q #关闭
:q! #强制退出并忽略更改
:e! #放弃所有修改,并打开原来文件
​
'''移动光标'''
h,j,k,l # ←,↓,→,↑ 
Ctrl f # 下一页 🌀   ctrl b # 上一页 🌀 
0 或 home #移到行首 🌀   $ 或 end  #移到行尾 🌀
( # 移到上一句首 🌀    ) # 移到下一句首 🌀
​
'''编辑 (命令模式)'''
u  #撤销上一步操作 undo 🌀
Ctrl r #恢复上一步操作 redo 🌀
​
'''帮助'''
:help


```

### ➡ Gedit

### ➡ Nano

### ➡ Jupyter

Anaconda 附带默认安装的软件有著名的 Jupyter Notebook （官网 [http://jupyter.org](https://link.jianshu.com?t=http%3A%2F%2Fjupyter.org) ）这个 Python 的交互式笔记本，支持运行40 多种编程语言。Jupyter Notebook 的本质是一个Web 应用程序，便于创建和共享文学化程序文档，支持实时代码，数学方程，可视化和 Markdown，还可以插入图片，视频，音频，等等。

Type `jupyter notebook` to launch the [Jupyter Notebook App](https://jupyter-notebook-beginner-guide.readthedocs.io/en/latest/what_is_jupyter.html#notebook-app) The notebook interface will appear in a new browser window or tab.

The _Jupyter Notebook App_ is a server-client application that allows editing and running [notebook documents](https://jupyter-notebook-beginner-guide.readthedocs.io/en/latest/what_is_jupyter.html#notebook-document) via a web browser. The _Jupyter Notebook App_ can be executed on a local desktop requiring no internet access \(as described in this document\) or can be installed on a remote server and accessed through the internet.  
In addition to displaying/editing/running notebook documents, the _Jupyter Notebook App_ has a “Dashboard” \([Notebook Dashboard](https://jupyter-notebook-beginner-guide.readthedocs.io/en/latest/what_is_jupyter.html#dashboard)\), a “control panel” showing local files and allowing to open notebook documents or shutting down their [kernels](https://jupyter-notebook-beginner-guide.readthedocs.io/en/latest/what_is_jupyter.html#kernel).

A notebook _kernel_ is a “computational engine” that executes the code contained in a [Notebook document](https://jupyter-notebook-beginner-guide.readthedocs.io/en/latest/what_is_jupyter.html#notebook-document). The _ipython kernel_, referenced in this guide, executes python code. Kernels for many other languages exist \([official kernels](http://jupyter.readthedocs.org/en/latest/#kernels)\).

When you open a [Notebook document](https://jupyter-notebook-beginner-guide.readthedocs.io/en/latest/what_is_jupyter.html#notebook-document), the associated _kernel_ is automatically launched. When the notebook is _executed_ \(either cell-by-cell or with menu _Cell -&gt; Run All_\), the _kernel_ performs the computation and produces the results. Depending on the type of computations, the _kernel_ may consume significant CPU and RAM. Note that the RAM is not released until the _kernel_ is shut-down.

浏览器是界面, 后台服务器是 IPython. shift Enter 运行 cell, 如果希望屏蔽输出，可以在最后一条语句之后添加一个分号：”;”

打开命令行，切换到某个目录下，输入ipython notebook。它会启动服务器，并打开浏览器。  
它会自动读取该目录下面的.ipynb文件.并显示。  
如果要新建一个文件的话 点按钮`New notebook`就好了。

Closing the browser \(or the tab\) **will not close** the [Jupyter Notebook App](https://jupyter-notebook-beginner-guide.readthedocs.io/en/latest/what_is_jupyter.html#notebook-app). To completely shut it down you need to **close the associated terminal**.  
In more detail, the [Jupyter Notebook App](https://jupyter-notebook-beginner-guide.readthedocs.io/en/latest/what_is_jupyter.html#notebook-app) is a server that appears in your browser at a default address \(_http://localhost:8888_\). Closing the browser will not shut down the server. You can reopen the previous address and the [Jupyter Notebook App](https://jupyter-notebook-beginner-guide.readthedocs.io/en/latest/what_is_jupyter.html#notebook-app) will be redisplayed.

## Other ✡️

```text
打开 tensorboard ; tensorboard --logdir logs

PATH 的语法为: #中间用冒号隔开export PATH=$PATH:<PATH 1>:<PATH 2>:<PATH 3>:------:<PATH N>
export PATH="$HOME/.rbenv/bin:$PATH"    
新增环境变量的mac 环境变量配置  vi ~/.bash_profile

source ~/.bash_profile 修改立即生效
 

```

### ➡ Github

#### ➡ ➡ 修改文件 ※

```python
git add<file> # 修改文件后运行这句,跟踪文件,可以依次跟踪多个文档,依次向后排列;添加当前仓库所有文件时直接使用 git add .
git commit-m'some words' #提交文件,一次性提交所有文件
git push originmaster# 推送修改文件到远程仓库
​
git status# 查看文件状态,
```

#### ➡ ➡ 常用命令查询

> [https://coding.net/help/doc/git/push.html](https://coding.net/help/doc/git/push.html)

```python
# 创建版本库
git clone <url>                  #克隆远程版本库
git init                         #初始化本地版本库
# 修改和提交
git status                       #查看状态
git diff                        #查看变更内容
git add .                        #跟踪所有改动过的文件
git add <file>                   #跟踪指定的文件
git mv<old><new>                #文件改名
git rm<file>                     #删除文件
git rm--cached<file>            #停止跟踪文件但不删除
git commit -m"commit messages" #提交所有更新过的文件
git commit --amend              #修改最后一次改动
# 查看提交历史
git log                    #查看提交历史
git log -p<file>          #查看指定文件的提交历史
git blame <file>           #以列表方式查看指定文件的提交历史
# 撤销
git reset --hardHEAD      #撤销工作目录中所有未提交文件的修改内容
git checkout HEAD <file>   #撤销指定的未提交文件的修改内容
git revert <commit>        #撤销指定的提交
git log --before="1 days" #退回到之前1天的版本
# 合并
git merge <branch>        #合并指定分支到当前分支
git rebase <branch>       #衍合指定分支到当前分支
# 远程操作
git remote -v                  #查看远程版本库信息
git remote show <remote>        #查看指定远程版本库信息
git remote add <remote> <url>   #添加远程版本库
git fetch <remote>              #从远程库获取代码
git pull <remote> <branch>      #下载代码及快速合并
git push <remote> <branch>      #上传代码及快速合并
git push <remote> :<branch/tag-name>  #删除远程分支或标签
git push --tags                      #上传所有标签
​
# 分支与标签
$ git branch                   #显示所有本地分支
$ git checkout <branch/tag>    #切换到指定分支和标签
$ git branch <new-branch>      #创建新分支
$ git branch -d<branch>       #删除本地分支
$ git tag                      #列出所有本地标签
$ git tag <tagname>            #基于最新提交创建标签
$ git tag -d<tagname>         #删除标签
​
# 强制覆盖命令
git push --force
​
```

#### ➡ ➡ 初始化 Github 仓库

在网页中新建仓库, 本地克隆版本库,

```text
gitclonegit@github.com:freelighting/NoteBook.git
```

在本地文件夹中创建 README.md 文件, 添加 README 文件并且提交\(commit 是提交的意思 -m: --message\)

```text
gitaddREADME.md 
gitcommit-m "READEME for my project."
```

向 GitHub 推送,完成版本初始化  

```text
gitpushoriginmaster
```

#### ➡ ➡ 删除部分文件

先在本地删除文档,然后提交\(-a: --all commit all changed files \)  

```text
gitrm<path><file>
gitcommit-a-m"a file was deleted"
gitpushoriginmaster
```

#### ➡ ➡ Gitbook

以后尝试用这gitbook 记笔记吧. 等有精力再弄.



##  NaN

## NaN

## NaN

## NaN

## NaN



