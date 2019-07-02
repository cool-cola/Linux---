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

### 8. 查看进程运行时间
可以使用下面命令查看进程已运行时间：
```
[root@VM_64_4_centos ~]# ps -p 3215 -o lstart,etime
                 STARTED     ELAPSED
Tue Jun 11 11:01:04 2019 21-00:15:31
```
其中 3215是你要查看进程的进程id

### 9. 快速切换目录
* cd - ：回到上一个目录
* cd：回到用户家目录

### 10. 多条命令执行
我们指定使用分隔符可以执行多条命令，例如：
>$ cd /temp/log/; rm -rf *

但是如果当前目录是 / 目录，并且/temp/log 目录不存在，那么就好发生激动人心的一幕：
> bash: cd: /temp/log: No such file or directory

因为；符号可以执行多条命令，但是不会因为前一条命令失败，而导致后面的命令不会执行；因此，cd执行失败后，仍然会继续执行rm -rf * ，由于当前处于/ 目录下，结果可想而知！

如果解决呢？很简单，使用&&，例如：
> $ cd /temp/log/&&rm -rf *

这样就会确保前一条命令执行成功后，才会执行后面一条

### 11. 查看压缩日志文件
有时候日志文件是压缩的，那么能不能偷懒下，不解压查看呢？当然可以的，例如：
> $ zcat test.gz

or
> zless test.gz

### 12. 清空文件内容
比如有一个大文件，你想快速删除，或者不想删除，但想清空内容：
>[root@VM_64_4_centos ~]# >test.xls

### 13. 将日志同时记录文件并打印到控制台
在执行shell 脚本，常常会将日志重定向，但是这样的话，控制台就没有打印了，如何使得既能记录日志，又能将日志输出到控制台呢？
> $ ./test.sh | tee test.log

### 14. 终止并恢复进程执行
我们使用ctrl + z暂停一个进程的执行，也可以使用fg 恢复执行。例如我们使用 
> cat filename

当我们发现文件内容可能很多时，使用ctrl + z 暂停程序，而如果又想要从刚才的地方继续执行，则只需要使用fg命令即可恢复执行。或者使用bg 命令使得进程继续在后台执行

### 15. 计算程序运行时间
我们可能会经常写一些小程序，并且想要知道它的运行时间，实际上我们可以很好的利用time 命令帮我们计算，例如：
```
$ time ./fibo 30
the 30 result is 832040

real 0m0.088s
user 0m0.084s
sys 0m0.004s
```
它会显示系统时间，用户时间以及实际使用的总时间。

### 16. 查看内存占用前10 的进程
> [root@VM_64_4_centos ~]# ps -aux | sort -k4nr | head -n 10

这里综合使用了 ps、sort、head 命令

### 17. 快速查看你需要的命令
我们知道man 可以查看命令的帮助手册，但是如果我们想要某个功能却不知道使用那个命令呢？别着急，还是可以使用man ：
```
[root@VM_64_4_centos ~]# man -k "copy file"
cp (1)               - copy files and directories
cpio (1)             - copy files to and from archives
File::Copy (3pm)     - Copy files or filehandles
install (1)          - copy files and set attributes
```
使用 -k 参数，使得与copy file 相关的帮助手册都显示出来了。

### 18. 命令行下的复制粘贴
我们知道，在命令行下，复制不能再是ctrl + c 了，因为它表示终止当前程序，而控制台下的复制粘贴需要使用下面的快捷键：
```
* CTRL + insert
* shift + insert
```

## 19. 搜索包含某个字符串的文件
例如，要在当前目录下查找包含test字符串的文件
```
[root@VM_64_4_centos ~]# grep -rn 'producer'
.bash_history:29:vim producer.py 
.bash_history:39:python producer.py
```
它便可以找到该字符串在哪个文件的第几行。

### 20. 屏幕冻结
程序运行时，终端可能输出大量的日志，你想简单查看一下，又不想记录日志文件，此时可以使用ctrl+s 按键，冻结屏幕，使得日志不再继续输出，而如果想要恢复，可使用ctrl+q退出冻结。

### 21. 无编辑器情况下编辑文本文件
如果在某些系统上连基本的vi编辑器都没有，那么可以使用下面的方式进行编辑内容：
```
[root@VM_64_4_centos ~]# cat >cookie.txt 
cookie: uin=o100007799884; token=2b547a450f0b[root@VM_64_4_centos ~]#
```
编辑完成后，ctrl + d即可保存

### 22. 查看elf文件




