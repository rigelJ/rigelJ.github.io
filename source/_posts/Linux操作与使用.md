---
title: Linux操作与使用
date: 2022-10-05 20:06:11
tags:
- Linux 
- 操作系统
- 命令行
categories:
- Linux/Unix
---

## Linux操作与使用

#### 目录

>操作系统与硬件
>
>主机规划与磁盘分区
>
>CentoOS安装
>
>登录与在线求助
>
>文件权限与目录管理
>
>磁盘划分与目录挂载
>
>系统压缩与备份
>
>程序编辑器vim
>



### 操作系统与硬件



#### 操作系统

>操作系统主要在管理与驱动硬件，因此必须要能够管理内存、管理装置、负责进程管理以及系统调用等等。因此，只要能够让硬件准备妥当的情况，就是一个合格的操作系统了。



#### Unix

>Unix 的前身是由贝尔实验室(Bell lab.)的Ken Thompson利用汇编语言写成的，后来在 1971-1973年间由Dennis Ritchie以C程序语言进行改写，才称为Unix。



#### BSD

>1977年由Bill Joy释出BSD (Berkeley Software Distribution),这些称为Unix-like的操作系统.



#### Minix

>1984年由Andrew Tanenbaum开始制作Minix操作系统，该系统可以提供原始码以及软件;



#### GNU计划

>1984年由Richard Sallman提倡GNU计划，倡导自由软件(Free software)，强调其软件可以 「自由的取得、复制、修改与再发行」，并规范出GPL授权模式，任何 GPL(General Public License)软件均不可单纯仅贩卖其软件，也不可修改软件授权。



#### Linux Kernel

>从Linux kernel 3.0开始，已经舍弃奇数、偶数的核心版本规划，新的规划使用主线版本(MainLine) 为依据，并提供长期支持版本 (longterm)来加强某些功能的持续维护。



#### Linux Distrbutiom

>Linux distributions的组成含有: [Linux Kernel + Free Software + Documentations(Tools) +可完全安装的程序」所制成的一套完整的系统。
>
>常见的Linux distributions分类有[商业、社群」分类法，或「RPM、DPKG」 分类法



### 主机规划与硬盘分区



#### 主机规划

>主机规划一定要按照自己的需求来进行使用。



#### 装置文件名

>磁盘装置文件名通常分为两种，实际SATA/USB装置文件名为/dev/sd[a-p], 而虚拟机的装置可能为/dev/vd[a-p]



#### MBR分区

> 磁盘的第一个扇区 主要记录了两个重要的信息，一是要启动记录区(Master Boot Record, MBR):可以安装开机管理程序的地方,有446 bytes ，二是分区表(artition table):记录整颗硬盘分区的状态，有64 bytes;
>
> 磁盘的MBR分区方式中，主要与延伸分区最多可以有四个，所以逻辑分区的装置文件名号码，一定是由从5号开始。

![image-20221007192837574](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007192837574.png)

> 如果采用逻辑分区，那么磁盘的规划会变成这样

![image-20221007192922041](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007192922041.png)



#### GPT分区

>如果磁盘容量大于2TB以上时，系统会自动使用GPT分区方式来处理磁盘分区。
>
>GPT分区已经没有延伸与逻辑分区槽的概念，你可以想象成所有的分区都是主分区.
>
>某些操作系统要使用GPT分区时，必须要搭配UEFI的新型BIOS 格式才可安装使用。

![image-20221007192955934](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007192955934.png)

#### 开机的流程

>开机的流程由: BIOS-->MBR-->boot loader-->核心文件。
>
>boot loader的功能主要有:提供选单、加载核心、转交控制权给其他loader。
>
>boot loader可以安装的地点有两个，分别是MBR与boot sector,这个特色造就了多重引导功能。

![image-20221007193014623](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007193014623.png)

#### 目录树

```
Linux 操作系统的文件使用目录树系统，与磁盘的对应需要有[挂载」的动作才行;
```

![image-20221007161907887](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007161907887.png)

> 挂载示意如下：

<img src="https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007162003856.png" alt="image-20221007162003856" style="zoom:80%;" />





### CentOS安装



#### 安装模式

>安装CentOS 7.x的模式至少有两种，分别是图形接口与文字接口;



#### 分区设定

>CentOS 7会主动依据你的磁盘容量判断要用MBR或GPT分区方式，你也可以强迫使用GPT，在安装时按下<kbd>tab</kbd>,在最后加入`ist.gpt`。
>
>若安装笔记本电脑时失败，可尝试在开机时加入`linux nofb apm=off acpi=off`来关闭省电功能;
>
>安装过程进入分区后，请以「自定义的分区模式」来处理自己规划的分区方式;
>
>常见的分区为 /  /boot  BIOS boot /home

![image-20221007162258318](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007162258318.png)

>规划后的分区如下

![image-20221007162726289](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007162726289.png)



#### 网络设定

>网卡和地址的正确配置如下

![image-20221007163140672](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007163140672.png)





### 登录与在线求助



#### root登录

>养成良好的操作习惯，尽量不要使用root 直接登入系统，应使用一般账号登入系统，有需要再转换身份可以透过「活动总览」查看系统所有使用的软件及快速启用惯用软件
>
>在终端机环境中，可依据提示字符为$或#判断为一般账号或root账号:
>
>使用`su -` 切换至root帐号



#### X-图形界面与命令行界面的切换

>预设情况下，Linux 提供ty1-tty6的终端机界面。
>
>在X的环境下想要「强制」重新启动X的组合按键为:<KBD>ALT</KBD>+<KBD>Ctrl</KBD>+<KBD>Backspace</KBD>
>
>从X环境切换至命令行界面的组合按键为：<KBD>ALT</KBD>+<KBD>Ctrl</KBD>+<KBD>F2-F6</KBD>
>
>无图形界面下切换X桌面使用`startx`指令，不过不一定能够使用。
>
>启动`graphic.target`服务并设置为默认，则自动启动图形界面



#### 语系支持

>如果输入指令出现乱码，需要进行语系的更改。

![image-20221007165447135](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007165447135.png)



#### 组合按键

>组合按键中, <kbd>Tab</kbd>按键 可做为命令补齐/档名补齐或/参数选项补齐
>
><kbd>Ctrl+c</kbd>可 以中断目前正在运作中的程序;



#### 帮助系统

>man指令是一个自带的帮助系统，可以查询指令以及系统文件的作用，例如，`man ls`以及`man issue`
>
>man page说明后面的数字中， 1代表一般账号可用指令，8代表系统管理员常用指令，5代表系统配置文件格式
>

![image-20221007193137847](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007193137847.png)

>info指令也是一个帮助系统，可以采用浏览器的方式进行点击跳转，可将一份说明文件拆成多个节点(node)显示，并具有类似超链接的功能，增加易读性;

![image-20221007170037728](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007170037728.png)

>此外可使用的帮助系统还有/usr/share/doc   --help  以及`tldr`，后者需要自行安装。



#### 文本编辑器nano

![image-20221007170237461](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007170237461.png)



#### 关机与注销

>系统需正确的关机比较不容易损坏，可使用shutdown, poweroff等指令关机。
>
>shutdown指令只有root管理员能够下达。
>
>使用exit注销帐号，返回登录界面
>
>在关机之前最好使用sync指令将内存中的数据写入储存。



### 文件权限与目录管理



#### rwx权限

>Linux的每个文件中，可分别给予使用者、群组与其他人三种身份个别的rwx权限;
>
>利用`ls -l`显示的文件属性中，第一个字段是文件的权限，共有十个位，第一个位是文件类型，接下来三个为一组共三组，为使用者、群组、其他人的权限，权限有r,w,x三种;

![image-20221007170605114](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007170605114.png)

>对于文件来说
>
>>r：可读取此一文件的实际内容，如读取文本文件的文字内容等
>
>>w：可以编辑、新增或者是修改该文件的内容(但不含删除该文件);
>
>>x：该文件具有可以被系统执行的权限。
>>

>对于目录来说
>
>>r ：浏览目录内容
>
>>w ：增加或删除目录内容
>
>>x ：切换进入目录，使得目录成为工作目录

![image-20221007171002409](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007171002409.png)

>文件的类型有以下几种

![image-20221007193427772](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007193427772.png)



#### 隐藏文件

>如果档名之前多一一个`.`，则代表这个文件为隐藏文件，隐藏文件需要使用`ls -a`查看

![image-20221007170605114](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007170605114.png)



#### 修改文件权限

>若需要root的权限时，可以使用`su-`这个指令来切换身份。处理完毕则使用exit 离开su的指令环境。
>
>更改文件的群组支持可用`chgrp`,修改文件的拥有者可用`chown`,修改文件的权限可用`chmod`
>
>`chmod`修改权限的方法有两种，分别是符号法与数字法，数字法中r,w,x分数为4.2.1;

>>符号法
>
>>`chmod +rx xx.py`
>

![image-20221007193514337](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007193514337.png)

>>数字法
>
>>`chmod 770 xx.py`
>

![image-20221007171143570](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007171143570.png)

#### 文件权限限制

>要开放目录给任何人浏览时，应该至少也要给予r及x的权限，但w权限不可随便给;
>
>能否读取到某个文件内容，跟该文件所在的目录权限也有关系,目录至少需要有x的权限。

![image-20221007171118654](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007171118654.png)



#### FHS目录配置

>根据FHS的官方文件指出，他们的主要目的是希望让使用者可以了解到已安装软件通常放置于那个目录下FHS订定出来的四种目录特色为: shareable, unshareable, static, variable等四类;

![image-20221007171342613](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007171342613.png)

>根据目录树架构，FHS定义三层主目录为/   /usr   /var

![image-20221007171523603](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007171523603.png)

> 根目录/ 的结构

![image-20221007171716624](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007171716624.png)

> /usr 目录的结构

![image-20221007171808024](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007171808024.png)

> /var 目录的结构

![image-20221007171833498](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007171833498.png)

> 不同目录之间的链接情况

![image-20221007171914229](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007171914229.png)



#### 绝对路径与相对路径

>绝对路径文件名为从根目录开始写起，否则都是相对路径的文件名。



#### 文件操作重要指令

>与目录相关的指令有: `cd, mkdir, rmdir, pwd,rm,mv,cp`等重要指令;
>
>`rmdir`仅能删除空目录，要删除非空目录需使用 -p 指令;
>
>`Is`可以检视文件的属性，尤其-d, -a, 1等选项特别重要!
>
>文件的复制、删除、移动可以分别使用: `cp, rm , mv`等指令来操作;



#### 特殊目录

![image-20221007173311358](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007173311358.png)

#### $PATH

>用户能使用的指令是依据PATH 变量所规定的目录去搜寻的;
>
>加入$PATH的路径内存放的指令执行文件可以直接在shell中输入指令名来执行
>
>使用`PATH = “$PATH=/root”`将路径加入PATH



#### 取得路径名称

![image-20221007173546414](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007173546414.png)



#### 查看文件内容

>检查文件的内容(读文件)可使用的指令包括有: `cat, tac, nl, more, lss, head, til,od`等
>
>`cat-n`与`nl`均可显示行号，但默认的情况下，空白行会不会编号并不相同;

![image-20221007173655406](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007173655406.png)

> less指令使用

![image-20221007173754819](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007173754819.png)

> od指令使用

![image-20221007173838377](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007173838377.png)



#### 修改文件参数

>touch的目的在修改文件的时间参数，但亦可用来建立空文件;
>
>一个文件记录的时间参数有三种，分别是access time(aime), status time (ctime), mdification time(mtime)

![image-20221007193936078](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007193936078.png)



#### 文件的预设权限

> 新建文件/目录时，新文件的预设权限使用umask来规范，其预设权限如下

![image-20221007194522691](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007194522691.png)

>利用umask更改预设权限，更改后

![image-20221007194649352](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007194649352.png)

![image-20221007194853337](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007194853337.png)



#### 文件的隐藏属性 

> 除了传统的rwx权限之外，在Ex2/Ext3/Ext4/xfs文件系统中，还存在隐藏属性，以下是所有隐藏属性，最常见的隐藏属性为+i和+a

![image-20221007195304005](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007195304005.png)

>使用chattr 给文件配置隐藏属性

![image-20221007195612867](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007195612867.png)

> 使用lsattr显示文件隐藏属性

![image-20221007195741048](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007195741048.png)



#### 文件的特殊权限

>文件具有SUID的特殊权限时,代表当用户执行此binary程序时，在执行过程中用户会暂时具有程序拥有者的权限

![image-20221007195959605](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007195959605.png)

>用一张漫画来说明这个权限的使用过程

![image-20221007200217090](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007200217090.png)

>目录具有SGID的特殊权限时，代表用户在这个目录底下新建的文件之群组都会与该目录的组名相同。

![image-20221007200631139](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007200631139.png)

>目录具有SBIT的特殊权限时，代表在该目录下用户建立的文件只有自己与root能够删除

<img src="https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007200730676.png" alt="image-20221007200730676" style="zoom:80%;" />

>给文件或目录加上SUID，SGID，SBIT权限，只需要在chmod 使用数字授权时候在标准数字之前加上代表三个权限的数字，SUID为4,  SGID为2,  SBIT为1

<img src="https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007201026907.png" alt="image-20221007201026907" style="zoom:80%;" />



#### 观察文件类型

> 使用file指令观察文件类型

<img src="https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007201131838.png" alt="image-20221007201131838"  />



#### 指令与文件的查找

> 搜寻指令的完整文件名可用which 或type ，这两个指令都是透过PATH变量来搜寻文件名;

![image-20221007201449046](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007201449046.png)

> 搜寻文件的完整档名可以使用whereis 找特定目录或locate 到数据库去搜寻，而不实际搜寻文件系统;

![image-20221007201507176](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007201507176.png)

> 用find可以加入许多选项来直接查询文件系统，以获得自己想要知道的档名，find指令复杂多变。具体可以参考
>
> `man find`



#### 权限和指令之间的关系（整合）

![image-20221007201747868](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007201747868.png)





### 磁盘划分和目录挂载



#### MBR和GPT

![image-20221007215146933](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007215146933.png)

#### 文件系统



**Ext文件系统**

>基本上Linux 的传统文件系统为ExI2，该文件系统内的信息主要有:
>
>superblock: 记录此filesystem 的整体信息，包括inode/block的总量、使用量、剩余量， 以及文件系统的格式与相关信息等;
>
>inode:记录文件的属性，一个 文件占用-一个inode,同时记录此文件的数据所在的block 号码;
>
>block:实际记录文件的内容，若文件太大时，会占用多个block.
>
>这种数据存取的方式我们称为索引式文件系统

![image-20221007215534068](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007215534068.png)

> 相比起来FAT格式的读取方式是这样的

![image-20221007215712073](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007215712073.png)

>Ext2文件系统主要有: boot sector, superblock, inode bitmap, block bitmap, inode table, data block等六大部分。
>
>Ext2文件系统的示意图如下.

![image-20221007215921814](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007215921814.png)

>data block是用来放置文件内容数据地方，在Ext2 文件系统中所支持的block 大小有1K,2K 及4K

>inode 记录文件的属性/权限等数据，其他重要项目为:每个 inode大小均为固定，128/256bytes 两种基本容量。
>
>每个文件都仅会占用一个inode而已，因此文件系统能够建立的文件数量与inode 的数量有关;
>
>文件的block 在记录文件的实际数据，目录的block 则在记录该目录底下文件名与其inode 号码的对照表;

![image-20221007220501891](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007220501891.png)

>superblock记录整个filesystem的信息，主要记录inode和block的总量，未使用和已使用的inode和block，大小等。



>使用dump2fs查询ext家族superblock的指令

![image-20221007221002782](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007221002782.png)

![image-20221007221040698](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007221040698.png)



**xfs文件系统**

>xfs文件系统主要分为三个部分，资料区，文件系统活动登录区，和实时运作区



#### 文件系统的操作



**查看文件系统磁盘使用量**

>查看文件系统的磁盘使用量使用指令df和du

>df列出文件系统的整体磁盘使用量

![image-20221007221859758](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007221859758.png)

>du 评估文件系统各个文件的磁盘使用量

<img src="https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007221934486.png" alt="image-20221007221934486"  />



**创建链接**

>创建链接有两种类型，分别是实体链接与符号链接的建立

>实体链接的建立，是在某个目录下新增一个链接到某inode号码的关联记录，这两个档名链接到同一个inode，无论你删除哪一个文档，文件的inode和block都是存在的，从另一个都可以访问到对应的文件。

![image-20221007222352413](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007222352413.png)

>其链接模式如图所示

![image-20221007222821931](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007222821931.png)

> 符号链接的建立是在建立一个独立的文件，而这个文件会让数据读取指向link的文件，所以当被链接的原文件被删除后，符号链接也作废了，有点像windows的快捷方式。

![image-20221007223057831](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007223057831.png)

>其链接模式如图所示

![image-20221007223128721](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007223128721.png)



#### 磁盘的分区，格式化与挂载



**观察磁盘分区状态** 

> 使用lsblk指令列出系统上所有磁盘列表

![image-20221007223351460](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007223351460.png)

>使用blkid列出装置的UUID，文件系统格式，等参数

![image-20221007223558635](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007223558635.png)

>使用parted列出磁盘的分区表类型与分区信息

![image-20221007223638672](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007223638672.png)



**进行磁盘分区**

>磁盘分区中，使用GPT格式的磁盘使用gdisk指令，使用MBR格式的磁盘使用fdisk指令
>
>先要透过lsblk和blkid找到磁盘，然后利用part查看分区表类型，最后再确定使用的指令

![image-20221007223815647](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007223815647.png)

>gdisk中，p为查看分区情况，n为增加一个分区，d为删除一个分区，q为不保存退出，w为保存退出
>
>其中增加分区的n，在LastSector这里使用+500M或+2G这样的描述划分存储量
>
>分区后w保存，而后使用partprobe -s  更新分区表信息

![image-20221007224251998](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007224251998.png)



**磁盘格式化**

>使用mkfs.xxx指令对不同的文件系统进行格式化，例如将分区格式化为xfs格式，使用mkfs.xfs指令进行

![image-20221007224433502](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007224433502.png)



**文件系统检验**

> 使用xfs_repair ，fsck.ext4 对错乱的文件系统进行整理修复

![image-20221007224625761](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007224625761.png)



 **文件系统挂载**

>使用mount进行挂载.

![image-20221007224832732](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007224832732.png)



>挂载CD或者DVD时，同样，一般将之挂在到根目录下的 /mnt目录查看

>重新挂载使用指令`mount -o remouont,rw,auto`

>将某个目录挂载到另一个目录使用指令`mount --bind /var /data/var`

>使用unmount指令卸出

![image-20221007225559098](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007225559098.png)

>使用xfs_admin和tune2fs修改labelname和UUID

![image-20221007225756390](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007225756390.png)

>设定开机挂载 ，将记录写入etc/fstab，格式模仿上面的就是了

>可以使用dd制作空的大文件再挂载到某个目录下当分区用

![image-20221007230208670](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221007230208670.png)

> 建立swap分区，可以通过增加分区进行，`swapon`，也通过空大文件挂载进行

> 挂载操作也可以使用parted实现，具体操作和gdisk相差不大



### 文件压缩和备份



#### 常见的压缩指令

> 压缩指令为透过一些运算方法去将原本的文件进行压缩，以减少文件所占用的磁盘容量。压缩前与压缩后的文件所占用的磁盘容量比值，就可以被称为是[压缩比」

>常见的压缩指令有gzip，bzip2和xz三种，他们的用法都差不多，zcat，bzcat和xzcat也是用于查看压缩文件内容，其使用方法也大多相同

![image-20221008221342368](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221008221342368.png)

![image-20221008221751871](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221008221751871.png)



#### 打包指令

>使用tar指令对文件进行打包，tar指令的常用选项如下

![image-20221008221926526](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221008221926526.png)

>简而言之可以归纳为如下的指令 

![image-20221008221935274](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221008221935274.png)

>tar指令还可以对目录进行备份，加上-p参数保留原有权限，加上-v参数会显示作用中的文件名，-J参数会花更多时间。

![image-20221008222243419](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221008222243419.png)

> 解压时候，如果只需要解压单一文件，可以使用grep指令

![image-20221008222408951](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221008222408951.png)

> 如果想排除某些文件可以使用exclude参数

![image-20221008222540399](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221008222540399.png)

>只备份比某个时间新的文件可以使用--newer-time参数

![image-20221008222708221](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221008222708221.png)



#### 文件系统备份



>xfs系统的备份可以使用xfs_dump指令进行，使用xfsrestore指令复原

![image-20221008223119606](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221008223119606.png)

>还可以 进行差异备份 

![image-20221008223533596](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221008223533596.png)

>可以使用xfstore -I指令进行查看备份的数据内容以及label

![image-20221008223642483](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221008223642483.png)

>复原的时候也可以分部进行，按照label进行定位复原

![image-20221008223718524](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221008223718524.png)

>使用-i参数进入互动备份界面

![image-20221008223902471](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221008223902471.png)



#### 光盘写入工具



>使用mkisofs指令建立映像档，储存需要的数据。

![image-20221008224235226](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221008224235226.png)

>这样操作会导致文件的混乱，所以我们使用-graft-point参数进行划分

![image-20221008231311733](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221008231311733.png)

**制作可开机光盘映像**



>取得iso映像之后，使用isoinfo指令对iso文件进行查看

![image-20221008231624761](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221008231624761.png)

>将iso镜像挂载到/mnt目录，而后将所有数据完整到/srv/newed里面，使用rsync指令完整复制所有权限属性等数据，这样在/srv/newed里面就有了完整的映像档内容。

![image-20221008231957898](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221008231957898.png)

>按照需要对iso镜像进行修改后恢复其为iso镜像即可。

![image-20221008232147990](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221008232147990.png)

>进行光盘刻录操作，centos是wdim指令，自己去查询自己所在的distribution中的光盘刻录指令，这里以wdim为例子

![image-20221008232320530](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221008232320530.png)

>先得找到刻录机的位置，一般都是/dev/sr0这样的文件名，QEMU是虚拟机的虚拟光驱，而ASUS是真实光驱

![image-20221008232451568](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221008232451568.png)

>最后使用iso进行刻录操作

![image-20221008232622911](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221008232622911.png)

>最后测试挂载一下，检验内容

![image-20221008232714078](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221008232714078.png)



#### 其他指令

>我们上面建立空的大文件使用的dd指令也可以进行备份操作，其中有一个重要操作就是将刚才的刻录后的光盘进行一个备份

![image-20221008232844977](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221008232844977.png)

>同样，这里也介绍了如何将iso镜像刻录到usb磁盘作为安装盘

![image-20221008233105343](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221008233105343.png)



>cpio指令也是一个备份指令，可以备份任何东西，但是要和find这类查询指令配合一起使用。使用><进行数据流重定向，从而进行备份和还原。

![image-20221009220206332](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221009220206332.png)

![image-20221009220535972](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221009220535972.png)





### Vim程序编辑器



#### Vim的三种模式

>vi有三种模式，- -般指令模式可变换到编辑与指令列模式，但编辑模式与指令列模式不能互换;一般模式切换编辑模式，可以通过i，a，o等指令，按下`ESC`键切换到一般模式，一般模式切换到指令列模式输入：，/，？切换，同样按下`ESC`键回到一般模式。

![image-20221009222419976](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221009222419976.png)



#### 切换指令列模式

>使用`:`切换至指令列模式，可以在此基础上进行退出`q`，储存`w`，读取`r`，临时跳出等操作`！`

![image-20221009224809443](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221009224809443.png)

#### 移动指令

>按下`hjkl`四个键可以上下左右移动，同样移动到行首`0`，行尾`$`,文件头`gg`，文件末尾`G`，某一列`nG`，向下移动几列`5j`，都可以使用不同的指令进行，其他具体指令参考如下。

![image-20221009222725370](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221009222725370.png)



​       

#### 搜索与替代指令

>**搜索，**使用`/word`和`？word`进行搜索，前者向下搜索，后者向上搜索，使用`n`和`N`指令移动到下一个匹配位置，

![image-20221009223303496](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221009223303496.png)

> **替代，**使用`：n1,n2s/word1/word2/g`将匹配到的字符进行替换，其他使用方式如下

![image-20221009223454878](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221009223454878.png)



#### 删除和复制指令

>**删除**，使用`x`删除光标位置字符，使用`dd`删除本行，使用`d1G`删除本行到文件末尾，其他使用如下

![image-20221009223740393](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221009223740393.png)



>**复制，**使用yy复制本行，使用`y1G`复制本行到文件末尾，其他相似使用如下

![image-20221009223916781](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221009223916781.png)



>粘贴，使用p和P将复制的数据贴在光标所指向的上一列或下一列

![image-20221009224055037](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221009224055037.png)



>**结合，**使用`J`指令合并上下列
>
>使用`c`重复删除多个指令，这个实际上和`ndd`差不多

![image-20221009224324625](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221009224324625.png)



>**重复，**使用`u`指令和`ctrl+r`指令，复原和重做上一个动作，使用.重复上一个操作

![image-20221009224516362](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221009224516362.png)



#### 暂存与救援，警告

> 不正常中断Vim后，再打开文件会有六个可用按钮分别对应不同的还原模式

![image-20221010220335279](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221010220335279.png)



#### 区块选择

> 在一般模式下，长按v再左右上下移动，可以选中周边的区块，选中后可以使用不同的指令进行操作。

![image-20221010220618713](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221010220618713.png)



#### 多文件和多窗口

>在打开文件时候，可以同时打开多个文件，这样进行操作的时候就可以使用不同的指令进行切换，例如使用`vim hosts /etc/hosts`开启两个文件后就可以使用，`n`和`N`指令进行上下切换。

![image-20221010220854275](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221010220854275.png)



>在打开一个文件的时候，可以使用`:sp file.txt`打开另一个窗口，并启动另一个文件`file.txt`

![image-20221010222456818](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221010222456818.png)

>使用`w+j`向上切换，同理向下切换

![image-20221010222553234](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221010222553234.png)



#### 环境设定与记录



>vim的环境设定参数能够提供vim启动的预设环境，常用的环境设定参数如下

![](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221010223135939.png)

>当然，可以在进入vim编辑之后再设定，但是每次设定多少有点麻烦，vim的设定值放置在 ～/vimrc这个文件中，如果没有可以自己手动建立，而后将所希望的设定值写入。

![image-20221010223413285](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221010223413285.png)



#### 一张图总结Vim

![image-20221012223355695](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221012223355695.png)

