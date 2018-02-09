### [weblogic.application.ModuleException: Context path '' is already ](https://stackoverflow.com/questions/16033609/weblogic-application-moduleexception-context-path-is-already-in-use-by-the-m)

* stackoverflow解决方法
    * 1. Stop the weblogic server
      
    * 2. Remove all war files from the 'autodeploy' folder in weblogic 3.Then start the weblogic server again(
    在weblogic目录下找到autodeploy文件夹把下面部署的包全部删除,一般做了这一步之后,重新部署运行基本就可以了)
    
    * 3. After that type the URL "http:// localhost:port/console/" in browser
    
    * 4. Go to " Configure applications" link
       
    * 5. Then select previous projects and the go stop -> When work completes
