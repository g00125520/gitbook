# hbase

## 列式存储

hbase中的列由列族和列修饰符组成，一个列族下可任意添加列，不受任何限制。

hbase本质是一个kv数据库，key由rowkey（行键）+colunmfamily（列族）+column qualifier（列修饰符）+timestamp（时间戳，版本）+keytype（类型）组成，而value则为值。准确定位一条数据，需要：rowkey+column+timestamp。修改一条数据本质为新增一条数据，只不过增加了一个新的版本。删除数据本质也是新增一条记录，然后将keytype标记为删除。

hbase通过rowkey对表进行横向切割，然后存储到hregionserver上hregion的store中，每个hregion上存储hbase表的一部分数据。一个列族的数据是存储在一个store中的。store中有mem store，store file，hfile，在写数据的时候，首先写到mem store中，当超过一定阈值，就会将内存中的数据刷新到磁盘上，形成storefiel，而storefile底层以hfile格式保存。

## phoenix

## coprocessor
