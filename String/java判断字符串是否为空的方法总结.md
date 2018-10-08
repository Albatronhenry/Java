[java 判断字符串是否为空的普通方法:](https://www.cnblogs.com/misybing/p/4833447.html)

* 方法一: 最多人使用的一个方法, 直观, 方便, 但效率很低:

```java
                      if(s == null ||"".equals(s));
                                    
```

* 方法二: 比较字符串长度, 效率高, 是我知道的最好一个方法:

```java
                      if(s == null || s.length() <= 0);
                      
 ```
 
* 方法三: Java SE 6.0 才开始提供的方法, 效率和方法二几乎相等, 但出于兼容性考虑, 推荐使用方法二.

```java
                     if(s == null || s.isEmpty());
```

* 方法四: 这是一种比较直观,简便的方法,而且效率也非常的高,与方法二、三的效率差不多:

```java
                     if (s == null || s == "");
```
 

注意:s == null 是有必要存在的.

　　如果 String 类型为null, 而去进行 equals(String) 或 length() 等操作会抛出java.lang.NullPointerException.

　　并且s==null 的顺序必须出现在前面，不然同样会抛出java.lang.NullPointerException.

　　如下Java代码:
  
  ```java

　　String str = null;

　　if(str.equals("") || str= == null){//会抛出异常

　　          System.out.println("success");

　　}

　　// "".equals(str);后置确保不会遇null报错。
  
```  
  -------------
  
  if(str=.equals("") || str= == null){//会抛出异常
 "".equales(str);后置确保不会遇null报错。
 
 原因解释:
 
   可以假设，如果str 是NULL, 他就不是一个字符串， NULL代表声明了一个空对象，根本就不是一个字符串。所以他就没有 equals() 这个方法，
   自然就报错了。而你写成 "".equals(str); 就不会有这个问题 ，因为 "" 是个字符串，有equals() 这个方法。

### 上面方法只能简单处理一般为空，在实际开发中，会出现NPE异常，使用工具类可以解决一般为空判断的NPE异常:

[StringUtils工具类的常用方法参考链接（isNotEmpty isNotBlank等）](https://blog.csdn.net/szwangdf/article/details/4075256)

下面分别对一些常用方法做简要介绍：

1. public static boolean isEmpty(String str)    判断某字符串是否为空，为空的标准是 str==null 或 str.length()==0    
下面是 StringUtils 判断是否为空的示例： 
```java
StringUtils.isEmpty(null) = true
StringUtils.isEmpty("") = true 
StringUtils.isEmpty(" ") = false //注意在 StringUtils 中空格作非空处理
StringUtils.isEmpty("   ") = false
StringUtils.isEmpty("bob") = false
StringUtils.isEmpty(" bob ") = false 
```
 
2. public static boolean isNotEmpty(String str)    判断某字符串是否非空，等于 !isEmpty(String str)    下面是示例： 
```java
StringUtils.isNotEmpty(null) = false      
StringUtils.isNotEmpty("") = false      
StringUtils.isNotEmpty(" ") = true      
StringUtils.isNotEmpty("         ") = true      
StringUtils.isNotEmpty("bob") = true      
StringUtils.isNotEmpty(" bob ") = true
```
3. public static boolean isBlank(String str)    判断某字符串是否为空或长度为0或由空白符(whitespace) 构成   下面是示例：  
```java
StringUtils.isBlank(null) = true      
StringUtils.isBlank("") = true      
StringUtils.isBlank(" ") = true      
StringUtils.isBlank("        ") = true      
StringUtils.isBlank("/t /n /f /r") = true   //对于制表符、换行符、换页符和回车符 
StringUtils.isBlank()   //均识为空白符      
StringUtils.isBlank("/b") = false   //"/b"为单词边界符      
StringUtils.isBlank("bob") = false      
StringUtils.isBlank(" bob ") = false 
```
4. public static boolean isNotBlank(String str)    判断某字符串是否不为空且长度不为0且不由空白符(whitespace) 构成，等于 !isBlank(String str)    下面是示例：
```java
StringUtils.isNotBlank(null) = false      
StringUtils.isNotBlank("") = false      
StringUtils.isNotBlank(" ") = false      
StringUtils.isNotBlank("         ") = false      
StringUtils.isNotBlank("/t /n /f /r") = false      
StringUtils.isNotBlank("/b") = true      
StringUtils.isNotBlank("bob") = true      
StringUtils.isNotBlank(" bob ") = true 
```
