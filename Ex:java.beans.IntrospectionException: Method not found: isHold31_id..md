[Exception in thread "main" java.beans.IntrospectionException: Method not found: isHold31_id](https://blog.csdn.net/raynaing/article/details/51614664)

工作中，使用反射方法调用，一直报上面的错误，后面检查发现是对应bean/DTO中的属性大小写没有正确书写，特意记录

如果bean中属性改成如下定义正确，private是可以反射拿到的
```java
	private String Hold31_id;
	
	public String getHold31_id() {
		return Hold31_id;
	}

	public void setHold31_id(String hold31_id) {
		Hold31_id = hold31_id;
	}
 ```
 

