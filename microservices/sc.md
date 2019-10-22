# Spring Cloud



## Eureka

### Eureka,Consul,Zookeeper
就cap来说，zk和consul做到了cp，而eureka则做到了ap，



## feign

### feign contract

通过feign.Contract，feign.Contract.BaseContract，feign.Contract.Default的模板方法将“targetType”中包含的所有关于HTTP的附加元信息抽取成结果集。SpringMvcContract继承了Contract.BaseContract并实现了ResourceLoaderAware接口。




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
