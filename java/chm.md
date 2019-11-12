# concurrenthashmap

分段加锁


longadder针对atomiclong进行优化，解决cas类操作在高并发场景下，使用乐观锁，会导致大量线程长时间重复循环。采用了类似分段cas操作，失败则自动迁移到下一个分段进行cas。
