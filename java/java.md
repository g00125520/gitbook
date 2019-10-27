# the java lang

## multi thread 

- [volatile](https://www.toutiao.com/a6714540996052386316/?tt_from=weixin&utm_campaign=client_share&wxshare_count=1&timestamp=1563429415&app=news_article&utm_source=weixin&utm_medium=toutiao_android&req_id=201907181356540101520222026391AD7&group_id=6714540996052386316)

## class loader

它负责将类的字节码形式转换成内存形式的类对象。字节码本质是字节数组，具有特定的复杂的内部结构。每个类对象内部有一个classloader字段来标识自己是由那个classloader来加载的。jvm不是一次加载全部的类，而是按需加载。程序在运行的过程中会逐渐遇到很多不认识的新类，这时就会调用classloader来加载。加载完成后就会将类对象存在classloader里面，下次不需要重新加载。

jvm内置三个重要的classloader，BootstrapClassLoader，ExtensionClassLoader和AppClassLoader。B负责加载运行时核心类，位于lib/rt.jar，E负责加载扩展类，位于lib/ext/中，A加载classpath环境变量定义路径中的类，包括自己编写的代码及三方依赖。URLClassloader可加载网络上的jar包和class文件。E和A都为U的子类，只不过指定的路径为本地文件路径。

程序运行过程中，如遇到一个未知的类，则jvm调用class对象的classloader来加载，如果A遇到没有加载的系统类路，则委托B和E加载，也就是双亲委派。A遇到一个未知的类时，并不立即搜索classpath，而是交给B加载，如果B可以加载，则不用麻烦E了。E在加载一个未知的类时，也并不立即搜索ext路径，而会交给B加载，如果B可以加载那么E就不用麻烦了，否则搜索ext加载。每个classloader都有一个parent属性指向父加载器，它们都尽量将工作交给父去做，只有父做不了才自己做。E的parent为null，当parent为null时，表示其父加载器为根加载器B。

forname同样使用调用者class对象的classloader来加载目标类，不过也提供了重载版本，可以指定具体的classloader，通过这种形式，可以突破内置加载器的限制，通过自定义类加载器允许我们自由加载任意来源类库。根据传递性，目标类库传递引用引用到的其他类库也将使用自定义加载器加载。

classloader里面有三个重要的方法，loadclass，findclass，defineclass。loadclass是加载目标类的入口，首先查找当前classloader和双亲是否加载了目标类,如果没有找到，则调用findclass让自定义加载器自己来加载。findclass需要子类实现，不同的加载器使用不同的逻辑来获取目标类的字节码，拿到之后调用defineclass将字节码转换为class对象。

自定义类加载器不要轻易覆盖loadclass方法，否则可能导致无法加载核心类库。在使用自定义类加载器时，要明确好它的父加载器，将父加载器通过子类构造函数传入，如果父加载器为null，则表示父加载器为根加载器。

class.forname和classloader.loadclass都可以用来加载目标类，但前者可以获取原生类型的class，后者则会报错，如："[I"

钻石依赖，指软件依赖导致同一个软件包的两个版本需要共存而不能有冲突。maven是这样解决钻石依赖的，它会从多个冲突的版本中选择一个来使用，如果不同版本的兼容性很差，则程序将无法正常编译。maven叫做扁平化依赖管理。使用classloader可以解决该问题，不同版本使用不同classloader来加载。即使同样的字节码使用不同的classloader加载出来的类都不能算为同一个类。

[sofa-ark](https://github.com/sofastack/sofa-ark),classloader隔离框架。



## native

## annotition



## ref

- [java 5](https://www.ibm.com/developerworks/cn/views/global/libraryview.jsp?sort_by=&show_abstract=true&show_all=&search_flag=&contentarea_by=Java+technology&search_by=%E6%82%A8%E4%B8%8D%E7%9F%A5%E9%81%93%E7%9A%84+5&topic_by=%E6%89%80%E6%9C%89+Java+technology+%E4%B8%BB%E9%A2%98&type_by=%E6%89%80%E6%9C%89+Java+technology+%E7%A7%8D%E7%B1%BB%E5%9E%8B&ibm-search=%E6%90%9C%E7%B4%A2)
