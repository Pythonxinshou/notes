目录 

1. linux 三剑客 grep、sed、awk

- 1.0 简介
- 1.1 grep
- 1.2 sed
- 1.3 awk

1. shell

- 2.1 Shell 脚本是什么
- 2.2 可以在 Shell 脚本中使用哪些类型的变量？
- 2.3 Shell 脚本中 `if` 语法如何嵌套?
- 2.4 Shell 脚本中 `case` 语句的语法?
- 2.5 Shell 脚本中 `for` 循环语法？
- 2.6 Shell 脚本中 `while` 循环语法？
- 2.7 Shell 脚本中 break 命令的作用？
- 2.8 Shell 脚本中 continue 命令的作用？
- 2.9 如何使脚本可执行?
- 2.10 如何调试 Shell脚本？
- 2.11 如何将标准输出和错误输出同时重定向到同一位置?
- 2.12 如何在 Shell 脚本如何定义函数呢？
- 2.13 如何执行算术运算？

1. 文件管理命令

- 3.1 cat 命令
- 3.2 chmod 命令
- 3.3 chown 命令
- 3.4 cp 命令
- 3.5 find 命令
- 3.6 head 命令
- 3.7 less 命令
- 3.8 ln 命令
- 3.9 locate 命令
- 3.10 more 命令
- 3.11 mv 命令
- 3.12 rm 命令
- 3.13 tail 命令
- 3.14 touch 命令
- 3.15 vim 命令
- 3.16 whereis 命令
- 3.17 which 命令

1. 文档编辑命令

- 4.1 grep 命令
- 4.2 wc 命令

1. 磁盘管理命令

- 5.1 cd 命令
- 5.2 df 命令
- 5.3 du 命令
- 5.4 ls命令
- 5.5 mkdir 命令
- 5.6 pwd 命令
- 5.7 rmdir 命令

1. 网络通讯命令

- 6.1 ifconfig 命令
- 6.2 iptables 命令
- 6.3 netstat 命令
- 6.4 ping 命令
- 6.5 telnet 命令

1. 系统管理命令

- 7.1 date 命令
- 7.2 free 命令
- 7.3 kill 命令
- 7.4 ps 命令
- 7.5 rpm 命令
- 7.6 top 命令
- 7.7  yum 命令

1. 备份压缩命令

- 8.1 bzip2 命令
- 8.2 gzip 命令
- 8.3 tar 命令
- 8.4 unzip 命令

**1. Linux 三剑客 grep / sed / awk**

### 1.0 简介

- Linux中最重要的三个命令在业界被称为“三剑客”，它们是awk,sed,grep。
- 我们现在知道Linux下一切皆文件，对Linux的操作就是对文件的处理，那么怎么能更好的处理文件呢？这就要用到我们上面的三剑客命令。
- grep擅长查找功能，sed擅长取行和替换。awk擅长取列。

### 1.1 grep

- grep: 过滤

```
grep [OPTIONS] PATTERN [FILE...]
--color=auto 对匹配到的文本着色显示
-v 显示不被pattern匹配到的行
-i 忽略字符大小写
-n 显示匹配的行号
-c 统计匹配的行数
-o 仅显示匹配到的字符串
-q 静默模式，不输出任何信息
-A # after, 后#行
-B # before, 前#行
-C # context, 前后各#行
-e 实现多个选项间的逻辑or关系
grep –e ‘cat ’ -e ‘dog’ file
-w 匹配整个单词
-E 使用ERE,相当于egrep
-F 相当于fgrep，不支持正则表达式
```

例：

1、包含root: grep -n root

![图片](https://mmbiz.qpic.cn/mmbiz_png/63ld15c6AC8RALTRotMHb5yweut5uEIaR6loykj7LsfkicPNQPegdoWZ9AaDibNJsB7JeduxNjagfuVKApPSBcsQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

2、不包含root: grep -nv root

![图片](https://mmbiz.qpic.cn/mmbiz_png/63ld15c6AC8RALTRotMHb5yweut5uEIayKz8bEomQ6Y8GiaP8yTwibx5hiaX1U4AQ1oUibEsLTR4jhKCAm490UK8ibw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

3、s开头: grep ^s

![图片](https://mmbiz.qpic.cn/mmbiz_png/63ld15c6AC8RALTRotMHb5yweut5uEIaJ9ssDbMNe2wUR3QGdZYvqHveeLjsBG2hJJ2RRdv8gfmBzCD9IGSNibg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

4、以n结尾: grep -n n$

![图片](https://mmbiz.qpic.cn/mmbiz_png/63ld15c6AC8RALTRotMHb5yweut5uEIa57MLm1QzmYibkDqC760Tjg7zJ03cO4YGFu3u7qnHPzOV1JZcnnYgxAQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

### 1.2 sed

- sed: 取行进行 打印、替换

```
sed [option]... 'script' inputfile
选项
-n 不输出模式空间内容到屏幕，即不自动打印
-e 多点编辑
-f /PATH/SCRIPT_FILE: 从指定文件中读取编辑脚本
-r 支持使用扩展正则表达式
-i 直接编辑文件
-i.bak 备份文件并原处编辑
script 地址定界
不给地址：对全文进行处理
单地址：
#: 指定的行，$：最后一行
/pattern/：被此处模式所能够匹配到的每一行
地址范围：
#,#
#,+#
/pat1/,/pat2/
`#,/pat1/
~：步进
1~2 奇数行
2~2 偶数行
编辑命令：
d 删除模式空间匹配的行，并立即启用下一轮循环
p 打印当前模式空间内容，追加到默认输出之后
a [\]text1 在指定行后面追加文本,支持使用\n实现多行追加
i [\]text 在行前面插入文本
c [\]text 替换行为单行或多行文本
w /path/somefile 保存模式匹配的行至指定文件
r /path/somefile 读取指定文件的文本至模式空间中匹配到的行后
= 为模式空间中的行打印行号
! 模式空间中匹配行取反处理
s///：查找替换,支持使用其它分隔符，s@@@，s###
替换标记：
g 行内全局替换
p 显示替换成功的行
w /PATH/TO/SOMEFILE 将替换成功的行保存至文件中
```

举例子：

1、打印第2行: sed -n 2p passwd

![图片](https://mmbiz.qpic.cn/mmbiz_png/63ld15c6AC8RALTRotMHb5yweut5uEIaV3I6k2lSpSSGIFN4E3w1Wr89ibzGxlW3CPcV7YMIVr6LaXIvdoNbglw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

2、打印2-5行: sed -n 2,5p passwd

![图片](https://mmbiz.qpic.cn/mmbiz_png/63ld15c6AC8RALTRotMHb5yweut5uEIaNYFH4ibib7dhq4V3WccCsx8UEDOZG8ste3Hrgzox4ZRLbkCSfWaszpvg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

3、root全替换abc: sed -i 's/root/abc/g' passwd

![图片](https://mmbiz.qpic.cn/mmbiz_png/63ld15c6AC8RALTRotMHb5yweut5uEIacGWUsqbbmK9yiaWF77iakt8jDP64fHBE82t0MLxhwqkfV15PzHmCZicCA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

- 直接修改读取的文件内容，而不是输出到终端。
- s ：取代，可以直接进行取代的工作。
- g: 是全局的意思。其中#是格式符，他也可以是@或者别的/。
- Sed替换格式是：sed -i ‘s/要替换的内容/替换成的内容/g' 文件名。

### 1.3 awk

- awk: 取列进行 打印

```
[root@debugresetreset54142x1 ~]# awk --help
Usage: awk [POSIX or GNU style options] -f 
progfile [--] file ...
Usage: awk [POSIX or GNU style options] 
[--] 'program' file ...
POSIX options:          GNU long options: (standard)
        -f progfile             --file=progfile
        -F fs                   --field-separator=fs
        -v var=val              --assign=var=val
Short options:          GNU long options: (extensions)
        -b                      --characters-as-bytes
        -c                      --traditional
        -C                      --copyright
        -d[file]                --dump-variables[=file]
        -e 'program-text'       --source='program-text'
        -E file                 --exec=file
        -g                      --gen-pot
        -h                      --help
        -L [fatal]              --lint[=fatal]
        -n                      --non-decimal-data
        -N                      --use-lc-numeric
        -O                      --optimize
        -p[file]                --profile[=file]
        -P                      --posix
        -r                      --re-interval
        -S                      --sandbox
        -t                      --lint-old
        -V                      --version
```

举例子：

1、打印文件第一列：

![图片](https://mmbiz.qpic.cn/mmbiz_png/63ld15c6AC8RALTRotMHb5yweut5uEIafEPmvvTrobHqib3WBHVMZH15w0HPDboicMFAAiaoXgEedAVnwzpo7MnDQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这里的分隔符是冒号 ，然后print打印第一列

2、输出字段1,3,6，以制表符作为分隔符

![图片](https://mmbiz.qpic.cn/mmbiz_png/63ld15c6AC8RALTRotMHb5yweut5uEIaNSwexKic2hIRgDFUHLZRHoplSluwOAm3icOhUraerJFDGSpm5icToiaKhA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

## 2. shell

### 2.1 Shell 脚本是什么

- 1个 Shell 脚本是一个文本文件，包含一个或多个命令。作为系统管理员，我们经常需要使用多个命令来完成一项任务，我们可以添加这些所有命令在一个文本文件(Shell 脚本)来完成这些日常工作任务。
- 什么是默认登录 Shell ？
- 在 Linux 操作系统，"/bin/bash" 是默认登录 Shell，是在创建用户时分配的。

### 2.2 可以在 Shell 脚本中使用哪些类型的变量？

在 Shell 脚本，我们可以使用两种类型的变量：

- 系统定义变量
- 系统变量是由系统系统自己创建的。这些变量通常由大写字母组成，可以通过 set 命令查看。
- 用户定义变量
- 用户变量由系统用户来生成和定义，变量的值可以通过命令 "echo $<变量名>" 查看。

------

在写一个 Shell 脚本时，如果你想要检查前一命令是否执行成功，在 if 条件中使用 $? 可以来检查前一命令的结束状态。

- 如果结束状态是 0 ，说明前一个命令执行成功。例如：

```
root@localhost:~## ls /usr/bin/shar
/usr/bin/shar
root@localhost:~## echo $?
0
```

- 如果结束状态不是0，说明命令执行失败。例如：

```
root@localhost:~## ls /usr/bin/share
ls: cannot access /usr/bin/share: No such file or directory
root@localhost:~## echo $?
2
```

### 2.3 Shell 脚本中 `if` 语法如何嵌套?

- if 语法

```
if [ 条件 ]
then
命令1
命令2
…..
else
if [ 条件 ]
then
命令1
命令2
….
else
命令1
命令2
…..
fi
fi
```

- 在 Shell 脚本中如何比较两个数字？
- 在 if-then 中使用测试命令（ -gt 等）来比较两个数字。例如：

```
#!/bin/bash
x=10
y=20
if [ $x -gt $y ]
then
echo “x is greater than y”
else
echo “y is greater than x”
fi
```

### 2.4 Shell 脚本中 `case` 语句的语法?

- 语法

```
case 变量 in
值1)
命令1
命令2
…..
最后命令
!!
值2)
命令1
命令2
……
最后命令
;;
esac
```

### 2.5 Shell 脚本中 `for` 循环语法？

- 语法

```
for 变量 in 循环列表
do
命令1
命令2
….
最后命令
done
```

### 2.6 Shell 脚本中 `while` 循环语法？

- 如同 for 循环，while 循环只要条件成立就重复它的命令块。
- 不同于 for循环，while 循环会不断迭代，直到它的条件不为真。
- 语法：

```
while [ 条件 ]
do
命令…
done
```

do-while 语句的基本格式？

do-while 语句类似于 while 语句，但检查条件语句之前先执行命令（LCTT 译注：意即至少执行一次。）。下面是用 do-while 语句的语法：

```
do
{
命令
} while (条件)
```

### 2.7 Shell 脚本中 break 命令的作用？

- break 命令一个简单的用途是退出执行中的循环。我们可以在 while 和 until 循环中使用 break 命令跳出循环。

### 2.8 Shell 脚本中 continue 命令的作用？

- continue 命令不同于 break 命令，它只跳出当前循环的迭代，而不是整个循环。continue 命令很多时候是很有用的，例如错误发生，但我们依然希望继续执行大循环的时候。

### 2.9 如何使脚本可执行?

- 使用 chmod 命令来使脚本可执行。例子如下：chmod a+x myscript.sh 。
- \#!/bin/bash 的作用？
- \#!/bin/bash 是 Shell 脚本的第一行，称为释伴（shebang）行。
- 这里 # 符号叫做 hash ，而 ! 叫做 bang。
- 它的意思是命令通过 /bin/bash 来执行。

### 2.10 如何调试 Shell脚本？

- 使用 -x' 数（sh -x myscript.sh）可以调试 Shell脚本。
- 另一个种方法是使用 -nv 参数(sh -nv myscript.sh)。

### 2.11 如何将标准输出和错误输出同时重定向到同一位置?

- 方法一：2>&1 (如## ls /usr/share/doc > out.txt 2>&1 ) 。
- 方法二：&> (如## ls /usr/share/doc &> out.txt ) 。

### 2.12 如何在 Shell 脚本如何定义函数呢？

- 函数是拥有名字的代码块。当我们定义代码块，我们就可以在我们的脚本调用函数名字，该块就会被执行。示例如下所示：

### 2.13 如何执行算术运算？

- 有两种方法来执行算术运算：
- 1、使用 expr 命令：## expr 5 + 2 。
- 2、用一个美元符号和方括号（表达式）：[16 + 4] ; test=$[16 + 4] 。

## 3. 文件管理命令

#### 3.1 cat 命令

cat 简介

- 1.一次显示整个文件:

```
cat filename
```

- 2.从键盘创建一个文件:

```
cat > filename
```

- 3.将几个文件合并为一个文件:

```
cat file1 file2 > file
```

#### 3.2 chmod 命令

chmod 简介

- Linux/Unix 的文件调用权限分为三级 : 文件拥有者、群组、其他。利用 chmod 可以控制文件如何被他人所调用。
- 用于改变 linux 系统文件或目录的访问权限。用它控制文件或目录的访问权限。该命令有两种用法。一种是包含字母和操作符表达式的文字设定法；另一种是包含数字的数字设定法。
- 每一文件或目录的访问权限都有三组，每组用三位表示，分别为文件属主的读、写和执行权限；与属主同组的用户的读、写和执行权限；系统中其他用户的读、写和执行权限。可使用 ls -l test.txt 查找。

------

chmod 权限说明：

```
-rw-r--r-- 1 root root 296K 11-13 06:03 log2012.log
```

- 第一列共有 10 个位置，第一个字符指定了文件类型。在通常意义上，一个目录也是一个文件。如果第一个字符是横线，表示是一个非目录的文件。如果是 d，表示是一个目录。从第二个字符开始到第十个 9 个字符，3 个字符一组，分别表示了 3 组用户对文件或者目录的权限。权限字符用横线代表空许可，r 代表只读，w 代表写，x 代表可执行。

------

chmod 常用参数：

```
-c 当发生改变时，报告处理信息
-R 处理指定目录以及其子目录下所有文件
```

chmod 权限范围：

```
u ：目录或者文件的当前的用户
g ：目录或者文件的当前的群组
o ：除了目录或者文件的当前用户或群组之外的用户或者群组
a ：所有的用户及群组
```

chmod 权限代号：

```
r ：读权限，用数字4表示
w ：写权限，用数字2表示
x ：执行权限，用数字1表示
- ：删除权限，用数字0表示
s ：特殊权限
```

------

chmod 实例：

- （1）所有用户可执行权限：a+x

```
chmod a+x t.log
```

- （2）撤销所有的权限 + 赋予可读权限：u=r

```
chmod u=r t.log 
```

- （3）属主分配(7)权限，所在组分配(5)，其他用户分配(1)

- - 7表示：读、写、执行
  - 5表示：读、执行
  - 1表示：执行

```
chmod 751 t.log -c（或者：chmod u=rwx,g=rx,o=x t.log)
```

#### 3.3 chown 命令

chown 简介

- chown 改为指定的 用户或组
- 用户可以是用户名或者用户 ID；
- 组可以是组名或者组 ID；
- 文件是以空格分开的要改变权限的文件列表，支持通配符。

```
-c 显示更改的部分的信息
-R 处理指定目录及子目录
```

------

实例：

- （1）改变拥有者和群组

```
chown -c mail:mail log2012.log
```

- （2）改变文件群组

```
chown -c :mail t.log
```

- （3）改变文件夹及子文件目录属主及属组为 mail

```
chown -cR mail: test/
```

#### 3.4 cp 命令

cp 简介

- 将源文件复制至目标文件，或将多个源文件复制至目标目录。
- 注意：命令行复制，如果目标文件已经存在会提示是否覆盖，而在 shell 脚本中，如果不加 -i 参数，则不会提示，而是直接覆盖！

```
-i 提示
-r 复制目录及目录内所有项目
-a 复制的文件与原文件时间一样
```

------

实例：

- （1）复制 a.txt 到 test 目录下，保持原文件时间，如果原文件存在提示是否覆盖。

```
cp -ai a.txt test
```

- （2）为 a.txt 建议一个链接（快捷方式）

```
cp -s a.txt link_a.txt
```

#### 3.5 find 命令

find 命令

- 用于在文件树中查找文件，并作出相应的处理。

命令格式：

```
find pathname -options [-print -exec -ok ...]
```

命令参数：

```
pathname: find命令所查找的目录路径。例如用.来表示当前目录，用/来表示系统根目录。
-print：find命令将匹配的文件输出到标准输出。
-exec：find命令对匹配的文件执行该参数所给出的shell命令。相应命令的形式为'command' {  } \;，注意{   }和\；之间的空格。
-ok： 和-exec的作用相同，只不过以一种更为安全的模式来执行该参数所给出的shell命令，在执行每一个命令之前，都会给出提示，让用户来确定是否执行。
```

命令选项：

```
-name 按照文件名查找文件
-perm 按文件权限查找文件
-user 按文件属主查找文件
-group  按照文件所属的组来查找文件。
-type  查找某一类型的文件，诸如：
   b - 块设备文件
   d - 目录
   c - 字符设备文件
   l - 符号链接文件
   p - 管道文件
   f - 普通文件
```

------

实例：

- （1）查找 48 小时内修改过的文件

```
find -atime -2
```

- （2）在当前目录查找 以 .log 结尾的文件。. 代表当前目录

```
find ./ -name '*.log'
```

- （3）查找 /opt 目录下 权限为 777 的文件

```
find /opt -perm 777
```

- （4）查找大于 1K 的文件

```
find -size +1000c
```

- （5）查找等于 1000 字符的文件

```
find -size 1000c 
```

#### 3.6 head 命令

- head 用来显示档案的开头至标准输出中，默认 head 命令打印其相应文件的开头 10 行。

常用参数：

```
-n<行数> 显示的行数（行数为复数表示从最后向前数）
```

------

实例：

- （1）显示 1.log 文件中前 20 行

```
head 1.log -n 20
```

- （2）显示 1.log 文件前 20 字节

```
head -c 20 log2014.log
```

- （3）显示 t.log最后 10 行

```
head -n -10 t.log
```

#### 3.7 less 命令

- less 与 more 类似，但使用 less 可以随意浏览文件，而 more 仅能向前移动，却不能向后移动，而且 less 在查看之前不会加载整个文件。

常用命令参数：

```
-i  忽略搜索时的大小写
-N  显示每行的行号
-o  <文件名> 将less 输出的内容在指定文件中保存起来
-s  显示连续空行为一行
/字符串：向下搜索“字符串”的功能
?字符串：向上搜索“字符串”的功能
n：重复前一个搜索（与 / 或 ? 有关）
N：反向重复前一个搜索（与 / 或 ? 有关）
-x <数字> 将“tab”键显示为规定的数字空格
b  向后翻一页
d  向后翻半页
h  显示帮助界面
Q  退出less 命令
u  向前滚动半页
y  向前滚动一行
空格键 滚动一行
回车键 滚动一页
[pagedown]： 向下翻动一页
[pageup]：   向上翻动一页
```

------

实例：

- （1）ps 查看进程信息并通过 less 分页显示

```
ps -aux | less -N
```

- （2）查看多个文件

```
less 1.log 2.log
```

#### 3.8 ln 命令

ln 命令

- 功能是为文件在另外一个位置建立一个同步的链接，当在不同目录需要该问题时，就不需要为每一个目录创建同样的文件，通过 ln 创建的链接（link）减少磁盘占用量。

链接分类

- 软件链接
- 硬链接

------

软链接

- 1.软链接，以路径的形式存在。类似于Windows操作系统中的快捷方式
- 2.软链接可以 跨文件系统 ，硬链接不可以
- 3.软链接可以对一个不存在的文件名进行链接
- 4.软链接可以对目录进行链接

------

硬链接

- 1.硬链接，以文件副本的形式存在。但不占用实际空间。
- 2.不允许给目录创建硬链接
- 3.硬链接只有在同一个文件系统中才能创建

------

常用参数：

- -b 删除，覆盖以前建立的链接
- -s 软链接（符号链接）
- -v 显示详细处理过程

实例：

- （1）给文件创建软链接，并显示操作信息

```
ln -sv source.log link.log
```

- （2）给文件创建硬链接，并显示操作信息

```
ln -v source.log link1.log
```

- （3）给目录创建软链接

```
ln -sv /opt/soft/test/test3 /opt/soft/test/test5
```

#### 3.9 locate 命令

- locate 与 find 命令相似，可以使用如 *、? 等进行正则匹配查找

常用参数：

```
-l num（要显示的行数）
-f   将特定的档案系统排除在外，如将proc排除在外
-r   使用正则运算式做为寻找条件
```

------

实例：

- （1）查找和 pwd 相关的所有文件(文件名中包含 pwd）

```
locate pwd
```

- （2）搜索 etc 目录下所有以 sh 开头的文件

```
locate /etc/sh
```

- （3）查找 /var 目录下，以 reason 结尾的文件

```
locate -r '^/var.*reason$'（其中.表示一个字符，*表示任务多个；.*表示任意多个字符）
```

#### 3.10 more 命令

- 功能类似于 cat, more 会以一页一页的显示方便使用者逐页阅读，而最基本的指令就是按空白键（space）就往下一页显示，按 b 键就会往回（back）一页显示。

命令参数：

```
+n      从笫 n 行开始显示
-n       定义屏幕大小为n行
+/pattern 在每个档案显示前搜寻该字串（pattern），然后从该字串前两行之后开始显示 
-c       从顶部清屏，然后显示
-d       提示“Press space to continue，’q’ to quit（按空格键继续，按q键退出）”，禁用响铃功能
-l        忽略Ctrl+l（换页）字符
-p       通过清除窗口而不是滚屏来对文件进行换页，与-c选项相似
-s       把连续的多个空行显示为一行
-u       把文件内容中的下画线去掉
```

常用操作命令：

```
Enter    向下 n 行，需要定义。默认为 1 行
Ctrl+F   向下滚动一屏
空格键  向下滚动一屏
Ctrl+B  返回上一屏
=       输出当前行的行号
:f     输出文件名和当前行的行号
V      调用vi编辑器
!命令   调用Shell，并执行命令
q       退出more
```

实例：

- （1）从第3行起显示

```
more +3 text.txt
```

- （2）在所列出文件目录详细信息，借助管道使每次显示 5 行

```
ls -l | more -5
```

#### 3.11 mv 命令

mv 命令

- 移动文件或修改文件名，根据第二参数类型（如目录，则移动文件；如为文件则重命令该文件）。
- 当第二个参数为目录时，第一个参数可以是多个以空格分隔的文件或目录，然后移动第一个参数指定的多个文件到第二个参数指定的目录中。

------

实例：

- （1）将文件 test.log 重命名为 test1.txt

```
mv test.log test1.txt
```

- （2）将文件 log1.txt,log2.txt,log3.txt 移动到根的 test3 目录中

```
mv llog1.txt log2.txt log3.txt /test3
```

- （3）将文件 file1 改名为 file2，如果 file2 已经存在，则询问是否覆盖

```
mv -i log1.txt log2.txt
```

- （4）移动当前文件夹下的所有文件到上一级目录

```
mv * ../
```

#### 3.12 rm 命令（万恶之源-多少程序员因为敲了它而跑路）

- 删除一个目录中的一个或多个文件或目录，如果没有使用 -r 选项，则 rm 不会删除目录。如果使用 rm 来删除文件，通常仍可以将该文件恢复原状。

```
rm [选项] 文件…
```

实例：

- （1）删除任何 .log 文件，删除前逐一询问确认：

```
rm -i *.log
```

- （2）删除 test 子目录及子目录中所有档案删除，并且不用一一确认：

```
rm -rf test
```

- （3）删除以 -f 开头的文件

```
rm -- -f*
```

#### 3.13 tail 命令

- 从文件末尾查看日志

常用参数：

```
-f 循环读取（常用于查看递增的日志文件）
-n<行数> 显示行数（从后向前）
```

例子

```
tail -f ping.log
```

#### 3.14 touch 命令

- Linux touch命令用于修改文件或者目录的时间属性，包括存取时间和更改时间。若文件不存在，系统会建立一个新的文件。
- ls -l 可以显示档案的时间记录。

语法

```
touch [-acfm][-d<日期时间>][-r<参考文件或目录>] [-t<日期时间>][--help][--version][文件或目录…]
```

参数说明：

```
a 改变档案的读取时间记录。
m 改变档案的修改时间记录。
c 假如目的档案不存在，不会建立新的档案。与 --no-create 的效果一样。
f 不使用，是为了与其他 unix 系统的相容性而保留。
r 使用参考档的时间记录，与 --file 的效果一样。
d 设定时间与日期，可以使用各种不同的格式。
t 设定档案的时间记录，格式与 date 指令相同。
–no-create 不会建立新档案。
–help 列出指令格式。
–version 列出版本讯息。
```

------

实例

- 使用指令"touch"修改文件"testfile"的时间属性为当前系统时间，输入如下命令：

```
$ touch testfile                #修改文件的时间属性 
```

- 首先，使用ls命令查看testfile文件的属性，如下所示：

```
$ ls -l testfile                #查看文件的时间属性  
#原来文件的修改时间为16:09  
-rw-r--r-- 1 hdd hdd 55 2011-08-22 16:09 testfile  
```

- 执行指令"touch"修改文件属性以后，并再次查看该文件的时间属性，如下所示：

```
$ touch testfile                #修改文件时间属性为当前系统时间  
$ ls -l testfile                #查看文件的时间属性  
#修改后文件的时间属性为当前系统时间  
-rw-r--r-- 1 hdd hdd 55 2011-08-22 19:53 testfile  
```

- 使用指令"touch"时，如果指定的文件不存在，则将创建一个新的空白文件。例如，在当前目录下，使用该指令创建一个空白文件"file"，输入如下命令：

```
$ touch file            #创建一个名为“file”的新的空白文件 
```

#### 3.15 vim 命令

Vim是从 vi 发展出来的一个文本编辑器。代码补完、编译及错误跳转等方便编程的功能特别丰富，在程序员中被广泛使用。

- 打开文件并跳到第 10 行：vim +10 filename.txt 。
- 打开文件跳到第一个匹配的行：vim +/search-term filename.txt 。
- 以只读模式打开文件：vim -R /etc/passwd 。
- 基本上 vi/vim 共分为三种模式，分别是命令模式（Command mode），输入模式（Insert mode）和底线命令模式（Last line mode）。

一图胜千言：

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

#### 3.16 whereis 命令

whereis 命令

- whereis 命令只能用于程序名的搜索，而且只搜索二进制文件（参数-b）、man说明文件（参数-m）和源代码文件（参数-s）。如果省略参数，则返回所有信息。whereis 及 locate 都是基于系统内建的数据库进行搜索，因此效率很高，而find则是遍历硬盘查找文件。

常用参数：

```
-b   定位可执行文件。
-m   定位帮助文件。
-s   定位源代码文件。
-u   搜索默认路径下除可执行文件、源代码文件、帮助文件以外的其它文件。
```

------

实例：

- （1）查找 locate 程序相关文件

```
whereis locate
```

- （2）查找 locate 的源码文件

```
whereis -s locate
```

- （3）查找 lcoate 的帮助文件

```
whereis -m locate
```

#### 3.17 which 命令

在 linux 要查找某个文件，但不知道放在哪里了，可以使用下面的一些命令来搜索：

```
which     查看可执行文件的位置。
whereis 查看文件的位置。
locate  配合数据库查看文件位置。
find        实际搜寻硬盘查询文件名称。
```

- which 是在 PATH 就是指定的路径中，搜索某个系统命令的位置，并返回第一个搜索结果。使用 which 命令，就可以看到某个系统命令是否存在，以及执行的到底是哪一个位置的命令。

常用参数：

```
-n  指定文件名长度，指定的长度必须大于或等于所有文件中最长的文件名。
```

------

实例：

- （1）查看 ls 命令是否存在，执行哪个

```
which ls
```

- （2）查看 which

```
which which
```

- （3）查看 cd

```
which cd（显示不存在，因为 cd 是内建命令，而 which 查找显示是 PATH 中的命令）
```

## 4. 文档编辑命令

#### 4.1 grep 命令

强大的文本搜索命令，grep

命令格式：

```
grep [option] pattern file|dir
```

常用参数：

```
-A n --after-context显示匹配字符后n行
-B n --before-context显示匹配字符前n行
-C n --context 显示匹配字符前后n行
-c --count 计算符合样式的列数
-i 忽略大小写
-l 只列出文件内容符合指定的样式的文件名称
-f 从文件中读取关键词
-n 显示匹配内容的所在文件中行数
-R 递归查找文件夹
```

------

grep 的规则表达式:

```
^  # 如：'^grep'匹配所有以grep开头的行。 
$  # 如：'grep$'匹配所有以grep结尾的行。 
.  # 如：'gr.p'匹配gr后接一个任意字符，然后是p。  
*  # 如：'*grep'匹配所有一个或多个空格后紧跟grep的行。
.*   # 任意字符。  
[]   #匹配指定字符，如'[Gg]rep'匹配Grep和grep。 
[^]  #匹配不在指定字符，如：'[^A-FH-Z]rep'匹配不包含A-R和T-Z的一个字母开头，紧跟rep的行。  
\(..\)  #标记匹配字符，如'\(love\)'，love被标记为1。   
\<      #锚定单词的开始，如:'\<grep'匹配包含以grep开头的单词的行。
\>      #锚定单词的结束，如'grep\>'匹配包含以grep结尾的单词的行。
x\{m\}  #重复字符x，m次，如：'0\{5\}'匹配包含5个o的行。 
x\{m,\}  #重复字符x,至少m次，如：'o\{5,\}'匹配至少有5个o的行。  
x\{m,n\}  #重复字符x，至少m次，不多于n次，如：'o\{5,10\}'匹配5--10个o的行。  
\w    #匹配文字和数字，如：'G\w*p'匹配以G后跟零个或多个文字或数字字符，然后是p。  
\W    #\w的反置形式，匹配一个或多个非单词字符，如点号句号等。  
\b    #单词锁定符，如: '\bgrep\b'只匹配grep。
```

------

实例：

- （1）查找指定进程

```
ps -ef | grep svn
```

- （2）查找指定进程个数

```
ps -ef | grep svn -c
```

- （3）从文件中读取关键词

```
cat test1.txt | grep -f key.log
```

- （4）从文件夹中递归查找以grep开头的行，并只列出文件

```
grep -lR '^grep' /tmp
```

- （5）查找非x开关的行内容

```
grep '^[^x]' test.txt
```

- （6）显示包含 ed 或者 at 字符的内容行

```
grep -E 'ed|at' test.txt
```

#### 4.2 wc 命令

wc(word count)功能为统计指定的文件中字节数、字数、行数，并将统计结果输出

命令格式：

```
wc [option] file..
```

命令参数：

```
-c 统计字节数
-l 统计行数
-m 统计字符数
-w 统计词数，一个字被定义为由空白、跳格或换行字符分隔的字符串
```

实例：

- （1）查找文件的 行数 单词数 字节数 文件名

```
wc text.txt

结果：

7     8     70     test.txt
```

- （2）统计输出结果的行数

```
cat test.txt | wc -l
```

## 5. 磁盘管理命令

#### 5.1 cd 命令

实例：

- （1）进入要目录

```
cd /
```

- （2）进入 “home” 目录

```
cd ~
```

- （3）进入上一次工作路径

```
cd -
```

- （4）把上个命令的参数作为cd参数使用。

```
cd !$
```

#### 5.2 df 命令

df 命令

- 显示磁盘空间使用情况。

```
-a 全部文件系统列表
-h 以方便阅读的方式显示信息
-i 显示inode信息
-k 区块为1024字节
-l 只显示本地磁盘
-T 列出文件系统类型
```

实例：

- （1）显示磁盘使用情况

```
df -l
```

- （2）以易读方式列出所有文件系统及其类型

```
df -haT
```

#### 5.3 du 命令

- du 命令也是查看使用空间的，但是与 df 命令不同的是 Linux du 命令是对文件和目录磁盘使用的空间的查看：

命令格式：

```
du [选项] [文件]
```

常用参数：

```
-a 显示目录中所有文件大小
-k 以KB为单位显示文件大小
-m 以MB为单位显示文件大小
-g 以GB为单位显示文件大小
-h 以易读方式显示文件大小
-s 仅显示总计
-c或--total  除了显示个别目录或文件的大小外，同时也显示所有目录或文件的总和
```

实例：

- （1）以易读方式显示文件夹内及子文件夹大小

```
du -h scf/
```

- （2）以易读方式显示文件夹内所有文件大小

```
du -ah scf/
```

- （3）显示几个文件或目录各自占用磁盘空间的大小，还统计它们的总和

```
du -hc test/ scf/
```

- （4）输出当前目录下各个子目录所使用的空间

```
du -hc --max-depth=1 scf/
```

#### 5.4 ls命令

- 就是 list 的缩写，通过 ls 命令不仅可以查看 linux 文件夹包含的文件，而且可以查看文件权限(包括目录、文件夹、文件权限)查看目录信息等等。

常用参数搭配：

```
ls -a 列出目录所有文件，包含以.开始的隐藏文件
ls -A 列出除.及..的其它文件
ls -r 反序排列
ls -t 以文件修改时间排序
ls -S 以文件大小排序
ls -h 以易读大小显示
ls -l 除了文件名之外，还将文件的权限、所有者、文件大小等信息详细列出来
```

实例：

- (1) 按易读方式按时间反序排序，并显示文件详细信息

```
ls -lhrt
```

- (2) 按大小反序显示文件详细信息

```
ls -lrS
```

- (3)列出当前目录中所有以"t"开头的目录的详细内容

```
ls -l t*
```

- (4) 列出文件绝对路径（不包含隐藏文件）

```
ls | sed "s:^:`pwd`/:"
```

- (5) 列出文件绝对路径（包含隐藏文件）

```
find $pwd -maxdepth 1 | xargs ls -ld
```

#### 5.5 mkdir 命令

mkdir 命令用于创建文件夹。

可用选项：

```
-m: 对新建目录设置存取权限，也可以用 chmod 命令设置;
-p: 可以是一个路径名称。此时若路径中的某些目录尚不存在,加上此选项后，系统将自动建立好那些尚不在的目录，即一次可以建立多个目录。
实例：
```

- （1）当前工作目录下创建名为 t的文件夹

```
mkdir t
```

- （2）在 tmp 目录下创建路径为 test/t1/t 的目录，若不存在，则创建：

```
mkdir -p /tmp/test/t1/t
```

#### 5.6 pwd 命令

pwd 命令用于查看当前工作目录路径。

实例：

- （1）查看当前路径

```
pwd
```

- （2）查看软链接的实际路径

```
pwd -P
```

#### 5.7 rmdir 命令

- 从一个目录中删除一个或多个子目录项，删除某目录时也必须具有对其父目录的写权限。
- 注意：不能删除非空目录

实例：

- 当 parent 子目录被删除后使它也成为空目录的话，则顺便一并删除：

```
rmdir -p parent/child/child11
```

## 6. 网络通讯命令

#### 6.1 ifconfig 命令

ifconfig 命令

- ifconfig 用于查看和配置 Linux 系统的网络接口。
- 查看所有网络接口及其状态：ifconfig -a 。
- 使用 up 和 down 命令启动或停止某个接口：ifconfig eth0 up 和 ifconfig eth0 down 。

#### 6.2 iptables 命令

iptables 命令

- iptables ，是一个配置 Linux 内核防火墙的命令行工具。功能非常强大，对于我们开发来说，主要掌握如何开放端口即可。例如：
- 把来源 IP 为 192.168.1.101 访问本机 80 端口的包直接拒绝：iptables -I INPUT -s 192.168.1.101 -p tcp --dport 80 -j REJECT 。
- 开启 80 端口，因为web对外都是这个端口

```
iptables -A INPUT -p tcp --dport 80 -j ACCEP
另外，要注意使用 iptables save 命令，进行保存。否则，服务器重启后，配置的规则将丢失。
```

#### 6.3 netstat 命令

netstat 命令

- Linux netstat命令用于显示网络状态。
- 利用netstat指令可让你得知整个Linux系统的网络情况。

语法

```
netstat [-acCeFghilMnNoprstuvVwx][-A<网络类型>][--ip]
```

参数说明：

```
-a或–all 显示所有连线中的Socket。
-A<网络类型>或–<网络类型> 列出该网络类型连线中的相关地址。
-c或–continuous 持续列出网络状态。
-C或–cache 显示路由器配置的快取信息。
-e或–extend 显示网络其他相关信息。
-F或–fib 显示FIB。
-g或–groups 显示多重广播功能群组组员名单。
-h或–help 在线帮助。
-i或–interfaces 显示网络界面信息表单。
-l或–listening 显示监控中的服务器的Socket。
-M或–masquerade 显示伪装的网络连线。
-n或–numeric 直接使用IP地址，而不通过域名服务器。
-N或–netlink或–symbolic 显示网络硬件外围设备的符号连接名称。
-o或–timers 显示计时器。
-p或–programs 显示正在使用Socket的程序识别码和程序名称。
-r或–route 显示Routing Table。
-s或–statistice 显示网络工作信息统计表。
-t或–tcp 显示TCP传输协议的连线状况。
-u或–udp 显示UDP传输协议的连线状况。
-v或–verbose 显示指令执行过程。
-V或–version 显示版本信息。
-w或–raw 显示RAW传输协议的连线状况。
-x或–unix 此参数的效果和指定"-A unix"参数相同。
–ip或–inet 此参数的效果和指定"-A inet"参数相同。
```

------

实例

- 如何查看系统都开启了哪些端口？

```
[root@centos6 ~ 13:20 #55]# netstat -lnp
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address               Foreign Address             State       PID/Program name
tcp        0      0 0.0.0.0:22                  0.0.0.0:*                   LISTEN      1035/sshd
tcp        0      0 :::22                       :::*                        LISTEN      1035/sshd
udp        0      0 0.0.0.0:68                  0.0.0.0:*                               931/dhclient
Active UNIX domain sockets (only servers)
Proto RefCnt Flags       Type       State         I-Node PID/Program name    Path
unix  2      [ ACC ]     STREAM     LISTENING     6825   1/init              @/com/ubuntu/upstart
unix  2      [ ACC ]     STREAM     LISTENING     8429   1003/dbus-daemon    /var/run/dbus/system_bus_socket
```

------

- 如何查看网络连接状况？

```
[root@centos6 ~ 13:22 #58]# netstat -an
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address               Foreign Address             State
tcp        0      0 0.0.0.0:22                  0.0.0.0:*                   LISTEN
tcp        0      0 192.168.147.130:22          192.168.147.1:23893         ESTABLISHED
tcp        0      0 :::22                       :::*                        LISTEN
udp        0      0 0.0.0.0:68                  0.0.0.0:*
```

------

- 如何统计系统当前进程连接数？

```
输入命令 netstat -an | grep ESTABLISHED | wc -l 。
输出结果 177 。一共有 177 连接数。
```

#### 6.4 ping 命令

ping 命令

- Linux ping命令用于检测主机。
- 执行ping指令会使用ICMP传输协议，发出要求回应的信息，若远端主机的网络功能没有问题，就会回应该信息，因而得知该主机运作正常。
- 指定接收包的次数

```
ping -c 2 www.baidu.com
```

#### 6.5 telnet 命令

telnet 命令

- Linux telnet命令用于远端登入。
- 执行telnet指令开启终端机阶段作业，并登入远端主机。

语法

```
telnet [-8acdEfFKLrx][-b<主机别名>][-e<脱离字符>][-k<域名>][-l<用户名称>][-n<记录文件>][-S<服务类型>][-X<认证形态>][主机名称或IP地址<通信端口>]
```

参数说明：

```
-8 允许使用8位字符资料，包括输入与输出。
-a 尝试自动登入远端系统。
-b<主机别名> 使用别名指定远端主机名称。
-c 不读取用户专属目录里的.telnetrc文件。
-d 启动排错模式。
-e<脱离字符> 设置脱离字符。
-E 滤除脱离字符。
-f 此参数的效果和指定"-F"参数相同。
-F 使用Kerberos V5认证时，加上此参数可把本地主机的认证数据上传到远端主机。
-k<域名> 使用Kerberos认证时，加上此参数让远端主机采用指定的领域名，而非该主机的域名。
-K 不自动登入远端主机。
-l<用户名称> 指定要登入远端主机的用户名称。
-L 允许输出8位字符资料。
-n<记录文件> 指定文件记录相关信息。
-r 使用类似rlogin指令的用户界面。
-S<服务类型> 设置telnet连线所需的IP TOS信息。
-x 假设主机有支持数据加密的功能，就使用它。
-X<认证形态> 关闭指定的认证形态。
```

------

实例

- 登录远程主机

```
# 登录IP为 192.168.0.5 的远程主机
telnet 192.168.0.5 
```

## 7. 系统管理命令

#### 7.1 date 命令

date 命令

- 显示或设定系统的日期与时间。

命令参数：

```
-d<字符串>  显示字符串所指的日期与时间。字符串前后必须加上双引号。
-s<字符串>  根据字符串来设置日期与时间。字符串前后必须加上双引号。
-u  显示GMT。
%H 小时(00-23)
%I 小时(00-12)
%M 分钟(以00-59来表示)
%s 总秒数。起算时间为1970-01-01 00:00:00 UTC。
%S 秒(以本地的惯用法来表示)
%a 星期的缩写。
%A 星期的完整名称。
%d 日期(以01-31来表示)。
%D 日期(含年月日)。
%m 月份(以01-12来表示)。
%y 年份(以00-99来表示)。
%Y 年份(以四位数来表示)。
```

------

实例：

- （1）显示下一天

```
date +%Y%m%d --date="+1 day"  //显示下一天的日期
```

- （2）-d参数使用

```
date -d "nov 22"  今年的 11 月 22 日是星期三
date -d '2 weeks' 2周后的日期
date -d 'next monday' (下周一的日期)
date -d next-day +%Y%m%d（明天的日期）或者：date -d tomorrow +%Y%m%d
date -d last-day +%Y%m%d(昨天的日期) 或者：date -d yesterday +%Y%m%d
date -d last-month +%Y%m(上个月是几月)
date -d next-month +%Y%m(下个月是几月)
```

#### 7.2 free 命令

free 命令

- 显示系统内存使用情况，包括物理内存、交互区内存(swap)和内核缓冲区内存。

命令参数：

```
-b 以Byte显示内存使用情况
-k 以kb为单位显示内存使用情况
-m 以mb为单位显示内存使用情况
-g 以gb为单位显示内存使用情况
-s<间隔秒数> 持续显示内存
-t 显示内存使用总合
```

实例：

- （1）显示内存使用情况

```
free
free -k
free -m
```

- （2）以总和的形式显示内存的使用信息

```
free -t
```

- （3）周期性查询内存使用情况

```
free -s 10
```

#### 7.3 kill 命令

kill 命令

- 如果任无法终止该程序可用"-KILL" 参数，
- SIGTERM（15）终止指定进程
- SIGKILL(9) 将强制结束进程
- root用户将影响用户的进程
- 非root用户只能影响自己的进程。

常用参数：

```
-l  信号，若果不加信号的编号参数，则使用“-l”参数会列出全部的信号名称
-a  当处理当前进程时，不限制命令名和进程号的对应关系
-p  指定kill 命令只打印相关进程的进程号，而不发送任何信号
-s  指定发送信号
-u  指定用户
```

实例：

- （1）先使用ps查找进程pro1，然后用kill杀掉

```
kill -9 $(ps -ef | grep pro1)
```

#### 7.4 ps 命令

ps 查看进程状态

- linux上进程有5种状态:
- 运行(正在运行或在运行队列中等待)
- 中断(休眠中, 受阻, 在等待某个条件的形成或接受到信号)
- 不可中断(收到信号不唤醒和不可运行, 进程必须等待直到有中断发生)
- 僵死(进程已终止, 但进程描述符存在, 直到父进程调用wait4()系统调用后释放)
- 停止(进程收到SIGSTOP, SIGSTP, SIGTIN, SIGTOU信号后停止运行运行)

5种状态码:

```
D 不可中断 uninterruptible sleep (usually IO)
R 运行 runnable (on run queue)
S 中断 sleeping
T 停止 traced or stopped
Z 僵死 a defunct (”zombie”) process
```

------

命令参数：

```
-A 显示所有进程
a 显示所有进程
-a 显示同一终端下所有进程
c 显示进程真实名称
e 显示环境变量
f 显示进程间的关系
r 显示当前终端运行的进程
-aux 显示所有包含其它使用的进程
```

------

实例：

- （1）显示当前所有进程环境变量及进程间关系

```
ps -ef
```

- （2）显示当前所有进程

```
ps -A
```

- （3）与grep联用查找某进程

```
ps -aux | grep apache
```

- （4）找出与 cron 与 syslog 这两个服务有关的 PID 号码

```
ps aux | grep '(cron|syslog)'
```

#### 7.5 rpm 命令

rpm 命令

- Linux rpm 命令用于管理套件。
- rpm(redhat package manager) 原本是 Red Hat Linux 发行版专门用来管理 Linux 各项套件的程序，由于它遵循 GPL 规则且功能强大方便，因而广受欢迎。逐渐受到其他发行版的采用。RPM 套件管理方式的出现，让 Linux 易于安装，升级，间接提升了 Linux 的适用度。

```
# 查看系统自带jdk
rpm -qa | grep jdk
# 删除系统自带jdk
rpm -e --nodeps 查看jdk显示的数据
# 安装jdk
rpm -ivh jdk-7u80-linux-x64.rpm
```

#### 7.6 top 命令

top 命令

- 显示当前系统正在执行的进程的相关信息，包括进程 ID、内存占用率、CPU 占用率等

常用参数：

```
-c 显示完整的进程命令
-s 保密模式
-p <进程号> 指定进程显示
-n <次数>循环显示次数
```

实例：

```
top - 14:06:23 up 70 days, 16:44,  2 users,  load average: 1.25, 1.32, 1.35
Tasks: 206 total,   1 running, 205 sleeping,   0 stopped,   0 zombie
Cpu(s):  5.9%us,  3.4%sy,  0.0%ni, 90.4%id,  0.0%wa,  0.0%hi,  0.2%si,  0.0%st
Mem:  32949016k total, 14411180k used, 18537836k free,   169884k buffers
Swap: 32764556k total,        0k used, 32764556k free,  3612636k cached
PID USER      PR  NI  VIRT  RES  SHR S %CPU %MEM    TIME+  COMMAND  
28894 root      22   0 1501m 405m  10m S 52.2  1.3   2534:16 java  
```

- 前五行是当前系统情况整体的统计信息区。
- 第一行，任务队列信息，同 uptime 命令的执行结果，具体参数说明情况如下：
- 14:06:23 — 当前系统时间
- up 70 days, 16:44 — 系统已经运行了70天16小时44分钟（在这期间系统没有重启过的）
- 2 users — 当前有2个用户登录系统
- load average: 1.15, 1.42, 1.44 — load average后面的三个数分别是1分钟、5分钟、15分钟的负载情况。
- load average数据是每隔5秒钟检查一次活跃的进程数，然后按特定算法计算出的数值。如果这个数除以逻辑CPU的数量，结果高于5的时候就表明系统在超负荷运转了。

------

- 第二行，Tasks — 任务（进程），具体信息说明如下：
- 系统现在共有206个进程，其中处于运行中的有1个，205个在休眠（sleep），stoped状态的有0个，zombie状态（僵尸）的有0个。

------

- 第三行，cpu状态信息，具体属性说明如下：

```
5.9%us — 用户空间占用CPU的百分比。
3.4% sy — 内核空间占用CPU的百分比。
0.0% ni — 改变过优先级的进程占用CPU的百分比
90.4% id — 空闲CPU百分比
0.0% wa — IO等待占用CPU的百分比
0.0% hi — 硬中断（Hardware IRQ）占用CPU的百分比
0.2% si — 软中断（Software Interrupts）占用CPU的百分比
```

- 备注：在这里CPU的使用比率和windows概念不同，需要理解linux系统用户空间和内核空间的相关知识！

------

- 第四行，内存状态，具体信息如下：

```
32949016k total — 物理内存总量（32GB）
14411180k used — 使用中的内存总量（14GB）
18537836k free — 空闲内存总量（18GB）
169884k buffers — 缓存的内存量 （169M）
```

------

- 第五行，swap交换分区信息，具体信息说明如下：

```
32764556k total — 交换区总量（32GB）
0k used — 使用的交换区总量（0K）
32764556k free — 空闲交换区总量（32GB）
3612636k cached — 缓冲的交换区总量（3.6GB）
```

------

- 第六行，空行。
- 第七行以下：各进程（任务）的状态监控，项目列信息说明如下：

```
PID — 进程id
USER — 进程所有者
PR — 进程优先级
NI — nice值。负值表示高优先级，正值表示低优先级
VIRT — 进程使用的虚拟内存总量，单位kb。VIRT=SWAP+RES
RES — 进程使用的、未被换出的物理内存大小，单位kb。RES=CODE+DATA
SHR — 共享内存大小，单位kb
S — 进程状态。D=不可中断的睡眠状态 R=运行 S=睡眠 T=跟踪/停止 Z=僵尸进程
%CPU — 上次更新到现在的CPU时间占用百分比
%MEM — 进程使用的物理内存百分比
TIME+ — 进程使用的CPU时间总计，单位1/100秒
COMMAND — 进程名称（命令名/命令行）
```

------

top 交互命令

```
h 显示top交互命令帮助信息
c 切换显示命令名称和完整命令行
m 以内存使用率排序
P 根据CPU使用百分比大小进行排序
T 根据时间/累计时间进行排序
W 将当前设置写入~/.toprc文件中
o或者O 改变显示项目的顺序
```

#### 7.7  yum 命令

yum 命令

- yum 前端软件包管理器。
- yum提供了查找、安装、删除某一个、一组甚至全部软件包的命令，而且命令简洁而又好记。

```
1.列出所有可更新的软件清单命令：yum check-update
2.更新所有软件命令：yum update
3.仅安装指定的软件命令：yum install <package_name>
4.仅更新指定的软件命令：yum update <package_name>
5.列出所有可安裝的软件清单命令：yum list
6.删除软件包命令：yum remove <package_name>
7.查找软件包 命令：yum search
8.清除缓存命令:
yum clean packages: 清除缓存目录下的软件包
yum clean headers: 清除缓存目录下的 headers
yum clean oldheaders: 清除缓存目录下旧的 headers
yum clean, yum clean all (= yum clean packages; yum clean oldheaders) :清除缓存目录下的软件包及旧的headers
实例
```

- 安装 pam-devel

```
[root@www ~]# yum install pam-devel
```

## 8. 备份压缩命令

#### 8.1 bzip2 命令

- 创建 *.bz2 压缩文件：bzip2 test.txt 。
- 解压 *.bz2 文件：bzip2 -d test.txt.bz2 。

#### 8.2 gzip 命令

gzip 命令

- 创建一个 *.gz 的压缩文件：gzip test.txt 。
- 解压 *.gz 文件：gzip -d test.txt.gz 。
- 显示压缩的比率：gzip -l *.gz 。

#### 8.3 tar 命令

tar 命令

- 用来压缩和解压文件。tar 本身不具有压缩功能，只具有打包功能，有关压缩及解压是调用其它的功能来完成。
- 弄清两个概念：打包和压缩。
- 打包是指将一大堆文件或目录变成一个总的文件；
- 压缩则是将一个大的文件通过一些压缩算法变成一个小文件

常用参数：

```
-c 建立新的压缩文件
-f 指定压缩文件
-r 添加文件到已经压缩文件包中
-u 添加改了和现有的文件到压缩包中
-x 从压缩包中抽取文件
-t 显示压缩文件中的内容
-z 支持gzip压缩
-j 支持bzip2压缩
-Z 支持compress解压文件
-v 显示操作过程
```

------

有关 gzip 及 bzip2 压缩:

gzip 实例：

- 压缩 gzip fileName .tar.gz 和.tgz
- 解压：gunzip filename.gz 或 gzip -d filename.gz 对应：
- tar zcvf filename.tar.gz
- tar zxvf filename.tar.gz

bz2实例：

- 压缩 bzip2 -z filename .tar.bz2
- 解压：bunzip filename.bz2或bzip -d filename.bz2 对应：
- tar jcvf filename.tar.gz
- tar jxvf filename.tar.bz2

------

实例：

- （1）将文件全部打包成 tar 包

```
tar -cvf log.tar 1.log,2.log 或tar -cvf log.*
```

- （2）将 /etc 下的所有文件及目录打包到指定目录，并使用 gz 压缩

```
tar -zcvf /tmp/etc.tar.gz /etc
```

- （3）查看刚打包的文件内容（一定加z，因为是使用 gzip 压缩的）

```
tar -ztvf /tmp/etc.tar.gz
```

- （4）要压缩打包 /home, /etc ，但不要 /home/dmtsai

```
tar --exclude /home/dmtsai -zcvf myfile.tar.gz /home/* /etc
```

#### 8.4 unzip 命令

unzip 命令

- 解压 *.zip 文件：unzip test.zip 。
- 查看 *.zip 文件的内容：unzip -l jasper.zip 。