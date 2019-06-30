# maven

## 插件
maven本质事一个插件框架，所有的任务都交给插件完成。每个任务对应一个目标，每个插件有一个或多个目标。调用插件目标的方式有两种，第一种将插件目标与生命周期阶段绑定然后在命令行输入生命周期阶段，如mvn compile，第二种直接执行插件目标，如mvn archetype:generate。常用插件列表[apache](http://maven.apache.org/plugins/index.html),[codehaus](http://mojo.codehaus.org/plugins.html)
