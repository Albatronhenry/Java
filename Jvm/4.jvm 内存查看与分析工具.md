[jvm 内存查看与分析工具](http://blog.chinaunix.net/uid-29632145-id-4615921.html)
----------------
* jps  虚拟机进程状况工具
  * 可以列出正在运行的虚拟机进程  其他JDK工具大多需要输入它查询到LVMID（本地虚拟机唯一ID）来确定要监控的是哪一个虚拟机进程,对于本地虚拟机,LVMID与操作系统ID是一致的
  * jps命令格式
    * jps [options][hostid]      cmd进入JDK的bin目录下,输入` jps -l  ` 可以显示所有进程,其他命令网络搜索使用
* jstat 虚拟机统计信息监视工具
* jinfo java配置信息工具   实时查看和调整虚拟机各项参数  jinfo -flag可以进一步细致的查看使用jps -v未被显示指定的参数的系统默认值    
* jmap 内存映像工具
     * jmap是jdk自带的jvm内存分析的工具，位于jdk的bin目录,所以使用时需要进入bin目录下
     
     ` jmap -dump:file=c:\dump.txt 5404   注意5404是我本机的java进程pid `
     
* jhat 虚拟机堆转储快照分析工具(一般不用来分析dump,耗时消耗硬件资源,分析功能比较简陋)

     * 上面说了，有很多工具都能分析jvm的内存dump文件，jhat就是sun jdk6及以上版本自带的工具，位于jdk的bin目录，执行 jhat -J -Xmx512m [file] ，
    
     * file就是dump文件路径。jhat内置一个简单的web服务器，此命令执行后，jhat在命令行里显示分析结果的访问地址
     
     ` jhat -J-Xmx512m  c:\dump.txt `  执行这句之后就会启动相应的端口 本级启动端口是 ` 7000 ` ,因此网页打开` http://localhost:7000/ `即可访问 
[JDK可视化工具]（）
----------
* jconsole  监视与管理控制台
     * jconsole是jdk自带的一个内存分析工具，它提供了图形界面。可以查看到被监控的jvm的内存信息，线程信息，类加载信息，MBean信息。 
* 其他查看分析工具点击蓝色链接查看
    
    
