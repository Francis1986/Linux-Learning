## 常用系统工作命令
---
### 命令索引
- [echo](#echo)：打印字符串或变量  
- [date](#date)：显示日期和时间   
- [reboot](#reboot)：重启   
- [poweroff](#poweroff)：关机   
- [wget](#wget)：下载   
- [ps](#ps)：查看进程   
- [top](#top)：查看当前进程   
- [pidof](#pidof)：查看进程的pid编号   
- [kill](#kill)：按pid编号终止进程   
- [killall](#killall)：按进程名称终止进程   
- [ifconfig](#ifconfig)：查看网卡名称和信息   
- [uname](#uname)：查看系统内核和版本信息   
- [uptime](#uptime)： 查看当前系统负载信息  
- [free](#free)：查看系统内存使用信息   
- [df](#df)：查看整个系统的存储空间
- [du](#du)：查看指定文件大小
- [who](#who)：查看当前登录的用户信息    
- [last](#last)：查看最后登录的用户信息   
- [history](#history)：查看历史命令   
- [sosreport](#sosreport)：收集系统架构和诊断信息
---

- <span id = echo>**echo命令**</span>   
　　echo命令用于在终端输出字符串或变量提取后的值，格式为`echo [字符串 | $变量]`。例如，把指定字符串`hello world`输出到终端屏幕的命令为： 

    ```
    [root@SLAVE19 /]# echo hello world
    hello world
    ```
- <span id = date>**date**</span>   
　　date命令用于显示及设置系统的时间或日期，格式为`date [选项] [+指定的格式]`。只需在强大的`date`命令中输入以`+`号开头的参数，即可按照指定格式来输出系统的时间或日期，这样在日常工作时便可以把备份数据的命令与指定格式输出的时间信息结合到一起。例如，把打包后的文件自动按照`年-月-日`的格式打包成`backup-2017-9-1.tar.gz`，用户只需要看一眼文件名称就能大概了解到每个文件的备份时间了。date命令中常见的参数格式及作用如下表所示：

    参数 |作用
    :---:|:---:
    `%t` | 跳格[Tab键]
    `%H` | 小时（00～23）
    `%I` | 小时（00～12）
    `%M` | 分钟（00～59）
    `%S` | 秒（00～59）
    `%j` | 今年中的第几天
    　　按照默认格式查看当前系统时间的date命令如下所示：
    
    ```
    [root@SLAVE19 /]# date
    Mon Jan  8 10:42:12 CST 2018
    ```
    　　按照“年-月-日小时:分钟:秒”的格式查看当前系统时间的date命令如下所示：
    ```
    [root@linuxprobe ~]# date "+%Y-%m-%d %H:%M:%S"
    2017-08-24 16:29:12
    ```
    　　将系统的当前时间设置为2017年9月1日8点30分的date命令如下所示：
    ```
    [root@linuxprobe ~]# date -s "20170901 8:30:00"
    Fri Sep 1 08:30:00 CST 2017
    ```
    　　date命令中的参数%j可用来查看今天是当年中的第几天。这个参数能够很好地区分备份时间的新旧，即数字越大，越靠近当前时间。该参数的使用方式以及显示结果如下：
    
    ```
    [root@SLAVE19 /]# date '+%j'
    008
    ```

- <span id = reboot>**reboot** </span>  
　　`reboot`命令用于重启系统，其格式为`reboot`。
由于重启计算机这种操作会涉及硬件资源的管理权限，因此默认只能使用root管理员来重启，其命令如下：
    
    ```
    [root@linuxprobe ~]# reboot
    ```
- <span id = poweroff>**poweroff** </span>     
　　`poweroff`命令用于关闭系统，其格式为`poweroff`。
该命令与reboot命令相同，都会涉及硬件资源的管理权限，因此默认只有root管理员才可以关闭电脑，其命令如下：

    ```
    [root@linuxprobe ~]# poweroff
    ```
- <span id = wget>**wget** </span>  
　　wget命令用于在终端中下载网络文件，格式为`wget [参数] 下载地址`。如果您没有Linux系统的管理经验，当前只需了解一下`wget`命令的参数以及作用，然后看一下下面的演示实验即可，切记不要急于求成。后面章节将逐步讲解Linux系统的配置管理方法，可以等您掌握了网卡的配置方法后再来进行这个实验操作。表2-5所示为`wget`命令的参数以及参数的作用。

    参数 | 作用
    :---:|:---
    `-b` | 后台下载模式
    `-p` | 下载到指定目录
    `-t` | 最大尝试次数
    `-c` | 断点续传
    `-p` | 下载页面内所有资源，包括图片、视频等
    `-r` | 递归下载
    　　尝试使用wget命令从本书的配套站点中下载本书的最新pdf格式电子文档，这个文件的完整路径为`http://www.linuxprobe.com/docs/LinuxProbe.pdf`，执行该命令后的下载效果如下：
        
    ```
    [root@linuxprobe ~]# wget http://www.linuxprobe.com/docs/LinuxProbe.pdf
    --2017-08-24 19:30:12 -- http://www.linuxprobe.com/docs/LinuxProbe.pdf
    Resolving www.linuxprobe.com (www.linuxprobe.com)... 220.181.105.185
    Connecting to www.linuxprobe.com (www.linuxprobe.com)|220.181.105.185|:80...
    connected.
    HTTP request sent, awaiting response... 200 OK
    Length: 45948568 (44M) [application/pdf]
    Saving to: ‘LinuxProbe.pdf’
    
    100%[===========================================>] 45,948,568 32.9MB/s in 1.3s
    
    2017-08-24 19:30:14 (32.9 MB/s) - ‘LinuxProbe.pdf’ saved [45948568/45948568]

    ```
    　　接下来，我们使用wget命令递归下载www.linuxprobe.com网站内的所有页面数据以及文件，下载完后会自动保存到当前路径下一个名为`www.linuxprobe.com`的目录中。执行该操作的命令为`wget -r -p http://www.linuxprobe.com`，该命令的执行结果如下:
    　　
    ```
    [root@linuxprobe ~]# wget -r -p http://www.linuxprobe.com
    --2017-08-24 19:31:41-- http://www.linuxprobe.com/
    Resolving www.linuxprobe.com... 106.185.25.197
    Connecting to www.linuxprobe.com|106.185.25.197|:80... connected.
    HTTP request sent, awaiting response... 200 OK
    Length: unspecified [text/html]
    Saving to: 'www.linuxprobe.com/index.html'
    ………………省略下载过程………………
    ```

- <span id = ps>**ps命令** </span>   
Linux系统进程的有以下五种状态:  
    **R(运行)**:进程正在运行或在运行队列中等待  
    **S(中断)**:进程处于休眠中，当某个条件形成后或者接收到信号时，则脱离该状态。  
    **D（不可中断)**:进程不响应系统异步信号，即便用kill命令也不能将其中断。  
    **Z(僵死)**:进程已经终止，但进程描述符依然存在,直到父进程调用wait4()系统函数后将进程释放。  
    **T(停止)**:进程收到停止信号后停止运行。  
    关于进程和线程可以看这里：
    [深入理解进程与线程](https://www.cnblogs.com/tiankong101/p/4229584.html)  
　　`ps`命令用于查看系统中的进程状态，格式为`ps [参数]`。
估计读者在第一次执行这个命令时都要惊呆一下—怎么会有这么多输出值，这可怎么看得过来？其实，刘遄老师通常会将ps命令与第3章的管道符技术搭配使用，用来抓取与某个指定服务进程相对应的PID号码。`ps`命令的常见参数以及作用如下表所示：

    参数 | 作用
    :---:|:---
    `-a` | 显示所有进程（包括其他用户的进程）
    `-u` | 用户以及其他详细信息
    `-x` | 显示没有控制终端的进程
    
    ```
    [root@SLAVE19 /]# ps aux
    USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
    root         1  0.0  0.0  43408  5396 ?        Ss   Jan02   0:12 /usr/lib/syste
    root         2  0.0  0.0      0     0 ?        S    Jan02   0:00 [kthreadd]
    root         3  0.0  0.0      0     0 ?        S    Jan02   0:01 [ksoftirqd/0]
    root         5  0.0  0.0      0     0 ?        S<   Jan02   0:00 [kworker/0:0H]
    root         6  0.0  0.0      0     0 ?        S    Jan02   0:02 [kworker/u64:0
    root         8  0.0  0.0      0     0 ?        S    Jan02   0:00 [migration/0]
    root         9  0.0  0.0      0     0 ?        S    Jan02   0:00 [rcu_bh]
    root        10  0.0  0.0      0     0 ?        S    Jan02   0:00 [rcuob/0]
    root        11  0.0  0.0      0     0 ?        S    Jan02   0:00 [rcuob/1]
    root        12  0.0  0.0      0     0 ?        S    Jan02   0:00 [rcuob/2]
    root        13  0.0  0.0      0     0 ?        S    Jan02   0:00 [rcuob/3]
    root        14  0.0  0.0      0     0 ?        S    Jan02   0:00 [rcuob/4]
    root        15  0.0  0.0      0     0 ?        S    Jan02   0:00 [rcuob/5]
    ---部分信息未显示--
    ```
- <span id = top>**top命令** </span>  
　　top命令用于动态地监视进程活动与系统负载等信息，其格式为`top`。top命令相当强大，能够动态地查看系统运维状态，完全将它看作Linux中的“强化版的Windows任务管理器”。top命令的运行界面如图所示。

    ```
    top - 16:28:56 up 3 days,  7:27,  6 users,  load average: 2.29, 1.90, 1.98
    Tasks: 444 total,   2 running, 442 sleeping,   0 stopped,   0 zombie
    %Cpu(s):  4.5 us,  0.6 sy,  0.0 ni, 92.5 id,  2.3 wa,  0.0 hi,  0.0 si,  0.0 s
    KiB Mem : 39587692+total,   979412 free, 11728516 used, 38316899+buff/cache
    KiB Swap: 31457276 total, 31457276 free,        0 used. 38364592+avail Mem 
    
      PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM     TIME+ COMMAND   
    24024 root      20   0  123688   4868   1952 R  99.3  0.0   1:00.92 python    
    15087 impala    20   0 40.956g 5.286g  29816 S  56.0  1.4 166:23.32 impalad   
      247 root      20   0       0      0      0 S   2.3  0.0  11:12.62 kswapd0   
      248 root      20   0       0      0      0 S   2.0  0.0   6:10.82 kswapd1   
    14170 yarn      20   0 2081812 1.041g  12864 S   0.7  0.3 194:41.41 java      
    14516 hive      20   0 5418716 1.188g  11040 S   0.7  0.3   4:04.34 java      
       48 root      20   0       0      0      0 S   0.3  0.0   0:13.80 rcuos/5   
     1625 root      20   0 2171148  50216   2800 S   0.3  0.0  49:03.00 cmf-agent 
     1665 root      20   0  224404  13876   1700 S   0.3  0.0   1:14.51 python    
     2573 root      20   0       0      0      0 S   0.3  0.0   0:34.89 kworker/0+
    13993 hdfs      20   0 1864444 0.987g  11232 S   0.3  0.3 131:14.00 java      
    24743 root      20   0  146408   2352   1416 R   0.3  0.0   0:00.07 top       
    30196 root      20   0       0      0      0 S   0.3  0.0   3:23.36 kworker/u+
        1 root      20   0   43408   5388   1884 S   0.0  0.0   0:08.68 systemd  
    注：第3行中的数据均为CPU数据并以百分比格式显示，例如“97.1 id”意味着有97.1%的CPU处理器资源处于空闲。
    ```
    第1行：系统时间、运行时间、登录终端数、系统负载（三个数值分别为1分钟、5分钟、15分钟内的平均值，数值越小意味着负载越低）。  
    第2行：进程总数、运行中的进程数、睡眠中的进程数、停止的进程数、僵死的进程数。  
    第3行：用户占用资源百分比、系统内核占用资源百分比、改变过优先级的进程资源百分比、空闲的资源百分比等。   
    第4行：物理内存总量、内存使用量、内存空闲量、作为内核缓存的内存量。  
    第5行：虚拟内存总量、虚拟内存使用量、虚拟内存空闲量、已被提前加载的内存量。  

- <span id = pidof>**pidof** </span>  
　　pidof命令用于查询某个指定服务进程的PID值，格式为`pidof [参数] [服务名称]`。每个进程的进程号码值（PID）是唯一的，因此可以通过PID来区分不同的进程。
    ```
    [root@linuxprobe ~]# pidof sshd
    2156
    ```
- <span id = x>**kill** </span>  
　　kill命令用于终止某个指定PID的服务进程，格式为`kill [参数] [进程PID]`。接下来，我们使用kill命令把上面用pidof命令查询到的PID所代表的进程终止掉，其命令如下所示。这种操作的效果等同于强制停止sshd服务。

    ```
    [root@linuxprobe ~]# kill 2156
    ```
- <span id = x>**killall**</span>   
　　killall命令用于终止某个指定名称的服务所对应的全部进程，格式为：`killall [参数] [进程名称]`。通常来讲，复杂软件的服务程序会有多个进程协同为用户提供服务，如果逐个去结束这些进程会比较麻烦，此时可以使用killall命令来批量结束某个服务程序带有的全部进程。下面以httpd服务程序为例，来结束其全部进程。由于RHEL7系统默认没有安装httpd服务程序，因此大家此时只需看操作过程和输出结果即可，等学习了相关内容之后再来实践。
    ```
    [root@linuxprobe ~]# pidof httpd
    13581 13580 13579 13578 13577 13576
    [root@linuxprobe ~]# killall httpd
    [root@linuxprobe ~]# pidof httpd
    [root@linuxprobe ~]# 
    ```
- <span id = ifconfig>**ifconfig**</span>   
　　ifconfig命令用于获取网卡配置与网络状态等信息，格式为`ifconfig [网络设备] [参数]`。使用ifconfig命令来查看本机当前的网卡配置与网络状态等信息时，其实主要查看的就是网卡名称、inet参数后面的IP地址、ether参数后面的网卡物理地址（又称为MAC地址），以及RX、TX的接收数据包与发送数据包的个数及累计流量（即下面加粗的信息内容）：

    ```
    [root@SLAVE19 zhangfan]# ifconfig
    enp129s0f0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
            ether e8:4d:d0:c5:c0:a6  txqueuelen 1000  (Ethernet)
            RX packets 0  bytes 0 (0.0 B)
            RX errors 0  dropped 0  overruns 0  frame 0
            TX packets 0  bytes 0 (0.0 B)
            TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
            device memory 0xc8100000-c81fffff  
    
    enp129s0f1: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
            ether e8:4d:d0:c5:c0:a7  txqueuelen 1000  (Ethernet)
            RX packets 0  bytes 0 (0.0 B)
            RX errors 0  dropped 0  overruns 0  frame 0
            TX packets 0  bytes 0 (0.0 B)
            TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
            device memory 0xc8000000-c80fffff  
    
    enp2s0f0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
            inet 10.100.28.100  netmask 255.255.255.0  broadcast 10.100.28.255
            inet6 fe80::3a4c:4fff:fee7:4221  prefixlen 64  scopeid 0x20<link>
            ether 38:4c:4f:e7:42:21  txqueuelen 1000  (Ethernet)
            RX packets 284864156  bytes 2801634764530 (2.5 TiB)
            RX errors 0  dropped 152367  overruns 0  frame 0
            TX packets 1331157667  bytes 1783052082986 (1.6 TiB)
            TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
    
    enp2s0f1: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
            ether 38:4c:4f:e7:42:22  txqueuelen 1000  (Ethernet)
            RX packets 0  bytes 0 (0.0 B)
            RX errors 0  dropped 0  overruns 0  frame 0
            TX packets 0  bytes 0 (0.0 B)
            TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
    
    lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
            inet 127.0.0.1  netmask 255.0.0.0
            inet6 ::1  prefixlen 128  scopeid 0x10<host>
            loop  txqueuelen 0  (Local Loopback)
            RX packets 49231806  bytes 1289827259530 (1.1 TiB)
            RX errors 0  dropped 0  overruns 0  frame 0
            TX packets 49231806  bytes 1289827259530 (1.1 TiB)
            TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
    ```
- <span id = uname>**uname命令**</span>   
　　uname命令用于查看系统内核与系统版本等信息，格式为`uname [-a]`。在使用uname命令时，一般会固定搭配上-a参数来完整地查看当前系统的内核名称、主机名、内核发行版本、节点名、系统时间、硬件名称、硬件平台、处理器类型以及操作系统名称等信息。

    ```
    [root@SLAVE19 zhangfan]# uname -a
    Linux SLAVE19 3.10.0-327.el7.x86_64 #1 SMP Thu Oct 29 17:29:29 EDT 2015 x86_64 x86_64 x86_64 GNU/Linux
    [root@SLAVE19 zhangfan]# cat /etc/redhat-release --查看linux版本信息
    Red Hat Enterprise Linux Server release 7.2 (Maipo)
    ```
- <span id = uptime>**uptime命令**</span>   
　　uptime用于查看系统的负载信息，格式为uptime。
uptime命令真的很棒，它可以显示当前系统时间、系统已运行时间、启用终端数量以及平均负载值等信息。平均负载值指的是系统在最近1分钟、5分钟、15分钟内的压力情况（下面加粗的信息部分）；负载值越低越好，尽量不要长期超过1，在生产环境中不要超过5。

    ```
    [root@SLAVE19 zhangfan]# uptime
     16:43:16 up 3 days,  7:41,  6 users,  load average: 1.45, 1.58, 1.80
    ```
- <span id = free>**free命令**</span>   
　　free用于显示当前系统中内存的使用量信息，格式为`free [-h]`。为了保证Linux系统不会因资源耗尽而突然宕机，运维人员需要时刻关注内存的使用量。在使用free命令时，可以结合使用-h参数以更人性化的方式输出当前内存的实时使用量信息。表2-8所示为在刘遄老师的电脑上执行`free -h`命令之后的输出信息。需要注意的是，输出信息中的中文注释是作者自行添加的内容，实际输出时没有相应的参数解释。

    ```
    [root@SLAVE19 zhangfan]# free -h
                  total        used        free      shared  buff/cache   available
    Mem:           377G         11G        977M         18M        365G        365G
    Swap:           29G          0B         29G
    ```
- <span id = df>**df命令**</span>   
　　df命令用于查看整个系统存储空间的大小

    ```
    [root@SLAVE19 /]# df -h
    Filesystem      Size  Used Avail Use% Mounted on
    /dev/sda3       193G   25G  169G  13% /
    devtmpfs        189G     0  189G   0% /dev
    tmpfs           189G     0  189G   0% /dev/shm
    tmpfs           189G   18M  189G   1% /run
    tmpfs           189G     0  189G   0% /sys/fs/cgroup
    /dev/loop0      3.8G  3.8G     0 100% /iso
    /dev/sda1       194M   93M  102M  48% /boot
    /dev/sdb1        18T   14T  4.0T  78% /data
    tmpfs            38G     0   38G   0% /run/user/0
    cm_processes    189G   89M  189G   1% /run/cloudera-scm-agent/process
    ```

- <span id = du>**du命令**</span>  
　　du命令用于查看指定文件的大小

    ```
    [root@SLAVE19 caoz]# du -h zhangfan
    0	zhangfan/xdr_s1mme_unzip
    32K	zhangfan/xdr_s1mme_final
    104G	zhangfan/infovista
    1.6G	zhangfan/huasheng_app_type
    5.7G	zhangfan/YUNWEI/201711
    5.7G	zhangfan/YUNWEI
    122M	zhangfan/xdr_bj_s1uftp_zf_zip_20180103
    0	zhangfan/xdr_bj_s1uftp_zf_unzip_20180103
    111G	zhangfan
    ```

- <span id = who>**who命令**</span>   
　　`who`用于查看当前登入主机的用户终端信息，格式为`who [参数]`。这三个简单的字母可以快速显示出所有正在登录本机的用户的名称以及他们正在开启的终端信息。表2-9所示为执行`who`命令后的结果。
    ```
    [root@SLAVE19 /]# who
    root     pts/0        2018-01-08 08:23 (10.100.4.12)
    root     pts/2        2018-01-05 14:22 (10.100.4.51)
    ```
- <span id = last>**last命令**</span>    
　　`last`命令用于查看所有系统的登录记录，格式为`last [参数]`。使用last命令可以查看本机的登录记录。但是，由于这些信息都是以日志文件的形式保存在系统中，因此黑客可以很容易地对内容进行篡改。千万不要单纯以该命令的输出信息而判断系统有无被恶意入侵！

    ```
    [root@SLAVE19 /]# last
    root     pts/0        10.100.4.12      Mon Jan  8 08:23   still logged in   
    root     pts/1        10.100.34.111    Fri Jan  5 17:09 - 18:42  (01:33)    
    root     pts/0        10.100.4.8       Fri Jan  5 15:04 - 17:18  (02:13)    
    root     pts/2        10.100.4.51      Fri Jan  5 14:22   still logged in   
    root     pts/5        10.100.34.101    Fri Jan  5 14:20 - 16:45  (02:24)    
    root     pts/3        10.100.4.12      Fri Jan  5 14:19 - 17:16  (02:56)    
    root     pts/2        10.100.4.51      Fri Jan  5 14:17 - 14:22  (00:05)    
    root     pts/1        10.100.34.101    Fri Jan  5 14:08 - 16:45  (02:36)    
    root     pts/2        10.100.34.101    Fri Jan  5 14:05 - 14:05  (00:00)    
    root     pts/1        10.100.34.101    Fri Jan  5 14:01 - 14:06  (00:05)    
    root     pts/4        10.100.34.111    Fri Jan  5 12:41 - 17:21  (04:39)    
    root     pts/3        10.100.34.111    Fri Jan  5 10:52 - 13:15  (02:23)    
    root     pts/2        10.100.34.111    Fri Jan  5 10:40 - 13:01  (02:20)    
    root     pts/1        10.100.34.111    Fri Jan  5 10:18 - 12:42  (02:23)    
    root     pts/0        10.100.35.37     Fri Jan  5 09:58 - 14:39  (04:40)    
    root     pts/1        10.100.34.111    Fri Jan  5 09:03 - 10:17  (01:14)    
    ```
- <span id = history>**history命令**</span>    
　　`history`命令用于显示历史执行过的命令，格式为`history [-c]`。`history`命令应该是作者最喜欢的命令。执行`history`命令能显示出当前用户在本地计算机中执行过的最近1000条命令记录。如果觉得1000不够用，还可以自定义`/etc/profile`文件中的HISTSIZE变量值。在使用`history`命令时，如果使用-c参数则会清空所有的命令历史记录。还可以使用“!编码数字”的方式来重复执行某一次的命令。总之，`history`命令有很多有趣的玩法等待您去开发。
    ```
    [root@SLAVE19 /]# history
       29  du -sh *
       30   ifconfig
       31  cd caoz/
       32  ll
       33  du -sh *
       34  cd zhangfan
       35  ll
       36  du -sh *
       37  cd xdr_s1mme_final
       38  ll
       39  du -sh *
       40      exit
       41  cd /data/
       42  ll
       43  du -sh
       44  du -sh *
       ...
    ```
- <span id = sosreport>**sosreport命令**</span>  
　　`sosreport`命令用于收集系统配置及架构信息并输出诊断文档，格式为sosreport。当Linux系统出现故障需要联系技术支持人员时，大多数时候都要先使用这个命令来简单收集系统的运行状态和服务配置信息，以便让技术支持人员能够远程解决一些小问题，亦或让他们能提前了解某些复杂问题。在下面的输出信息中，加粗的部分是收集好的资料压缩文件以及校验码，将其发送给技术支持人员即可：

    ```
    [root@linuxprobe ~]# sosreport
    sosreport (version 3.0)
    This command will collect diagnostic and configuration information from
    this Red Hat Enterprise Linux system and installed applications.
    
    An archive containing the collected information will be generated in
    /var/tmp and may be provided to a Red Hat support representative.
    Any information provided to Red Hat will be treated in accordance with
    the published support policies at:
    https://access.redhat.com/support/
    The generated archive may contain data considered sensitive and its
    content should be reviewed by the originating organization before being
    passed to any third party.
    
    No changes will be made to system configuration.
    Press ENTER to continue, or CTRL-C to quit. 此处敲击回车来确认收集信息
    
    Please enter your first initial and last name [linuxprobe.com]: 此处敲击回车来确认主机编号
    Please enter the case number that you are generating this report for: 此处敲击回车来确认主机编号
    
    Running plugins. Please wait ...
    Running 70/70: yum...
    Creating compressed archive...
    Your sosreport has been generated and saved in:
    
    /var/tmp/sosreport-linuxprobe.com-20170905230631.tar.xz
    The checksum is: 79436cdf791327040efde48c452c6322
    Please send this file to your support representative.
    ```