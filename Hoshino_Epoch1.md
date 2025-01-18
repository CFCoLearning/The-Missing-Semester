# CFC Studio 共学 Epoch1 指引
---
# Hoshino

> I'm joker king.

## 笔记证明

<!-- Content_START --> 

### 01.06

Study Time: 3h (Allright, I spend most of my time on reading English text, it's so hard for me.)

#### Note

The shell is a textual interface for computer, they allow you to run programs, give them input, and inspect their output in a semi-structured way.

The shell is a programming environment.Running a command in the shell is similar to writing a piece of code that the shell interprets and executes. When a command is entered, the shell searches for an executable program either in the directories listed in the `$PATH` environment variable or in the current directory (if specified explicitly).

#### Exercises

In `shell scripting` and `command-line operations`, the difference between **single quotes**`''` and **double quotes** `""`  lies in how they handle variables, special characters, and escape sequences. 

Everything inside single quotes is treated literally. Variables, escape characters, and special characters are not interpreted; they are taken as plain text.But double quotes allow the interpretation of variables, escape sequences, and command substitutions, while preserving spaces and special characters as part of the string.

![image-20250106220057226](https://minio.drivefly.cn:443/image-hoshino/blog/2025/01/06/image-20250106220057226.png)

This command line performs four operations.Firt, it runs the `./semester` to get some info.Second, `grep` filters the output of `./semester` to include only lines containing the string `last-modified`.Third, `cut` extracts specific fields from the lines filtered by grep(`-d' '` specifies that fields in the line are separated by spaces, `-f2-` instructs `cut` to output everything from the second field onwards).At last, `>` will  redirect the output of the previous commands to a file named `last-modified.txt`.

![image-20250106220743702](https://minio.drivefly.cn:443/image-hoshino/blog/2025/01/06/image-20250106220743702.png) 

### 01.10

Study Time: 2h.

#### Note

The last lecture has said that the `shell` is a programming enviroments, so most shells have their own scripting language with variables, control flow and its own syntax.Therefore, I think using `shell script` is just writing a short piece of code.

> Notice：`shell` and `shell script` are different things. `shell` is an application that provides an interface through which users access the services of the operating system kernel.But `shell script` is a program written for `shell`.
>

Unlike other programming languages we know, in `bash`, whitespace is a special keyword, it is used to split the parameters.And `bash` uses a variety of special variables to refer to arguments, error codes, and other relevant variables.

In `bash`, commands can be used to conditionally execute commands using `&&` (and operator) and `||` (or operator), both of which are short-circuiting operators.

Whenever you place `$( CMD )` it will execute `CMD`, get the output of the command and substitute it in place. A lesser known similar feature is *process substitution*, `<( CMD )` will execute `CMD` and place the output in a temporary file and substitute the `<()` with that file’s name.

When performing comparisons in `bash`, try to use double brackets `[[ ]]` in favor of simple brackets `[ ]`. Chances of making mistakes are lower although it won’t be portable to `sh`. A more detailed explanation can be found [here](http://mywiki.wooledge.org/BashFAQ/031).

The shell *globbing* can help you to provide arguments that are similar.

> - Wildcards - Whenever you want to perform some sort of wildcard matching, you can use `?` and `*` to match one or any amount of characters respectively. For instance, given files `foo`, `foo1`, `foo2`, `foo10` and `bar`, the command `rm foo?` will delete `foo1` and `foo2` whereas `rm foo*` will delete all but `bar`.
> - Curly braces `{}` - Whenever you have a common substring in a series of commands, you can use curly braces for bash to expand this automatically. This comes in very handy when moving or converting files.

Note that scripts need not necessarily be written in bash to be called from the terminal.Because if a text file begin with the `shebang` line(a line starting with `#!`), then the `kernel` will know to execute this script with which interpreter,, so we can also use  a python interpreter by using `#!/usr/local/bin/python`(like this).

It is good practice to write `shebang` lines using the [`env`](https://www.man7.org/linux/man-pages/man1/env.1.html) command that will resolve to wherever the command lives in the system, increasing the portability of your scripts. To resolve the location, `env` will make use of the `PATH` environment variable we introduced in the first lecture. For this example the `shebang` line would look like `#!/usr/bin/env python`.

> When a text file with a `shebang` is used as if it were an executable in a Unix-like operating system, the program loader mechanism parses the rest of the file's initial line as an interpreter directive.

> Some differences between shell functions and scripts that you should keep in mind are:
>
> - Functions have to be in the same language as the shell, while scripts can be written in any language. This is why including a shebang for scripts is important.
> - Functions are loaded once when their definition is read. Scripts are loaded every time they are executed. This makes functions slightly faster to load, but whenever you change them you will have to reload their definition.
> - Functions are executed in the current shell environment whereas scripts execute in their own process. Thus, functions can modify environment variables, e.g. change your current directory, whereas scripts can’t. Scripts will be passed by value environment variables that have been exported using [`export`](https://www.man7.org/linux/man-pages/man1/export.1p.html)
> - As with any programming language, functions are a powerful construct to achieve modularity, code reuse, and clarity of shell code. Often shell scripts will include their own function definitions.

### 01.11

Study Time: 1h.

#### Note

Today I got familiar with the use of several shell tools and did some exercises.

#### Exercise

1. > `-l`use a long listing format.
   >
   > `-h` with `-l` and `-s`, print sizes like 1K 234M 2G etc.
   >
   > `--sort=WORD` sort by WORD instead of name: none (-U), size (-S), time(-t), version (-v), extension (-X), width.
   >
   > `--time=WORD` select which timestamp used to display or sort; access time (-u): atime, access, use; metadata change time (-c):ctime, status; modified time (default): mtime,modification; birth time: birth, creation;with -l, WORD determines which time to show; with --sort=time, sort by WORD (newest first).
   >
   > `--color[=WHEN]`  color the output WHEN; more info below

```shell
ls -lha --sort=time --time=atime --color=auto
```

![](https://raw.githubusercontent.com/xszhangxiaocuo/picBed/master/picBed/image-20250111175249287.png)

2.

```shell
marco() {
    export MARCO_DIR=$(pwd)  # Save the current working directory in the environment variable MARCO_DIR
    echo "Saved current directory: $MARCO_DIR"
}

polo() {
    if [ -z "$MARCO_DIR" ]; then
        echo "No directory saved. Please run 'marco' first."
    else
        cd "$MARCO_DIR"  # Switch to the saved directory
        echo "Changed to saved directory: $MARCO_DIR"
    fi
}
```

3.

target_script.sh

```shell
#!/usr/bin/bash

n=$(( RANDOM % 50 ))

if [[ $n -eq 42 ]]; then
    echo "Something went wrong"
    >&2 echo "The error was using magic numbers"
    exit 1 
fi

echo "Everything went according to plan"
exit 0 
```

main_script

```shell
#!/usr/bin/bash

output_file="script_output.log"
error_file="script_error.log"

run_count=0

while true; do
    ((run_count++))

    # Call target_script, capturing output and errors
    ./target_script.sh >> "$output_file" 2>> "$error_file"

    if [[ $? -ne 0 ]]; then
        break
    fi
done

echo "The script ran $run_count times before failing."
echo "Standard Output was saved to $output_file"
echo "Standard Error was saved to $error_file"
```

### 01.16

Study Time: 2h.

#### Note

Today I mainly experienced the use of nvim plugin in VS code.

Vim is a deeply customizable editor with very powerful functions.You don't need a mouse to use Vim, you can quickly view the contents of the file using just the keyboard.But for me, I still prefer to use VS code.So I decide to use a Vim plugin for VS code.I think this will be the best way to use Vim for me.

> Vim avoids the use of the mouse, because it’s too slow; Vim even avoids using the arrow keys because it requires too much movement.The end result is an editor that can match the speed at which you think.

I have to admit that this is right.Using the mouse to position is waste of time, we can be faster by only use keyboard.However, in actual project development, it is obviously inappropriate to only use vVm for code editing. We still need an IDE to help us complete project development.So I think using Vim through a plugin in VS code to complete a project is a more appropriate solution.This can not only complete project development easier, but also improve our code editing efficiency and experience.

### 01.18

Study Time: 1h

#### Note

Today I mainly learned how to use awk, sed and grep.

Awk is an application for processing text files. Almost all Linux systems come with this program.It processes each line of the file in turn and reads each field in it. For text files with the same format for each line, such as logs and CSV, awk may be the most convenient tool.Awk is not only a tool software, but also a programming language.

Sed is a stream editor. It is a very important tool in text processing and can be used perfectly with regular expressions. When processing, the current line is stored in a temporary buffer, called the "pattern space". Then the sed command is used to process the contents of the buffer. After the processing is completed, the contents of the buffer are sent to the screen. Then the next line is processed, and this is repeated until the end of the file. The file content does not change unless you use redirection storage output. Sed is mainly used to automatically edit one or more files; simplify repeated operations on files; write conversion programs, etc.

grep (global search regular expression (RE) and print out the line) is a powerful text search tool that can use regular expressions to search text and print out matching lines. It is used to filter/search for specific characters. Regular expressions can be used with a variety of commands, making it very flexible to use.

Proficient use of these three tools can meet most data processing needs.



<!-- Content_END -->