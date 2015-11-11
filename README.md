OurJS 0.1.x
====

Free Blog Engine, Forum System, Website Template and CMS Platform based on Node.JS and Redis
----

Author : Kris Zhang

[ourjs 0.1.x](https://github.com/newghost/ourjs/tree/0.1.x) using redis

[ourjs 0.0.x](https://github.com/newghost/ourjs/tree/0.0.x) using memory & file system



OurJS 0.1.x 版
====

OurJS 基于Node.JS和Redis的开源的高性能博客引擎，网站模板，论坛系统和轻量级的CMS系统

[ourjs 0.1.x](https://github.com/newghost/ourjs/tree/0.1.x) 基于Reis

[ourjs 0.0.x](https://github.com/newghost/ourjs/tree/0.0.x) 基于文件系统


常见问题
====




如何安装ourjs 0.1.x
----

首先下载最新的 ourjs，单击右侧的 [Download ZIP](https://github.com/newghost/ourjs/archive/0.1.x.zip) 下载最新版(也可使用 git clone 复制0.1.x的branch, npm中发布的是0.0.x版)； 然后你需要安装　[redis](http://redis.io)，windows版的是由微软维护的，可在[MSOpenTech](https://github.com/MSOpenTech/redis)下载； 最后单击 ourjs.sh 或 ourjs.cmd 即可运行, 默认侦听 8051 端口， 即: http://localhost:8051


你可以安装第三方redis管理客户端 [RedisDesktopManager](http://redisdesktop.com/) 方便调试与查看 redis 数据。





ourjs 0.1.x 基于哪些框架
----

web框架使用的是 [websvr](https://github.com/newghost/websvr)， 只用一个文件实现，支持include模板文件及其嵌套； 
数据库ORM采用的是 [redblade](https://github.com/newghost/redblade)，同样只用一个文件实现； 只要事先定好[schema](https://github.com/newghost/ourjs/tree/0.1.x/schema)，可以让你像mongodb那样更新redis数据， 自动邦你创建index/ keyword等索引； 推荐使用原生redis指令读取数据，redblade更新数据，这样可以发挥redis的超强性能。不过首先你需要对redis指令和数据类型非常熟悉。
模板引擎采用了我认为性价比最高的 [doT](http://olado.github.io/doT/) 十分钟上手。


为什么要保留node_modules文件夹
----

npm在某些情况下经常出现不用过的情况； 同时ourjs所采用的所有模块都是平台不相关的，再加上有时侯需要对redblade等模块做一些修改，这些修改只有稳定运行一段时间才能发布到npm上面，因此保留了node_modules文件夹。



为什么ourjs 0.1.x版可以应对超大规模并发
----

ourjs 0.0.x 使用内存和文件系统；　相当于在node.js中实现了一个内存数据库，即先读写内存立即返回后，再同步到文件系统； 这种机制的优点是无任何依赖只需要装node.js即可运行，使用非常低的服务器配置就可支撑较大流量，运行稳定，半年多重启一次； ourjs.com 使用这种构架；　缺点是所有状态都在一个node.js线程中，无法分布式集群化部署，理论上无法应对超大规模并发量，而且数据更操作会略显复杂。

ourjs 0.1.x 所有session和内容均存放在redis中，网站进程不存放任何状态， 当需要应对超大规模流量时可布暑多个ourjs实例，通过更改config.js，让每个实例侦听不同端口，然后通过nginx反向代理或 DNS round robin 做负载均衡，集群化布暑和单个实例布暑不需要更改应用层的任何代码。


为什么不用mongodb？如何像mongodb那样操作redis
----

mongodb是非常好的nosql文档数据库，数据更新查询非常方便，但它是基于文件系统的，硬盘I/O的读写速度会严重限制网站可承受的最大并发量。
而redis是目前公认的速度最快的基于内存的键值对数据库，但redis的缺点也非常明显，仅提供最基本的hash set, list, sorted set等基于数据类型，不分表，没有schema，没有索引，没有外键，缺少int/date等基本数据类型，多条件查询需要通过集合内联(sinter,zinterstore)和连接间接实现，操作不便，开发效率低，可维护性不佳； 因此一般不将其视为完整的数据库单独使用，很多网站将redis作为高速缓存和session状态存储层，然后再与其他数据库搭配使用。 




如何安装和快速入门
----

要运行 ourjs　请先安装　[redis](http://redis.io)

中文支持： http://ourjs.com/bbs/OurJS




















License
----

BSD, See our license file