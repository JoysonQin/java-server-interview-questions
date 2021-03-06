## java基础   

1、Arrays.sort实现原理和Collections.sort实现原理。<br/>
答：Collections.sort方法底层会调用Arrays.sort方法，底层实现都是TimeSort实现的。TimSort算法就是找到已经排好序数据的子序列，然后对剩余部分排序，然后合并起来.<br/>
2.foreach和while的区别(编译之后)  
3.线程池的种类，区别和使用场景 
答：4种 FixedThreadPool 用于任务量比较固定但耗时长的任务，
        CachedThreadPool用于比较适合任务量大但耗时少的任务。
        ScheduledThreadPool 适用于执行定时任务和具体固定周期的重复任务。
        SingleThreadPool适用于多个任务顺序执行的场景。
-----分析线程池的实现原理和线程的调度过程   
-----线程池如何调优   
-----线程池的最大线程数目根据什么确定  
答：线程池中线程的数目是跟线程池所要处理的任务性质有关的
    任务的性质：CPU密集型任务、IO密集型任务、混合型任务。
    任务的优先级：高、中、低。
    任务的执行时间：长、中、短。
    任务的依赖性：是否依赖其他系统资源，如数据库连接等。
性质不同的任务可以交给不同规模的线程池执行。
针对不同的任务性质而言：CPU密集型任务应配置尽可能小的线程，如配置CPU个数+1的线程数，IO密集型任务应配置尽可能多的线程，因为IO操作不占用CPU，不要让CPU闲下来，应加大线程数量，如配置两倍CPU个数+1，而对于混合型的任务，如果可以拆分，拆分成IO密集型和CPU密集型分别处理，前提是两者运行的时间是差不多的，如果处理时间相差很大，则没必要拆分了。
任务对其他系统资源有依赖：如某个任务依赖数据库的连接返回的结果，这时候等待的时间越长，则CPU空闲的时间越长，那么线程数量应设置得越大，才能更好的利用CPU。 
线程等待时间所占比例越高，这样的话CPU空闲时间比较多，为了能够更好的利用CPU，需要较多线程。
如果线程CPU时间所占比例越高，说明CPU比较繁忙，此时需要越少线程。 
另外，如果线程数量过多，线程之间的切换也会带来开销。
是否使用线程池就一定比使用单线程高效呢？
答案是否定的，比如Redis就是单线程的，但它却非常高效，基本操作都能达到十万量级/s。从线程这个角度来看，部分原因在于：多线程带来线程上下文切换开销，单线程就没有这种开销。
-----动态代理的几种方式   
答：1.jdk的动态代理，要实现同一个借口。依靠反射原理实现，对目标类实现增强，利用切面。
    2.CGLib的动态代理，利用ASM动态生成字节码。不需要实现同一个借口，利用集成方式。
-----HashMap的并发问题   
答：https://www.cnblogs.com/andy-zhou/p/5402984.html
http://blog.csdn.net/justloveyou_/article/details/62893086
        并发且resize时候，可能会出现循环链表，出现死循环。
-----了解LinkedHashMap的应用吗  
答：http://blog.csdn.net/justloveyou_/article/details/71713781 基于hashmap和linklist进行了排序，经常使用的元素就放在后面，最近最少使用的就排在了链表的前面，基于LinkedHashMap的访问顺序的特点，可构造一个LRU（Least Recently Used）最近最少使用简单缓存。也有一些开源的缓存产品如ehcache的淘汰策略（LRU）就是在LinkedHashMap上扩展的。
------反射的原理，反射创建类实例的三种方式是什么？   
cloneable接口实现原理，浅拷贝or深拷贝   
Java NIO使用   
hashtable和hashmap的区别及实现原理，hashmap会问到数组索引，hash碰撞怎么解决   
arraylist和linkedlist区别及实现原理   
反射中，Class.forName和ClassLoader区别   
String，Stringbuffer，StringBuilder的区别？   
有没有可能2个不相等的对象有相同的hashcode   
简述NIO的最佳实践，比如netty，mina   
TreeMap的实现原理   

### JVM相关   

类的实例化顺序，比如父类静态数据，构造函数，字段，子类静态数据，构造函数，字段，他们的执行顺序   
JVM内存分代   
Java 8的内存分代改进   
JVM垃圾回收机制，何时触发MinorGC等操作   
jvm中一次完整的GC流程（从ygc到fgc）是怎样的，重点讲讲对象如何晋升到老年代，几种主要的jvm参数等   
你知道哪几种垃圾收集器，各自的优缺点，重点讲下cms，g1   
新生代和老生代的内存回收策略   
Eden和Survivor的比例分配等   
深入分析了Classloader，双亲委派机制   
JVM的编译优化   
对Java内存模型的理解，以及其在并发中的应用   
指令重排序，内存栅栏等   
OOM错误，stackoverflow错误，permgen space错误   
JVM常用参数   
tomcat结构，类加载器流程   
volatile的语义，它修饰的变量一定线程安全吗    
g1和cms区别,吞吐量优先和响应优先的垃圾收集器选择    
说一说你对环境变量classpath的理解？如果一个类不在classpath下，为什么会抛出ClassNotFoundException异常，如果在不改变这个类路径的前期下，怎样才能正确加载这个类？   
说一下强引用、软引用、弱引用、虚引用以及他们之间和gc的关系      

### JUC/并发相关   

ThreadLocal用过么，原理是什么，用的时候要注意什么   
Synchronized和Lock的区别   
synchronized 的原理，什么是自旋锁，偏向锁，轻量级锁，什么叫可重入锁，什么叫公平锁和非公平锁   
concurrenthashmap具体实现及其原理，jdk8下的改版   
用过哪些原子类，他们的参数以及原理是什么   
cas是什么，他会产生什么问题（ABA问题的解决，如加入修改次数、版本号）   
如果让你实现一个并发安全的链表，你会怎么做   
简述ConcurrentLinkedQueue和LinkedBlockingQueue的用处和不同之处   
简述AQS的实现原理    
countdowlatch和cyclicbarrier的用法，以及相互之间的差别?   
concurrent包中使用过哪些类？分别说说使用在什么场景？为什么要使用？  
LockSupport工具   
Condition接口及其实现原理   
Fork/Join框架的理解   
jdk8的parallelStream的理解   
分段锁的原理,锁力度减小的思考    

## Spring   

Spring AOP与IOC的实现原理   
Spring的beanFactory和factoryBean的区别   
为什么CGlib方式可以对接口实现代理？   
RMI与代理模式   
Spring的事务隔离级别，实现原理   
对Spring的理解，非单例注入的原理？它的生命周期？循环注入的原理，aop的实现原理，说说aop中的几个术语，它们是怎么相互工作的？  
Mybatis的底层实现原理      
MVC框架原理，他们都是怎么做url路由的   
spring boot特性，优势，适用场景等   
quartz和timer对比   
spring的controller是单例还是多例，怎么保证并发的安全   

## 分布式相关    

Dubbo的底层实现原理和机制   
描述一个服务从发布到被消费的详细过程   
分布式系统怎么做服务治理   
接口的幂等性的概念   
消息中间件如何解决消息丢失问题    
Dubbo的服务请求失败怎么处理   
重连机制会不会造成错误   
对分布式事务的理解   
如何实现负载均衡，有哪些算法可以实现？  
Zookeeper的用途，选举的原理是什么？      
数据的垂直拆分水平拆分。  
zookeeper原理和适用场景   
zookeeper watch机制   
redis/zk节点宕机如何处理    
分布式集群下如何做到唯一序列号   
如何做一个分布式锁   
用过哪些MQ，怎么用的，和其他mq比较有什么优缺点，MQ的连接是线程安全的吗   
MQ系统的数据如何保证不丢失   
列举出你能想到的数据库分库分表策略；分库分表后，如何解决全表查询的问题。   

## 算法&数据结构&设计模式   

海量url去重类问题（布隆过滤器）  
数组和链表数据结构描述，各自的时间复杂度   
二叉树遍历   
快速排序   
BTree相关的操作    
在工作中遇到过哪些设计模式，是如何应用的   
hash算法的有哪几种，优缺点，使用场景   
什么是一致性hash   
paxos算法   
在装饰器模式和代理模式之间，你如何抉择，请结合自身实际情况聊聊   
代码重构的步骤和原因，如果理解重构到模式？   

## 数据库   

MySQL InnoDB存储的文件结构   
索引树是如何维护的？   
数据库自增主键可能的问题  
MySQL的几种优化   
mysql索引为什么使用B+树   
数据库锁表的相关处理   
索引失效场景    
高并发下如何做到安全的修改同一行数据，乐观锁和悲观锁是什么，INNODB的行级锁有哪2种，解释其含义     
数据库会死锁吗，举一个死锁的例子，mysql怎么解决死锁     

## Redis&缓存相关   

Redis的并发竞争问题如何解决了解Redis事务的CAS操作吗   
缓存机器增删如何对系统影响最小，一致性哈希的实现   
Redis持久化的几种方式，优缺点是什么，怎么实现的   
Redis的缓存失效策略    
缓存穿透的解决办法   
redis集群，高可用，原理     
mySQL里有2000w数据，redis中只存20w的数据，如何保证redis中的数据都是热点数据   
用Redis和任意语言实现一段恶意登录保护的代码，限制1小时内每用户Id最多只能登录5次   
redis的数据淘汰策略   

## 网络相关   

http1.0和http1.1有什么区别   
TCP/IP协议   
TCP三次握手和四次挥手的流程，为什么断开连接要4次,如果握手只有两次，会出现什么   
TIME_WAIT和CLOSE_WAIT的区别   
说说你知道的几种HTTP响应码   
当你用浏览器打开一个链接的时候，计算机做了哪些工作步骤   
TCP/IP如何保证可靠性，数据包有哪些数据组成    
长连接与短连接     
Http请求get和post的区别以及数据包格式   
简述tcp建立连接3次握手，和断开连接4次握手的过程；关闭连接时，出现TIMEWAIT过多是由什么原因引起，是出现在主动断开方还是被动断开方。    

## 其他  

maven解决依赖冲突,快照版和发行版的区别   
Linux下IO模型有几种，各自的含义是什么  
实际场景问题，海量登录日志如何排序和处理SQL操作，主要是索引和聚合函数的应用   
实际场景问题解决，典型的TOP K问题   
线上bug处理流程   
如何从线上日志发现问题    
linux利用哪些命令，查找哪里出了问题（例如io密集任务，cpu过度）   
场景问题，有一个第三方接口，有很多个线程去调用获取数据，现在规定每秒钟最多有10个线程同时调用它，如何做到。    
用三个线程按顺序循环打印abc三个字母，比如abcabcabc。   
常见的缓存策略有哪些，你们项目中用到了什么缓存系统，如何设计的   
设计一个秒杀系统，30分钟没付款就自动关闭交易（并发会很高）   
请列出你所了解的性能测试工具   
后台系统怎么防止请求重复提交？   
有多个相同的接口，我想客户端同时请求，然后只需要在第一个请求返回结果的时候返回给客户端     
