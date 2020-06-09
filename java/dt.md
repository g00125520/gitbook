
## distribute transcation
- [saga](https://www.jianshu.com/p/e4b662407c66?from=timeline&isappinstalled=0)
- [2pc&3pc](https://www.jianshu.com/p/dd6a340e50b2)
- [tcc](https://www.cnblogs.com/jajian/p/10014145.html)
- [xa](https://blog.csdn.net/wuzhiwei549/article/details/79925618)
- [可靠消息最终一致性](https://www.cnblogs.com/haizai/p/11954339.html)
- [seata设计原理](https://yq.aliyun.com/articles/715556?spm=a2c4e.11157919.spm-cont-list.23.3b31f2047Bulkr)
- [seata](https://github.com/seata/seata)


## 分布式锁

redission的实现思路，client加锁时，如果时redis集群，会首先hash到一台机器，然后发送一段lua脚本（保证操作原子性）：if (redis.call('exists',keys[1]) == 0) then redis.call('hset',keys[1],argv[2],1);redis.call('pexpire',keys[1],argv[1]);return nil; end; if(redis.call('hexists',keys[1],argv[2] ==1) then redis.call('hincrby',keys[1],argv[2],1);redis.call('pexpire',keys[1],argv[1]);return nil; end; return redis.call('pttl',keys[1]);其中，keys[1]为要加的锁，如'SyncTaskLock'，argv[1]为锁的默认生存时间，默认30秒，argv[2]为加锁的客户端id。


上面的逻辑为，如果锁不存在，则加锁，通过hset lock完成，设置一个hash的数据结构，并设置超时时间。如果另外一个client尝试加
锁，发现lock已经存在，然后判断lock的hash中是否存在client2的id不存在，则返回client2一个数字，pttl lock代表lock剩余生存时
间。此后，client2进入一个循环，不停尝试加锁。而client1一但加锁成功，则会启动一个watch dog每隔10s检查一下，如果client1还
持有锁，则不断延长锁的生存时间。如果client1已经持有锁但又想重复加锁，则进入第二个if，通过hincrby增加client1加锁的次数。
当释放锁的时候，则每次对加锁的次数减一，如果发现加锁次数为0，则删除lock，然后client2就可以尝试加锁了。

如果对某个redis master写入了锁，此时会异步复制给对应的master slave，但该过程中一旦发生master宕机，主备切换，就会导致client2在新的master上加锁成功，client1也加锁成功。


curator基于zk实现，锁是zk上的一个节点，zk的节点分为四种，持久节点，持久顺序节点，临时节点和临时顺序节点。分布式锁用到了
临时顺序节点。当a和b对zk发起加锁请求时，两者都在锁节点下创建一个临时顺序节点。假如a先发起，创建完临时节点后，a会检查下lock节点下的所有子节点，如果a是第一个创建节点的，那么a加锁成功。当b来尝试加锁时，也会先创建一个临时顺序节点，b也会检查lock节点下的所有子节点，发现之前a已经创建过了，则加锁失败，之后b会对a创建的节点添加一个监听器，监听这个节点是否被删除。a释放锁的时候，删除自己创建的临时节点，zk通知监听这个节点的监听器，也就是b，b会重新尝试去获取锁。采用临时节点，如果某个客户端创建临时顺序节点之后，不小心宕机，zk会感知到那个客户端宕机，自动删除对应的临时顺序节点。



## 服务注册，zk，eureka，consul，nacos

cap理论，一致性c，所有的节点在同一时间具有相同的数据；可用性a，保证每个请求无论成功或失败都有响应；分区容忍，系统中任意
信息的丢失或失败不影响系统的正常运行；a保证系统本身对外可用，而p则保证系统本事的正常运行。cap三者只能同时满足其中的两者
，不能三者同时满足。

zk满足cp，不能保证a。对于数据存储的场景，一致性应该是首先被保证的，但对服务发现却不是，不同节点存储的服务提供信息不相同
，也不会有太严重的后果。zk在进行leader选举的时候，服务是不可用的。

eureka则满足ap，不同于zk选举leader的过程，eu采用的p2p对等通信，是去中心化的架构，无master/slave之分，每个peer是对等的。
节点通过彼此相互注册来提高可用性，每个节点需要添加一个或多个有效的serviceurl指向其他节点。每个节点都可被是为其他节点的副本。集群中如果某台server宕机，则client的请求会自动切换到新的server节点上，当宕机的server恢复后，eureka会再次将其纳入到服务器集群管理之中。当节点开始接收client请求时，所有的操作都会在节点间进行复制，将请求复制到该server当前所知的其他所有节点中。当一个新的server启动后，会首先尝试从邻近节点获取所有注册列表信息。并通过geteurekaserviceurls方法获取所有的节点，通过心跳契约定期更新。server在一定时间没有接收到某个服务实例的心跳（默认30秒）将会注销该实例（通过eureka.instance.lease-expiration-duration-in-seconds配置）。server节点端时间丢失过多心跳，将进入自我保护模式。eureka集群只要还有一台server还在，就能保证注册服务可用，虽然可能不是最新的。

eureka的另外一种自我保护机制，如果15分钟内超过85%的节点都没有正常心跳，那么eureka就认为client与注册中心出现了网络故障。eureka不再从注册表中移除因长时间没有收到心跳而过期的服务；eureka仍能够接收新服务注册和查询请求，但不会被同步到其他节点上
；当网络稳定时，当前实例新注册的信息会被同步到其他节点中。


consul内置服务注册与发现，分布一致性协议实现，健康检查，kv存储，多数据中心方案等。遵循cp，保证强一致性和分区容错性，使用了raft算法。consul的强一致性导致服务注册比eureka慢，因为raft协议要求必须过半数的节点都写入成功才认为注册成功，leader挂掉时，重新选举期间整个consul不可用。相对，eureka则保证高可用和最终一致性。服务注册较快，因为不需要等注册信息replicate到其
他节点，也不保证replicate成功。当数据不一致时，虽然a，b节点的注册信息不完全相同，但每个eureka仍然能够正常对外提供服务，
但会出现查询服务信息时，请求a查询不到，但请求b就可以。


nacos是阿里开源，支持基于dns和基于rpc的服务发现。nacos除了服务的注册发现之外，还支持动态配置服务，可以让你以中心化，外部化和动态化的方式管理所有环境的应用配置和服务配置。动态配置消除了配置变更时重新部署应用和服务的需要。nacos=springcloud注
册中心+springcloud配置中心。


参考：

- [jianshu](https://www.jianshu.com/p/bfcc8855f3d4)
- [nacos](https://nacos.io/zh-cn/docs/quick-start.html)

