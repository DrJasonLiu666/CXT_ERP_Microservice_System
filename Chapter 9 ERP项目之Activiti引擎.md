 注：本章资源已上传至github，详见：https://github.com/DrJasonLiu666/CXT_ERP_Microservice_System/releases/download/systemaa/ERPProject.zip

https://github.com/DrJasonLiu666/CXT_ERP_Microservice_System/releases/download/systema1r/Vendor.s_Data.zip

 另有GitLab上保留的一份资源，详见：[Dr. Chen2012 / ErpMMSDevBack · GitLab](https://gitlab.com/JackChen-Strong/cxterpmmsdevback)



# 1 介绍

该公司ERP项目的Activiti是前后端不分离项目，Idea启动后，在Chrome输入localhost:8889（application中设置port为8889），即可登录流程页面。

 ERP分前端服务器ant-design-vue、后端服务器JeecgBoot，而Activiti只需要一台。

# 2 流程设计

## 2.1 流程图（举例）

![img](https://github.com/DrJasonLiu666/CXT_ERP_Microservice_System/blob/main/photos/Chapter%209%20ERP%E9%A1%B9%E7%9B%AE%E4%B9%8BActiviti%E5%BC%95%E6%93%8E/1.png)

流程唯一标识：***作为启动流程、获取待办等的\******key\******值，必须定义。\***

## 2.2 参与者配置约定

![img](https://github.com/DrJasonLiu666/CXT_ERP_Microservice_System/blob/main/photos/Chapter%209%20ERP%E9%A1%B9%E7%9B%AE%E4%B9%8BActiviti%E5%BC%95%E6%93%8E/2.png)

![img](https://github.com/DrJasonLiu666/CXT_ERP_Microservice_System/blob/main/photos/Chapter%209%20ERP%E9%A1%B9%E7%9B%AE%E4%B9%8BActiviti%E5%BC%95%E6%93%8E/3.png)

1. 开始事件ID: Start
2. 结束事件ID: End
3. 第一个环节ID: First(其他需要业务处理逻辑的节点可以自定义ID)
4. 环节参与者任务派遣格式 ${nextUser}
5. 利用节点表单的标识Key属性配置该节点参与者类型 
   1. BPM:guardian=从流程实例参数中获取
   2. Dept:Start=查询启动人所在组织领导
   3. Dept:Start:20=查找启动人组织权重是20的领导
   4. Dept:Start:L20=查找启动人组织层级是20的领导
   5. Dept:Start:Casecade:0=从用户当前组织开始级联查找领导
   6. Dept:Start:Casecade:30=查询启动人组织权重是 30的领导(Casecade=当前权重没有，则向上级找)
   7. Dept:Submit:10=查询提交人组织权重是 10的领导
   8. Dept:Submit:L20=查找提交人组织层级是20的领导
   9. Dept:Submit:Casecade:0=从用户当前组织开始级联查找领导；
   10. Dept:Submit:Casecade:L20=查找提交人组织层级是20的领导,如果没有则级联查找上一层级组织领导；
   11. Dept:Bpm:user:10=查找传给bpm参数的user的部门是10的领导
   12. Node:nodeId=查找指定节点ID对应的参与者；
   13. Role:R001=查询角色 R001配置的用户；
   14. Clazz:com.ibm.test.ParticipantServiceImpl(spring管理的bean名称)=自定义查找参与者方法，需要实现接口 IParticipantService - 未测试 
6. 利用节点表单属性 
   1. order: 节点排序(越小越靠前)，暂时不需要。流程有唯一路径（并行时可设置节点的先后顺序）；
   2. skip: id=skip,name=EMPTY:SAME, EMPTY=节点参与者为空时跳过，SAME=节点参与者与当前处理人相同时跳过 ；
7. 会签内置参数（同一个节点多人处理时使用） 
   1. nrOfInstances：总实例数，Collection中的数量；
   2. nrOfCompletedInstances：已经完成的实例数。（可配置节点的完成条件：${nrOfCompletedInstances==1}即可实现抢占模式，多人收到待办，只要其中一人处理则流程自动流转）；
   3. nrOfActiveInstances：还没有完成的实例数。

# 3 前端组件

## 3.1 路径

# ![img](https://github.com/DrJasonLiu666/CXT_ERP_Microservice_System/blob/main/photos/Chapter%209%20ERP%E9%A1%B9%E7%9B%AE%E4%B9%8BActiviti%E5%BC%95%E6%93%8E/4.png)

## 3.2 引入方式

![img](https://github.com/DrJasonLiu666/CXT_ERP_Microservice_System/blob/main/photos/Chapter%209%20ERP%E9%A1%B9%E7%9B%AE%E4%B9%8BActiviti%E5%BC%95%E6%93%8E/5.png)

## 3.3 组件说明

| **属性名**       | **说明**                                                     | **举例**                                                     |
| ---------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| formInfo         | 业务表单                                                     |                                                              |
| nextNodeUrl      | 获取目标节点url地址，默认 /bpm/nextNodeInfo                  |                                                              |
| hideBtns         | 用于主动隐藏指定按钮,格式：数组，可选值：save/submit/approve/consult/reject/assign |                                                              |
| validate         | 提交流程时，表单验证回调函数，验证通过需要调用callback方法，该方法接收业务指定参与者 | ![img](https://github.com/DrJasonLiu666/CXT_ERP_Microservice_System/blob/main/photos/Chapter%209%20ERP%E9%A1%B9%E7%9B%AE%E4%B9%8BActiviti%E5%BC%95%E6%93%8E/10.png) |
| showProcessModel | 是否显示流程图定义模板，默认不显示                           | ![img](https://github.com/DrJasonLiu666/CXT_ERP_Microservice_System/blob/main/photos/Chapter%209%20ERP%E9%A1%B9%E7%9B%AE%E4%B9%8BActiviti%E5%BC%95%E6%93%8E/11.png) |
| generate         | 创建流程业务参数回调函数，showProcessModel为true时使用，以更好的展示实时流程图模型 |                                                              |
| save             | 保存回调函数                                                 |                                                              |
| submit           | 提交流程回调函数                                             |                                                              |
| back             | 流程驳回回调函数                                             |                                                              |
| delete           | 流程删除回调函数                                             |                                                              |
| close            | 关闭当前页签                                                 |                                                              |

## 3.4 组件初始化

![img](https://github.com/DrJasonLiu666/CXT_ERP_Microservice_System/blob/main/photos/Chapter%209%20ERP%E9%A1%B9%E7%9B%AE%E4%B9%8BActiviti%E5%BC%95%E6%93%8E/6.png)

## 3.5 其他总结

### 3.5.1 路径

activiti-activiti-src-main-resource，包括但不限于该路径下的static、templates。

### 3.5.2 前端home页面

上述路径下，templates中的home.html。

### 3.5.3 登录login页面

上述路径下，templates中的login.html。

### 3.5.4 流程定义管理页面

上述路径下，templates中的ProcDefManage.html。

### 3.5.5 流程实例管理页面

上述路径下，templates中的ProcInstManage.html。

# 4 后端接口客户端

## 4.1 路径

![img](https://github.com/DrJasonLiu666/CXT_ERP_Microservice_System/blob/main/photos/Chapter%209%20ERP%E9%A1%B9%E7%9B%AE%E4%B9%8BActiviti%E5%BC%95%E6%93%8E/7.png)

## 4.2 流程相关操作

### 4.2.1 启动流程

URL地址：[/restOperate/startProc](http://localhost:8889/restOperate/startProc)

实现方法：

```
/**
 * @description 流程启动或提交(procInstId不为空)
 * @param bpmParam userName 提交人
 *                procDefId 流程模板 ID
 *                busKey 业务单据号
 *                procInstId[可选] 流程实例 ID
 *                variables[可选] 其他业务参数
 * @return
 */
public Result start(JSONObject bpmParam) 
```

### 4.2.2 获取待办

URL地址：/restOperate/todo

实现方法：

```
/**
 * @description 获取待办
 * @param bpmParam userName 当前用户
 * @return
 */
public Result todo(JSONObject bpmParam) 
```

### 4.2.3 获取目标节点

URL地址：/restOperate/getNextNodeInfo

实现方法：

```
/**
 * 获取目标节点
 * @param bpmParam procDefId 流程定义ID(todo列表获取)
 *                 actDefId 当前节点ID(todo列表获取)
 *                 procInstId 流程实例ID
 *                 variables 业务参数JSON字符串
 * @return
 */
public Result nextNodeInfo(JSONObject bpmParam)
```

### 4.2.4 提交流程

URL地址：/restOperate/submit

实现方法：

```
/**
 * 流程提交
 * @param bpmParam userName 当前处理人
 *                 taskId 当前处理任务ID
 *                 actDefId 当前节点
 *                 destActDefId 目标节点ID
 *                  variables 其他业务参数
 * @return
 */
public Result submit(JSONObject bpmParam)
```

### 4.2.5 获取审批记录

URL地址：/restOperate/findHistory

实现方法：

```
/**
 * @description 获取审批记录
 * @param bpmParam procInstId 流程实例ID
 * @return
 */
public Result history(JSONObject bpmParam)
```

### 4.2.6 任务转办

URL地址：/restOperate/assign

实现方法：

```
/**
 * 任务分派
 * @param bpmParam taskId 当前任务ID
 *                 procInstId 流程实例ID
 *                 userName 当前处理人
 *                 variables 业务参数 
 *                     nextUser 要转办的用户
 * @return
 */
public Result assign(JSONObject bpmParam)
```

### 4.2.7 获取可驳回的节点

URL地址：/restOperate/getPreNodeInfo

实现方法：

```
/**
 * 获取可退回的节点信息
 * @param bpmParam taskId 当前任务ID
 * @return
 */
public Result preNodeInfo(JSONObject bpmParam)
```

### 4.2.8 流程驳回

URL地址：/restOperate/back

实现方法：

```
/**
 * 退回到指定节点
 * @param bpmParam taskId 当前任务ID
 *                 userName 当前处理人 
 *                 nextNodeId 要驳回的节点定义ID 
 *                 variables 业务参数
 *                     nextUser 目标节点参与者
 *                     comment 审批意见
 * @return
 */
public Result back(JSONObject bpmParam)
```

### 4.2.9 任务委派

URL地址：/restOperate/consult

实现方法：

```
/**
 * 委派任务
 * @param bpmParam taskId,procInstId,userName,variables
 */
public Result consult(JSONObject bpmParam)
```

### 4.2.10 完成委派

URL地址：/restOperate/consultResolve

实现方法：

```
/**
 * 完成委派
 */
public Result consultResolve(JSONObject bpmParam)
```

### 4.2.11 删除流程

URL地址：/restOperate/delete

实现方法：

```
/**
 * 删除流程
 * @param bpmParam
 * @return
 */
public Result delete(JSONObject bpmParam)
```

### 4.2.12 获取流程实例信息

URL地址：/restOperate/procInstInfo

实现方法：

```
/**
 * 获取流程信息
 */
public Result getProcInstInfo(String userName, String procInstId, String taskId) 
```

### **4.2.13 获取用户审批过的流程列表****(****处理中或已结束****)**

URL地址：/restOperate/approved

实现方法：

```
/**
 * 查询我审批过的
 * @param bpmParam userName 当前用户
 *                 procDefId 流程定义ID
 *                 variables
 *                     flowStatus 90=已结束，20=处理中
 * @return
 */
public Result approved(JSONObject bpmParam)
```

### 4.2.14 获取流程定义模型

URL地址：/restOperate/getProcessModel

实现方法：

```
/**
 * 流程定义模板信息
 * @param bpmParam procDefId 流程定义ID
 *                 procInstId 流程实例ID
 *                 variables 业务参数，用于判断流程中的分支条件
 */
public Result getProcessModel(JSONObject bpmParam)
```

## 4.3 其他总结



### 4.3.1 路径

activiti-activiti-src-main-java-com.cxt。

### 4.3.2 启动项

上述路径下的ActivitiserviceApplication文件。

### 4.3.3 常用文件

上述路径下，controller中的ProcController（流程管理的功能实现）和ProcRestController（流程实例跑通的功能实现）。
