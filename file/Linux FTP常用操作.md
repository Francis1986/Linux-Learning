## FTP操作
---
#### 索引
- [ftp登录](#ftp登录)
- [ftp文件操作](#ftp文件操作)
- [ftp下载](#ftp下载)
---

- <span id = ftp登录>**ftp登录**</span>
```
ftp -vn 192.184.100.21 --登录FTP
user username password --用户名密码
```
- <span id = ftp文件操作>**ftp文件操作**</span>
```
cd path --打开ftp服务器某路径
ls --列出所在目录所有文件
lcd path --打开本地服务器某路径
```
- <span id = ftp下载>**ftp下载**</span>
```
prompt off #下载时不再询问，直接下载，不加这句话，每下载一个文件都要问一次是否下载
mget *S1UHTTP* #mget+文件名的通配符
```