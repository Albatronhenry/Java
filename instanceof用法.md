java 中的[instanceof](http://blog.csdn.net/liranke/article/details/5574791) 运算符是用来在运行时指出对象是否是特定类的一个实例。instanceof通过返回一个布尔值来指出，这个对象是否是这个特定类或者是它的子类
的一个实例。

用法：

result = object instanceof class

参数：

Result：布尔类型。

Object：必选项。任意对象表达式。

Class：必选项。任意已定义的对象类。

说明：

如果 object 是 class 的一个实例，则 instanceof 运算符返回 true。如果 object 不是指定类的一个实例，或者 object 是 null，则返回 false。

 

例子如下：

```java

package com.yonyou;

interface A {
}

class B implements A {

}

class C extends B {

}

public class TestTwo {
	public static void main(String[] args) {
		A a = null;
		B b = null;
		boolean res;

		System.out.println(" ---instanceoftest test case 1: ---");
		res = a instanceof A;
		System.out.println("a instanceof A: " + res);

		res = b instanceof B;
		System.out.println("b instanceof B: " + res);

		System.out.println("/n ---instanceoftest test case 2: ---");
		a = new B();
		b = new B();

		res = a instanceof A;
		System.out.println("a instanceof A: " + res);

		res = a instanceof B;
		System.out.println("a instanceof B: " + res);

		res = b instanceof A;
		System.out.println("b instanceof A: " + res);

		res = b instanceof B;
		System.out.println("b instanceof B: " + res);

		System.out.println("/n ---instanceoftest test case 3: ---");
		B b2 = (C) new C();

		res = b2 instanceof A;
		System.out.println("b2 instanceof A: " + res);

		res = b2 instanceof B;
		System.out.println("b2 instanceof B: " + res);

		res = b2 instanceof C;
		System.out.println("b2 instanceof C: " + res);
	}
}


```

---------

运行结果如下:

![instance of](https://github.com/Albatronhenry/UploadFile/blob/master/pic/instance%20of.png)



