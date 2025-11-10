# 0 官网

JeecgBoot官网：[JEECG官方网站 - 基于BPM的低代码开发平台](http://jeecg.com/)

Ant-design-vue官网：[Ant Design of Vue - Ant Design Vue (antdv.com)](https://1x.antdv.com/docs/vue/introduce-cn/)

# 1 前后端关联（服务器IP+服务器端口号+context path）

前端vue2启动后，代码中指定端口号，并利用前端服务器IP，以此生成前端登录的网址（如http://10.98.13.207:8892/）；

前端配置文件 env、vue.config.js等等五个文件中，所有URL指向后端地址（后端服务器IP➕端口号，如VUE_APP_API_BASE_URL=http://10.98.13.204:31275/cxtmatnr ）。其中/cxtmatnr用于当多个后端公用一个后端服务器端口时对后端工程的区分，后端工程中在applicaition配置文件中的server——servlet——context path中命名，同时前端五个配置文件指向后端服务器网址的地方也要加相同的命名

后端服务器端口号在application中配置（即server中的port）

# 2 下载附件或者导出数据生成excel

## 2.1 如后台template模板导出

### 2.1.1 前端URL使用

- ①配置文件中指明后端路径（后端服务器IP+端口+context path）
- ②indax.js中配置缩写
- ③vue文件中定义URL并使用

### 2.1.2 前端添加@click=downloadTemplate函数

两个参数：文件名；token（token在vue文件的export default的created中定义）；

该函数里面使用window.open函数创建新页面下载；

### 2.1.3 后端使用公共组件

后端使用  模板下载公共组件（DownloadController.java中的 “/download/template”）;

需将模板放置在templates文件中

##   2.2 将column列（或者指定字段）生成对应的excel并下载（用于填写，有时需带出数据）



# 3 上传附件（可以不是excel）（文件Nas挂载方式，弄清如何实现上传、配置文件等）

## 3.1 前端<a-upload>

### 3.1.1 `<a-upload>` 使用

```
<a-upload>自动生成导入弹窗，并在<a-upload>与</a-upload>之间形成上传功能实现区域（功能区、显示区）
 <a-upload>
   <a-button> 按钮名称</a-button>
 </a-upload>
```

### 3.1.2 `<a-upload>` 中的各个参数
- ①name：上传种类，如file、picture等；
- ②action：指向后端服务器URL，常见于读取excel内容并返回给前端；
- ③multiple：上传时是否可一次上传多个文件；
- ④accept：可接受的<name>类型；
- ⑤showUploadList：暂不确定；
- ⑥data：暂不确定；
- ⑦beforeUpload：上传前进行的触发事件；
- ⑧change：对应上传后，action中的URL返回报文；

【示例】
```
    <a-upload name="file"
            :action="url.import"
            :multiple="false"
            accept=".xlsx"
            :showUploadList="false"
            :data="importBusiData"
            :beforeUpload="handleBeforeUpload"
            @change="handleUploadChange"
    \>
        <a-button class="level2Button" size="small" type="primary" icon="import">{{$t('btn.import')}}</a-button>
    </a-upload>
```

## 3.2 后端（Nas挂载方式如何实现文件上传到文件服务器）

#   4 excel内容读取（读取excel内容填写在前端相应位置）

## 4.1 后端（url.import）

### 4.1.1 数据处理

①使用 EXCEL处理工具中的标准类读取 excel中数据：List<String[]> data = ExcelUtil.getInstance().parse(file.getOriginalFilename(), file.getInputStream())。无需自己写程序慢慢读取；

②对数据进行校验、处理；

### 4.1.2 返回报文

①后端返回给前端的是info名称的object，info结构：info{ file:{..., response, ... }, fileList: Array(1) }。

②info.file.status分为 uploading、 done、error三种：

    uploading意味着上传中，后端传回的Info报文中并没有info.file.response;
    
    done意味着上传完成，架构自动将info.file.response封装到info中，前端可获取到数据；
    
    error意味着上传失败。

## 4.2 前端（:action="url.import"；handleBeforeUpload；handleUploadChange）

handleUploadChange的入参info为架构自动封装，url.import的return Return.ok(entity)会按照状态自动封装到info中，即info.file.response
 

# 5 解决vue每次发版后要清理浏览器缓存后用户才能用最新发版内容

## 5.1 ERP示例

![img](https://github.com/DrJasonLiu666/CXT_ERP_Microservice_System/blob/main/photos/Chapter%2015%20ERP%E9%A1%B9%E7%9B%AE%E4%B9%8B%E9%83%A8%E5%88%86%E5%A4%8D%E6%9D%82%E5%8A%9F%E8%83%BD%E7%9A%84%E5%AE%9E%E7%8E%B0/1.png)

## 5.2 教程

[vue 解决每次发版后要清理浏览器缓存 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/389290842)

# 6 JeecgBoot定时任务

## 6.1 参数含义

## ![img](https://github.com/DrJasonLiu666/CXT_ERP_Microservice_System/blob/main/photos/Chapter%2015%20ERP%E9%A1%B9%E7%9B%AE%E4%B9%8B%E9%83%A8%E5%88%86%E5%A4%8D%E6%9D%82%E5%8A%9F%E8%83%BD%E7%9A%84%E5%AE%9E%E7%8E%B0/2.png)
