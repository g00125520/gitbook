# Lock

## Lock in jvm

synchronized，实例方法对实例进行锁，静态方法则对类进行锁。进入锁区间之前首先竞争锁，得到者进入执行，其他等待锁释放之后进入执行。通过jvm的monitorenter,monitorexit或者ACC_SYNCHRONIZED实现。



## Distribute lock

[基于etcd实现](https://www.toutiao.com/a6708613773353026051/?tt_from=weixin&utm_campaign=client_share&wxshare_count=1&timestamp=1561982858&app=news_article&utm_source=weixin&utm_medium=toutiao_android&req_id=2019070120073801015203021635050E9&group_id=6708613773353026051)

[基于zk实现]()
