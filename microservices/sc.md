# Spring Cloud



## Eureka

### Eureka,Consul,Zookeeper
就cap来说，zk和consul做到了cp，而eureka则做到了ap，



## feign

### feign contract

通过feign.Contract，feign.Contract.BaseContract，feign.Contract.Default的模板方法将“targetType”中包含的所有关于HTTP的附加元信息抽取成结果集。SpringMvcContract继承了Contract.BaseContract并实现了ResourceLoaderAware接口。


## hystrix

雪崩效应，基础服务故障导致的级联故障，将不可用逐渐放大的过程。要防止，必须有容错机制，实现：网络请求设置超时，使用断路器模式。正常情况下，一个远程调用需在几十毫秒内响应，如果响应太慢，则远程调用的线程就不能释放，资源不能释放，最终导致服务不可用。断路器可以理解为对容易导致错误的操纵的代理，它能统计一段时间内调用失败的次数，并决定是正常请求依赖的服务还是直接返回。

hystrix首先包裹请求，使用hystrixcommand或者hystrixobservablecommand包裹对依赖的调用逻辑，每个命令在独立线程中执行，跳闸机制，当某个服务的错误率超过一定阈值时，hystrix可以自动或者手动跳闸，停止请求该服务一段时间。资源隔离，hystrix为每个依赖都维护了一个小型的线程池或者信号量，如果该线程池已满，发往该依赖的请求就被立即拒绝，而不是排队等候，从而加速失败判定。

执行回退逻辑并不代表断路器已经打开，请求失败，超时，被拒绝以及断路器打开都会执行回退逻辑。

服务熔断、降级、限流、异步RPC 


## zuul

使用zuul来实现服务聚合，rxjava。


## sc统一配置和nacos

引导上下问，bootstrap

- [gitlab](https://about.gitlab.com/solutions/high-availability/)
- [rabbitmq](https://www.rabbitmq.com/ha.html)
- [nacos](https://nacos.io/zh-cn/docs/quick-start.html)

## sleuth

sleuth为sc提供了分布式跟踪的解决方案，大量借用了dapper，zipkin和htrace的设计。span跨度，基本工作单由，用一个64位的id唯一标识，除id外，span还包括描述，时间戳事件，键值对的注解等。



## problems

- ribbon的配置类不应该在主应用程序上下问的@ComponentScan中；

componentscan默认扫描的路径为application类所在的包及子包，如果配置类被扫描，则配置类会被所有的ribbon客户端共享，如果只想配置某个client，则在ribbonclient注解中通过configuration属性单独配置。

-


## Reference

- [Eureka与Zookeeper对比](http://dockone.io/article/78)
- [itmuch for spring cloud](http://www.itmuch.com/spring-cloud/spring-cloud-index/)
- [Cloud Native Application](https://pivotal.io/platform-as-a-service/migrating-to-cloud-native-application-architectures-ebook)
- [12-factors Apps](https://12factor.net/zh_cn/)
- [book code](https://github.com/huangjava/spring-cloud-docker-microservice-book-code)
- [eureka,consul,zk](https://www.cnblogs.com/daniels/p/10269140.html)
- [consul](https://www.consul.io/docs/index.html)
- [loadbalanced](https://blog.csdn.net/u011063112/article/details/81295376)
- [zipkin](https://zipkin.io/pages/quickstart.html)
