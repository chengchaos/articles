# Shell 的命令

## 命令的类别

Bash可以使用的命令分成四类。

- 可执行程序
- Shell 提供的命令
- Shell 函数
- 前三类命令的别名

## type, whatis

`type`命令可以显示命令类型。

```bash
$ type command
```

下面是几个例子。

```bash
$ type type
type is a shell builtin

$ type ls
ls is aliased to `ls --color=tty'

$ type cp
cp is /bin/cp
```

`whatis`命令显示指定命令的描述。

```bash
$ whatis ls
ls (1) - list directory contents
```

## apropos

`apropos`命令返回符合搜索条件的命令列表。

```bash
$ apropos floppy
create_floppy_devices (8) - udev callout to create all possible
fdformat (8) - Low-level formats a floppy disk
floppy (8) - format floppy disks
gfloppy (1) - a simple floppy formatter for the GNOME
mbadblocks (1) - tests a floppy disk, and marks the bad
mformat (1) - add an MSDOS filesystem to a low-level
```

## alias, unalias

`alias`命令用来为命令起别名。

```bash
$ alias foo='cd /usr; ls; cd -'

$ type foo
foo is aliased to `cd /usr; ls ; cd -'
```

上面命令指定`foo`为三个命令的别名。以后，执行`foo`就相当于一起执行这三条命令。

注意，默认情况下，别名只在当前Session有效。当前Session结束时，这些别名就会消失。

`alias`命令不加参数时，显示所有有效的别名。

```bash
$ alias
alias l.='ls -d .* --color=tty'
alias ll='ls -l --color=tty'
alias ls='ls --color=tty'
```

`unalias`命令用来取消别名。

```bash
$ unalias foo
$ type foo
bash: type: foo: not found
```

## which

`which`命令显示可执行程序的路径。

```bash
$ which ls
/bin/ls
```

`which`命令用于Shell内置命令时（比如`cd`），将没有任何输出。

## help，man

`help`命令用于查看Shell内置命令的帮助信息，`man`命令用于查看可执行命令的帮助信息。

```bash
$ help cd
$ man ls
```

`man`里面的文档一共有8类，如果同一个命令，匹配多个文档，`man`命令总是返回第一个匹配。如果想看指定类型的文档，命令可以采用下面的形式。

```bash
$ man 5 passwd
```

## script

`script`命令会将输入的命令和它的输出，都保存进一个文件。

```bash
$ script [file]
```

如果没有指定文件名，则所有结果会保存进当前目录下`typescript`文件。结束录制的时候，可以按下`Ctrl + d`。

## export

`export`命令用于将当前进程的变量，输出到所有子进程。

## 命令的连续执行

多个命令可以写在一起。

Bash 提供三种方式，定义它们如何执行。

```bash
# 第一个命令执行完，执行第二个命令
command1; command2

# 只有第一个命令成功执行完（退出码0），才会执行第二个命令
command1 && command2

# 只有第一个命令执行失败（退出码非0），才会执行第二个命令
command1 || command2
```

上面三种执行方法的退出码，都是最后一条执行的命令的退出码。