#### [String、String.valueOf、toString](http://blog.csdn.net/u012467492/article/details/52995489)

1.String：
---------

毫无疑问，这种就是强转形式，简单方便，效率高。

强转原本就是字符串的东西，如果原本不是字符串的话，那么就会报错。

```java

Boolean boolean1 = true;         
String str3 = (String)boolean1;//这行代码会报错，编译不过

```

2.toString():
---------------

在API文档中是这样说的，返回此对象本身（它已经是一个字符串了！！！）。按照它的意思就是说一般的对象或者参数都是有toString()的方法的，只是要注意在一个参数

定义为int类型是就没有这个方法了。还有就是当参数为空的时候.toString()方法就会报出空指针异常，这是这个方法的不好的地方使用时需要仔细斟酌一下

```java

Object obj = getObject();
System.out.println(obj.toString());

```

就如这上面的代码表示的一样，如果obj不为空，那么就能正常编译，那么如果obj取出来为空的话，那么就会报出空指针异常的。

3.String.valueOf()：
-------------------

这个方法是静态的，直接通过String调用，可以说是完美，只是平时不习惯这样写而已，这样的实现避免了前面两个的不足和缺点。首先来看看他内部的实现机制：

```java

public static String valueOf(Object obj){return (obj==null) ? "null" : obj.toString()};

```

```java
 
     /**
	   * 输出为1
	   */  
	  int i = 1;
		System.err.println(String.valueOf(i));
		
	   /**
	   * 输出为空(null值) 
	   */   
        char[] chars={' '};  
        String.valueOf(chars); 
        
      // 导致空指针  
        char[] chars1=null;  
        String.valueOf(chars1);  

```

[为什么String.valueOf(null)，会走到valueOf(char[])这个重载，而不是其他重载呢？](http://blog.csdn.net/yangzhaomuma/article/details/51173138)
-------------------------------------------------------------------------

因为java中对重载的匹配是，当重载都能匹配的时候，优先选择范围小，精度高的方法，因此，它自动重载了char[]这个方法。



