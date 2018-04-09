 [==和equals区别](https://blog.csdn.net/chance2015/article/details/51427304)
----------------------

* 普通类型比较:
  == 和 equals 没有区别
  
  * String对象 == 和equals 有区别
  

```java

package com.yonyou;
import java.util.ArrayList;
import java.util.List;

public class TestTwo {
	public static void main(String[] args) {
		int i = 1;
		int j = 1;
		System.err.println(i == j); // true  普通类型
		String k = "henry";
		String L = "henry";
		System.err.println(k == L); // true  普通类型
		System.err.println(k.equals(L)); // true  普通类型
		
		String M = new String("henry");
		String N = new String("henry");
		System.err.println(M == N);  //false  对象引用地址不同
		System.err.println(M.equals(N));  //true  String对象中重写了equals方法
		
		List ls1 = new ArrayList();
		ls1.add(M);
		List ls2 = new ArrayList();
		ls2.add(N);
		System.err.println(ls1.equals(ls2));  //true
		
	}
}

  
```
