工程：ActivitiDemo


注：本章资源已上传至github，详见(https://github.com/DrJasonLiu666/CXT_ERP_Microservice_System/releases/download/cxt_erp/PrivateActiviti.zip)

Activiti官网地址：https://www.activiti.org/

Activiti下载地址：https://github.com/Activiti

学习视频：https://www.bilibili.com/video/BV1Ya411z7kW?p=4


Activiti启动步骤：

S1：安装IDEA2019.1.4版本，以及actiBPM插件。

 原版本是ideaIC-2022.2.3，但IDEA2019.1.4之后的版本不再支持actiBPM插件，因此重新安装版本ideaIC-2019.1.4。
 
 至此，我的电脑装了两个IDEA版本（先装高版本，再装低版本）
 
 启动IDEA2019.1.4时提示"import IntelliJ IDEA Settings from"，我没有选引入，是直接打开。
 
 在JetBrains官网下载actiBPM插件，并从本地引入IDEA2019.1.4中（因为IDEA Market里面的actiBPM存在版本过低的情况）：https://plugins.jetbrains.com/plugin/7429-actibpm/versions
 

S2：创建activiti数据库，并执行java（BasicDemo中的TestCreateTable）生成表，注意数据库连接的配置。
   
   ①引入ActivitiDemo工程；
   
   
   ②配置JDK1.8。
   
   安装教程：https://blog.csdn.net/u014454538/article/details/88085316；
   
   下载地址：https://www.oracle.com/java/technologies/downloads/#java8

   
   ③然后如视频中，执行BasicDemo中的TestCreateTable创建数据库
   
   报错一：log4j:ERROR setFile(null,true) call failed.  java.io.FileNotFoundException: E:actactiviti.log (系统找不到指定的路径。)
   
   方案：在BasicDemo的log4j.properties中修改  【log4j.appender.LOGFILE.File=E:\act\activiti.log】 为  【log4j.appender.LOGFILE.File=D:\0projects\PrivateActiviti\activiti.log】
   
   D:\0projects\PrivateActiviti\activiti.log为本人所创建的日志文件夹（activiti.log）路径
   
   报错二：org.apache.commons.dbcp.SQLNestedException: Cannot create PoolableConnectionFactory (Unknown database 'activiti')
   
   方案：在DBeaver中的localhost连接中创建 activiti数据库，同时修改配置文件中dataSource配置，使其指向localhost连接中的activiti。

   
   ④解决上述问题后，再次执行，在localhost连接中的activiti数据库下生成25张表。


S3：创建流程（如leave流程，leave.bpmn），并实现从BPMN到pgn图片的转换
  
  ①leave.bpmn文件中的乱码处理（详见视频）
  
  ②BPMN文件本质是XML，同时ActivitiDemo支持将BPMN文件生成图片（详见视频）


S4：部署流程（如leave流程）
 
 ①执行BasicDemo中ActivitiDemo函数的testDeployment方法后，将bpm和PNG添加到数据库中。此时testDeployment只能一次部署一种流程，即不能同时部署多种流程，只能由一种流程在线。
 
 【出现五种报错】
 
 
 ②执行BasicDemo中ActivitiDemo函数的deployProcessByZip方法后，可同时将多种不同流程部署上线。（ZIP文件中包含每种流程的BPMN文件和PGN文件）
