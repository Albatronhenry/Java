### [debug模式启动不起来](https://blog.csdn.net/YYQQ323/article/details/79807004)

用的是myeclipse，weblogic调bug的时候，启动debug模式，卡在了一个地方，怎么也不往下走了，重启eclipse也没用，后来`清除掉所有断点`之后就好了

同时注意  myeclipse -->project -->`build Automatically` 选中,不然修改了,没有更新,weblogic 会一直缓存不更新,导致相应更新的代码出不来效果

如果清除了所有断点还是走不下去,那么清除weblogic目录下domains目录下servers--cache/tmp两个文件夹,再选择重启myeclipse.重启myeclipse,如果还是不行,就只能重启电脑

