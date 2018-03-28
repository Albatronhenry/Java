[<BEA-141281> <unable to get file lock, will retry ...>](https://www.cnblogs.com/davidwang456/p/3730330.html)
---------------

概述
由于先前服务器直接down掉了，所有进程都非正常的进行关闭了，也就导致了下次启动weblogic的时候报了以下错误：

<2012-3-2 下午05时08分34秒 CST> <Info> <Management> <BEA-141281> <unable to get file lock, will retry …> 
<2012-3-2 下午05时08分44秒 CST> <Info> <Management> <BEA-141281> <unable to get file lock, will retry …>

解决办法
一.删掉Domain下的*.lok文件

1. 删除edit.lok

进入到domain_home下：

cd /u01/Oracle/Middleware/user_projects/domains/idm_domain

将edit.lok文件删掉

rm edit.lok

2.删除config.lok

进入到domain_home/config下：

cd /u01/Oracle/Middleware/user_projects/domains/idm_domain/config/

将config.lok文件删掉

rm config.lok

3.删除AdminServer.lok

cd /u01/Oracle/Middleware/user_projects/domains/idm_domain/servers/AdminServer/tmp

rm AdminServer.lok

4.删除EmbeddedLDAP.lok

/u01/Oracle/Middleware/user_projects/domains/idm_domain/servers/AdminServer/data/ldap/ldapfiles

rm EmbeddedLDAP.lok

二.删掉Domain下的*.DAT文件：

进入到domain_home当中

cd /u01/Oracle/Middleware/user_projects/domains/idm_domain

找到文件被删掉

[oracle@idm idm_domain]$ find servers/ -name "*.DAT" 
servers/AdminServer/data/store/diagnostics/WLS_DIAGNOSTICS000000.DAT 
servers/AdminServer/data/store/default/_WLS_ADMINSERVER000000.DAT

重新启动weblogic，搞定！
