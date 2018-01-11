# 输入与输出重定向
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

# 管道符
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

# 转义符
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

# 环境变量