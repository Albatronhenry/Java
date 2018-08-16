[weblogic打包启动out of memory](https://blog.csdn.net/qq_18756241/article/details/54409827)
修改对应的文件参数即可(其中标记的为需要修改的参数项):
优化过程：


1、 修改weblogic的D:\Oracle\Middleware\user_projects\domains\***_domain\bin\setDomainEnv.cmd文件中关于内存的参数配置

修改前：

if "%JAVA_VENDOR%"=="Sun" (

set WLS_MEM_ARGS_64BIT=-Xms256m -Xmx512m

set WLS_MEM_ARGS_32BIT=-Xms256m -Xmx512m

) else (

set WLS_MEM_ARGS_64BIT=-Xms512m -Xmx512m

set WLS_MEM_ARGS_32BIT=-Xms512m -Xmx512m

)

…..

 

set MEM_PERM_SIZE_32BIT=-XX:PermSize=48m

……

 

set MEM_MAX_PERM_SIZE_32BIT=-XX:MaxPermSize=128m

修改后：

if "%JAVA_VENDOR%"=="Sun" (

set WLS_MEM_ARGS_64BIT=-Xms256m -Xmx512m

set WLS_MEM_ARGS_32BIT=-Xms`512`m –Xmx`1024`m

) else (

set WLS_MEM_ARGS_64BIT=-Xms512m -Xmx512m

set WLS_MEM_ARGS_32BIT=-Xms512m -Xmx`1024`m

)

…..

 

set MEM_PERM_SIZE_32BIT=-XX:PermSize=`256`m

……

 

set MEM_MAX_PERM_SIZE_32BIT=-XX:MaxPermSize=`256`m
