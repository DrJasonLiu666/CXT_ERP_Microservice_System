 注：本章资源已上传至CSDN，详见https://github.com/DrJasonLiu666/CXT_ERP_Microservice_System/releases/download/package/ERPDBData.zip


第一部分：oracle安装教程

 https://blog.csdn.net/weixin_51487415/article/details/123728792
 
 【教程中解锁Scott用户时出现 //ORA-01918: 用户 'SCOTT' 不存在//问题 解决方法】
 
 https://blog.csdn.net/weivi001/article/details/45342483?locationNum=8

全局数据库名

 orcl
 
 用户名
 
 system/SYSDBA /SYSOPER 
 
 口令\密码
 
 admin

数据库管理后台地址

 https://localhost:5500/em/
 
 system
 
 admin

自带用户

 scott
 
 tiger


 第二部分：PL/SQL Developer安装教程
 
 教程：https://blog.csdn.net/qq_37705525/article/details/123663414
 
 下载官网地址：https://www.allroundautomations.com/registered-plsqldev/



第三部分：DBeaver连接Oracle
 
 教程：https://jingyan.baidu.com/article/aa6a2c14aeadf20d4c19c4e9.html
 
 /*
 
 错误：
 
 Can’t create driver instance
 
 Error creating driver ‘Oracle’ instance.
 
 Most likely required jar files are missing.
 
 You should configure jars in driver settings.

Reason: can’t load driver class ‘oracle.jdbc.OracleDriver’

 Error creating driver ‘Oracle’ instance.
 
 Most likely required jar files are missing.
 
 You should configure jars in driver settings.

Reason: can’t load driver class ‘oracle.jdbc.OracleDriver’

 oracle.jdbc.OracleDriver
 
 oracle.jdbc.OracleDriver

原因是缺少Oracle数据库驱动

解决教程

 https://www.cnblogs.com/wwssgg/p/16532326.html
 
 */



第四部分：DBeaver运行sql脚本创建

 教程：【解决Ubuntu下DBeaver执行sql脚本文件报错：No active connection】
 
 https://blog.csdn.net/qq_36476631/article/details/110536512

4.1 创建表空间（ERP_TBS）和创建用户（CXTERP）

 sqlPlus命令行输入语句：
 
 // 创建表空间
 
 SQL> create  tablespace  ERP_TBS  datafile  'D:\0projects\waigua\DB\ERP_TBS.DBF' size  3000m;
 
 // 创建用户
 
 //使用命令行时报错create user CXTERP identified by ekp1234 default tablespace ERP_TBS ;
 
 采用在数据库中新建模式
 
 //分配用户权限
 
 grant connect,resource,dba to CXTERP;
 
 教程
 
 https://blog.csdn.net/tianynnb/article/details/124360616
 
 https://jingyan.baidu.com/article/a378c960d3a611b3282830ed.html

DROP TABLESPACE CXTERP INCLUDING CONTENTS AND DATAFILES;

 DROP TABLESPACE CXTERP INCLUDING CONTENTS AND DATAFILES CASCADE CONSTRAINTS;

【执行后报  SQL 错误 [942] [42000]: ORA-00942: 表或视图不存在】

 【对应报错的sql语句
 
 CREATE UNIQUE INDEX "CXTERP"."SYS_C0026166" ON "CXTERP"."ACT_RU_IDENTITYLINK" ("ID_") 
 
  PCTFREE 10 INITRANS 2 MAXTRANS 255 COMPUTE STATISTICS 
  
  STORAGE(INITIAL 65536 NEXT 1048576 MINEXTENTS 1 MAXEXTENTS 2147483645
  
  PCTINCREASE 0 FREELISTS 1 FREELIST GROUPS 1
  
  BUFFER_POOL DEFAULT FLASH_CACHE DEFAULT CELL_FLASH_CACHE DEFAULT)
  
  TABLESPACE "ERP_TBS" ;
  
  CREATE INDEX "CXTERP"."ACT_IDX_IDENT_LNK_USER" ON "CXTERP"."ACT_RU_IDENTITYLINK" ("USER_ID_") 
  
  PCTFREE 10 INITRANS 2 MAXTRANS 255 COMPUTE STATISTICS 
  
  STORAGE(INITIAL 65536 NEXT 1048576 MINEXTENTS 1 MAXEXTENTS 2147483645
  
  PCTINCREASE 0 FREELISTS 1 FREELIST GROUPS 1
  
  BUFFER_POOL DEFAULT FLASH_CACHE DEFAULT CELL_FLASH_CACHE DEFAULT)
  
  TABLESPACE "ERP_TBS" ;
  
  CREATE INDEX "CXTERP"."ACT_IDX_IDENT_LNK_GROUP" ON "CXTERP"."ACT_RU_IDENTITYLINK" ("GROUP_ID_") 
  
  PCTFREE 10 INITRANS 2 MAXTRANS 255 COMPUTE STATISTICS 
  
  STORAGE(INITIAL 65536 NEXT 1048576 MINEXTENTS 1 MAXEXTENTS 2147483645
  
  PCTINCREASE 0 FREELISTS 1 FREELIST GROUPS 1
  
  BUFFER_POOL DEFAULT FLASH_CACHE DEFAULT CELL_FLASH_CACHE DEFAULT)
  
  TABLESPACE "ERP_TBS" ;
  
  CREATE INDEX "CXTERP"."ACT_IDX_TSKASS_TASK" ON "CXTERP"."ACT_RU_IDENTITYLINK" ("TASK_ID_") 
  
  PCTFREE 10 INITRANS 2 MAXTRANS 255 COMPUTE STATISTICS 
  
  STORAGE(INITIAL 65536 NEXT 1048576 MINEXTENTS 1 MAXEXTENTS 2147483645
  
  PCTINCREASE 0 FREELISTS 1 FREELIST GROUPS 1
  
  BUFFER_POOL DEFAULT FLASH_CACHE DEFAULT CELL_FLASH_CACHE DEFAULT)
  
  TABLESPACE "ERP_TBS" ;
  
  CREATE INDEX "CXTERP"."ACT_IDX_ATHRZ_PROCEDEF" ON "CXTERP"."ACT_RU_IDENTITYLINK" ("PROC_DEF_ID_") 
  
  PCTFREE 10 INITRANS 2 MAXTRANS 255 COMPUTE STATISTICS 
  
  STORAGE(INITIAL 65536 NEXT 1048576 MINEXTENTS 1 MAXEXTENTS 2147483645
  
  PCTINCREASE 0 FREELISTS 1 FREELIST GROUPS 1
  
  BUFFER_POOL DEFAULT FLASH_CACHE DEFAULT CELL_FLASH_CACHE DEFAULT)
  
  TABLESPACE "ERP_TBS" ;】
