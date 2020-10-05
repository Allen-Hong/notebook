# **springboot**



1. 优点：

   - 简化spring应用的初始搭建和开发过程，使用特定的方式（properties或yml）的方式进行配置
   - 创建独立的spring应用程式 main方法运行
   - 嵌入式的Tomcat 不需要部署 war文件
   - 简化maven配置
   - 自动配置spring添加对应功能starter自动化配置

2. 特点：

   - 约定大约配置
   - 热部署(devtools)有效减少开发工作

3. 自动配置原理：

   - @EnableAutoConfigration 自动去maven中读取每个starter中的spring.factories文件，该文件配置了所有需要spring容器创建的bean

     