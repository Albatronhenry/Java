#  [String字符串拼接方式比较](http://blog.csdn.net/yh_zeng2/article/details/73441551)

字符串String的拼接有：
-------------------

* “+” 

* concat () 

* StringBuilder

* StringBuffer

性能的从低到高进行排序，则顺序为：

“+”  <  concat ()  < StringBuffer < StringBuilder 。

使用"+"性能是最差的，应该避免使用！！！

StringBuilder的性能是最高的，StringBuffer和StringBuilder之间怎么取舍要用哪个？
--------------------------------------------------------------------------

两者的区别是：


StringBuffer是 ` 线程安全 ` 的，而StringBuilder不是。

在 ` 高并发的应用 ` 中，应该考虑使用StringBuffer! ！ 

大家查看JDK源码就可以知道，StringBuffer和StringBuilder这两个类实现的接口都是一样的，只不过 StringBuffer的很多方法
都加上了 ` synchronized ` 关键字修饰。

性能测试代码及时间如下:
---------------------

```java

public class TestOne  
{  
  
    public static void main(String args[]) {  
        int num = 100000;  
        testAdd(num);  
        testConcat(num);  
        testStringBuffer(num);  
        testStringBuilder(num);  
    }  
  
    public static void testAdd(int num){  
        long start = System.currentTimeMillis();  
        String str = "";  
        for(int i = 0; i < num; i++){  
            str += i;  
        }  
        System.out.println("字符串拼接使用 + 耗时：" + (System.currentTimeMillis() - start) + "ms");  
    }  
  
    public static void testConcat(int num){  
        long start = System.currentTimeMillis();  
        String str = "";  
        for(int i = 0; i < num; i++){  
            str.concat(String.valueOf(i));  
        }  
        System.out.println("字符串拼接使用 concat 耗时：" + (System.currentTimeMillis() - start) + "ms");  
    }  
  
    public static void testStringBuffer(int num){  
        long start = System.currentTimeMillis();  
        StringBuffer stringBuffer = new StringBuffer();  
        for(int i = 0; i < num; i++){  
            stringBuffer.append(String.valueOf(i));  
        }  
        stringBuffer.toString();  
        System.out.println("字符串拼接使用 StringBuffer 耗时：" + (System.currentTimeMillis() - start) + "ms");  
    }  
  
    public static void testStringBuilder(int num){  
        long start = System.currentTimeMillis();  
        StringBuilder stringBuilder = new StringBuilder();  
        for(int i = 0; i < num; i++){  
            stringBuilder.append(String.valueOf(i));  
        }  
        stringBuilder.toString();  
        System.out.println("字符串拼接使用 StringBuilder 耗时：" + (System.currentTimeMillis() - start) + "ms");  
    }  
  
  
}  


```

控制台运行结果:
-------------------

字符串拼接使用 + 耗时：36647ms

字符串拼接使用 concat 耗时：49ms

字符串拼接使用 StringBuffer 耗时：21ms

字符串拼接使用 StringBuilder 耗时：17ms

