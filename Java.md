https://javaguide.cn/java/collection/java-collection-questions-01.html
OOP特点：封装、继承、多态（继承、重写override、向上转型）


抽象类和接口的区别：允许一个类遵循（implements）多个接口，不需要构造函数和保持状态
的功能抽象就用接口
不允许有构造函数，变量声明默认是static类型，函数方法不允许是final，default关键字可以配合private方法使用，可以继承


序列化：对象转换为字节流，Parcelable（通讯偏重）是安卓专用Serializable（持久化偏重），Serializable是将整个类序列化，而Parcelable是将类中的数据做拆分进行传输，因此Parcelable效率更高


== 和 equals()，还有个===（Java没有）：==比较地址，equals比较string内容


hashCode和equals：hashCode只能说明映射的地址一样


final, finally 和 finalize：继承，异常，GC


Array 和 ArrayList：Array是类，ArrayLists是容器，ArrayLists没有固定大小


反射：运行时程序可以访问、检测和修改它本身状态或行为的一种能力

运行时能够从外部修改class属性，比如C++已经编译为机器码了，根本不存在类的概念

Java比C++更安全，C++需要手动管理内存，Java有GC
C++是编译型语言，Java解释编译都有，通过先将高级语言编译成class字节码，再通过JVM解释运行，同时通过JIT编译热点代码加速，一般来说JVM能够实现平台无关性，C++甚至每个包都得手动编译
Java的网络编程与并发比起C++更易用，例如Java提供了多种线程安全的类，例如ConcurrentHashMap，CopyOnWriteArrayList，BlockingQueue，而C++的std容器不保证线程安全，需要用锁、互斥量、原子变量实现

细节来讲Java不提供指针，Java类是单继承（接口可以多继承）
Java只支持方法重载，C++在此之上还支持运算符重载，复杂度更高

JVM
接触的最多的是HotSpot VM（Oracle），有个更新的GraalVM

JDK
javac和一些其他工具，例如jdb
Java的优化几乎都在JIT，其他很少，常量折叠是其中一个

JRE
解释运行Java class程序（JIT）

字节码
字节码不像机器码一样针对特定的机器，Java程序无需重新编译即可在多种操作系统上运行
在.class->机器码，这一步，JVM类加载器首先加载字节码文件，然后通过解释器执行，比较频繁的代码JIT会将其字节码对应的机器码保存下来加速（还有AOT），所谓的JIT预热就是前面统计执行次数执行时间比较长的那段时间

可以通过GraalVM实现Java编译为机器码，使用的是AOT技术，可能就用不了反射了

位运算符
Java的无符号移位运算符>>>，忽略符号位。>>带符号位右移，负数高位补1
实际上只支持int和long，short、byte、char会先转化为int
超过位数会先取余

基本数据类型
字节数是固定的
特别的是char占两个字节，因为UTF-16。boolean没有定义字节

Java 里使用 long 类型的数据一定要在数值后面加上 L，否则将作为整型解析

基本类型和包装类型
基本类型一般只用在常量和局部变量，不能被用作泛型
局部变量基本类型放在栈中，几乎所有成员基本数据类型放在堆中（静态变量放在方法区）
基本类型默认不是null而是值
==比值
图片: https://odocs.myoas.com/uploader/f/62BRgDwwVc2bqQrV.png?accessToken=eyJhbGciOiJIUzI1NiIsImtpZCI6ImRlZmF1bHQiLCJ0eXAiOiJKV1QifQ.eyJleHAiOjE2OTE2MzA0NTQsImZpbGVHVUlEIjoiNXhrR01FQk1WdlNaV3czWCIsImlhdCI6MTY5MTYyOTg1NCwiaXNzIjoidXBsb2FkZXJfYWNjZXNzX3Jlc291cmNlIiwidXNlcklkIjoyODAzNDJ9.s5TCVbAUFiS3skAUlm71_oHcQaR9K0vgtQ7b7GYehnM

包装类型
如果满足条件，则会从缓存（常量池）中寻找指定数值，若找到缓存，则不会新建对象，只是指向指定数值对应的包装类对象
Integer i1 = 40;
Integer i2 = new Integer(40);
new的另算，也就是说上面两个不==

Byte,Short,Integer,Long 这 4 种包装类默认创建了数值 [-128，127] 的相应类型的缓存数据，Character 创建了数值在 [0,127] 范围的缓存数据，Boolean 直接返回 True or False。

装/拆箱
Integer i = 10 等价于 Integer i = Integer.valueOf(10)
int n = i 等价于 int n = i.intValue();
实际上Interger这些类型很多都是通过拆/装箱实现的

解决浮点数运算精度丢失
BigDecimal a = new BigDecimal("1.0");
BigDecimal b = new BigDecimal("0.9");

BigDecimal x = a.subtract(b);

没有运算符重载，得一个个写成员函数

大数
BigInteger 内部使用 int[] 数组来存储任意大小的整形数据

重载重写
overload/override
编译期/运行期
private/final/static 则子类就不能重写该方法，static能够被再次声明（意思就是两个static方法毫无关系）

为什么说overload是在编译期，override是在运行期，因为overload实际上是直接产生了两个函数名类似的函数，override只有在运行时才确定调用哪个类的方法

重写要遵循“两同两小一大”
“两同”即方法名相同、形参列表相同；“两小”指的是子类方法返回值类型应比父类方法返回值类型更小或相等，子类方法声明抛出的异常类应比父类方法声明抛出的异常类更小或相等；“一大”指的是子类方法的访问权限应比父类方法的访问权限更大或相等。

使用String... args匹配变长
 
面向对象
构造
添加了构造方法后默认的无参构造就没有了

特点
封装、继承、多态

接口与抽象类
不能被实例化
接口强调行为关系，抽象类强调从属关系
一个类只能继承一个类，但是可以有多个接口
接口中成员变量只能是public static final

浅拷贝与深拷贝
浅：clone方法，会新建但是会复制对象内部的引用
深：全new，如果有拷贝构造应该可以用

Object
自带：getClass、hashCode、equals（默认还是比地址）、clone、toString、notify、notifyAll、wait x 3重载、finalize（被GC时触发）

Java只有值传递
主要还是为了安全，如果在某个方法内部改变了引用就坏了

hashCode和equals共同判断是否相等
所以重写equals必须重写hashCode，先调hashCode，相等再调equals
实际上应该是相等的对象必须具有相同的hash值，而默认的hash值时通过地址计算的

String
String不可变（内部使用final关键字，也没public方法修改），StringBuilder不安全，StringBuffer安全
JDK9中直接用"+"，唯一一个重载，但是for循环里面不会服用StringBuilder

字符串常量池

String s1 = new String("abc");这句话创建了几个字符串对象？
会创建 1 或 2 个字符串对象
常量池有了的话只会在堆中创建

String#intern（String类的intern方法），将字符串对象的引用保存在常量池中，返回引用

异常
Exception与Error
他们的父类的Throwable，前者可以被catch，后者不建议catch，一般是些没法处理的问题，例如Virtual MachineError，OutOfMemoryError（OOM），NoClassDefFoundError
checked异常必须被处理，要么自己try catch，要么在函数名后加上throws xxx交给调用者处理

Checked Exception与Unchecked
checked没被catch或throws是不让过编译的
除了RuntimeException和它的子类其他全是checked，例如IO，ClassNotFoundException，SQLException

unchecked，例如NullPointerException、IllegalArgumentException，ArrayIndexOutOfBoundsException

Throwable类
String getMessage(): 返回异常发生时的简要描述
String toString(): 返回异常发生时的详细信息
String getLocalizedMessage(): 在 Throwable 的子类覆盖这个方法，可以生成本地化信息。如果子类没有覆盖该方法，则该方法返回的信息与 getMessage()返回的结果相同
void printStackTrace()

try-catch-finally
finally不要return，否则try中return会被忽略

try-with-resources：会自动调用close

泛型
public class GenericClass<T>{}
public <T> void genericFunction(T t){}

反射
说用了反射不如说自己用了注解，注解是通过编译器扫描替换或反射实现的
Jetpack Compose中的@Component
默认必须有Target注明注解对象，Retention注明修饰的类型

SPI与API
API由接口方实现，SPI由调用方实现，调用方只需要定标准
比如说一个框架，API就是程序员直接用，SPI是框架扩展人员使用，比如说通过注入来改变软件的行为方式，我感觉有点像Java的接口，例如一个Array，定义了一个List接口，然后实现是ArrayList

（日志）

SPI缺点：并发实例不安全，遍历效率低（整个类都得load），错误不好定位

序列化/反序列化
数据结构与字节流的转换过程

类似于应用层变成传输数据的数据包
禁止序列化，transient，用在不想被序列化的数据前
JSON、XML也是一种文本类序列化的方式

自带的序列化不支持跨语言、性能差、不安全
Protobuf见得多，是一种基于二进制的序列化方法

流
InputStream/Reader（字符）
OutputStream/Writer（字符）
字节流byte
字符流string
字节快，后者编码问题

语法糖
泛型、自动拆装箱、变长参数、枚举、内部类、增强 for 循环、try-with-resources 语法、lambda 表达式

集合
集合概览
Collection、Map两大接口
Collection下有List、Set、Queue接口

List有序
Set无序
Queue
Map kv型

API
https://javaguide.cn/java/collection/java-collection-questions-01.html#queue-1

List
ArrayList数组（动态）
Vector数组
LinkedList双向链表
Set
HashSet（HashMap实现的）
LinkedHashSet，HashSet的子类，通过LinkedHashMap实现，LinkedHashMap又是基于HashMap实现的，维护了添加顺序
TreeSet红黑树
Queue
PriorityQueue数组实现的二叉堆（完全二叉树）
ArrayQueue数组+双指针
Map
HashMap数组Hash，链表解决冲突（拉链法）。数组先扩容后链表长度大于阈值转化为红黑树
LinkedHashMap（可以顺序访问插入的数据）
Hashtable数组+链表（有全局锁）（ConcurrentHashMap是分段锁，更快）（ConcurrentHashMap）、CopyOnWriteArrayList）
TreeMap红黑树


ConcurrentHashMap：
利用 synchronized +比较交换锁写入数据（防止ABA）（Node加锁），Node是数组和红黑树的转换，锁升级机制也提高了性能

Comparable 和 Comparator：
Comparable 接口实际上是出自java.lang包 它有一个 compareTo(Object obj)方法用来排序Comparator接口实际上是出自 java.util 包它有一个comp

基础
代理模式
定义一个接口
写一个类实现一个接口
定义一个代理

语法糖：
泛型擦除
box/unbox
内部类
assert竟然不是默认启用的！！！

string、stringbuilder是变长的、stringbuffer是线程安全的

浅拷贝和引用的区别是对象还是不同的！但数据可能是相同的（地址）

string为什么不能被继承，我认为主要是两点，一是性能，二是安全性，性能是经过final修饰JIT可以做各种优化而不用进行很多安全检查，安全性是不可变对象是线程安全的

sleep与yield
yield会让出执行权，但是比它优先级更低的也不会执行

JNI允许Java代码和其他语言写的代码进行交互

权限修饰符：public protected default private

父类向子类转换：子父子+强制转换
容器
ArrayList 和 Array
ArrayList中使用泛型，而Array中使用Object来储存数据，所以ArrayList更安全
总的来说凡是使用泛型的最好都用包装类型

Array能不能存null得分情况，基本数据类型的Array是不让存null的，对象当然可以

List容器
ArrayList
LinkedList

Set容器
HashSet
LinkedHashSet
TreeSet

Queue容器
PriorityQueue
ArrayQueue

Map容器
HashMap
LinkedHashMap
Hashtable
TreeMap

Hashtable线程安全，所有操作都加锁，KV都不能是null
HashMap，KV都可以是null，当K是null时直接Key=0

选择 TreeMap和HashMap，线程安全ConcurrentHashMap

RandomAccess
只有数组类的能够实现RandomAccess接口，可以直接直接计算元素的地址进行访问

offer、poll、peak会返回特殊值（也不是不会抛出异常，容量问题才不会抛出异常）

Map类容器有一个loadfactor，这个其实是已用/总共，小于这个数就会进行扩容
Hashtable默认大小是11，用了质数减少冲突，HashMap默认大小是16，方便进行Hash（v&size-1）
HashMap链表长度>8且数组长度大于64时会转换为红黑树

循环遍历删除，去调用迭代器的remove方法而不是原集合的remove方法（会报ConcurrentModificationException）

toMap方法value为null时会空指针异常

Collection#removeIf来删除元素

ArrayList 1.5倍扩容
add用了System.arraycopy，toArray和扩容用了Arrays.copyOf

ConcurrentHashMap主要是写入的时候加锁，如果Node为空就CAS写入数据
如果hashcode==MOVED扩容
否则就加sychronized

CopyOnWriteArrayList使用ReentrantLock与COW，直接读

Thread是类Runnable是接口

ArrayBlockingQueue有put和take

并发
Java起码有两个栈：虚拟机栈和本地方法栈，多线程会有更多栈

公有：堆和字符串常量池
私有：虚拟机栈、本地方法栈、程序计数器

并发比起并行来并不是真正同时执行，同步在结果没有返回之前会一直等待

线程生命周期：
NEW
RUNNABLE（操作系统在此基础上有READY和RUNNING）
BLOCKED（从线程的生命周期来讲一般是不处于WAITING状态且锁被其他线程持有）（sleep，suspend，wait，yield）（说人话，sleep、wait，无法获取锁，IO阻塞）
WAITING
TIME_WAITING
TERMINATED

sleep和wait
sleep不释放锁
wait用于线程间通信
sleep是thread的static方法，而wait是Object本地方法

悲观锁例子：ReentrantLock
乐观锁例子：Longadder

CAS有ABA的问题，循环时间稍长，只能操作一个变量

公平锁：先申请先获得
非公平锁：随机，性能更好

sychronized：隐式，关键字
ReetrantLock：显式，类，粒度更小、扩展性更好

线程池：
maxCoreSize 即使是有空闲的线程也会创建新线程来执行任务
maxPoolSize 队列满了后才会使用超过maxCoreSize的部分
Queue
可能还有Factory和Reject Handler

Callable可以抛出异常和返回结果，Runnable更简洁

线程池饱和策略
AbortPolicy 抛RejectedExecutionException
CallerRunsPolicy 调用当前线程运行
DiscardPolicy 直接扔
DiscardOldestPolicy 丢弃最早到且未处理的任务

跳表：分层设计，上面的层有较大的粒度

IO
装饰器模式：组合代替继承，强调增加新功能
适配器模式：接口互不兼容的类的协调工作
工厂模式：就是把创建对象的代码封装起来
观察者模式：消息传递

JVM
总的来说，分：
程序计数器
Java 虚拟机栈
本地方法栈
堆
方法区
运行时常量池
字符串常量池
直接内存
图片: https://odocs.myoas.com/uploader/f/4ZLy10Bnr7wbpv83.png?accessToken=eyJhbGciOiJIUzI1NiIsImtpZCI6ImRlZmF1bHQiLCJ0eXAiOiJKV1QifQ.eyJleHAiOjE2OTE2MzA1MDcsImZpbGVHVUlEIjoiUjEzajhNMXJyTnN3cG1rNSIsImlhdCI6MTY5MTYyOTkwNywiaXNzIjoidXBsb2FkZXJfYWNjZXNzX3Jlc291cmNlIiwidXNlcklkIjoyODAzNDJ9.0F8nk1D8xQLcKm1XllHxWTHa-hm03zX_0CI8uCIpyp4


虚拟机栈是执行class的
本地方法栈是执行 native方法的
堆存放对象实例和数组

内存分配：
对象都会首先在 Eden 区域分配，在一次新生代垃圾回收后，如果对象还存活，则会进入 S0 或者 S1，并且对象的年龄还会加 1(Eden 区->Survivor 区后对象的初始年龄变为 1)，当它的年龄增加到一定程度，就会被晋升到老年代中。

方法区会存储已被虚拟机加载的 类信息、字段信息、方法信息、常量、静态变量、即时编译器编译后的代码缓存等数据。可以认为方法区是元空间的接口，元空间是方法区的实现。

Java主要管理的是堆
分代垃圾收集算法：Eden->S0->S1->Tenured->MetaSpace

对象会优先在Eden分配，当Eden满了后会执行一次Minor GC，将无法分配到S0、S1的对象直接转移到Tenured。其他的则会分配到S0、S1。

每在S0、S1经过一次Minor GC age就会增1，到达阈值时就会升级到老年代。

这里不如看官方的说明（ParallelGC）
首先GC是分两种的，一种Automatic GC，一种Generational GC
MetaSpace使用来存运行中应用需要的外部class和method的，full GC包括MetaSpace
1、所有新对象都放在Eden
2、Eden满后触发minor GC
3、有引用的对象会放在S0，没引用的会被清空
4、下一次minor GC时Eden中有引用的对象会放在S1，S0中的有引用的对象age增1，也向S1移动
5、再下一次minor GC同4，S0和S1身份对调
6、之后的minor GC后，age到达阈值的对象会移动到Tensured
7、最后，Tensured会发生major GC清空未使用的对象

死亡判断
引用计数：不用，有循环引用的问题
可达性分析：从GC Roots（包括活动线程、静态变量、JNI引用）出发，不可达的就是可以回收的
有强引用（OOM都不GC）、软引用（可以被GC）、弱引用（很容易被GC）、虚引用（不对GC产生影响）

GC算法：
标记-清除：标记不回收的，完事后清除
效率不高+内存碎片

复制算法：分两块，复制不回收的
可用内存变小+如果不回收的比较对就慢

标记-整理：存活对象向一端移动
效率不高

分代收集：前面介绍的

GC算法实现：
Serial：STW（stop the world）
ParNew：前面的多线程版本，新生代标记-复制、老年代标记-整理
Parallel Scavenge：关注CPU使用而不是停顿

CMS：
并发，标记-清除
1、暂停用户线程记录root，2、开启用户线程记录可达对象并跟踪新的部分，3、重新标记前面的新的部分，4、并发清除

另外还有G1、ZGC
这两个主要是直接将堆分为若干个区域，通过标记region确定区域类别，多了一个Humongous用来存放大对象

类
生命周期
加载-验证-准备-解析-初始化-使用-卸载

重点是加载器：
加载：将二进制数据流映射成为相应的数据结构，生成class对象

每个class都能获得其getClassLoader
有三种：BootstrapClassLoader（JVM的一部分，所以如果getClassLoader是null的话就是它了）、ExtensionClassLoader、AppClassLoader

双亲委派模型：
先委托给其父类加载class，如果父类找不到再由其加载
主要是为了避免重复加载，因为被不同类加载器加载的类被视为两个不同的类，能够直达顶层加载器

新特性
Java8 
字符串增强
Interface的default和static
Lambda
stream：strings.stream().forEach(System.out::println);

Java11
字符串增强
ZGC
Lambda：可以用var进行局部变量类型推断

Java17
增强伪随机数
删除Applet
switch类型匹配：case Integer i -> String.format("int %d", i);
