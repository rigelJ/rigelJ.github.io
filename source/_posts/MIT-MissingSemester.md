---
title: MIT-MissingSemester
date: 2023-03-18 18:33:16
tags:
- MIT
- Vim
- Git
- Bash
categories:
- Learning Record
---



**“对于计算机教育来说，从操作系统到机器学习，这些高大上课程和主题已经非常多了。然而有一个至关重要的主题却很少被专门讲授，而是留给学生们自己去探索。 这部分内容就是：精通工具。在这个系列课程中，我们会帮助您精通命令行、使用强大的文本编辑器、使用版本控制系统提供的多种特性等等。”**

​                                                                                        **——【MIT】The Missing Semester**

## Description

Name：MIT-MissingSemester

Time：20h

Tips：Bash  |  Script  |  Vim  |  Data-Wrangling |  Git |  Debuging |  Security

Project：https://github.com/rigelJ/Learning-CS-fromScratch/tree/develop/missing_semester



## Guides

- Shell
	- echo  
		- echo "hello world"
		- echo  $PATH  环境变量
	- which 
		
		- ? 判断该程序是在哪个目录被打开的 
	- path  
		- ? 描述计算机里文件的位置
			- 绝对路径
				- ？ 绝对准确的定义一个文件的位置
				- pwd  查看当前路径
			- 相对路径
				- ？ 相对当前路径所在路径
				- ..  上一层目录
				- .  当前目录
				- ~ 用户相关目录
				- - 上一个进入的目录，切换目录
	- cd   
		- ? change the dir
		- 绝对路径或相对路径
	- ls
		- ？ 显示当前目录所有文件
		- -l  文件类型、权限
			- rwx权限  
				- 文件
					- r读w写x执行
				- 目录
					- r阅读清单w重命名新建删除文件x搜索
	- mv  
		- ？ rename a file
		- mv  dotfile.md foo.md
	- cp  
		- ? copy file
		- cp  xxx
	- rm
		- ? remove file
		- rmdir  
			- ？ remove  dir
	- cut
		
		- cut -d '' -f2
	- ctrl + L   clear
	- stream
		- > 重定向输出流
			>
			> - echo  hello > hello.txt
		-  < 重定向输出流
			
			- cat < hello.txt
		- >>  追加
		- |  管道符号
			- ls | tail  -n1
			- curl --head --silent google.com | grep -i content-length 
	- root
		- sudo
		- tee
			- echo 1000 | sudo tee brightness
	- xdg-open