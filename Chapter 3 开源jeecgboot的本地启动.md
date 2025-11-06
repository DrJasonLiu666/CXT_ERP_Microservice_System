# 1 jeecgboot官网以及开发手册

jeecgboot官网：[JEECG官方网站 - 基于BPM的低代码开发平台](http://www.jeecg.com/)

jeecgboot开发文档：[Maven私服设置 · JeecgBoot 开发文档 · 看云](http://doc.jeecg.com/2043876)

ant-design-vue官网：[Ant Design of Vue - Ant Design Vue (antdv.com)](https://1x.antdv.com/docs/vue/introduce-cn/)

ant-design-vue开发文档：[简介 | Vue.js (vuejs.org)](https://cn.vuejs.org/guide/introduction.html)

语言学习：[菜鸟教程 - 学的不仅是技术，更是梦想！ (runoob.com)](https://www.runoob.com/)



之前从jeecgboot官网Git下来了前后端，应该参照ERP项目进行了部分改动。详见GitLab如下：

JeecgBootFrontVue2：https://gitlab.com/JackChen-Strong/jeecgbootfrontvue2

JeecgBootBack：https://gitlab.com/JackChen-Strong/jeecgbootback

# 2 前端Vue2启动

前端使用vue2

下载地址：[GitHub - jeecgboot/ant-design-vue-jeecg: ⭐️「企业级低代码平台」Vue2版UI，基于 Vue2+AntDesignVue 实现的 Ant Design Pro，提供强大代码生成器的低代码平台。 前端页面代码和后端功能代码一键生成，不需要写任何代码，保持jeecg一贯的强大！！](https://github.com/jeecgboot/ant-design-vue-jeecg)

IDE：vscode。本人主观上没有修改VSCODE配置，采用默认配置。ide配置可详见官网：[通过IDEA启动项目 · JeecgBoot 开发文档 · 看云](http://doc.jeecg.com/2043874)

前端启动：五步。如下：

①git clone先下载再导入文件 或者 git vcs在线导入文件

②修改五个配置文件（尤其是sso）

③npm install     

④npm install yarm -g

⑤npm run serve

# 3 后端jeecgboot启动

## 3.1 启动过程

后端使用JeecgBoot架构

 下载地址：[GitHub - jeecgboot/jeecg-boot: ⭐️「企业级低代码平台」前后端分离架构SpringBoot 2.x，SpringCloud，Ant Design&Vue，Mybatis，Shiro，JWT。强大的代码生成器让前后端代码一键生成，无需写任何代码! 引领新的开发模式OnlineCoding->代码生成->手工MERGE，帮助Java项目解决70%重复工作，让开发更关注业务，既能快速提高效率，帮助公司节省成本，同时又不失灵活性。](https://github.com/jeecgboot/jeecg-boot)
 
 后端启动步骤详见：[IDEA导入项目 · JeecgBoot 开发文档 · 看云](http://doc.jeecg.com/2043873#__26)

IDE：idea或者eclipse（eclipse需安装lombok）【本人是用idea启动，主观上没有修改idea配置，采用默认配置。ide配置可详见官网：[通过IDEA启动项目 · JeecgBoot 开发文档 · 看云](http://doc.jeecg.com/2043874)】

 ①后端启动时发生数据库配置错误问题，需要安装sql。sql安装完成后，修改项目配置 (即数据库)，其中：数据库配置(连接和账号密码)。
 
 ②再次启动后端，报错：execute error. SELECT * FROM QRTZ_LOCKS WHERE SCHED_NAME = 'MyScheduler' AND LOCK_NAME = ? FOR UPDATE
 java.sql.SQLSyntaxErrorException: Table 'jeecgboot.qrtz_locks' doesn't exist。原因：我在cmd中创建数据库的时候，数据库命名为jeecgboot（localhost连接也被命名为jeecgboot连接，后续可在DBeaver中重新命名为localhost连接），所以会有两级名称一样的jeecgboot库，然后执行sql文件在localhost连接中生成jeecg-boot数据库，造成localhost连接下面有jeecgboot和jeecg-boot两个库。系统找到jeecgboot库里面去了，实际里面是空的。删除jeecgboot库，只留下jeecg-boot库，同时修改application文件中的dataSource配置。
 
 ③再次启动后端时，报错：ERROR o.s.d.redis.listener.RedisMessageListenerContainer:665 - Connection failure occurred. Restarting subscription task after 5000 ms。原因：本地没有安装redis，同时后端redis配置也没有更新。redis安装完成后，修改项目配置 (即Redis)，其中：Redis配置（配置redis的host(为localhost）和port（为6379，即原始默认端口））。
 
 ④再次启动后端时成功执行。

⑤注意：关闭命令行窗口后，redis关闭，因此每次启动jeecgboot时都需要先在命令行中输入 redis-server 从而启动redis，另外需要注意每次启动jeecgboot时mysql有没有启动。
 
 ⑥在浏览器中登录网页，报错：“启动失败: 检查到当前菜单表是Vue3版本，导致菜单加载异常，请切换到Vue2版菜单！参考：[切换Vue2路由菜单表 · JeecgBoot 开发文档 · 看云](http://doc.jeecg.com/3075165)”。按照参考链接进行操作即可。（本人是在DBeaver中直接手动更换两个表的名称，没有写sql）

⑦成功运行jeecgboot。
 
 【jeecgboot缺点：我的jeecgboot没有流程引擎，有的同学说他们的有，可能是版本不同，但可以借助activiti进行集成开发从而实现流程功能；其次，jeecgboot的代码生成器貌似侧重于报表之类（比如大屏报表），无法提供类似于蓝凌的低代码平台】

## 3.2 sql数据库安装

### 3.2.1 安装MYSQL5.7.20版本

①安装教程（My SQL Installer 5.7.20 的 X86，32-bit版本：有可执行文件）：
 [超详细MySQL安装及基本使用教程_mysql安装教程_千羽千寻的博客-CSDN博客](https://blog.csdn.net/bobo553443/article/details/81383194)

 ②使用MySQL Workbench执行sql文件创建数据库的教程：
 [怎么使用MySQL workbench将.sql文件导入数据库_workbeach 导入.sql_鸡汤本汤的博客-CSDN博客](https://blog.csdn.net/YangTinTin/article/details/102856963)
 
 ③使用MySQL Workbench新建数据库的教程：
 [MySQL Workbench使用教程](http://c.biancheng.net/view/2625.html)
 
 ④数据库连接工具：DBeaver

DBeaver使用教程：[图文并茂教你使用dbeaver连接oracle数据库，以及建表_Silver gradient的博客-CSDN博客](https://blog.csdn.net/z19950712/article/details/117689017)

### 3.2.2 安装MYSQL8.0.32版本

①安装教程（mysql-8.0.32-winx64没有可执行文件）：
 [mysql 8.0.32安装 windows server 超详细_杨熤的博客-CSDN博客](https://blog.csdn.net/weixin_44641729/article/details/129170352)
 [windows 安装 mysql-8.0.32 压缩包方式 - klvchen - 博客园](https://www.cnblogs.com/klvchen/p/17140142.html)
    
     S1：下载并解压；
     
     S2：Mysql安装目录下的bin文件中创建my.ini和data文件（my.ini配置文件中的 basedir和datadir修改成自己的安装地址）；
     
     S3：设置环境变量MYSQL_HOME，并编辑PATH变量；
     
     S4：在cmd中操作（启动mysql并修改密码和权限）【在cmd中操作MYSQL时注意执行语句是否以 英文分号 ; 结尾】
     
            注意：在桌面中启动cmd并进入mysql的bin目录下。
                       
                       后续在cmd的mysql_bin目录下执行命令的顺序为：
                                    mysqld --install    #安装MYSQL
                                    
                                    mysqld --initialize --console;  # 获取root的初始密码
                                    
                                    net start mysql    # 启动MYSQL
                                    
                                    mysql -u root -p    # 用root账号登录，会提示你输入密码
                                    
                                    \# 修改密码，其中 klvchen 为密码
                                    
                                    ALTER USER 'root'@'localhost' IDENTIFIED BY 'klvchen';
                                    
                                    use mysql;
                                    
                                    update user set host = '%' where user = 'root';
                                    
                                    flush privileges;
                                    
                                    ALTER USER 'root'@'%' PASSWORD EXPIRE NEVER;
                                    
                                    flush privileges;
                                    
     S5：最后，在cmd中测试连接数据库。

②在cmd中执行sql文件创建数据库的教程（在cmd中操作MYSQL时注意执行语句是否以 英文分号 ; 结尾）：
 [mysql数据库用source命令导入.sql文件，执行SQL语句_mysql source 带sql参数_dmfrm的博客-CSDN博客](https://blog.csdn.net/u010889616/article/details/48226719)
 
 该链接中方法二：[MySQL cmd命令行 执行sql脚本文件_cmd执行mysql脚本_替这位空想家惊讶的博客-CSDN博客](https://blog.csdn.net/weixin_43708069/article/details/108724495)

\# 首先在cmd中进入mysql安装目录下的bin文件（本机为： D:\0projects\SQL\mysql-8.0.32-winx64\bin）

 d:cd D:\0projects\SQL\mysql-8.0.32-winx64\bin
 
 \# 启动mysql
 
 net start mysql
 
 \# 登录Mysql
 
 mysql -u root -p
 
 \# 创建数据库jeecgboot
 
 CREATE DATABASE jeecgboot;
 
 \# 进入相应数据库
 
 use jeecgboot;
 
 \# 用source命令执行脚本文件（本人移动了jeecgboot文件中jeecgboot-mysql-5.7.sql的位置）
 
 source D:\0projects\SQL\jeecgbootDB\jeecgboot-mysql-5.7.sql;

### 3.2.3 在cmd中修改root密码（针对mysql-8.0.32-winx64版本）

【mysql-8.0.32-winx64版本的语法规则可参照下面链接中安装mysql8.0.32winx64时的语法：[mysql 8.0.32安装 windows server 超详细_杨熤的博客-CSDN博客](https://blog.csdn.net/weixin_44641729/article/details/129170352)】
 
 \# 首先cmd中进入mysql安装目录下的bin文件（本机为： D:\0projects\SQL\mysql-8.0.32-winx64\bin）
 
 d:cd D:\0projects\SQL\mysql-8.0.32-winx64\bin
 
 \# 启动mysql
 
 net start mysql
 
 \# 登录Mysql
 
 mysql -u root -p
 
 \# 修改root密码
 
 update user set authentication_string = 'root' where user = 'root' ;
 
 【不知道密码是哪一列时，可参考如下方式慢慢查表】
 
 \# 进入mysql
 
 use mysql;
 
 \# 获取关于user信息的所有列，从中找到保存密码的列
 
 select * from user;

## 3.3 redis安装

### 3.3.1 安装教程

使用cmd安装：[Windows下安装Redis图文教程_redis windows_喵代王-香菜的博客-CSDN博客](https://blog.csdn.net/chen15369337607/article/details/119334531)

图形化方式安装：[最新版Redis安装配置教程（Windows+Linux）_redis安装教程_Baret-H的博客-CSDN博客](https://blog.csdn.net/qq_45173404/article/details/107715530)
 
下载地址：[Releases · tporadowski/redis · GitHub](https://github.com/tporadowski/redis/releases)

### 3.3.2 redis是什么

Redis是现在最受欢迎的NoSQL（非关系型）数据库之一，是一种key-value存储系统。详见：[Redis是什么？看这一篇就够了 - 葡萄城技术团队 - 博客园](https://www.cnblogs.com/powertoolsteam/p/redis.html)

【sql是关系型，redis与sql互补】

# 4 jeecgboot工程启动SOP

## 4.1 先检查数据库是否在线

### 4.1.1 问题描述

我的电脑重启后，发生mysql-8.0.32-winx64版本登陆不上的情况，且my.ini中免密登录设置也无效。试了很多方法但都没有解决问题，只能卸载并重装mysql。

### 4.1.2 卸载并重装mysql-8.0.32-winx64版本

1） mysql-8.0.32-winx64卸载步骤（七步）：

     S1：在  Windows管理工具——服务  中将Mysql状态设置为禁用；
     
     S2：控制面板 - 程序 - 程序和功能，将mysql server等相关内容卸载掉，将所有的MySQL的应用全部卸载掉；
     
     S3：删除MySQL安装目录下的MySQL文件夹。  C:\Program Files\MySQL，将这个文件夹也要删除。
     
     S4：打开注册表编辑器，删除注册表。利用快捷键win+R，输入“regedit”，回车，打开注册表编辑器。
     
           ①删除HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Services\Eventlog\Application\MySQL 文件夹
           
           ②删除 HKEY_LOCAL_MACHINE\SYSTEM\ControlSet002\Services\Eventlog\Application\MySQL 文件夹
           
           ③删除 HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Eventlog\Application\MySQL文件夹
           
     S5：删除C:\ProgramData\MySQL目录。ProgramData这个文件是默认隐藏的，可以在我的电脑- 查看中设置显示隐藏的项目，将这个目录下面的mysql文件删除。
     
     S6：打开服务发现MySql服务仍然残留在系统服务里（即状态为禁用的MySQL）。
     
     S7：删除残留服务（也可更改服务名，不影响重新安装对应服务，但明显不合理）：打开CMD执行sc delete MySQL  # 这里的MySQL是你要删除的服务名。

2）重装mysql-8.0.32-winx64时注意：
    
    ①Windows管理工具——服务中没有MySQL实例；
    
    ②需将原MYSQL安装目录删除后改名（本人是从sql改为MysqlReinstall）；
    
    ③因此系统变量MYSQL_HOME也需要重新指定值；
    
    ④my.init也需要重新配置basedir和datadir的参数；
    
    ⑤同时要保证执行 【mysqld --initialize --console】前， \bin\data是空目录）

### 4.1.3 mysql-8.0.32-winx64卸载教程

[MySql8.0以上版本彻底卸载_mysql8.0卸载_小马哥的博哥的博客-CSDN博客](https://blog.csdn.net/weixin_44933309/article/details/106425371)

## 4.2 再启动redis：【在cmd中输入： redis-server； 】

如何redis启动出现问题，可参照安装redis时的教程解决。

## 4.3 然后检查并更新前后端代码配置，并启动前后端代码；

1 问题：内网中，其他设备输入内网前端登录地址，可以进入登录界面但显示没有连上后端；使用公网地址登录时，一直是加载界面。（已有解决方案详见  微信—文件传输助手）

2 公网地址：https://706d3q4079.yicp.fun

## 4.4 登录系统；
