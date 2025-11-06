# 1 开发环境

## 1.1 ERP项目示例

![img](https://github.com/DrJasonLiu666/CXT_ERP_Microservice_System/blob/main/photos/Chapter%206%20ERP%E9%A1%B9%E7%9B%AE%E4%B9%8B%E7%B3%BB%E7%BB%9F%E6%90%AD%E5%BB%BA/1.png)

# 2 版本管理GitLab

## 2.1 ERP项目示例

![img](https://github.com/DrJasonLiu666/CXT_ERP_Microservice_System/blob/main/photos/Chapter%206%20ERP%E9%A1%B9%E7%9B%AE%E4%B9%8B%E7%B3%BB%E7%BB%9F%E6%90%AD%E5%BB%BA/2.png)

![img](https://github.com/DrJasonLiu666/CXT_ERP_Microservice_System/blob/main/photos/Chapter%206%20ERP%E9%A1%B9%E7%9B%AE%E4%B9%8B%E7%B3%BB%E7%BB%9F%E6%90%AD%E5%BB%BA/3.png)

![img](https://github.com/DrJasonLiu666/CXT_ERP_Microservice_System/blob/main/photos/Chapter%206%20ERP%E9%A1%B9%E7%9B%AE%E4%B9%8B%E7%B3%BB%E7%BB%9F%E6%90%AD%E5%BB%BA/4.png)

## 2.2 搭建GitLab私服

①参考教程：[(47条消息) GitLab 私服搭建_gitlabsifu_wachoo的博客-CSDN博客](https://blog.csdn.net/Byd_chao/article/details/105784749)

# 3 部署管理Jenkins

## 3.1 Jenkins官网

[Jenkins](https://www.jenkins.io/zh/)

## 3.2 搭建Jenkins私服

### 3.2.1 教程

[【Jenkins】Linux搭建Jenkins平台 - KK_Yolanda - 博客园 (cnblogs.com)](https://www.cnblogs.com/zhaoxd07/p/4956637.html#:~:text=② 下载一个tomcat容器在webapps中放入jenkins.war%2C不要解压。 ③ 在cd %2Fopt%2Fsoft%2Ftomcat%2Fwebapps%2F,中执行 java -jar jenkins.war ④ 查看日志是否有异常，访问http%3A%2F%2Fip%3A8080即可看到jenkins界面，jenkins安装成功。)

### 3.2.2 一键发版（Pipeline的使用）

1）作用：Pipeline的使用实现了一键发版；

2）Pipeline配置路径：某一工程 —— 配置 —— 流水线（定义：Pipeline script；脚本：【详见2.2.3】）

### 3.2.3 Pipeline配置脚本（以ERP项目为例）

1）Activiti_DEV

```TypeScript
try{
    stage('checkout'){
        node('master'){ 
          git branch:'dev', credentialsId: '4cbb8626-96fc-45c6-a48a-80ee3766a745', url: 'git@10.98.16.63:erp/activity.git' 
        }
    }
    stage('mvn build'){
        node('master'){
            withEnv(["PATH+MAVEN=${tool 'maven'}/bin"]){
                sh 'pwd'
                sh 'mvn -f activity/  clean install  -Dmaven.test.skip=true'
            }
        }
    }
    stage('docker build'){
        node('master'){
            sh 'pwd'
            sh 'bash ./activity/buildDockerImageDev.sh'
        }
    }
    
    stage('deploy&restart'){
        node('master'){
            //正式环境k8s master 重启
            sleep 20
            sh 'ssh root@10.98.13.204 "kubectl rollout restart -n erp deployment erp-activity-v1"'
        }
    }
    
}catch(error){
    currentBuild.result = 'FAILED'
    throw error
}finally{
    
}
```



2）Activiti_PRD

```TypeScript
try{    
    stage('checkout'){        
        node('master'){           
            git branch:'prd', credentialsId: '4cbb8626-96fc-45c6-a48a-80ee3766a745', url: 'git@10.98.16.63:erp/activity.git'         
            
        }    
        
    }    
    stage('mvn build'){        
        node('master'){           
            withEnv(["PATH+MAVEN=${tool 'maven'}/bin"]){                
                sh 'pwd'                
                sh 'mvn -f activity/  clean install  -Dmaven.test.skip=true'            
                
            }        
            
        }    
        
    }    
    stage('docker build'){        
        node('master'){            
            sh 'pwd'            
            sh 'bash ./activity/buildDockerImageDev.sh'        
        }    
        
    }        
    stage('deploy&restart'){        
        node('master'){            
            //正式环境k8s master 重启            
            sleep 20            
            sh 'ssh root@10.98.16.70 "kubectl rollout restart -n erp-bpm deployment erp-activity-v1"'        
            
        }    
        
    }    
    
}catch(error){    
    currentBuild.result = 'FAILED'    
    throw error
    
}
    
finally{    
        
    }
```



3）PRPO_BACK_DEV

```TypeScript
try{
    stage('checkout'){
        node('master'){ 
          git branch:'dev', credentialsId: '4cbb8626-96fc-45c6-a48a-80ee3766a745', url: 'git@10.98.16.63:erp/erp.git' 
        }
    }
    stage('mvn build'){
        node('master'){
            withEnv(["PATH+MAVEN=${tool 'maven'}/bin"]){
                sh 'pwd'
                sh 'mvn -f console/ clean install  -Dmaven.test.skip=true'
            }
        }
    }
    stage('docker build'){
        node('master'){
            sh 'pwd'
            sh 'bash ./console/buildDockerImageDev.sh'
        }
    }
    
    stage('deploy&restart'){
        node('master'){
            //正式环境k8s master 重启
            sleep 200
            sh 'ssh root@10.98.13.204 "kubectl rollout restart -n erp deployment erp-console-v1"'
        }
    }
    
}catch(error){
    currentBuild.result = 'FAILED'
    throw error
}finally{
    
}
```



4）PRPO_BACK_PRD

```TypeScript
try{
    stage('checkout'){
        node('master'){ 
          git branch:'prd', credentialsId: '4cbb8626-96fc-45c6-a48a-80ee3766a745', url: 'git@10.98.16.63:erp/erp.git' 
        }
    }
    stage('mvn build'){
        node('master'){
            withEnv(["PATH+MAVEN=${tool 'maven'}/bin"]){
                sh 'pwd'
                sh 'mvn -f console/ clean install  -Dmaven.test.skip=true'
            }
        }
    }
    stage('docker build'){
        node('master'){
            sh 'pwd'
            sh 'bash ./console/buildDockerImageDev.sh'
        }
    }
    
    stage('deploy&restart'){
        node('master'){
            //正式环境k8s master 重启
            sleep 200
            sh 'ssh root@10.98.16.70 "kubectl rollout restart -n erp-bpm deployment erp-console-v1"'
        }
    }
    
}catch(error){
    currentBuild.result = 'FAILED'
    throw error
}finally{
    
}
```


5）PRPO_FRONT_DEV

```TypeScript
try{
    stage('checkout'){
        node('master'){
           sh 'echo hello world'
           git branch:'dev', credentialsId: '4cbb8626-96fc-45c6-a48a-80ee3766a745', url: 'git@10.98.16.63:erp/erpweb.git' 
          
        } 
    }
    stage('clean'){
        node('master'){
            sh 'rm -rf /data/jenkins/workspace/erp_front/frontend/node_modules'
            sh 'rm -rf /data/erpweb_dev/*'
            sh 'echo clean finish'
        }
    }
    stage('build'){
        node('master'){
          sh 'cp -r /data/erp_node/node_modules /data/jenkins/workspace/erp_front/frontend/node_modules'
            dir('/data/jenkins/workspace/erp_front/frontend/node_modules/.bin/'){
               sh 'pwd'
               sh 'chmod -R 775 ./*'   
            }
            nodejs('nodejs'){
               sh 'node -v'
               sh 'npm -v'
               sh 'whoami'
               sh 'pwd'
               sh 'cd frontend/  && npm run build'
               sh 'cp -r /data/jenkins/workspace/erp_front/frontend/dist/* /data/erpweb_dev'
               dir('/data/nginx/sbin/'){
                   sh 'pwd'
                   sh './nginx -s stop'
                   sh './nginx'
               } 
            } 
        }
    }
}catch(error){
    currentBuild.result = "FAILED";
    throw error
}finally{
    
}
```



6）PRPO_FRONT_PRD

```TypeScript
try{    
    stage('checkout'){        
        node('master'){           
            sh 'echo hello world'           
            git branch:'prd',
            credentialsId: '4cbb8626-96fc-45c6-a48a-80ee3766a745', url: 'git@10.98.16.63:erp/erpweb.git'                   
        }     
        
    }    
    stage('clean'){        
        node('master'){            
            sh 'rm -rf /data/jenkins/workspace/erp_front_prd/frontend/node_modules'            
            sh 'rm -rf /data/erpweb_prd/*'            
            sh 'echo clean finish'        
        }    
    }    
    stage('build'){        
        node('master'){          
            sh 'cp -r /data/erp_node/node_modules /data/jenkins/workspace/erp_front_prd/frontend/node_modules'            
            dir('/data/jenkins/workspace/erp_front_prd/frontend/node_modules/.bin/')
            {               
                sh 'pwd'               
                sh 'chmod -R 775 ./*'               
            }            
            nodejs('nodejs'){               
                sh 'node -v'               
                sh 'npm -v'               
                sh 'whoami'               
                sh 'pwd'               
                sh 'cd frontend/  && npm run build'               
                sh 'cp -r /data/jenkins/workspace/erp_front_prd/frontend/dist/* /data/erpweb_prd'               
                sh 'scp -r /data/jenkins/workspace/erp_front_prd/frontend/dist/* root@10.98.16.71:/data/erpweb_prd'               
                sh 'ssh root@10.98.16.71 "/usr/local/nginx/sbin/nginx -s reload"'               
                sh 'ssh root@10.98.16.71 "/usr/local/nginx/sbin/nginx -t"'      
                sh 'scp -r /data/jenkins/workspace/erp_front_prd/frontend/dist/* root@10.98.16.72:/data/erpweb_prd'               
            }         
        }    
    }
}catch(error){    
    currentBuild.result = "FAILED";    
    throw error
}finally{   
}
```


## 3.3 ERP项目示例

![img](https://github.com/DrJasonLiu666/CXT_ERP_Microservice_System/blob/main/photos/Chapter%206%20ERP%E9%A1%B9%E7%9B%AE%E4%B9%8B%E7%B3%BB%E7%BB%9F%E6%90%AD%E5%BB%BA/3.3.1.png)

![img](https://github.com/DrJasonLiu666/CXT_ERP_Microservice_System/blob/main/photos/Chapter%206%20ERP%E9%A1%B9%E7%9B%AE%E4%B9%8B%E7%B3%BB%E7%BB%9F%E6%90%AD%E5%BB%BA/3.3.2.png)

![img](https://github.com/DrJasonLiu666/CXT_ERP_Microservice_System/blob/main/photos/Chapter%206%20ERP%E9%A1%B9%E7%9B%AE%E4%B9%8B%E7%B3%BB%E7%BB%9F%E6%90%AD%E5%BB%BA/3.3.3.png)



# 4 依赖管理Maven

## 4.1 私服存在的合理性

### 4.1.1 参考教程

[Maven私服Nexus的搭建 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/86074102)

[Maven 私服搭建指南 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/148636979)

### 4.1.2 原因

①Maven用户直接连接远程仓库下载构件的做法是Maven不建议使用的（尤其是对一个开发团队来说），Maven的最佳实践就是使用Maven私服来构建整个团队的项目部署和管理。

②当我们在 pom 文件中依赖了某个包后，如果在没有做特殊配置（也就是使用 maven 的默认配置）的情况下，Maven 会首先到本地仓库去搜索，如果本地仓库没有此依赖包，会到中央仓库获取，默认的中央仓库地址是 http://repo1.maven.org/maven2，服务器在国外，可想而知，速度是没办法保证的。有时候运气不好，晚上拉下来一个开源项目，执行 Maven 包安装，早上睡醒了一看，还没下载完，你说来气不。

## 4.2 搭建Maven私服Nexus

### 4.2.1 sonatype官网

[Welcome to Sonatype Help](https://help.sonatype.com/docs)

### 4.2.2 参考教程

[(47条消息) Nexus下载、安装与使用_lovelife000的博客-CSDN博客](https://blog.csdn.net/lovelife000/article/details/125880764)

## 4.3 Maven依赖在代码中的引用

pom.xml文件中每个依赖的<url></url>

```XML
	<!--jar upload-->
	<distributionManagement>
		<repository>
			<id>cxtmis-release</id>
			<name>maven-releases</name>
			<url>http://10.98.16.63:8090/repository/maven-releases/</url>
		</repository>
		<snapshotRepository>
			<id>cxtmis-snapshots</id>
			<name>maven-snapshots</name>
			<url>http://10.98.16.63:8090/repository/maven-snapshots/</url>
		</snapshotRepository>
	</distributionManagement>
```


## 4.4 ERP项目示例

![img](https://github.com/DrJasonLiu666/CXT_ERP_Microservice_System/blob/main/photos/Chapter%206%20ERP%E9%A1%B9%E7%9B%AE%E4%B9%8B%E7%B3%BB%E7%BB%9F%E6%90%AD%E5%BB%BA/8.png)

![img](https://github.com/DrJasonLiu666/CXT_ERP_Microservice_System/blob/main/photos/Chapter%206%20ERP%E9%A1%B9%E7%9B%AE%E4%B9%8B%E7%B3%BB%E7%BB%9F%E6%90%AD%E5%BB%BA/9.png)

# 5 镜像仓库HARBOR

## 5.1 ERP项目示例

![img](https://github.com/DrJasonLiu666/CXT_ERP_Microservice_System/blob/main/photos/Chapter%206%20ERP%E9%A1%B9%E7%9B%AE%E4%B9%8B%E7%B3%BB%E7%BB%9F%E6%90%AD%E5%BB%BA/10.png)

## 5.2 容器镜像DOCKER

### 5.2.1 为什么使用DOCKER

即，使同一主机（如服务器）或集群能够同时运行不同的应用程序而不互相干扰（使用同一 IP地址，但不同端口）。

现代软件开发的目标之一是应用程序既能运行在同一主机或集群上，又能彼此隔离，这样它们就不会过度干扰彼此的操作或维护，但由于要运行包、库和其他软件组件，这样就会变得会比较困难。

解决这个问题的方案之一是用虚拟机，它将相同硬件上的应用程序完全隔离，并将软件组件之间的冲突和硬件资源之间的竞争降到最低，但是虚拟机体积比较庞大，每个虚拟机都需要自己的操作系统，所以通常是GB大小而且很难维护和升级。

与虚拟机相反，容器将应用程序的执行环境彼此隔离，但共享底层OS内核。它们通常以兆字节为单位，使用的资源比虚拟机少得多，而且几乎是立即启动的。可以做到在相同的硬件上更密集地打包，而不需要花费太多的精力和开销。

详见：[什么是Docker容器，它有什么作用？ - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/139588660)

## 5.3 （容器）镜像仓库HARBOR

### 5.3.1 原因

在默认情况下，我们安装好 Docker 后，其默认访问的远端镜像仓库是 Docker Hub，在国内访问 Docker Hub 一般都是龟速（主要体现在 `docker push/pull` 操作），但我们可以通过配置一些国内的镜像仓库地址来加速访问，如搭建私有化容器镜像仓库HARBOR。

详见：[浅谈镜像仓库的选择 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/384680246)

### 5.3.2 搭建私有化HARBOR

1）教程：[(47条消息) Harbor镜像仓库的安装以及Docker从Harbor上传与下载镜像_倔强的耗子的博客-CSDN博客](https://blog.csdn.net/weixin_44178366/article/details/106988199)

# 6 容器管理HUBESPHERE

## 6.1 KUBESPERE官网

[面向云原生应用的容器混合云，支持 Kubernetes 多集群管理的 PaaS 容器云平台解决方案 | KubeSphere](https://kubesphere.io/zh/)

## 6.2 KUBESPHERE安装教程

[(47条消息) (史上最完整)k8s和kubesphere搭建图文教程_两人一城的博客-CSDN博客](https://blog.csdn.net/weixin_42604996/article/details/119112972)

## 6.3 ERP项目示例

![img](https://github.com/DrJasonLiu666/CXT_ERP_Microservice_System/blob/main/photos/Chapter%206%20ERP%E9%A1%B9%E7%9B%AE%E4%B9%8B%E7%B3%BB%E7%BB%9F%E6%90%AD%E5%BB%BA/11.png)

![img](https://github.com/DrJasonLiu666/CXT_ERP_Microservice_System/blob/main/photos/Chapter%206%20ERP%E9%A1%B9%E7%9B%AE%E4%B9%8B%E7%B3%BB%E7%BB%9F%E6%90%AD%E5%BB%BA/12.png)

![img](https://github.com/DrJasonLiu666/CXT_ERP_Microservice_System/blob/main/photos/Chapter%206%20ERP%E9%A1%B9%E7%9B%AE%E4%B9%8B%E7%B3%BB%E7%BB%9F%E6%90%AD%E5%BB%BA/13.png)

![img](https://github.com/DrJasonLiu666/CXT_ERP_Microservice_System/blob/main/photos/Chapter%206%20ERP%E9%A1%B9%E7%9B%AE%E4%B9%8B%E7%B3%BB%E7%BB%9F%E6%90%AD%E5%BB%BA/14.png)

![img](https://github.com/DrJasonLiu666/CXT_ERP_Microservice_System/blob/main/photos/Chapter%206%20ERP%E9%A1%B9%E7%9B%AE%E4%B9%8B%E7%B3%BB%E7%BB%9F%E6%90%AD%E5%BB%BA/15.png)



# 7 文件管理（Nas挂载）

## 7.1 ERP项目示例

![img](https://github.com/DrJasonLiu666/CXT_ERP_Microservice_System/blob/main/photos/Chapter%206%20ERP%E9%A1%B9%E7%9B%AE%E4%B9%8B%E7%B3%BB%E7%BB%9F%E6%90%AD%E5%BB%BA/16.png)



# 8 （通用）API接口管理

## 8.1 ERP项目示例

![img](https://github.com/DrJasonLiu666/CXT_ERP_Microservice_System/blob/main/photos/Chapter%206%20ERP%E9%A1%B9%E7%9B%AE%E4%B9%8B%E7%B3%BB%E7%BB%9F%E6%90%AD%E5%BB%BA/17.png)

# 9 集群k8s

## 9.1 ERP项目示例

![img](https://github.com/DrJasonLiu666/CXT_ERP_Microservice_System/blob/main/photos/Chapter%206%20ERP%E9%A1%B9%E7%9B%AE%E4%B9%8B%E7%B3%BB%E7%BB%9F%E6%90%AD%E5%BB%BA/18.png)

## 9.2 K8S安装教程

[(47条消息) (史上最完整)k8s和kubesphere搭建图文教程_两人一城的博客-CSDN博客](https://blog.csdn.net/weixin_42604996/article/details/119112972)

# 10 Swagger

## 10.1 示例

Swagger生成接口文档，并支持在线测试接口

![img](https://github.com/DrJasonLiu666/CXT_ERP_Microservice_System/blob/main/photos/Chapter%206%20ERP%E9%A1%B9%E7%9B%AE%E4%B9%8B%E7%B3%BB%E7%BB%9F%E6%90%AD%E5%BB%BA/19.png)

# 11 杂记

## 11.1 Apache服务器和tomcat服务器区别

1.概述

Apache与Tomcat都是Apache开源组织开发的用于处理HTTP服务的项目，两者都是免费的，都可以做为独立的Web服务器运行。Apache是Web服务器而Tomcat是Java应用服务器。

2.具体区分

Apache服务器 只处理 静态HTML；tomcat服务器 静态HTML 动态 JSP Servlet 都能处理。

一般是把 Apache服务器与tomcat服务器 搭配在一起用。 Apache服务器负责处理所有 静态的页面/图片等信息。Tomcat只处理动态的部分。

（1）Apache：是C语言实现的，专门用来提供HTTP服务。

特性：简单、速度快、性能稳定、可配置（代理）

1、主要用于解析静态文本，并发性能高，侧重于HTTP服务；

2、支持静态页（HTML），不支持动态请求如：CGI、Servlet/JSP、PHP、ASP等；

3、具有很强的可扩展性，可以通过插件支持PHP，还可以单向Apache连接Tomcat实现连通；

4、Apache是世界使用排名第一的Web服务器。

（2）Tomcat：是Java开发的一个符合JavaEE的Servlet规范的JSP服务器（Servlet容器），是 Apache 的扩展。

特性：免费的Java应用服务器

1、主要用于解析JSP/Servlet，侧重于Servlet引擎；

2、支持静态页，但效率没有Apache高；支持Servlet、JSP请求；

3、Tomcat本身也内置了一个HTTP服务器用于支持静态内容，可以通过Tomcat的配置管理工具实现与Apache整合。


3.Apache 和Tomcat组合

两者整合后优点：如果请求是静态网页则由Apache处理，并将结果返回；如果是动态请求，Apache会将解析工作转发给Tomcat处理，Tomcat处理后将结果通过Apache返回。这样可以达到分工合作，实现负载远衡，提高系统的性能。

4.总结

apache是web服务器，tomcat是应用（java）服务器，它只是一个servlet容器，可以认为是apache的扩展，但是可以独立于apache运行。

换句话说，apache是一辆卡车，上面可以装一些东西如html等。但是不能装水，要装水必须要有容器（桶），而这个桶也可以不放在卡车上。

## 11.2 服务器部署的几种形式

 环境&技术架构的几种形式，即服务器部署的几种形式，各服务软件的部署方式：

【集中式服务器，独立式服务器】

详见链接：

[(23条消息) B/S架构及其运行原理_蜘蛛侠不会飞的博客-CSDN博客_b/s](https://blog.csdn.net/qq_40587575/article/details/79673478)

## 11.3 服务器连接工具

 **1、putty 与winscp 有什么区别， 装了 winscp 可以由 putty 替换么 ？**

具体用法 是什么 ？

PuTTY是一个Telnet、SSH、rlogin、纯TCP以及串行接口连接软件。较早的版本仅支持Windows平台，在最近的版本中开始支持各类Unix平台，并打算移植至Mac OS X上。除了官方版本外，有许多第三方的团体或个人将PuTTY移植到其他平台上，像是以Symbian为基础的移动电话。PuTTY为一开放源代码软件，主要由Simon Tatham维护，使用MIT licence授权。随着Linux在服务器端应用的普及，Linux系统管理越来越依赖于远程。在各种远程登录工具中，Putty是出色的工具之一。Putty是一个免费的、Windows 32平台下的telnet、rlogin和ssh客户端，但是功能丝毫不逊色于商业的telnet类工具。

WinSCP是一个Windows环境下使用SSH的开源图形化SFTP客户端。同时支持SCP协议。它的主要功能就是在本地与远程计算机间安全的复制文件。WinSCP是一个Windows环境下使用SSH的开源图形化SFTP客户端。同时支持SCP协议。它的主要功能就是在本地与远程计算机间安全的复制文件。

可以同时使用的呀。

putty 输入命令行的。

winscp主要是删除，上传文件的时候有个图形界面，方便。
 
【1出自：原文链接：[(25条消息) putty 与winscp 区别_lxw1844912514的博客-CSDN博客](https://blog.csdn.net/lxw1844912514/article/details/100027170)】



**2、FileZilla，WinSCP，VNC，putty，mstsc区别**

FileZilla是ftp用的，WinSCP是连接Windows和Linux的，VNC是Windows以图形界面访问Linux或者mac的，putty是Windows连接Linux命令行的，mstsc（Microsoft Terminal Service Client）是Windows连接Windows的远程桌面。

Filezilla分为client和server。其中FileZilla Server是Windows平台下一个小巧的第三方FTP[服务器](https://cloud.tencent.com/product/cvm?from=10680)软件，系统资源也占用非常小，可以让你快速简单的建立自己的FTP服务器

【2出自：原文链接：[FileZilla，WinSCP，VNC，putty，mstsc区别 - 腾讯云开发者社区-腾讯云 (tencent.com)](https://cloud.tencent.com/developer/article/1352397#:~:text=FileZilla，WinSCP，VNC，putty，mstsc区别 发布于2018-10-09 19%3A05%3A02 阅读 1.5K,0 FileZilla是ftp用的，WinSCP是连接Windows和Linux的，VNC是Windows以图形界面访问Linux或者mac的，putty是Windows连接Linux命令行的，mstsc（Microsoft Terminal Service Client）是Windows连接Windows的远程桌面。)】



**3、\**\*\*\*\*\*\*\*\*\*\*\*\*[使用WinScp连接远程服务器和传输文件](https://www.cnblogs.com/fuyaozhishang/p/8033849.html)\*\*\*\*\*\*\*\*\*\*\*\*\****

[使用WinScp连接远程服务器和传输文件 - 你要 - 博客园 (cnblogs.com)](https://www.cnblogs.com/fuyaozhishang/p/8033849.html)

## 11.4 BS系统（即Web开发）通信原理

- 一个端口代表一个软件（一个端口代表一个应用，一个端口仅代表一个服务）。
- 一个计算机当中有很多软件，每一个软件启动之后都有一个端口号。
- 在同一个计算机上，端口号具有唯一性。

详见一：[(23条消息) JavaWeb学习笔记二：BS结构系统通信原理_i既来之的博客-CSDN博客](https://blog.csdn.net/qq_45372862/article/details/128240847?ops_request_misc=&request_id=&biz_id=102&utm_term=BS结构学习&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-0-128240847.nonecase&spm=1018.2226.3001.4187)

##  11.5 MyBatis-plus

1 简介

学习参考教程：

[(54条消息) MyBatis-Plus快速入门与进阶详解 ＜＜目录＞＞_Zack_tzh的博客-CSDN博客](https://blog.csdn.net/Zack_tzh/article/details/107486968)

2 常用知识点

2.1 设置entity实体类对应的表名、字段名

1. 参考教程：[(54条消息) MyBatis-Plus（二）设置实体类对应的表名、字段名_mybatisplus指定表名_Zack_tzh的博客-CSDN博客](https://blog.csdn.net/Zack_tzh/article/details/107487209)

2. 关键字：驼峰命名，下划线命名。

## 11.6 Java中的annotation注解

参考教材：

[一篇文章，全面掌握Java自定义注解（Annontation） - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/60730622)

[Java注解 - Java教程 (yiibai.com)](https://www.yiibai.com/java/java-annotation-tutorial.html#:~:text=Java注解 1 1. 什么是注解 Java注解用于为Java代码提供元数据。 作为元数据，注解不直接影响你的代码执行，但也有一些类型的注解实际上可以用于这一目的。 Java注解通常用于以下目的： 编译器指令,没有函数体； 没有函数参数； 返回的声明必须在一个特定的类型： 基本类型 (boolean%2C int%2C float%2C…) )

[(54条消息) java中为什么要用注解_java中的注解，真的很重要，你理解了嘛？_weixin_39779537的博客-CSDN博客](https://blog.csdn.net/weixin_39779537/article/details/114134990)

## 11.7 ERP项目的启动

代码、架构；

配置（文件）、依赖（pom.xml、Maven、Dependency等等）、环境（本地开发环境、测试环境、生产环境等等）、服务器

Nexus（Maven私服搭建）教程：http://c.biancheng.net/nexus/

Sonatype Nexus Repository Manager

业务系统

权限管理系统

Activiti

## 11.8 PRPO前端私有化

在vue2菜单管理中创建菜单栏，vscode中引入相应代码，并在角色管理中进行菜单授权；
