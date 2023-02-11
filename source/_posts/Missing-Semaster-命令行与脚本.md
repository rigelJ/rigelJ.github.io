---
title: Missing_Semaster-命令行与脚本
date: 2022-10-05 20:45:18
tags:
- MIT
- MissingSemaster
- 编程素养
categories:
- Learn
---

## Missing_Semaster-命令行与脚本

这部分课程内容，介绍了使用 bash 作为脚本语言的一些基础知识，以及许多 shell 工具，这些工具涵盖了您将在命令行中不断执行的几个最常见的任务。

以下是课程所包含的内容



### 理解shell的界面，参数和环境变量$PATH

```shell
missing:~$ 
missing:~$ date
Fri 10 Jan 2020 11:49:31 AM EST
missing:~$ 
missing:~$ echo hello
hello
missing:~$ echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
missing:~$ which echo
/bin/echo
missing:~$ /bin/echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```



### 使用cd切换路径，使用pwd查看当前路径

```shell
missing:~$ pwd
/home/missing
missing:~$ cd /home
missing:/home$ pwd
/home
missing:/home$ cd ..
missing:/$ pwd
/
missing:/$ cd ./home
missing:/home$ pwd
/home
missing:/home$ cd missing
missing:~$ pwd
/home/missing
missing:~$ ../../bin/echo hello
hello
```



### 使用ls查看给定目录中的内容，了解附带参数如-l,-a 的分别含义

```shell
missing:~$ ls
missing:~$ cd ..
missing:/home$ ls
missing
missing:/home$ cd ..
missing:/$ ls
bin
boot
dev
etc
home
...
missing:~$ ls -l /home
drwxr-xr-x 1 missing  users  4096 Jun 15  2019 missing
```



### 使用echo，cat，tail，head指令对输出进行控制，理解重定向符号<>和管道符号|的意义

```shell
missing:~$ echo hello > hello.txt
missing:~$ cat hello.txt
hello
missing:~$ cat < hello.txt
hello
missing:~$ cat < hello.txt > hello2.txt
missing:~$ cat hello2.txt
hello
missing:~$ ls -l / | tail -n1
drwxr-xr-x 1 root  root  4096 Jun 20  2019 var
```



### 了解超级用户root的权限，掌握切换和使用root账户的指令，利用tee指令传递权限

>#### 以下是一个tee指令使用的实例
>
>
>
>例如，笔记本电脑屏幕的亮度通过以下调用的文件公开brightness
>
>```
>/sys/class/backlight
>```
>
>
>
>通过将值写入该文件，我们可以更改屏幕亮度。你的第一反应可能是做这样的事情：
>
>```shell
>$ sudo find -L /sys/class/backlight -maxdepth 2 -name '*brightness*'
>/sys/class/backlight/thinkpad_screen/brightness
>$ cd /sys/class/backlight/thinkpad_screen
>$ sudo echo 3 > brightness
>An error occurred while redirecting file 'brightness'
>open: Permission denied
>```
>
>
>
>在上面的例子中，shell（就像你的用户一样进行身份验证）在将其设置输出之前，会尝试打开亮度文件进行写入，但由于 shell 不以 root 身份运行，因此无法执行此操作。
>
>```shell
>$ echo 3 | sudo tee brightness
>```
>
>
>
>由于该程序是打开文件进行写入的程序，并且它以 运行方式运行，因此权限全部解决。



### 掌握shell中变量赋值的两种形式，了解“”与’‘的区别，掌握其他特殊变量的用法

>#### 变量赋值与访问
>
>
>
>**普通赋值**
>
>```shell
>foo=bar
>echo "$foo"
># prints bar
>echo '$foo'
># prints $foo
>```
>
>
>
>**将指令执行结果赋值给变量**
>
>```shell
>foo=$(pwd)
>echo $foo
># /home/donnie
>```
>
>
>
>#### 特殊变量
>
>>$0- 当前脚本名称
>>
>>$1 - 到9 当前脚本的第n个参数
>>
>>$@ -  当前脚本所有参数的集合 
>>
>>$# -  当前脚本参数的数量
>>
>>$? -  上一个命令的返回代码
>>
>>$$ - 当前脚本的进程标识号 （PID）
>>
>>!!  -   上一命令，包括参数。
>
>



### 掌握逻辑运算符和通配符以及大括号的使用

>#### 逻辑运算符 && ||  ;
>
>```shell
>false || echo "Oops, fail"
># Oops, fail
>
>true || echo "Will not be printed"
>#
>
>true && echo "Things went well"
># Things went well
>
>false && echo "Will not be printed"
>#
>
>true ; echo "This will always run"
># This will always run
>
>false ; echo "This will always run"
># This will always run
>```
>
>
>
>#### 通配符 * ?  和 { }
>
>```shell
>convert image.{png,jpg}
># Will expand to
>convert image.png image.jpg
>
>cp /path/to/project/{foo,bar,baz}.sh /newpath
># Will expand to
>cp /path/to/project/foo.sh /path/to/project/bar.sh /path/to/project/baz.sh /newpath
>
># Globbing techniques can also be combined
>mv *{.py,.sh} folder
># Will move all *.py and *.sh files
>
>
>mkdir foo bar
># This creates files foo/a, foo/b, ... foo/h, bar/a, bar/b, ... bar/h
>touch {foo,bar}/{a..h}
>touch foo/x bar/y
># Show differences between files in foo and bar
>diff <(ls foo) <(ls bar)
># Outputs
># < x
># ---
># > y
>```



### 了解shell函数和脚本之间的关系和差异，掌握两者的使用方法

>#### shell函数
>
>````bash
># mcd.sh
>
>mcd () {
>    mkdir -p "$1"
>    cd "$1"
>}
>````
>
>将函数载入环境
>
>`source mcd.sh`
>
>
>
>#### 脚本
>
>
>
>*bash脚本**
>
>```shell
>#!/bin/bash
>
>echo "Starting program at $(date)" # Date will be substituted
>
>echo "Running program $0 with $# arguments with pid $$"
>
>for file in "$@"; do
>    grep foobar "$file" > /dev/null 2> /dev/null
>    # When pattern is not found, grep has exit status 1
>    # We redirect STDOUT and STDERR to a null register since we do not care about them
>    if [[ $? -ne 0 ]]; then
>        echo "File $file does not have any foobar, adding one"
>        echo "# foobar" >> "$file"
>    fi
>done
>```
>
>
>
>**python脚本** 
>
>```shell
>#!/usr/local/bin/python
>
>import sys
>for arg in reversed(sys.argv[1:]):
>    print(arg)
>```



### 掌握find，fd，help和man等文件查找指令，grep，rg等模式匹配指令

>#### find
>
>````shell
># Find all directories named src
>find . -name src -type d
># Find all python files that have a folder named test in their path
>find . -path '*/test/*.py' -type f
># Find all files modified in the last day
>find . -mtime -1
># Find all zip files with size in range 500k to 10M
>find . -size +500k -size -10M -name '*.tar.gz'
>````
>
>#### man
>
>```shell
>missing:~$ man l
>```



**以上是所有shell课程中的重点内容，以为到这就结束了？远不止如此。**

**以下是我认为课程需要我们额外去学习的内容**

[Linux操作与使用]: 
[Bash编程与管理]: 



