---
title: MIT-MissingSemester
date: 2023-03-19 15:46:59
tags:
- MIT
- tools
categories:
- Learning Record
---



**“对于计算机教育来说，从操作系统到机器学习，这些高大上课程和主题已经非常多了。然而有一个至关重要的主题却很少被专门讲授，而是留给学生们自己去探索。 这部分内容就是：精通工具。在这个系列课程中，我们会帮助您精通命令行、使用强大的文本编辑器、使用版本控制系统提供的多种特性等等。”**

​                                                                                                                                                                  **——【MIT】The Missing Semester**

# Description

Name：MIT-MissingSemester

Time：20h

Tips：Bash  |  Script  |  Vim  |  Data-Wrangling |  Git |  Debuging |  Security

Project：[Learning-CS-fromScratch](https://github.com/rigelJ/Learning-CS-fromScratch/tree/develop/missing_semester)

-----



# GUIDE



## Shell

**如今的计算机有着多种多样的交互接口让我们可以进行指令的的输入，从炫酷的图像用户界面（GUI），语音输入甚至是 AR/VR 都已经无处不在。 这些交互接口可以覆盖 80% 的使用场景，但是它们也从根本上限制了您的操作方式——你不能点击一个不存在的按钮或者是用语音输入一个还没有被录入的指令。 为了充分利用计算机的能力，我们不得不回到最根本的方式，使用文字接口：Shell**



执行指令

- echo  

  - echo "hello world"

    ```bash
    missing:~$ echo hello
    hello
    ```

- $PATH

  - shell通过$PATH的值来寻找echo cd这类执行程序的位置，当我们执行 echo 命令时，shell 了解到需要执行 echo 这个程序，随后它便会在 $PATH 中搜索由 : 所分割的一系列目录，基于名字搜索该程序。当找到该程序时便执行

    ```bash
    missing:~$ echo $PATH
    /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
    ```

- which 

  - 判断该程序是在哪个目录被打开的 

    ```bash
    missing:~$ which echo
    /bin/echo
    missing:~$ /bin/echo $PATH
    /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
    ```

位置导航

- 描述计算机里文件的位置

  - 绝对路径
    - 绝对准确的定义一个文件的位置
    - pwd  查看当前路径
  - 相对路径
    - 相对当前路径所在路径
    - ..  上一层目录
    - .  当前目录
    - ~ 用户相关目录
    - 上一个进入的目录，切换目录

  ```bash
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

- cd   

  - 切换目录
  - 后跟绝对路径或相对路径

- ls

  - 显示当前目录所有文件
  - -l  文件类型、权限
    - rwx权限  
      - 文件
        - r读权限
        - w写权限
        - x执行权限
      - 目录
        - r阅读清单权限
        - w重命名新建删除文件权限
        - x搜索权限

  ````bash
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
  ````

- mv  

  - 重命名或移动文件
  - mv  dotfile.md foo.md

- cp  

  - 复制文件
  - cp  xxx

- rm

  - 删除文件
  - rmdir  
    - 删除目录

创建程序间的链接

- 重定向输出流

  ``` bash
  echo  hello > hello.txt
  ```

- 重定向输入流

  ```bash
  cat < hello.txt
  ```

- 追加

  ```bash
  echo hello >> hello.txt
  ```

- |  管道符号,  允许我们将一个程序的输出和另外一个程序的输入连接起来：

  ```bash
  ls | tail  -n1
  curl --head --silent google.com | grep -i content-length 
  ```

- root权限

  - sudo  使用root权限执行指令
  - tee
    - echo 1000 | sudo tee brightness



----

## VIM

**在编程的时候，你会把大量时间花在阅读/编辑而不是在写代码上。所以，Vim 是一个多模态编辑 器：它对于插入文字和操纵文字有不同的模式。Vim 是可编程的（可以使用 Vimscript 或者像 Python 一样的其他程序语言），Vim 的接口本身也是一个程序语言：键入操作（以及其助记名） 是命令，这些命令也是可组合的。Vim 避免了使用鼠标，因为那样太慢了；Vim 甚至避免用 上下左右键因为那样需要太多的手指移动。**

**这样的设计哲学使得 Vim 成为了一个能跟上你思维速度的编辑器。**



Vim

- 编辑模式

  - 模式切换

    >在默认设置下，Vim 会在左下角显示当前的模式。Vim 启动时的默认模式是正常模式。通常你会把大部分 时间花在正常模式和插入模式。
    >
    >你可以按下 <ESC>（退出键）从任何其他模式返回正常模式。在正常模式，键入 i 进入插入 模式，R 进入替换模式，v 进入可视（一般）模式，V 进入可视（行）模式，<C-v> （Ctrl-V, 有时也写作 ^V）进入可视（块）模式，: 进入命令模式。

  - Normal mode

    - 移动光标
      - hjkl  前后左右
      - wb  前后移动一个单词  e  移到单词末尾
      - 0$ 行首行尾    ^行首的第一个非空字符
      - ctrl  ud   上下翻页
      - HML  屏幕的顶中底
      - gg  G 文件开头结尾
      - f/F+x   移动到上下一个x字符   t/T +x  x前一个字符
    - 编辑删除
      - 插入
        - i  当前插入
        - o/O 上下一行插入
      - 删除编辑复制
        - x 删除当前字符
        - s 替换当前字符
        - d + e   删除到结尾
        - c + e   编辑到结尾
        - y + w  复制一个单词
        - dd/cc/yy  整行删除/编辑/复制
      - 替换
        - r+x   将当前字符替换为x
      - 撤销
        - u  撤销操作 
        - ctrl+r 恢复撤销
      - v  选中
      - p 粘贴
    - 计数操作
      - 4j  向下4行
      - 7dw  往后删除7个单词
      - c2w  往后修改2个单词
    - 修饰符
      - ci( 更改当前括号内容
      - da' 删除单引号字符串 包括周围的字符串

  - Insert mode

    - N + i

  - Replace mode

    - N + r

  - Visual  mode  

    - N + v
    - Visual Line  +shift   一次选中一行
    - Visual Block  +ctrl   按块选中

  - Command Line mode  

    - N + :

    - ：q  结束 

      -  ：qa  结束多个

    - ：w  保存文件

    - :  e  打开文件并编辑

    - : help 帮助

    - : sp  切分同一文件

      - Ctrl + w + hjkl  切换文件

    - ：！ls   指令

    - ：r   读取文件并粘贴

      - : r !ls   可以把命令输出的内容粘贴到当前光标所在处

    - / 搜索

      - /word   在文档中搜索word
      - n  下一个匹配
      - . 重复之前的行动

    - : %s 替换

      ```vim
      %s/foo/bar/gc  替换所有foo为bar,并确认
      
      5,12s/foo/bar/g 将第 5 行到第 12 行（含）的所有行的每个“foo”更改为“bar”。
      ```

- .vimrc 配置文件

  - Vim 由一个位于 ~/.vimrc 的文本配置文件
- Vim 能够被重度自定义，花时间探索自定义选项是值得的。
  - [VIm配置参考]( https://missing-semester-cn.github.io/2020/files/vimrc )

- vim插件 

  - 插件管理器

    - vundle 旧
    - vim plug  新
- nerdtree  文件浏览器
  - CTRLp  文件浏览
- colorscheme  主题切换
  - 更多插件
- [Vim Awesome](https://vimawesome.com )
  
- 其他程序的vim模式

  - Shell
    - export EDITOR=vim。 这是一个用来决定当一个程序需要启动编辑时启动哪个的环境变量。
  - Readline
    - 通过在 ~/.inputrc 添加`set editing-mode vi`

- 其他

  - Vim 的网页浏览快捷键 browsers
  - Google Chrome 的 Vimium 
  - Firefox 的 Tridactyl
  - [其他支持vim键位绑定的软件](https://reversed.top/2016-08-13/big-list-of-vim-like-software )

- vim的拓展学习资料

  - vimtutor  直接在终端键入，这个是最好的教程
- [Vim wiki](http://vim.wikia.com/wiki/Vim_Tips_Wiki )
  - [vim Adventures](https://vim-adventures.com/ "a game to learning vim ")

-----

## Data wrangling

**您是否曾经有过这样的需求，将某种格式存储的数据转换成另外一种格式? 肯定有过，对吧！具体来讲，我们需要不断地对数据进行处理，直到得到我们想要的最终结果。**

**数据整理需要您能够明确哪些工具可以被用来达成特定数据整理的目的，并且明白如何组合使用这些工具。**



Data Wrangling

- bash三剑客

  - awk
    - example
      - `'{print $2}' `  选择第二列
      - `'$1==1 && $2 ~  /^c.*e$/' {print $0}*  `   第一列是1  第二列符合c开头e结尾的模式
      - `‘BEGIN { rows = 0 }  $1==1 $2 ~ /^c.*e$/{rows+=1} END {print rows}’* `   每当匹配到合适的行则row+1 ，最后输出row的值
    - awk
      - 将每一行进行分割按照模块进行操作,awk读取一行，分割后操作，然后下一行，以此类推
      - 格式  awk 【选项】【操作或模式】
      - -F 指定分割字符
      - 内建变量
        - NF	当前处理的行的字段个数（就是：有多少列）
        - NR	当前处理的行的行号（就是：有多少行）
        - FNR	读取文件的记录数（行号），从1开始，新的文件重新从1开始计数
        - $0	当前处理的行的整行内容（就是：表示一行的内容）
        - $n	当前处理行的第n个字段（就是：第n列）
        - FILENAME	被处理的文件名
        - FS	指定每行的字段分隔符，默认为空格或制表位（相当于选项 -F ）
        - OFS	输出字段的分隔符，默认也是空格
      - BEGIN开始和END结尾
        - BEGIN：一般用来做初始化操作，仅在读取数据记录之前执行一次
        - END：一般用来做汇总操作，仅在读取完数据记录之后执行一次
      - 模糊匹配
        - $1 ~ /xx/  xx可以使用标准正则表达式进行匹配
      - 参考网址
        - [awk参考](https://blog.csdn.net/m0_57515995/article/details/125713566)
  - sed 
    - example
      - `cat ssh.log | sed 's/.*Dissconnected from//' * `将以某个模式结尾的部分替换为空
      - `echo "bba"  | sed ‘s/[ab]//g’  `匹配a或者b
      - `echo “abcaba” | sed -E 's/(ab)*//g)'* `匹配ab
      - `echo "abcababc" | sed -E 's/(ab|bc)//g)'  `匹配ab或bc
      - `'s/^.*？Dissconnected from (invalid | authenticating)?  user  (.*)  [0-9.]+ port [0-9]+ (\[preauth\]?$)/ \2/g'`
        - ^$ 开头与结尾
        - ? 0/1次  + 1∞次  . 0∞次  [0-9] 范围  
        - (.*) 且没有修饰符的为捕获组*
        - ？ 改为非贪婪匹配
    - sed
      - 用于对整行进行各种操作
      - 格式 sed 【选项】【操作】 参数
      - 选项
        - -E 使用扩展正则
      - 操作
        - p  输出
          - sed -n ‘4,/the/p’
        - i  插入
          - sed '/the/a 我是谁' 
        - d   删除
          - sed '/\.$/d' 
        - c  替换
        - s  替换指定字符，可以使用正则模式匹配
          - sed  -n 's/the/THE/'
          - g  全部替换
        - g G w  r  a 迁移
          - G  追加指定行后   H 复制到剪贴板
            - sed '1,5/{H;d};14G'
          - w  另存为文件
            -  sed '/the/w out.file'
      - 参考网址
        - [sed](https://blog.csdn.net/qq_57377057/article/details/126216920)
  - grep
    - example
      - `ssh tsp jounralctl  | grep ssh`
      - `sshtsp 'journalctl | grep ssh | grep "Disconnected from"' | less`
      - -v  反选
    - grep 
      - 格式  grep 【参数】【过滤的规则】
      - 参数
        - -n   显示过滤行所在行号
        - -c   显示匹配到的行数
        - -o   只显示匹配到的内容
        - -q  静默输出
        - -i  忽略大小写
        - -v  反向查找，显示不符合匹配的结果
        - -w   匹配某个词
        - -E 使用扩展正则
        - -R 递归查询
          - grep -R "root" /etc/
        - -l   打印文件路径
          - grep -Rl "root" /etc/
        - -A  -B  -C  匹配前后各几n行
          - grep -n -C 2 "mail" /etc/passwd
      - 正则表达式
        - grep的过滤规则中可使用正则表达式进行过滤

- 其他工具

  - wc  -l  行数统计
  - sort   排序
    - -n 数值排序
    - -k  选中空白分割
    - 1，1  从第一列到第一列
  - uniq -c  去掉重复的数据 统计数目
  - tail -n 10  从最后算起的10行
  - paste -sd  改为以tab分割的行
  - bc   简易计算器
    - `echo "1+2" | bc -l	`
    - `awk '$1 !=1 {print $1}' | paste -sd+ | bc -l`
  - R  统计语言
  - gnuplot   图表绘制
  - xargs  将行作为参数传递

- 正则表达式基础

  - [参考]: https://regexone.com/

  - abc…	Letters

  - 123… 	Digit

  - \d  	Any Digit

  - \D 	Any Non-digit character

  - .	Any Character

  - \.	 Period 

  - [abc]	Only a, b, or c

  - [^abc]	Not a, b, nor c

  - [a-z]	Characters a to z

  - [0-9]	Numbers 0 to 9

  - \w 	Any Alphanumeric character

  - \W 	Any Non-alphanumeric character

  - {m}	m  Repetitions

  - {m,n} 	m to n Repetitions

  - .Zero or more repetitions

  - +One or more repetitions

  - ?  Optional character

  - \s 	Any Whitespace

  - \S 	Any Non-whitespace character

  - ^… $	Starts and ends

  - (…) 	Capture Group

  - (a(bc)) 	Capture Sub-group

  - (.*) 	Capture all

  - (abc|def) 	Matches abc or def



----

## Git

**版本控制系统 (VCSs) 是一类用于追踪源代码（或其他文件、文件夹）改动的工具。顾名思义，这些工具可以帮助我们管理代码的修改历史；不仅如此，它还可以让协作编码变得更方便。**

**为什么说版本控制系统非常有用？即使您只是一个人进行编程工作，它也可以帮您创建项目的快照，记录每个改动的目的、基于多分支并行开发等等。和别人协作开发时，它更是一个无价之宝，您可以看到别人对代码进行的修改，同时解决由于并行开发引起的冲突。**

**现代的版本控制系统可以帮助您轻松地（甚至自动地）回答以下问题：**

- **当前模块是谁编写的**
- **这个文件的这一行是什么时候被编辑的？是谁作出的修改？修改原因是什么呢？**
- **最近的1000个版本中，何时/为什么导致了单元测试失败？**

**进行版本控制的方法很多。Git 拥有一个经过精心设计的模型，这使其能够支持版本控制所需的所有特性，例如维护历史记录、支持分支和促进协作。**



Git

- Git的数据模型

  - [自下而上的 Git](https://jwiegley.github.io/git-from-the-bottom-up/1-Repository/4-how-trees-are-made.html)

- Git的命令行接口

  - 配置

    - git config
      - 级别
        - /etc/gitconfig   system系统上所有用户通用
        - ~/.config/git/config  global当前用户
        - .git/config   local当前仓库
        - 高级别可覆盖
      - git config --list  查看所有配置
      - git config --system/global/local xxx=xxx 三级设定  
        -  user.name
        -  user.email
        -  core.editor

  - 帮助

    - git help

  - 基础

    - 获取Git仓库

      - git init  创建一个新的 git 仓库，其数据会存放在一个名为 .git 的目录下
      - git clone  从远端下载仓库
        - git clone -b master  指定clone分支

    - 记录每次更新到仓库

      - git status 显示当前的仓库状态

      - git add <filename> 添加文件到暂存区

      - .gitignore  忽略指定文件

        > 所有空行或者以 `#` 开头的行都会被 Git 忽略。可以使用标准的 glob 模式匹配，它会递归地应用在整个工作区中。匹配模式可以以（`/`）开头防止递归。匹配模式可以以（`/`）结尾指定目录。要忽略指定模式以外的文件或目录，可以在模式前加上叹号（`!`）取反。

      - git diff  查看尚未暂存的文件更新了哪些部分

        - git diff --staged  比对已暂存文件与最后一次提交的文件差异
        - git diff --cached  查看已经暂存起来的变化
        - git diff  <版本1> <版本4> <file>

      - git commit 创建一个新的提交

        - git commit -m xxxx  以说明进行提交
        - git commit -a 自动将修改的都提交

      - rm + git rm  删除某个文件

      - git rm  --cached README 

      - git  mv  filefrom fileto  重命名文件

    - 查看提交历史

      - git log  查找所有历史提交
        - git log -p 显示每次提交的差异
        - git log --stat 显示每次提交被修改的文件
        - git log --pretty=format:"%h - %an, %ar : %s"  定制显示格式
        - git log  --all --graph  --decorate  以流程图的形式显示 历史提交
        - git  log grep  显示说明匹配的的提交‘’

    - 撤销操作

      - git commit --amend  这次提交会合并覆盖上次提交
      - git reset  HEAD  <file> 取消所有暂存区的提交/某个文件的提交
      - git checkout  -- xxxx文件  撤销该文件尚未提交的修改

    - 远端操作

      - git remote add origin https://github.com/schacon/ticgit 添加一个远程仓库
      - git remote rm origin  断开远端仓库
      - git remote  -v 查看已经配置的远程仓库服务器
      - git fetch origin 拉取远端分支信息
      - git branch -r 查看远端分支
      - git remote show origin  获取远程分支的更多信息
      - git push origin master(：master) 将对象传送至远端并更新远端引用
      - 跟踪分支
        - git check out -b test 创建并切换到新分支
        - git  push -u origin test  推送到远程分支，并且跟踪远程分支
        - git checkout -b newtest origin/test 新建分支并跟踪远程分支
        - git branch -u origin/test  设置已有的本地分支跟踪拉取的远程分支
        - git branch -r -d origin/branchname 删除本地跟踪的远程分支
        - git push origin --delete branchname  删除仓库的远程分支

    - 标签

      - 创建标签
        - 附注标签
          - git tag -a v1.4 -m "my version 1.4"
        - 轻量标签
          - git tag v1.4-lw
      - git tag -a v1.2 <版本号> 给之前的某个提交打标签
      - git push origin --tags  推送所有标签到远端
      - 删除标签
        - 删除本地
          -  git tag -d v1.4-lw  
        - 删除远端
          -  git push origin --delete <tagname> 
      - 检出标签对应的文件版本
        -  git checkout 2.0.0

    - 别名

      - git config --global alias.co checkout 

  - 分支

    - git branch testing  创建分支
    - git checkout testing  分支切换
    - git merge  合并分支
      - 合并冲突
        - 打开文件修改冲突后git add，然后commit
      - --no-ff  能够将被合并的分支独立显示
    - git branch 分支管理
      - git branch -v  查看所有分支及其最后一次提交
      - git branch --merge/--no-merge 合并/未合并的分支
    - git branch -d  删除分支，未合并的分支不能删除，强制丢弃使用-D
    - git 分支流
      - master和develop作为常驻分支
      - feature分支
        - 功能分支用以开发新的版本功能，从develop引出，开发功能完成后，再合并回develop
      - release分支
        - 发布分支准备新的生产版本，从develop引出，而后分别合并回develop和master分支
      - hotfix分支
        - 修补分支从master分支创建，比如版本1.2是当前运行版本的一个原因，出现一个错误，因此从master1.2这个位置引出，而后合并回master1.21和develop
      - 参考
        - [git分支工作流](https://nvie.com/posts/a-successful-git-branching-model/)
    - 远程分支
      - git ls-remote <name> 显示远程引用的完整列表
      - git  fetch  更新远端分支情况
      - git push <remote> <branch> 将本地当前分支推送到远程分支
      - git checkout  -b <branch> <remote:branch> 在新的远程分支上建立本地分支，该分支自动跟踪远端分支
      - git branch   -vv 可以看到本地分支的所有跟踪分支
      - git push origin --delete <remotename>  删除服务器上的远端分支
    - 变基
      - 你可以使用 rebase 命令将提交到某一分支上的所有修改都移至另一分支上，就好像“重新播放”一样。merge和rebase的整合方法的最终结果没有任何区别，但是变基使得提交历史更加整洁。
      - git rebase --onto master server client  假设你希望将 client中的修改合并到主分支并发布，但暂时并不想合并 server中的修改， 因为它们还需要经过更全面的测试。这时，你就可以使用git rebase 命令的 --onto 选项

  - 服务器

    - 协议
      - 本地协议  
        - git clone /srv/git/project.git 克隆一个本地版本库
        - git remote add local_proj /srv/git/project.git_ 增加一个本地版本库到现有的 Git 项目
      - HTTP协议
        - 智能HTTP协议
        - 哑HTTP协议
          - 只需要把一个裸版本库放在 HTTP 根目录，设置一个叫做 post-update 的挂钩就可以了 。 此时，只要能访问 web 服务器上你的版本库，就可以克隆你的版本库。
          - `cd /var/www/htdocs/  git clone --bare /path/to/git_project gitproject.git  cd gitproject.git  mv hooks/post-update.sample hooks/post-update  chmod a+x hooks/post-update_  `克隆版本库并放在http的根目录
          - `git clone https://example.com/gitproject.git `访问web服务器并clone版本库
      - SSH协议  
        - git clone ssh://[user@]server/project.git 使用ssh协议克隆版本库
        - 用 SSH 协议的优势有很多。 首先，SSH 架设相对简单 —— SSH 守护进程很常见，多数管理员都有使用经验，并且多数操作系统都包含了它及相关的管理工具。 其次，通过 SSH 访问是安全的 —— 所有传输数据都要经过授权和加密。 最后，与 HTTPS 协议、Git 协议及本地协议一样，SSH 协议很高效，在传输前也会尽量压缩数据。
        - SSH 协议的缺点在于它不支持匿名访问 Git 仓库。 如果你使用 SSH，那么即便只是读取数据，使用者也得通过 SSH 访问你的主机， 这使得 SSH 协议不利于开源的项目，毕竟人们可能只想把你的仓库克隆下来查看。 如果你只在公司网络使用，SSH 协议可能是你唯一要用到的协议。 如果你要同时提供匿名只读访问和 SSH 协议，那么你除了为自己推送架设 SSH 服务以外， 还得架设一个可以让其他人访问的服务。
      - Git协议
        - 最后是 Git 协议。 这是包含在 Git 里的一个特殊的守护进程；它监听在一个特定的端口（9418），类似于 SSH 服务，但是访问无需任何授权。 要让版本库支持 Git 协议，需要先创建一个 `git-daemon-export-ok` 文件 —— 它是 Git 协议守护进程为这个版本库提供服务的必要条件 —— 但是除此之外没有任何安全措施。 要么谁都可以克隆这个版本库，要么谁也不能。 这意味着，通常不能通过 Git 协议推送。 由于没有授权机制，一旦你开放推送操作，意味着网络上知道这个项目 URL 的人都可以向项目推送数据。
    - 服务器上搭建Git
      - `git clone --bare my_project_ my_project.git_` 将现有仓库导出为裸仓库--即不包含当前工作目录
      - `scp -r my_project.git user@git.example.com:/srv/git_  `若服务器上存在/srv/git目录，复制裸仓库来创建一个新仓库
      - `git clone user@git.example.com:/srv/git/my_project.git_` 克隆你的仓库，如果一个用户，通过使用 SSH 连接到一个服务器，并且其对 /srv/git/my_project.git_ 目录拥有可写权限，那么他将自动拥有推送权限。
      - `ssh user@git.example.com cd /srv/git/my_project.git   git init --bare --shared`  如果到该项目目录中运行  git init  命令，并加上  --shared  选项， 那么 Git 会自动修改该仓库目录的组权限为可写。 注意，运行此命令的工程中不会摧毁任何提交、引用等内容。
    - [剩余参考架设git服务器](https://git-scm.com/book/zh/v2/%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%B8%8A%E7%9A%84-Git-%E5%8D%8F%E8%AE%AE)

  - Github 

    - [参考Git - 账户的创建和配置 (git-scm.com)](https://git-scm.com/book/zh/v2/GitHub-%E8%B4%A6%E6%88%B7%E7%9A%84%E5%88%9B%E5%BB%BA%E5%92%8C%E9%85%8D%E7%BD%AE)

- Git差错补救

  - [如何从错误中恢复](https://ohshitgit.com/#magic-time-machine)



---

## Debugging

**代码不能完全按照您的想法运行，它只能完全按照您的写法运行，这是编程界的一条金科玉律。**

**让您的写法符合您的想法是非常困难的。在这节课中，我们会传授给您一些非常有用技术，帮您处理代码中的 bug 和程序性能问题。**



Debuging

- printf
  - 调试代码的第一种方法往往是在您发现问题的地方添加一些打印语句，然后不断重复此过程直到您获取了足够的信息并找到问题的根本原因。
- log
  - 优势
    - 您可以将日志写入文件、socket 或者甚至是发送到远端服务器而不仅仅是标准输出
    - 日志可以支持严重等级（例如 INFO, DEBUG, WARN, ERROR等)，这使您可以根据需要过滤日志
    - 对于新发现的问题，很可能您的日志中已经包含了可以帮助您定位问题的足够的信息。
  - 优化日志可读性
    - `echo -e "\e[38;2;255;0;0mThis is red\e[0m" `会打印红色的字符串
  - 第三方日志系统
    - 对于 UNIX 系统来说，程序的日志通常存放在 /var/log，例如，nginx web 服务器就将其日志存放于 /var/log/nginx
    - 目前，系统开始使用 system log，您所有的日志都会保存在这里。大多数（但不是全部的）Linux 系统都会使用 systemd，systemd 会将日志以某种特殊格式存放于 /var/log/journal
    - 类似地，在 macOS 系统中是 /var/log/system.log，但是有更多的工具会使用系统日志，它的内容可以使用 log show 显示。
    - 对于大多数的 UNIX 系统，您也可以使用 dmesg 命令来读取内核的日志。
  - 向系统日志中写日志
    - 写入日志
      - `logger “Hello Logs”`
    - 查看是否写入 
      - `log show --last 1m | grep Hello  MacOS`
      - `journalctl --since  "1m ago" | grep Hello  LINUX`
- 代码调试
  - 调试器是一种可以允许我们和正在执行的程序进行交互的程序
    - 调试器可以实现
      - 当到达某一行时将程序暂停；
      - 一次一条指令地逐步执行程序；
      - 程序崩溃后查看变量的值；
      - 满足特定条件时暂停程序；
  - pdb Python使用的调试器
    - `pip install --user ipdb ` 下载pdb调试器
    - `python -m ipdb  bubble.py`  用pdb调试python程序
    - 常用指令
      - l(ist) - 显示当前行附近的11行或继续执行之前的显示；
      - s(tep) - 执行当前行，并在第一个可能的地方停止；
      - n(ext) - 继续执行直到当前函数的下一条语句或者 return 语句；
      - b(reak) - 设置断点（基于传入的参数）；
      - p(rint) - 在当前上下文对表达式求值并打印结果。
      - r(eturn) - 继续执行直到当前函数返回；
      - q(uit) - 退出调试器。
      - len() 长度
      - ！c 检视c的值，！后是python值
    - 参考
      - [MartinLwx/pdb-tutorial: A simple tutorial about effectively using pdb (github.com)](https://github.com/MartinLwx/pdb-tutorial)
  - 其他调试器
    - gdb 
    - lldb
  - 调试工具
    - strace  追踪程序执行的系统调用
      - strace作为一种动态跟踪工具，能够帮助运维高效地定位进程和服务故障。
      - strace能够打开应用进程的这个黑盒，通过系统调用的线索，告诉你进程的行为
        - 系统调用
          - 系统调用（英语：system call），又称为系统呼叫，指运行在用户空间的程序向操作系统内核请求需要更高权限运行的服务。
          - linux常见的系统调用
            - open/close/read/write/chmod等 文件和设备访问类
            - fork/clone/execve/exit/getpid等  进程管理类 
            - signal/sigaction/kill 等  信号类 
            - brk/mmap/mlock等  内存管理 
            - IPC shmget/semget  进程间通信
            - socket/connect/sendto/sendmsg 信号量，共享内存，消息队列等
      - strace的两种运行模式
        - `strace ls -lh /var/log/messages ` 通过它启动要跟踪的进程
        - `strace -p 17553 `通过查看pid通过pid跟踪
      - strace选项
        - -tt 在每行输出的前面，显示毫秒级别的时间
        - -T 显示每次系统调用所花费的时间
        - -v 对于某些相关调用，把完整的环境变量，文件stat结构等打出来。
        - -f 跟踪目标进程，以及目标进程创建的所有子进程
        - -e 控制要跟踪的事件和跟踪行为,比如指定要跟踪的系统调用名称
          - -e trace=file   跟踪和文件访问相关的调用(参数中有文件名)
          - -e trace=process  和进程管理相关的调用，比如fork/exec/exit_group
          - -e trace=network  和网络通信相关的调用，比如socket/sendto/connect
          - -e trace=signal    信号发送和处理相关，比如kill/sigaction
          - -e trace=desc  和文件描述符相关，比如write/read/select/epoll等
          - -e trace=ipc 进程见同学相关，比如shmget等-o 把strace的输出单独写到指定的文件
        - -s 当系统调用的某个参数是字符串时，最多输出指定长度的内容，默认是32个字节
        - -p 指定要跟踪的进程pid, 要同时跟踪多个pid, 重复多次-p选项即可。 
      - strace 实例
        - `strace -tt -T -f -e trace=file -o /data/log/strace.log -s 1024 ./nginx ` 跟踪nginx, 看其启动时都访问了哪些文件
    - tcpdump/wireshark 网络数据包分析工具
  - 静态分析
    - pyflakes
      - 当我们使用 pyflakes 分析代码的时候，我们会得到与这两处 bug 相关的错误信息。
    - mypy
    - other code linter
      - python
        - pylint
        - pep8
        - bandit
      - shell
        - shellcheck
      - vim
        - ale
        - syntastic
      - 其他语言
        - [analys-tools-dev/static-analysis](https://github.com/analysis-tools-dev/static-analysis)
        - [caramelomartins/awesome-linters](https://github.com/caramelomartins/awesome-linters)
- 性能分析
  - time
    - 对于工具来说，需要区分真实时间、用户时间和系统时间。
      - real - 从程序开始到结束流失掉的真实时间，包括其他进程的执行时间以及阻塞消耗的时间（例如等待 I/O或网络）；
      - user- CPU 执行用户代码所花费的时间；
      - sys - CPU 执行系统内核代码所花费的时间。
    - time curl https://missing.csail.mit.edu &> /dev/null  可以看到三种时间输出
  - 性能分析工具
    - CPU时间
      - 大多数情况下，当人们提及性能分析工具的时候，通常指的是 CPU 性能分析工具,CPU 性能分析工具有两种： 追踪分析器（tracing）及采样分析器（sampling）
        - 追踪分析器 会记录程序的每一次函数调用
        - 采样分析器则只会周期性的监测（通常为每毫秒）您的程序并记录程序堆栈。
      - Python中的cProfile模块
        - `python -m cProfile -s tottime grep.py 1000 '^(import|\s*def)[^,]*$' *.py *  `分析每次函数调用所消耗的时间
        - 它显示的是每次函数调用的时间，看上去可能快到反直觉，尤其是如果您在代码里面使用了第三方的函数库，因为内部函数调用也会被看作函数调用
        - ![image-20230319162231081](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20230319162231081.png)
      - line profiler 分析器
        - 如果我们使用 line profiler，它会基于行来显示时间
        - pip  install line_profiler_  安装kernprof工具
        - 装饰您要用@profile配置文件的功能。装饰器将在运行时自动可用。
        - kernprof -l -v aaa.py  使用kernprof工具分析，逐行判断所用时间
        - ![image-20230319162244327](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20230319162244327.png)
    - 内存占用
      - 像 C 或者 C++ 这样的语言，内存泄漏会导致您的程序在使用完内存后不去释放它。++为了应对内存类的 Bug，我们可以使用类似 [Valgrind](https://valgrind.org/) 这样的工具来检查内存泄漏问题。
      - 对于 Python 这类具有垃圾回收机制的语言，内存分析器也是很有用的，因为对于某个对象来说，只要有指针还指向它，那它就不会被回收。
        - memory-profiler
          - python -m memory_profiler example.py _ 逐行分析所占用的内存
          - ![image-20230319162251551](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20230319162251551.png)
    - 事件分析
      - perf
        - [perf](http://man7.org/linux/man-pages/man1/perf.1.html) 命令将 CPU 的区别进行了抽象，它不会报告时间和内存的消耗，而是报告与您的程序相关的系统事件。
    - 可视化
      - 对于*采样分析器*来说，常见的显示 CPU 分析数据的形式是 [火焰图](http://www.brendangregg.com/flamegraphs.html)，火焰图会在 Y 轴显示函数调用关系，并在 X 轴显示其耗时的比例。火焰图同时还是可交互的，您可以深入程序的某一具体部分，并查看其栈追踪（您可以尝试点击下面的图片）。
        - 					![image-20230319162259009](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20230319162259009.png)
      - *调用图和控制流图*可以显示子程序之间的关系，它将函数作为节点并把函数调用作为边。将它们和分析器的信息（例如调用次数、耗时等）放在一起使用时，调用图会变得非常有用，它可以帮助我们分析程序的流程。
        -  在 Python 中您可以使用[pycallgraph](http://pycallgraph.slowchop.com/en/master/) 来生成这些图片。
        -  ![image-20230319162304527](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20230319162304527.png)
    - 资源监控
      - 有时候，分析程序性能的第一步是搞清楚它所消耗的资源。程序变慢通常是因为它所需要的资源不够了。例如，没有足够的内存或者网络连接变慢的时候。
      - 通用监控
        - htop
          - htop 可以显示当前运行进程的多种统计信息。htop 有很多选项和快捷键，常见的有：`<F6>` 进程排序、 `t` 显示树状结构和 `h` 打开或折叠线程。 
        - glances
          - 它的实现类似但是用户界面更好。如果需要合并测量全部的进程，
        - dstat
          - 它可以实时地计算不同子系统资源的度量数据，例如 I/O、网络、 CPU 利用率、上下文切换等等；
      - I/O
        - iotop
          -  可以显示实时 I/O 占用信息而且可以非常方便地检查某个进程是否正在执行大量的磁盘读写操作；
      - 磁盘使用
        - df
          - 可以显示每个分区的信息
        - du
          - 显示当前目录下每个文件的磁盘使用情况
        - ncdu
          - 是一个交互性更好的 du ，它可以让您在不同目录下导航、删除文件和文件夹；
      - 内存使用
        - free
          - 可以显示系统当前空闲的内存
      - 打开文件
        - lsof
          - 可以列出被进程打开的文件信息。 当我们需要查看某个文件是被哪个进程打开的时候，这个命令非常有用
      - 网络链接配置 
        - ss
          - 监控网络包的收发情况以及网络接口的显示信息，常见的一个使用场景是找到端口被进程占用的信息。如果要显示路由、网络设备和接口信息，您可以使用ip
      - 网络使用
        - [nethogs](https://github.com/raboof/nethogs) 和[iftop](http://www.ex-parrot.com/pdw/iftop/)是非常好的用于对网络占用进行监控的交互式命令行工具。
    - 软件评估
      - 有时候，您只需要对黑盒程序进行基准测试，并依此对软件选择进行评估。
      - hyperfine
        - hyperfine可以帮您快速进行基准测试
        - hyperfine --warmup 3 'fd -e jpg'  'find . -iname "*.jpg"' * 测试fd与find的速度
          - 						![image-20230319162312344](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20230319162312344.png)

---

## Metaprogramming

**我们这里说的 “元编程（metaprogramming）” 是什么意思呢？好吧，对于本文要介绍的这些内容，这是我们能够想到的最能概括它们的词。因为我们今天要讲的东西，更多是关于 流程 ，而不是写代码或更高效的工作。本节课我们会学习构建系统、代码测试以及依赖管理。**



Metaprogramming
- 构建系统
	- 对于大多数系统来说，不论其是否包含代码，都会包含一个“构建过程”。有时，您需要执行一系列操作。通常，这一过程包含了很多步骤，很多分支。执行一些命令来生成图表，然后执行另外的一些命令生成结果，然后再执行其他的命令来生成最终的论文。
	- 从本质上讲，这些工具都是非常类似的。您需要定义依赖、目标和规则。您必须告诉构建系统您具体的构建目标，系统的任务则是找到构建这些目标所需要的依赖，并根据规则构建所需的中间产物，直到最终目标被构建出来。
	- 构建工具
		- make
			- paper.pdf:  paper.tex plot-data.png  | pdflatex paper.tex
			- plot-%.png:  %.dat plot.py  | ./plot.py -i  $*.dat -o  $@*
			- 这个文件中的指令，即如何使用右侧文件构建左侧文件的规则。或者，换句话说，冒号左侧的是构建目标，冒号右侧的是构建它所需的依赖。缩进的部分是从依赖构建目标时需要用到的一段程序。
			- 规则中的 % 是一种模式，它会匹配其左右两侧相同的字符串。
- 依赖管理
	- 就您的项目来说，它的依赖可能本身也是其他的项目。您也许会依赖某些程序(例如 python)、系统包 (例如 openssl)或相关编程语言的库(例如 matplotlib)。
	- 现在，大多数的依赖可以通过某些软件仓库来获取，这些仓库会在一个地方托管大量的依赖，我们则可以通过一套非常简单的机制来安装依赖。例如 Ubuntu 系统下面有Ubuntu软件包仓库，您可以通过 apt 这个工具来访问， RubyGems 则包含了 Ruby 的相关库，PyPi 包含了 Python 库，
	- 版本控制
		- 大多数被其他项目所依赖的项目都会在每次发布新版本时创建一个版本号。通常看上去像 8.1.3 或 64.1.20192004。版本号一般是数字构成的，但也并不绝对。
		- 我们可以指定当前项目需要基于某个版本，甚至某个范围内的版本，或是某些项目来构建。这么做的话，即使某个被依赖的库发生了变化，依赖它的软件可以基于其之前的版本进行构建。
		- 不同项目所用的版本号其具体含义并不完全相同，但是一个相对比较常用的标准是[语义版本号](https://semver.org/)，这种版本号具有不同的语义，它的格式是这样的：主版本号.次版本号.补丁号。
			- 如果新的版本没有改变 API，请将补丁号递增；
			- 如果您添加了 API 并且该改动是向后兼容的，请将次版本号递增；
			- 如果您修改了 API 但是它并不向后兼容，请将主版本号递增。
		- 这么做有很多好处。现在如果我们的项目是基于您的项目构建的，那么只要最新版本的主版本号只要没变就是安全的 ，次版本号不低于之前我们使用的版本即可。换句话说，如果我依赖的版本是`1.3.7`，那么使用`1.3.8`、`1.6.1`，甚至是`1.3.0`都是可以的。如果版本号是 `2.2.4` 就不一定能用了，因为它的主版本号增加了。
		- 使用依赖管理系统的时候，您可能会遇到锁文件（*lock files*）这一概念
			- 锁文件列出了您当前每个依赖所对应的具体版本号。通常，您需要执行升级程序才能更新依赖的版本。这么做的原因有很多，例如避免不必要的重新编译、创建可复现的软件版本或禁止自动升级到最新版本（可能会包含 bug）。
- 持续集成
	- 随着您接触到的项目规模越来越大，您会发现修改代码之后还有很多额外的工作要做。您可能需要上传一份新版本的文档、上传编译后的文件到某处、发布代码到 pypi，执行测试套件等等。或许您希望每次有人提交代码到 GitHub 的时候，他们的代码风格被检查过并执行过某些基准测试？如果您有这方面的需求，那么请花些时间了解一下持续集成。
	- 持续集成，或者叫做 CI ，它指的是那些“当您的代码变动时，自动运行的东西”，市场上有很多提供各式各样 CI 工具的公司，这些工具大部分都是免费或开源的。比较大的有 Travis CI、Azure Pipelines 和 GitHub Actions。
	- 它们的工作原理都是类似的：您需要在代码仓库中添加一个文件，描述当前仓库发生任何修改时，应该如何应对。目前为止，最常见的规则是：如果有人提交代码，执行测试套件。当这个事件被触发时，CI 提供方会启动一个（或多个）虚拟机，执行您制定的规则，并且通常会记录下相关的执行结果。您可以进行某些设置，这样当测试套件失败时您能够收到通知或者当测试全部通过时，您的仓库主页会显示一个徽标。
- 测试简介
	- - 测试套件：所有测试的统称。
	- 单元测试：一种“微型测试”，用于对某个封装的特性进行测试。
	- 集成测试：一种“宏观测试”，针对系统的某一大部分进行，测试其不同的特性或组件是否能协同工作。
	- 回归测试：一种实现特定模式的测试，用于保证之前引起问题的 bug 不会再次出现。
	- 模拟（Mocking）: 使用一个假的实现来替换函数、模块或类型，屏蔽那些和测试不相关的内容。例如，您可能会“模拟网络连接” 或 “模拟硬盘”。



---

## Security

**我们将关注比如散列函数、密钥生成函数、对称/非对称密码体系这些安全和密码学的概念是如何应用于前几节课所学到的工具（Git和SSH）中的。**

**本课程不能作为计算机系统安全 (6.858) 或者 密码学 (6.857以及6.875)的替代。 如果你不是密码学的专家，请不要试图创造或者修改加密算法。从事和计算机系统安全相关的工作同理。**

**这节课将对一些基本的概念进行简单（但实用）的说明。 虽然这些说明不足以让你学会如何 设计 安全系统或者加密协议，但我们希望你可以对现在使用的程序和协议有一个大概了解。**



Security

-  熵
  -   [熵](https://en.wikipedia.org/wiki/Entropy_(information_theory))度量了不确定性并可以用来决定密码的强度。
  -  熵的单位是 比特。对于一个均匀分布的随机离散变量，熵等于log*2(n)* n代表所有可能的个数，比如一个骰子就是6，硬币就是2，一个六面骰子的熵为log2（6）
-  散列函数
  -   [密码散列函数](https://en.wikipedia.org/wiki/Cryptographic_hash_function) (Cryptographic hash function) 可以将任意大小的数据映射为一个固定大小的输出。
  -   [SHA-1](https://en.wikipedia.org/wiki/SHA-1)可以将任意大小的输入映射为一个160比特（可被40位十六进制数表示）的输出。
  -  散列函数可以被认为是一个不可逆，看上去随机，具有确定性的函数 
  -  散列函数的应用
  	-  Git中的内容寻址存储(Content addressed storage)
  	-  文件的信息摘要(Message digest)， 用户从镜像站下载安装文件后可以对照公布的哈希值来确定安装文件没有被篡改。
  -  密钥生成函数
  	-  针对每个用户随机生成一个盐 salt = random() ，并存储盐，以及密钥生成函数对连接了盐的明文密码生成的哈希值KDF(password + salt)。在验证登录请求时，使用输入的密码连接存储的盐重新计算哈希值，KDF(input + salt)，并与存储的哈希值对比。
-  对称加密
  -  对称加密中加解密所使用的密钥是相同的 
  -   [AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard) 是现在常用的一种对称加密系统。
-  非对称加密
  -  非对称加密使用两个具有不同功能的密钥： 一个是私钥(private key)，不向外公布；另一个是公钥(public key)，公布公钥不像公布对称加密的共享密钥那样可能影响加密体系的安全性。
  -  非对称加密进行加密时，使用公钥对信息进行加密，解密时再使用私钥进行解密。
  -  非对称加密的签名与验证
  	-  签名
  		-  首先对信息进行哈希计算，得到哈希值
  		-  而后使用私钥对得到的哈希进行运算得到密钥
  		-  将签名附在信息后发送
  	-  验证签名
  		-  收到消息后，提取消息的签名部分
  		-  用公钥对消息进行运算得到哈希1
  		-  对消息正文进行哈希运算得到哈希2
  		-  比对12得出结论
  	-  权威机构的签名称为证书
-  密钥分发
  -  Signal的信任模型是，信任用户第一次使用时给出的身份，同时支持用户线下面对面交换公钥
  -  PGP使用的是信任网络,简单来说，如果我想加入一个信任网络，则必须让已经在信任网络中的成员对我进行线下验证，验证无误后，信任网络的成员使用私钥对我的公钥进行签名。这样我就成为了信任网络的一部分。
  	-  信任网络的具体实现方式
  		-  比方说，A给了我一个公钥，我信任他给我的公钥，于是将公钥加上自己的签名放入公钥串
  		-  当A发送一个加密消息给我时，他将消息用自己的私钥签名后，将签名附带在消息后发送
  		-  我收到消息，首先对签名真实性进行验证，要验证发送的消息是否A，那么我就要通过他附带的签名，因此需要A的公钥
  		-  我在公钥串中寻找A的公钥，找到后，通过公钥后签名验证公钥合法性后使用该公钥对附带的签名进行验证，合法则说明这个信息确实来自A
  	-  GPG 加密软件
  		-  具体实现方式
  			-  生成公私钥
  			-  密钥管理
  				-  列出密钥
  				-  删除密钥
  					-  删除私钥
  					-  删除公钥
  				-  输出密钥
  					-  输出二进制密钥
  					-  输出ASCII密钥
  				-  输入密钥
  					-  从文件输入
  					-  从密钥服务器输入
  				-  上传密钥
  			-  加密与解密
  				-  加密
  				-  解密
  			-  签名
  				-  对文件签名
  					-  二进制签名
  					-  ASCII码签名
  					-  单独签名
  				-  签名+加密
  				-  验证签名
  		-  实现参考
  			-   [阮一峰的GPG教程](https://www.ruanyifeng.com/blog/2013/07/gpg.html)
  			-   [GPG使用教程](https://blog.csdn.net/qq_33919450/article/details/115706604)
  -  [Keybase](https://keybase.io/blog/chat-apps-softer-than-tofu)主要使用社交网络证明 (social proof)，和一些别的精巧设计。
-  案例分析
  -  密码管理器
  	-  密码管理器会帮助你对每个网站生成随机且复杂（表现为高熵）的密码，并使用你指定的主密码配合密钥生成函数来对称加密它们。
  -  两步验证
  	-   [两步验证](https://en.wikipedia.org/wiki/Multi-factor_authentication)要求用户同时使用密码（“你知道的信息”）和一个身份验证器（“你拥有的物品”，比如[YubiKey](https://www.yubico.com/)来消除密码泄露或者[钓鱼攻击](https://en.wikipedia.org/wiki/Phishing)的威胁。
  -  全盘加密
  	-  使用一个由密码保护的对称密钥来加密盘上的所有信息。
  -  聊天加密
  	-   [Signal](https://signal.org/)和[Keybase](https://keybase.io/)使用非对称加密对用户提供端到端(End-to-end)安全性。
  	-  为了保证安全性，应使用线下方式验证Signal或者Keybase的用户公钥，或者信任Keybase用户提供的社交网络证明。
  -  SSH
  	-  当你运行`ssh-keygen`命令，它会生成一个非对称密钥对：公钥和私钥(public*key, private*key)。
  	-  公钥最终会被分发，它可以直接明文存储。 但是为了防止泄露，私钥必须加密存储。
  	-   `ssh-keygen`命令会提示用户输入一个密码，并将它输入密钥生成函数 产生一个密钥。最终，`ssh-keygen`使用对称加密算法和这个密钥加密私钥。
  	-  在实际运用中，当服务器已知用户的公钥（存储在`.ssh/authorized_keys`文件中，一般在用户HOME目录下），尝试连接的客户端可以使用非对称签名来证明用户的身份——这便是[挑战应答方式](https://en.wikipedia.org/wiki/Challenge%E2%80%93response_authentication)。 简单来说，服务器选择一个随机数字发送给客户端。客户端使用用户私钥对这个数字信息签名后返回服务器。 服务器随后使用`.ssh/authorized_keys`文件中存储的用户公钥来验证返回的信息是否由所对应的私钥所签名。这种验证方式可以有效证明试图登录的用户持有所需的私钥。


---

## potpourri

potpourri
- 修改键位映射
	- [Linux - xmodmap](https://wiki.archlinux.org/index.php/Xmodmap) 或者 [Autokey](https://github.com/autokey/autokey)
	- Windows - 控制面板，[AutoHotkey](https://www.autohotkey.com/) 或者 [SharpKeys](https://www.randyrants.com/category/sharpkeys/)
- 守护进程
  - 大部分计算机都有一系列在后台保持运行，不需要用户手动运行或者交互的进程。这些进程就是守护进程。
  - systemd
    - Linux 中的 `systemd`（the system daemon）是最常用的配置和运行守护进程的方法。
    - 用户使用 `systemctl` 命令和 `systemd` 交互来`enable`（启用）、`disable`（禁用）、`start`（启动）、`stop`（停止）、`restart`（重启）、或者`status`（检查）配置好的守护进程及系统服务。
    - 如果你只是想定期运行一些程序，可以直接使用 [cron](https://www.man7.org/linux/man-pages/man8/cron.8.html)。它是一个系统内置的，用来执行定期任务的守护进程。
    - 使用了守护进程来运行一个简单的 Python 程序
    - ![image-20230319165320134](https://blogqc.oss-cn-guangzhou.aliyuncs.com/image/image-20230319165320134.png)
- FUSE
	- [FUSE](https://en.wikipedia.org/wiki/Filesystem_in_Userspace)（用户空间文件系统）允许运行在用户空间上的程序实现文件系统调用，并将这些调用与内核接口联系起来。
	- FUSE 可以用于实现如：一个将所有文件系统操作都使用 SSH 转发到远程主机，由远程主机处理后返回结果到本地计算机的虚拟文件系统。
	- 一些FUSE文件系统
		- [sshfs](https://github.com/libfuse/sshfs)：使用 SSH 连接在本地打开远程主机上的文件
		- [rclone](https://rclone.org/commands/rclone_mount/)：将 Dropbox、Google Drive、Amazon S3、或者 Google Cloud Storage 一类的云存储服务挂载为本地文件系统
- 备份
	- 有效备份方案的几个核心特性是：版本控制，删除重复数据，以及安全性。
- API
	- 大多数线上服务提供的 API（应用程序接口）让你可以通过编程方式来访问这些服务的数据。
	- 这些 API 大多具有类似的格式。它们的结构化 URL 通常使用 `api.service.com` 作为根路径，用户可以访问不同的子路径来访问需要调用的操作，以及添加查询参数使 API 返回符合查询参数条件的结果。
	- [IFTTT](https://ifttt.com/) 这个网站可以将很多 API 整合在一起，让某 API 发生的特定事件触发在其他 API 上执行的任务。IFTTT 的全称If This Then That 足以说明它的用法，比如在检测到用户的新推文后，自动发布在其他平台。
- 常见命令行标志参数
	- - help 帮助
	- -i  交互式操作
	- - v 查看版本
	- -vvv 查看详细版本
	- -r  递归执行
	- --   将--后出现的参数作为普通内容
- VPN
	- MIT 向有访问校内资源需求的成员开放自己运营的 [VPN](https://ist.mit.edu/vpn)。如果你也想自己配置一个 VPN，可以了解一下 [WireGuard](https://www.wireguard.com/)Live USB 是包含了完整操作系统的闪存盘。 以及 [Algo](https://github.com/trailofbits/algo)。
- Markdown
- Live USB
	- [Live USB](https://en.wikipedia.org/wiki/Live_USB) 是包含了完整操作系统的闪存盘。
	- Live USB 的用途
		- 作为安装操作系统的启动盘；
		- 在不将操作系统安装到硬盘的情况下，直接运行 Live USB 上的操作系统；
		- 对硬盘上的相同操作系统进行修复；
		- 恢复硬盘上的数据。
	- 你可以使用[UNetbootin](https://unetbootin.github.io/) 、[Rufus](https://github.com/pbatard/rufus) 等 Live USB 写入工具制作。
- Docker,Vagrant,VMS
	- [虚拟机](https://en.wikipedia.org/wiki/Virtual_machine)（Virtual Machine）以及容器化（containerization）等工具可以帮助你模拟一个包括操作系统的完整计算机系统。
	- [Vagrant](https://www.vagrantup.com/) 是一个构建和配置虚拟开发环境的工具。它支持用户在配置文件中写入比如操作系统、系统服务、需要安装的软件包等描述，然后使用 `vagrant up` 命令在各种环境（VirtualBox，KVM，Hyper-V等）中启动一个虚拟机。[Docker](https://www.docker.com/) 是一个使用容器化概念的类似工具。
	- 租用云端虚拟机可以享受以下资源的即时访问：
		- 便宜、常开、且有公共IP地址的虚拟机用来托管网站等服务
		- 有大量 CPU、磁盘、内存、以及 GPU 资源的虚拟机
		- 超出用户可以使用的物理主机数量的虚拟机
	- 受欢迎的 VPS 服务商有 [Amazon AWS](https://aws.amazon.com/)，[Google Cloud](https://cloud.google.com/),[Microsoft Azure](https://azure.microsoft.com/)以及[DigitalOcean](https://www.digitalocean.com/)。
- 交互式记事本编程
	- 现在最受欢迎的交互式记事本环境大概是 [Jupyter](https://jupyter.org/)



----

# End

