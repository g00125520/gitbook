the basic theroy

## cap
partition tolerance:分区容错，分布式系统分布在多个子网，两个分区之间一定会出现无法正常通信的情况。consistency:一致性，多个子网中某个服务器数据更新之后，其他子网必须同步更新。availability:可用性，只要收到用户请求，服务器就必须响应。

cap理论指出，上面三种情况不可能同时满足，一般情况下p必须满足，只能在c和a之间进行取舍。

## base
basically available:基本可用。分布式系统出现故障时，允许损失部分可用，保证核心可用。soft state：软状态，允许系统存在中间状态而不影响系统的整体可用。eventual consistency：最终一致，系统中所有数据副本经过一定时间之后，最终能够达到一致状态。base通过牺牲强一致性获取可用性。




