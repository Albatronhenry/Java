# Java
reflect Q&A

e.g
---------------------------------------------------

    
```java

> package com.yonyou;

public class Test02 {

	public static void main(String[] args) {
	
	  1----------->针对产生的对象获取
		Henry henry = new Henry();
		System.err.println(henry.getClass());
		
          2----------->针对类名直接获取
		System.out.println(Henry.class);
		
  
		try {
	   3 --------->直接Class类通过包名获取
			Class h1 =Class.forName("com.yonyou.Henry");
			System.out.println(h1);
		} catch (ClassNotFoundException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		System.err.println();

	}

}
class Henry{
	public Henry(){
		System.err.println("Henry's constructor");
	}
}

``` 



