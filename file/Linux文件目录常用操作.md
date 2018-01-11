## 常用文件和目录操作
---
### 命令索引
- [pwd](#pwd)：查看当前所在目录
- [cd](#cd)：切换工作目录
- [ls](#ls)：显示文件
- [cat](#cat)：查看文件内容
- [more](#more)：翻页模式查看文件内容
- [head](#head)：查看文件前几行
- [tail](#tail)：查看文件的后几行
- [tr](#tr)：字符替换
- [wc](#wc)：文本统计
- [stat](#stat)：查看文件存储信息和时间信息
- [cut](#cut)：按列提取文本
- [diff](#diff)：比较文件的异同
- [touch](#touch)：创建空白文件或设置文件的时间
- [mkdir](#mkdir)：建立新文件
- [cp](#cp)：文件复制
- [mv](#mv)：剪切或重命名文件
- [rm](#rm)：删除文件
- [dd](#dd)：按照指定大小和个数的数据块来复制文件或转换文件
- [file](#file)：查看文件类型
- [tar](#tar)：压缩或解压文件
- [grep](#grep)：按关键词搜索文件
- [find](#find)：按条件查找文件
---

- <span id = pwd>**pwd命令**</span>  
　　pwd命令用于显示用户当前所处的工作目录，格式为`pwd [选项]`。
    
    ```
    [root@SLAVE19 caoz]# pwd
     /data/caoz
    ```
- <span id = cd>**cd命令**</span>  
　　cd命令用于切换工作路径，格式为`cd [目录名称]`。
这个命令应该是最常用的一个Linux命令了。可以通过cd命令迅速、灵活地切换到不同的工作目录。除了常见的切换目录方式，还可以使用`cd -`命令返回到上一次所处的目录，使用`cd..`命令进入上级目录，以及使用`cd ~`命令切换到当前用户的家目录，亦或使用`cd ~username`切换到其他用户的家目录。例如，可以使用`cd 路径`的方式切换进/etc目录中：

- <span id = ls>**ls命令**</span>  
　　ls命令用于显示目录中的文件信息，格式为`ls [选项] [文件]` 。所处的工作目录不同，当前工作目录下的文件肯定也不同。使用ls命令的`-a`参数看到全部文件（包括隐藏文件），使用`-l`参数可以查看文件的属性、大小等详细信息。将这两个参数整合之后，再执行ls命令即可查看当前目录中的所有文件并输出这些文件的属性信息：

    ```
    [root@SLAVE19 caoz]# ls -al
    total 160
    drwx------ 17 caoz caoz  4096 Jan  4 13:34 .
    drwxr-xr-x 12 root root  4096 Jan  5 14:19 ..
    -rwxrwxrwx  1 caoz caoz  1173 Sep 25 16:23 0-all-HDFS-Import.sh
    -rwxrwxrwx  1 caoz caoz   257 Sep 26 12:31 0-dpi-HDFS-Import.sh
    -rwxrwxrwx  1 caoz caoz  1317 Sep  6 17:34 1-all-Create_mtable.sh
    -rwxrwxrwx  1 caoz caoz   565 Sep 26 12:33 1-dpi-Create_mtable.sh
    -rwxrwxrwx  1 caoz caoz  2667 Sep  6 17:42 2-all-Preparation.sh
    -rwxrwxrwx  1 caoz caoz  1083 Sep  7 14:50 3-all-insertflag.sh
    -rw-------  1 caoz caoz 46534 Jan  4 13:34 .bash_history
    -rw-r--r--  1 caoz caoz    18 Jul  8  2015 .bash_logout
    -rw-r--r--  1 caoz caoz   193 Jul  8  2015 .bash_profile
    -rw-r--r--  1 caoz caoz   231 Jul  8  2015 .bashrc
    drwxrwxr-x  3 caoz caoz    25 Sep  6 16:38 .cache
    ...
    ```


- <span id = cat>**cat命令**</span>  
　　cat命令用于查看纯文本文件（内容较少的），格式为“cat [选项] [文件]”。Linux系统中有多个用于查看文本内容的命令，每个命令都有自己的特点，比如这个cat命令就是用于查看内容较少的纯文本文件的。cat这个命令也很好记，因为cat在英语中是“猫”的意思，小猫咪是不是给您一种娇小、可爱的感觉呢？  
　　如果在查看文本内容时还想顺便显示行号的话，不妨在cat命令后面追加一个-n参数：

    ```
    [root@SLAVE19 zhangfan]# cat -n unzip_zf_poolmap.py 
         1	# coding:utf-8
         2	import os
         3	import glob
         4	import tarfile
         5	from multiprocessing import Pool
         6	import time
         7	
         8	def unzip_file(file):
         9	    target_path = './xdr_bj_s1uftp_zf_unzip_20180103'
        10	    try:
        11	        tar = tarfile.open(file)
        12	        tar.extractall(target_path)
        13	        tar.close()
        14	    except Exception as e:
        15	        print('Exception:',e)
        16	    
        17	if __name__ == "__main__":
        18	    print ("start extract")
    ```

- <span id = more>**more命令**</span>  
　　more命令用于查看纯文本文件（内容较多的），格式为`more [选项]文件`。  
　　如果需要阅读长篇小说或者非常长的配置文件，那么“小猫咪”可就真的不适合了。因为一旦使用cat命令阅读长篇的文本内容，信息就会在屏幕上快速翻滚，导致自己还没有来得及看到，内容就已经翻篇了。因此对于长篇的文本内容，推荐使用more命令来查看。more命令会在最下面使用百分比的形式来提示您已经阅读了多少内容。您还可以使用空格键或回车键向下翻页：

    ```
    [root@linuxprobe ~]# more initial-setup-ks.cfg 
    #version=RHEL7
    # X Window System configuration information
    xconfig  --startxonboot
    
    # License agreement
    eula --agreed
    # System authorization information
    auth --enableshadow --passalgo=sha512
    # Use CDROM installation media
    cdrom
    # Run the Setup Agent on first boot
    firstboot --enable
    # Keyboard layouts
    keyboard --vckeymap=us --xlayouts='us'
    # System language
    lang en_US.UTF-8
    
    ignoredisk --only-use=sda
    # Network information
    network  --bootproto=dhcp --device=eno16777728 --onboot=off --ipv6=auto
    network  --bootproto=dhcp --hostname=linuxprobe.com
    --More--(43%)
    
    ```

- <span id = head>**head命令**</span>  
　　head命令用于查看纯文本文档的前N行，格式为`head [选项] [文件]`。  
　　在阅读文本内容时，谁也难以保证会按照从头到尾的顺序往下看完整个文件。如果只想查看文本中前20行的内容，该怎么办呢？head命令可以派上用场了：
    ```
    [root@linuxprobe ~]# head -n 20 initial-setup-ks.cfg 
    #version=RHEL7
    # X Window System configuration information
    xconfig  --startxonboot
    
    # License agreement
    eula --agreed
    # System authorization information
    auth --enableshadow --passalgo=sha512
    # Use CDROM installation media
    cdrom
    # Run the Setup Agent on first boot
    firstboot --enable
    # Keyboard layouts
    keyboard --vckeymap=us --xlayouts='us'
    # System language
    lang en_US.UTF-8
    
    ignoredisk --only-use=sda
    # Network information
    network  --bootproto=dhcp --device=eno16777728 --onboot=off --ipv6=auto
    ```

- <span id = tail>**tail命令**</span>  
　　tail命令用于查看纯文本文档的后N行或持续刷新内容，格式为`tail [选项] [文件]`。  
　　我们可能还会遇到另外一种情况，比如需要查看文本内容的最后20行，这时就需要用到tail命令了。tail命令的操作方法与head命令非常相似，只需要执行`tail -n 20 文件名 `命令就可以达到这样的效果。tail命令最强悍的功能是可以持续刷新一个文件的内容，当想要实时查看最新日志文件时，这特别有用，此时的命令格式为`tail -f 文件名`：

    ```
    [root@linuxprobe ~]# tail -f /var/log/messages
    May  4 07:56:38 localhost gnome-session: Window manager warning: Log level 16: 
    STACK_OP_ADD: window 0x1e00001 already in stack
    May  4 07:56:38 localhost gnome-session: Window manager warning: Log level 16: 
    STACK_OP_ADD: window 0x1e00001 already in stack
    May  4 07:56:38  localhost  vmusr[12982]: [ warning] [Gtk] gtk_disable_setlocale()
    must be called before gtk_init()
    May  4 07:56:50 localhost systemd-logind: Removed session c1.
    Aug  1 01:05:31 localhost systemd: Time has been changed
    Aug  1 01:05:31 localhost systemd: Started LSB: Bring up/down networking.
    Aug  1 01:08:56 localhost dbus-daemon: dbus[1124]: [system] Activating service 
    name='com.redhat.SubscriptionManager' (using servicehelper)
    Aug  1 01:08:56 localhost dbus[1124]: [system] Activating service name='com.
    redhat.SubscriptionManager' (using servicehelper)
    Aug  1 01:08:57 localhost dbus-daemon: dbus[1124]: [system] Successfully activated
    service 'com.redhat.SubscriptionManager'
    Aug  1 01:08:57 localhost dbus[1124]: [system] Successfully activated service '
    com.redhat.SubscriptionManager'
    ```


- <span id = tr>**tr命令**</span>  
　　tr命令用于替换文本文件中的字符，格式为`tr [原始字符] [目标字符]`。  
　　在很多时候，我们想要快速地替换文本中的一些词汇，又或者把整个文本内容都进行替换，如果进行手工替换，难免工作量太大，尤其是需要处理大批量的内容时，进行手工替换更是不现实。这时，就可以先使用cat命令读取待处理的文本，然后通过管道符（详见第3章）把这些文本内容传递给tr命令进行替换操作即可。例如，把某个文本内容中的英文全部替换为大写：

    ```
    [root@SLAVE19 IUCS_bj_zf_final_20171219]# cat test.txt | tr [a-z] [A-Z] 
     ABCDEFGHIJKLMNOPQRSTUVWXYZ
    ```

- <span id = wc>**wc命令**</span>  
　　wc命令用于统计指定文本的行数、字数、字节数，格式为`wc [参数] 文本`。  
　　每次我在课堂上讲到这个命令时，总有同学会联想到一种公共设施，其实这两者毫无关联。Linux系统中的wc命令用于统计文本的行数、字数、字节数等。如果为了方便自己记住这个命令的作用，也可以联想到上厕所时好无聊，无聊到数完了手中的如厕读物上有多少行字。  
　　wc的参数以及相应的作用如下表所示所示：

    参数 | 作用
    :---:|:---:
    `-l` | 只显示行数
    `-w` | 只显示单词数
    `-c` | 只显示字节数
    　　在Linux系统中，passwd是用于保存系统账户信息的文件，要统计当前系统中有多少个用户，可以使用下面的命令来进行查询，是不是很神奇：
    
    ```
    [root@SLAVE19 /]# wc -l /etc/passwd
    53 /etc/passwd
    ```

- <span id = stat>**stat命令**</span>  
　　stat命令用于查看文件的具体存储信息和时间等信息，格式为`stat 文件名称`。  
　　stat命令可以用于查看文件的存储信息和时间等信息，命令`stat anaconda-ks.cfg`会显示出文件的三种时间状态（已加粗）：Access、Modify、Change。这三种时间的区别将在下面的touch命令中详细详解：
    
    ```
    [root@SLAVE19 zhangfan]# stat unzip_zf_poolmap.py 
      
      File: unzip_zf_poolmap.py
      Size: 721       	Blocks: 8          IO Block: 4096   regular file
    Device: 811h/2065d	Inode: 26777764063  Links: 1
    Access: (0777/-rwxrwxrwx)  Uid: (    0/    root)   Gid: (    0/    root)
    Access: 2018-01-08 16:02:08.066130412 +0800
    Modify: 2018-01-04 16:09:26.821086718 +0800
    Change: 2018-01-04 16:09:31.418068284 +0800
     Birth: -
    ```
- <span id = cut>**cut命令**</span>  
　　cut命令用于按“列”提取文本字符，格式为`cut [参数] 文本`。
在Linux系统中，如何准确地提取出最想要的数据，这也是我们应该重点学习的内容。一般而言，按基于“行”的方式来提取数据是比较简单的，只需要设置好要搜索的关键词即可。但是如果按列搜索，不仅要使用`-f`参数来设置需要看的列数，还需要使用`-d`参数来设置间隔符号。passwd在保存用户数据信息时，用户信息的每一项值之间是采用冒号来间隔的，接下来我们使用下述命令尝试提取出passwd文件中的用户名信息，即提取以冒号`：`为间隔符号的第一列内容：
    ```
    [root@SLAVE19 zhangfan]# cut -f1 -d: /etc/passwd
    root
    bin
    daemon
    adm
    lp
    sync
    shutdown
    halt
    mail
    operator
    ---部分信息未显示---
    ```
- <span id = diff>**diff命令**</span>  
　　diff命令用于比较多个文本文件的差异，格式为`diff [参数] 文件`。在使用diff命令时，不仅可以使用`--brief`参数来确认两个文件是否不同，还可以使用`-c`参数来详细比较出多个文件的差异之处，这绝对是判断文件是否被篡改的有力神器。例如，先使用cat命令分别查看`diff_A.txt`和`diff_B.txt`文件的内容，然后进行比较：
    
    ```
    [root@SLAVE19 zhangfan]# diff -c diff_A.txt diff_B.txt
    *** diff_A.txt	2018-01-09 09:49:18.121400861 +0800
    --- diff_B.txt	2018-01-09 09:42:09.120133445 +0800
    ***************
    *** 1 ****
    ! 123456344
    --- 1 ----
    ! 123456
    ```

- <span id = touch>**touch命令**</span>  
　　touch命令用于创建空白文件或设置文件的时间，格式为`touch [选项] [文件]`。在创建空白的文本文件方面，这个touch命令相当简捷，简捷到没有必要铺开去讲。比如，touch linuxprobe命令可以创建出一个名为linuxprobe的空白文本文件。对touch命令来讲，有难度的操作主要是体现在设置文件内容的修改时间（mtime）、文件权限或属性的更改时间（ctime）与文件的读取时间（atime）上面。touch命令的参数及其作用如下表所示:

    参数 | 作用
    :---:|:---:
    `-a` | 仅修改“读取时间”（atime）
    `-m` | 仅修改“修改时间”（mtime）
    `-d` | 同时修改atime与mtime
    　　接下来，我们先使用ls命令查看一个文件的修改时间，然后修改这个文件，最后再通过touch命令把修改后的文件时间设置成修改之前的时间（很多黑客就是这样做的呢）：

    ```
    [root@linuxprobe ~]# ls -l anaconda-ks.cfg 
    -rw-------. 1 root root 1213 May  4 15:44 anaconda-ks.cfg
    [root@linuxprobe ~]# echo "Visit the LinuxProbe.com to learn linux skills" >> 
    anaconda-ks.cfg
    [root@linuxprobe ~]# ls -l anaconda-ks.cfg
    -rw-------. 1 root root 1260 Aug  2 01:26 anaconda-ks.cfg
    [root@linuxprobe ~]# touch -d "2017-05-04 15:44" anaconda-ks.cfg 
    [root@linuxprobe ~]# ls -l anaconda-ks.cfg 
    -rw-------. 1 root root 1260 May  4 15:44 anaconda-ks.cfg
    ```
- <span id = mkdir>**mkdir命令**</span>  
　　mkdir命令用于创建空白的目录，格式为`mkdir [选项] 目录`。
在Linux系统中，文件夹是最常见的文件类型之一。除了能创建单个空白目录外，mkdir命令还可以结合`-p`参数来递归创建出具有嵌套叠层关系的文件目录。
    
    ```
    [root@linuxprobe ~]# mkdir linuxprobe
    [root@linuxprobe ~]# cd linuxprobe
    [root@linuxprobe linuxprobe]# mkdir -p a/b/c/d/e
    [root@linuxprobe linuxprobe]# cd a
    [root@linuxprobe a]# cd b
    [root@linuxprobe b]#
    ```

- <span id = cp>**cp命令**</span>  
　　cp命令用于复制文件或目录，格式为`cp [选项] 源文件 目标文件`。大家对文件复制操作应该不陌生，在Linux系统中，复制操作具体分为3种情况：  
　　如果目标文件是目录，则会把源文件复制到该目录中；  
　　如果目标文件也是普通文件，则会询问是否要覆盖它；  
　　如果目标文件不存在，则执行正常的复制操作。  
　　cp命令的参数及其作用如表所示。

    参数 | 作用
    :---:|:---:
    `-p` | 保留原始文件的属性
    `-d` | 若对象为“链接文件”，则保留该“链接文件”的属性
    `-r` | 递归持续复制（用于目录）
    `-i` | 若目标文件存在则询问是否覆盖
    `-a` | 相当于-pdr（p、d、r为上述参数）
    接下来，使用touch创建一个名为install.log的普通空白文件，然后将其复制为一份名为x.log的备份文件，最后再使用ls命令查看目录中的文件：
    
    ```
    [root@linuxprobe ~]# touch install.log
    [root@linuxprobe ~]# cp install.log x.log
    [root@linuxprobe ~]# ls
    install.log x.log
    ```
- <span id = mv>**mv命令**</span>  
　　mv命令用于剪切文件或将文件重命名，格式为`mv [选项] 源文件 [目标路径|目标文件名]`。剪切操作不同于复制操作，因为它会默认把源文件删除掉，只保留剪切后的文件。如果在同一个目录中对一个文件进行剪切操作，其实也就是对其进行重命名：
    
    ```
    [root@linuxprobe ~]# mv x.log linux.log
    [root@linuxprobe ~]# ls
    install.log linux.log
    ```


- <span id = rm>**rm命令**</span>  
　　rm命令用于删除文件或目录，格式为`rm [选项] 文件`。
在Linux系统中删除文件时，系统会默认向您询问是否要执行删除操作，如果不想总是看到这种反复的确认信息，可在rm命令后跟上`-f`参数来强制删除。另外，想要删除一个目录，需要在rm命令后面一个`-r`，否则删除不掉。我们来尝试删除前面创建的install.log和linux.log文件：

    ```
    [root@linuxprobe ~]# rm install.log
    rm: remove regular empty file ‘install.log’? y
    [root@linuxprobe ~]# rm -f linux.log
    [root@linuxprobe ~]# ls
    [root@linuxprobe ~]#
    ```
- <span id = dd>**dd命令**</span>  
　　dd命令用于按照指定大小和个数的数据块来复制文件或转换文件，格式为`dd [参数]`。  
　　dd命令是一个比较重要而且比较有特色的一个命令，它能够让用户按照指定大小和个数的数据块来复制文件的内容。当然如果愿意的话，还可以在复制过程中转换其中的数据。Linux系统中有一个名为`/dev/zero`的设备文件，每次在课堂上解释它时都充满哲学理论的色彩。因为这个文件不会占用系统存储空间，但却可以提供无穷无尽的数据，因此可以使用它作为dd命令的输入文件，来生成一个指定大小的文件。dd命令的参数及其作用如表:

    参数 | 作用
    :---:|:---:
    `if` | 输入文件的名称
    `of` | 输出的文件名称
    `bs` | 设置每个“块”的大小
    `count` | 设置要复制“块”的个数
    
  　　例如我们可以用dd命令从/dev/zero设备文件中取出一个大小为560MB的数据块，然后保存成名为560_file的文件。在理解了这个命令后，以后就能随意创建任意大小的文件了：  
  　　
    ```
    [root@SLAVE19 zhangfan]# dd if=/dev/zero of=test bs=200M count=3
    3+0 records in
    3+0 records out
    629145600 bytes (629 MB) copied, 0.497356 s, 1.3 GB/s
    ```
   　　 dd命令的功能也绝不仅限于复制文件这么简单。如果您想把光驱设备中的光盘制作成iso格式的镜像文件，在Windows系统中需要借助于第三方软件才能做到，但在Linux系统中可以直接使用dd命令来压制出光盘镜像文件，将它变成一个可立即使用的iso镜像：
    
    ```
    [root@linuxprobe ~]# dd if=/dev/cdrom of=RHEL-server-7.0-x86_64-LinuxProbe.Com.iso
    7311360+0 records in
    7311360+0 records out
    3743416320 bytes (3.7 GB) copied, 370.758 s, 10.1 MB/s
    ```
    　　考虑到有些读者会纠结bs块大小与count块个数的关系，下面举一个吃货的例子进行解释。假设小明的饭量（即需求）是一个固定的值，用来盛饭的勺子的大小即bs块大小，而用勺子盛饭的次数即count块个数。小明要想吃饱（满足需求），则需要在勺子大小（bs块大小）与用勺子盛饭的次数（count块个数）之间进行平衡。勺子越大，用勺子盛饭的次数就越少。有上可见，bs与count都是用来指定容量的大小，只要能满足需求，可随意组合搭配方式。

- <span id = file>**file命令**</span>  
　　file命令用于查看文件的类型，格式为`file 文件名`。
在Linux系统中，由于文本、目录、设备等所有这些一切都统称为文件，而我们又不能单凭后缀就知道具体的文件类型，这时就需要使用file命令来查看文件类型了。

    ```
    [root@linuxprobe ~]# file anaconda-ks.cfg 
    anaconda-ks.cfg: ASCII text
    [root@linuxprobe ~]# file /dev/sda
    /dev/sda: block special
    ```

- <span id = tar>**tar命令**</span>  
  　　tar命令用于对文件进行打包压缩或解压，格式为`tar [选项] [文件]`。在Linux系统中，常见的文件格式比较多，其中主要使用的是`.tar`或`.tar.gz`或`.tar.bz2`格式，我们不用担心格式太多而记不住，其实这些格式大部分都是由tar命令来生成的。刘遄老师将讲解最重要的几个参数，以方便大家理解。tar命令的参数及其作用如表所示：

    参数 | 作用
    :---:|:---:
    `-c` | 创建压缩文件
    `-x` | 解开压缩文件
    `-t` | 查看压缩包内有哪些文件
    `-z` | 用Gzip压缩或解压
    `-j` | 用bzip2压缩或解压
    `-v` | 显示压缩或解压的过程
    `-f` | 目标文件名
    `-p` | 保留原始的权限与属性
    `-P` | 使用绝对路径来压缩
    `-C` | 指定解压到的目录
  
  　　首先，`-c`参数用于创建压缩文件，`-x`参数用于解压文件，因此这两个参数不能同时使用。其次，`-z`参数指定使用Gzip格式来压缩或解压文件，`-j`参数指定使用`bzip2`格式来压缩或解压文件。用户使用时则是根据文件的后缀来决定应使用何种格式参数进行解压。在执行某些压缩或解压操作时，可能需要花费数个小时，如果屏幕一直没有输出，您一方面不好判断打包的进度情况，另一方面也会怀疑电脑死机了，因此非常推荐使用-v参数向用户不断显示压缩或解压的过程。`-C`参数用于指定要解压到哪个指定的目录。`-f`参数特别重要，它必须放到参数的最后一位，代表要压缩或解压的软件包名称。刘遄老师一般使用`tar -czvf 压缩包名称.tar.gz 要打包的目录`命令把指定的文件进行打包压缩；相应的解压命令为`tar -xzvf 压缩包名称.tar.gz`。下面我们来逐个演示下打包压缩与解压的操作。先使用`tar`命令把`/etc`目录通过`gzip`格式进行打包压缩，并把文件命名为`etc.tar.gz`：  
  　　
    ```
    [root@linuxprobe ~]# tar -czvf etc.tar.gz /etc
    tar: Removing leading '/' from member names
    /etc/
    /etc/fstab
    /etc/crypttab
    /etc/mtab
    /etc/fonts/
    /etc/fonts/conf.d/
    /etc/fonts/conf.d/65-0-madan.conf
    /etc/fonts/conf.d/59-liberation-sans.conf
    /etc/fonts/conf.d/90-ttf-arphic-uming-embolden.conf
    /etc/fonts/conf.d/59-liberation-mono.conf
    /etc/fonts/conf.d/66-sil-nuosu.conf
    ………………省略部分压缩过程信息………………
    ```
    接下来将打包后的压缩包文件指定解压到`/root/etc`目录中（先使用`mkdir`命令来创建`/root/etc`目录）：
    
    ```
    [root@linuxprobe ~]# mkdir /root/etc
    [root@linuxprobe ~]# tar xzvf etc.tar.gz -C /root/etc
    etc/
    etc/fstab
    etc/crypttab
    etc/mtab
    etc/fonts/
    etc/fonts/conf.d/
    etc/fonts/conf.d/65-0-madan.conf
    etc/fonts/conf.d/59-liberation-sans.conf
    etc/fonts/conf.d/90-ttf-arphic-uming-embolden.conf
    etc/fonts/conf.d/59-liberation-mono.conf
    etc/fonts/conf.d/66-sil-nuosu.conf
    etc/fonts/conf.d/65-1-vlgothic-gothic.conf
    etc/fonts/conf.d/65-0-lohit-bengali.conf
    etc/fonts/conf.d/20-unhint-small-dejavu-sans.conf
    ………………省略部分解压过程信息………………
    ```

- <span id = grep>**grep命令**</span>  
　　grep命令用于在文本中执行关键词搜索，并显示匹配的结果，格式为`grep [选项] [文件]`。grep命令的参数及其作用如表所示:

    参数 | 作用
    :---:|:---:
    -b | 将可执行文件（binary）当作文本文件（text）来搜索
    -c | 仅显示找到的行数
    -i | 忽略大小写
    -n | 显示行号
    -v | 反向选择—仅列出没有“关键词”的行
    
    grep命令是用途最广泛的文本搜索匹配工具，虽然有很多参数，但是大多数基本上都用不到。刘遄老师在总结了近10年的运维工作和培训教学的经验后，提出的本书的写作理念“去掉不实用”绝对不是信口开河。如果一名IT培训讲师的水平只能停留在“技术的搬运工”层面，而不能对优质技术知识进行提炼总结，那对他的学生来讲绝非好事。我们在这里只讲两个最最常用的参数：`-n`参数用来显示搜索到信息的行号；`-v`参数用于反选信息（即没有包含关键词的所有信息行）。这两个参数几乎能完成您日后80%的工作需要，至于其他上百个参数，即使以后在工作期间遇到了，再使用`man grep`命令查询也来得及。  
    　　在Linux系统中，`/etc/passwd`文件是保存着所有的用户信息，而一旦用户的登录终端被设置成`/sbin/nologin`，则不再允许登录系统，因此可以使用grep命令来查找出当前系统中不允许登录系统的所有用户信息：
    
    ```
    [root@linuxprobe ~]# grep /sbin/nologin /etc/passwd
    bin:x:1:1:bin:/bin:/sbin/nologin
    daemon:x:2:2:daemon:/sbin:/sbin/nologin
    adm:x:3:4:adm:/var/adm:/sbin/nologin
    lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
    mail:x:8:12:mail:/var/spool/mail:/sbin/nologin
    operator:x:11:0:operator:/root:/sbin/nologin
    ………………省略部分输出过程信息………………
    ```

- <span id = find>**find命令**</span>  
　　find命令用于按照指定条件来查找文件，格式为`find [查找路径] 寻找条件 操作`。本书中曾经多次提到Linux系统中的一切都是文件，接下来就要见证这句话的分量了。在Linux系统中，搜索工作一般都是通过find命令来完成的，它可以使用不同的文件特性作为寻找条件（如文件名、大小、修改时间、权限等信息），一旦匹配成功则默认将信息显示到屏幕上。find命令的参数以及作用如表:
    参数 | 作用
    :---:|:---:
    `-name` | 匹配名称
    `-perm` | 匹配权限（mode为完全匹配，-mode为包含即可）
    `-user` | 匹配所有者
    `-group` | 匹配所有组
    `-mtime -n +n`| 匹配修改内容的时间（-n指n天以内，+n指n天以前）
    `-atime -n +n`| 匹配访问文件的时间（-n指n天以内，+n指n天以前）
    `-ctime -n +n`| 匹配修改文件权限的时间（-n指n天以内，+n指n天以前）
    `-nouser`| 匹配无所有者的文件
    `-nogroup`| 匹配无所有组的文件
    `-newer f1 !f2`| 匹配比文件f1新但比f2旧的文件
    `--type b/d/c/p/l/f`| 匹配文件类型（后面的字母参数依次表示块设备、目录、字符设备、管道、链接文件、文本文件）
    `-size`| 匹配文件的大小（+50KB为查找超过50KB的文件，而-50KB为查找小于50KB的文件）
    `-prune`| 忽略某个目录
    `-exec …… {}\`| 后面可跟用于进一步处理搜索结果的命令（下文会有演示）  
     -|-
    
    这里需要重点讲解一下`-exec`参数重要的作用。这个参数用于把find命令搜索到的结果交由紧随其后的命令作进一步处理，它十分类似于第3章将要讲解的管道符技术，并且由于find命令对参数的特殊要求，因此虽然exec是长格式形式，但依然只需要一个减号（-）。根据文件系统层次标准（Filesystem Hierarchy Standard）协议，Linux系统中的配置文件会保存到/etc目录中（详见第6章）。如果要想获取到该目录中所有以host开头的文件列表，可以执行如下命令：

    ```
    [root@linuxprobe ~]# find /etc -name "host*" -print
    /etc/avahi/hosts
    /etc/host.conf
    /etc/hosts
    /etc/hosts.allow
    /etc/hosts.deny
    /etc/selinux/targeted/modules/active/modules/hostname.pp
    /etc/hostname
    ```
    如果要在整个系统中搜索权限中包括SUID权限的所有文件（详见第5章），只需使用-4000即可：
    
    ```
    [root@linuxprobe ~]# find / -perm -4000 -print
    /usr/bin/fusermount
    /usr/bin/su
    /usr/bin/umount
    /usr/bin/passwd
    /usr/sbin/userhelper
    /usr/sbin/usernetctl
    ………………省略部分输出信息………………
    ```
