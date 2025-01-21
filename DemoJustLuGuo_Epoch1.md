# CFC Studio 共学 Epoch1 指引

---

# [DemoJustLuGuo]

## 笔记证明

<!-- Content_START --> 

### 01.06

#### 学习时长：50 分钟

跟着视频在进行基本命令行的学习 (使用 powershell)

在运行 ls -l 命令时 powershell 突然报错：

> Get-ChildItem: Missing an argument for parameter 'LiteralPath'. Specify a parameter of type 'System.String[]' and try again.

百度后发现错误是因为 Powershell 使用-LiteralPath，因为该选项与-l 匹配，但它需要一个参数。（这里应该是 windows 与 linux 命令使用的差异导致的）
查阅命令帮助后发现 powershell 可直接使用 ls 或 dir、gci 等命令列出文件目录

> 或者使用 ls -Path 'C:\Users\YourUsername\Documents'

在此之前使用查看环境变量 echo $PATH命令也遇到了同样的问题，不过在经过弹幕提醒后知道了windows的powershell使用的是$env:path 命令

总结：最近的时间比较紧，今天就先看到这里，使用 powershell 的原因是我忽视了 windows 与 linux 之间的区别，在学习之时被这些奇妙错误搞麻了，目前已老实安装 bash，等考试完后会补上接下来的课程的。

### 01.08

#### 学习时长：50 分钟

安装了 wsl 之后学习完了第一节的内容

基本都是跟着视频在打，蛮不错的，除了 wsl 是虚拟机导致一些内核的改不了之外，其他的没有遇到什么问题。做了课后作业，就先传上来吧，还有一科没考完呢。

```bash
 sakuraauro@DemoJustLuGuo:/tmp/$ cd /tmp
 sakuraauro@DemoJustLuGuo:/tmp/$ mkdir missing
 sakuraauro@DemoJustLuGuo:/tmp$ ls
missing
snap-private-tmp
systemd-private-856d00b5580a4e4ab51e9660bc84158c-polkit.service-7eTcE0
systemd-private-856d00b5580a4e4ab51e9660bc84158c-systemd-logind.service-kBkmIl
systemd-private-856d00b5580a4e4ab51e9660bc84158c-systemd-resolved.service-uWN9Q6
systemd-private-856d00b5580a4e4ab51e9660bc84158c-systemd-timesyncd.service-kXJsTp
systemd-private-856d00b5580a4e4ab51e9660bc84158c-wsl-pro.service-jXoXvM
  sakuraauro@DemoJustLuGuo:/tmp$ cd missing
  sakuraauro@DemoJustLuGuo:/tmp/missing$ touch semester
  sakuraauro@DemoJustLuGuo:/tmp/missing$ ls
semester
  sakuraauro@DemoJustLuGuo:/tmp/missing$ echo '#!/bin/sh' > semester
  sakuraauro@DemoJustLuGuo:/tmp/missing$ echo 'curl --head --silent https://missing.csail.mit.edu' >> sem
ester
  sakuraauro@DemoJustLuGuo:/tmp/missing$ cat semester
#!/bin/sh
curl --head --silent https://missing.csail.mit.edu.com
  sakuraauro@DemoJustLuGuo:/tmp/missing$ /tmp/missing/semester
-bash: /tmp/missing/semester: Permission denied
  sakuraauro@DemoJustLuGuo:/tmp/missing$ sudo /tmp/missing/semester
sudo: /tmp/missing/semester: command not found
  sakuraauro@DemoJustLuGuo:/tmp/missing$ man chmod
  sakuraauro@DemoJustLuGuo:/tmp/missing$ ls -l
total 8
drwxr-xr-x 2 sakuraauro sakuraauro 4096 Jan 8 22:18 missing
-rw-r--r-- 1 sakuraauro sakuraauro 65 Jan 8 22:33 semester
  sakuraauro@DemoJustLuGuo:/tmp/missing$ chmod 777 semester
  sakuraauro@DemoJustLuGuo:/tmp/missing$ ls -l
total 8
drwxr-xr-x 2 sakuraauro sakuraauro 4096 Jan 8 22:18 missing
-rwxrwxrwx 1 sakuraauro sakuraauro 65 Jan 8 22:33 semester
  sakuraauro@DemoJustLuGuo:/tmp/missing$ ./semester
  sakuraauro@DemoJustLuGuo:/tmp/missing$ sudo ./semester(没输出？ 好像还是执行不出来)
  sakuraauro@DemoJustLuGuo:/tmp/missing$ ls -l
total 8
drwxr-xr-x 2 sakuraauro sakuraauro 4096 Jan 8 22:18 missing
-rwxrwxrwx 1 sakuraauro sakuraauro 65 Jan 8 22:33 semester
  sakuraauro@DemoJustLuGuo:/tmp/missing$ cd
  sakuraauro@DemoJustLuGuo:~$ echo '-rwxrwxrwx 1 sakuraauro sakuraauro 65 Jan 8 22:33 semester' > last-modified.txt
  sakuraauro@DemoJustLuGuo:~$ ls -l
total 8
 drwxr-xr-x 2 sakuraauro sakuraauro 4096 Jan 8 21:10 TEST
-rw-r--r-- 1 sakuraauro sakuraauro 62 Jan 8 22:41 last-modified.txt
  sakuraauro@DemoJustLuGuo:~$ cd /sys/class/power_supply/BAT1
  sakuraauro@DemoJustLuGuo:/sys/class/power_supply/BAT1$ cat capacity
94
```
### 01.10

#### 学习时长：1小时

Bash 中的字符串通过 ' 和 " 分隔符来定义，但是它们的含义并不相同。以 ' 定义的字符串为原义字符串，其中的变量不会被转义，而 " 定义的字符串会将变量值进行替换。

>  foo=bar
>
>  echo "$foo"
> 
>  打印 bar
> 
>  echo '$foo'
> 
>  打印 $foo

自己实操的时候没有正确理解这段话
在执行 `echo "mkdir -p "$1""` 时一直奇怪为什么输出只有 `mkdir -p`
实际上正确的写法应该是`echo 'mkdir -p "$1"'`(~~日常铸币~~)

___

这章还讲到了 &&（与操作符） 和 ||（或操作符）  两种运算符，我具体的实操是这样的

```bash
sakuraauro@DemoJustLuGuo:~/TEST$ true || echo 123
sakuraauro@DemoJustLuGuo:~/TEST$ echo $?
0                        ##true返回0，即执行前一个命令成功
sakuraauro@DemoJustLuGuo:~/TEST$ false || echo 123
123                      ##false返回1，即执行前一个命令失败，将执行后一个命令
sakuraauro@DemoJustLuGuo:~/TEST$ true && echo 123
123                      ##true返回0即执行成功，将执行后一个命令
sakuraauro@DemoJustLuGuo:~/TEST$ false && echo 123
sakuraauro@DemoJustLuGuo:~/TEST$ echo $?
1                        ##false返回1即执行失败，不会执行后一个命令
```

___

还讲到了三种通配符，个人实操了一遍感觉确实有助于提升效率。这里就先把它列出来

>1.当你想要利用通配符进行匹配时，你可以分别使用 ? 和 * 来匹配一个或任意个字符。例如，对于文件 foo, foo1, foo2, foo10 和 bar, rm foo? 这条命令会删除 foo1 和 foo2 ，而 rm foo* 则会删除除了 bar 之外的所有文件。
>
>2.花括号 {} - 当你有一系列的指令，其中包含一段公共子串时，可以用花括号来自动展开这些命令。这在批量移动或转换文件时非常方便。

下面是我的示例

```bash
sakuraauro@DemoJustLuGuo:~/TEST$ touch test{1..9}.txt ##创建名为test1到test9的txt文件
sakuraauro@DemoJustLuGuo:~/TEST$ ls
change.sh    hi.txt     test2.txt  test5.txt  test8.txt
document.sh  more       test3.txt  test6.txt  test9.txt
hello.txt    test1.txt  test4.txt  test7.txt
sakuraauro@DemoJustLuGuo:~/TEST$ rm test?.txt  ##删除所有带test(x).txt的文件（好像只在10以内有效？）
sakuraauro@DemoJustLuGuo:~/TEST$ ls
change.sh  document.sh  hello.txt  hi.txt  more
```

以下是另一个示例
```bash
sakuraauro@DemoJustLuGuo:~/TEST$ touch test{1..11}.txt  ##创建名为test1到test11的txt文件
sakuraauro@DemoJustLuGuo:~/TEST$ ls
change.sh    hi.txt     test10.txt  test3.txt  test6.txt  test9.txt
document.sh  more       test11.txt  test4.txt  test7.txt
hello.txt    test1.txt  test2.txt   test5.txt  test8.txt
sakuraauro@DemoJustLuGuo:~/TEST$ rm test?.txt  ##删除所有带test(x).txt的文件
sakuraauro@DemoJustLuGuo:~/TEST$ ls
change.sh    hello.txt  more        test11.txt
document.sh  hi.txt     test10.txt  ##这里test10.txt和test11.txt并没有被删除
sakuraauro@DemoJustLuGuo:~/TEST$ rm test??.txt
sakuraauro@DemoJustLuGuo:~/TEST$ ls
change.sh  document.sh  hello.txt  hi.txt  more  ##把?换成??就可以删除掉了
```
另外，使用`rm test*.txt`命令应该会更方便，不过看使用场景吧。

### 01.12

#### 学习时长：1小时

先补上上一节的作业
```bash

#!/bin/bash

 export new_workspace=""

 marco(){
         new_workspace=$(pwd)
 }

 polo(){
         cd "$new_workspace"
 }
 
 下面是终端输出
 
 sakuraauro@DemoJustLuGuo:~/afterwork$ marco marco.sh
sakuraauro@DemoJustLuGuo:~/afterwork$ cd
sakuraauro@DemoJustLuGuo:~$ polo
sakuraauro@DemoJustLuGuo:~/afterwork$
```

```bash
#!/usr/bin/env bash  

 standard_out="standard_out.txt"
 standard_error="standard_error.txt"
 success_count=0
 while true;do
          n=$(( RANDOM % 100 ))

 if [[ n -eq 42 ]]; then
    echo "Something went wrong" >> "$standard_out"
    >&2 echo "The error was using magic numbers" >> "$standard_error"
    exit 1
 fi

 echo "Everything went according to plan" >> "$standard_out"
 if [ $? -ne 0 ]; then  
        echo "脚本在失败前共运行了 $success_count 次"
        break
   fi
    ((success_count++))
done

cat "$standard_out"
cat "$standard_error"
```

学习了vim编辑器的使用
基本上 vim 共分为这几种模式：
1.正常模式：在文件中四处移动光标进行修改
2.插入模式：插入文本
3.替换模式：替换文本
4.可视化模式（一般，行，块）：选中文本块
5.命令模式：用于执行命令

下面是一些从讲义上摘抄下来的内容，上手这个还是需要点时间的，抄下来方便自己查看

>你可以按下 <ESC>（退出键）从任何其他模式返回正常模式。在正常模式，键入 i 进入插入 模式，R 进入替换模式，v 进入可视（一般）模式，V 进入可视（行）模式，<C-v> （Ctrl-V, 有时也写作 ^V）进入可视（块）模式，: 进入命令模式。

___

>在正常模式下键入 : 进入命令行模式。 在键入 : 后，你的光标会立即跳到屏幕下方的命令行。 这个模式有很多功能，包括打开，保存，关闭文件，以及 退出 Vim。
>
>:q 退出（关闭窗口）
>
>:w 保存（写）
>
>:wq 保存然后退出
>
>:e {文件名} 打开要编辑的文件
>
>:ls 显示打开的缓存
>
>:help {标题} 打开帮助文档

___

>基本移动: hjkl （左， 下， 上， 右）     **卧槽这个左下上右太抽象了，哪怕左上下右也行啊**
>
>行： 0 （行初）， ^ （第一个非空格字符）， $ （行尾）
>
>翻页： Ctrl-u （上翻）， Ctrl-d （下翻）
>
>i 进入插入模式
>
>但是对于操纵/编辑文本，不单想用退格键完成
>
>比如 d{移动命令} 再 i
>
>x 删除字符（等同于 dl）
>
>s 替换字符（等同于 xi） 
>
>更多值得学习的: 比如 ~ 改变字符的大小写

___

### 01.13

#### 学习时长：1小时

本节课讲的内容是使用ssh获取远程服务器的日志文件，通过搜索、过滤来找到并整理需要的数据
说实话这一节讲的内容有点密了，这里就先整理出自己认为有用的

sed编辑器

主要是运用s（替换命令）。s 命令的语法如下：s/REGEX/SUBSTITUTION/, 其中 REGEX 部分是我们需要使用的正则表达式，而 SUBSTITUTION 是用于替换匹配结果的文本。

正则表达式

>. 除换行符之外的 “任意单个字符”
>
>* 匹配前面字符零次或多次
>
>+ 匹配前面字符一次或多次
>
>[abc] 匹配 a, b 和 c 中的任意一个
>
>(RX1|RX2) 任何能够匹配 RX1 或 RX2 的结果
>
>^ 行首
>
>$ 行尾

sed 的正则表达式有些时候是比较奇怪的，它需要你在这些模式前添加 \ 才能使其具有特殊含义。或者，您也可以添加 -E 选项来支持这些匹配。~~（你怎么知道我刚刚实操就被坑了）~~

感觉就这些需要重点记一下（其实是后面用方便直接打开看，就不用一个个点网页看语法使用示例了），其他的看了但是总感觉云里雾里的，说实话还是更喜欢把自己的实操记录的输出复制上来，可以更直观的看到我写了什么，为什么这么写。

~~（还有感觉这正则表达式不像是人发明出来的）~~

### 01.14

##### 学习时长：1小时

shell在执行一些命令时会出现响应慢的情况
使用`ctrl+c`可以停止命令的执行，它的本质是给进程发送了一个信号以改变其执行。
结束进程的信号还包括`SIGINT`(CTRL+C) `SIGQUIT`(CTRL+\) `SIGTERM`(kill -TERM <PID>)

不仅如此，信号机制中还有`SIGSTOP`(CTRL+Z)以暂停进程的信号，我们可以使用 fg 或 bg 命令恢复暂停的工作。它们分别表示在前台继续或在后台继续。

终端多路复用常用的复用器是`tmux`,使用tmux可以同时运行多个任务，或者一边运行编辑器一边运行程序。tmux常用的快捷键都是以`CTRL+B`起手，`X`结束的，这里就先列举几个自己感觉常用的吧

- mux 开始新会话
- tmux new -s NAME 以指定名称开始一个新会话
- tmux ls 列出当前所有会话
- 在 tmux 中输入 <C-b> d ，将当前会话分离
- c 创建一个新窗口，使用 <C-d> 关闭
- <C-b> N 跳转到第 N 个窗口

别名：
一些常用的命令可以使用别名来代替输入，感觉跟之前讲到的 脚本差不多，不同的是脚本声明一个函数，然后通过`source`命令加载，别名是通过`alias`命令定义的，而且应该一次只能定义一个长命令
在默认情况下 shell 并不会保存别名。为了让别名持续生效，需要将配置放进shell的启动文件里，像是 .bashrc 或 .zshrc

感觉这节主要还是以演示居多吧，所以就先写到这里。今天主要就是给wsl装了个可视化界面  ~~（虽然我觉得并不好看）~~  总结就是摸了。

### 01.15

#### 学习时长：90分钟

今天为了试一下ssh的使用，给家里不用的老电脑也安装了wsl（别问我为什么也安装wsl，问就是没那么多空间）

安装了wsl后，在初次启动时并没有弹出设置用户的提示，而是直接以root权限进入了
这里需要创建自己的用户名
通过`adduser`命令设置，这时会让你输入密码，之后就一堆巴拉巴拉的没用的个人信息，我全跳过了
然后使用`vim`命令编辑`/etc/sudoers`,在打开的配置文件中，找到root ALL=(ALL:ALL) ALL 在下面添加刚设的用户名加上ALL=(ALL:ALL)ALL 就可以
还可以通过`cat /etc/passwd |grep 用户名` 来验证自己的配置是否被正确保存了

接下来就是使用ssh命令了，使用`ssh ip地址`后弹出

>ssh: connect to host 192.168.1.5 port 22: Connection refused

这是由于wsl并没有内置`openssh-server`，就需要执行`sudo app-get install openssh-server`以安装

安装之后我们再执行ssh命令，我们会惊奇的发现：

>connect to host 192.168.1.5 port 22: Connection refused
>
>哈哈，还是不行
>

别急，因为ssh服务妹有启动，这时我们执行` /etc/init.d/ssh start`之后就可以了

注意的是一定要`ssh 该系统上存在的用户名@ip地址 `才可以，为什么这么说呢，你猜是谁直接输ip地址最后输密码输到怀疑人生。

哦对，还有个公钥登录的方法，简单来说就是使用`ssh-keygen`命令生成一个公钥，再用`ssh-copy-id 用户名@ip地址`发送到目标主机后。之后再用ssh登录就不用输入密码了。

搞完这一套步骤，不出意外你就可以享受ssh带来的便利了。

这里贴一点自己的操作

```bash
sakuraauro@DemoJustLuGuo:~$ ssh 192.168.1.5
ssh: connect to host 192.168.1.5 port 22: Connection refused #这里是刚开始尝试
sakuraauro@DemoJustLuGuo:~$ sudo apt-get install openssh-server
（省略掉输出）
sakuraauro@DemoJustLuGuo:~$ /etc/init.d/ssh start
Starting ssh (via systemctl): ssh.serviceFailed to start ssh.service: Interactive authentication required.
See system logs and 'systemctl status ssh.service' for details.
 failed!    #这里的意思好像是执行失败了，我没懂，所以我接下来准备看一下ssh服务的状态
sakuraauro@DemoJustLuGuo:~$ systemctl status ssh.service
○ ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/usr/lib/systemd/system/ssh.service; disabled; preset: enabled)
     Active: inactive (dead)      #ssh服务被加载了，但是并不在活跃状态？我试试看能不能跑
TriggeredBy: ● ssh.socket
       Docs: man:sshd(8)
             man:sshd_config(5)  
```
---
```bash             
sakuraauro@DemoJustLuGuo:~$ ssh 192.168.1.5
The authenticity of host '192.168.1.5 (192.168.1.5)' can't be established.
ED25519 key fingerprint is SHA256:(省略掉).
sakuraauro@192.168.1.5's password:
Permission denied, please try again.
sakuraauro@192.168.1.5's password:
Permission denied, please try again.
sakuraauro@192.168.1.5's password:
sakuraauro@192.168.1.5: Permission denied (publickey,password). #这里输了好几次密码但是没有成功，我有点自我怀疑了。
```
---
```bash
sakuraauro@DemoJustLuGuo:~$ ssh shimarin@192.168.1.5
shimarin@192.168.1.5's password:
Welcome to Ubuntu 24.04.1 LTS (GNU/Linux 4.4.0-19041-Microsoft x86_64)
（下面是一些状态信息，直接省略掉）
shimarin@WINPC-xxxxxxxx:~$     #前缀变成了另一台电脑的用户名及名字，ssh连接成功了，下面用logout断开连接
shimarin@WINPC-906291016:~$ logout
Connection to 192.168.1.5 closed.
```

### 01.16

#### 学习时长：1小时

学习了git的使用

简单来说，在git中文件被称作 Blob 对象（数据对象），也就是一组数据。目录则被称之为“树”，它将名字与 Blob 对象或树对象进行映射，快照则是被追踪的最顶层的树。
一个树看起来可能是这样的：

```
<root> (tree)  #这是一个快照
|
+- foo (tree)
|  |
|  + bar.txt (blob, contents = "hello world")  #名为foo的树包含了一个文件（对象）bar.txt
|
+- baz.txt (blob, contents = "git is wonderful")  #这个文件是直接指向快照的
```

git中的提交是不可改变的。但这并不代表错误不能被修改，只不过这种“修改”实际上是创建了一个全新的提交记录。而引用则被更新为指向这些新的提交。

git还包括一个暂存区，在编辑快照时，改动会存在此区中，允许指定下次快照中要包括哪些改动。

git的命令行：（只列了一些自己应该会常用的）
- git init: 创建一个新的 git 仓库，其数据会存放在一个名为 .git 的目录下
- git status: 显示当前的仓库状态
- git add <filename>: 添加文件到暂存区
- git commit: 创建一个新的提交
- git diff <filename>: 显示与暂存区文件的差异
- git checkout <revision>: 更新 HEAD 和目前的分支
- git branch: 显示分支
- git merge <revision>: 合并到当前分支
- git mergetool: 使用工具来处理合并冲突
- git remote add <name> <url>: 添加一个远端
- git push <remote> <local branch>:<remote branch>: 将对象传送至远端并更新远端引用
- git fetch: 从远端获取对象/索引
- git pull: 相当于 git fetch; git merge
- git clone: 从远端下载仓库
- git checkout -- <file>: 丢弃修改
- git commit --amend: 编辑提交的内容或信息
- git reset HEAD <file>: 恢复暂存的文件

本节课主要注重于理解git的设计以让我们更好地使用它，在上这节课之前我就已经开始使用了，所以听起来并不感觉有什么不理解的地方。将这节课的内容放到共学项目上的报名步骤就很好理解了，首先要报名的人fork主仓库，将报名信息合并到主仓库，等待报名成功后每天将学习日志直接提交到主仓库，这里每日的提交就相当于创建了一个新快照。当然以防万一你也可以先提交到自己分支的仓库，确保OK后再合并到主仓库。

今天就先看到这里，主要是感觉重理解的课程确实没啥好写的。 ~~（开始看我的爆炸梦之颂乐人偶）~~

### 01.18

#### 学习时长：1小时

昨天看了一点网上的教程尝试在局域网搭一个网站，但是折腾了两个小时失败了，就没有写笔记。

今天就继续看调试与性能分析这节的内容，讲的是如何处理代码中的bug和优化代码，前面调试代码改变输出结果的颜色就不多写了，把代码引用过来就行了，试了一下还挺好玩的。

>echo -e "\e[38;2;255;0;0mThis is red\e[0m"  #打印红色的字符串:this is red
>
>控制色彩的字符名为ANSI颜色控制码，这个就不多说了，贴个维基的介绍：https://zh.wikipedia.org/wiki/ANSI%E8%BD%AC%E4%B9%89%E5%BA%8F%E5%88%97

还有个是大部分linux的系统日志都会使用`systemd`，这是一个系统守护进程，systemd会将日志存放在/var/log/journal，可以使用`journalctl`命令显示这些信息。之前在讲ssh的时候就用过这个代码，因为系统日志有些长就可以通过`grep`命令将我们需要的信息过滤出来。还有些其他的工具类似于`lnav`也可以很好的展现和浏览日志。

虽然说大部分人在代码遇到问题时都会在发现问题的地方添加打印语句，但是在运行一些大型代码时就会显得难以下手，这时可以使用调试器，课上使用的示例语言是`python`(pdb)，这里是我的实操记录。


```bash
#wsl并没有预装python，这里我们先安装
sakuraauro@DemoJustLuGuo:~$ python
Command 'python' not found, did you mean:
  command 'python3' from deb python3
  command 'python' from deb python-is-python3
sakuraauro@DemoJustLuGuo:~$ sudo apt install python3 #如果忘了python的安装命令又不想百度或者用apt命令查，可以试着打与其相关的命令，linux会提醒你的（笑）
sakuraauro@DemoJustLuGuo:~$ python
Command 'python' not found, did you mean:
  command 'python3' from deb python3
  command 'python' from deb python-is-python3 #安装了之后还是这样，是因为安装的python3插件的命令是python3
  sakuraauro@DemoJustLuGuo:~$ sudo apt install python-is-python3
  sakuraauro@DemoJustLuGuo:~$ python
Python 3.12.3 (main, Nov  6 2024, 18:32:19) [GCC 13.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information. #把另外一个叫python-is-python3的插件也装上了，既然能显示出来版本信息了就应该没问题了
```

---
写在之后：要使用pdb请安装python-dev-is-python3
---

```bash
#这里直接复制了讲义上的python代码，先执行一遍。
sakuraauro@DemoJustLuGuo:~/TEST$ vim debug.py
sakuraauro@DemoJustLuGuo:~/TEST$ python debug.py
Traceback (most recent call last):
  File "/home/sakuraauro/TEST/debug.py", line 11, in <module>
    print(bubble_sort([4, 2, 1, 8, 7, 6]))
          ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/home/sakuraauro/TEST/debug.py", line 6, in bubble_sort
    if arr[j] > arr[j+1]:
                ~~~^^^^^
IndexError: list index out of range   #这里输出的错误出现在6和11行，有个IndexError（索引列表越界）错误，我们使用pdb来修复此代码
sakuraauro@DemoJustLuGuo:~/TEST$ pdb debug.py
(省略中间的输出)

IndexError: list index out of range
Uncaught exception. Entering post mortem debugging
Running 'cont' or 'step' will restart the program
> /home/sakuraauro/TEST/debug.py(6)bubble_sort()
-> if arr[j] > arr[j+1]:  #这里直接执行pdb(c)命令，当程序运行到第6行时便崩溃了
(Pdb) p arr
[2, 1, 1, 7, 6, 6]
(Pdb) p j
5                     #在程序终止运行的地方打印数组的结果，arr中有2,1,1,7,6,6六个数，j的值是5，代入表达式就是 arr[5] > arr[6] 这里的arr[6]表示数组第七个数，所以这里出现了越界错误
sakuraauro@DemoJustLuGuo:~/TEST$ vim debug.py
sakuraauro@DemoJustLuGuo:~/TEST$ python debug.py
[1, 1, 1, 6, 6, 6]    #我们将第五行的range(n)改为range(n-1)后再运行代码就能够输出结果了，此时第六行的执行结果应该是 arr[4] > arr [5] 符合要求。
```

这章内容有点多，课虽然看完了但是实操还没做完，分两天做吧

### 01.19
#### 学习时间：45分钟

关于web的开发者工具，这在以后应该是要经常要用的东西，在浏览器中按F12即可打开，火狐的开发者工具应该和chrome有点差别，其他的大概没什么特别的了，毕竟大部分浏览器的内核用的都是chromium嘛。

接下来是静态分析的内容，依旧引用的是讲义的内容，py的静态分析工具`pyflakes`依旧需要使用apt命令安装，这个就不多说了。
```bash
sakuraauro@DemoJustLuGuo:~/TEST$ python debug.py
0
1
2
3
4
Traceback (most recent call last):
  File "/home/sakuraauro/TEST/debug.py", line 12, in <module>
    print(baz)
          ^^^
NameError: name 'baz' is not defined. Did you mean: 'bar'?
```
我们先直接执行一遍这个代码，错误输出为第12行，但是当我们修改过后，输出仍为0,1,2,3,4,0,2。前面的数并没有按照预期输出42。这里就直接使用pyflakes进行操作。

>sakuraauro@DemoJustLuGuo:~/TEST$ pyflakes3 debug.py
>
>debug.py:7:5: redefinition of unused 'foo' from line 4

下面的性能分析与优化内容，我觉得比较有趣的是利用分析器来显示各函数调用所需的时间，还有利用`Valgrind`这个工具检测内存泄漏问题（沟槽的内存泄漏）。其他的话，我觉得还是得自己实战写代码，在真正着手进行优化的时候才能真正学到。

还有资源监控的内容，就过了一遍，但是我在执行`free`命令时发现一些奇怪的东西
```bash
sakuraauro@DemoJustLuGuo:~/TEST$ free -m
               total        used        free      shared  buff/cache   available
Mem:            7550         911        5846           3        1043        6638
Swap:           2048           0        2048
```
wsl的内存是与windows共享的吗？既然是共享，那么7550这个总内存是从哪里获得的数据呢，这里空闲内存也与任务管理器的对不上，下面swap压缩内存倒是之前折腾手机的时候在scene上没少见过，不过鉴于我在各个方面都了解一点但都是半罐水的特性，我也分析不出个所以然。

今天疑似交的有点过晚了，下次一定先学习再打电动（心虚）

### 01.20
#### 学习时间：45分钟

这个元编程看的有点晕晕的，就不写太多了。但是在跟着做构建系统的实操时出现了一些小问题。具体表现为python缺失`matplotlib`这个运行库，而且使用pip命令安装后报错。
```bash
sakuraauro@DemoJustLuGuo:~/TEST/makeTEST$ pip install matplotlib
error: externally-managed-environment

× This environment is externally managed
╰─> To install Python packages system-wide, try apt install
    python3-xyz, where xyz is the package you are trying to
    install.

    If you wish to install a non-Debian-packaged Python package,
    create a virtual environment using python3 -m venv path/to/venv.
    Then use path/to/venv/bin/python and path/to/venv/bin/pip. Make
    sure you have python3-full installed.

    If you wish to install a non-Debian packaged Python application,
    it may be easiest to use pipx install xyz, which will manage a
    virtual environment for you. Make sure you have pipx installed.

    See /usr/share/doc/python3.12/README.venv for more information.    #错误类型为‘外部管理环境错误’，没懂这是什么意思，根据报错给的建议安装了几个包也没用，直接丢gpt试试了
   
```
把报错丢给gpt分析了一下，gpt的说法是`这个错误是因为您的操作系统配置了 PEP 668，限制在全局范围内通过 pip 安装 Python 包。这种机制是为了保护系统的 Python 环境，避免非系统软件对系统核心环境产生影响。`
根据gpt的解决方法，这里选择创建一个虚拟环境，使用`python3 -m venv myenv`创建一个名为myenv的虚拟环境
输入`source myenv/bin/activate`以激活虚拟环境，最后再pip install就可以了。

今天好像有点摸，但是给家里的路由器刷了openwrt，有了这几天折腾linux的基础，玩这个确实更得心应手了。准备等返校了继续研究一下校园网，去年校园网验证加强了之后机制就很奇怪，装了魔改过的openwrt就会被检测到，但是装一个干净的固件或者是padavan就不会检测到，而且在校园网设备页面显示的是电脑的mac。也不像是UA2F的问题，感觉应该是哪个软件包的锅，回校再看看怎么解决。

最后模仿amberheart做一个结束告别（玩尬的）
```bash
sakuraauro@DemoJustLuGuo:~/TEST$ jp2a nina1.png
kkkx;,,,,'..     dddddo,       ,;;;;,;;;;;;;;;;;;;;;;;;;;;;;;;;;.     .,.         .;:::
kkkd;,,.         ;ddddddo,      .;;,,,,,,;;;;;;;;;;;;;;;;;;;;;;.     .oddc.         .;;
Okkd,.            .;odddddo,      ',,,,,;,;;;:;:::;;;;;;::;;;;.     .lddo;,,'..       ,
Okko,     .::::'     ,odddddl.     ..',,,;;;;;;c:::::::::c:;,,'    .,,,:;,,,,oddc     ,
kkko,     ldddddo;.    'lddddd,    .',,,,;;::,;:kcc:;;:;;;,,,,,'  ;:,,,,,,,,cddo.     ,
kkkl,     .;dddddddc.    ......   .',,,,;;c0:::xXc;,,,,,,,,,,,,;.ldddlc;,,,,,;;      .,
kkko:;.      ;ddddddo   ........ .',,,,;:ckkcclXNl;;,,;,,,,,,,,,,;coddddoc;,,.      .''
kkkdol:.      .,llllc  .ddddddd:';'''',xkXNN0kONNk:;;;d,,,,,'',,,,,,;:lddddo.      ..''
kkkl:,                 .odoooool:;,;x;dKOkxOXXXNNXOxdOOc,,''''',,;,,,,,,:co.      ....'
0kxdo,    .ccccddll.           .c,,dd;KX0XXKKNNNNNNXXNNXc,''''',,dol:;,,,'      .......
K0OOk;    .ddddKXdd.           .;,';:cXXXXNNNNNNNNNKkdONXx,'''''..;lddoo'      ........
ollll,    .,,,,OX;'.    cool;;;l,:'''cKNNNNNNNNNNNNNNXkkNx,,''''    .'OK.     .........
llllol.        ON,     ;KNNKdddoll;'''dNNNXoldkOXNNNNXXXO:x0,''lo,   .Xk     ..........
kxxxxxkl'....:x0Xdo:.cOXXNNKdddl;;;''',dXN0xkkdlONNNNNXk:kOl'''NMMNk:cXc      .........
NNNNNNNNNNWWXKNKXOXKXKWWWWWKdddl,,,'''oldKNK000KNNNX0d:,;;'',,dMMWNNXKXo:      ........
WWWWWWWWWWWXXKXXNXNXXXNWWWWXddd:'.',;;cddx0KKKKX0kl;'''......'oKNKKX0XXKXO     ........
WWWWWWWWNWWKXKKKKKKKKKXWWWWKdccc::loooodd0XXXXXKkddc,''',;...   dXXNXNXXX0,    ........
WWWWWWWWWWWokKKKKKKKKKokXWXd;,,,;cccoolkXXXKKKKKOd:cclldc::'...;0KKKXKKXKKc   ........d
WWWWWWWWWWWdckKKKKKKK0:;;:,,,,'',,,,;cONWW0o;kNNNKoc;,::,,,',,;;0KKKKKKKKO.  .........d
WWWWWWWWWWWXc:oxkkkxdc,,,,,',,,,,,,,,;KN0o,.''o0XX:,,',,,,,,,,,;d0KKKKKKk;............d
WWWWWWWWWWWWx;,,,,,,,,,,,,'''',',,,;ldO:....x...:Oo:,'',,,,,,,,,,;:loddl,.............d
WWWWWWWWWWWWWo;,,,,,,,''''''''''',,,c0Oc;..;X'..,ddc;''''',,,,,,,,,,,,,,..............d
WWWWWWWWWWWWWWO,,,,,'''',,''''''',,;oXNNx..oO'.dNNo;,''''''',,',',,,,,''.............'d
WWWWWWWWWWWWWWWx;,,,,,,,,,''''''',,;oNNK'.'OO,.;X0;,'''''''',,,,,,'',,'..............'d
0000KKKKKKKKXXXXOo:,,,,''''''''',,,;xx',,.',,'..'....,''''''',,,,,,,,,'..............,d
ooooddddddddddxxxxdoc:;,''''''''',,;kx,::.,;;,;:;....''''''''',,,,,:co;..............'d
,,,,,,,,,,,,,,,;;;;;;cl;''''''..o:o:xNNXXXXXKXXXK:;;o'..'''''''':odddo;...............'
;;;::::;;;;;;::clodl;ox:.'''''''',lcoNWNNNKxXNNNk:l,''.'''''''',odddoo;................
...............'''''..'...........'.';;;;;;;;;;;'''.............''''''.................
```
~~中专乐队女孩井芹仁菜向你说晚安~~

### 01.21
#### 学习时间：1小时

又是在阴间的时间提交commit，我已经很努力调整作息了果咩纳塞

今天看的是安全和密码学这一课，但是感觉这节有点晦涩了，只是了解一下。
平常设置密码的话，edge/chrome倒是有个生成密码的功能，平常注册一些奇奇怪怪的网站会用这个。
密码管理器倒是也有用过，之前小小体验了一下朋友部署的bitwarden，感觉确实挺不错的，但是没有坚持用下去。

感觉这个加密挺有意思的。关于加密，我记得初中在贴吧找资源的时候，楼主会用`base64`这种编码来加密网址防止伸手党和被和谐。不过这种方式不需要key，很难称得上安全。这里介绍了对称加密与非对称加密，两者的区别应该是是否区分公钥/私钥。
感觉讲义讲的不是很清楚，这里就找了点自己摘抄的

>对称加密算法
>特性：
1、加密、解密使用同一个密钥，效率高
2、将原始数据分割成固定大小的块，逐个进行加密
缺陷：
1、 密钥过多
2、密钥分发
3、数据来源无法确认
>


> 非对称加密算法
公钥加密： 密钥是成对出现
公钥：公开给所有人； public key
私钥：自己留存，必须保证其私密性； secret key (private)
特点：用公钥加密数据，只能使用与之配对的私钥解密；反之亦然
功能：
数字签名：主要在于让接收方确认发送方身份
对称密钥交换：发送方用对方的公钥加密一个对称密钥后发送给对方
数据加密：适合加密较小数据
缺点：密钥长， 加密解密效率低下
>
```bash
#这里使用gpg对称加密方法来试了一下
sakuraauro@DemoJustLuGuo:~$ gpg --gen-key
（跳过中间的输出）
Real name: shimarin
Email address: shimarin3915@gmail.com
You selected this USER-ID:
    "shimarin <shimarin3915@gmail.com>"
    Change (N)ame, (E)mail, or (O)kay/(Q)uit? o
We need to generate a lot of random bytes. It is a good idea to perform
some other action (type on the keyboard, move the mouse, utilize the
disks) during the prime generation; this gives the random number
generator a better chance to gain enough entropy.
gpg: /home/sakuraauro/.gnupg/trustdb.gpg: trustdb created
gpg: directory '/home/sakuraauro/.gnupg/openpgp-revocs.d' created
gpg: revocation certificate stored as '/home/sakuraauro/.gnupg/openpgp-revocs.d/xxxxxxxxxxxxxxxxxxxxx.rev'
public and secret key created and signed.

pub   ed25519 2025-01-21 [SC] [expires: 2028-01-21]
      xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
uid                      shimarin <shimarin3915@gmail.com>
sub   cv25519 2025-01-21 [E] [expires: 2028-01-21]
#这里密钥就创建好了
```
---
```bash
sakuraauro@DemoJustLuGuo:~$ touch hoshimachi.txt
sakuraauro@DemoJustLuGuo:~$ vim hoshimachi.txt
彗星のごとく現れたスターの原石！アイドルVtuberの星街すいせいでーす！ すいちゃんは——今日もかわいい！  #这个是txt里面的内容
sakuraauro@DemoJustLuGuo:~$ gpg --output hoshimachi.gpg --encrypt --recipient shimarin3915@gmail.com hoshimachi.txt
sakuraauro@DemoJustLuGuo:~$ scp -r hoshimachi.gpg shimarin@192.168.1.5:/home/shimarin
#这里把这个文件用ssh发送到我的老电脑上
sakuraauro@DemoJustLuGuo:~$ gpg --export -o new.key xxxxxxxxxxxxxxxxxxxxxxxxx
#这里通过--list-keys显示的密钥，将该密钥导出为一个叫new.key的文件，接下来用自己喜欢的方式将这个文件发送到老电脑，使用--import导入就可以解密上面的gpg文件了。
```
ssh好玩捏，下次还玩🥰🥰🥰
<!-- Content_END -->