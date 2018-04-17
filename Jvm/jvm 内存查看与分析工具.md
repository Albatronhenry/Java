[jvm 内存查看与分析工具](http://blog.chinaunix.net/uid-29632145-id-4615921.html)
----------------
* jconsole
     * jconsole是jdk自带的一个内存分析工具，它提供了图形界面。可以查看到被监控的jvm的内存信息，线程信息，类加载信息，MBean信息。
     
* jmap
     * jmap是jdk自带的jvm内存分析的工具，位于jdk的bin目录,所以使用时需要进入bin目录下
     
     ` jmap -dump:file=c:\dump.txt 5404   注意5404是我本机的java进程pid `
     
* jhat

     * 上面说了，有很多工具都能分析jvm的内存dump文件，jhat就是sun jdk6及以上版本自带的工具，位于jdk的bin目录，执行 jhat -J -Xmx512m [file] ，
    
     * file就是dump文件路径。jhat内置一个简单的web服务器，此命令执行后，jhat在命令行里显示分析结果的访问地址
     
     ` jhat -J-Xmx512m  c:\dump.txt `  执行这句之后就会启动相应的端口 本级启动端口是 ` 7000 ` ,因此网页打开` http://localhost:7000/ `即可访问 
     
* 其他查看分析工具点击蓝色链接查看
    
    
