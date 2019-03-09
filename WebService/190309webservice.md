[webservice 学习]()
--------
1.IDEA 快速搭建ws server&client [参考](https://blog.csdn.net/qq_21399933/article/details/78797071)

*  1.1 创建ws服务端（jdk1.8） new -- file -- project -- webservice (注意勾选 Generate sample server code       
*  1.2 生成项目后，启动相应类，打开浏览器查看即可
```java
public class HelloWorld {
  @WebMethod
  public String sayHelloWorldFrom(String from) {
    String result = "Hello, world, from " + from;
    System.out.println(result);
    return result;
  }
  public static void main(String[] argv) {
    Object implementor = new HelloWorld ();
    String address = "http://localhost:9000/HelloWorld";
    Endpoint.publish(address, implementor);
  }
}
```

*  1.3 创建ws客户端（jdk1.6）新版idea与1.8会存在bug,编写相应测试类、方法，运行即可
```java
public class HelloWorldClient {
  public static void main(String[] argv) {
    /**
     * 步骤：1 调用其中接口HelloWorld 实例化对应类HelloWorldService 并获取相应端口 getHelloWorldPort
     *       2 其次调用相应实例对应的方法即可实现
     */
    mypackage.HelloWorld service = new HelloWorldService().getHelloWorldPort();
    //invoke business method
    System.err.print(service.sayHelloWorldFrom("henry"));

  }
}

```
控制台输出，测试通过：
```console
Hello, world, from henry
```

2.IDEA实现调用天气查询ws [参考](https://blog.csdn.net/qq_43147940/article/details/84713480)
*  2.1 先创建对应client项目，然后执行下面步骤
*      直接调用weather ws，会有点问题，需要将http://www.webxml.com.cn/WebServices/WeatherWebService.asmx?wsdl保存到本地
*      将 <s:element ref=“s:schema”/>下的<s:any/>改成 <s:any minOccurs=“2” maxOccurs=“2”/>
*      将修改后保存的WeatherWS.wsdl文件放到client项目src对应包（本次包名是mypackage）目录下
*      在client项目上右键，webservice=>Generate JavaCode from wsdl，即可生成对应调用代码
*      WS接口网址：http://www.webxml.com.cn/zh_cn/index.aspx
*  2.2 创建example包，创建调用类WeatherClient，编写相应调用代码即可
```java
public class WeatherClient {
    public static void main(String[] args) throws  RemoteException, ParserConfigurationException {
        //实例初始化
        WeatherWS ww = new WeatherWS();
        //获取接口
        WeatherWSSoap wws = ww.getPort(WeatherWSSoap.class);
        //获取国家信息 ArrayOfString 想当于 list<String>
        ArrayOfString reg = wws.getRegionCountry();
        List<String> region = reg.getString();
        for (String r : region
                ) {
            System.out.println(r.toString());
        }
        //获取省份信息
        ArrayOfString ct = wws.getRegionProvince();
        List<String> city = ct.getString();
        for (String c: city
             ) {
            System.err.print(c);
        }
        //获取天气信息
        ArrayOfString weather = wws.getWeather("2117","");
        List<String> weath = weather.getString();
        for (String a : weath) {
            System.out.println(a.toString());
        }

    }
}
```
控制台输出：
```console
...
英国,3247
约旦,3173
越南,3156
智利,3523

黑龙江,3113吉林,3114辽宁,3115内蒙古,3116河北,3117河南,3118山东,3119山西,31110江苏,31111安徽,31112陕西,31113宁夏,31114甘肃,31115青海,31116湖北,31117湖南,31118浙江,31119江西,31120福建,31121贵州,31122四川,31123广东,31124广西,31125云南,31126海南,31127新疆,31128西藏,31129台湾,31130北京,311101上海,311102天津,311103重庆,311104香港,311201澳门,311202钓鱼岛,311203江西 南昌

南昌
2117
2019/03/09 15:05:00
今日天气实况：气温：11℃；风向/风力：东风 2级；湿度：84%
紫外线强度：最弱。空气质量：良。
紫外线指数：最弱，辐射弱，涂擦SPF8-12防晒护肤品。
健臻·血糖指数：不易波动，天气条件不易引起血糖波动。
穿衣指数：较冷，建议着厚外套加毛衣等服装。
洗车指数：不宜，有雨，雨水和泥水会弄脏爱车。
空气污染指数：良，气象条件有利于空气污染物扩散。

3月9日 小雨转阴
7℃/11℃
北风小于3级
7.gif
...
```


