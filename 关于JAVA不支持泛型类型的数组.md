[关于JAVA不支持泛型类型的数组](http://www.blogjava.net/sean/archive/2005/08/09/9630.html)

因为这样做会破坏类型安全。核心的问题在于Java范型和C#范型存在根本区别：Java的范型停留在编译这一层，到了运行时，这些范型的信息其实是被抹掉的；而C#的范型
做到了MSIL这一层。Java的做法不必修改JVM，减少了潜在的大幅改动和随之而来的风险，也许同时也反映出Java Bytecode规范在设计之初的先天不足；C#则大刀阔斧，连
CLR一起改以支持更彻底的范型，换句话说，在范型这一点上，感觉C#更C++一点。
 
在Java中，Object[]数组可以是任何数组的父类，或者说，任何一个数组都可以向上转型成它在定义时指定元素类型的父类的数组，这个时候如果我们往里面放不同于原始数
据类型 但是满足后来使用的父类类型的话，编译不会有问题，但是在运行时会检查加入数组的对象的类型，于是会抛ArrayStoreException：

```java

String[] strArray = new String[20];
Object[] objArray = strArray;
objArray[0] = new Integer(1); // throws ArrayStoreException at runtime
 
```

因为Java的范型会在编译后将类型信息抹掉，这样如果Java允许我们使用类似

```java

Map<Integer, String>[] mapArray = new Map<Integer, String>[20];

```

这样的语句的话，我们在随后的代码中可以把它转型为Object[]然后往里面放Map<Double, String>实例。这样做不但编译器不能发现类型错误，就连运行时的数组存储检查
对它也无能为力，它能看到的是我们往里面放Map的对象，我们定义的<Integer, String>在这个时候已经被抹掉了，于是而对它而言，只要是Map，都是合法的。

[拓展](https://www.cnblogs.com/scutwang/articles/3735219.html)
