[RenameTo() 使用问题:](http://www.iteye.com/topic/149328)
------------------

```java

          File oldName = new File("C:\\Test\\x.txt");
	        File newName = new File("C:\\t.txt");
	        //检查要重命名的文件是否存在，是否是文件  
	        if (!oldName.exists() || oldName.isDirectory()) {  
	  
	            System.out.println("File does not exist: " + oldName);  
	            return;  
	        }  
 
	  
	        if(oldName.renameTo(newName)) {
	            System.out.println("已重命名");
	        } else {
	            System.out.println("Error");
	        }
		    
	}
  
```


* 注意newName 所对应的路径必须是不存在的,不然就会一直输出Error的问题
  * 其他跨平台问题,点击本文标题查看详解
