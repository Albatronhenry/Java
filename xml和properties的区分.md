# Java

配置文件一般为后缀名是`.xml`或者是`.properties`的文件，当然两者的共同点就是存储项目启动所需的环境设置啦！今天我们主要对比一下他们之间的不同。


【***`看外表`***】

1、sys-config.xml
2、sys-config.properties



【***`对比`***】从表面上看，.xml格式的要比.properties格式的结构要清晰一些，而.properties文件要比.xml文件结构要简单一些。

【***`看内涵`***】

   1、从结构上来说：
       .xml文件主要是树形结构。
   .properties文件主要是以key-value键值对的形式存在。

   2、从灵活程度上来说：
          .xml格式的文件要比.properties格式的文件更灵活一些
   .properties格式的文件已键值对形式存在，主要就是赋值，而且只能赋值，不能够进行其他的操作。
   .xml格式的文件可以有多种操作方法，例如添加一个属性，或者做一些其他的定义等。

   3、从使用便捷程度来说：  
        .properties格式的文件要比.xml文件配置起来简单一些。
   配置.properties只需要简单的getProperty(key)方法或者setProperty(key,value)方法就可以读取或者写入内容；
   配置.xml文件的时候通常要查看文档，因为配置比较繁琐，花费时间长才可以配置完整。

  4、从应用程度上来说：
      .properties文件比较适合于小型简单的项目。
   .xml文件适合大型复杂的项目，因为它比较灵活。
   
   [Reference-website](http://blog.csdn.net/luckystar689/article/details/52578317)
