# Linux的目录结构
![image.png](https://cdn.nlark.com/yuque/0/2021/png/21907867/1630313358769-837973a4-dc8e-41d9-b992-3a11558906d1.png#clientId=u8e647d4e-3c02-4&from=paste&id=u1ab189cf&originHeight=75&originWidth=720&originalType=url&ratio=1&rotation=0&showTitle=false&size=60165&status=done&style=none&taskId=u2eb15eae-cbdf-4e51-a390-cce0675bab4&title=)

- bin (binaries)存放二进制可执行文件
- sbin (super user binaries)存放二进制可执行文件，只有root才能访问
- etc (etcetera)存放系统配置文件
- usr (unix shared resources)用于存放共享的系统资源
- home 存放用户文件的根目录
- root 超级用户目录
- dev (devices)用于存放设备文件
- lib (library)存放跟文件系统中的程序运行所需要的共享库及内核模块
- mnt (mount)系统管理员安装临时文件系统的安装点
- boot 存放用于系统引导时使用的各种文件
- tmp (temporary)用于存放各种临时文件
- var (variable)用于存放运行时需要改变数据的文件
# 网络连接的三种模式
1、桥接模式：虚拟系统与外部系统使用同一个网段，在网络上处于同等低位，虚拟系统可以与外部系统进行通讯，但是容易造成IP冲突<br />2、NAT模式：虚拟系统使用与主机不同的网段，并且在主机上映射再映射一个IP。可以与外部网络系统通讯，并且不会造成IP冲突<br />3、仅主机模式<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/21907867/1630073962612-20a04138-67a0-48df-9060-60468e90f1e1.png#clientId=uae0aeee4-3be9-4&from=paste&height=302&id=uc16f4093&originHeight=603&originWidth=1211&originalType=binary&ratio=1&rotation=0&showTitle=false&size=310190&status=done&style=none&taskId=ud72d3d42-2f22-41e8-a334-a3a34de618a&title=&width=605.5)
# 文件管理
## 绝对路径和相对路径
Linux的目录结构为树状结构，最顶级的目录为根目录 /。<br />其他目录通过挂载可以将它们添加到树中，通过解除挂载可以移除它们。<br />**绝对路径：**<br />路径的写法，由根目录 / 写起，例如：/usr/share/doc 这个目录。<br />**相对路径：**<br />路径的写法，不是由 / 写起，例如由 /usr/share/doc 要到 /usr/share/man 底下时，可以写成：cd ../man 
## 处理目录的常用命令

- ls: 列出目录
- cd：切换目录
- pwd：显示目前的目录
- mkdir：创建一个新的目录
- cp: 复制文件或目录
- rm: 移除文件或目录
- mv: 移动文件与目录，或修改文件与目录的名称

你可以使用 _man [命令]_ 来查看各个命令的使用文档，如 ：man cp。
# 文件内容查看
Linux系统中使用以下命令来查看文件的内容：

- cat 由第一行开始显示文件内容
- tac 从最后一行开始显示，可以看出 tac 是 cat 的倒着写！
- nl  显示的时候，顺道输出行号！
- more 一页一页的显示文件内容
- less 与 more 类似，但是比 more 更好的是，他可以往前翻页！
- head 只看头几行
- tail 只看尾巴几行
- echo命令 输出字符串或提取Shell变量的值

# 文件属性
在Linux中，权限显示出来的第一个字符代表的含义：

- 当为[ **d** ]则是目录
- 当为[ **-** ]则是文件；
- 若是[ **l** ]则表示为链接文档 ( link file )；
- 若是[ **b** ]则表示为装置文件里面的可供储存的接口设备 ( 可随机存取装置 )；
- 若是[ **c** ]则表示为装置文件里面的串行端口设备，例如键盘、鼠标 ( 一次性读取装置 )。
```shell
[root@localhost ~]# ll
total 8
-rw-------. 1 root root 2775 Nov 11  2020 anaconda-ks.cfg
drwxr-xr-x. 2 root root   80 Jan 21  2021 backup
drwxr-xr-x. 2 root root    6 Jul 22 19:20 Desktop
drwxr-xr-x. 2 root root    6 Jul 22 19:20 Documents
drwxr-xr-x. 2 root root    6 Jul 22 19:20 Downloads
drwxr-xr-x. 2 root root    6 Jul 22 19:20 Music
-rw-------. 1 root root 2055 Nov 11  2020 original-ks.cfg
drwxr-xr-x. 2 root root    6 Jul 22 19:20 Pictures
drwxr-xr-x. 2 root root    6 Jul 22 19:20 Public
drwxr-xr-x. 2 root root    6 Jul 22 19:20 Templates
drwxr-xr-x. 2 root root    6 Jul 22 19:20 Videos

```

接下来的字符中，以三个为一组，且均为『rwx』 的三个参数的组合。<br />其中，[ r ]代表可读(read)、[ w ]代表可写(write)、[ x ]代表可执行(execute)。<br />要注意的是，这三个权限的位置不会改变，如果没有权限，就会出现减号[ - ]

![image.png](https://cdn.nlark.com/yuque/0/2021/png/21907867/1630314722955-61812165-6550-4c58-96f9-f25c3829d758.png#clientId=u8e647d4e-3c02-4&from=paste&id=u4b6fdb4a&originHeight=275&originWidth=678&originalType=url&ratio=1&rotation=0&showTitle=false&size=113495&status=done&style=none&taskId=ubb50bcb6-3cea-4a60-90cd-3217a9d75aa&title=)

每个文件针对每类访问者定义了三种主要权限<br />r：Read 读<br />w：Write 写<br />x：execute 执行<br />X：针对目录加执行权限，文件不加执行权限（因文件具备执行权限有安全隐患）<br />注意：root账户不受文件权限的读写限制，执行权限受限制<br />**对于文件和目录来说，r，w，x有着不同的作用和含义：**<br />**针对文件：**<br /> r：读取文件内容 <br />w：修改文件内容 <br />x：执行权限对除二进制程序以外的文件没什么意义<br />**针对目录：目录本质可看做是存放文件列表、节点号等内容的文件**<br />r：查看目录下的文件列表<br />w：删除和创建目录下的文件 <br />x：可以cd进入目录，能查看目录中文件的详细属性，能访问目录下文件内容（基础权限）<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/21907867/1630315066750-ca873449-f45d-42af-9027-685ee7d31a5c.png#clientId=u8e647d4e-3c02-4&from=paste&id=u616e2f0f&originHeight=226&originWidth=1293&originalType=url&ratio=1&rotation=0&showTitle=false&size=71245&status=done&style=none&taskId=uf4d38824-2fbd-4016-b33e-4095804bc40&title=)<br />用户获取文件权限的顺序： 先看是否为所有者，如果是，则后面权限不看；再看是否为所属组，如果是，则后面权限不看。<br />每种身份(owner/group/others)各自的三个权限(r/w/x)分数是需要累加的，例如当权限为：[-rwxrwx---] 分数则是：

- owner = rwx = 4+2+1 = 7
- group = rwx = 4+2+1 = 7
- others= --- = 0+0+0 = 0

`chmod 770 filename`
## 文件属性常用命令
**1、chgrp：更改文件属组**<br />chgrp是英语单词“change group”的缩写，命令的作用和其中文释义一样，为用于变更文件或目录的所属群组。<br />**语法格式: **chgrp [参数] [目录]<br />**常用参数： **

| -c | 效果类似”-v”参数，但仅回报更改的部分 |
| --- | --- |
| -f | 不显示错误信息 |
| -h | 对符号连接的文件作修改，而不更动其他任何相关文件 |
| -R | 递归处理，将指定目录下的所有文件及子目录一并处理 |
| -v | 显示指令执行过程 |
| --reference | 把指定文件或目录的所属群组全部设成和参考文件或目录的所属群组相同 |

**2、chown：更改文件属主，也可以同时更改文件属组**<br />Linux/Unix 属于多用户多任务操作系统，所有的文件皆有拥有者。利用 chown 命令可以将指定文件的拥有者改为指定的用户或组，用户可以是用户名或者用户ID，组可以是组名或者组ID，文件是以空格分开的要改变权限的文件列表，支持通配符。 一般来说，这个指令仅限系统管理者(root)所使用，普通用户没有权限改变文件所属者及所属组。<br />**语法格式：**chown [参数]<br />**常用参数：**

| -R | 对目前目录下的所有文件与子目录进行相同的拥有者变更 |
| --- | --- |
| -c | 若该文件拥有者确实已经更改，才显示其更改动作 |
| -f | 若该文件拥有者无法被更改也不要显示错误讯息 |
| -h | 只对于连结(link)进行变更，而非该 link 真正指向的文件 |
| -v | 显示拥有者变更的详细资料 |
| --help | 显示辅助说明 |
| --version | 显示版本 |

**3、chmod：更改文件9个属性**<br />chmod命令的英文原意是“change the permissions mode of a file”，我们简称为“change mode”，意为用来改变文件或目录权限的命令，但是只有文件的属主和超级用户root才能执行这个命令。有两种模式，一种是采用权限字母和操作符表达式；另一种是采用数字。<br />**语法格式：** chmod [参数] [文件]<br />**常用参数：**

| -c | 若该文件权限确实已经更改，才显示其更改动作 |
| --- | --- |
| -f | 若该文件权限无法被更改也不显示错误讯息 |
| -v | 显示权限变更的详细资料 |
| -R | 对目前目录下的所有文件与子目录进行相同的权限变更(即以递回的方式逐个变更) |

# 账号管理
Linux系统是一个多用户多任务的分时操作系统，任何一个要使用系统资源的用户，都必须首先向系统管理员申请一个账号，然后以这个账号的身份进入系统。<br />用户的账号一方面可以帮助系统管理员对使用系统的用户进行跟踪，并控制他们对系统资源的访问；另一方面也可以帮助用户组织文件，并为用户提供安全性保护。<br />每个用户账号都拥有一个唯一的用户名和各自的口令。<br />用户在登录时键入正确的用户名和口令后，就能够进入系统和自己的主目录。<br />实现用户账号的管理，要完成的工作主要有如下几个方面：

- 用户账号的添加、删除与修改。
- 用户口令的管理。
- 用户组的管理。
## 用户账号的管理
用户账号的管理工作主要涉及到用户账号的添加、修改和删除。<br />添加用户账号就是在系统中创建一个新账号，然后为新账号分配用户号、用户组、主目录和登录Shell等资源。
## 添加账号 useradd
useradd命令用来创建新的用户或更改用户的信息。<br />useradd可用来建立用户帐号。帐号建好之后，再用passwd设定帐号的密码。使用useradd指令所建立的帐号，实际上是保存在/etc/passwd文本文件中。<br />**语法格式：**useradd [参数] [用户名]<br />**常用参数：**

| -D | 改变新建用户的预设值 |
| --- | --- |
| -c | 添加备注文字 |
| -d | 新用户每次登陆时所使用的家目录 |
| -e | 用户终止日期，日期的格式为YYYY-MM-DD |
| -f | 用户过期几日后永久停权。当值为0时用户立即被停权，而值为-1时则关闭此功能，预设值为-1 |
| -g | 指定用户对应的用户组 |
| -G | 定义此用户为多个不同组的成员 |
| -m | 用户目录不存在时则自动创建 |
| -M | 不建立用户家目录，优先于/etc/login.defs文件设定 |
| -n | 取消建立以用户名称为名的群组 |
| -r | 建立系统帐号 |
| -u | 指定用户id |

## 切换用户 su
su命令用于切换当前用户身份到指定用户或者以指定用户的身份执行命令或程序。<br />普通用户切换到root用户，可以使用su -- 或su root,但是必须输入root密码才能完成切换。root用户切换到普通用户，可以使用su username,不需要输入任何密码即可完成切换。<br />**语法格式: **su [选项] [用户名]<br />**常用参数：**

| -c或--command | 执行完指定的指令后，即恢复原来的身份 |
| --- | --- |
| -f或--fast | 适用于csh与tsch，使shell不用去读取启动文件 |
| -l或--login | 改变身份时，也同时变更工作目录，以及HOME,SHELL,USER,logname,此外，也会变更PATH变量 |
| -m,-p或--preserve-environment | 变更身份时，不要变更环境变量 |
| -s或--shell | 指定要执行的shell |
| --help | 显示帮助信息 |
| --version | 显示版本信息 |

## 删除用户 userdel
userdel命令用于删除指定的用户及与该用户相关的文件，英文全称即“user delete”。其实userdel命令实际上是修改了系统的用户账号文件 /etc/passwd、/etc/shadow以及/etc/group文件。这与Linux系统”一切操作皆文件”的思想正好吻合。<br />值得注意的是，但是如果有该要删除用户相关的进程正在运行，userdel命令通常不会删除一个用户账号。如果确实必须要删除，可以先终止用户进程，然后再执行userdel命令进行删除。但是userdel命令也提供了一个面对该种情况的参数，即”-f”选项。<br />**语法格式：**userdel [参数] [用户名]<br />**常用参数：**

| -f | 强制删除用户账号 |
| --- | --- |
| -r | 删除用户主目录及其中的任何文件 |
| -h | 显示命令的帮助信息 |

## 修改用户	usermod
usermod命令用于修改用户账号 。usermod可用来修改用户账号的各项设定，修改系统账号文件来反映通过命令行指定的变化。<br />**语法格式：**usermod [参数]<br />**常用参数：**

| -c<备注> | 修改用户账号的备注文字 |
| --- | --- |
| -d<登入目录> | 修改用户登入时的目录 |
| -e<有效期限> | 修改账号的有效期限 |
| -f<缓冲天数> | 修改在密码过期后多少天即关闭该账号 |
| -g<群组> | 修改用户所属的群组 |
| -G<群组> | 修改用户所属的附加群组 |
| -l<账号名称> | 修改用户账号名称 |
| -L | 锁定用户密码，使密码无效 |
| -s<shell> | 修改用户登入后所使用的shell |
| -u<uid> | 修改用户ID |
| -U | 解除密码锁定 |

## 修改用户账户密码 passwd	
passwd命令用于设置用户的认证信息，包括用户密码、账户锁定、密码失效等。直接运行passwd命令修改当前的用户密码，对其他用户的密码操作需要管理员权限。<br />**常用格式：**passwd [参数]<br />**常用参数：**

| -d | 删除密码 |
| --- | --- |
| -l | 锁定用户密码，无法被用户自行修改 |
| -u | 解开已锁定用户密码，允许用户自行修改 |
| -e | 密码立即过期，下次登陆强制修改密码 |
| -k | 保留即将过期的用户在期满后能仍能使用 |
| -S | 查询密码状态 |

# 用户组管理
## 新建用户组 groupadd
groupadd命令用于创建一个新的工作组，新工作组的信息将被添加到系统文件中。<br />**语法格式：**groupadd [参数]<br />**常用参数：**

| -g | 指定新建工作组的id |
| --- | --- |
| -r | 创建系统工作组，系统工作组的组ID小于500 |
| -K | 覆盖配置文件“/ect/login.defs” |
| -o | 允许添加组ID号不唯一的工作组 |

## 删除用户组 groupdel
groupdel命令用于删除指定的工作组，本命令要修改的系统文件包括/ect/group和/ect/gshadow。<br />userdel修改系统账户文件，删除与 GROUP 相关的所有项目。给出的组名必须存在。若该群组中仍包括某些用户，则必须先删除这些用户后，方能删除群组。<br />**语法格式**：groupdel [参数] [群组名称]<br />**常用参数**：

| -h | 显示帮助信息 |
| --- | --- |
| -R | 在chroot_dir目录中应用更改并使用chroot_dir目录中的配置文件 |

通过查看/etc/group配置文件里面不存在linuxcool组，说明已经被删除了。
```shell
[root@linuxcool ~]# more /etc/group|grep linuxcool
```
## 修改用户组 groupmod
groupmod命令用于更改群组的识别码或名称时。不过大家还是要注意，用户名不要随意修改，组名和 GID 也不要随意修改，因为非常容易导致管理员逻辑混乱。如果非要修改用户名或组名，则建议大家先删除旧的，再建立新的。<br />**语法格式：**groupmod [参数]<br />**常用参数：**

| -g | 设置欲使用的群组识别码 |
| --- | --- |
| -o  | 重复使用群组识别码 |
| -n | 设置欲使用的群组名称 |

## 切换用户组 newgrp
newgrp命令类的英文全称为“new group”,该命令类似login指令，当它是以相同的帐号，另一个群组名称，再次登入系统。欲使用newgrp指令切换群组，您必须是该群组的用户，否则将无法登入指定的群组。<br />单一用户要同时隶属多个群组，需利用交替用户的设置。若不指定群组名称，则newgrp指令会登入该用户名称的预设群组。<br />**语法格式：**newgrp [参数]<br />**常用参数：**

| --help | 在线帮助 |
| --- | --- |
| --vesion | 显示版本信息 |

# 磁盘管理 
Linux磁盘管理常用命令为 df、du。

- df ：显示磁盘空间使用情况
- du：查看磁盘占用空间
- fdisk：磁盘分区
- lsblk：查看系统的磁盘
- mount：文件系统挂载

## 显示磁盘空间使用情况 df
df命令的英文全称即“Disk Free”，顾名思义功能是用于显示系统上可使用的磁盘空间。默认显示单位为KB，建议使用“df -h”的参数组合，根据磁盘容量自动变换合适的单位，更利于阅读。<br />日常普遍用该命令可以查看磁盘被占用了多少空间、还剩多少空间等信息。<br />**语法格式：** df [参数] [指定文件]<br />**常用参数：**

| -a | 显示所有系统文件 |
| --- | --- |
| -B <块大小> | 指定显示时的块大小 |
| -h | 以容易阅读的方式显示 |
| -H | 以1000字节为换算单位来显示 |
| -i | 显示索引字节信息 |
| -k | 指定块大小为1KB |
| -l | 只显示本地文件系统 |
| -t <文件系统类型> | 只显示指定类型的文件系统 |
| -T | 输出时显示文件系统类型 |
| -- -sync | 在取得磁盘使用信息前，先执行sync命令 |

## 查看空间 du
du命令的英文全称是“Disk Usage”，即用于查看磁盘占用空间的意思。但是与df命令不同的是du命令是对文件和目录磁盘使用的空间的查看，而不是某个分区。<br />**语法格式：**du [参数] [文件]<br />**常用参数： **

| -a | 显示目录中所有文件大小 |
| --- | --- |
| -k | 以KB为单位显示文件大小 |
| -m | 以MB为单位显示文件大小 |
| -g | 以GB为单位显示文件大小 |
| -h | 以易读方式显示文件大小 |
| -s | 仅显示总计 |

## 磁盘分区 fdisk
fdisk命令的英文全称是“Partition table manipulator for Linux”，即作为磁盘的分区工具。进行硬盘分区从实质上说就是对硬盘的一种格式化， 用一个形象的比喻，分区就好比在一张白纸上画一个大方框，而格式化好比在方框里打上格子。<br />**语法格式：**fdisk [参数]<br />**常用参数：**

| -b | 指定每个分区的大小 |
| --- | --- |
| -l | 列出指定的外围设备的分区表状况 |
| -s | 将指定的分区大小输出到标准输出上，单位为区块 |
| -u | 搭配”-l”参数列表，会用分区数目取代柱面数目，来表示每个分区的起始地址 |
| -v | 显示版本信息 |

```shell
[root@hecs-x-medium-2-linux-20210831094415 ~]# fdisk -l
Disk /dev/vda: 40 GiB, 42949672960 bytes, 83886080 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x1bec7a05

Device     Boot Start      End  Sectors Size Id Type
/dev/vda1  *     2048 83886079 83884032  40G 83 Linux


Disk /dev/vdb: 100 GiB, 107374182400 bytes, 209715200 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes

[root@hecs-x-medium-2-linux-20210831094415 ~]# fdisk /dev/vdb 

//
更改将仅保留在内存中，直到您决定写入它们。

在使用write命令之前要小心。

设备不包含可识别的分区表。
//

Welcome to fdisk (util-linux 2.32.1).
Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.

Device does not contain a recognized partition table.
Created a new DOS disklabel with disk identifier 0xb611d4d2.

Command (m for help): m

Help:

  DOS (MBR)
   a   toggle a bootable flag
   b   edit nested BSD disklabel
   c   toggle the dos compatibility flag

  Generic
   d   delete a partition												//删除一个分区
   F   list free unpartitioned space						//列出可用的未分区空间
   l   list known partition types								//列出分	区的类型
   n   add a new partition											//添加一个新的分区
   p   print the partition table								//打印分区表
   t   change a partition type									//改变分区类型
   v   verify the partition table								
   i   print information about a partition

  Misc
   m   print this menu
   u   change display/entry units
   x   extra functionality (experts only)

  Script
   I   load disk layout from sfdisk script file
   O   dump disk layout to sfdisk script file

  Save & Exit
   w   write table to disk and exit								//把分区表写入硬盘并退出
   q   quit without saving changes								//退出不保存

  Create a new label
   g   create a new empty GPT partition table
   G   create a new empty SGI (IRIX) partition table
   o   create a new empty DOS partition table
   s   create a new empty Sun partition table


Command (m for help): 

```
## 查看系统的磁盘 lsblk
lsblk命令的英文是“list block”，即用于列出所有可用块设备的信息，而且还能显示他们之间的依赖关系，但是它不会列出RAM盘的信息。<br />lsblk命令包含在util-linux-ng包中，现在该包改名为util-linux。<br />**语法格式：**lsblk [参数]<br />**常用参数：**

| -a | 显示所有设备 |
| --- | --- |
| -b | 以bytes方式显示设备大小 |
| -d | 不显示 slaves 或 holders |
| -D | print discard capabilities |
| -e | 排除设备 |
| -f | 显示文件系统信息 |
| -h | 显示帮助信息 |
| -i | use ascii characters only |
| -m | 显示权限信息 |
| -l | 使用列表格式显示 |
| -n | 不显示标题 |
| -o | 输出列 |
| -P | 使用key=”value”格式显示 |
| -r | 使用原始格式显示 |
| -t | 显示拓扑结构信息 |

## 文件系统挂载 mount
mount命令用于加载文件系统到指定的加载点。此命令的最常用于挂载cdrom，使我们可以访问cdrom中的数据，因为你将光盘插入cdrom中，Linux并不会自动挂载，必须使用Linux mount命令来手动完成挂载。<br />**语法格式：**mount [参数]<br />**常用参数： **

| -t | 指定挂载类型 |
| --- | --- |
| -l | 显示已加载的文件系统列表 |
| -h | 显示帮助信息并退出 |
| -V | 显示程序版本 |
| -n | 加载没有写入文件“/etc/mtab”中的文件系统 |
| -r | 将文件系统加载为只读模式 |
| -a | 加载文件“/etc/fstab”中描述的所有文件系统 |

# 系统管理

- rpm：rpm软件包管理
- find：查找和搜索文件
- uname：显示系统信息
## RPM软件包管理器
rpm命令是Red-Hat Package Manager（RPM软件包管理器）的缩写， 该命令用于管理Linux 下软件包的软件。在 Linux 操作系统下，几乎所有的软件均可以通过RPM 进行安装、卸载及管理等操作。<br />概括的说，rpm命令包含了五种基本功能：安装、卸载、升级、查询和验证。<br />**语法格式：**rpm [参数] [软件包]<br />**常用参数：**

| -a | 查询所有的软件包 |
| --- | --- |
| -b或-t | 设置包装套件的完成阶段，并指定套件档的文件名称； |
| -c | 只列出组态配置文件，本参数需配合”-l”参数使用 |
| -d | 只列出文本文件，本参数需配合”-l”参数使用 |
| -e或--erase | 卸载软件包 |
| -f | 查询文件或命令属于哪个软件包 |
| -h或--hash | 安装软件包时列出标记 |
| -i | 显示软件包的相关信息 |
| --install | 安装软件包 |
| -l | 显示软件包的文件列表 |
| -p | 查询指定的rpm软件包 |
| -q | 查询软件包 |
| -R | 显示软件包的依赖关系 |
| -s | 显示文件状态，本参数需配合”-l”参数使用 |
| -U或--upgrade | 升级软件包 |
| -v | 显示命令执行过程 |
| -vv | 详细显示指令执行过程 |

## 查找和搜索文件 find
find命令可以根据给定的路径和表达式查找的文件或目录。find参数选项很多，并且支持正则，功能强大。和管道结合使用可以实现复杂的功能，是系统管理者和普通用户必须掌握的命令。<br />find如不加任何参数，表示查找当前路径下的所有文件和目录，如果服务器负载比较高尽量不要在高峰期使用find命令，find命令模糊搜索还是比较消耗系统资源的。<br />**语法格式**：find [参数] [路径] [查找和搜索范围]<br />**常用参数**：

| -name | 按名称查找 |
| --- | --- |
| -size | 按大小查找 |
| -user | 按属性查找 |
| -type | 按类型查找 |
| -iname | 忽略大小写 |

## 显示系统信息 uname
uname命令的英文全称即“Unix name”。<br />用于显示系统相关信息，比如主机名、内核版本号、硬件架构等。<br />如果未指定任何选项，其效果相当于执行”uname -s”命令，即显示系统内核的名字。<br />**语法格式：**uname [参数]<br />**常用参数：**

| -a | 显示系统所有相关信息 |
| --- | --- |
| -m | 显示计算机硬件架构 |
| -n | 显示主机名称 |
| -r | 显示内核发行版本号 |
| -s | 显示内核名称 |
| -v | 显示内核版本 |
| -p | 显示主机处理器类型 |
| -o | 显示操作系统名称 |
| -i | 显示硬件平台 |

# 文件传输

- tftp：上传及下载文件
- curl：文件传输工具
- fsck：检查并修复Linux文件系统
## 上传及下载文件 tftp
tftp命令用于传输文件。ftp让用户得以下载存放于远端主机的文件，也能将文件上传到远端主机放置。<br />tftp是简单的文字模式ftp程序，它所使用的指令和ftp类似。<br />**语法格式：**tftp [参数]<br />**常用参数：**

| connect | 连接到远程tftp服务器 |
| --- | --- |
| mode | 文件传输模式 |
| put | 上传文件 |
| get | 下载文件 |
| quit | 退出 |
| verbose | 显示详细的处理信息 |
| trace | 显示包路径 |
| status | 显示当前状态信息 |
| binary | 二进制传输模式 |
| ascii | ascii 传送模式 |
| rexmt | 设置包传输的超时时间 |
| timeout | 设置重传的超时时间 |
| help | 帮助信息 |
| ? | 帮助信息 |

## 文件传输工具 curl
curl命令是一个利用URL规则在shell终端命令行下工作的文件传输工具；它支持文件的上传和下载，所以是综合传输工具，但按传统，习惯称curl为下载工具。<br />作为一款强力工具，curl支持包括HTTP、HTTPS、ftp等众多协议，还支持POST、cookies、认证、从指定偏移处下载部分文件、用户代理字符串、限速、文件大小、进度条等特征；做网页处理流程和数据检索自动化。<br />**语法格式：**curl [参数] [网址]<br />**常用参数：**

| -O | 把输出写到该文件中，保留远程文件的文件名 |
| --- | --- |
| -u | 通过服务端配置的用户名和密码授权访问 |

## 检查并修复Linux文件系统  fsck
sck命令的英文全称是“filesystem check”，即检查文件系统的意思，常用于检查并修复Linux文件系统的一些错误信息，操作文件系统需要先备份重要数据，以防丢失。<br />Linux fsck命令用于检查并修复Linux文件系统，可以同时检查一个或多个 Linux 文件系统；若系统掉电或磁盘发生问题，可利用fsck命令对文件系统进行检查。<br />**语法格式：**fsck [参数] [文件系统]<br />**常用参数：**

| -a | 自动修复文件系统，不询问任何问题 |
| --- | --- |
| -A | 依照/etc/fstab配置文件的内容，检查文件内所列的全部文件系统 |
| -N | 不执行指令，仅列出实际执行会进行的动作 |
| -P | 当搭配”-A”参数使用时，则会同时检查所有的文件系统 |
| -r | 采用互动模式，在执行修复时询问问题，让用户得以确认并决定处理方式 |
| -R | 当搭配”-A”参数使用时，则会略过/目录的文件系统不予检查 |
| -t | 指定要检查的文件系统类型 |
| -T | 执行fsck指令时，不显示标题信息 |
| -V | 显示指令执行过程 |

# 网络通讯

- ssh：安全连接客户端
- netstat：显示网络状态
- ping：测试主机间网络连通性
- ifconfig：显示或设置网络设备
## 安全连接客户端 ssh
ssh命令是openssh套件中的客户端连接工具，可以给予ssh加密协议实现安全的远程登录服务器，实现对服务器的远程管理。<br />**语法格式: **ssh [参数] [远程主机]<br />**常用参数：**

| -1 | 强制使用ssh协议版本1 |
| --- | --- |
| -2 | 强制使用ssh协议版本2 |
| -4 | 强制使用IPv4地址 |
| -6 | 强制使用IPv6地址 |
| -A | 开启认证代理连接转发功能 |
| -a | 关闭认证代理连接转发功能 |
| -b<IP地址> | 使用本机指定的地址作为对位连接的源IP地址 |
| -C | 请求压缩所有数据 |
| -F<配置文件> | 指定ssh指令的配置文件，默认的配置文件为“/etc/ssh/ssh_config” |
| -f | 后台执行ssh指令 |
| -g | 允许远程主机连接本机的转发端口 |
| -i<身份文件> | 指定身份文件（即私钥文件） |
| -l<登录名> | 指定连接远程服务器的登录用户名 |
| -N | 不执行远程指令 |
| -o<选项> | 指定配置选项 |
| -p<端口> | 指定远程服务器上的端口 |
| -q | 静默模式，所有的警告和诊断信息被禁止输出 |
| -X | 开启X11转发功能 |
| -x | 关闭X11转发功能 |
| -y | 开启信任X11转发功能 |

## 显示网络状态 netstat
netstat 命令用于显示各种网络相关信息，如网络连接，路由表，接口状态 (Interface Statistics)，masquerade 连接，多播成员 (Multicast Memberships) 等等。<br />从整体上看，netstat的输出结果可以分为两个部分：一个是Active Internet connections，称为有源TCP连接，其中”Recv-Q”和”Send-Q”指%0A的是接收队列和发送队列。这些数字一般都应该是0。如果不是则表示软件包正在队列中堆积。这种情况只能在非常少的情况见到；另一个是Active UNIX domain sockets，称为有源Unix域套接口(和网络套接字一样，但是只能用于本机通信，性能可以提高一倍)。<br />**语法格式：**netstat [参数]<br />**常用参数：**

| -a | 显示所有连线中的Socket |
| --- | --- |
| -p | 显示正在使用Socket的程序识别码和程序名称 |
| -u | 显示UDP传输协议的连线状况 |
| -i

 | 显示网络界面信息表单 |
| -n | 直接使用IP地址，不通过域名服务器 |

## 测试主机间网络连通性 ping
ping命令主要用来测试主机之间网络的连通性，也可以用于。执行ping指令会使用ICMP传输协议，发出要求回应的信息，若远端主机的网络功能没有问题，就会回应该信息，因而得知该主机运作正常。<br />不过值得我们注意的是：Linux系统下的ping命令与Windows系统下的ping命令稍有不同。Windows下运行ping命令一般会发出4个请求就结束运行该命令；而Linux下不会自动终止，此时需要我们按CTR+C终止或者使用-c参数为ping命令指定发送的请求数目。<br />**语法格式：**ping [参数] [目标主机]<br />**常用参数：**

| -d | 使用Socket的SO_DEBUG功能 |
| --- | --- |
| -c | 指定发送报文的次数 |
| -i | 指定收发信息的间隔时间 |
| -I | 使用指定的网络接口送出数据包 |
| -l | 设置在送出要求信息之前，先行发出的数据包 |
| -n | 只输出数值 |
| -p | 设置填满数据包的范本样式 |
| -q | 不显示指令执行过程 |
| -R | 记录路由过程 |
| -s | 设置数据包的大小 |
| -t | 设置存活数值TTL的大小 |
| -v | 详细显示指令的执行过程 |

```shell
利用ping命令获取百度网址的IP地址
[root@hecs-x-medium-2-linux-20210831094415 ~]# ping -c 1  www.baidu.com |grep from
64 bytes from 180.101.49.11 (180.101.49.11): icmp_seq=1 ttl=49 time=11.5 ms

```
## 显示或设置网络设备 ifconfig
ifconfig命令的英文全称是“network interfaces configuring”，即用于配置和显示Linux内核中网络接口的网络参数。用ifconfig命令配置的网卡信息，在网卡重启后机器重启后，配置就不存在。要想将上述的配置信息永远的存的电脑里，那就要修改网卡的配置文件了。<br />**语法格式：**ifconfig [参数]<br />**常用参数：**

| add<地址> | 设置网络设备IPv6的IP地址 |
| --- | --- |
| del<地址> | 删除网络设备IPv6的IP地址 |
| down | 关闭指定的网络设备 |
| up | 启动指定的网络设备 |
| IP地址 | 指定网络设备的IP地址 |

```shell
[root@hecs-x-medium-2-linux-20210831094415 ~]# ifconfig
docker0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        inet 172.17.0.1  netmask 255.255.0.0  broadcast 172.17.255.255
        ether 02:42:3b:33:5c:dc  txqueuelen 0  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.0.196  netmask 255.255.255.0  broadcast 192.168.0.255
        inet6 fe80::f816:3eff:fe81:2000  prefixlen 64  scopeid 0x20<link>
        ether fa:16:3e:81:20:00  txqueuelen 1000  (Ethernet)
        RX packets 262915  bytes 356591922 (340.0 MiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 112784  bytes 10269703 (9.7 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

```
