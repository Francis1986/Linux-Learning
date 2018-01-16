## HDFS的基本操作

---
#### 索引
- [数据库内新建表](#数据库内新建表) 
- [向表内put数据](#向表内put数据)
- [查看数据库中的表和数据](#查看数据库中的表和数据)  
---


- <span id = 数据库内新建表>**数据库内新建表**</span>

    ```
    hdfs dfs -mkdir -p /user/hive/warehouse/unicomidmp.db/tablename
    ```

- <span id = 向表内put数据>**向表内put数据**</span>
    ```
    hdfs dfs -put sourcedata_path /user/hive/warehouse/unicomidmp.db/tablename
    ```

- <span id = 查看数据库中的表和数据>**查看数据库中的表和数据**</span>
    ```
    hdfs dfs -du -h /user/hive/warehouse/unicomidmp.db/文件的通配符
    ```