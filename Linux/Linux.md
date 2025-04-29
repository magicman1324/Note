# Linux

## 系统

Windows Linux Unix

## 发行版

Debian,Ubuntu,CentOS,Fedora,Red Hat Enterprise Linux,Arch Linux,OpenSUSE

Debian-->>Ubuntu,Kali,Kanotix

Red Hat Enterprise Linux-->>CentOS

Fedora-->>Red Hat Enterprise Linux,Berry Linux,Moblin

OpenSUSE-->>OpenSUSE Tumbleweed,OpenSUSE Leap,OpenSUSE MicroOS

## 学习部分

### 1.Linux kernel 内核

### 2.GNU 工具

### 3.GNU Desktop 环境

### 4.Application 应用

![](../imgs/组成.png)

## Linux 内核：操作系统

1.硬件设备 管理使用

2.软件程序---》操作软件

3.系统内存

4.文件管理 保存，删除，修改文件

### Linux文件系统：读和写的标准

```
 文件系统  -  Linux  支持的文件系统类型：ext,  ext2, ext3, ext4, hpfs, iso9660, JFS, minix,
       msdos, ncpfs, nfs, ntfs, proc, Reiserfs, smb, sysv, umsdos, vfat, XFS, xiafs
```

ubuntu20.04支持的文件系统如上

![](F:\Study\notes\Linux\imgs\文件类型.png)

## GNU组织

### 1.GNU核心：

原本在Unix上的一些命令和工具，被模仿（移植）到了Linux上。

供Linux使用的这套工具：coreutils  软件包

(1)用来处理文件的工具

(2)用来操作文本的工具

(3)用来管理进程的工具

### 2.shell提供给用户使用的软件：用户拿它来使用电脑，并且和电脑交互

命令行shell提供一个命令行界面（CLI）

图形shell提供一个图形用户界面（GUI）

Linux shell->CLI Command-Line Interface

### 3.CLI shell

bash shell 基础shell

zsh ash korn tcsh

### 4.GUI

1.X Windows

2.KDE

3.GNOME

4Unity:不同于GNOME，KDE，Unity并非一个桌面包



## Linux命令

https://wangchujiang.com/linux-command/

mike@mike-virtual-machine:~$

用户名@机器名:当前所在目录 $等待用户输入

~用户home目录

### ls 命令

```shell
ls
ls -a #显示隐藏文件
```

```shell
man ls#查看帮助文档
```

### 文件扩展匹配符

*-->代表多个字符

?-->代表一个字符

```shell
ls -l fhs-2.3.pdf
ls -l fhs-2.3 copy?.pdf
ls -l *.pdf
```

![](F:\Study\notes\Linux\imgs\文件扩展匹配符.png)

### 元字符通配符 [] !

```shell
ls -l f[a-x]ck.txt	
```

![](F:\Study\notes\Linux\imgs\元字符通配符.png)

### Linux根目录

```shell
cd /
```

\ Windows  反斜线

/ Linux 正斜线

/ 根目录 最终的

```shell
cd .. #返回上一级目录
```

```
/bin 二进制目录 GNU工具
/etc 系统配置文件目录
/home 主目录，显示所有用户目录
/lib 库目录
/mnt 挂载目录，U盘
挂载---外在的设备和电脑进行连接
Mount point for mounting a filesystem temporarily
/proc 伪文件系统
/run 运行目录
/tmp 临时目录
/var 可变目录
/boot 启动目录
/dev 设备目录
/media 媒体目录Mount point for removeable media
/opt 可选目录
/root root用户的主目录 管理员 Linux中普通用户与管理员分开
/sbin 系统二进制目录，GNU高级管理员使用的命令工具
/srv 服务目录 本地服务
/usr 用户二进制目录，GNU工具
/usr/bin
```

#### FHS 系统层级标准

https://www.pathname.com/fhs/

### cd命令

```shell
cd    # 进入用户主目录；
cd /  # 进入根目录
cd ~  # 进入用户主目录；
cd .  #进入当前目录 . 指当前文件
cd ..  # 返回上级目录（若当前目录为“/“，则执行完后还在“/"；".."为上级目录的意思）；
cd ../..  # 返回上两级目录；
cd !$  # 把上个命令的参数作为cd参数使用。*****
注意使用!$ 
前一行不能出现其他命令
```

### 绝对路径与相对路径

绝对路径 （全）

```shell
gedit ~/Documents/doc/1.txt
```

~ ---> /home/mike/

相对路径

✨一定要设置故事背景，即我在哪？

```shell
gedit ./Documents/doc/1.txt
gedit Documents/doc/1.txt
```

### touch命令

```shell
touch 1.txt
```

touch创建一个空文件并更新它的时间

如果已经存在不会覆盖，但是会更新时间

### cp命令

cp 你想复制什么文件 你想复制到哪

cp 源文件 目标文件

```shell
cp -i#覆盖既有文件之前先询问用户
cp -R/r#递归处理，将指定目录下的所有文件与子目录一并处理；
```

### 终端光标移动技巧

```shell
tab               #自动补全
ctrl+上下左右方向键 #按照单词_单词跳跃
ctrl+L            #向下移动一页
ctrl+a            #移动行首
ctrl+e            #移动行尾
ctrl+u            #清除光标前的输入
ctrl+k            #清除光标后的输入
ctrl+r            #搜索之前输入过的命令

```

### 软链接与硬链接

链接文件 

1.符号链接（软链接）----快捷方式

原来的文件/文件夹必须是存在的

2.硬链接

副本

原来的文件/文件夹必须是存在的

软链接：

1. 软链接，以路径的形式存在。类似于Windows操作系统中的快捷方式
2. 软链接可以 跨文件系统 ，硬链接不可以
3. 软链接可以对一个不存在的文件名进行链接
4. 软链接可以对目录进行链接

硬链接

1. 硬链接，以文件副本的形式存在。但不占用实际空间。
2. 不允许给目录创建硬链接
3. 硬链接只有在同一个文件系统中才能创建



cp linkfile 类似于分享快捷方式 会导致无法打开

```shell
ln -s 源文件 链接文件 #创建软链接
ln 源文件 链接文件    #创建硬链接
```

![](F:\Photos\snipaste\Linux\软链接与硬链接.png)

第5列的0 6 0 表明软链接是与原文件单独分开的，会占用额外字节

硬链接则类似副本

### mv命令

重命名或者移动

```shell
mv 1.txt 2.txt #将1.txt重命名为2.txt
mv 1.txt ~/Documents/doc    
```

### rm命令

```shell
rm 文件
rm -i 文件
```

创建和删除文件夹

目录（文件夹）

```shell
mkdir
rmdir
```

### 查看文件类型

```shell
file 文件
```

### 查看文件内容

```shell
cat 文件
cat -A 文件
more 文件
less 文件#/字符串：向下搜索"字符串"的功能
     文件#?字符串：向上搜索"字符串"的功能
tail 文件#查看末尾10行
tail -n 2 文件#查看末尾2行
head #同理
```

查看进程

```shell
top
ps
ps -aux | grep named # 查看named进程详细信息
kill #杀死进程
```

### 挂载

Windows插入u盘 会产生新的虚拟盘 

![](F:\Photos\snipaste\Linux\挂载.png)

```shell
sudo fdisk -l
sudo mount /dev/sdb4 /mnt #将u盘映射到/mnt
sudo umount /media/mike/USB  #结束挂载
```

![](F:\Photos\snipaste\Linux\挂载linux.png)

查看磁盘信息

```shell
df -h 
du -h  
```

排序

```shell
sort
```

搜索

```shell
grep
```

### 打包压缩归档解压缩

.Z

gzip .gz

zip .zip

bzip2 .bz2

```shell
tar -c, --create               #创建一个新归档
    -x, --extract, --get       #从归档中解出文件
    -z, --gzip, --gunzip, --ungzip   #通过 gzip 过滤归档
     -v, --verbose              #详细地列出处理的文件
     -f: 使用档案名字，切记，这个参数是最后一个参数，后面只能接档案名。
```



```shell
tar -zcvf log.tar.gz log2012.log   #打包后，以 gzip 压缩
tar -zxvf /opt/soft/test/log.tar.gz #将tar包解压
```

### 父子shell

![](F:\Photos\snipaste\Linux\父子shell.png)

### 分号与括号在shell作用

![](F:\Photos\snipaste\Linux\分号在shell作用.png)

分号 依次执行命令

括号 在子shell中执行命令

```shell
echo $BASH_SUBSHELL #查看子shell数量
```

### sleep与jobs命令

```shell
sleep 300
sleep 300& #输出pid
jobs -l
```

![](F:\Photos\snipaste\Linux\sleep与jobs.png)

### 外部命令和内建命令

![](F:\Photos\snipaste\Linux\外部命令.png)

![外部命令与内建命令](F:\Photos\snipaste\Linux\外部命令与内建命令.png)

![](F:\Photos\snipaste\Linux\外部命令查看.png)

### history命令

![](F:\Photos\snipaste\Linux\history命令.png)

```shell
!行号 #执行所在行的历史命令
```

### alias

起别名

```shell
alias ll='ls -alF'
```

### 全局变量和局部变量(已理解)

```shell
printenv #显示系统环境变量
```

### 包管理系统PMS

软件安装、更新、卸载

解决工具依赖

LOL wegame

qq空间 qq

dpkg、rpm

dpkg：

```shell
apt-get
apt-cache
aptitude
```

### 安装、更新、卸载

```shell
sudo apt update  #查找更新
sudo apt upgrade #一键更新
sudo apt remove
```

### 用户与权限

id身份证

用户id　UID　数字

```shell
mike:x:1000:1000:mike,,,:/home/mike:/bin/bash
用户名:密码:UID:组ID:描述:用户home目录:默认使用的shell

```

![](F:\Photos\snipaste\Linux\文件与文件夹权限.png)

​	

```

    当为 d 则是目录
    当为 - 则是文件；
    若是 l 则表示为链接文档(link file)；
    若是 b 则表示为装置文件里面的可供储存的接口设备(可随机存取装置)；
    若是 c 则表示为装置文件里面的串行端口设备，例如键盘、鼠标(一次性读取装置)。

```

![](F:\Photos\snipaste\Linux\文件夹权限.png)

#### chmod

![](F:\Photos\snipaste\Linux\chmod.png)

![](F:\Photos\snipaste\Linux\Snipaste_2024-09-06_00-35-51.png)

