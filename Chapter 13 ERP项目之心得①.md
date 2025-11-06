 注：本章资源已上传至CSDN，详见https://github.com/DrJasonLiu666/CXT_ERP_Microservice_System/releases/download/esaegae/MySummary.zip



# 1 JeecgBoot架构

## 1.1 后端构成

### 1.1.1 参考教程

https://blog.csdn.net/m0_55464994/article/details/113923449

### 1.1.2 构成

基础、持久、安全；

 缓存、打印、连接池；
 
 微服务的架构与技术栈，及其他；

## 1.2 后端架构文档

https://docs.gechiui.com/zhangdaiscott-jeecg-boot/1.html

## 1.3 架构层级关系

application ——> client层；

 entity ——> service层；（entity用service层自带方法，或者逐层写方法）

注意：新建某entity的service时，需要逐层新建其他底层的文件，否则报错：

 Field erpTDaSettingService in org.jeecg.modules.matnr.controller.ErpTMaterialController required a bean of type 'org.jeecg.modules.matnr.service.IErpTDaSettingService' that could not be found.

#   2 vue架构

## 2.1 vue生命周期（钩子函数）

### 2.1.1 定义

### 2.1.2 过程图

【过程：1 2 2 4；3 1 3】

### 2.1.3 生命周期函数（四个阶段，四类钩子）

①创建/初始化；

②挂载；

③更新；

④销毁；

### 2.1.4 参考教程

https://blog.csdn.net/su2231595742/article/details/115186957

https://blog.csdn.net/weixin_65548623/article/details/127563205

utm_medium=distribute.wap_relevant.none-task-blog-2~default~baidujs_baidulandingword~default-5-127563205-blog-128554902.wap_blog_relevant_default&spm=1001.2101.3001.4242.4

https://zhuanlan.zhihu.com/p/277779087

https://blog.csdn.net/LUNJINGJIE/article/details/94024149

## 2.2 前端运行机制--页面渲染流程

### 2.2.1 教程

https://zhuanlan.zhihu.com/p/130857030

https://zhuanlan.zhihu.com/p/277779087

### 2.2.2 前提

浏览器将域名通过网络通信从服务器拿到html文件后，再进行页面渲染。

### 2.2.3 过程

HTML文件（字节） -> 字符 -> Token -> 节点 -> DOM树；

## 2.3 vue初次加载时文件执行顺序（进入登录界面）

### 2.3.1 参考教程

https://blog.csdn.net/jiaoyangdetian/article/details/115760691

### 2.3.2 过程

main.js（程序的入口文件） -> index.html（vue项目的默认首页） -> App.vue（用App.vue的templete替换index.html中的<div id="app"></div>） -> index.js（路由文件，将对应的组件渲染到router-view中） -> 对应组件【first.vue（登录界面），或者其他vue界面】

## 2.4 ant design vue路由功能的实现/路由守卫

### 2.4.1 功能描述：动态路由

### 2.4.2 参考教程

https://blog.csdn.net/chenlx99/article/details/122744403

https://developer.aliyun.com/article/922874

https://www.cnblogs.com/junwu/p/14794358.html#:~:text=antd%20design%20pro%20vue%20%E7%9A%84%E8%B7%AF%E7%94%B1%E6%9C%89%E4%B8%A4%E7%A7%8D%E6%96%B9%E5%BC%8F,%E4%B8%80%E7%A7%8D%E6%98%AF%E5%89%8D%E7%AB%AF%E5%AE%9A%E4%B9%89%E5%A5%BD%E8%B7%AF%E7%94%B1routes%EF%BC%8C%E7%94%B1%E5%90%8E%E7%AB%AF%E8%BF%94%E5%9B%9Eroles%E8%BF%9B%E8%A1%8C%E8%BF%87%E6%BB%A4%20%EF%BC%9B%20%E5%8F%A6%E4%B8%80%E7%A7%8D%E6%98%AF%E5%90%8E%E7%AB%AF%E8%BF%94%E5%9B%9E%20routes%20%E5%88%97%E8%A1%A8%20%E7%94%9F%E6%88%90menu%E3%80%82

https://blog.csdn.net/weixin_65548623/article/details/127563205?utm_medium=distribute.wap_relevant.none-task-blog-2~default~baidujs_baidulandingword~default-5-127563205-blog-128554902.wap_blog_relevant_default&spm=1001.2101.3001.4242.4

## 2.5 整个系统级全局常量的声明

1）在src/utils/GlobalConstant.js文件中定义各个常量

 export const GlobalConstant = { maxExportSize =  50000}，

2）在src/main.js文件中改名：Vue.prototype.G_CONST = GlobalConstant;

3）在其他vue文件中引用，如：var pageSize = this.G_GONST.maxExportSize;

# 3 社区

## 3.1 华为开发者联盟

https://huaweicloud.csdn.net/?utm_source=blog_detail

## 3.2 csdn

## 3.3 gitcode

## 3.4 gitee

## 3.5 github

## 3.6 gitlab

## 3.7 stackOverFlow

## 3.8 PHP中文网

https://www.php.cn/

# 4 vue学习（不含架构）

## 4.1 Web三件套  基础知识学习

### 4.1.1 作用：HTML  侧重于结构/标签；CSS  侧重于样式；JS  侧重于逻辑；

### 4.1.2 学习教程（待吸收）

https://blog.csdn.net/weixin_65548623/category_11739767.html?spm=1001.2014.3001.5482

## 4.2 当浏览器窗口尺寸改变触发Resize()后，页面问题解决方案

### 4.2.1 常见问题

页面刷新Reflow，清理了之前的数据。

### 4.2.2 解决方案

1）页面自适应窗口大小（onresize

https://blog.csdn.net/m0_47901007/article/details/121920505

2）HTML页面缩小后显示滚动条

https://blog.csdn.net/qq_44614115/article/details/113964768

### 4.2.3 resize事件监听用法

https://blog.csdn.net/zouhai1/article/details/119940253

## 4.3 前端中五种  位置设定方式

### 4.3.1 教程

https://blog.csdn.net/qq_39347364/article/details/104999151

### 4.3.2 五种position：

①static：默认值,设置坐标无效。如20px；

②absolute：绝对定位。不占据文档流，在网页中需要重叠的位置使用，如金字塔；

③relative：相对定位。占据文档流，主要给绝对定位提供包含块，如一层层嵌套；

④fixed：固定定位。脱离文档流，用于网页上跟随着 视口移动的元素，如固定的横条与侧向条；

⑤sticky：粘性定位。页面达到一定高度时，脱离文档流。效果是吸附浏览器顶部。

## 4.4 a-input与j-input输入框的区别

### 4.4.1 代码

```
 <a-col :span="5">
       <a-input v-model="queryParam.zmaktxZh"/>
       <j-input v-model="queryParam.zmaktxZh"/>
      </a-col>
```



### 4.4.2 区别

在前端组件中输入“盐酸”时，<a-input/>中的【queryParam.zmaktxZh=盐酸】；<j-input/>中的【queryParam.zmaktxZh=*盐酸*】，即<j-input/>用星号* 封装值，造成传给后端的参数为【 *值* 】，而<a-input/>传给后端的参数就是【值】本身，因此<j-input/>多了两个星号* 。

## 4.5 column横向条添加或者删除行

### 4.5.1 添加行

1）添加功能按钮；

 <a-button class="level2Button" @click="addRow" size="small" type="primary" icon="plus">{{$t('btn.add')}}</a-button>
 
 2）添加功能按钮触发函数；
 
       addRow() {
         let nitem = {
           vid: randomUUID(),
           matnr: undefined,
           zmaktxEn: undefined,
           zmaktxZh: undefined,
           werks: undefined,
           zzremark: undefined,
           zm015: undefined,
         };
         this.dataSource.push(nitem);
       },
       
 3）引用randomUUID包；
 
 import {randomUUID } from '@/utils/util'
 
 4）给每列添加相应的slot；
 
 <a-table>与</a-table>间添加插槽实现方法，实现方法不要用v-model；
 
 5）添加每行的选择框，以及行管理相关的函数与变量；
 
 6）将每一行绑定唯一的key或者rowkey值，便于管理；
 
 7）序号重新计算，如果每行有的话；

### 4.5.2 删除行

1）添加每行的选择框，以及行管理相关的函数与变量；

 （1）<a-table>中的rowSelection属性添加每行的选择框
 
 :rowSelection="{selectedRowKeys: selectedRowKeys, onChange: onSelectChange}"
 
 （2）该页面全局变量声明
 
 selectedRowKeys: [],
 
 selectedRows: [],
 
 （3）添加行管理函数onChange
 
 onSelectChange(selectedRowKeys, selectionRows) {
 
         this.selectedRowKeys = selectedRowKeys;
         
         this.selectionRows = selectionRows;
         
 },
 
 2）添加删除按钮；
 
 <a-button class="level2Button" @click="deleteRows" size="small" type="danger" icon="delete" :disabled="columns.length!=0">{{$t('btn.delete')}}</a-button>
 
 3）添加 删除触发函数deleteRows；
 
       deleteRows() {
         debugger
         if(this.selectedRowKeys && this.selectedRowKeys.length >= 1) {
           let dataSource = [];
           this.dataSource.forEach(d => {
             debugger
             const target = this.selectedRowKeys.find(id => id == (d.id || d.vid));
             if(!target) {
               dataSource.push(d);
             }
           });
           debugger
           this.dataSource = dataSource;
           this.selectedRowKeys = [];
           this.selectedRows = [];
         }
       },
       
 4）将每一行绑定唯一的key或者rowkey值，便于删除与管理
 
 用<a-table>中的rowKey属性
 
 :rowKey="r => r.id || r.vid"
 
 5）序号重新计算，如果每行有的话

## 4.6 excel导出导入功能与 表格的行添加与删除，以及插槽功能（如a-input编辑）的配合使用。

即 页面table表格原本只有excel导出和导入功能（因此只能先在excel中编辑数据后再上传），

①先实现 excel导入数据后支持在页面编辑（插槽，value="text"），避免只能在excel修改后再上传；

②再实现行add添加与delete删除功能。

### 4.6.1 表格每行插槽slot中的初始值

<template slot="input" slot-scope="text, record">
           <a-input placeholder="请输入内容" :value="text"></a-input>
 </template>
 
 （1）插槽ID：slot="input"；
 
 （2）excel导入的数值传给表格的插槽：slot-scope="text, record"
 
 （3）插槽初始值 要么是新增行时的空或新增之后的手动输入，要么是从后台获得的数值（如对导入的excel的数值的读取）：   :value="text"

### 4.6.2 功能描述

①export导出excel模板用于填写（可为template中模板，或者用页面columns列或其他字段自动生成）；

 ②import导入excel模板，用于读取所填写的数据反馈给前端；
 
 ③add添加行，delete删除行；
 
 ④import导入的数据text展示在插槽<a-input>中，实现在页面中再次编辑数据而无需再次导入，即设置初始值value="text"，而不是v-model；
 
 <template slot="input" slot-scope="text, record">
           <a-input placeholder="请输入内容" :value="text"></a-input>
 </template>

v-model双向绑定；value初始值。

 ⑤table表格的columns中使用插槽，供编辑。

## 4.7 插槽使用总结

### 4.7.1 插槽slot的参数

<template slot="input" slot-scope="text, record">
           <a-input placeholder="请输入内容" :value="text"></a-input>
 </template>

 （1）slot="input"是指插槽名称；使用了该插槽的table列均可以使用该插槽；
 
 （2）slot-scope="text, record"是指：当table中具体某行的某列插槽使用时，该插槽实例的值text，以及其所在行的值record。
 
 slot   slot-scope
 
 插槽类   插槽实例的值与行号。


### 4.7.2 对table表单下columns中的slot进行数据绑定：插槽中输入的值实时传给全局变量this.dataSource

参考教程：MMS系统——src.views.matnr.CleanRepairPartsApply.vue中的slot="slot"插槽

 <template :slot="slot" slot-scope="text, record" v-for="slot in editorCells">
       <SelectCell v-bind:key="slot" :text="text" dictCode="COMMON_FLAG" @change="handleChangeCell(record.id||record.vid, slot, $event)" @click="stopPropagation" />
 </template>
         
 （1）@change触发事件，只要里面输入的值改变，就会触发事件；
 
 （2）使用 $event参数：该参数实时获取页面数值变化，通常配置@change触发事件使用。

### 4.7.3 插槽分类以及各类的用法

1）分类：①匿名插槽；②具名插槽；③作用域插槽；

 2）参考教程：https://blog.csdn.net/xy19950125/article/details/108876237

### 4.7.4 输入功能的插槽、下拉选择框插槽、弹窗选择插槽

1）详见MMS CleanRepairPartsApply.vue页面中的插槽使用：全部是import包引入。

##   4.8 父页面与弹窗之间的传值

### 4.8.1 父页面到弹窗（五步：2、1、1、1）：  

【定义页面功能键位置，定义ref方法与回调方法；import；components；定义click触发事件】     

 //①<template>中声明弹窗，并声明去的方法： ref方法与弹窗名digMatnr。同时声明回来的方法，即回调方法：dlgMatnrOk
 
 <DlgMatnr ref="dlgMatnr" @callback="dlgMatnrOk" />
 
 //②import引入弹窗组件   
 
 import DlgMatnr from '@views/searchhelp/DlgMatnr'
 
 //③components中声明弹窗组件
 
 components: {
       DlgMatnr,
     },
     
 //④<template>中定义页面上的弹窗触发功能键
 
 <a-input-search placeholder="请选择" :value="text" enter-button @search="dlgMatnrClick(record)" @pressEnter="dlgMatnrClick(record)"/>
 
 //⑤定义弹窗触发事件dlgMatnrClick（使用this.$refs.弹窗名 的方法跳转弹窗）
 
 dlgMatnrClick(data) {
 
         console.log(data);
         
         debugger
         
         this.searchMatnr = data.vid;
         
         this.$refs.dlgMatnr.loadPage({
         
         });
         
 // 跳转至弹窗
 
 // this.$refs.dlgMatnr.loadPage({  “参数”  });
 
 },

###   4.8.2 弹窗到父页面（2步）：

//①定义跳回父页面的位置，如 ok，close，或者点x；

 <a-modal
 
   :title="title"
   
   :width="800"
   
   :visible="visible"
   
   :initdata="initdata"
   
   @ok="handleOk"
   
   @cancel="close"
   
  \>
  
 </a-modal>
 
 //②定义跳回触发事件，使用跳回方法$emit，从而触发父页面的回调方法


 handleOk () {
 
     this.backdata = this.selectionRows[0];
     
     this.$emit('callback', this.backdata);
     
     this.close();
     
    },
    
    close () {
    
     this.$emit('close');
     
     this.visible = false;
     
    },
    
 //③父页面中定义回调方法，使用弹窗的传值
 
       dlgMatnrOk(data) {
         console.log("dlgMatnrOk", data);
         debugger
         for(let step = 0; step < this.dataSource.length; step++){
           let item = this.dataSource[step];
           if(item.vid == this.searchMatnr){
             item.matnr = data.matnr;
             item.werks = data.werks;
             item.zmaktxEn = data.zmaktxEn;
             item.zmaktxZh = data.zmaktxZh;
             this.searchhelp = "";
             break;
           }
         }
       },

### 4.8.3 口诀：

ref ——> props；

emit ——> callback

### 4.8.4 vue2传值方式总结 （十二种方法）

https://blog.csdn.net/Frazier1995/article/details/116069811

## 4.9 前端开发中失去焦点和获取焦点

### 4.9.1 参考教程

https://zhidao.baidu.com/question/1834514702766274740.html

### 4.9.2 应用

插槽中 Input输入插槽的使用，使$event的值为 编辑过程中的整个值，而不是单词输入的数值，即onfocus与onblur之间的整个事件段内的输入值。

## 4.10 vue中的信息提示

### 4.10.1 语法举例

this.$message.success(res.message);

 this.$message.error(res.message);

## 4.11 init()位置

Script ——> export default  ——> methods ——> init()

 init第四层

## 4.12 <a-table>表格标签

### 4.12.1 <a-table>标签的常见属性

  <a-table
  
      ref="table"
      
      size="middle"
      
      bordered
      
      rowKey="id"
      
      :columns="tabelOneColumns"
      
      :dataSource="tableOneAreaValue"
      
      :pagination="ipagination"
      
      :loading="loading"
      
      :scroll="{y: 460 }"
      
   \>
   
   </a-table>
   
 1）rowKey属性：行标志。每行的独有标志，一般运用randomUUID()定义，用于区分各行；
 
 2）:columns属性：表格中所存在的各列，在created中定义tabelOneColumns；
 
 3）:dataSource属性：表格中各列的数据来源；
 
 4）:pagination属性：用于是否启用翻页/页码的功能。
 
   页码pageNo相关表达式：this.searchAreaParameter.pageNo = this.ipagination.current;
   
   每页大小pageSize相关表达式：this.searchAreaParameter.pageSize = this.ipagination.pageSize;
   
   总数相关表达式：this.ipagination.total = res.result.total || 0;
   
   【注意：用current获取页码】
   
 loadData(current){
 
      this.loading = true;
      
      if(current){
      
       this.ipagination.current = current;
       
      }
      
      debugger
      
      this.searchAreaParameter.pageNo = this.ipagination.current;
      
      this.searchAreaParameter.pageSize = this.ipagination.pageSize;
      
      getAction(this.url.search, this.searchAreaParameter).then(res => {
      
       console.log("搜索结果：", res);
       
       if(res.success){
       
        this.tableOneAreaValue = res.result.records;
        
        this.ipagination.total = res.result.total || 0;
        
        this.loading = false;
        
       }else{
       
        this.$message.error(res.message);
        
        this.loading = false;
        
       }
       
      })
      
     },
     
 5）:loading属性：【待明了】；
 
 6）:scroll属性：用于是否启用滑动条；

## 4.13 单个页面级loading常量的使用

### 4.13.1 使用场景

如点击search按钮时的加载开始（this.loading = true）和加载结束（this.loading = false）这段时间内的加载旋转图标。

## 4.14 直接在前端将table表格中的columns数据 生成excel文件并下载的通用方法

// filename, sheetTitle, mergeCols, columns, dataSource

 this.exportExcelWithTable('Material Report.xlsx', '', [], this.columns, res.result.records);

实例：

     exportMaterialReport() {
      var params = Object.assign({}, this.queryParam);
      params.pageNo = 1;
      params.pageSize = this.G_CONST.maxExportSize;
      this.loading = true;
      getAction(this.url.list, params).then(res => {
        console.log(this.$options.name, "loadData", res);
        if(res.success) {
         // filename, sheetTitle, mergeCols, columns, dataSource
         this.exportExcelWithTable('Material Report.xlsx', '', [], this.columns, res.result.records);
        } else {
         this.error(res.message);
        }
        this.loading = false;
      });
     },

## 4.15 前端开发文档之一

腾讯云：https://cloud.tencent.com/developer/section/1489869

## 4.16 选择框的使用

### 4.16.0 教程

https://cloud.tencent.com/developer/section/1489869

### 4.16.1 单选框

<a-radio-group></a-radio-group>

 <a-radio-group v-model="result.second.cronEvery">
  
       <a-row>
       
        <a-radio value="1">每一秒钟</a-radio>
        
       </a-row>
       
       <a-row>
       
        <a-radio value="2">每隔
        
         <a-input-number size="small" v-model="result.second.incrementIncrement" :min="1" :max="59"></a-input-number>
         
         秒执行 从
         
         <a-input-number size="small" v-model="result.second.incrementStart" :min="0" :max="59"></a-input-number>
         
         秒开始
         
        </a-radio>
        
       </a-row>
       
       <a-row>
       
        <a-radio value="3">具体秒数(可多选)</a-radio>
        
        <a-select style="width:354px;" size="small" mode="multiple" v-model="result.second.specificSpecific">
        
         <a-select-option v-for="(val,index) in 60" :key="index" :value="index">{{ index }}</a-select-option>
         
        </a-select>
        
       </a-row>
       
       <a-row>
       
        <a-radio value="4">周期从
        
         <a-input-number size="small" v-model="result.second.rangeStart" :min="1" :max="59"></a-input-number>
         
         到
         
         <a-input-number size="small" v-model="result.second.rangeEnd" :min="0" :max="59"></a-input-number>
         
         秒
         
        </a-radio>
        
       </a-row>
       
      </a-radio-group>

### 4.16.2 多选框

<a-checkgroup></a-radio-group>

         <a-checkbox-group v-model="flowInfo.nextUserList">
         
          <template v-for="(user, ind) in nextUserInfo">
          
           <a-checkbox :value="user.username">{{user.realname}}</a-checkbox>
           
          </template>
          
         </a-checkbox-group>

# 5 Java学习

## 5.1 Java注解（传输数据）

### 5.1.1 教程

https://blog.csdn.net/qq_36317994/article/details/79571605

 https://blog.csdn.net/java_xdo/article/details/88711192
 
 https://zhuanlan.zhihu.com/p/596177264

### 5.1.2 mapping

Java中的mapping归根到底就是两种请求，即：post和get。以Web为对象，按照目的的不同：

 ①get是Web请求数据，目的是后端返回前端所需的数据；
 
 ②post是Web发送数据给后端接收，目的是后端接收数据并返回处理结果；

## 5.2 SpringMVC

### 5.2.1 教程

https://zhuanlan.zhihu.com/p/100723581

 https://blog.csdn.net/qq_58168493/article/details/122634493

### 5.2.2 发展历程

原始MVC模式——WEB开发的MVC——SpringMVC

## 5.3 JDBC

### 5.3.1 教程

https://blog.csdn.net/m0_37761437/article/details/1104689441 

## 5.4 不区分大小写进行数据库oracle查询

### 5.4.1 方法一：在mapper.xml中用REGEXP_LIKE方法

  <select id="getByName" resultType="org.jeecg.modules.erp.entity.ErpHVendor">
   
     select * from ERP_H_VENDOR where REGEXP_LIKE(zname,#{name}, 'i')
     
   </select>

### 5.4.2 方法二：queryWrapper中使用UPPER()和toUpperCase()

if(StringUtils.isNotBlank(para.getZmaktxEn())) {

      queryWrapper.like("UPPER(ZMAKTX_EN)", para.getZmaktxEn().toUpperCase());
      
 };

## 5.5 entity间传值（从header到matnrPartsVo，对应关系：相同的property之间）

BeanUtils.copyProperties(header, matnrPartsVo);

## 5.6 java异步编程

### 5.6.1 教程

https://www.cnblogs.com/mikechenshare/p/16706624.html

https://www.cnblogs.com/mghio/p/15087427.html#:~:text=Java%20%E5%BC%82%E6%AD%A5%E7%BC%96%E7%A8%8B%E7%9A%84%E5%87%A0%E7%A7%8D%E6%96%B9%E5%BC%8F%201%20%E5%89%8D%E8%A8%80%20%E5%BC%82%E6%AD%A5%E7%BC%96%E7%A8%8B%E6%98%AF%E8%AE%A9%E7%A8%8B%E5%BA%8F%E5%B9%B6%E5%8F%91%E8%BF%90%E8%A1%8C%E7%9A%84%E4%B8%80%E7%A7%8D%E6%89%8B%E6%AE%B5%E3%80%82%20%E5%AE%83%E5%85%81%E8%AE%B8%E5%A4%9A%E4%B8%AA%E4%BA%8B%E6%83%85%E5%90%8C%E6%97%B6%E5%8F%91%E7%94%9F%EF%BC%8C%E5%BD%93%E7%A8%8B%E5%BA%8F%E8%B0%83%E7%94%A8%E9%9C%80%E8%A6%81%E9%95%BF%E6%97%B6%E9%97%B4%E8%BF%90%E8%A1%8C%E7%9A%84%E6%96%B9%E6%B3%95%E6%97%B6%EF%BC%8C%E5%AE%83%E4%B8%8D%E4%BC%9A%E9%98%BB%E5%A1%9E%E5%BD%93%E5%89%8D%E7%9A%84%E6%89%A7%E8%A1%8C%E6%B5%81%E7%A8%8B%EF%BC%8C%E7%A8%8B%E5%BA%8F%E5%8F%AF%E4%BB%A5%E7%BB%A7%E7%BB%AD%E8%BF%90%E8%A1%8C%EF%BC%8C%E5%BD%93%E6%96%B9%E6%B3%95%E6%89%A7%E8%A1%8C%E5%AE%8C%E6%88%90%E6%97%B6%E9%80%9A%E7%9F%A5%E7%BB%99%E4%B8%BB%E7%BA%BF%E7%A8%8B%E6%A0%B9%E6%8D%AE%E9%9C%80%E8%A6%81%E8%8E%B7%E5%8F%96%E5%85%B6%E6%89%A7%E8%A1%8C%E7%BB%93%E6%9E%9C%E6%88%96%E8%80%85%E5%A4%B1%E8%B4%A5%E5%BC%82%E5%B8%B8%E7%9A%84%E5%8E%9F%E5%9B%A0%E3%80%82%20...%202,FutureTask%20%E7%B1%BB%E6%9D%A5%E8%A1%A8%E7%A4%BA%E5%BC%82%E6%AD%A5%E8%AE%A1%E7%AE%97%E7%BB%93%E6%9E%9C%E3%80%82%20...%204%20CompletableFuture%20%E6%96%B9%E5%BC%8F%20...%20%E6%9B%B4%E5%A4%9A%E9%A1%B9%E7%9B%AE

### 5.6.2 分类（五种方法）

一、线程异步

 二、Future异步
 
 三、CompletableFuture异步
 
 四、SpringBoot @Async异步
 
 五、Guava异步

## 5.7 java中自定义class类并定义方法

参考教程
 https://blog.csdn.net/weixin_45817985/article/details/127023248?spm=1001.2101.3001.6650.6&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-6-127023248-blog-107396176.235%5Ev27%5Epc_relevant_t0_download&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-6-127023248-blog-107396176.235%5Ev27%5Epc_relevant_t0_download&utm_relevant_index=7

## 5.8 java集合框架图

作用：java.utils包下各类工具的使用

 参考教程
 
 https://blog.csdn.net/qq_43759656/article/details/107396176#:~:text=%E5%88%9B%E5%BB%BA%E9%9B%86%E5%90%88%E5%AF%B9%E8%B1%A1%E7%9A%84%E4%B8%A4%E7%A7%8D%E6%96%B9%E5%BC%8F%EF%BC%9A%201%20%E4%BD%BF%E7%94%A8list%E6%8E%A5%E5%8F%A3%20new,%E5%AE%9E%E7%8E%B0%E7%B1%BB%202%20%E4%BD%BF%E7%94%A8ArrayList%E5%A3%B0%E6%98%8E%E5%AF%B9%E8%B1%A1%EF%BC%8C%20%E6%B3%9B%E5%9E%8B%E4%BC%A0%E7%9A%84%E7%B1%BB%E5%9E%8B%E4%B8%8D%E8%83%BD%E6%98%AF%E5%9F%BA%E6%9C%AC%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B%EF%BC%8C%E5%8F%AA%E8%83%BD%E6%98%AF%E5%BC%95%E7%94%A8%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B%EF%BC%8C%E5%8D%B3%E5%8C%85%E8%A3%85%E7%B1%BB

https://blog.csdn.net/oman001/article/details/104843676
