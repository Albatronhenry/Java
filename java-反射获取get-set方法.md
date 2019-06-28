因项目实现需要，需要针对传入字段属性，进行getter/setter方法取值赋值，这里考虑通过反射实现，相应代码如下，以此备忘

```java
 //遍历coa必录且需底级要素
      for (int j = 0; j < checkEleList.size(); j++) {
    	   XMLData xmlData =  (XMLData) checkEleList.get(j);
    	   String eleStr = (String) xmlData.get("ele_code"); 
    	   //通过反射实现
				try {
					//先拼接对应get方法
			    	String getMethodString ="get"+eleStr.substring(0,1).toUpperCase()+eleStr.substring(1);
			    	//get属性值
			    	Object getObject;
					Method getMethod = psd.getClass().getMethod(getMethodString);
					getObject = getMethod.invoke(psd);
					   //针对get方法取值不为空的字段属性进行赋值处理
					if(StringUtils.isNotEmpty(getObject.toString())){
						//拼接对应set方法
						 String setMethodString ="set"+eleStr.substring(0,1).toUpperCase()+eleStr.substring(1);
						 Method setMethod = psd.getClass().getMethod(setMethodString, String.class);
						 setMethod.invoke(psd, getObject);
					}
				} catch (SecurityException e) {
					throw new RuntimeException("导入数据根据要素" + eleStr + "赋值失败！", e);
				} catch (NoSuchMethodException e) {
					throw new RuntimeException("导入数据根据要素" + eleStr + "赋值失败！", e);
				}catch (IllegalArgumentException e) {
					throw new RuntimeException("导入数据根据要素" + eleStr + "赋值失败！", e);
				} catch (IllegalAccessException e){
					throw new RuntimeException("导入数据根据要素" + eleStr + "赋值失败！", e);
				} catch (InvocationTargetException e) {
					throw new RuntimeException("导入数据根据要素" + eleStr + "赋值失败！", e);
				} 	 
      }




```
