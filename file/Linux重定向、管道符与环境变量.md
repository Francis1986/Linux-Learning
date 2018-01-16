# 索引
- [输入与输出重定向](#1)
- [管道符](#2)
- [转义符](#3)
- [环境变量](#4)


# <span id = 1>**输入与输出重定向**</span>   
简而言之，输入重定向是指把文件导入到命令中，而输出重定向则是指把原本要输出到屏幕的数据信息写入到指定文件中。在日常的学习和工作中，相较于输入重定向，我们使用输出重定向的频率更高，所以又将输出重定向分为了标准输出重定向和错误输出重定向两种不同的技术，以及清空写入与追加写入两种模式。输入输出重定向的标准模式为：
- **标准输入重定向（STDIN，文件描述符为0）**：默认从键盘输入，也可从其他文件或命令中输入。
- **标准输出重定向（STDOUT，文件描述符为1）**：默认输出到屏幕。
- **错误输出重定向（STDERR，文件描述符为2）**：默认输出到屏幕。

输入重定向的标准格式如下表：

符号 | 作用
:---:|:---:
`命令 < 文件` | 将文件作为命令的标准输入
`命令 << 分界符` | 从标准输入中读入，直到遇见分界符才停止
`命令 < 文件1 > 文件2`|将文件1作为命令的标准输入并将标准输出到文件2
示例：

```
[root@SLAVE19 ~]# wc -l < test.md
16
```
输出重定向的标准格式如下表：

符号 | 作用
:---:|:---
`命令 > 文件`|将标准输出重定向到一个文件中（清空原有文件的数据）
`命令 2> 文件`|将错误输出重定向到一个文件中（清空原有文件的数据）
`命令 >> 文件`|将标准输出重定向到一个文件中（追加到原有内容的后面）
`命令 2>> 文件`|将错误输出重定向到一个文件中（追加到原有内容的后面）
`命令 >> 文件 2>&1`或`命令&>>文件`|将标准输出与错误输出共同写入到文件中（追加到原有内容的后面）

示例：
- 将标准输出重定向到一个文件中（清空原有文件的数据）
```
[root@SLAVE19 ~]# ls > test.md
[root@SLAVE19 ~]# cat test.md
anaconda-ks.cfg
APP_BJ.csv
HS_USER_APP_BJ.csv
imei_ci_jingweidu.csv
imei_ci_jingweidu_nx.csv
phone_attach.csv
sjd_zhibo_me_dis_6pro.csv
sjd_zhibo_me_dis_bj.csv
sjd_zhibo_me_dis_fj.csv
sjd_zhibo_me_dis_hen.csv
sjd_zhibo_me_dis_nx.csv
sjd_zhibo_me_dis_sc.csv
sjd_zhibo_me_dis_sx.csv
test
test.md
```
- 将错误输出重定向到一个文件中（清空原有文件的数据）
```
[root@SLAVE19 ~]# ls rr.txt 2> test.md  #rr.txt文件不存在
[root@SLAVE19 ~]# cat test.md
ls: cannot access rr.txt: No such file or directory
```
- 将标准输出重定向到一个文件中（追加到原有内容的后面）
```
[root@SLAVE19 ~]# ls >> test.md
[root@SLAVE19 ~]# cat test.md
ls: cannot access rr.txt: No such file or directory
anaconda-ks.cfg
APP_BJ.csv
HS_USER_APP_BJ.csv
imei_ci_jingweidu.csv
imei_ci_jingweidu_nx.csv
phone_attach.csv
sjd_zhibo_me_dis_6pro.csv
sjd_zhibo_me_dis_bj.csv
sjd_zhibo_me_dis_fj.csv
sjd_zhibo_me_dis_hen.csv
sjd_zhibo_me_dis_nx.csv
sjd_zhibo_me_dis_sc.csv
sjd_zhibo_me_dis_sx.csv
test
test.md
```
- 将错误输出重定向到一个文件中（追加到原有内容的后面）
```
[root@SLAVE19 ~]# ls ddd.txt 2>> test.md  #dd.txt文件不存在
[root@SLAVE19 ~]# cat test.md
ls: cannot access rr.txt: No such file or directory
anaconda-ks.cfg
APP_BJ.csv
HS_USER_APP_BJ.csv
imei_ci_jingweidu.csv
imei_ci_jingweidu_nx.csv
phone_attach.csv
sjd_zhibo_me_dis_6pro.csv
sjd_zhibo_me_dis_bj.csv
sjd_zhibo_me_dis_fj.csv
sjd_zhibo_me_dis_hen.csv
sjd_zhibo_me_dis_nx.csv
sjd_zhibo_me_dis_sc.csv
sjd_zhibo_me_dis_sx.csv
test
test.md
ls: cannot access ddd.txt: No such file or directory
```

# <span id = 2>**管道符**</span>
形式

```
命令1 | 命令2 |...|命令n
```
含义：管道符右侧的命令将管道符左侧的命令输出结果作为输入
示例1：查询当前目录中文件个数

```
[root@SLAVE19 /]# ls | wc -l
23
```
示例2：修改用户密码  
注：在修改用户密码时，通常都需要输入两次密码以进行确认，这在编写自动化脚本时将成为一个非常致命的缺陷。通过把管道符和passwd命令的--stdin参数相结合，我们可以用一条命令来完成密码重置操作：
```
[root@linuxprobe ~]# echo "linuxprobe" | passwd --stdin root
Changing password for user root.
passwd: all authentication tokens updated successfully.
```

# <span id = 3>**转义符**</span>
最常用的转移符：  
- **反斜杠（\）**：使反斜杠后面的一个变量变为单纯的字符串。  
- **单引号（''）**：转义其中所有的变量为单纯的字符串。  
- **双引号（""）**：保留其中的变量属性，不进行转义处理。  
- **反引号（``）**：把其中的命令执行后返回结果。

示例1：$$本来是显示当前程序的进程ID号，如果想输出$，就必须加转移符`\`
```
[root@SLAVE19 /]# price=5
[root@SLAVE19 /]# echo Price is $$price
Price is 7028price
[root@SLAVE19 /]# echo Price is \$$price
Price is $5
```
# <span id = 4>**环境变量**</span>
- **常用的的环境变量**   
　　变量是计算机系统用于保存可变值的数据类型。在Linux系统中，变量名称一般都是大写的，这是一种约定俗成的规范。我们可以直接通过变量名称来提取到对应的变量值。Linux系统中的环境变量是用来定义系统运行环境的一些参数，比如每个用户不同的家目录、邮件存放位置等。  
　　为了通过环境变量帮助Linux系统构建起能够为用户提供服务的工作运行环境，需要数百个变量协同工作才能完成。您当然没有必要去把每一个变量都看一遍，而应该在最宝贵的书籍中为读者精讲最重要的内容。为了更好地帮助大家理解变量的作用，刘遄老师给大家举个例子。前文中曾经讲到，在Linux系统中一切都是文件，Linux命令也不例外。那么，在用户执行了一条命令之后，Linux系统中到底发生了什么事情呢？简单来说，命令在Linux中的执行分为4个步骤。  
**第1步**：判断用户是否以绝对路径或相对路径的方式输入命令（如/bin/ls），如果是的话则直接执行。  
**第2步**：Linux系统检查用户输入的命令是否为“别名命令”，即用一个自定义的命令名称来替换原本的命令名称。可以用alias命令来创建一个属于自己的命令别名，格式为“alias 别名=命令”。若要取消一个命令别名，则是用unalias命令，格式为“unalias 别名”。我们之前在使用rm命令删除文件时，Linux系统都会要求我们再确认是否执行删除操作，其实这就是Linux系统为了防止用户误删除文件而特意设置的rm别名命令，接下来我们把它取消掉：
    ```
    [root@linuxprobe ~]# ls
    anaconda-ks.cfg Documents initial-setup-ks.cfg Pictures Templates
    Desktop Downloads Music Public Videos
    [root@linuxprobe ~]# rm anaconda-ks.cfg 
    rm: remove regular file ‘anaconda-ks.cfg’? y
    [root@linuxprobe~]# alias rm
    alias rm='rm -i'
    [root@linuxprobe ~]# unalias rm
    [root@linuxprobe ~]# rm initial-setup-ks.cfg 
    [root@linuxprobe ~]#
    ```

    **第3步**：Bash解释器判断用户输入的是内部命令还是外部命令。内部命令是解释器内部的指令，会被直接执行；而用户在绝大部分时间输入的是外部命令，这些命令交由步骤4继续处理。可以使用“type命令名称”来判断用户输入的命令是内部命令还是外部命令。  
    **第4步**：系统在多个路径中查找用户输入的命令文件，而定义这些路径的变量叫作PATH，可以简单地把它理解成是“解释器的小助手”，作用是告诉Bash解释器待执行的命令可能存放的位置，然后Bash解释器就会乖乖地在这些位置中逐个查找。PATH是由多个路径值组成的变量，每个路径值之间用冒号间隔，对这些路径的增加和删除操作将影响到Bash解释器对Linux命令的查找。
    ```
    [root@linuxprobe ~]# echo $PATH
    /usr/local/bin:/usr/local/sbin:/usr/bin:/usr/sbin:/bin:/sbin
    [root@linuxprobe ~]# PATH=$PATH:/root/bin
    /usr/local/bin:/usr/local/sbin:/usr/bin:/usr/sbin:/bin:/sbin:/root/bin
    ```
    　　
    　　这里有比较经典的问题：“为什么不能将当前目录（.）添加到PATH中呢? ” 原因是，尽管可以将当前目录（.）添加到PATH变量中，从而在某些情况下可以让用户免去输入命令所在路径的麻烦。但是，如果黑客在比较常用的公共目录/tmp中存放了一个与ls或cd命令同名的木马文件，而用户又恰巧在公共目录中执行了这些命令，那么就极有可能中招了。  
    　　所以，作为一名态度谨慎、有经验的运维人员，在接手了一台Linux系统后一定会在执行命令前先检查PATH变量中是否有可疑的目录，另外读者从前面的PATH变量示例中是否也感觉到环境变量特别有用呢。我们可以使用env命令来查看到Linux系统中所有的环境变量，而刘遄老师为您精挑细选出了最重要的10个环境变量，如下表所示：

    变量名称 | 作用
    :---:|:---:
    `HOME`|用户主目录
    `SHELL`|用户在使用Shell解释器名称
    `HISTSIZE`|输出的历史命令记录条数
    `HISTFILESIZE`|保存的历史命令记录条数
    `MAIL`|邮件保存路径
    `LANG`|系统语言、语系名称
    `RANDOM`|生成一个随机数字
    `PS1`|Bash解释器的提示符
    `PATH`|定义解释器搜索用户执行命令的路径
    `EDITOR`|用户默认的文本编辑器
    
    **示例**：查看家目录路径
    
    ```
    [root@SLAVE19 ~]# echo $HOME
    /root
    ```

- **自定义环境变量**  
    **示例**：将常用的工作目录设置成环境变量WORK
    
    ```
    [root@SLAVE19 data]# WORK=/data/caoz/zhangfan
    [root@SLAVE19 data]# cd $WORK
    [root@SLAVE19 zhangfan]# pwd
    /data/caoz/zhangfan
    ```
