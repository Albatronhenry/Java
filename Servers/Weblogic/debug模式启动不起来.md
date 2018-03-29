### debug模式启动不起来

用的是myeclipse，weblogic调bug的时候，启动debug模式，卡在了一个地方，怎么也不往下走了，重启eclipse也没用，后来清除掉自己打的断点之后就好了

同时注意  myeclipse -->project -->build Automatically 选中,不然修改了,没有更新,weblogic 会一直缓存不更新,导致相应更新的代码出不来效果
