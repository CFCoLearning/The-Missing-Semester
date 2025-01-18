# CFC Studio 共学 Epoch1 指引
---
# [AmberHeart]

## 笔记证明

<!-- Content_START -->

### 01.11

#### 今日学习时间:40min
#### 学习内容小结:Windows和Linux的差异,很大


Let's study Shell!


先前有在Windows尝试用过PowerShell，大概是Shell的一种分支?


终端→显示Shell的窗口


拓展联想：cmd属于shell的一种吗?查找后：√


your platform plus like 'terminal' 发现已有打开后是类似powershell的界面?


该查找cmd,powerShell,terminal三者间的区别了


区别大概是：

①PowerShell以系统性管理任务进程为主,而Windows terminal则属于终端模拟器应用程序？

②PowerShell侧重于管理,Windows terminal则以开发,模拟环境为主？

test

①尝试使用echo输出带有空格的字符串

②尝试使用‘+’

③执行echo 283 + pro 输出如下

>283

>+

>pro

思考:echo的执行是将变量自前向后依次输出？

查找后发现用法近似感觉像是Python中的print,也可以执行程序


执行echo $path无输出

>查找后发现windows系统应执行echo $ENv:path

>输出成功


执行which echo报错

>which为linux命令

>查找后发现Windows类似命令Get-command

>输出成功


执行cd /home报错

>估计是绝对路径下linux与windows文件夹不同产生的差异问题,不打算进一步查询


执行cd -报错

>linux与windows的差异问题 老实用绝对路径回去了


执行ls -l报错

>老套的差异问题 查到-LiteralPath似乎有近似作用但是需要参数


执行ls 出现以下内容

>d-----      ...

>d-----      ...

>d-r---      ...

>dar---      ...

>d-r---      ...

>dar--l      ...

不同于linux的前缀 查找后发现下列关系

d 目录

r 可读

w 可写

a 全体用户

吧大概

l什么意思没查到就是了


总结:大部分时间和精力花在了解决Linux与Windows的系统差异上,等安装wsl整好bash后提速应该就会很快了,总之摸鱼摸爽了

总结:摸了

### 01.12

#### 今日学习时间：90min
#### 学习内容小结：感觉还行
#### 问题：作业中最后一part里：记事本中无内容的原因是什么（大致代码如下）
```bash
SHHis@AmberHeart:/tmp# cat ./missing/semester.txt | grep -i last-modified | cut --delimiter=":" -f2 >> ./last-modified.txt
SHHis@AmberHeart:/tmp# cat last-modified.txt
```

#### 以下是今天的学习内容

配置了wsl,大概能够试着以Linux的环境进行后续学习了

先试着找了找路径在哪

>root@AmberHeart:~# cd ..
>root@AmberHeart:/# ls
>bin   dev  home  lib    lib64   lost+found  mnt  proc  run   snap  sys  usr
>boot  etc  init  lib32  libx32  media       opt  root  sbin  srv   tmp  var

大概是知道了,但是上课神游好奇@前面的root能不能改名

查了下要用gedit,装了下改了下好了<br><br>

然后顺带学了一点markdown的语法,接下来试着用自己喜欢的格式做笔记<br><br>

```bash
SHHis@AmberHeart:~# cd -
-bash: cd: OLDPWD not set
SHHis@AmberHeart:~# echo hello
hello
SHHis@AmberHeart:~# echo nichika > SHHis.txt
SHHis@AmberHeart:~# cat SHHis.txt
nichika
SHHis@AmberHeart:~# cat < SHHis.txr
-bash: SHHis.txr: No such file or directory
SHHis@AmberHeart:~# cat < SHHis.txt
nichika
SHHis@AmberHeart:~# cat < SHHis.txt > CoMETIK.txt
```
所以执行的方式类似于从左到右的顺序?

```bash
SHHis@AmberHeart:~# ls -l
total 20
drwxr-xr-x 2 root root 4096 Jan 13 00:38 283
drwxr-xr-x 2 root root 4096 Jan 13 00:41 283pro
-rw-r--r-- 1 root root    8 Jan 13 01:00 CoMETIK.txt
-rw-r--r-- 1 root root   16 Jan 13 01:02 SHHis.txt
drwx------ 4 root root 4096 Jan 13 00:50 snap
SHHis@AmberHeart:~# ls -l /
total 2272
lrwxrwxrwx   1 root root       7 May 31  2023 bin -> usr/bin
drwxr-xr-x   2 root root    4096 May 31  2023 boot
drwxr-xr-x  16 root root    3540 Jan 13 00:50 dev
drwxr-xr-x  99 root root    4096 Jan 13 00:53 etc
drwxr-xr-x   2 root root    4096 Apr 15  2020 home
-rwxrwxrwx   1 root root 2260248 Nov 10 00:26 init
lrwxrwxrwx   1 root root       7 May 31  2023 lib -> usr/lib
lrwxrwxrwx   1 root root       9 May 31  2023 lib32 -> usr/lib32
lrwxrwxrwx   1 root root       9 May 31  2023 lib64 -> usr/lib64
lrwxrwxrwx   1 root root      10 May 31  2023 libx32 -> usr/libx32
drwx------   2 root root   16384 Jan 13 00:31 lost+found
drwxr-xr-x   2 root root    4096 May 31  2023 media
drwxr-xr-x   6 root root    4096 Jan 13 00:31 mnt
drwxr-xr-x   2 root root    4096 May 31  2023 opt
dr-xr-xr-x 301 root root       0 Jan 13 00:32 proc
drwx------   7 root root    4096 Jan 13 01:00 root
drwxr-xr-x  24 root root     740 Jan 13 00:49 run
lrwxrwxrwx   1 root root       8 May 31  2023 sbin -> usr/sbin
drwxr-xr-x  11 root root    4096 Jan 13 00:50 snap
drwxr-xr-x   2 root root    4096 May 31  2023 srv
dr-xr-xr-x  11 root root       0 Jan 13 00:30 sys
drwxrwxrwt  11 root root    4096 Jan 13 00:50 tmp
drwxr-xr-x  14 root root    4096 May 31  2023 usr
drwxr-xr-x  13 root root    4096 May 31  2023 var
SHHis@AmberHeart:~# tail -nl
tail: invalid number of lines: ‘l’
SHHis@AmberHeart:~# ls -l / | tail -n1
drwxr-xr-x  13 root root    4096 May 31  2023 var
SHHis@AmberHeart:~# ls -l / | tail -n3 > robot.txt
SHHis@AmberHeart:~# cat robot.txt
drwxrwxrwt  11 root root    4096 Jan 13 00:50 tmp
drwxr-xr-x  14 root root    4096 May 31  2023 usr
drwxr-xr-x  13 root root    4096 May 31  2023 var
SHHis@AmberHeart:~# curl --head --silent google.com
```
然后他死了,大概是google.com需要梯子的问题<br><br>

于是试了试别的网址

```bash
SHHis@AmberHeart:~# curl --head --silent baidu.com
HTTP/1.1 200 OK
Date: Sun, 12 Jan 2025 17:07:04 GMT
Server: Apache
Last-Modified: Tue, 12 Jan 2010 13:48:00 GMT
ETag: "51-47cf7e6ee8400"
Accept-Ranges: bytes
Content-Length: 81
Cache-Control: max-age=86400
Expires: Mon, 13 Jan 2025 17:07:04 GMT
Connection: Keep-Alive
Content-Type: text/html

SHHis@AmberHeart:~# curl --head --silent baidu.com | grep -i content-length
Content-Length: 81
SHHis@AmberHeart:~# curl --head --silent baidu.com | grep -i content-length | cut --delimiter=' ' -f2
81
SHHis@AmberHeart:~# curl --head --silent shinycolors.enza.fun
HTTP/1.1 301 Moved Permanently
Server: CloudFront
Date: Sun, 12 Jan 2025 17:09:31 GMT
Content-Type: text/html
Content-Length: 167
Connection: keep-alive
Location: https://shinycolors.enza.fun/
X-Cache: Redirect from cloudfront
Via: 1.1 b20771afac2acd15ec58304838134668.cloudfront.net (CloudFront)
X-Amz-Cf-Pop: NRT20-P1
X-Amz-Cf-Id: Sp7n_KUHHKK2OoGNN7PAfqQBdrW3h4AU63h1-X8huxG_vX9wbmWDLw==

SHHis@AmberHeart:~# curl --head --silent shinycolors.enza.fun | grep -i content-length | cut --delimiter=' ' -f2
167
SHHis@AmberHeart:~# curl --head --silent granbluefantasy.com
SHHis@AmberHeart:~# curl --head --silent granbluefantasy.jp
HTTP/1.1 301 Moved Permanently
Server: CloudFront
Date: Sun, 12 Jan 2025 17:10:46 GMT
Content-Type: text/html
Content-Length: 167
Connection: keep-alive
Location: https://granbluefantasy.jp/
X-Cache: Redirect from cloudfront
Via: 1.1 ded1ee0f770839d2b2fb7225385749c6.cloudfront.net (CloudFront)
X-Amz-Cf-Pop: TPE50-C1
X-Amz-Cf-Id: aerUs3oVKRI4OInPIJE328GCEyg9NrLn0cal_H5OfiXfTheWf5fcyQ==

SHHis@AmberHeart:~# curl --head --silent granbluefantasy.jp | grep -i content-length | cut --delimiter=' ' -f2
167
```
接下来是内核相关的内容,因为是虚拟机所以没什么多少可尝试的
```bash
SHHis@AmberHeart:~# cd /sys
SHHis@AmberHeart:/sys# ls
block  bus  class  dev  devices  firmware  fs  kernel  module
SHHis@AmberHeart:/sys# ls
block  bus  class  dev  devices  firmware  fs  kernel  module
SHHis@AmberHeart:/sys# cd class/
SHHis@AmberHeart:/sys/class# ls
bdi    cuse     hidraw  ipvtap   misc  pci_bus       ppp  rtc          scsi_generic  tty  vfio
block  devlink  input   macvtap  nd    phy           pps  scsi_device  scsi_host     uio  virtio-ports
bsg    drm      iommu   mem      net   power_supply  ptp  scsi_disk    thermal       vc   vtconsole
SHHis@AmberHeart:/sys/class# cd backlight/
-bash: cd: backlight/: No such file or directory
SHHis@AmberHeart:/sys/class# cd -
/sys
SHHis@AmberHeart:/sys# cd --
```

然后尝试了用xdg-open打开先前的文件

```bash
SHHis@AmberHeart:~# xdg-open SHHis.txt

Command 'xdg-open' not found, but can be installed with:

apt install xdg-utils
```

看起来是没有安装xdg-utils的原因?尝试了安装

```bash
SHHis@AmberHeart:~# apt install xdg-utils
...
...
E: Failed to fetch http://security.ubuntu.com/ubuntu/pool/main/g/gcc-9/gcc-9-base_9.4.0-1ubuntu1~20.04.1_amd64.deb  404  Not Found [IP: 91.189.91.83 80]
E: Failed to fetch http://security.ubuntu.com/ubuntu/pool/main/g/gcc-9/cpp-9_9.4.0-1ubuntu1~20.04.1_amd64.deb  404  Not Found [IP: 91.189.91.83 80]
E: Unable to fetch some archives, maybe run apt-get update or try with --fix-missing?
```

报错了,似乎是没有更新apt-get?尝试了更新

```bash
SHHis@AmberHeart:~# apt-get update
...
...
Reading package lists... Done
```

大概是成功了的样子,再尝试安装了一下xdg-utils,这次成功了

```bash
...
...
Processing triggers for libc-bin (2.31-0ubuntu9.9) ...
/sbin/ldconfig.real: /usr/lib/wsl/lib/libcuda.so.1 is not a symbolic link

```

然后就是回归到用xdg-open打开SHHis.txt了

>SHHis@AmberHeart:~# xdg-open SHHis.txt
打开后出现类似这样的画面
```bash
nichika
nichika
~
~
~
~
~
~
"SHHis.txt" 2L,16C                  1,1     All
```
大概是成功打开记事本了<br><br>

研究了一下发现左下角可以实行命令，右下角是光标所在点<br><br>

发现可以在这里更改记事本内容试着更改了然后百度了如何退出<br><br>

试着输入:q!退出后发现并没有保存修改的内容,大概是因为强制退出<br><br>

以下是作业：<br><br>

```bash
SHHis@AmberHeart:~# ls
283  283pro  CoMETIK.txt  SHHis.txt  man  robot.txt  snap
SHHis@AmberHeart:~# echo $SHELL
/bin/bash
SHHis@AmberHeart:~# cd /tmp
SHHis@AmberHeart:/tmp# mkdir missing
SHHis@AmberHeart:/tmp# man touch
SHHis@AmberHeart:/tmp# touch missing/semester.txt
SHHis@AmberHeart:/tmp# echo "#!/bin/sh" >> missing/semester.txt
-bash: !/bin/sh: event not found
SHHis@AmberHeart:/tmp# echo '#!/bin/sh' >> missing/semester.txt
SHHis@AmberHeart:/tmp# echo 'curl --head --silent https://missing.csail.mit.edu' >> missing/semester.txt
SHHis@AmberHeart:/tmp# cat missing/semester.txt
#!/bin/sh
curl --head --silent https://missing.csail.mit.edu
SHHis@AmberHeart:/tmp# ./missing
-bash: ./missing: Is a directory
SHHis@AmberHeart:/tmp# ./missing/semester
-bash: ./missing/semester: No such file or directory
SHHis@AmberHeart:/tmp# ./missing/semester.txt
-bash: ./missing/semester.txt: Permission denied
SHHis@AmberHeart:/tmp# man chmod
SHHis@AmberHeart:/tmp# man chmod
SHHis@AmberHeart:/tmp# chmod u+x missing/semester.txt
SHHis@AmberHeart:/tmp# ./missing/semester.txt
HTTP/2 200
server: GitHub.com
content-type: text/html; charset=utf-8
last-modified: Sat, 21 Dec 2024 16:53:01 GMT
access-control-allow-origin: *
etag: "6766f26d-205d"
expires: Sun, 12 Jan 2025 18:11:45 GMT
cache-control: max-age=600
x-proxy-cache: MISS
x-github-request-id: 8DBD:17396:383F968:3992BFC:67840386
accept-ranges: bytes
age: 0
date: Sun, 12 Jan 2025 18:01:45 GMT
via: 1.1 varnish
x-served-by: cache-lax-kwhp1940061-LAX
x-cache: MISS
x-cache-hits: 0
x-timer: S1736704906.531356,VS0,VE97
vary: Accept-Encoding
x-fastly-request-id: 19e7286566136e29ca3c507c6b7e7059b6057aa9
content-length: 8285
SHHis@AmberHeart:/tmp# cat missing/semester.txt | grep -i last-modified | cut --delimiter=':' -f2 >> ./last-modified.txt
SHHis@AmberHeart:/tmp# cat last-modified.txt

SHHis@AmberHeart:/tmp# chmod u+x missing/semester.txt
SHHis@AmberHeart:/tmp# cat missing/semester.txt | grep -i last-modified | cut --delimiter=":" -f2 >> ./last-modified.txt
SHHis@AmberHeart:/tmp# cat last-modified.txt

SHHis@AmberHeart:/tmp# cat .missing/semester.txt | grep -i last-modified | cut --delimiter=':' -f2 >> ./last-modified.txt
cat: .missing/semester.txt: No such file or directory
SHHis@AmberHeart:/tmp# cat ./missing/semester.txt | grep -i last-modified | cut --delimiter=":" -f2 >> ./last-modified.txt
SHHis@AmberHeart:/tmp# cat last-modified.txt

(一直输出空白不知道是什么问题,试着找了找权限和别的问题)
SHHis@AmberHeart:/tmp# ls -l
total 24
-rw-r--r-- 1 root root    2 Jan 13 02:16 last-modified.txt
drwxr-xr-x 2 root root 4096 Jan 13 01:50 missing
-rw-r--r-- 1 root root    0 Jan 13 01:46 semester
-rw-r--r-- 1 root root    0 Jan 13 01:48 semester.txt
drwx------ 4 root root 4096 Jan 13 00:50 snap-private-tmp
drwx------ 3 root root 4096 Jan 13 00:32 systemd-private-1082091ed04b42e6adc2d449ff635cf9-ModemManager.service-q97nSi
drwx------ 3 root root 4096 Jan 13 00:32 systemd-private-1082091ed04b42e6adc2d449ff635cf9-systemd-logind.service-KUc6Vi
drwx------ 3 root root 4096 Jan 13 00:32 systemd-private-1082091ed04b42e6adc2d449ff635cf9-systemd-resolved.service-EO3Tai
SHHis@AmberHeart:/tmp# ls -l ./missing/semester.txt
-rwxr--r-- 1 root root 61 Jan 13 01:54 ./missing/semester.txt
SHHis@AmberHeart:/tmp# file ./missing/semester.txt
./missing/semester.txt: POSIX shell script, ASCII text executable
(还是失败,放弃了)
SHHis@AmberHeart:/tmp# echo ' Sat,21 Dec 2024 16:53:01 GMT' > last-modified.txt
SHHis@AmberHeart:/tmp# cat last-modified.txt
 Sat,21 Dec 2024 16:53:01 GMT
SHHis@AmberHeart:/tmp# echo '今天就学习到这，下次再见捏'
今天就学习到这，下次再见捏。
```

### 01.13
#### 今日学习时长:45分钟
#### 学习总结：相关变量参数、格式以及试了试vim

Bash字符串中''不被转义，“”会被转义字符所替换 例如$<br><br>

执行过程中的空格有其致命性,使用时需注意<br><br>

```bash
foo=bar
#可以正常执行
foo = bar
#直接报错
```
接下来是一些可以用于脚本执行中的参数<br><br>
```bash
$0脚本名 $1-$9对应的第几个参数

$#参数数量 $@所有参数 $?参数正确性返回值

!!上一个参数 类似于方向键↑大概 可以用sudo !!来获得权限执行上一个命令

$_ 可以用于提取脚本中最后一个参数 $$脚本的执行进程识别码
```

此外命令可以配合||和&&使用 相当于or和and<br><br>

true返回码固定为0 false为1<br><br>

感觉在实操过程中熟悉一下就ok了<br><br>

```bash
SHHis@AmberHeart:~# false || echo "BangDream!"
BangDream!
SHHis@AmberHeart:~# true && echo '!! means BangDream!'
!! means BangDream!
```
此外尝试试着用vim看看够不够熟练
```bash
SHHis@AmberHeart:~# vim BangDream.sh
BangDream(){
        mkdir -p "$1"
        cd "$1"
        false || echo "$1" >> BangDream.txt
        true && echo "$1 is a part of BangDream" >> BangDream.txt
}
SHHis@AmberHeart:~# BangDream mikoto
BangDream: command not found
SHHis@AmberHeart:~# source BangDream.sh
SHHis@AmberHeart:~# BangDream mikoto
SHHis@AmberHeart:~/mikoto# cat BangDream.txt
mikoto
mikoto is a part of BangDream
```
稍微研究了一下,看起来是成功了<br><br>

今天事情有点多比较赶,就学到这吧
```bash
SHHis@AmberHeart:~/mikoto# echo "$(true&&cat BangDream.txt | grep -i mikoto | cut -d' ' -f1)向各位说下次见"
mikoto
mikoto向各位说下次见
```

### 01.15
#### 今日学习时长：120min
#### 总结：学的不多 基本在实操
```bash
SHHis@AmberHeart:~# touch SHHis{1,5}.txt
SHHis@AmberHeart:~# echo $(ls)
283 283pro BangDream.sh CoMETIK.txt SHHis.txt SHHis1.txt SHHis5.txt man mcd.sh mikoto robot.txt snap test
```
这里的话似乎是因为没有装zsh导致结果输出并不是SHHis1-SHHis5的感觉<br><br>

后面尝试了另一种方式发现可行

```bash
SHHis@AmberHeart:~# touch shinycolors{1..9}.txt
SHHis@AmberHeart:~# echo $(ls)
283 283pro BangDream.sh CoMETIK.txt SHHis.txt man mcd.sh mikoto robot.txt script.py shinycolors1.txt shinycolors2.txt shinycolors3.txt shinycolors4.txt shinycolors5.txt shinycolors6.txt shinycolors7.txt shinycolors8.txt shinycolors9.txt snap test
SHHis@AmberHeart:~# rm shinycolors*
SHHis@AmberHeart:~# ls
283  283pro  BangDream.sh  CoMETIK.txt  SHHis.txt  man  mcd.sh  mikoto  robot.txt  script.py  snap  test
```

用于批量操作下的命令优化<br><br>

由于是wsl,不方便在外部环境中寻找python,有关python脚本的这段仅作记录<br><br>

脚本开头第一行的shebang用于解释脚本选择的命令解释器,<br>
shebang行课使用env命令来利用环境变量中的程序解析脚本,利用的是PATH环境变量定位<br>
例如：
>#!/usr/bin/env python
<br>

这个叫fzf的用于文件检索挺好用的<br><br>

还有这个tree的可视化很清晰<br><br>

以下是本节的作业:<br><br>

```bash
#不知道排序哪里出了问题不能自动排序，于是加了一个sort手动排序，此外丢失了颜色
SHHis@AmberHeart:~# ls -a -h -l -u --color=auto | sort -k 6,8
total 84K
-rw-r--r--  1 root root  161 Jan 15 13:36 .profile
-rw-r--r--  1 root root 3.1K Jan 15 13:36 .bashrc
drwxr-xr-x 19 root root 4.0K Jan 15 13:39 ..
drwx------  2 root root 4.0K Jan 15 13:47 .cache
drwx------  3 root root 4.0K Jan 15 13:47 .config
drwx------  4 root root 4.0K Jan 15 13:47 snap
drwxr-xr-x  2 root root 4.0K Jan 15 13:47 283
drwxr-xr-x  2 root root 4.0K Jan 15 13:47 283pro
drwxr-xr-x  2 root root 4.0K Jan 15 13:47 mikoto
drwxr-xr-x  2 root root 4.0K Jan 15 13:47 test
drwx------  9 root root 4.0K Jan 15 13:58 .
-rw-------  1 root root 7.1K Jan 15 14:29 .viminfo
-rw-r--r--  1 root root    0 Jan 15 14:29 .motd_shown
-rw-r--r--  1 root root    0 Jan 15 14:29 man
-rw-r--r--  1 root root    1 Jan 15 14:29 script.py
-rw-r--r--  1 root root    8 Jan 15 14:29 CoMETIK.txt
-rw-r--r--  1 root root   16 Jan 15 14:29 SHHis.txt
-rw-r--r--  1 root root   33 Jan 15 14:29 mcd.sh
-rw-r--r--  1 root root  142 Jan 15 14:29 BangDream.sh
-rw-r--r--  1 root root  150 Jan 15 14:29 robot.txt
-rw-------  1 root root 5.2K Jan 15 14:36 .bash_history

#变量叫wrun是因为电音教父的where are you now
SHHis@AmberHeart:~# vim marco.sh
marco(){
        export wrun=$(pwd) || exit
        echo "save as = $wrun"
}
polo(){
        cd $(wrun) || exit
        echo "tp success"
}
SHHis@AmberHeart:~# source marco.sh
SHHis@AmberHeart:~# cd ..
SHHis@AmberHeart:/# marco
save as = /
SHHis@AmberHeart:/# cd -
/root
SHHis@AmberHeart:~# polo
tp success
SHHis@AmberHeart:/#

#反复试了挺久 感觉还有点问题
SHHis@AmberHeart:~# vim mytest.sh
#!/usr/bin/env bash

n = $(( RANDOM % 100 ))

if [[ n -eq 42 ]]; then
        echo "Something went wrong"
        >&2 echo "The error was using magic numbers"
        exit 1
fi


echo "Everything went according to plan"

SHHis@AmberHeart:~# vim finaltest.sh

#!/usr/bin/env bash

jishu=0
shuchubz="shuchubz.txt"
shuchucw="shuchucw.txt"
>$shuchubz
>$shuchucw

while true;do
        ((jishu = jishu + 1))
        chmod +x mytest.sh
        ./mytest.sh >> $shuchubz 2>>$shuchucw
        if [ $? -ne 0 ]; then
                echo "error at $jishu"
                break
        fi
done
cat $shuchubz
cat $shuchucw

SHHis@AmberHeart:~# source finaltest.sh
error at 90
Everything went according to plan
...
...
Everything went according to plan
Something went wrong
The error was using magic numbers
#大概是path中没zip命令相关的原因，总之失败了
SHHis@AmberHeart:~# find . -type f -name "*.txt" | xargs zip yasuo.zip
xargs: zip: No such file or directory

SHHis@AmberHeart:~# vim pailie.sh
pailie(){
        n=$(ls -a -h -l -u | sort -k 6,8) || exit
        echo "$n"
}

SHHis@AmberHeart:~# source pailie.sh
SHHis@AmberHeart:~# pailie
total 124K
-rw-r--r--  1 root root  161 Jan 15 13:36 .profile
-rw-r--r--  1 root root 3.1K Jan 15 13:36 .bashrc
drwxr-xr-x 19 root root 4.0K Jan 15 13:39 ..
drwx------  2 root root 4.0K Jan 15 13:47 .cache
drwx------  3 root root 4.0K Jan 15 13:47 .config
drwx------  4 root root 4.0K Jan 15 13:47 snap
drwxr-xr-x  2 root root 4.0K Jan 15 13:47 283
drwxr-xr-x  2 root root 4.0K Jan 15 13:47 283pro
drwxr-xr-x  2 root root 4.0K Jan 15 13:47 mikoto
drwxr-xr-x  2 root root 4.0K Jan 15 13:47 test
-rw-r--r--  1 root root    0 Jan 15 14:29 .motd_shown
-rw-r--r--  1 root root    0 Jan 15 14:29 man
-rw-r--r--  1 root root    1 Jan 15 14:29 script.py
-rw-r--r--  1 root root    8 Jan 15 14:29 CoMETIK.txt
-rw-r--r--  1 root root   16 Jan 15 14:29 SHHis.txt
-rw-r--r--  1 root root   33 Jan 15 14:29 mcd.sh
-rw-r--r--  1 root root  142 Jan 15 14:29 BangDream.sh
-rw-r--r--  1 root root  150 Jan 15 14:29 robot.txt
-rw-r--r--  1 root root   96 Jan 15 15:13 marco
-rw-r--r--  1 root root  110 Jan 15 15:17 marco.sh
-rw-------  1 root root 5.2K Jan 15 15:40 .bash_history
-rw-r--r--  1 root root   34 Jan 15 15:40 shuchucw.log
-rw-r--r--  1 root root 2.5K Jan 15 15:40 shuchubz.log
-rw-r--r--  1 root root   34 Jan 15 15:41 shuchucw.txt
-rw-r--r--  1 root root 3.0K Jan 15 15:41 shuchubz.txt
-rwxr-xr-x  1 root root  199 Jan 15 15:41 mytest.sh
-rw-r--r--  1 root root  289 Jan 15 15:42 finaltest.sh
-rw-------  1 root root 8.8K Jan 15 15:56 .viminfo
-rw-r--r--  1 root root   69 Jan 15 15:56 pailie.sh
drwx------  9 root root 4.0K Jan 15 15:56 .
```
差不多就学到这了 主要是vim吧大概<br><br>

```bash
SHHis@AmberHeart:~# vim baibai.sh
baibai(){
        n=$1
        echo "今天就学到这里，$n向各位告辞，各位下次再见捏~"
}
SHHis@AmberHeart:~# source baibai.sh
SHHis@AmberHeart:~# baibai 七草日花
今天就学到这里，七草日花向各位告辞，各位下次再见捏~
```

### 01.16
#### 今日学习时长：70min
#### 总结：vim修饰语数字之类的组合使用挺方便
normal[正常] 
[I]→  [ESC]← insert[插入]
[R]→  [ESC]← replace[替换]
[V]→  [ESC]← visual[可视化]
[shift]+[V]→ [ESC]← line[可视行]
[ctrl]+[V]→  [ESC]← block[可视块]
[:]→  [ESC]← command-line[命令行]


vim 命令间可做到加法<br><br>

命令之间的组合还挺方便的 例如ci[之类的<br><br>

主要是以vim编辑器操作内容为主的课程 后面实操可能感触更大<br><br>

在这就简单记录一下快捷键操作<br><br>

```bash
基本移动: hjkl （左， 下， 上， 右）
词： w （下一个词）， b （词初）， e （词尾）
行： 0 （行初）， ^ （第一个非空格字符）， $ （行尾）
屏幕： H （屏幕首行）， M （屏幕中间）， L （屏幕底部）
翻页： Ctrl-u （上翻）， Ctrl-d （下翻）
文件： gg （文件头）， G （文件尾）
行数： :{行数}<CR> 或者 {行数}G ({行数}为行数)
杂项： % （找到配对，比如括号或者 /* */ 之类的注释对）
查找： f{字符}， t{字符}， F{字符}， T{字符}
查找/到 向前/向后 在本行的{字符}
, / ; 用于导航匹配
搜索: /{正则表达式}, n / N 用于导航匹配
-------------------
i 进入插入模式
但是对于操纵/编辑文本，不单想用退格键完成
O / o 在之上/之下插入行
d{移动命令} 删除 {移动命令}
例如，dw 删除词, d$ 删除到行尾, d0 删除到行头。
c{移动命令} 改变 {移动命令}
例如，cw 改变词
比如 d{移动命令} 再 i
x 删除字符（等同于 dl）
s 替换字符（等同于 xi）
可视化模式 + 操作
选中文字, d 删除 或者 c 改变
u 撤销, <C-r> 重做
y 复制 / “yank” （其他一些命令比如 d 也会复制）
p 粘贴
更多值得学习的: 比如 ~ 改变字符的大小写
-----------------
ci( 改变当前括号内的内容
ci[ 改变当前方括号内的内容
da' 删除一个单引号字符串， 包括周围的单引号
```
大致试了实操,组合在使用的时候真的很方便<br><br>

vimtutor也挺有意思的,看了会试着实操了一下<br><br>

```bash
SHHis@AmberHeart:~# source baibai.sh
SHHis@AmberHeart:~# baibai 疯狂星期四阿贝母鸡卡
今天就学到这里，疯狂星期四阿贝母鸡卡向各位告辞，各位下次再见捏~
```

### 01.17
#### 学习时长：70min
远程执行服务器 ssh<br><br>

有关于sed的正则表达式<br><br>

捕获组,指定特殊值并重复使用<br><br>

sort | uniq -c 去除排序后重复行 并计数 感觉挺有用<br><br>

学了不少,不如先找个日志练手，诶,刚好脸上就有个杀戮尖塔的运行日志<br><br>

不过好像看不到具体哪个mod引起的闪退,就用sed的正则表达式让他可视化一下<br><br>

来看看哪个基础mod在杀戮尖塔运行过程中是大头<br><br>
```bash
SHHis@AmberHeart:~# cat SlayTheSpire.log
...#省略上万条
12:19:10.470 INFO helpers.FileSaver> Save thread will die now.
12:19:10.470 INFO core.CardCrawlGame> Shutting down publisher integrations...
12:19:10.473 INFO steam.SteamTicker> [ERROR] SteamAPI stopped running.
12:19:10.476 INFO core.CardCrawlGame> Flushing logs to disk. Clean shutdown successful.

SHHis@AmberHeart:~# cat SlayTheSpire.log | sed -E 's/.*(INFO | DEBUG )(.*)>.*/\2/'
#先提取一下具体出现的基础mod
...
spireTogether.SpireTogetherMod
spireTogether.SpireTogetherMod
spireTogether.SpireTogetherMod
core.CardCrawlGame
core.CardCrawlGame
core.CardCrawlGame
core.CardCrawlGame
helpers.FileSaver
helpers.FileSaver
core.CardCrawlGame
steam.SteamTicker
core.CardCrawlGame
#大致是提取出来了 虽然有不少乱七八糟的就当没看见吧（
SHHis@AmberHeart:~# cat SlayTheSpire.log | sed -E 's/.*(INFO | DEBUG )(.*)>.*/\2/' | sort | uniq -c
#进行一个序的排
...
      2 steamInput.SteamInputDetect
      1 steamInput.SteamInputHelper
      1 ststwitch.TwitchConfig
     23 togawasakikomod
    476 unlock.UnlockTracker
SHHis@AmberHeart:~# cat SlayTheSpire.log | sed -E 's/.*(INFO | DEBUG )(.*)>.*/\2/' | sort | uniq -c | sort -nk1,1 | tail -n10
#然后把里面最大头的提取一下
    163 helpers.TipHelper����
    242 helpers.TipHelper��ҫ
    304 dungeons.AbstractDungeon
    312 ActLikeIt
    336 helpers.AsyncSaver
    442 helpers.FileSaver
    476 unlock.UnlockTracker
    880 helpers.File
   3454 basemod.BaseMod
   4027 spireTogether.SpireTogetherMod
```


### 01.18
#### 今日学习时长：30min

sleep 有点意思<br><br>

SIGQUIT 退出 这是SIG+单词组的组合？<br><br>

让程序在执行过程中暂停并继续 不过SIGINT似乎可以在执行过程中被检测<br><br>

部分信号如SIGKILL无法被检测 不过注意父子程序关系型可能会报错<br><br>

暂停与后台执行进程 命令+&的后缀让命令在后台运行 可以通过jobs查看目前执行任务<br><br>

nohup的忽略SIGHUP封装来运行程序<br><br>

```bash
SHHis@AmberHeart:~# sleep 300
^Z
[1]+  Stopped                 sleep 300
SHHis@AmberHeart:~# jobs
[1]+  Stopped                 sleep 300
SHHis@AmberHeart:~# bg %1
[1]+ sleep 300 &
SHHis@AmberHeart:~# jobs
[1]+  Running                 sleep 300 &
SHHis@AmberHeart:~# kill -STOP %1
SHHis@AmberHeart:~# jobs
[1]+  Stopped                 sleep 300
SHHis@AmberHeart:~# fg %1
sleep 300
^Z
[1]+  Stopped                 sleep 300
SHHis@AmberHeart:~# jobs
[1]+  Stopped                 sleep 300
SHHis@AmberHeart:~# kill -SIGHUP %1
SHHis@AmberHeart:~# jobs
[1]+  Hangup                  sleep 300
#大致随便试了下
```
```bash
SHHis@AmberHeart:~# source baibai.sh
SHHis@AmberHeart:~# baibai SORRYBUSYseeyounextday海外邮寄好贵啊
今天就学到这里，SORRYBUSYseeyounextday海外邮寄好贵啊向各位告辞，各位下次再见捏~
```

### 01.19
#### 今日学习时长：60min 基本在翻阅

tmux 一个终端多路复用器？相当于浏览器的多标签窗口？<br><br>

在实操过程中或许挺实用,用不断的nohup之类的切进程还挺麻烦的或许<br><br>

```bash
SHHis@AmberHeart:~# tmux
[exited]
SHHis@AmberHeart:~# tmux new -s cometik
[exited]
SHHis@AmberHeart:~# tmux ls
no server running on /tmp/tmux-0/default
SHHis@AmberHeart:~#
```

奇怪的是退出后看不到有运行的tmux 或许是文件夹问题？<br><br>

窗口的一些操作也执行不出来 不知道为什么<br><br>

总之tmux之类的大概是相当于可视化操作优化布局了<br><br>
```bash
SHHis@AmberHeart:~# alias bb="source baibai.sh | baibai SHHis"
SHHis@AmberHeart:~# bb
今天就学到这里，SHHis向各位告辞，各位下次再见捏
```
这个alias真的挺有用的 超实用派 包括后面修改配置文件<br><br>

服务器这块,之前尝试弄git终端的时似乎搞过一些有关ssh密钥的<br><br>

感觉这块还是有点糊,可以等以后实操熟悉熟悉<br><br>

粗忙几天 之后就闲下来了估计 我向画像发誓<br><br>
```bash
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@%@%@@@@@@@@@@@@@@@@@%%%@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@@@%%%%%%%%%%%%%%%%%%%%%%%%#*****#*****###*######*******#####******##%%%%%%%%%%%%%%%%%%%%%%%%%%%%@@@
@@%%%%%%%%%%%%%%%%%%%%%%%#****##**+**####***#########****####********###%%%%%%%%%%%%%%%%%%%%%%%%%%@@
@@%%%%%%%%%%%%%%%%%%%%%#****##**++*######***#############***##****#*****##%%%%%%%%%%%%%%%%%%%%%%%%@@
@@%%%%%%%%%%%%%%%%%%%##***###***+*#######***#####**#######***###***#******##%%%%%%%%%%%%%%%%%%%%%%@@
@@%%%%%%%%%%%%%%%%%#*****###*****#########**#####***#######***###*++##***#**#%%%%%%%%%%%%%%%%%%%%%@@
@@%%%%%%%%%%%%%%%%#****#*##*+***##########**######**########*+*####++*##**##*#%%%%%%%%%%%%%%%%%%%%@@
@@%%%%%%%%%%%%%%%#*#*****##**#############**####*#*+*#*###**#*++*###++*##***###%%%%%%%%%%%%%%%%%%%@@
@@%%%%%%%%%%%%%%####*#**##*+*#############*+*######*+*#*##**##*+*####++*##***###%%%%%%%%%%%%%%%%%%@@
@@%%%%%%%%%%%%%%#####***##++##*#####*#####*++###**#*++*####**##*+*###*=+*##*+*#*##%%%%%%%%%%%%%%%%@@
@@%%%%%%%%%%%%%######+*##*+*#**#########*#*+*###***#*++*####+*#*++*###+=+###*+*#**%%%%%%%%%%%%%%%%@@
@@%%%%%%%%%%%%#*####*+*##*+*#+*########**#*+#%###*+*#*=+*###*+*#*=+#*#*==*###*+*#*#%%%%%%%%%%%%%%%@@
@@%%%%%%%%%%%%**#*##++*##*+**+*########**#*+%@%###++*#*=+**##*+*#+=***#*=+*#**++##*#%%%%%%%%%%%%%%@@
@@%%%%%%%%%%%#*#**#*++###*+**=*#####*##+*#+*@@@%#**++*#*=+***#*+#*++**#*==+**#*+*#**%%%%%%%%%%%%%%@@
@@%%%%%%%%%%#**#**#*=+###*+*+=*####*##*+**+%@@@@@#*******=+++*#++#*=****+==****++*#*#%%%%%%%%%%%%%%@
@@%%%%%%%%%%#*##**#*=+###*+*+=####**##++*+#@@@@@@@%****+*+===+**++*++**#*==+****+*#**%%%%%%%%%%%%#%@
@%%%%%%%%%%%******#*=+*##*++=+###*+*#*+***@@@@@@@@@%*++**+++===+++++=+*#*+==****++##*#%%%%%%%%%%%#%@
@%#%%%%%%%%#******#*=+*##*+==+***+=*++***%@@@@@@@@@@@%#+****+++=+++===**#+==+****+*#**#%%%%%%%%%%#%@
@%#%#%%%%#%#********==*###+===**+=+*+*++#@@@@@@@@@@@@@@%#****+++++=====*#*===****+*#**##%%%###%###%@
@%#######%%#********==****+==**+=+++*++#@@@@@@@@@@@@@@@@@%#****++***++=+#*+==+***+*#*+*####%#%####%@
@%#%#######**#******==+***+==+==+++*++%@@@@@@@@@@@@@@@@#**+==+=---=*##+=*#+===++*++#*=+*#%########%@
@%#########**##*****===**#+====+++*++#@@@@@@@@@@@@@@@@%*=-::-=--:::-=+#**#*++=++**=***++*#########%@
@%#########**##*****===+*#*==++===-==+#%@@@@@@@@@@@@@@**#*++++====++-:=#**#**+=++*+**##+**########%@
@%#########**##*****==++*#*===::------=*%@@@@@@@@@@@@@@@@%%#*++**+*@#=*%%*#*+*+=+*++*###+**#######%@
@%#########**###****==++*#*-:-===++===+#%@@@@@@@@@@@@@@@@#**#%%##%%%*%@@%*##*##==*+=**##*+**######%@
@%#########**###***++=++*#*=*%#%#*++**+#@@@@@@@@@@@@@@@@@@%##%%%#%%%@@@@#%###**+=++=**###*+**#####%@
@%##########*###*+*++=*+*#**%@#+**#####%@@@@@@@@@@@@@@@@@@@@%%%%%%@@@@@@#%#*#*#*=++=+**####+**####%@
@%##########**###**+==***##**%@%##%%%#%@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@%###*##*===+=+**#####****##%@
@%##########**####*+===**###%%%%%%##%%@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@#%@@%*#*===+==***#####****#%@
@%###########*+###*+===+*#**@@@@@@@@@@@@@@@@@@@@%@@@@@@@@@@@@@@@@@@@@@%*#%#++*#+=====+**######****%@
@%############***#*+====+#**%@@@@@@@@@@@@@@@@@@@%%@@@@@@@@@@@@@@@@@@@@*===-==+*+======**#######***%@
@%##############***+====+#*+#@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@%=-======**======+**#######*+#@
@%################*+====+#*=+#@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@%+-=======+*=======+**#######*%@
@%################*++===*#*===*@@@@@@@@@@@@@@@@@@@@@@@@%@@@@@@@@@@@#==========+*+=======***#######%@
@%################*++===+#*====+%@@@@@@@@@@@@@%%@@@@@%%@@@@@@@@@@%*===========+*========+***######%@
@%###############**+====+#+======*%@@@@@@@@@@@@@@@@@@@@@@@@@@@@%*=-===========+*+========+***#####%@
@%###############*+++===+*+========+#%@@@@@@@@@@@@@@@@@@@@@@@%*=-===========++**==========+***####%@
@%###############*+**===+**===========+*#%@@@@@@@@@@@@@@@@@%##+=============+**+======+=====***###%@
@%##############*++##++++**==+========---=+*%%@@@@@@@@@@%#####*============+***=======+*+====***##%@
@%##############*+*#**++++*+==============-=*####%%%%%####%%#%*===========+*##*========+*+====+***%@
@%#############*++*#**++*****===============#%%#########%%%%%%#=----=====+*###+=========+**=++=+**%@
@%*############*+*##**+==*#***+=+======-===+#%%%%%%%%%%%%%%@@@%+=++======***##+==========+**+++==+#@
@%*############*+*##**+==+*##***+=====++***#%%%%%%%%%%%%@@@@@@@%#%@@#+==**+##*+============***+++=#@
@%*###########*++*#***+===+*##*+++**#@@###%@@@@@@@@@@@@@@@@@@@%@@@@@@@#+*+*##*+=============+***+=#@
@%*#**#*#*#****++###*********##***#@@@#%@@@@@@@@@@@@@@@@@@@@%%@@@@@@@@%**+*##*+===============+**+#@
@%*************+*#*++#%##@@#*#####+#@%%%%%%%@@@@@@@%%%%%%%%%@@@@@@@@@@#*##+##**##*++===========+**%@
@%*************++=-=%%*#@@@#**###@++#@@@@@@@@@@@@%%@@@@%%%@@@@@@@@@@@@#+#*+*#**+===++=============#@
@%**********#*=-::=%@##@@@#**+**##=*#@@@@@@@@@@@@@@@@%%%@@@@@@@@@@@@@@*=*#*+**+=:::::---==========#@
@@%#********+-:::-#@*+***+=+====++#%=----==========+#@@@@@@@@@@@@@@@%#+=+##+=+===-:::::::--=====+#@@
@@@@@%%%%%%%######@@%##########%@@@@#####*********#%@@@@@@@@@@@@@@@@%%%%##%#####%############%%%@@@@
```


<!-- Content_END -->