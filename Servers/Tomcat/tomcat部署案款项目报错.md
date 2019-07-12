现场部署修改的代码后，登陆后500 ，内部服务器错误，使用版本为tomcat 8 [参考](https://bbs.csdn.net/topics/392288641)

 ```js
 // 20190711 begin 密码校验 
		var testPassword =/^(?=.*?[a-z])(?=.*?[A-Z])(?=.*?\d)(?=.*?[!#@*&.])[a-zA-Z\d!#@*&.]{8,15}$/;
			if(testPassword.test(plainPassword) == false){
				$("#loginPwdCheckMeg").html("请尽快修改密码：8-20位大小写字母+数字+符号组成!");
		  		$("#checkLoginPwdDiv").show();
				document.cookie="isCheckedPassword=请尽快修改密码：8-20位大小写字母+数字+符号组成!";				
			};
	//20190711 end 密码校验 	
 
 问题原因：
 document.cookie里面的key-value中value为中文导致解析报 :
 java.lang.IllegalArgumentException: Invalid character found in the request target. The valid characters are defined
 解决方案：
 网上查询是版本问题，故将标志中文改成了 document.cookie="isCheckedPassword=isCheckedPassword";	问题解决
 ```
 
 
