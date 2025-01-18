# CFC Studio 共学 Epoch1 指引
---
# [YamKH514]

> 一般路过，不必在意

## 笔记证明

<!-- Content_START --> 
### 01.06

Duration of study: 1h \
What did I learn today: The Shell

Try to use English handouts and study note.

` which ` Programe \
Using ` which ` to find out the address which argument you entered.

    ~/The-Missing-Semester$ which which
    /usr/bin/which

今天先到这儿，有几科重量级还要复习 ⊙﹏⊙∥

### 01.08

Duration of study: 1h \
What did I learn today: Using the Shell

A path on the shell is a delimited list of directories \
It separated by ` / ` on Linux or OS X and ` \ `on Windows. \
We can use ` pwd ` to get currented path, ` ls ` to list files and directories on currented path, ` cd ` to change currented working directory. \
Entering ` ls -l /home `, the shell will output:
```bash
ren@ren-VMware-Virtual-Platform:~/The-Missing-Semester$ ls -l /home
total 4
drwxr-x--- 27 ren ren 4096 Jan  8 23:13 ren
```
Using ` -l ` to get more infomation about each file or directory present.
The ` drwxr-x--- ` indicate what permissions the owner of the file (`ren`), the owning group (`ren`), and everyone else respectively have the given permission. \
- ` - ` indicates that the grpup or user does not have the given permission.
- ` w ` indicate ` modify `
- ` r ` indicate ` read `
- ` x ` indicate ` execute `. If you want to enter a directory, you need this permission.

Using `man` programe to get more information about a programe, like:
```bash
$ man ls
```

### 01.09

Duration of study: 1h \
What did I learn today: Using the Shell

Normally, a programe's input and output are both our terminal. We can use `< file` and `> file` to rewire the input and output streams of a program to a file. We can also use `>>` to append to a file.
```bash
ren@ren-VMware-Virtual-Platform:~$ echo hello > hello.txt
ren@ren-VMware-Virtual-Platform:~$ cat hello.txt 
hello
ren@ren-VMware-Virtual-Platform:~$ cat < hello.txt 
hello
ren@ren-VMware-Virtual-Platform:~$ echo world >> hello.txt 
ren@ren-VMware-Virtual-Platform:~$ cat hello.txt 
hello
world
```
The `|` operator lets us "chain" programe such that the output of one is the input of another.
```bash
ren@ren-VMware-Virtual-Platform:~$ ifconfig | grep 192
        inet 192.168.10.134  netmask 255.255.255.0  broadcast 192.168.10.255
```

Homework

```bash
ren@ren-VMware-Virtual-Platform:/tmp$ mkdir missing
ren@ren-VMware-Virtual-Platform:/tmp$ cd ./missing/
ren@ren-VMware-Virtual-Platform:/tmp/missing$ touch semester
ren@ren-VMware-Virtual-Platform:/tmp/missing$ chmod 777 semester
ren@ren-VMware-Virtual-Platform:/tmp/missing$ ./semester | grep last-modified > ~/last-modified.txt
ren@ren-VMware-Virtual-Platform:/tmp/missing$ cat ~/last-modified.txt
last-modified: Sat, 21 Dec 2024 16:53:01 GMT
```

### 01.10

Duration of study: 40min \
What did I learn today: Shell Scripting

Using `foo=bar` to access the value of the variable with `$foo`. Using `foo = bar` will not work, because it will be interpreted as calling the `foo` program with argumenrs `=` and `bar`. \
Using `'` and `"` to define strings, but they are not equivalent. Strings delimited with `'` will not substitute variable value whereas whereas `"` delimited strings will. \
`bash` supports control flow techniques including `if`, `case`, `while` and `for`. It also supports for defining function, like:
```bash
mcd () {
    mkdir -p "$1"
    cd "$1"
}
```
`Bash` uses a veriety of special variables to refer to arguments, error codes, and other relevant variables.
> `$0` - Name of the script
>
> `$1` to `$9` - Arguments to the script. `$1` is the first argument and so on.
>
> `$@` - All the arguments
>
> `$#` - Number of arguments
>
> `$?` - Return code of the previous command
>
> `$$` - Process identification number (PID) for the current script
>
> `!!` - Entire last command, including arguments. A common pattern is to execute a command only for it to fail due to missing permissions; you can quickly re-execute the command with sudo by doing `sudo !!`
>
> `$_` - Last argument from the last command. If you are in an interactive shell, you can also quickly get this value by typing `Esc` followed by `.` or `Alt+.`

### 01.11

Duration of study: 40min \
What did I learn today: Shell Scripting and Shell Tools

When we perform comparisons in bash, try to use double brackets `[[]]` in favor of simple brackets `[]`.It will reduce chances of making mistakes although it can't be portable to `sh`.

What is shell globbing（通配）?
> When launching scripts, you will often want to provide arguments that are similar. Bash has ways of making this easier, expanding expressions by carrying out filename expansion. These techniques are often referred to as shell globbing.
- Wildcards: Using `?` and `*` to match one or any amount of characters respectively.
- Curly braces`{}`: Whenever we have a common substring in a series of commands,wo can use `{}` for bash to expand this automatically.
```bash
mv *{.py,.sh} folder
# Will move all *.py and *.sh files
```

Using `man` command to  learn how to use commands, or using [TLDR pages](https://tldr.sh/) to check example use cases of a command quickly.

Using `find` to find where the file is. Its syntax can sometimes be tricky to remember, so we can use `fd` which is a simple, fast and user-frindly alternative to `find`.
```bash
# Find all directories named src
find . -name src -type d
# Find all python files that have a folder named test in their path
find . -path '*/test/*.py' -type f
# Find all files modified in the last day
find . -mtime -1
# Find all zip files with size in range 500k to 10M
find . -size +500k -size -10M -name '*.tar.gz'
# Delete all files with .tmp extension
find . -name '*.tmp' -exec rm {} \;
# Find all PNG files and convert them to JPG
find . -name '*.png' -exec convert {} {}.jpg \;
```

Using `grep`, `ack`, `ag` and `rg` to find code.

### 01.12

Duration of study: 30min \
What did I learn today: Vim Editors

Vim's modal editing
Vim has multiple operating modes:
- Normal: moving around a file and making edits
- Insert: inserting text
- Replace: replacing text
- Visual: selecting blocks of text
- Command-line: running a command

Pressing `<ESC>` to switch from any mode back to Normal. From Normal mode, you can:
- enter Insert mode with `i`
- enter Replace mode with `R`
- enter Visual mode with `v`
- enter Visual Line mode with `V`
- enter Visual Block mode with `^V`
- enter Command-line mode with `:`

**Command-line** \
When you enter `:` to change Command-line mode, you can type:
>- `:q` quit (close window)
>- `:w` save (“write”)
>- `:wq` save and quit
>- `:e` {name of file} open file for editing
>- `:ls` show open buffers
>- `:help {topic}` open help
>   - `:help :w` opens help for the :w command
>   - `:help w` opens help for the w movement

### 01.13

Duration of study: 30min \
What did I learn today: Vim Editors

**Movement**
> - 基本移动: `hjkl` （左， 下， 上， 右）
> - 词： `w` （下一个词）， `b` （词初）， `e` （词尾）
> - 行： `0` （行初）， `^` （第一个非空格字符）， `$` （行尾）
> - 屏幕： `H` （屏幕首行）， `M` （屏幕中间）， `L` （屏幕底部）
> - 翻页： `Ctrl-u` （上翻）， `Ctrl-d` （下翻）
> - 文件： `gg` （文件头）， `G` （文件尾）
> - 行数： `:{行数}<CR>` 或者 `{行数}G` ({行数}为行数)
> - 杂项： `%` （找到配对，比如括号或者 `/* */` 之类的注释对）
> - 查找： `f{字符}`， `t{字符}`， `F{字符}`， `T{字符}`
>   - 查找/到 向前/向后 在本行的{字符}
>   - `,` / `;` 用于导航匹配
> - 搜索: `/{正则表达式}`, `n` / `N` 用于导航匹配

**Slection** \
可视化模式：
> - 可视化：v
> - 可视化行： V
> - 可视化块：Ctrl+v

**Edits**
> - `i` 进入插入模式
>   - 但是对于操纵/编辑文本，不单想用退格键完成
> - `O` / `o` 在之上/之下插入行
> - `d{移动命令}` 删除 {移动命令}
>   - 例如，`dw` 删除词, `d$` 删除到行尾, `d0` 删除到行头。
> - `c{移动命令}` 改变 {移动命令}
>   - 例如，`cw` 改变词
>   - 比如 `d{移动命令}` 再 `i`
> - `x` 删除字符（等同于 `dl`）
> - `s` 替换字符（等同于 `xi`）
> - 可视化模式 + 操作
>   - 选中文字, `d` 删除 或者 `c` 改变
> - `u` 撤销, `<C-r>` 重做
> - `y` 复制 / “yank” （其他一些命令比如 `d` 也会复制）
> - `p` 粘贴

**Counts**
> - `3w` 向后移动三个词
> - `5j` 向下移动 5 行
> - `7dw` 删除 7 个词

简要记录了一下Vim的操作命令，初见上手是真的痛苦。后续的自定义Vim就留着以后慢慢研究吧。(´。＿。｀)

### 01.15

Duration of study: 1h \
What did I learn today: Data Wrangling

How to figure out who's trying to log my server?
```bash
ssh myserver journalctl | grep sshd
```
This command using a pipe to stream a remote file through `grep` on our local host.

We can do the filtering on the remote computer.
```bash
ssh myserver 'journalctl | grep sshd | grep "Disconnected from"' > ssh.log
```

And then, We further organize the data.
```bash
ssh myserver journalctl
 | grep sshd
 | grep "Disconnected from"
 | sed -E 's/.*Disconnected from (invalid |authenticating )?user (.*) [^ ]+ port [0-9]+( \[preauth\])?$/\2/'
 | sort | uniq -c
 | sort -nk1,1 | tail -n10
 | awk '{print $2}' | paste -sd,
```

**Regular expressions** \
Google how to use Regular expressions when you need to use it. And Using [regex debugger](https://regex101.com/) to debug.

**How to use `sed`** \
[sed | tldr InBrowser.App](https://tldr.inbrowser.app/pages.zh/linux/sed)

**How to use `sort`** \
[sort | tldr InBrowser.App](https://tldr.inbrowser.app/pages.zh/common/sort)

Using `paste` to combine lines(`-s`) by a given single-character delimiter(`-d`;`,` in this case).

`awk`, a programming language which is really good at processing text streams. \
But at the same time, `awk` is complex. Browsing [awk | tldr InBrowser.App](https://tldr.inbrowser.app/pages.zh/common/awk) to get more infomation.

### 01.16

Duration of study: 1h \
What did I learn today: Command-line Environment

**Job Control**
- Killing a process \
    When a process receives a signal (which is a UNIX communication mechanism) it stops its execution, deal with the signal and potentially changes the flow of execution based on the information that the signal. This signal are `software interrupts`. \
    When we type `^C`, our shell will deliver a `SIGINT` signal to the process.
    ```python
    #!/usr/bin/env python
    import signal, time

    def handler(signum, time):
        print("\nI got a SIGINT, but I am not stopping")

    signal.signal(signal.SIGINT, handler)
    i = 0
    while True:
        time.sleep(.1)
        print("\r{}".format(i), end="")
        i += 1
    ```
    We can find that we can't kill this program by using `^C`, but if we use `^\` we can successfully kill this program.
    ```bash
    ren@ren-VMware-Virtual-Platform:~$ python3 test.py 
    18^C
    I got a SIGINT, but I am not stopping
    22^C
    I got a SIGINT, but I am not stopping
    37^\Quit (core dumped)
    ```
    `^\` means `SIGQUIT`. \
   Both `SIGINT` and `SIGQUIT` are usually used to exit the process, but the `SIGTERM` is a more generic graceful signal for asking a process to exit. And we can use `kill -TERM <PID>` to send this signal.

- Pausing and backgrounding processes \
    Typing `^Z` will send `SIGSTOP` to pauses a process. We can then continue the paused job in the foreground or background using `fg` or `bg`, respectively. And we also can type `jobs` to list the unfinished jobs associated with the current terminal session.
    ```bash
    ren@ren-VMware-Virtual-Platform:~$ sleep 1000
    ^Z
    [1]+  Stopped                 sleep 1000
    ren@ren-VMware-Virtual-Platform:~$ jobs
    [1]+  Stopped                 sleep 1000
    ren@ren-VMware-Virtual-Platform:~$ sleep 1000 &
    [2] 6747
    ren@ren-VMware-Virtual-Platform:~$ jobs
    [1]+  Stopped                 sleep 1000
    [2]-  Running                 sleep 1000 &
    ren@ren-VMware-Virtual-Platform:~$ fg %1
    sleep 1000
    ^Z
    [1]+  Stopped                 sleep 1000
    ```

**Terminal Multiplexers**
> The most popular terminal multiplexer these days is tmux.

[A Quick and Easy Guide to tmux](https://hamvocke.com/blog/a-quick-and-easy-guide-to-tmux/)

### 01.17

Duration of study: 30min \
What did I learn today: Command-line Environment

**Aliases** \
Using `alias` command to config aliases, like:
```bash
alias ll="ls -lh"
```

**Copying files over SSH** \
- Using `ssh+tee` commands.
    ```bash
    cat localfile | ssh remote_server tee serverfile
    ```
- Using `scp` command to copy large amounts of files/directories.
    ```bash
    scp path/to/local_file remote_host:path/to/remote_file
    ```

### 01.18

Duration of study: 30min \
What did I learn today: Debugging and Profiling

**Debugging**

> “The most effective debugging tool is still careful thought, coupled with judiciously placed print statements” — Brian Kernighan, Unix for Beginners.

- Printing and Logging
- Using debuggers, like [cgdb](https://cgdb.github.io/)

**Profiling**

- Using Timing
- Using Profilers
    - CPU profilers
        Using `cProfile` in python
    - Memory leak analysis
        We can use Valgrind that help us identify memory leaks
    - Resource Monitoring: \
        **General Monitoring**: `htop` \
        **IO operations**: `iotop` \
        **Disk Usage**: `df` \
        **Memory Usage**: `free` \
        **Open Files**: `lsof` \
        **Network Connections and Config**: `ss` \
        **Network Usage**: `nethogs` and `iftop`

<!-- Content_END -->