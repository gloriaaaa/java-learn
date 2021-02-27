- [linux命令学习](#linux----)
  * [命令帮助](#----)
  * [文件、目录管理](#-------)
  * [进程、作业管理](#-------)
  * [网络命令](#----)
  * [其他命令](#----)
# linux命令学习

## 命令帮助
- `whatis`
- `info`
- `man`
```
gloria@gloria-ThinkPad-E450:~$ whatis ls
ls (1)               - list directory contents

gloria@gloria-ThinkPad-E450:~$ whatis -w "ls*"
ls (1)               - list directory contents
lsattr (1)           - list file attributes on a Linux second extended file s...
lsb_release (1)      - print distribution-specific information
lsblk (8)            - list block devices
lscpu (1)            - display information about the CPU architecture
lsdiff (1)           - show which files are modified by a patch
lsearch (3)          - linear search of an array
lseek (2)            - reposition read/write file offset
lseek64 (3)          - reposition 64-bit read/write file offset
lshw (1)             - list hardware
lsinitramfs (8)      - list content of an initramfs image
lsipc (1)            - show information on IPC facilities currently employed ...
lslocks (8)          - list local system locks
lslogins (1)         - display information about known users in the system
lsmod (8)            - Show the status of modules in the Linux Kernel
lsof (8)             - list open files
lspci (8)            - list all PCI devices
lspcmcia (8)         - display extended PCMCIA debugging information
lspgpot (1)          - extracts the ownertrust values from PGP keyrings and l...
lstat (2)            - get file status
lstat64 (2)          - get file status
lsusb (8)            - list USB devices
```

## 文件、目录管理
- 创建目录　`mkdir`
- 删除 
	-　删除文件　`rmdir test`
	- 删除空目录　`rmdir test 或　rm -d test`
	- 删除目录和文件　`rm -rf file`
- 查看当前目录下文件个数　`find ./ | wc -l`
-　进入目录 `cd`
- 显示路径　`pwd`
- 显示文件　`ls`
- 以列表的方式显示目录项　`ls -lrt`
- 查找文件或目录　`find ./ -name '*.log'`
注：
```
rm [选项] 文件
-f, --force          强力删除，不要求确认
-i                   每删除一个文件或进入一个子目录都要求确认
-I                   在删除超过三个文件或者递归删除前要求确认
-r, -R               递归删除子目录
-d, --dir            删除空目录
-v, --verbose        显示删除结果

```

```
gloria@gloria-ThinkPad-E450:~$ mkdir linux
gloria@gloria-ThinkPad-E450:~$ cd linux
gloria@gloria-ThinkPad-E450:~/linux$ mkdir test
gloria@gloria-ThinkPad-E450:~/linux$ ls
test
gloria@gloria-ThinkPad-E450:~/linux$ rm test
rm: 无法删除'test': 是一个目录
gloria@gloria-ThinkPad-E450:~/linux$ rm -rf test
gloria@gloria-ThinkPad-E450:~/linux$ ls
gloria@gloria-ThinkPad-E450:~/linux$ mkdir test
gloria@gloria-ThinkPad-E450:~/linux$ rm -d test
gloria@gloria-ThinkPad-E450:~/linux$ ls
gloria@gloria-ThinkPad-E450:~/linux$ mkdir test
gloria@gloria-ThinkPad-E450:~/linux$ ls
test
gloria@gloria-ThinkPad-E450:~/linux$ rmdir test
gloria@gloria-ThinkPad-E450:~/linux$ ls
gloria@gloria-ThinkPad-E450:~/linux$ 
gloria@gloria-ThinkPad-E450:~/linux$ touch 1.log
gloria@gloria-ThinkPad-E450:~/linux$ touch 2.log
gloria@gloria-ThinkPad-E450:~/linux$ find ./ -name '*.log'
./1.log
./2.log
gloria@gloria-ThinkPad-E450:~/linux$ ls -lrt
总用量 0
-rw-rw-r-- 1 gloria gloria 0 2月  15 20:53 1.log
-rw-rw-r-- 1 gloria gloria 0 2月  15 20:53 2.log
gloria@gloria-ThinkPad-E450:~/linux$ 
```

文件操作命令
- 查看两个文件间的差别 `diff 1.log 2.log -y -W 50`
	- 加上-y -w　可以并排比较
- 只看前10行　`head -10 filename`
- 显示文件倒数五行 `tail -5 filename`
```
gloria@gloria-ThinkPad-E450:~/linux$ diff 1.log 2.log  -y -W 50
1			1
2			2
3		      <
4			4
5			5
6		      <
7		      <
8		      <
9		      <
10		      <
11		      <
12		      <

```


关于`cat`命令
```
语法格式
cat [-AbeEnstTuv] [--help] [--version] fileName
参数说明：
-n 或 --number：由 1 开始对所有输出的行数编号。
-b 或 --number-nonblank：和 -n 相似，只不过对于空白行不编号。
-s 或 --squeeze-blank：当遇到有连续两行以上的空白行，就代换为一行的空白行。
-v 或 --show-nonprinting：使用 ^ 和 M- 符号，除了 LFD 和 TAB 之外。
-E 或 --show-ends : 在每行结束处显示 $。
-T 或 --show-tabs: 将 TAB 字符显示为 ^I。
-A, --show-all：等价于 -vET。
-e：等价于"-vE"选项；
-t：等价于"-vT"选项；
```
- `cat -n textfile1 > textfile2` 把 textfile1 的文档内容加上行号后输入 textfile2 这个文档里
- `cat -b textfile1 textfile2 >> textfile3` 把 textfile1 和 textfile2 的文档内容加上行号（空白行不加）之后将内容附加到 textfile3 
- `cat /dev/null > /etc/test.txt` 清空 /etc/test.txt 文档内容
- cat 也可以用来制作镜像文件。例如要制作软盘的镜像文件，将软盘放好后输入：｀cat /dev/fd0 > OUTFILE｀。相反的，如果想把 image file 写到软盘，输入：｀cat IMG_FILE > /dev/fd0｀

```
gloria@gloria-ThinkPad-E450:~/linux$ diff 1.log 2.log  -y -W 50
1			1
2			2
3		      <
4			4
5			5
6		      <
7		      <
8		      <
9		      <
10		      <
11		      <
12		      <

```

权限修改
- 改变文件的拥有者：chown
- 改变文件读、写、执行等属性：chmod
- 递归子目录修改：chown -R user source/
- 增加脚本可执行权限：chmod +x filename
- ln sourcefile destfile：硬连接；删除一个，将仍能找到；
- ln -s sourcefile destfile：符号链接(软链接)；删除源，另一个无法使用；



## 进程、作业管理
参考 https://blog.csdn.net/baidu_41666198/article/details/97813890

`ps` 用于报告系统进程状态
`ps -a`：显示所有终端机下的执行程序，除了阶段作业领导者之外。
`ps a`：显示现行终端机下的所有程序，包括其他用户的程序。
`ps -A`：显示所有程序。
`ps -u`：以用户为主的格式来显示程序状况。
`ps -x`：显示所有程序，不以终端机来区分。
其中展示的进程状态有５种
- R 运行
- S 中断
- D 不可中断
- Z 僵死
- T 停止

```
gloria@gloria-ThinkPad-E450:~/linux$ ps -a
  PID TTY          TIME CMD
10594 pts/2    00:00:00 ps
gloria@gloria-ThinkPad-E450:~/linux$ ps a
  PID TTY      STAT   TIME COMMAND
 1019 tty7     Ssl+   1:44 /usr/lib/xorg/Xorg -core :0 -seat seat0 -auth /var/ru
 1279 tty1     Ss+    0:00 /sbin/agetty --noclear tty1 linux
 5204 pts/2    Ss     0:00 bash
10595 pts/2    R+     0:00 ps a
gloria@gloria-ThinkPad-E450:~/linux$ ps -A
  PID TTY          TIME CMD
    1 ?        00:00:01 systemd
    2 ?        00:00:00 kthreadd
    3 ?        00:00:00 ksoftirqd/0
    5 ?        00:00:00 kworker/0:0H
    7 ?        00:00:02 rcu_sched
    8 ?        00:00:00 rcu_bh
    9 ?        00:00:00 migration/0
   10 ?        00:00:00 watchdog/0
   11 ?        00:00:00 watchdog/1
   12 ?        00:00:00 migration/1
   13 ?        00:00:00 ksoftirqd/1
   15 ?        00:00:00 kworker/1:0H
   16 ?        00:00:00 watchdog/2
   17 ?        00:00:00 migration/2
   18 ?        00:00:00 ksoftirqd/2
   20 ?        00:00:00 kworker/2:0H


gloria@gloria-ThinkPad-E450:~/linux$ ps -u
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
gloria    5204  0.0  0.0  24708  5432 pts/2    Ss   17:49   0:00 bash
gloria   10168  0.0  0.0  39104  3328 pts/2    R+   21:04   0:00 ps -u
gloria@gloria-ThinkPad-E450:~/linux$ ps -x
  PID TTY      STAT   TIME COMMAND
 1954 ?        Ss     0:00 /lib/systemd/systemd --user
 1955 ?        S      0:00 (sd-pam)
 1961 ?        Sl     0:00 /usr/bin/gnome-keyring-daemon --daemoniz
```

- `top`实时动态地查看系统的整体运行情况，互动式界面。
	- 输入P：根据CPU使用百分比大小进行排序
	- M：根据驻留内存大小进行排序
	- i：使top不显示任何闲置或者僵死进程。
- `kill`使指定程序终止。若仍无法终止该程序，程序或工作的编号可利用ps指令或job指令查看。
- `ipcs`参考https://blog.csdn.net/dalongyes/article/details/50616162
- `ipcsm`
- `jobs`
```
gloria@gloria-ThinkPad-E450:~/linux$ ipcs -a

--------- 消息队列 -----------
键        msqid      拥有者  权限     已用字节数 消息      

------------ 共享内存段 --------------
键        shmid      拥有者  权限     字节     连接数  状态      
0x00000000 2359296    gloria     600        524288     2          目标       
0x00000000 1998849    gloria     600        524288     2          目标       
0x00000000 1015810    gloria     600        16777216   2                       
0x00000000 1802243    gloria     700        16472      2          目标       
0x00000000 524292     gloria     600        524288     2          目标       
0x00000000 851973     gloria     600        524288     2          目标       
0x00000000 1179654    gloria     600        524288     2          目标       
0x00000000 1409031    gloria     600        524288     2          目标       
0x00000000 1507336    gloria     600        524288     2          目标       
0x00000000 4063241    gloria     600        4194304    2          目标       
0x00000000 1638410    gloria     600        524288     2          目标       
0x00000000 1736715    gloria     600        524288     2          目标       
0x00000000 1769484    gloria     600        67108864   2          目标       
0x00000000 2654221    gloria     600        524288     2          目标       
0x00000000 3473422    gloria     700        166320     2          目标       
0x00000000 2162703    gloria     600        524288     2          目标       
0x00000000 3276817    gloria     600        524288     2          目标       
0x00000000 3309586    gloria     600        67108864   2          目标       

--------- 信号量数组 -----------
键        semid      拥有者  权限     nsems     

gloria@gloria-ThinkPad-E450:~/linux$ ipcs -q

--------- 消息队列 -----------
键        msqid      拥有者  权限     已用字节数 消息      

gloria@gloria-ThinkPad-E450:~/linux$ ipcs -m

------------ 共享内存段 --------------
键        shmid      拥有者  权限     字节     连接数  状态      
0x00000000 2359296    gloria     600        524288     2          目标       
0x00000000 1998849    gloria     600        524288     2          目标       
0x00000000 1015810    gloria     600        16777216   2                       
0x00000000 1802243    gloria     700        16472      2          目标       
0x00000000 524292     gloria     600        524288     2          目标       
0x00000000 851973     gloria     600        524288     2          目标       
0x00000000 1179654    gloria     600        524288     2          目标       
0x00000000 1409031    gloria     600        524288     2          目标       
0x00000000 1507336    gloria     600        524288     2          目标       
0x00000000 4128777    gloria     600        4194304    2          目标       
0x00000000 1638410    gloria     600        524288     2          目标       
0x00000000 1736715    gloria     600        524288     2          目标       
0x00000000 1769484    gloria     600        67108864   2          目标       
0x00000000 2654221    gloria     600        524288     2          目标       
0x00000000 3473422    gloria     700        166320     2          目标       
0x00000000 2162703    gloria     600        524288     2          目标       
0x00000000 3276817    gloria     600        524288     2          目标       
0x00000000 3309586    gloria     600        67108864   2          目标       

gloria@gloria-ThinkPad-E450:~/linux$ ipcs -s

--------- 信号量数组 -----------
键        semid      拥有者  权限     nsems     

gloria@gloria-ThinkPad-E450:~/linux$ 
```

## 网络命令

- `ifconfig` 配置和显示Linux内核中网络接口的网络参数。用ifconfig命令配置的网卡信息，在网卡重启后机器重启后，配置就不存在。
- `iptables` 是Linux上常用的防火墙软件，是netfilter项目的一部分。可以直接配置，也可以通过许多前端和图形界面配置。
- `route` 用来显示并设置Linux内核中的网络路由表，route命令设置的路由主要是静态路由。直接在命令行下执行route命令来添加路由，不会永久保存，当网卡重启或者机器重启之后，该路由就失效了；可以在/etc/rc.local中添加route命令来保证该路由设置永久有效。
- `netstat` 用来打印Linux中网络系统的状态信息。如接口/网卡状态(-i)，路由表(-r)，网络连接(-a)，tcp相关选项(-t)，udp相关选项(-u)，按各个协议统计(-s)。参考https://www.cnblogs.com/ftl1012/p/netstat.html
- `tcpdump`打印所有经过网络接口的数据包的头信息，也可以使用-w选项将数据包保存到文件中，方便以后分析。
- `scp`可以将本地localpath指向的文件上传到远程主机的path路径，或者遍历下载path路径下的整个文件系统，到本地的localpath

```
gloria@gloria-ThinkPad-E450:~/linux$ ifconfig
docker0   Link encap:以太网  硬件地址 02:42:9d:ec:dc:2e  
          inet 地址:172.17.0.1  广播:172.17.255.255  掩码:255.255.0.0
          UP BROADCAST MULTICAST  MTU:1500  跃点数:1
          接收数据包:0 错误:0 丢弃:0 过载:0 帧数:0
          发送数据包:0 错误:0 丢弃:0 过载:0 载波:0
          碰撞:0 发送队列长度:0 
          接收字节:0 (0.0 B)  发送字节:0 (0.0 B)

enp0s25   Link encap:以太网  硬件地址 50:7b:9d:15:89:18  
          UP BROADCAST MULTICAST  MTU:1500  跃点数:1
          接收数据包:0 错误:0 丢弃:0 过载:0 帧数:0
          发送数据包:0 错误:0 丢弃:0 过载:0 载波:0
          碰撞:0 发送队列长度:1000 
          接收字节:0 (0.0 B)  发送字节:0 (0.0 B)
          中断:20 Memory:f1300000-f1320000 

lo        Link encap:本地环回  
          inet 地址:127.0.0.1  掩码:255.0.0.0
          inet6 地址: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  跃点数:1
          接收数据包:4020 错误:0 丢弃:0 过载:0 帧数:0
          发送数据包:4020 错误:0 丢弃:0 过载:0 载波:0
          碰撞:0 发送队列长度:1 
          接收字节:328017 (328.0 KB)  发送字节:328017 (328.0 KB)

wlp4s0    Link encap:以太网  硬件地址 e4:f8:9c:df:5d:72  
          inet 地址:192.168.1.5  广播:192.168.1.255  掩码:255.255.255.0
          inet6 地址: fe80::b92c:6db2:6e38:7de9/64 Scope:Link
          inet6 地址: fe80::5d7b:ac32:b0c5:1dfc/64 Scope:Link
          inet6 地址: fe80::ea26:11bc:c879:d6b0/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  跃点数:1
          接收数据包:59993 错误:0 丢弃:0 过载:0 帧数:0
          发送数据包:27776 错误:0 丢弃:0 过载:0 载波:0
          碰撞:0 发送队列长度:1000 
          接收字节:35763538 (35.7 MB)  发送字节:4772940 (4.7 MB)

gloria@gloria-ThinkPad-E450:~/linux$ iptables -h
iptables v1.6.0

Usage: iptables -[ACD] chain rule-specification [options]
       iptables -I chain [rulenum] rule-specification [options]
       iptables -R chain rulenum rule-specification [options]
       iptables -D chain rulenum [options]
       iptables -[LS] [chain [rulenum]] [options]
       iptables -[FZ] [chain] [options]
       iptables -[NX] chain
       iptables -E old-chain-name new-chain-name
       iptables -P chain target [options]
       iptables -h (print this help information)

gloria@gloria-ThinkPad-E450:~/linux$ route
内核 IP 路由表
目标            网关            子网掩码        标志  跃点   引用  使用 接口
default         192.168.1.1     0.0.0.0         UG    600    0        0 wlp4s0
link-local      *               255.255.0.0     U     1000   0        0 docker0
172.17.0.0      *               255.255.0.0     U     0      0        0 docker0
192.168.1.0     *               255.255.255.0   U     600    0        0 wlp4s0

```
## 其他命令
- `free`
- `useradd`