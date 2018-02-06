### String中的trim()方法

项目部分代码使用:

```java

// 如果 没有条件限制则返回全部
    if (relationCodes == null || relationCodes.trim().equals("")) {
      return result;
    }
// 过滤
    String[] contidion = relationCodes.trim().replace('|', ',').split(",");
    List list = result.getRecordList();

```

测试代码:

```java

    public static void main(String arg[]){  
      
            String a=" hello world ";  
      
            String b="hello world";  
      
            System.out.println(b.equals(a));  
      
            a=a.trim();//去掉字符串首尾的空格  
      
            System.out.println(a.equals(b));  
        }  

执行结果：
        a: hello world  , false
        a: hello world  , true 

```

trim(replace(request("pwd"),"'",""))：将替换之后的值首尾两端的空格去掉。

    * 去除空格的作用在于防止有时因系统自身格式多加了空格而造成该值与数据库相应的值不相等；
    
    * 将单引号去掉或变成全角的意义在于防止简单的SQL语句注入而造成不必要的损失。
