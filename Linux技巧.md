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
使用df 命令可以快速查看各挂载路径磁盘占用情况

#### 5.2 当前目录各子目录占用空间大小
如果你已经知道home目录占用空间大小，你想知道usr 目录下各个目录占用情况：

```
[root@VM_64_4_centos usr]# du -h --max-depth=1 /usr
747M	/usr/lib
4.0K	/usr/etc
311M	/usr/local
4.0K	/usr/games
312M	/usr/share
129M	/usr/bin
41M	/usr/libexec
74M	/usr/src
163M	/usr/lib64
49M	/usr/sbin
9.0M	/usr/include
1.8G	/usr
```
这里指定了目录深度，否则的话，它会递归统计子目录占用空间大小，可自动尝试。

#### 5.3 当前内存使用情况

```
[root@VM_64_4_centos usr]# free -h
              total        used        free      shared  buff/cache   available
Mem:           991M        121M         77M        516K        791M        686M
Swap:            0B          0B          0B
```
通过free 的结果，很容易看到当前总共内存多少，剩余可用内存多少等等

##### 5.3.1 使用-h 参数
不知道你是否注意到，在前面几个命令中，都使用了-h 参数，它的作用是使得结果以人类可读的方式呈现，所以我们看到它呈现的单位是G、M 等，如果不使用-h 参数，可以自行尝试会呈现什么样的结果。

### 6. 根据名称查找进程id
想快速直接查找进程id，可以使用：
```
[root@VM_64_4_centos ~]# pgrep ssh
2992
17706
22515
24582
24583
```
或者
```
[root@VM_64_4_centos ~]# pidof sshd
22515 17706 2992
```
其中，sshd 是进程名称

### 7. 根据名称杀死进程
一般我们可以使用kill -9 pid 的方式杀死一个进程，但是这样就需要先找到这个进程的进程id，实际上我们也可以直接根据名称杀死进程，例如：
> killall hello
or
> pkill hello
