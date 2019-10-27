# maven

## 插件

maven本质事一个插件框架，所有的任务都交给插件完成。每个任务对应一个目标，每个插件有一个或多个目标。调用插件目标的方式有两种，第一种将插件目标与生命周期阶段绑定然后在命令行输入生命周期阶段，如mvn compile，第二种直接执行插件目标，如mvn archetype:generate。常用插件列表[apache](http://maven.apache.org/plugins/index.html),[codehaus](http://mojo.codehaus.org/plugins.html)

## archetype

[creating archetypes](http://maven.apache.org/guides/mini/guide-creating-archetypes.html)

```java
//根据骨架生成项目：
mvn archetype:generate -DarchetypeGroupId=org.apache.maven.archetypes -DarchetypeArtifactId=maven-archetype-quickstart -DarchetypeVersion=1.3 -X
//生成项目骨架：
mvn archetype:generate -DarchetypeGroupId=org.apache.maven.archetypes  -DarchetypeArtifactId=maven-archetype-archetype   -DgroupId=com.demo  -DartifactId=App
//根据项目生成框架:
mvn archetype:create-from-project
//更新本地骨架列表：
mvn archetype:crawl
//使用本地的骨架：
mvn archetype:generate -DarchetypeCatalog=local 
//使用远程骨架
mvn org.apache.maven.plugins:maven-archetype-plugin:2.4:generate -DarchetypeCatalog=https://repository.apache.org/content/repositories/snapshots/
mvn org.apache.maven.plugins:maven-archetype-plugin:2.4:generate\
     -DarchetypeGroupId=org.apache.flink \
     -DarchetypeArtifactId=flink-quickstart-java \
     -DarchetypeCatalog=https://repository.apache.org/content/repositories/snapshots/ \
     -DarchetypeVersion=1.3-SNAPSHOT \
     -DgroupId=wiki-edits \
     -DartifactId=wiki-edits \
     -Dversion=0.1 \
     -Dpackage=wikiedits \
     -DinteractiveMode=false

```


## ref

- [plugin develop](http://maven.apache.org/plugin-developers/)
- [archetype](https://github.com/apache/maven-archetype/)
