### 餐饮数据可视化

####  一、语言环境安装

1.JDK的安装与配置
首先运行安装包，红色标记的是jdk的安装路径，默认即可，一直点击下一步。

![输入图片说明](images/image1.png)

安装完成之后会自己添加环境变量。

####  二、安装编译软件IDEA
在IDEA官网下载安装包
https://www.jetbrains.com/idea/download/?section=windows
选择我们的安装路径进行安装
注意：这个路径下必须是空文件夹

![输入图片说明](images/image2.png)

安装完成后打开IDEA

####  三、Maven的安装和配置
##### 1.Maven下载
https://maven.apache.org/download.cgi

![输入图片说明](images/image3.png)

##### 2.Maven安装
将maven安装包放在此电脑->文档下的文件夹里，解压

![输入图片说明](images/image4.png)

将下载的安装包解压成上图

![输入图片说明](images/image5.png)

##### 3.配置环境变量
1.在“计算机”图标上单击鼠标右键，选择“属性”，在弹出对话框中单击“高级”选项卡，在弹出对话框中单击“环境变量”按钮

![输入图片说明](images/image6.png)

2.点击新建系统变量，添加变量名MAVEN_HOME,点击浏览目录，找到你的MAVEN解压地址。

![输入图片说明](images/image7.png)

3.添加完成后显示以下内容

![输入图片说明](images/image8.png)

4.选中PATH，点击编辑

![输入图片说明](images/image9.png)

5.点击新建，浏览，找到MAVEN路径下的bin文件夹，点击确定，把所有弹框点击确定

![输入图片说明](images/image10.png)

6.配置本地仓库
第一步、在maven目录下新建repository文件夹

![输入图片说明](images/image11.png)

第二步、打开maven的配置文件 settings.xml
在maven目录下的conf文件夹里

![输入图片说明](images/image12.png)

![输入图片说明](images/image13.png)

在settings.xml文件中如图所示位置里面添加:
<localRepository>自己的repository目录</localRepository>

![输入图片说明](images/image14.png)



第四步、把远程仓库改成阿里的，不然用的是国外的，速度很慢，在本地仓库里的依赖不够多的时候，大部分时候还得靠远程仓库
将下面配置加到<mirrors></mirrors>中间，如下所示：

```
<mirror>        
  <id>nexus-aliyun</id>      
  <name>nexus-aliyun</name>    
  <url>http://maven.aliyun.com/nexus/content/groups/public</url>      
  <mirrorOf>central</mirrorOf>        
</mirror>    
```

![输入图片说明](images/image15.png)

7.在IDEA配置远程仓库路径

![输入图片说明](images/image16.png)

配置maven home path:

![输入图片说明](images/image17.png)

配置maven的settings文件路径：

![输入图片说明](images/image18.png)

配置仓库路径：

![输入图片说明](images/image19.png)

为了让我们每次新建项目时，指定maven路径，设置新项目设置

![输入图片说明](images/image20.png)

![输入图片说明](images/image21.png)

####  四、创建Web项目
#####  1.新建一个springboot Maven项目

![输入图片说明](images/image22.png)

##### 2.设置项目名称、语言、类型、JDK、java版本等，点击下一步。
项目名称设置为foodDemo

![输入图片说明](images/image23.png)

##### 3.设置SpringBoot版本，在搜索框搜索添加Spring Web、MyBatis Framework、MySQL Driver、Thymeleaf

![输入图片说明](images/image24.png)

添加web数据池依赖环境，在pom.xml文件里添加

![输入图片说明](images/image25.png)


```
<dependency>
   <groupId>com.alibaba</groupId>
   <artifactId>druid-spring-boot-starter</artifactId>
   <version>1.2.11</version>
</dependency>
<dependency>
   <groupId>com.alibaba</groupId>
   <artifactId>fastjson</artifactId>
   <version>1.2.79</version>
</dependency>
<dependency>
    <groupId>org.codehaus.janino</groupId>
    <artifactId>janino</artifactId>
    <version>3.0.8</version>
</dependency>
```




点击刷新按钮
右上角找到maven点击insatll安装

![输入图片说明](images/image26.png)

##### 4.Spring Web应用设置
（1）设置项目结构外观

![输入图片说明](images/image27.png)

（2）在项目文件夹下创建以下package


![输入图片说明](images/image28.png)


注意：Impl  第一个是大写的i ，第二个是小写的l （L）

（3）把application.properties改成application.yaml

![输入图片说明](images/image29.png)

在这个文件里面添加以下内容：
修改自己的mysql的数据库名称和用户名、密码
模型层的路径

```
server:
  port: 8888
  tomcat.uri-encoding: UTF-8
spring:
  thymeleaf:
    prefix: classpath:/templates/
    suffix: .html
    mode: HTML
    encoding: UTF-8
    servlet:
      content-type: text/html
    cache: false
  datasource:
    url: jdbc:mysql://127.0.0.1:3306/food?useUnicode=true&characterEncoding=utf8&zeroDateTimeBehavior=convertToNull&useSSL=true&serverTimezone=GMT%2B8
    driver-class-name: com.mysql.cj.jdbc.Driver
    username: root
    password: root
    type: com.alibaba.druid.pool.DruidDataSource
    druid:
      initial-size: 20
      max-active: 100
      min-idle: 10

mybatis:
  mapper-locations: classpath:mapper/*.xml
  type-aliases-package: com.example.foodDemo.entity
```



![输入图片说明](images/image30.png)




####  五、数据集导入
####  1.创建数据库（food），设置字符集utf8mb4

![输入图片说明](images/image31.png)

#####  2.导入数据
在gitee上下载数据库文件
https://gitee.com/little-love-you/visualization-of-catering-data.git
下载完成后导入mysql数据库中

##### 3.效果如下：

![输入图片说明](images/image32.png)

## 六、数据的分析


![输入图片说明](images/image33.png)

## 七、后端项目搭建
项目结构如下如所示：

![输入图片说明](images/image34.png)

##### 1.模型层
在entity文件夹下创建food (class)类

```
public class food {
    private String foodType;
    private String foodAddr;
    private Integer commentCount;
    private String taste;
    private String environment;
    private double service;
    private double cost;
    private String city;

    @Override
    public String toString() {
        return "food{" +
                "foodType='" + foodType + '\'' +
                ", foodAddr='" + foodAddr + '\'' +
                ", commentCount=" + commentCount +
                ", taste='" + taste + '\'' +
                ", environment='" + environment + '\'' +
                ", service=" + service +
                ", cost=" + cost +
                ", city='" + city + '\'' +
                '}';
    }

    public String getFoodType() {
        return foodType;
    }

    public void setFoodType(String foodType) {
        this.foodType = foodType;
    }

    public String getFoodAddr() {
        return foodAddr;
    }

    public void setFoodAddr(String foodAddr) {
        this.foodAddr = foodAddr;
    }

    public Integer getCommentCount() {
        return commentCount;
    }

    public void setCommentCount(Integer commentCount) {
        this.commentCount = commentCount;
    }

    public String getTaste() {
        return taste;
    }

    public void setTaste(String taste) {
        this.taste = taste;
    }

    public String getEnvironment() {
        return environment;
    }

    public void setEnvironment(String environment) {
        this.environment = environment;
    }

    public double getService() {
        return service;
    }

    public void setService(double service) {
        this.service = service;
    }

    public double getCost() {
        return cost;
    }

    public void setCost(double cost) {
        this.cost = cost;
    }

    public String getCity() {
        return city;
    }

    public void setCity(String city) {
        this.city = city;
    }
}
```


##### 2.数据持久层
在mapper文件夹下创建FoodMapper (interface)接口

```
import org.apache.ibatis.annotations.Mapper;

import java.util.List;
import java.util.Map;

@Mapper
public interface FoodMapper {
    //花费前十的平均口味评分、平均服务评分、平均环境评分
    List<Map<String,Double>> findCostTop10();

    //地区和平均消费关系
    List<Map<String,Double>> findAddrCost();

    //地区和服务评分的关系
    List<Map<String,Double>> findAddrService();

    //食物种类和点评人数的关系
    List<Map<String,Integer>> findTypeComment();

    //地区和环境的关系
    List<Map<String,Double>> findAddrEnvironment();
}
3.数据服务层
●在service文件夹下创建FoodService (interface) 接口
import java.util.List;
import java.util.Map;

public interface FoodService {
    //花费前十的平均口味评分、平均服务评分、平均环境评分
    List<Map<String,Double>> findCostTop10();

    //地区和平均消费关系
    List<Map<String, Double>> findAddrCost();

    //地区和服务评分的关系
    List<Map<String, Double>> findAddrService();

    //食物种类和点评人数的关系
    List<Map<String, Integer>> findTypeComment();

    //地区和环境的关系
    List<Map<String, Double>> findAddrEnvironment();
}

```


●在Impl文件夹下创建FoodServiceImpl（class）

```
import com.example.foodDemo.mapper.FoodMapper;
import com.example.foodDemo.service.FoodService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import java.util.List;
import java.util.Map;

@Service
public class FoodServiceImpl implements FoodService {

    private final FoodMapper foodMapper;

    @Autowired
    public FoodServiceImpl(FoodMapper foodMapper) {
        this.foodMapper = foodMapper;
    }

    @Override
    public List<Map<String, Double>> findCostTop10() {
        return foodMapper.findCostTop10();
    }

    @Override
    public List<Map<String, Double>> findAddrCost() {
        return foodMapper.findAddrCost();
    }

    @Override
    public List<Map<String, Double>> findAddrService() {
        return foodMapper.findAddrService();
    }

    @Override
    public List<Map<String, Integer>> findTypeComment() {
        return foodMapper.findTypeComment();
    }

    @Override
    public List<Map<String, Double>> findAddrEnvironment() {
        return foodMapper.findAddrEnvironment();
    }
}
```



##### 4.控制层
在controller文件夹下创建FoodController（class）类

```
import com.alibaba.fastjson.JSON;
import com.example.foodDemo.service.FoodService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;
import java.util.List;
import java.util.Map;

@Controller
public class FoodController {
    private final FoodService foodService;
    @Autowired
    public FoodController(FoodService foodService) {
        this.foodService = foodService;
    }

    //花费前十的平均口味评分、平均服务评分、平均环境评分
    @RequestMapping("/getCostTop10")
    @ResponseBody
    public String getCostTop10(){
        List<Map<String,Double>> costTopList = foodService.findCostTop10();
        String str = JSON.toJSONString(costTopList);
        System.out.println(str);
        return str;
    }

    //地区和平均消费关系
    @RequestMapping("/getAddrCost")
    @ResponseBody
    public String getAddrCost(){
        List<Map<String, Double>> addrCostMap = foodService.findAddrCost();
        String str = JSON.toJSONString(addrCostMap);
        System.out.println(str);
        return str;
    }

    //地区和服务评分的关系
    @RequestMapping("/getAddrService")
    @ResponseBody
    public String getAddrService(){
        List<Map<String, Double>> addrServiceMap = foodService.findAddrService();
        String str = JSON.toJSONString(addrServiceMap);
        System.out.println(str);
        return str;
    }

    @RequestMapping("/getTypeComment")
    @ResponseBody
    public String getTypeComment(){
        List<Map<String, Integer>> typeComment = foodService.findTypeComment();
        String str = JSON.toJSONString(typeComment);
        System.out.println(str);
        return str;
    }

    @RequestMapping("/getAddrEnvironment")
    @ResponseBody
    public String getAddrEnvironment(){
        List<Map<String, Double>> addrEnvironment = foodService.findAddrEnvironment();
        String str = JSON.toJSONString(addrEnvironment);
        System.out.println(str);
        return str;
    }
}
```



##### 5.mybatis配置
在resources文件夹下的mapper下创建文件，名为FoodMapper.xml

![输入图片说明](images/image36.png)

![输入图片说明](images/image37.png)

内容如下：
注意：红色字体是自己的FoodMapper所在的位置

![输入图片说明](images/image38.png)


```
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd" >
<mapper namespace="com.example.foodDemo.mapper.FoodMapper">
    <select id="findCostTop10" resultType="java.util.Map">
        select foodType,ROUND(AVG(cost),2) as avgCost,ROUND(AVG(taste),2) as avgTaste,ROUND(AVG(service),2) as avgService,ROUND(AVG(environment),2) as avgEnvironment from catering_data where foodType is not null GROUP BY foodType ORDER BY avgCost desc limit 10
    </select>
    <select id="findAddrCost" resultType="java.util.Map">
        select foodAddr,ROUND(AVG(cost),1) as avgCost from catering_data where foodAddr is not null GROUP BY foodAddr HAVING avgCost > 0 ORDER BY avgCost desc
    </select>
    <select id="findAddrService" resultType="java.util.Map" >
        select foodAddr,ROUND(AVG(service),2) as avgService from catering_data where foodAddr is not null GROUP BY foodAddr ORDER BY avgService desc
    </select>
    <select id="findTypeComment" resultType="java.util.Map">
        select foodType,ROUND(AVG(commentCount)) as avgComment from catering_data where foodType is not null GROUP BY foodType ORDER BY avgComment desc
    </select>
    <select id="findAddrEnvironment" resultType="java.util.Map">
        select foodAddr,AVG(environment) as avgEnvironment from catering_data where foodAddr is not null GROUP BY foodAddr ORDER BY avgEnvironment desc limit 10
    </select>
</mapper>

```

## 八、前端项目创建
●在templates文件夹下新建html文件

```
<!DOCTYPE html>

<html lang="">
<head>
   <meta charset="utf-8" />
   <meta name="viewport" content="width=device-width,initial-scale=1,minimum-scale=1,maximum-scale=1,user-scalable=no" />
   <title>餐饮数据可视化分析</title>
   <link rel="stylesheet" type="text/css" href="/css/app.css" />
   <script src="/js/jquery-3.6.3.min.js"></script>
   <script src="/js/echarts.min.js"></script>
   <script type="text/javascript" src="/js/shanghai.js"></script>
   <script src="/js/echarts-wordcloud.js"></script>
   <script src="/js/food.js"></script>
</head>

<body>
<header id="header">
   <h3 class="header-title">上海餐饮数据可视化分析</h3>
</header>

<div id="container">
   <div id="flexCon">
      <div class="flex-row">
         <div class="flex-cell flex-cell-l">
            <div class="chart-wrapper">
               <h3 class="chart-title">各行政区平均餐饮消费分析</h3>
               <div class="chart-div" id="e1">

               </div>
            </div>
         </div>
         <div class="flex-cell flex-cell-c">
            <div class="chart-wrapper">
               <h3 class="chart-title">地区服务评分图</h3>
               <div class="chart-div" id="e2">

               </div>
            </div>
         </div>
         <div class="flex-cell flex-cell-r">
            <div class="chart-wrapper">
               <h3 class="chart-title">菜系点评数词云图</h3>
               <div class="chart-div chart-done" id="e3">

               </div>
            </div>
         </div>
      </div>
      <div class="flex-row">
         <div class="flex-cell flex-cell-lc">
            <div class="chart-wrapper">
               <h3 class="chart-title">排名前十的菜系评分</h3>
               <div class="chart-div chart-done" id="e4">

               </div>
            </div>
         </div>
         <div class="flex-cell flex-cell-r">
            <div class="chart-wrapper">
               <h3 class="chart-title">地区环境评分图</h3>
               <div class="chart-div chart-done" id="e5">

               </div>
            </div>
         </div>
      </div>
   </div>
</div>
</body>
</html>
```


●在static文件夹下的css、js、img文件夹中放入配置文件
从我的gitee中下载相关文件即可
https://gitee.com/little-love-you/visualization-of-catering-data.git

![输入图片说明](images/image39.png)

## 九、启动项目

![输入图片说明](images/image40.png)

![输入图片说明](images/image41.png)










