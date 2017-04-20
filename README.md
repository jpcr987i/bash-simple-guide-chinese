# bash-simple-guide-chinese
bash简明入门,linux shell 入门指南 教程

### May you share freely, never taking more than you give.

## 目录
  1. [基础操作](#1-basic-operations)  
    1.1. [文件操作](#11-file-operations)  
    1.2. [文本操作](#12-text-operations)  
    1.3. [文件夹操作](#13-directory-operations)  
    1.4. [SSH, 系统信息, 网络信息](#14-ssh-system-info--network-operations)  
    1.5. [系统进程查看(TODO)](#15-process-monitoring-operations)
  2. [基础sheel脚本编程](#2-basic-shell-programming)  
    2.1. [变量](#21-variables)  
    2.2. [数组](#22-array)  
    2.3. [字符串操作](#23-string-substitution)  
    2.4. [方法/函数](#24-functions)  
    2.5. [条件语句](#25-conditionals)  
    2.6. [循环](#26-loops)  
  3. [基础技巧](#3-tricks)  
  4. [调试](#4-debugging)  
  

# 1. 基础操作

### a. `export`
显示所有系统环境变量，如果想查看某个具体变量的详细信息，可以使用 `echo $VARIABLE_NAME`.  
```bash
export
```
示例:
```bash
$ export
AWS_HOME=/Users/adnanadnan/.aws
LANG=en_US.UTF-8
LC_CTYPE=en_US.UTF-8
LESS=-R

$ echo $AWS_HOME
/Users/adnanadnan/.aws
```

### b. `whatis`
whatis 用来查看某个命令、系统调用或者库函数的简单描述
```bash
whatis something
```
示例:
```bash
$ whatis ls
ls (1)             - list directory contents
```

### c. `whereis`
查看某个命令的可执行文件、资源文件、帮助页面的绝对地址
```bash
whereis name
```
示例:
```bash
$ whereis php
/usr/bin/php
```

### d. `which`
在PATH变量指定的路径中搜索某个系统命令的位置并且返回第一个搜索结果。也就是说使用which命令就可以看到某个系统命令是否存在以及执行的到底是哪一个位置的命令
```bash
which program_name 
```
示例:
```bash
$ which php
/c/xampp/php/php
```

### e. clear
清空当前屏幕或终端上显示的内容

## 1.1. 文件操作
<table>
   <tr>
      <td><a href="#a-cat">cat</a></td>
      <td><a href="#b-chmod">chmod</a></td>
      <td><a href="#c-cp">cp</a></td>
      <td><a href="#d-diff">diff</a></td>
      <td><a href="#e-file">file</a></td>
      <td><a href="#f-find">find</a></td>
      <td><a href="#g-gunzip">gunzip</a></td>
      <td><a href="#h-gzcat">gzcat</a></td>
      <td><a href="#i-gzip">gzip</a></td>
      <td><a href="#j-head">head</a></td>
   </tr>
   <tr>
      <td><a href="#k-lpq">lpq</a></td>
      <td><a href="#l-lpr">lpr</a></td>
      <td><a href="#m-lprm">lprm</a></td>
      <td><a href="#n-ls">ls</a></td>
      <td><a href="#o-more">more</a></td>
      <td><a href="#p-mv">mv</a></td>
      <td><a href="#q-rm">rm</a></td>
      <td><a href="#r-tail">tail</a></td>
      <td><a href="#s-touch">touch</a></td>
   </tr>
</table>

### a. `cat`
在UNIX或Linux下可以实现:  
```bash
cat filename; cat file1 file2      #显示一个或多个文件的所有内容
cat file1 file2 > newcombinedfile  #合并多个文件的内容到一个新的文件
cat < file1 > file2                #复制 file1 到 file2
```

### b. `chmod`
改变文件的读、写、执行权限  [命令详解](https://www.ibm.com/support/knowledgecenter/zh/ssw_aix_71/com.ibm.aix.cmds1/chmod.htm)

```bash
chmod -options filename
```

### c. `cp`
文件复制
```bash
cp path-from/filename1 path-to/filename2 #从filename1 复制到 filename2
```


### d. `diff`
比较两个文件的内容，并将差异显示出来 
```bash
diff filename1 filename2
```

### e. `file`
查看文件的类型
```bash
file filename
```
示例:
```bash
$ file index.html
 index.html: HTML document, ASCII text
```
### f. `find`
在指定文件夹中查找文件    [命令详解](http://man.linuxde.net/find)
```bash
find directory options pattern
```
示例:
```bash
$ find . -name README.md
$ find /home/user1 -name '*.png'
```

### g. `gunzip`
解压一个gzip文件
```bash
gunzip filename
```

### h. `gzcat`
在不解压的情况下查看一个gzip文件  
```bash
gzcat filename
```

### i. `gzip`
使用gzip方式压缩一个文件 
```bash
gzip filename
```

### j. `head`
显示某个文件的前10行 
```bash
head filename
```

### k. `lpq`
查看打印机队列情况
```bash
lpq
```
示例:
```bash
$ lpq
Rank    Owner   Job     File(s)                         Total Size
active  adnanad 59      demo                            399360 bytes
1st     adnanad 60      (stdin)                         0 bytes
```

### l. `lpr`
使用打印机打印某个文件
```bash
lpr filename
```

### m. `lprm`
删除打印机队列中的某个任务 
```bash
lprm jobnumber
```

### n. `ls`
用来显示目标文件夹的文件列表，常用参数： `-l` 参数可以列出文件的大小、所属者和相应权限、以及文件的最后修改时间 `-a` 参数显示目标文件夹内所用的文件，包括隐藏文件，更多参数请看 [命令详解](http://man.linuxde.net/ls).  
```bash
ls option
```
示例:
<pre>
$ ls -la
rwxr-xr-x   33 adnan  staff    1122 Mar 27 18:44 .
drwxrwxrwx  60 adnan  staff    2040 Mar 21 15:06 ..
-rw-r--r--@  1 adnan  staff   14340 Mar 23 15:05 .DS_Store
-rw-r--r--   1 adnan  staff     157 Mar 25 18:08 .bumpversion.cfg
-rw-r--r--   1 adnan  staff    6515 Mar 25 18:08 .config.ini
-rw-r--r--   1 adnan  staff    5805 Mar 27 18:44 .config.override.ini
drwxr-xr-x  17 adnan  staff     578 Mar 27 23:36 .git
-rwxr-xr-x   1 adnan  staff    2702 Mar 25 18:08 .gitignore
</pre>

### o. `more`
每次一屏显示文本。该命令在每屏后暂停，并在屏幕底部打印单词 More。如果随后按回车键，more 命令会再显示一行。如果按下空格键，more 命令显示文本的另一屏。按 q 键退出  
```bash
more filename
```

### p. `mv`
移动一个文件
```bash
mv filename1 filename2  #移动filename1文件到filename2位置
```
也可以用来对一个文件重命名:
```bash
mv old_name new_name
```

### q. `rm`
删除一个文件. 如果用这个命令直接删除一个文件夹将报错，删除文件夹需要加上-r的参数，文件夹下的所有子文件和文件夹将被一同删除，使用-f参数可进行强制删除，不进行任何提示(慎用)
```bash
rm filename
rm -r directory
rm -f /   # never use this!
```

### r. `tail`
显示文件的最后10行，-f 参数可以监听文件尾部，一有新内容就显示，-n 参数可以指定需要显示的行数，常用于显示和监视日志文件
```bash
tail filename
tail -n 15 -f some_log_file #监听文件末尾变化并显示文件的最后15行的内容
```

### s. `touch`
用来修改文件时间戳，或者新建一个不存在的文件
```bash
touch filename
```
Example:
```bash
$ touch trick.md
```

## 1.2. 文本操作

<table>
    <tr>
      <td><a href="#a-awk">awk</a></td>
      <td><a href="#b-cut">cut</a></td>
      <td><a href="#c-echo">echo</a></td>
      <td><a href="#d-egrep">egrep</a></td>
      <td><a href="#e-fgrep">fgrep</a></td>
      <td><a href="#f-fmt">fmt</a></td>
      <td><a href="#g-grep">grep</a></td>
      <td><a href="#h-nl">nl</a></td>
      <td><a href="#i-sed">sed</a></td>
      <td><a href="#j-sort">sort</a></td>
   </tr>
   <tr>
      <td><a href="#k-tr">tr</a></td>
      <td><a href="#l-uniq">uniq</a></td>
      <td><a href="#m-wc">wc</a></td>
   </tr>
</table>

### a. `awk`
AWK是一种处理文本文件的语言，是一个强大的文本分析工具。

[awk三十分钟入门教程](https://segmentfault.com/a/1190000007338373)

```bash
awk '/search_pattern/ { action_to_take_if_pattern_matches; }' file_to_parse
```
简单示例: 以下是`/etc/passwd`文件中的内容
```
root:x:0:0:root:/root:/usr/bin/zsh
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
```
我们使用下面的命令来查找并返回上面文本中每一行的第一个单词，也就是用户名信息

`-F` 参数指定了文本的分隔符，这里后面跟了一个`:`，说明使用冒号作为每行文本的分隔符进行分析

`{ print $1 }` 表示打印出每一行第一个匹配到冒号的字符串
```bash
awk -F':' '{ print $1 }' /etc/passwd
```
执行命令后得到如下结果:
```
root
daemon
bin
sys
sync
```


### b. `cut`
移除文本中的某个或某几个部分


```bash
*示例文本*:
red riding hood went to the park to play
```

*使用如下命令实现:使用空格作为分隔符，并显示分割后的第2 第7 第9个字符串*
```bash
cut -d " " -f2,7,9 example.txt
```
执行结果:
```bash
riding park play
```

### c. `echo`
显示一行字符串

*显示 "Hello World"*
```bash
echo Hello World
```
```bash
Hello World
```

*显示 "Hello World" 并换行*
```bash
echo -ne "Hello\nWorld\n"
```
```bash
Hello
World
```

### d. `egrep`
在输入文件中搜索与用 第二个 参数指定的模式相匹配的行 (alias for: 'grep -E')

*example.txt*
```bash
Lorem ipsum
dolor sit amet, 
consetetur
sadipscing elitr,
sed diam nonumy
eirmod tempor
invidunt ut labore
et dolore magna
aliquyam erat, sed
diam voluptua. At
vero eos et
accusam et justo
duo dolores et ea
rebum. Stet clita
kasd gubergren,
no sea takimata
sanctus est Lorem
ipsum dolor sit
amet.
```

*找出包含 "Lorem" 或者 "dolor" 单词的行*
```bash
egrep '(Lorem|dolor)' example.txt
or
grep -E '(Lorem|dolor)' example.txt
```
```bash
Lorem ipsum
dolor sit amet,
et dolore magna
duo dolores et ea
sanctus est Lorem
ipsum dolor sit
```

### e. `fgrep`
查找包含指定字符串的行  (alias for: 'grep -F')

*example.txt*
```bash
Lorem ipsum
dolor sit amet,
consetetur
sadipscing elitr,
sed diam nonumy
eirmod tempor
foo (Lorem|dolor) 
invidunt ut labore
et dolore magna
aliquyam erat, sed
diam voluptua. At
vero eos et
accusam et justo
i have (Lorem|dolor)
rebum. Stet clita
kasd gubergren,
no sea takimata
sanctus est Lorem
ipsum dolor sit
amet.
```

*在example.txt查找包含 '(Lorem|dolor)' 字符串的行*
```bash
fgrep '(Lorem|dolor)' example.txt
or
grep -F '(Lorem|dolor)' example.txt
```
```bash
foo (Lorem|dolor) 
i have (Lorem|dolor)
```

### f. `fmt`
文本格式化

*example.txt (1 line)*
```bash
Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet.
```

*使用20字符宽度输出*
```bash
cat example.txt | fmt -w 20
```
```bash
Lorem ipsum
dolor sit amet,
consetetur
sadipscing elitr,
sed diam nonumy
eirmod tempor
invidunt ut labore
et dolore magna
aliquyam erat, sed
diam voluptua. At
vero eos et
accusam et justo
duo dolores et ea
rebum. Stet clita
kasd gubergren,
no sea takimata
sanctus est Lorem
ipsum dolor sit
amet.
```

### g. `grep`
根据pattern在filename中查找匹配到的文本行
```bash
grep pattern filename
```
示例:
```bash
$ grep admin /etc/passwd
_kadmin_admin:*:218:-2:Kerberos Admin Service:/var/empty:/usr/bin/false
_kadmin_changepw:*:219:-2:Kerberos Change Password Service:/var/empty:/usr/bin/false
_krb_kadmin:*:231:-2:Open Directory Kerberos Admin Service:/var/empty:/usr/bin/false
```
可以使用 `-i` 参数来忽略大小写，使用 `-r` 参数来遍历某个文件夹下的所有文件
```bash
$ grep -r admin /etc/
```

### h. `nl`
打印文本并在每行头部显示行数，-S参数可以指定行数后的一个分隔符

*example.txt*
```bash
Lorem ipsum
dolor sit amet,
consetetur
sadipscing elitr,
sed diam nonumy
eirmod tempor
invidunt ut labore
et dolore magna
aliquyam erat, sed
diam voluptua. At
vero eos et
accusam et justo
duo dolores et ea
rebum. Stet clita
kasd gubergren,
no sea takimata
sanctus est Lorem
ipsum dolor sit
amet.
```

*显示行数并用点'.'分隔*
```bash
nl -s "." example.txt 
```
```bash
     1. Lorem ipsum
     2. dolor sit amet,
     3. consetetur
     4. sadipscing elitr,
     5. sed diam nonumy
     6. eirmod tempor
     7. invidunt ut labore
     8. et dolore magna
     9. aliquyam erat, sed
    10. diam voluptua. At
    11. vero eos et
    12. accusam et justo
    13. duo dolores et ea
    14. rebum. Stet clita
    15. kasd gubergren,
    16. no sea takimata
    17. sanctus est Lorem
    18. ipsum dolor sit
    19. amet.
```

### i. `sed`
流式文本编辑器

*example.txt*
```bash
Hello This is a Test 1 2 3 4
``` 

*把所有空格替换成 " - "*
```bash
sed 's/ /-/g' example.txt
```
```bash
Hello-This-is-a-Test-1-2-3-4
```

*把所有数字替换成字母 "d"*
```bash
sed 's/[0-9]/d/g' example.txt
```
```bash
Hello This is a Test d d d d
```

### j. `sort`
给文本按行排序

*example.txt*
```bash
f
b
c
g
a
e
d
```

*sort example.txt*
```bash
sort example.txt
```
```bash
a
b
c
d
e
f
g
```

*对example.txt进行随机排序*
```bash
sort example.txt | sort -R
```
```bash
b
f
a
c
d
g
e
```

### k. `tr`
按模式将文本转换或替换

*example.txt*
```bash
Hello World Foo Bar Baz!
```

*把所有小写字母替换为大写字母*
```bash
cat example.txt | tr 'a-z' 'A-Z' 
```
```bash
HELLO WORLD FOO BAR BAZ!
```

*把所有空格替换为换行符*
```bash
cat example.txt | tr ' ' '\n'
```
```bash
Hello
World
Foo
Bar
Baz!
```

### l. `uniq`
去除文本中的重复行

*example.txt*
```bash
a
a
b
a
b
c
d
c
```

*先排序后去除重复行可以得到文本中唯一行结果*
```bash
sort example.txt | uniq
```
```bash
a
b
c
d
```

*-c参数可以显示出该行在文本中出现的次数*
```bash
sort example.txt | uniq -c
```
```bash
    3 a
    2 b
    2 c
    1 d
```

### m. `wc`
打印出一个文本有多少行、多少个单词、多少个字符
```bash
wc filename
```
Example:
```bash
$ wc demo.txt
7459   15915  398400 demo.txt
```
 `7459` 表示行数, `15915` 表示单词数 `398400` 表示字符数

## 1.3. 文件夹操作

<table>
   <tr>
      <td><a href="#a-cd">cd</a></td>
      <td><a href="#b-mkdir">mkdir</a></td>
      <td><a href="#c-pwd">pwd</a></td>
   </tr>
</table>

### a. `cd`
切换当前所在的目录 
```bash
$ cd
```

```bash
cd dirname
cd /var 
cd ~ #切换至当前用户目录
cd - #切换至上一个目录
```

### b. `mkdir`
创建文件夹
```bash
mkdir dirname
```

### c. `pwd`
显示当前所在目录的绝对路径 
```bash
pwd
```

## 1.4. SSH, 系统信息, 网络信息

<table>
   <tr>
      <td><a href="#a-bg">bg</a></td>
      <td><a href="#b-cal">cal</a></td>
      <td><a href="#c-date">date</a></td>
      <td><a href="#d-df">df</a></td>
      <td><a href="#e-dig">dig</a></td>
      <td><a href="#f-du">du</a></td>
      <td><a href="#g-fg">fg</a></td>
      <td><a href="#h-finger">finger</a></td>
      <td><a href="#i-kill">kill</a></td>
      <td><a href="#j-killall">killall</a></td>
   </tr>
   <tr>
      <td><a href="#k-last">last</a></td>
      <td><a href="#l-man">man</a></td>
      <td><a href="#m-passwd">passwd</a></td>
      <td><a href="#n-ping">ping</a></td>
      <td><a href="#o-ps">ps</a></td>
      <td><a href="#p-quota">quota</a></td>
      <td><a href="#q-scp">scp</a></td>
      <td><a href="#r-ssh">ssh</a></td>
      <td><a href="#s-top">top</a></td>
      <td><a href="#t-uname">uname</a></td>
   </tr>
   <tr>
      <td><a href="#u-uptime">uptime</a></td>
      <td><a href="#v-w">w</a></td>
      <td><a href="#w-wget">wget</a></td>
      <td><a href="#x-whoami">whoami</a></td>
      <td><a href="#y-whois">whois</a></td>
   </tr>
</table>

### a. `bg`
显示在后台运行的任务

### b. `cal`
显示当前系统日期

### c. `date`
显示当前系统日期和事件

### d. `df`
查看磁盘使用情况

### e. `dig`
查看DNS信息
```bash
dig domain
```

### f. `du`
查询文件或目录的磁盘使用空间  [命令详解](http://www.cnblogs.com/chijianqiang/archive/2011/05/09/2041592.html)
```bash
du [option] [filename|directory]
```

示例:
```bash
du -sh pictures
1.4M pictures
```

### g. `fg`
将某个作业放在前台运行

### h. `finger`
显示某个系统用户的信息
```bash
finger username
```

### i. `kill`
终止某个指定pid的进程 
```bash
kill PID
```

### j. `killall`
使用进程名字终止进程
```bash
killall processname
```

### k. `last`
显示某个账户最后一次登录信息
```bash
last yourUsername
```

### l. `man`
帮助手册, 不懂你就man一下
```bash
man command
```

### m. `passwd`
修改当前登录用户的密码

### n. `ping`
ping某个主机
```bash
ping host
```

### o. `ps`
查看系统进程
```bash
ps -u yourusername
```

### p. `quota`
显示磁盘使用情况和限额.  
```bash
quota -v
```

### q. `scp`
在本地主机和远程主机，或者两台远程主机之间传送文件

*本地传到远程*：
```bash
scp source_file user@host:directory/target_file
```
*远程传到本地*
```bash
scp user@host:directory/source_file target_file
scp -r user@host:directory/source_folder farget_folder
```
-p参数可以指定端口
```bash
scp -P port user@host:directory/source_file target_file
```

### r. `ssh`
远程连接一台主机
```bash
ssh user@host
```
-p参数可以指定端口
```bash
ssh -p port user@host
```

### s. `top`
显示当前系统活跃进程和cpu、内存使用情况

### t. `uname`
打印系统 kernel 信息
```bash
uname -a
```

### u. `uptime`
查看用户在线时间

### v. `w`
查看当前系统登录用户

### w. `wget`
文件下载工具
```bash
wget file
```

### x. `whoami`
查看当前登录用户的用户名

### y. `whois`
查看某个域名拥有者的信息
```bash
whois domain
```

# 2. 基础bash sheel脚本编程


在bash脚本的第一行要写上`#!/bin/bash`来告诉系统该脚本是bash脚本

这一行在Linux中被称为 `shebang`. 

```bash
#!/bin/bash
```

## 2.1. 变量

在bash脚本中声明变量与其他语言类似，而且不用声明变量的类型，直接赋值就可以生效，可以接受字符串、数字等变量类型

示例:
```bash
str="hello world"
```

上面这行代码创建了一个名为str的变量，并给它赋值为"hello world"

使用的时候在变量名前加上$进行调用

Example:
```bash
echo $str   # hello world
```
## 2.2. 数组
数组是一组数据的集合，在bash脚本中对数组的大小没有限制，

下标同样从0开始

下面示例的方法可以创建数组：

示例:
```bash
array[0] = val
array[1] = val
array[2] = val  #方式一
array=([2]=val [0]=val [1]=val) #方式二
array=(val val val)  #方式三
```
显示数组的第一个元素

```bash
${array[0]}
```

查看数组包含的个数

```bash
${#array[@]}
```

Bash 像如下示例支持三元运算操作

```bash
${varname:-word}    # 如果varname存在且不为null，则返回varname的值，否则返回word
${varname:=word}    # 如果varname存在且不为null，则返回varname的值，否则将word赋值给varname
${varname:+word}    # 如果varname存在且不为null，则返回word的值， 否则返回null
```

## 2.3 字符串操作



```bash
${variable#pattern}         # 如果变量内容从头开始的数据符合“pattern”，则将符合的最短数据删除
${variable##pattern}        # 如果变量内容从头开始的数据符合“pattern”，则将符合的最长数据删除
${variable%pattern}         # 如果变量内容从尾向前的数据符合“pattern”，则将符合的最短数据删除
${variable%%pattern}        # 如果变量内容从尾向前的数据符合“pattern”，则将符合的最长数据删除
${variable/pattern/string}  # 如果变量内容符合“pattern”，则第一个匹配的字符串会被string替换
${variable//pattern/string} # 如果变量内容符合“pattern”，则所有匹配的字符串会被string替换
${#varname}                 # 返回变量的长度
```

## 2.4. 函数/方法
与其他语言类似，方法是一组可复用操作的集合

```bash
functname() {
    shell commands
}
```

示例:
```bash
#!/bin/bash
function hello {
   echo world!
}
hello

function say {
    echo $1
}
say "hello world!"
```
当调用hello函数时，屏幕将输出"world"

当调用say函数时，将在屏幕输出传入的第一个参数，在上例中就是"hello world!"

## 2.5. 条件语句

与其他语言类似，也包含 if then else语句 和 case语句

```bash
if [ expression ]; then   # [] 与 expression之间要有空格
    will execute only if expression is true
else
    will execute if expression is false
fi
```

case语句:

```bash
case expression in
    pattern1 )
        statements ;;
    pattern2 )
        statements ;;
    ...
esac
```

基本比较符:

```bash
statement1 && statement2  # statement1为true并且 statement2为true 则返回true
statement1 || statement2  # 至少一个为true，则返回true

str1=str2       # 比较两个字符串是否相等
str1!=str2      # 比较两个字符串是否不等
-n str1         # 判断str1是否为 非null
-z str1         # 判断str1是否为 null

-a file         # file文件是否存在
-d file         # file是否是一个文件夹
-f file         # file文件是否是一个普通的非文件夹文件
-r file         # 是否有可读权限
-s file         # 是否存在文件并且文件内容不为空
-w file         # 是否有可写权限
-x file         # 是否有可执行权限
-N file         # 文件是否在最后一次读取时被修改
-O file         # 是否是文件的所有者
-G file         # 文件的所属组是否与你属于同一组

file1 -nt file2     # file1是否比file2新 （newer than）
file1 -ot file2     # file1是否比file2旧 （older than）

-lt     # 小于
-le     # 小于等于
-eq     # 等于
-ge     # 大于等于
-gt     # 大于
-ne     # 不等
```

## 2.6. 循环

支持三种循环语句. `for`， `while` ， `until`.

`for` 语句:
```bash
for x := 1 to 10 do
begin
  statements
end

for name [in list]
do
  statements that can use $name
done

for (( initialisation ; ending condition ; update ))
do
  statements...
done
```

`while` 语句:
```bash
while condition; do
  statements
done
```

`until` 语句:
```bash
until condition; do
  statements
done
```





# 3. 调试
有几个简单的调试命令可以在bash中使用
bash命令加上 -n 参数可以不执行脚本，只检查语法错误
bash命令加上 -v 参数可以在脚本执行前把脚本内容显示出来
bash命令加上 -x 参数可以在脚本执行过程中逐步显示执行的脚本内容

```bash
bash -n scriptname
bash -v scriptname
bash -x scriptname
```



## License

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)


