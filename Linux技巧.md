### 1. 前言
Linux 中的一些小技巧可以大大提升日常工作效率，本文总结了哪些提高效率 or 简单有效的Linux 技巧！

### 2. 命令编辑及光标移动
这里有很多快捷键可以帮我们修正自己的命令。接下来使用光标二字代替光标的位置。

#### 2.1 删除从开头到光标处的命令文本
>  ctrl + u, 例如：
>  [root@hadoop4 ~]# cd /proc/tty; ls -al

如果此时使用ctrl + u 快捷键，那么该条命令都会被清除，而不需要长按backspace按键。

#### 2.2 删除从光标到结尾处的命令文本
> ctrl + k, 例如：
> [root@hadoop4 ~]# cd /proc/tty光标; ls -al

如果此时使用ctrl + k 快捷键，那么从光标开始处到结尾的命令文本将会被删除。

还有其他的操作，不再举例，例如：
* ctrl + a：光标移动到命令开头
* ctrl + e：光标移动到命令结尾
* ctrl + w：删除一个词（以空格隔开的字符串）
* alt + f：光标向前移动一个单词
* alt + b: 光标向后移动一个单词

### 3. 历史命令快速执行
我们都知道history 记录了执行的历史命令，而使用 ！+ 历史命令前的数字，可快速执行历史命令。另外，还可以使用ctrl + r 搜索执行过的命令。

#### 3.1 部分历史命令查看
history 会显示大量的历史命令，而fc -l 只会显示部分。

### 4. 实时查看日志
> $ tail -f filename.log

tail -f 加文件名，可以实时显示日志文件内容。当然，使用less 命令查看文件内容，并且使用shift + f 按键，也可达到类似的效果。

### 5. 磁盘或内存情况查看
#### 5.1 怎么知道当前磁盘是否满了吗？

```
[root@VM_64_4_centos ~]# df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/vda1        50G  4.0G   43G   9% /
devtmpfs        486M     0  486M   0% /dev
tmpfs           496M   24K  496M   1% /dev/shm
tmpfs           496M  500K  496M   1% /run
tmpfs           496M     0  496M   0% /sys/fs/cgroup
tmpfs           100M     0  100M   0% /run/user/0
```
