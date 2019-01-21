##### 今天组长要求我对一个生产上的出现数据遗漏问题进行数据更新操作；
    问题如下：
    ```
    --数据更新操作
    update table set count=1 where flag='0' and type='2' and create_time>='2019-01-18 ' and create_time =<'2019-01-21';
    ```
    
因为是生产环境的更新操作，因此，需要数据库中的表进行备份操作；

```
--首先创建备份表
create table_bak like tbale; 

--刷选出需要备份的结果插入刚才的备份表中：tbale_bak
insert into 
table_bak
select * from table where flag='0' and type='2' and create_time>='2019-01-18 ' and create_time =<'2019-01-21';
```

说明：以上是mysql常用的数据备份操作（相同结构的表，字段一致）；至于字段不一致的表，可以使用以下方法
```
    insert into 目标表(字段1,字段2,...) select 字段1,字段2,...from 来源表即可
```
    