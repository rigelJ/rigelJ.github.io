---
title: Linux高级操作与管理
date: 2022-10-06 19:54:49
tags:
- Linux 
- 操作系统
- 命令行
categories:
- Linux
---

## Linux高级操作与管理

#### 目录

>操作环境bash
>
>正规表示与文件格式化
>
>shell脚本撰写与执行
>
>帐号管理与ACL权限设定
>
>磁盘配额与文件系统
>
>例行与工作排程
>
>进程管理与SELinux
>
>系统服务相关管理
>
>登录档分析
>
>模块管理与Loader
>
>基础设定与备份策略
>
>软件安装与Talball
>
>核心编译与管理



***转为Effia记录模式***



### 操作环境Bash



### 正规表示与文件格式化



### shell脚本撰写与执行



### 账户管理与ACL权限

- **GID与UID**

   - **Linux 操作系统上面，关于账号与群组，其实记录的是UID/GID 的数字而已**

   - **使用者的账号/群组与UID/GID的对应，参考/et/passwd 及/etc/group 两个文件**

     ![image-20221022194809193](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20221022194809193.png)

   - **/etc/passwd文件结构以冒号隔开,共分为七个字段，分别是[账号名称、密码、UID、GID、全名、家目录、shell」**

   - **账号的密码已经移动到/etc/shadow 文件中，该文件权限为仅有root 可以更动。该文件分为九个字段，内容为「账号名称、加密密码、密码更动日期、密码最小可变动日期、密码最大需变动日期、密码过期前警告日数、密码失效天数、账 号失效日、保留未使用」 **

   - **uId 只有0与非为0两种，非为0则为一般账号。一般账号又分为系统账号 (1-999) 及可登入者账号(大于1000) **

   -  **使用者可以支持多个群组，其中在新建文件时会影响新文件群组者，为有效群组。而写入/etc/passwd 的第四个字段者，称为初始群组。 **
-  **建立，更改与删除账号和群组**
   -  **与使用者建立、更改参数、删除有关的指令为: useradd, usermod, userdel等，密码建立则为passwd;与群组建立、修改、删除有关的指令为: groupadd, groupmod, groupdel等; **
      -  User add  
         -  -d   home dir
         -  -s    shell
         -  -c    注释
         -  -g   init group
         -  -G   other groups
      -  User mod 
         -  同上
      -  Userdel
         -  -l   del dir
   -  **群组的观察与有效群组的切换分别为: groups 及newgp指令; **
   -  **useradd 指令作用参考的文件有: /etc/defaultuseradd, etclogin.defs, /et/skel/等等 **
   -  **观察用户详细的密码参数，可以使用 chage -l 账号」来处理; **
   -  **用户自行修改参数的指令有: chsh, chfn等，观察指令则有: id, finger **
      -  chsh
         -  xxxx
-  **ACL权限管理**
   -  **ACL的功能需要文件系统有支持，CentOS7 预设的XFS确实有支持ACL功能**
   -  **ACL可进行单一个人或群组的权限管理，但ACL的启动需要有文件系统的支持; **
   -  **ACL的设定可使用setfacl ，查阅则使用getfacl ; **
      -  [Setfacl/Getfacl](http://c.biancheng.net/view/3132.html "行行行")
   -  **身份切换可使用su，亦可使用sudo，但使用sudo者，必须先以visudo 设定可使用的指令; **
      -  visudo
         -  我们可以修改*/etc/sudoers*文件来设置用户的sudo权限，修改/etc/sudoers一定要使用visudo命令，它可以让我们比较安全的修改此文件。
         -  visudo有以下特性：
            -  锁定文件避免多个同时编
            -  检查语法的完整性
            -  检查解析错误，以避免用户错误输入
            -  使用root的权限直接执行visudo，打开suders文件
         -  $visudo
            -  注意：这里不需要输入shduers文件的路径，默认为/etc/sudoers。可以使用-f指定sudoers文件。
         -  设置sudo权限
            -  语法格式
               -  用户  主机=（用户身份） 命令列表
                  -  用户：用户可以是直接用户名（如：root），也可以是以%开头表示的用户组（如：%wheel）。
                  -  主机：使用Host\_Alias定义主机的别名
                  -  命令列表：使用Cmnd\_Alias定义命令别名，多个命令使用逗号隔开
            -  用法
               -  找到下面这一行：                                            
                  -  `root  ALL=(ALL)   ALL`
               -  允许用户在所有主机上执行所有命令的权限：           
                  -  `test   ALL=（ALL） ALL`
               -  设置组执行所有命令的权限                                 
                  -  `%mygroup  ALL= (ALL)  ALL`
               -  设置组无需密码执行所有命令的权限                       
                  -   `%mygroup    ALL=(ALL)   NOPASSWD: ALL`
               -  wheel
                  -  在Linux有一个特殊的组wheel，它允许此组的用户执行所有命令的权限。
                  -  使用visudo打开sudoers文件，找到                  
                     -   `%wheel ALL=(ALL)   ALL`
                  -  如果此行被注释掉，把#去掉，然后把用户添加到此组即可。                                              
                     -  `usermod -aG wheel myuser`
   -  **PAM模块可进行某些程序的验证程序!与PAM模块有关的配置文件位于/etc/pam.d/****\* 及/etc/security/ 系统上面账号登入情况的查询，可使用w, who, last, lastlog等; **
   -  **在线与使用者交谈可使用write, wall,脱机状态下可使用mail 传送邮件! **

