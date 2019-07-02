项目中因需要将一个查询出来的字符转变成数字，然后再将数字转变为字符，其中出现一些问题，[特此备注](https://blog.csdn.net/iteye_12157/article/details/81891407)

刚开始的时候考虑直接使用int强转，但是因为数字为 8251007710（超过int长度，故选用double类型

但是存在问题就是double类型直接使用科学计数法了，这与我们的业务场景需要保存数据不一致，所以需要格式化

```java
String numString = "8251007710";
double db = Double.parseDouble(numString);
DecimalFormat df = new DecimalFormat("0");
numString = df.format(++db);
```
