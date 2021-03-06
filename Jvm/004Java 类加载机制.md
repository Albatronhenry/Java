[Java 类加载机制](http://www.cnblogs.com/aspirant/p/7200523.html)
-------------
#### 类加载器
负责读取 Java 字节代码，并转换成java.lang.Class类的一个实例；

类加载器与类的”相同“判断
类加载器除了用于`加载类`外，还可用于确定类在Java虚拟机中的`唯一性`

即便是同样的字节代码，被不同的类加载器加载之后所得到的类，也是不同的。

通俗一点来讲，要判断两个类是否“相同”，前提是这两个类必须被同一个类加载器加载，否则这个两个类不“相同”。

这里指的“相同”，包括类的Class对象的`equals()`方法、`isAssignableFrom()`方法、`isInstance()`方法、`instanceof`关键字等判断出来的结果。

#### 类加载器种类

启动类加载器，Bootstrap ClassLoader，加载JACA_HOME\lib，或者被-Xbootclasspath参数限定的类

扩展类加载器，Extension ClassLoader，加载\lib\ext，或者被java.ext.dirs系统变量指定的类

应用程序类加载器，Application ClassLoader，加载ClassPath中的类库

自定义类加载器，通过继承ClassLoader实现，一般是加载我们的自定义类

#### 双亲委派模型

类加载器 Java 类如同其它的 Java 类一样，也是要由类加载器来加载的；除了启动类加载器，每个类都有其父类加载器（父子关系由组合（不是继承）来实现）；

所谓双亲委派是指每次收到类加载请求时，先将请求委派给父类加载器完成（所有加载请求最终会委派到顶层的Bootstrap ClassLoader加载器中），如果父类加载器无法完成这个加载（该加载器的搜索范围中没有找到对应的类），子类尝试自己加载。

![22](https://images2015.cnblogs.com/blog/879896/201604/879896-20160415085506488-408997874.png)
##### 双亲委派好处

* 避免同一个类被多次加载；
* 每个加载器只能加载自己范围内的类； 

#### 类加载过程
类加载分为三个步骤：`加载`，`连接`，`初始化`；

如下图 , 是一个类从加载到使用及卸载的全部生命周期，图片来自参考资料；

![44](https://images2015.cnblogs.com/blog/879896/201604/879896-20160414224549770-60006655.png)


#### 加载
根据一个类的全限定名(如cn.edu.hdu.test.HelloWorld.class)来读取此类的二进制字节流到JVM内部;

将字节流所代表的静态存储结构转换为方法区的运行时数据结构（hotspot选择将Class对象存储在方法区中，Java虚拟机规范并没有明确要求一定要存储在方法区或堆区中）

转换为一个与目标类型对应的java.lang.Class对象；

#### 连接
##### 验证

验证阶段主要包括四个检验过程：文件格式验证、元数据验证、字节码验证和符号引用验证;

##### 准备

为类中的所有静态变量分配内存空间，并为其设置一个初始值（由于还没有产生对象，实例变量将不再此操作范围内）；

##### 解析

将常量池中所有的符号引用转为直接引用（得到类或者字段、方法在内存中的指针或者偏移量，以便直接调用该方法）。这个阶段可以在初始化之后再执行。

##### 初始化
  在连接的准备阶段，类变量已赋过一次系统要求的初始值，而在初始化阶段，则是根据程序员自己写的逻辑去初始化类变量和其他资源，举个例子如下：
```java
    public static int value1  = 5;
    public static int value2  = 6;
    static{
        value2 = 66;
    }
```
在准备阶段value1和value2都等于0；

在初始化阶段value1和value2分别等于5和66；

*  所有类变量初始化语句和静态代码块都会在编译时被前端编译器放在收集器里头，存放到一个特殊的方法中，这个方法就是<clinit>方法，即类/接口初始化方法，该方法只能在类加载的过程中由JVM调用；
*  编译器收集的顺序是由语句在源文件中出现的顺序所决定的，静态语句块中只能访问到定义在静态语句块之前的变量；
*  如果超类还没有被初始化，那么优先对超类初始化，但在<clinit>方法内部不会显示调用超类的<clinit>方法，由JVM负责保证一个类的<clinit>方法执行之前，它的超类<clinit>方法已经被执行。
*  JVM必须确保一个类在初始化的过程中，如果是多线程需要同时初始化它，仅仅只能允许其中一个线程对其执行初始化操作，其余线程必须等待，只有在活动线程执行完对类的初始化操作之后，才会通知正在等待的其他线程。(所以可以利用静态内部类实现线程安全的单例模式)
*  如果一个类没有声明任何的类变量，也没有静态代码块，那么可以没有类<clinit>方法；
##### 何时触发初始化

* 为一个类型创建一个新的对象实例时（比如new、反射、序列化）
* 调用一个类型的静态方法时（即在字节码中执行invokestatic指令）
* 调用一个类型或接口的静态字段，或者对这些静态字段执行赋值操作时（即在字节码中，执行getstatic或者putstatic指令），不过用final修饰的静态字段除外，它被初始化为一个编译时常量表达式
* 调用JavaAPI中的反射方法时（比如调用java.lang.Class中的方法，或者java.lang.reflect包中其他类的方法）
* 初始化一个类的派生类时（Java虚拟机规范明确要求初始化一个类时，它的超类必须提前完成初始化操作，接口例外）
* JVM启动包含main方法的启动类时。
