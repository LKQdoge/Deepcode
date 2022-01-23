# Day 6

## Linux操作系统相关

+ 帮助命令

  + Man

    **命令名称：man**
    命令所在路径：/usr/bin/man
    **功能描述：获得帮助信息**
    **语法：man【命令】**（name显示命令是作用）
    **语法：man【配置文件】**（不需要写配置文件的绝对路径）

    ![在这里插入图片描述](https://img-blog.csdnimg.cn/2020080110164061.png)**按q退出，/搜索内容**

  + help

    **命令名称：help**
    命令所在路径：shell内置命令
    **功能描述：获得shell内置命令的帮助信息**
    **语法：help【命令】**

    ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200801102054292.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM2OTI2MDM3,size_16,color_FFFFFF,t_70)

    + info

      > 就内容来说，info页面比man page编写得要更好、更容易理解，也更友好，但man page使用起来确实要更容易得多。一个man page只有一页，而info页面几乎总是将它们的内容组织成多个区段(称为节点)，每个区段也可能包含子区段(称为子节点)。理解这个命令的窍门就是不仅要学习如何在单独的Info页面中浏览导航，还要学习如何在节点和子节点之间切换。

**语法info(选项)(参数)**

选项-d：添加包含info格式帮助文档的目录；

-f：指定要读取的info格式的帮助文档；

-n：指定首先访问的info帮助文件的节点；

-o：输出被选择的节点内容到指定文件。

**常用快捷键**

N键：显示(相对于本节点的)下一节点的文档内容。

P键：显示(相对于本节点的)前一节点的文档内容。

U键：进入当前命令所在的主题。

M键：敲M键后输入命令的名称就可以查看该命令的帮助文档了。

G键：敲G键后输入主题名称，进入该主题。

L键：回到上一个访问的页面。

SPACE键：向前滚动一页。

BACKUP或DEL键：向后滚动一页。

Q：退出info。



**在帮助窗口中：**

Ctrl-x 0 关闭帮助窗口

Ctrl-x Ctrl-c 关闭整个 Info

q 退出 info

n 打开与本 Node 关联的下一个 Node

p 打开与本 Node 关联的前一个 Node

u 打开与本 Node 关联的上一个 Node

l 回到上一次访问的 Node

m或g 选择一个菜单项(Node 的名字)

输入指定菜单的名字后按回车，打开指定菜单项关联的 Node

空格键 下一页(PageDown 也可以，下一页从当前页的最后两行开始算起)

下一个 Node (若当前页在 Node 文档的末尾)

Del 键 上一页(PageUp 也可以，上一页从当前页的开始两行开始算起)

上一个 Node (若当前页 Node 文档的开始)

b 或 t 或 Home 文档的开始(b 是 begining 的意思)

e 或 End 文档的末尾(b 是 ending 的意思)

Ctrl-l 刷新当前页，若当前文档显示情况有问题时

Ctrl-g 取消所键入的指令



+ 文件与目录相关操作

  + 目录的增删查改

    【 增 】mkdir新建一个新的目录：mkdir,该命令有可选参数，运用 mkdir -p可以一次构建对层目录；mkdir -m 可以给目录赋予权限；

    【 删 】 rmdir删除一个空的目录：rmdir，安全考虑下，目录的删除需要一层一层的删除，并且被包含的目录中不包含目录或者文件；rm -r 目录名 命令可以将目录下所有东西都删除

    【 改】cd切换目录：cd，Change Directory
    对于有执行权限的目录，都可以通过该命令切换进入该命令；

    【 查 】pwd显示当前目录：pwd，Print Working Directory,该命令会显示完整路径。

  + 目录或文件的复制

    >   文件与目录的复制使用同一个命令：cp(copy)；由于文件权限与文件所属用户和用户组挂钩，因此不同的用户执行复制命令会有不一样的效果。
    >     默认情况下，cp命令复制所得的目的文件或目录的所有者是命令操作者本身，而目的文件或目录的权限相对源文件也会有改变，通过该命令一些参数的使用，对这些改变可以实现一些控制，具体可总结为高级用户(eg:root)可以在复制的时候使用参数保留低级用户文件的所有属性，而低级用户拷贝高级用户的文件或目录时是文件的所有者和所有组信息不会改变，但是文件权限可以。
    >

cp [-adfilprsu] 		源文件或目录  						目的文件或目录 
cp [-adfilprsu] 		源文件1，源文件2，源文件3.....			目录
源文件有两个或两个以上，则目的文件一定要是目录才行

+ + 移除文件或目录

    rm [-fir] 文件或目录
    -f:忽略不存在的文件，不会出现警告信息；
    -i:在删除前会询问用户是否操作；
    -r:递归删除，常用在目录的删除；注意与rmdir相区分；

    若删除文件名带有短号“-”，则使用rm ./文件名或者是使用两个短号的形式：rm - - 文件名的形式；

  + 移动或更名文件或目录

    mv [-fiu]  原文件 目的文件：将原文件或目录改名为目的文件或目录
    mv [-fiu] 原文件 目录  ：将原文件移动到某一目录下；原文件可以是多个；
    -f:如果目标文件已存在，直接覆盖不询问；
    -i:目标文件存在，询问是否覆盖；
    -u:目标文件已存在且原文件比较新才会更新，
    也即是如果移动文件到目录下时已有该文件会根据两个文件的新旧来决定是否需要移动

  + 获取文件名或目录名

    basename 完整路径：获取文件名
    dirname  完整路径：获取目录名

  + 命令文件的存放路径查找

    在Linux系统中，一切命令也是文件，不同的版本可能拥有相同的命令但是命令文件的存放位置不同，在需要对命令文件进行修改时就可以利用以下命令查找具体命令的存放路径：

    which [-a] command :
    -a将所有由PATH目录中可以找到的命令均列出，没有该参数时，仅列出第一个被找到的命令名称。

  + 普通文件的存放路径查找

    文件的查找与命令文件的查找不同，主要使用以下几种命令:

    whereis [-bmsu] 文件或目录名
    locate [-ir] 关键字（可只使用文件的部分名称，类似模糊查询的概念）

    

    whereis 与locate两个查询命令查找Linux系统的一个数据库文件，该文件记录系统内的所有文件，其创建是默认每天执行一次，这两个查询命令查找该数据库文件，无需直接去硬盘中访问数据，速度很快，但是由于数据库文件的更新频率问题，如果系统中增删了某些文件，可能会造成查找结果的偏差。
    数据库文件的存放路径：/var/lib/mlocate
    解决数据库与磁盘不同步方案：利用updatedb命令手动更新数据库文件；

    find [PATH] [option][action]

    find查找命令可以实现很多更细致的查找但是由于find直接查找硬盘对于老旧的磁盘效率会比较低。
    find可以实现的细致查找：

    时间参数：-atime n,-ctime n,-mtime n,newer file;
    文件属性参数：-uid n;-gid n;-user name;-group name;-nouser;-nogroup;
    文件权限与名称参数：-name,-size [±]SIZE,-type,-perm mode,-perm -mode,-perm +mode;
    组合命令：-exec command {},可以对查找后的文件执行command命令，例如find / -perm +7000 -exec ls -l {} 找到某个文件并将其列出来；

    

+ 打包与压缩

  >   在具体总结各类压缩文件之前，首先要 弄清两个概念：打包和压缩。打包是指将一大堆文件或目录什么的变成一个总的文件，压缩则是将一个大的文件通过一些压缩算法变成一个小文件。为什么要区分这 两个概念呢？其实这源于Linux中的很多压缩程序只能针对一个文件进行压缩，这样当你想要压缩一大堆文件时，你就得先借助另外的工具将这一大堆文件先打 成一个包，然后再就原来的压缩程序进行压缩。

**打包**

+ tar
  	-c			打包
  	-v			显示操作过程
  	-f			指定文件名
  	-x			解包
  	-t			查看包里边文件内容
  	-r			添加文件到包里边
  	--get		从包里拿出指定的文件
  	--delete	删除包里边指定的文件
  	-C			指定解包目录
  	-cvf 		绝对路径	指定打包路径

+ 压缩和解压

  + zip

    zip -r xxx.tar.zip        压缩
    unzip xxx.tar.zip         解压

  + gzip

    gzip xxx.tar           压缩
    gunzip xxx.tar.gz      解压

    tar -zcvf xxx.tar.gz /xxx    打包压缩
    tar -zxvf xxx.tar.gz         解包解压

  + bzip2

    bzip2 xxx.tar         压缩
    bunzip2 xxx.tar.bz2   解压

    tar -jcvf xxx.tar.bz2 /xxx   打包压缩
    tar -jxvf xxx.tar.bz2        解包解压

+ vim文本编辑器

  vim编辑器分为三种主要模式：
  命令模式（编辑模式）：默认模式，移动光标，剪切/粘贴文本（界面表现：左下角显示文件名或为空）
  插入模式（输入模式）：修改文本（界面表现：左下角显示—INSERT–）插入模式下，按ESC按键返回命令模式
  末行模式（扩展模式）：保存、退出等（界面表现：左下角显示—VISUAL–）末行模式下连续按两次ESC按键返回末行模式

用vim打开文件用法:
例如:【vim abc.txt】打开abc.txt文件
例如：【vim +# abc.txt】打开abc.txt文件，光标定位在abc.txt文件的第#行
例如：【vim + abc.txt】打开abc.txt文件，光标定位在最后一行
例如：【vim +/PATTERN abc.txt】打开abc.txt文件，定位第一次被PATTERN(模式)匹配到的行的行首

模式之间的切换
注意：vim打开文件后，默认进入的模式为：命令模式：
命令模式下进入插入模式（输入模式）输入：【i】或者【o】或者【a】等
命令模式下进入末行模式（扩展模式）输入：【:】
使用vim编辑多个文件
【vim FILE1 FILE2 FILE3】可以同时编辑FILE1 FILE2 FILE3这三个文件
【:next】切换至下一个文件
【:prev】切换至前一个文件
【:last】切换至最后一个文件
【:first】切换至第一个文件



+ 用户权限管理

  + root用户与普通用户

    > root账号为系统的超级管理员账号，拥有最高级别的权限
    > administrator为普通账号，具体用户哪些权限要看账号分配了哪些权限，它只是一个叫做“管理员”的账号，跟其他普通账号并无区别，即linux中一个账号为administrator的用户可能并不是管理员，如果分配了一些权限，它也可以成为管理员，但永远没有root权限高。

+ + root 用户可以直接执行系统命令

    apt update

  + 非 root 用户，需要加一个 sudo 命令

    sudo apt update

  + 用户信息

    /etc/passwd

  +  用户密码

    /etc/shadow

  + 组信息

    /etc/group

  +  查看adduser下的所有命令

    man adduser

  + 查看当前用户

    whoami

+ 用户与用户组

  > Linux系统是一个多用户多任务的分时操作系统，任何一个要使用系统资源的用户，都必须首先向系统管理员申请一个账号，然后以这个账号的身份进入系统。
  >
  > 用户的账号一方面可以帮助系统管理员对使用系统的用户进行跟踪，并控制他们对系统资源的访问；另一方面也可以帮助用户组织文件，并为用户提供安全性保护。
  >
  > 每个用户账号都拥有一个唯一的用户名和各自的口令。
  >
  > 用户在登录时键入正确的用户名和口令后，就能够进入系统和自己的主目录。
  >
  > 实现用户账号的管理，要完成的工作主要有如下几个方面：
  >
  > - 用户账号的添加、删除与修改。
  > - 用户口令的管理。
  > - 用户组的管理。

+ home目录

  > **存放用户的主目录**。如果建立一个用户，用户名是“ji”,那么在/home目录下就有一个对应的/home/ji路径，用来存放用户的主目录。

+ 以管理员身份运行

  #### set uid

  设置使文件在执行阶段具有文件所有者的权限。典型的文件是 `/usr/bin/passwd` 如果一般用户执行该文件, 则在执行过程中, 该文件可以获得root权限, 从而可以更改用户的密码。

  #### set gid

  该权限只对目录有效. 目录被设置该位后, 任何用户在此目录下创建的文件都具有和该目录所属的组相同的组。

  #### sticky bit

  该位可以理解为防删除位。一个文件是否可以被某用户删除, 主要取决于该文件所属的组是否对该用户具有写权限。 如果没有写权限, 则这个目录下的所有文件都不能被删除, 同时也不能添加新的文件. 如果希望用户能够添加文件，但同时不能删除文件, 则可以对文件使用sticky bit位. 设置该位后, 就算用户对目录具有写权限, 也不能删除该文件。

**具体的操作方法**

操作这些标志与操作文件权限的命令是一样的, 都是 `chmod`。有两种方法来操作。

$ chmod u+s temp #为temp文件加上setuid标志. (setuid 只对文件有效)
$ chmod g+s tempdir #为tempdir目录加上setgid标志 (setgid 只对目录有效)
$ chmod o+t temp #为temp文件加上sticky标志 (sticky只对文件有效)

设置完成后，可以通过`ls -l`查看效果。

$ ls -l
rwsrw-r--   1 rousseau  staff   85 Sep 22  2017 test1   #表示有setuid标志
rwxrwsrw-   1 rousseau  staff   85 Sep 22  2017 test2   #表示有setgid标志
rwxrw-rwt   1 rousseau  staff   85 Sep 22  2017 test3   #表示有sticky标志
rwSr--r--   1 rousseau  staff   85 Sep 22  2017 test4



## 系统管理相关

+ 正则表达式

  > 正则表达式就是为处理大量的字符串而定义的一套规则和方法。 通过定义的这些特殊符号的辅助，系统管理员就可以快速过滤、替换或者输出需要的字符串。

+ 文本查找

  + grep(文件内容的过滤显示命令)

    常用选项参数：“-v”反向筛选出不含指定关键词的行；

    常用选项参数：“-i”以忽略大小写的方式来筛选；

    + find

      find：实时查找，精确匹配，速度略慢

      \#find  [options]  [查找路径]  [查找条件]  [处理动作]

      默认：查找路径：当前目录

      查找条件：查找指定路径下的所有文件

      处理动作：显示在标准输出上

    

+ 网络配置

  **ifconfig配置命令**

  　　`ifconfig`命令可以查看与配置网络状态。命令结果如下：

  ```
  eth0      Link encap:Ethernet  HWaddr 00:0C:29:11:30:39  
            inet addr:192.168.134.129  Bcast:192.168.134.255  Mask:255.255.255.0
            inet6 addr: fe80::20c:29ff:fe11:3039/64 Scope:Link
            UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
            RX packets:19731 errors:0 dropped:0 overruns:0 frame:0
            TX packets:502 errors:0 dropped:0 overruns:0 carrier:0
            collisions:0 txqueuelen:1000 
            RX bytes:1248492 (1.1 MiB)  TX bytes:58905 (57.5 KiB)
  
  lo        Link encap:Local Loopback  
            inet addr:127.0.0.1  Mask:255.0.0.0
            inet6 addr: ::1/128 Scope:Host
            UP LOOPBACK RUNNING  MTU:16436  Metric:1
            RX packets:0 errors:0 dropped:0 overruns:0 frame:0
            TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
            collisions:0 txqueuelen:0 
            RX bytes:0 (0.0 b)  TX bytes:0 (0.0 b)
  ```

  （`lo`表示本地回环网卡的信息）
  　　使用`ifconfig`命令还可以临时设置某一网卡的IP地址和子网掩码。如：

  ifconfig eth0 192.168.0.200 netmask 255.255.255.0



**配置文件**

*网卡信息文件*

　　查看第一张网卡的网卡信息：

vi /etc/sysconfig/network-scripts/ifcfg-eth0

信息如下：

```
DEVICE=eth0
HWADDR=00:0C:29:11:30:39
TYPE=Ethernet
UUID=5ab36190-a5df-4bf1-94d8-6c126afd05f1
ONBOOT=yes
NM_CONTROLLED=yes
BOOTPROTO=dhcp
```

*DNS配置文件*

　　查看DNS配置文件：

vi /etc/resolv.conf

内容如下：

```
; generated by /sbin/dhclient-script
search localdomain
nameserver 192.168.134.2
```



+ 磁盘管理

  > 磁盘是一种计算机的外部存储器设备，由一个或多个覆盖有磁性材料的铝制或玻璃制的碟片组成，用来存储用户的信息，这种信息可以反复地被读取和改写。绝大多数磁盘被永久封存在一个密封的盒子里。

**fdisk命令：查看系统的分区详细信息**

查看系统的分区详细信息：fdisk -l

**文件系统管理工具命令**

创建文件系统的工具:mkfs mkfs.ext2, mkfs.ext3, mkfs.ext4, mkfs.xfs, mkfs.vfat,

检测及修复文件系统的工具:fsck fsck.ext2, fsck.ext3, …

ext系列文件系统专用管理工具：mke2fs
语法结构：
mke2fs [OPTIONS] device
**e2label命令：卷标的查看与设定**
查看：e2label device
设定：e2label device LABEL

**tune2fs命令：查看或修改ext系列文件系统的某些属性**
语法结构：
tune2fs [OPTIONS] device
命令选项：
-l：查看超级块的内容；
修改指定文件系统的属性：
-j：ext2 --> ext3；
-L LABEL：修改卷标；
-m #：调整预留空间百分比；
注意：块大小创建后不可修改；

**dumpe2fs命令：显示ext系列文件系统的属性信息**
语法结构：
dumpe2fs [-h] device
resize2fs [选项] device [size]
调整ext2\ext3\ext4文件系统的大小
-f：强制执行

**e2fsck：磁盘修复 检查时先卸载**



## Sheel

> 常用的Shell：bash由 GNU 组织开发，sh 是 UNIX 上的标准 shell，是第一个流行的 Shell，bash保持了对 sh shell 的兼容性，是各种 Linux 发行版默认配置的 shell。现在sh 已经基本被 bash 代替，bash是sh的扩展补充，但是也有些是不兼容的，大多数情况下区别不大，特殊场景可以使用 bash 代替 sh。

+ 管道与重定向

  + I/O重定向

    ```
    <       将标准输入重定向到指定文件
    >       将标准输出重定向到指定文件，覆盖原内容
    >>      将标准输出重定向到指定文件，添加到末尾
    2>      将标准错误重定向到指定文件，覆盖原内容
    2>>     将标准错误重定向到指定文件，添加到末尾
    2>&1    将标准错误重定向到标准输出确定的文件
    &>      将标准输出和标准错误重定向到指定文件
    2> /dev/null    将标准错误重定向到/dev/null，起到隐藏命令错误信息的作用
        
    /dev/null 称为位桶(bit bucket)的系统设备，只接受输入但不对输入进行处理
    ```

+ 管道

  ```
  [ | ]      将命令的标准输出传送到另一个命令的标准输入中
  使用下面的命令可以起到过滤器的作用:
      	sort, uniq, wc, grep, head, tail, tee
  ```

  + 常用的管道命令

    1、cat: 合并文件
       (1) 读取一个或多个文件，并把他们复制到标准输出中
       (2) 重定向标准输出后，相当于合并文件
       (3) 不带参数时，，可以借此创建文本文件
    2、sort: 对文本行排序
    3、uniq: 报告或删除文件中重复的行(相邻的)
    	-d  只保留重复的行
    4、wc(word count): 打印文件中的换行符、字和字节的个数
    	-l  只输出行数
    5、grep: 打印匹配行
    	-i  忽略大小写
    	-v  输出不匹配的行
    6、head: 输出文件的前几行内容
    	-n  调整输出的行数
    7、tail: 输出文件的后几行内容
    	-n  调整输出的行数
    	-f  监控(实时查看)文件，当文件更新时显示文件变更，可用于跟踪日志文件的状态(root权限)
    8、tee: 读取标准输入的数据，并将其内容输出到标准输出和文件中
    	相当于创建管道的分，将一个输入同时输出到文件和标准输出



+ 进程和内存的查看与调整

  + 查看系统进程

    1、图形方式查看
    gnome-system-monitor

    2、进程查看命令
    ps -A ##所有进程
    -a ##在当前环境中运行的进程，不包含环境信息
    -u ##显示进程用户信息
    a ##在当前环境中运行的进程
    x ##列出系统中所有运行包含tty输出设备
    f ##显示进程的父子关系
    e ##显示进程的详细信息（系统资源的调用）

  + ps

    **ps aux ##显示系统中所有进程并显示进程用户**

    **ps ef ##显示进程详细信息并显示进程父子关系**

    **ps ax ##显示当前系统中的所有进程**

    **pstree ##显示当前系统的进程树**

  + top

  > VIRT：virtual memory usage 虚拟内存
  > 1、进程“需要的”虚拟内存大小，包括进程使用的库、代码、数据等
  > 2、假如进程申请100m的内存，但实际只使用了10m，那么它会增长100m，而不是实际的使用量
  >
  > RES：resident memory usage 常驻内存
  > 1、进程当前使用的内存大小，但不包括swap out
  > 2、包含其他进程的共享
  > 3、如果申请100m的内存，实际使用10m，它只增长10m，与VIRT相反
  > 4、关于库占用内存的情况，它只统计加载的库文件所占内存大小
  >
  > SHR：shared memory 共享内存
  > 1、除了自身进程的共享内存，也包括其他进程的共享内存
  > 2、虽然进程只使用了几个共享库的函数，但它包含了整个共享库的大小
  > 3、计算某个进程所占的物理内存大小公式：RES – SHR
  > 4、swap out后，它将会降下来
  >
  > DATA
  > 1、数据占用的内存。如果top没有显示，按f键可以显示出来。
  > 2、真正的该程序要求的数据空间，是真正在运行中要使用的。

top 运行中可以通过 top 的内部命令对进程的显示方式进行控制。内部命令如下：
s – 改变画面更新频率
l – 关闭或开启第一部分第一行 top 信息的表示
t – 关闭或开启第一部分第二行 Tasks 和第三行 Cpus 信息的表示
m – 关闭或开启第一部分第四行 Mem 和 第五行 Swap 信息的表示
N – 以 PID 的大小的顺序排列表示进程列表
P – 以 CPU 占用率大小的顺序排列进程列表
M – 以内存占用率大小的顺序排列进程列表
h – 显示帮助
n – 设置在进程列表所显示进程的数量
q – 退出 top
s – 改变画面更新周期

+ free

  > free 命令用来显示系统内存状态，包括系统物理内存、虚拟内存（swap 交换分区）、共享内存和系统缓存的使用情况，其输出和 top 命令的内存部分非常相似。

free 命令的基本格式如下：

[root@localhost ~]# free [选项]

**第一行显示的是各个列的列表头信息，各自的含义如下所示：**

- total 是总内存数；
- used 是已经使用的内存数；
- free 是空闲的内存数；
- shared 是多个进程共享的内存总数；
- buffers 是缓冲内存数；
- cached 是缓存内存数。



+ sar

  **sar命令常用格式**

  sar [options] [-A] [-o file] t [n]

  其中：

  t为采样间隔，n为采样次数，默认值是1；

  -o file表示将命令结果以二进制格式存放在文件中，file 是文件名。

  

  options 为命令行选项，sar命令常用选项如下：

  -A：所有报告的总和

  -u：输出CPU使用情况的统计信息

  -v：输出inode、文件和其他内核表的统计信息

  -d：输出每一个块设备的活动信息

  -r：输出内存和交换空间的统计信息

  -b：显示I/O和传送速率的统计信息

  -a：文件读写情况

  -c：输出进程统计信息，每秒创建的进程数

  -R：输出内存页面的统计信息

  -y：终端设备活动情况

  -w：输出系统交换活动信息





+ 变量与环境变量

  所有的应用程序和脚本都可以访问环境变量
  可以使用`env`或`printenv`命令查看当前shell中所定义的全部环境变量

  ```
  $> env
  PWD=/home/clif/ShellCookBook
  HOME=/home/clif
  SHELL=/bin/bash
  # ......
  ```

要查看其它进程的环境变量

```
cat /proc/$PID/environ
```

使用等号操作符为变量赋值，两边没有空格的等号是赋值操作符，加上空格的等号表示的是等量关系测试

```
varName=value # 如果value包含空白字符，需要将其放入引号中
```

在变量名之前加上美元符号（$）就可以访问变量的内容

```
var="value" # 将"value"赋给变量var
echo $var
echo ${var} # 使用花括号界定变量名
```

**可以在printf、echo或其它命令的双引号中引用变量值**

**环境变量是从父进程中继承而来的变量**

**export命令声明了将由子进程所继承的一个或多个变量**

**PATH变量列出了一系列可供shell搜索特定应用程序的目录**



+ 计划任务

  > 在Linux系统中，主要有两种执行计划任务的方式， 一种是仅**执行一次，**我们常用at来实现，另一种是执行一些周期性任务，我们使用crontab来实现 我们一般用at命令来执行需要定时执行的，一次性的这种任务，比如说，我需要在早晨7点的时候，重启我的nginx，首先，在终端输入at 7:00，之后输入systemctl restart nginx，然后按Ctrl+d来提交这个任务.