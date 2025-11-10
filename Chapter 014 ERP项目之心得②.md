 注：本章资源已上传至CSDN，详见https://github.com/DrJasonLiu666/CXT_ERP_Microservice_System/releases/download/esaegae/MySummary.zip



# 1 异步（加载，上传）【或者后台运行（校验）、按需处理（加载，查看）等类似功能的实现】

## 1.1 教程

## 1.2 Web学习社区总结

https://developer.mozilla.org/zh-CN/

## 1.3 可采用的【异步】实现方法

### 1.3.1 前端

1）方法介绍（五种方法）

 https://blog.csdn.net/weixin_46022934/article/details/121322193
 
 2）（1）常用方法一：使用关键字。async与await；
 
 https://www.cnblogs.com/joe235/p/15238208.html
 
 https://www.cnblogs.com/zhoujuan/p/11692818.html
 
 2）（2）常用方法二：promise与callback；
 
 https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise/Promise

### 1.3.2 后端

1）方法介绍（四类方法）

 https://www.w3cschool.cn/article/55411104.html
 
 https://juejin.cn/post/7063002513573675045
 
 2）（1）常用方法一：定时任务；
 
 2）（2）常用方法二：https://www.cnblogs.com/lk0528/p/14965707.html

## 1.4 BPM中使用场景：

### 1.4.1 整体系统场景

vue2前端中：审批历史的异步加载；table的items过多时上传采取异步。

 JeecgBoot后端中：先return返回给前端结果，数据处理（如运算）异步运行。

### 1.4.2 前端场景

vue2前端中可采取的方式：

 异步（如加载，上传）

 后台运行（如校验）
 
 按需处理（如查看，使用）

### 1.4.3 后端场景

JeecgBoot后端可采取的方式：

## 1.5 代码实现示例

vue2前端中【异步加载】的实现，以审批历史的加载为例：

 ①目标page页面中引入<bpmApproval.vue>文件的页面组件；
 
 ②<bpmApproval.vue>文件的使用异步方法：this.asyncAll（）【在<common.js>文件中定义】

 ```
       loadHistory() {
         debugger
         this.loading = true;
         let len = this.procInstIds.length - 1;
         console.log("loadHistory this.procInstIds", this.procInstIds);
         let asyncFuncs = [];
         this.procInstIds.forEach((procInstId, ind) => {
           asyncFuncs.push(this.asyncLoadHistory(procInstId));
         });
         this.asyncAll(asyncFuncs, (data) => {
           debugger
           console.log("loadHistory All", data);
           let dataSource = [];
           for(let i = 0; i < data.length; i++) {
             dataSource = dataSource.concat(data[i]);
           }
           // 需要处理一下 recall的 node name，与recall的操作节点一致
           dataSource.forEach((d, ind) => {
             if(this.G_CONST.bpmAction.recall == d.action) {
               d.nodeName = dataSource[ind - 1].nodeName;
             }
           });
           console.log("dataSource", dataSource);
           this.dataSource = dataSource;
           // 将附件添加到审核历史中
           this.addAttachment();
           // 根据审批历史判断是否能进行撤回操作
           this.toggleRecallBtn();
           this.parseAgentUser();
           // 获取其他已审核结束的流程的审批附件
           this.loadApprovedAttachments();
           this.loading = false;
         });
       },
```

 ③<common.js>文件中定义方法：this.asyncAll（）

 ```
   asyncAll: function (funcs, callback) {
    debugger
    Promise.all(funcs).then(res => {
     callback(res);
    }, reason => {
     console.log(reason);
    })
   },
```

 执行过程：loadHistory中的this.asyncAll() ——> promise ——> callback(res) ——> loadHistory中的callback(data)
 
 promise,callback

# 2 后端先返回前端报文，再执行其他逻辑

## 2.1 参考教程

https://blog.csdn.net/qq_31772441/article/details/109848307

https://blog.csdn.net/flower_CSDN/article/details/128340853?spm=1001.2101.3001.6661.1&utm_medium=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-128340853-blog-109848307.235%5Ev27%5Epc_relevant_t0_download&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-128340853-blog-109848307.235%5Ev27%5Epc_relevant_t0_download&utm_relevant_index=1

# 3 后端使用json格式将数据返回给前端的三种方式的实现

## 3.1 参考教程

https://blog.csdn.net/qq_41063141/article/details/93379021

# 4 java中创建线程与线程池

## 4.1 参考教程

https://blog.csdn.net/qq_35275233/article/details/87893337

https://blog.csdn.net/qq_44324963/article/details/108375479?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_baidulandingword~default-1-108375479-blog-87893337.235^v27^pc_relevant_t0_download&spm=1001.2101.3001.4242.2&utm_relevant_index=4

https://blog.csdn.net/weixin_47872288/article/details/122086158?spm=1001.2101.3001.6650.17&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7ERate-17-122086158-blog-87893337.235%5Ev27%5Epc_relevant_t0_download&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7ERate-17-122086158-blog-87893337.235%5Ev27%5Epc_relevant_t0_download&utm_relevant_index=23

# 5 JUC多线程高并发编程

## 5.1 参考教程

https://blog.csdn.net/weixin_47872288/article/details/119453092
 https://blog.csdn.net/lyly4413/article/details/87866726
