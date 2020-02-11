# understand mysql

## index

in or 到底走不走索引


- [数据库索引](https://mp.weixin.qq.com/s/YMbRJwyjutGMD1KpI_fS0A)
- [MyISAM与InnoDB的索引差异](https://mp.weixin.qq.com/s/FUXPXKfKyjxAvMUFHZm9UQ)



## lock

- [Next-Key Lock](https://www.cnblogs.com/zhoujinyi/p/3435982.html)
- [MySQL死锁分析](https://mp.weixin.qq.com/s/Qv5QzzVoUtIB58UmIRG-lQ)


## transcation

[四种事务隔离级](https://www.cnblogs.com/zhoujinyi/p/3437475.html)


## 数据库字段允许空值，会遇到一些问题： 

- 负向查询（!=1）不能命中索引，会导致全表扫描；
- 允许空值，不等于查询不会将空值行包含进来，而需要：id != 1 or id is null:
- 上面的or会导致全表扫描，需要用union合并两次的结果，则可以命中索引；
- 建议建表时加上default值，可以避免空值的坑；


## explain的使用和sql优化

explain中type字段描述了找到所需数据使用的扫描方式，常见的有：
- system：系统表，少量数据，不需要进行磁盘io；
- const：常量链接；pk或者unique上的等值查询；
- eq_ref：主键索引primary key或者非空唯一索引unique not null等值扫描；pk或者unique上的join查询，等值匹配，对于前表的每一行，后表只有一行命中；
- ref：非主键非唯一索引等值扫描；可能有多行命中；
- range：索引上的范围扫描；如：between/in/>；
- index：索引树扫描；如：innoDB的count;
- ALL：全表扫描；



两类隐藏的不能利用索引的情况：
- 表的列类型与where值类型不一致，强制类型转换，不能命中索引，需要全表扫描；
- join两个表的字符编码不同；



## data

sudo mysql -uroot -pDtDream0209  dmall -e "select id,catalog_template_id,catalog_template_data from catalog_his into outfile '/tmp/dd'"
