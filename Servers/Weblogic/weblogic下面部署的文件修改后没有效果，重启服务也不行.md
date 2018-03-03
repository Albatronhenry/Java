### [weblogic下面部署的文件修改后没有效果，重启服务也不行](https://zhidao.baidu.com/question/511444769.html)

解决方法:
-----------

因为在{domain}/servers/AdminServer/下有jsp缓存，停止服务后，请删除该目录下的tmp目录与cache目录，再启动服务

其他解释:

浏览器的缓存清理为Ctrl+F5。server缓存如果是jsp或js文件，Linux环境下一般touch下就好了，建议看下用户权限，如果权限设置过小则无权访问该页面。不行的话就
清空tmp里文件。直接重启就好了。

WLS Start Mode=Development  开发模式可以替换。

生产模式下不能自动部署，需要到Weblogic控制台或用Weblogic deployment工具。
