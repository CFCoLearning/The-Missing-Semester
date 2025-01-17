# CFC Studio 共学 Epoch1 指引

---

# RisingGalaxy

> I, who am so lazy, am still learning, what about you?

## Note

<!-- Content_START -->

### 01.06

Learning time: _next day_ `00:00 - 01:00` | `1 hour`

---

**Summary:**

Simply finished the course overview and shell part of the study, in fact, most of the basic commands before, these days the exam is busy, so today is the end.

However, here is another command line instruction, from the open source project [**tldr** _(too long; don't read)_](https://github.com/tldr-pages/tldr), compared to man, I think this project is more suitable for understanding and learning commands.

> 还是不习惯英文，后续我还是采用中文记录吧。

---

**Practice**

由于使用的是 Linux 虚拟机，Q10 未完成，其它均已完成。

以下简单记录一些注意点：

- Q5: 如果是一行一行地写入，记得使用 `>>` 而不是 `>`
- Q9: `./semester | grep -i '^last-modified:' | cut -d ' ' -f 2- > ~/last-modified.txt`
  可以分为三部分，先将 `semester` 的输出通过管道传递给 `grep`，再将 `grep` 的输出通过管道传递给 `cut`，最后将 `cut` 的输出通过管道传递给 `>`，将结果写入文件。其中 `grep` 的 `-i` 选项表示忽略大小写，`cut` 的 `-d ' '` 选项表示使用空格作为分隔符，`-f 2-` 表示从第二个字段开始输出。

---

### 01.07

> Learning Time: About 8 to 9 hours
>
> > 大部分时间都去玩 `fzf` 和 `neovim` 的配置了 `=.=`

---

**About `fzf`**

以前一直都是愚蠢的通过方向键上下切换找历史命令，或者通过 history 查询。
这次学到了 `Ctrl-R`，对于大多数的 shell 来说都是可以使用的，按下后可以输入字串进行匹配，查找历史命令，可以通过方向键精确定位到需要查找的命令，反复敲击相当于翻页吧。

我的 Ubuntu 使用 `sudo apt-get install fzf` 安装的并不是最新的，无法使用 `--bash`、`--zsh`、`--fish` 等选项，这些选项尽在 fzf 0.48.0 或更高版本中可用。

我使用的 shell 是 fish，将下行添加到 shell 配置文件中，可以设置 shell 集成

```bash
fzf --fish | source
```

可以配置键绑定，只需要在上方那一行中添加对应的参数即可。

比如禁用 `Ctrl-R`，仅需要将参数置空即可

```bash
fzf --fish | FZF_CTRL_R_OPTS= source
```

默认情况下是按照相关性排序的。可以通过再按一次 `Ctrl-R` 切换为按时间排序。可以通过添加 `--no-sort` 到 `FZF_CTRL_R_OPTS` 来默认启按时间排序。

同样可以添加下述内容到 `FZF_CTRL_R_OPTS` 产生不同效果：

- `--exact`: 使用精确（非模糊）匹配
- `--preview 'echo {}' --preview-window up:3:hidden:wrap`: 太长的命令在屏幕上无法完全显示。可以使用 `--preview` 选项在预览窗口上显示完整命令。`--preview-window` 选项是对预览窗口的配置 `up:3:hidden:wrap` 表示预览窗口在主窗口上方，高度为 3 行，且默认隐藏，且文本自动换行。
- `--bind 'ctrl-/:toggle-preview'`: 绑定 `Ctrl-/` 用于切换预览窗口
- `--bind 'ctrl-y:execute-silent(echo -n {2..} | tmux load-buffer -)+abort'` 绑定 `Ctrl-y` 用于复制该条命令到剪贴板，这里由于我是 ubuntu，采用的是 tmux 的剪贴板
- `--color header:italic`: 用于标题显示为斜体
- `--header 'Press Ctrl-Y to copy command into clipboard'"`: 设定标题
- `--tmux bottom,40%`: fzf 将在 tmux 弹出窗口中启动，当没有使用 tmux 时，将被忽略。`# --tmux [center|top|bottom|left|right][,SIZE[%]][,SIZE[%][,border-native]]`，其中第一个 size 为宽度，第二个为高度，仅有一个时根据位置不同而不同，比如位于 bottom 时，size 为高度，位于 right 时为宽度。此前提到的 `--preview-window` 的 size 设置同理，那个 3 行可以更换为百分比。

`Ctrl-T` 通常是 Shell 的默认快捷键，用于交换光标前后的字符（例如，将 `abd|def` 变为 `abd|cef`）。

不过在安装 `fzf` 后，`Ctrl-T` 的作用就变成了在当前目录及其子目录中递归搜索文件，并将选中的文件路径插入到命令行中。

也可以对其进行相关配置，类似于上述对 `Ctrl-R` 的配置。

`fzf` 还有其他常用的快捷键：

- `Ctrl-G`：搜索 Git 文件（需要配置 Git 插件）
- `Alt-C`：搜索目录并切换到选中的目录

我的 `fzf` 在 fish 中是这样配置的：

```bash
fzf --fish | source

set -gx FZF_CTRL_R_OPTS "
    --no-sort
    --bind 'ctrl-y:execute-silent(echo -n {2..} | tmux load-buffer -)+abort'
    --header 'Press CTRL-Y to copy command into clipboard'
"

set -gx FZF_DEFAULT_OPTS "
    --preview 'echo {}'
    --preview-window up:3:hidden:wrap
    --bind 'ctrl-/:toggle-preview'
    --color bg+:#363A4F,bg:#24273A,spinner:#F4DBD6,hl:#ED8796 \
    --color fg:#CAD3F5,header:#ED8796,info:#C6A0F6,pointer:#F4DBD6 \
    --color marker:#F4DBD6,fg+:#CAD3F5,prompt:#C6A0F6,hl+:#ED8796 \
    --color header:italic
    --header 'Select a file'
    --prompt 'Search> '
    --tmux bottom,80%,50%
    --bind 'alt-1:reload(find . -maxdepth 1)'
    --bind 'alt-2:reload(find . -maxdepth 2)'
    --bind 'alt-3:reload(fd)'
"

set -gx FZF_CTRL_T_OPTS "
    --preview 'cat {}'
    --preview-window right:60%:hidden:wrap
    --tmux bottom,80%,50%
"
```

可配置性很高，今天就暂时先玩到这里吧，下次空了我专门写篇文章总结下这些配置吧，很有意思，`fzf` 也很强大。

---

**Practice**

Q1:

- 所有文件(包括隐藏文件): `ls -a` 或 `ls --all`
- 文件打印以人类可以理解的格式输出 (例如，使用 454M 而不是 454279954): `ls -h` 或 `ls --human-readable`
- 文件以最近访问顺序排序: `ls -t` 或 `ls --sort=time`
- 以彩色文本显示输出结果: `ls --color[=WHEN]` 其中 `WHEN` 可以是 `always`、`yes`、`force`、`never`、`no`、`none`、`auto`、`tty`、`if-tty` 等，也可以省略，省略时是彩色

Q2: 由于我使用的是 fish，因此写法与 bash 有一点不同

```bash
# marco.fish
# 定义一个全局变量来保存当前目录
set -g MARCO_DIR ""

# marco 函数：保存当前工作目录
function marco
    set -g MARCO_DIR $(pwd)
    echo "当前位置已记录: $MARCO_DIR"
end

# polo 函数：返回到执行 marco 时保存的目录
function polo
    if test -z "$MARCO_DIR"
        echo "未找到记录的位置，请先运行一次 marco 以记录"
    else
        cd "$MARCO_DIR" || echo "跳转 $MARCO_DIR 时失败"
    end
end
```

Q3:

```bash
#!/usr/bin/env bash

# 定义日志文件
LOGFILE="output.log"

# 清空日志文件
> "$LOGFILE"

# 计数器，记录运行次数
COUNT=0

# 循环运行目标脚本，直到它出错
while true; do
    # 增加计数器
    COUNT=$((COUNT + 1))

    # 运行目标脚本，并将标准输出和标准错误流追加到日志文件
    ./target_script.sh >> "$LOGFILE" 2>&1

    # 检查上一个命令的退出状态
    if [[ $? -ne 0 ]]; then
        echo "脚本在第 $COUNT 次运行时失败。"
        echo "以下是日志文件的内容："
        cat "$LOGFILE"
        break
    fi
done
```

其中值得一提的是 `./target_script.sh >> "$LOGFILE" 2>&1` 中的 `2>&1`，其意思是将标准错误流重定向到标准输出流（文件描述符 `1`）的同一位置，而前面的 `>> "$LOGFILE"` 已经将标准输出流重定向到了 `$LOGFILE`，因此通过 `2>&1` 就将标准错误流也重定向到了 `$LOGFILE` 中，如果不使用 `2>&1`，即 `./target_script.sh >> "$LOGFILE"` 那么 `./target_script.sh` 中往标准输出流的内容会被正确的重定向到 `$LOGFILE` 中而标准错误流则会直接输出到终端。

Q4:

通过 `find` 的 `-print0` 将找到的文件名以 `null` 字符（ `\0` ）分隔输出。这是为了正确处理文件名中包含空格或特殊字符的情况。

`xargs` 的 `-d '\0'` 是指定 `null` 字符（ `\0` ）作为分隔符，与 `find -print0` 配合使用。

```bash
find . -type f -name "*.html" -print0 | xargs -d '\0' zip html_files.zip
```

或者更简洁的写法将 `-d '\0'` 写为 `-0`，二者等效。

```bash
find . -type f -name "*.html" -print0 | xargs -0 zip html_files.zip
```

Q5:

```bash
#!/usr/bin/env bash

# 用法：./recent_files.sh /path/to/directory [atime|mtime]

DIR="${1:-.}"  # 默认当前目录
TIME_TYPE="${2:-mtime}"  # 默认按修改时间排序

if [[ "$TIME_TYPE" == "atime" ]]; then
  FORMAT="%X %n"
elif [[ "$TIME_TYPE" == "mtime" ]]; then
  FORMAT="%Y %n"
else
  echo "错误：时间类型必须是 'atime' 或 'mtime'"
  exit 1
fi

find "$DIR" -type f -exec stat --format="$FORMAT" {} + | sort -nr | cut -d' ' -f2-
```

其中 `:-` 表示如果前面的变量为空或为设置，则使用后面的值。

`stat` 是一个用于显示文件或文件系统状态的命令行工具。

`--format="格式字符串"` 其中格式字符串为使用 `%` 开头的占位符来指定要显示的字段

以下是一些常用的 `stat` 占位符

| 占位符 | 说明                           |
| :----: | :----------------------------- |
|  `%n`  | 文件名                         |
|  `%s`  | 文件大小（字节）               |
|  `%U`  | 文件所有者的用户名             |
|  `%G`  | 文件所属的用户组               |
|  `%A`  | 文件的访问权限（人类可读格式） |
|  `%a`  | 文件的访问权限（八进制格式）   |
|  `%F`  | 文件类型（例如普通文件、目录） |
|  `%X`  | 最后访问时间（时间戳）         |
|  `%Y`  | 最后修改时间（时间戳）         |
|  `%Z`  | 最后状态变更时间（时间戳）     |
|  `%w`  | 文件创建时间（时间戳）         |

`find "$DIR" -type f -exec stat --format="$FORMAT" {} + | sort -nr | cut -d' ' -f2-` 中的 `+` 的作用为将多个文件一次性传递给 `stat`，而不是每次传递一个文件（比 `\;` 更高效）

`sort -nr` 中 `-n` 表示按数值排序（因为时间戳是数字），`-r` 表示按逆序排序（从小到大，即最新的文件在前）

`cut -d' ' -f2-` 中 `-d' '` 表示指定字段分隔符为空格，`-f2-` 表示提取从第 2 个字段开始的所有内容（即去掉时间戳，只保留文件名）

`cut` 是一个用于从文本行中提取特定字段的命令行工具。它通常用于处理结构化文本（例如 CSV 文件、日志文件等），通过指定分隔符和字段编号来提取所需的内容。

基本语法:

```bash
cut [选项] 文件
```

常用选项:

| 选项           | 说明                                                       |
| :------------- | :--------------------------------------------------------- |
| `-d`           | 指定字段分隔符（默认是制表符 `\t`）                        |
| `-f`           | 指定要提取的字段编号（从 1 开始）                          |
| `-c`           | 按字符位置提取内容（例如 `-c 1-5` 提取第 1 到第 5 个字符） |
| `--complement` | 提取除指定字段之外的所有内容                               |

cut 的 -f 选项支持多种字段范围语法：

| 语法    | 说明                            | 示例输入  | 输出    |
| :------ | :------------------------------ | :-------- | :------ |
| `-fN`   | 提取第 N 个字段                 | `a b c d` | `b`     |
| `-fN-`  | 提取从第 N 个字段开始的所有字段 | `a b c d` | `b c d` |
| `-fN-M` | 提取第 N 到第 M 个字段          | `a b c d` | `b c`   |
| `-f-M`  | 提取从第 1 个字段到第 M 个字段  | `a b c d` | `a b c` |

### 01.12

> Learning Time: About `3` hours

---

尽管已经是用过一段时间的 vim 了，但确实还是第一次知道原来还内置了一个教程 `vimtutor`，而且居然还有中文，用这个入门确实是很不错的，之前全靠搜索和从键位图里根据需求去找，如果能在第一次使用时过一遍 `vimtutor` 估计会轻松很多。所以用一个对自己陌生的工具时确实还是可以考虑先看看官方的相关教程，~~当然也不是所有的教程都做的很好~~，同时如果我自己做一些工具的话，也应考虑做一个 nice tutorial。

### 01.17

> Learning Time: About `1` hours

---

近期也是学到了很多的工具，它们都有自己相应的配置文件，配置起来确实有些许麻烦，因此基本上当我们的配置基本上成形后会考虑将其备份、同步，比较普通的做法大概就是自己将其手动备份到其它地方进行保存，不过这样太过麻烦，也考虑了下参考大多数人的借助 Github 进行备份，这确实是不错的做法了，定期维护下就好。

这段时间忙于杂七杂八的事情，有点担心这里落后太多跟不上，还好看了下发现原来好多东西在之前的使用中由于踩坑也好还是主动学习也好也有问其他朋友获知的也好，已经基本上都是接触了解过了，果然还是实践出真知啊。

刚开始学习这个课程时，我遇到了一个问题，如果是没有开启梯子的环境下我无法 clone、fetch 仓库，因此使用镜像站，然而当更新了内容尝试 push 时发现镜像站没法 push，这比较尴尬。我现在倒是通过设置了多个远端来处理了这个问题，不过也不能算是解决？一个是镜像远端一个是官方远端，每当我尝试 fetch 时就选择镜像远端这样稳定直接。当我需要 push 内容时则选择官方远端，不过之所以说不算是解决问题，因为没有梯子的话，官方远端在 push 时确实也不是每次都能让我稳定地更新。

git 中撤销这部分的内容感觉对我来说是很重要的知识，我好几次操作失误了，把 git 弄得乱糟糟的还不弄不清楚怎么复原，越弄越乱。这个教程真的很有意思，对于这些工具都分享了许多很有帮助的资源，[Oh Shit, Git!?!](https://ohshitgit.com/) 很有意思，也确实对我帮助蛮大的。

不过对于我这种懒人而言，我还是更倾向于使用图形用户界面客户端，比如 windows 这边的 github desktop，至少使用起来我不会太容易搞出问题，很多操作都比较直观。

<!-- Content_END -->
