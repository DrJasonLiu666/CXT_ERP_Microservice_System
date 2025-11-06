# 1 v-if、v-else的用法（来源MMS）

```html
<!-- 1 v-if、v-else的用法（来源MMS） -->
<a-col :span="3">
            <a-form-model-item :label="$t('mass.form.zzzzz')" required prop="zzzzz" v-if="formInfo.zzchangetype=='01'"></a-form-model-item>
            <a-form-model-item :label="$t('mass.form.zzzzz')" v-else ></a-form-model-item>
</a-col>
```


# 2 带搜索功能的下拉框（来源MMS）

```html
<!-- 详见vue2的readMe，也可参考：https://www.cnblogs.com/liyhbk/p/14282272.html -->
<a-col :span="5">
            <!-- 下拉搜索 -->
            <a-form-item v-if="formInfo.zzchangetype=='01'" style="width: 300px">
              <j-search-select-tag
                placeholder="通过关键字搜索"
                v-model="formInfo.zzzzz"
                dict="MASS_SPECIAL_FIELD">    <!-- 用dict指定字典集，指定多个字典用逗号隔开，例：dict="sys_depart,depart_name,id" -->          
                <!-- 字典集过大时，可选用异步加载，详见vue的readMe -->
              </j-search-select-tag>
            </a-form-item>

            <!-- 使用数据字典的下拉框 -->
            <j-dict-select-tag v-model="formInfo.zzzzz" dictCode="MASS_SPECIAL_FIELD" v-if="formInfo.zzchangetype=='01'"/>
            <j-dict-select-tag v-model="formInfo.zzzzz" v-else disabled/>
</a-col>
<!-- 下拉搜索其他实现方式：MMS_Material Apply中的国家下拉框选择 -->
<a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zm003')" required prop="zm003"></a-form-model-item>
</a-col>
<a-col :span="5">
              <a-select v-model="formInfo.zm003" :showSearch="true"
                        :filter-option="filterOption" @change="loadCities"
                        :disabled="!formRights[currNodeId]||!formRights[currNodeId].sourceInfo.canEdit">
                <a-select-option v-for="country in countries" :key="country.name" :value="country.name">
                  {{ country.name }}
                </a-select-option>
              </a-select>
</a-col>
```


# 3 v-model.trim：过滤输入的空格

可参考：https://www.cnblogs.com/liyhbk/p/14282272.html

# 4 v-for中的index_key_value

可参考：[详解v-for各个参数_v-for有几个参数_年轻的猴的博客-CSDN博客](https://blog.csdn.net/qq_42388853/article/details/111168033)

```html
如：[	            【key】:【value】	                      【index】
                    {name:"朱少鹏1",gender:"男",age:"22"},  -----  0
                    {name:"朱少鹏2",gender:"男",age:"22"},  -----  1
                    {name:"朱少鹏3",gender:"男",age:"22"},  -----  2
                    ]
```


# 5 vue图标组件

可参考：[vue、vue 所有图标属性、vue Icon 所有图标属性、vue 图标所有类型属性、vue 自定义图标 Icon属性_用生命在耍帅ㅤ的博客-CSDN博客](https://blog.csdn.net/weixin_43583693/article/details/101364701)

```html
<template>
    <a-card>
        // 文字标题旁边的问号图标。悬浮于图标上时可以显示出提示文字，并实现click事件：downloadAttachmentRule。
        <template #title>
            {{ $t('attachment.name') }} <a-icon v-if="showTips"   @click="downloadAttachmentRule" :title="$t('matnr.attachrule')" type="info-circle" theme="twoTone" twoToneColor="#eb2f96" />
        </template>
    </a-card>
</template>

<script>

  export default {
    methods: {
//  	vue图标的click事件：downloadAttachmentRule
        downloadAttachmentRule() {
            window.open(this.url.template + "?token=" + this.attachInfo.token + "&fileName=" + encodeURI(this.templateName));
        },
  }
</script>

<style>
  @import "~@assets/css/style.css";
</style>
```


![img](https://github.com/DrJasonLiu666/CXT_ERP_Microservice_System/blob/main/photos/Chapter%2010%20ERP%E9%A1%B9%E7%9B%AE%E4%B9%8B%E5%89%8D%E7%AB%AF%E9%83%A8%E5%88%86%E5%8A%9F%E8%83%BD%E7%9A%84%E6%80%BB%E7%BB%93%E2%91%A0/1.png)

#  6 横向条items中的弹窗与插槽设计

## 6.1 插槽功能

## 6.1.1 横向条某行中某一栏的单栏弹窗式插槽功能示例（无图标）_MMS

![img](https://github.com/DrJasonLiu666/CXT_ERP_Microservice_System/blob/main/photos/Chapter%2010%20ERP%E9%A1%B9%E7%9B%AE%E4%B9%8B%E5%89%8D%E7%AB%AF%E9%83%A8%E5%88%86%E5%8A%9F%E8%83%BD%E7%9A%84%E6%80%BB%E7%BB%93%E2%91%A0/2.png)


## 6.1.2 横向条某行中某一栏的单栏弹窗式插槽功能示例（有图标）_WMS

![img](https://github.com/DrJasonLiu666/CXT_ERP_Microservice_System/blob/main/photos/Chapter%2010%20ERP%E9%A1%B9%E7%9B%AE%E4%B9%8B%E5%89%8D%E7%AB%AF%E9%83%A8%E5%88%86%E5%8A%9F%E8%83%BD%E7%9A%84%E6%80%BB%E7%BB%93%E2%91%A0/3.png)



## 6.1.3 横向条某行中某一栏的数控式填充框插槽功能示例_WMS

![img](https://github.com/DrJasonLiu666/CXT_ERP_Microservice_System/blob/main/photos/Chapter%2010%20ERP%E9%A1%B9%E7%9B%AE%E4%B9%8B%E5%89%8D%E7%AB%AF%E9%83%A8%E5%88%86%E5%8A%9F%E8%83%BD%E7%9A%84%E6%80%BB%E7%BB%93%E2%91%A0/4.png)



## 6.1.4 横向条某行中某一栏的无数控纯填充框插槽功能示例_WMS

![img](https://github.com/DrJasonLiu666/CXT_ERP_Microservice_System/blob/main/photos/Chapter%2010%20ERP%E9%A1%B9%E7%9B%AE%E4%B9%8B%E5%89%8D%E7%AB%AF%E9%83%A8%E5%88%86%E5%8A%9F%E8%83%BD%E7%9A%84%E6%80%BB%E7%BB%93%E2%91%A0/5.png)



## 6.1.5 横向条某行中某一栏的下拉框插槽功能示例_MMS

![img](https://github.com/DrJasonLiu666/CXT_ERP_Microservice_System/blob/main/photos/Chapter%2010%20ERP%E9%A1%B9%E7%9B%AE%E4%B9%8B%E5%89%8D%E7%AB%AF%E9%83%A8%E5%88%86%E5%8A%9F%E8%83%BD%E7%9A%84%E6%80%BB%E7%BB%93%E2%91%A0/6.png)

## 6.2 弹窗功能

### 6.2.1 横向条中add添加行时的整行弹窗功能示例_WMS

![img](https://github.com/DrJasonLiu666/CXT_ERP_Microservice_System/blob/main/photos/Chapter%2010%20ERP%E9%A1%B9%E7%9B%AE%E4%B9%8B%E5%89%8D%E7%AB%AF%E9%83%A8%E5%88%86%E5%8A%9F%E8%83%BD%E7%9A%84%E6%80%BB%E7%BB%93%E2%91%A0/7.png)

# 7 前后端传值功能

## 7.1 前端不同页面间传参

可参考：

https://blog.csdn.net/Street_Partners/article/details/84933429

https://blog.csdn.net/qq_33368846/article/details/103802140

https://blog.csdn.net/weixin_30352191/article/details/99334232

## 7.2 前后端间传参

可参考：[前后端交互之传参的几种常见方式_前后端传参方式_明成祖Judy的博客-CSDN博客](https://blog.csdn.net/wjqsm/article/details/123409550)    

# 8 页面间数据传输组件

## 8.1 $emit 【功能描述：子组件在列表中进行了选择，从而将所选列表值传给父组件】

1 实现方式（通过事件关联）：
     
     1）子组件：子组件可以利用“$emit”触发父组件的自定义事件，语法为“vm.$emit( event, […args] )”；
   
     （1）【使用位置】

```html
<!-- 表单区域  -->
     <a-modal
      centered
      :title="title"
      :width="1000"
      :visible="visible"
      @ok="handleOk"
      @cancel="handleCancel"
      :cancelText="$t('btn.close')">

<!-- style_export default中方法，关联事件selectFinished  -->
        handleOk() {
        this.dataSource2 = this.selectedRowKeys;
        console.log("data:" + this.dataSource2);
        this.$emit("selectFinished", this.dataSource2);
        this.visible = false;
      },
```



     2）父组件【关联事件selectFinished】

     （1）【使用位置】

```html
<!-- 表单区域 -->
<Select-User-Modal ref="selectUserModal" @selectFinished="selectOK"></Select-User-Modal>


<!-- style_export default中方法，关联事件selectFinished -->
selectOK(data) {
        let params = {}
        params.roleId = this.currentRoleId
        params.userIdList = []
        for (var a = 0; a < data.length; a++) {
          params.userIdList.push(data[a])
        }
        console.log(params)
        postAction(this.url.addUserRole, params).then((res) => {
          if (res.success) {
            this.loadData2()
            this.$message.success(res.message)
          } else {
            this.$message.warning(res.message)
          }
        })
      },
```


 2 实例代码：
 
 System Setting——角色管理——选择“已有用户”
 
 【代码位置】
 
 父组件：system/roleuserlist
 
 子组件：modules/SelectUserModal


 3 可详见：
 https://www.yisu.com/zixun/690986.html#:~:text=vue%E4%B8%AD%20%E5%85%B3%E4%BA%8E%24emit%E7%9A%84%E7%94%A8%E6%B3%95%201%E3%80%81%E7%88%B6%E7%BB%84%E4%BB%B6%E5%8F%AF%E4%BB%A5%E4%BD%BF%E7%94%A8%20props,%E6%8A%8A%E6%95%B0%E6%8D%AE%E4%BC%A0%E7%BB%99%E5%AD%90%E7%BB%84%E4%BB%B6%E3%80%82%202%E3%80%81%E5%AD%90%E7%BB%84%E4%BB%B6%E5%8F%AF%E4%BB%A5%E4%BD%BF%E7%94%A8%20%24emit%20%E8%A7%A6%E5%8F%91%E7%88%B6%E7%BB%84%E4%BB%B6%E7%9A%84%E8%87%AA%E5%AE%9A%E4%B9%89%E4%BA%8B%E4%BB%B6%E3%80%82

## 8.2 ref（vue2中使用ref来调用子组件的方式）

1 功能描述：参数从父组件传往子组件，使子组件利用该参数进行搜索；子组件搜索结果传回父组件相应位置，甚至子组件的数据修改也传回父组件；

2 实现描述：

​    1）①ref父组件调用子组件；②componet申明组件；③$refs使用组件中的方法。

​    2）①import：import组件所在文件，如DlgLgort组件（所在文件命名为DlgLgort，该组件命名是在文件DlgLgort的name处命名为DlgLgort）；②component： component中声明组件，必须用组件原名；③template中使用<组件名称/>：类似于声明，声明ref（此处可将组件重命名，如ref="dlgLgort"）以及@callback（子组件参数回写到父组件）；④methods： methods中用this.$refs.组件名.组件方法 ，实现对组件方法的调用；⑤参数回传父组件：data

3 可详见：①https://blog.csdn.net/qq_41619796/article/details/114291319
      
      ②https://blog.csdn.net/wuyan1001/article/details/82220479

## 8.3 v-model（双向数据绑定）

可参考：[vue自定义组件，v-model完美使用方式_vue中v-model怎么用_iamlujingtao的博客-CSDN博客](https://blog.csdn.net/iamlujingtao/article/details/103929372)

# 9 表单中required必填实现

```html
表单a-form-mode要有rules才有效：
1【格式】
a-form-mode
    rules
        required
            prop
rules{
    prop（定义验证方式，以及反馈信息）
}
2【属性】
可以添加validator进行验证，具体如链接：
https://blog.csdn.net/weixin_44015555/article/details/116148216
3【功能描述】
强制要求输入、反馈错误信息、验证输入内容是否符合标准
```


# 10 vue前端中某vue文件引用其他vue文件的template，二者形成在同一个页面时，用prop传值

1 可参考：[Vue中props用法和传值问题_vue props_xx小黄人的博客-CSDN博客](https://blog.csdn.net/VegetableKCCCC/article/details/119410145)

2 引入文件matnrApply

```html
<template>
  <!-- 查询区域 -->
  <a-spin :tip="$t('message.processing')" :spinning="loading">
    <a-form-model
          layout="horizontal"
          ref="formRef"
          :rules="rules"
          :model="formInfo"
        >
      <div class="table-page-search-wrapper table-page-customer-search-wrapper">
        <a-card :title="$t('matnr.form.applyInfo')">
          <a-row :gutter="24">
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zzuserid')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input-group compact>
                <a-input v-model="formInfo.zzuserid" style="width:40%" disabled />
                <a-input v-model="formInfo.zzusername" style="width:60%" disabled />
              </a-input-group>
            </a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zzorgid')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input-group compact>
                <a-input v-model="formInfo.zzorgid" style="width:40%" disabled />
                <a-input v-model="formInfo.zzorgname" style="width:60%" disabled />
              </a-input-group>
            </a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zzbpmno')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input v-model="formInfo.zzbpmno" disabled />
            </a-col>
          </a-row>
          <a-row :gutter="24">
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.matnr')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input v-model="formInfo.matnr" disabled />
            </a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zzcretedate')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input v-model="formInfo.zzcretedate" disabled />
            </a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.kostl')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input-group compact>
                <a-input v-model="formInfo.kostl" style="width:40%" disabled />
                <a-input v-model="formInfo.kostlname" style="width:60%" disabled />
              </a-input-group>
            </a-col>
          </a-row>
          <a-row :gutter="24">
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.werks')" required prop="werks"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <j-dict-select-tag v-model="formInfo.werks" dictCode="WERKS" :disabled="!formRights[currNodeId]||!formRights[currNodeId].applyInfo.canEdit" />
            </a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zzpirun')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-checkbox v-model="formInfo.zzpirunChk" :disabled="!formRights[currNodeId]||!formRights[currNodeId].applyInfo.canEdit" />
            </a-col>
          </a-row>
          <a-row :gutter="24">
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zzpurpose')" required prop="zzpurpose"></a-form-model-item>
            </a-col>
            <a-col :span="21">
              <a-textarea v-model="formInfo.zzpurpose" :autoSize="{minRows:2}" :disabled="!formRights[currNodeId]||!formRights[currNodeId].applyInfo.canEdit" />
            </a-col>
          </a-row>
        </a-card>

        <a-card :title="$t('matnr.form.sourceInfo')" style="margin-top:10px;">
          <a-row :gutter="24">
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zz1stsc')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-checkbox v-model="formInfo.zz1stscChk" @change="val=>{if(formInfo.zz1stscChk){formInfo.zm012=undefined;formInfo.zm013=undefined;}}" :disabled="!formRights[currNodeId]||!formRights[currNodeId].sourceInfo.canEdit" />
            </a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zm001')" required prop="zm001"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input v-model="formInfo.zm001" :disabled="!formRights[currNodeId]||!formRights[currNodeId].sourceInfo.canEdit" />
            </a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zm002')" required prop="zm002"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input v-model="formInfo.zm002" :disabled="!formRights[currNodeId]||!formRights[currNodeId].sourceInfo.canEdit" />
            </a-col>
          </a-row>
          <a-row :gutter="24">
            <a-col :span="3">
              <a-form-model-item v-if="!formInfo.zz1stscChk" :label="$t('matnr.form.zm012')" required prop="zm012"></a-form-model-item>
              <a-form-model-item v-if="formInfo.zz1stscChk" :label="$t('matnr.form.zm012')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input-search v-if="!formInfo.zz1stscChk" v-model="formInfo.zm012" enter-button @search="dlgMatnrClick" @pressEnter="dlgMatnrClick" :disabled="!formRights[currNodeId]||!formRights[currNodeId].sourceInfo.canEdit" />
              <a-input v-if="formInfo.zz1stscChk" v-model="formInfo.zm012" disabled />
            </a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zm021')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input v-model="formInfo.zm021" :disabled="!formRights[currNodeId]||!formRights[currNodeId].sourceInfo.canEdit" />
            </a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zm025')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input v-model="formInfo.zm025" :disabled="!formRights[currNodeId]||!formRights[currNodeId].sourceInfo.canEdit" />
            </a-col>
          </a-row>
          <a-row :gutter="24">
            <a-col :span="3">
              <a-form-model-item v-if="!formInfo.zz1stscChk" :label="$t('matnr.form.zm013')" required prop="zm013"></a-form-model-item>
              <a-form-model-item v-if="formInfo.zz1stscChk" :label="$t('matnr.form.zm013')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input v-if="!formInfo.zz1stscChk" v-model="formInfo.zm013" :disabled="!formRights[currNodeId]||!formRights[currNodeId].sourceInfo.canEdit" />
              <a-input v-if="formInfo.zz1stscChk" v-model="formInfo.zm013" disabled />
            </a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zm023')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input v-model="formInfo.zm023" :disabled="!formRights[currNodeId]||!formRights[currNodeId].sourceInfo.canEdit" />
            </a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zm027')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input v-model="formInfo.zm027" :disabled="!formRights[currNodeId]||!formRights[currNodeId].sourceInfo.canEdit" />
            </a-col>
          </a-row>
          <a-row :gutter="24">
            <a-col :span="8"></a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zm022')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input v-model="formInfo.zm022" :disabled="!formRights[currNodeId]||!formRights[currNodeId].sourceInfo.canEdit" />
            </a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zm026')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input v-model="formInfo.zm026" :disabled="!formRights[currNodeId]||!formRights[currNodeId].sourceInfo.canEdit" />
            </a-col>
          </a-row>
          <a-row :gutter="24">
            <a-col :span="8"></a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zm003')" required prop="zm003"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-select v-model="formInfo.zm003" :showSearch="true"
                        :filter-option="filterOption" @change="loadCities"
                        :disabled="!formRights[currNodeId]||!formRights[currNodeId].sourceInfo.canEdit">
                <a-select-option v-for="country in countries" :key="country.name" :value="country.name">
                  {{ country.name }}
                </a-select-option>
              </a-select>
            </a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zzagadr')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input v-model="formInfo.zzagadr" :disabled="!formRights[currNodeId]||!formRights[currNodeId].sourceInfo.canEdit" />
            </a-col>
          </a-row>
          <a-row :gutter="24">
            <a-col :span="8"></a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zm020')" required prop="zm020"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-select v-model="formInfo.zm020" :showSearch="true"
                        :filter-option="filterOption"
                        :disabled="!formRights[currNodeId]||!formRights[currNodeId].sourceInfo.canEdit">
                <a-select-option v-for="city in cities" :key="city.name" :value="city.name">
                  {{ city.name }}
                </a-select-option>
              </a-select>
            </a-col>
          </a-row>
          <a-row :gutter="24">
            <a-col :span="8"></a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zzmkadr')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input v-model="formInfo.zzmkadr" :disabled="!formRights[currNodeId]||!formRights[currNodeId].sourceInfo.canEdit" />
            </a-col>
          </a-row>
        </a-card>

        <a-card :title="$t('matnr.form.basicView')" style="margin-top:10px;">
          <a-row :gutter="24">
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.mtart')" required prop="mtart"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <j-dict-select-tag v-model="formInfo.mtart" dictCode="MATERIAL_TYPE"
                                 :triggerChange="true" @change="val=>{formInfo.mtart=val;formInfo.matkl=undefined;formInfo.wgbez=undefined;}"
                                 :disabled="!(formRights[currNodeId]&&formRights[currNodeId].basicView)&&(formRights[currNodeId].basicView.canEdit||(formRights[currNodeId].basicView.editable&&formRights[currNodeId].basicView.editable.includes('mtart')))" />
            </a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.matkl')" required prop="matkl"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input-search v-model="formInfo.matkl" enter-button @search="dlgMatklClick" @pressEnter="dlgMatklClick"
                              :disabled="!(formRights[currNodeId]&&formRights[currNodeId].basicView)&&(formRights[currNodeId].basicView.canEdit||(formRights[currNodeId].basicView.editable&&formRights[currNodeId].basicView.editable.includes('matkl')))" />
            </a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.wgbez')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input v-model="formInfo.wgbez" disabled />
            </a-col>
          </a-row>
          <a-row :gutter="24">
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zmaktxEn')" required prop="zmaktxEn"></a-form-model-item>
            </a-col>
            <a-col :span="9">
              <a-input v-model="formInfo.zmaktxEn" :placeholder="$t('placeholder.maxLength', {length:40})" :maxLength='40' :disabled="!formRights[currNodeId]||!formRights[currNodeId].basicView.canEdit" />
            </a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zmaktxZh')" required prop="zmaktxZh"></a-form-model-item>
            </a-col>
            <a-col :span="9">
              <a-input v-model="formInfo.zmaktxZh" :placeholder="$t('placeholder.maxLength', {length:40})" :maxLength='40' :disabled="!formRights[currNodeId]||!formRights[currNodeId].basicView.canEdit" />
            </a-col>
          </a-row>
          <a-row :gutter="24">
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zmaktxLong')"></a-form-model-item>
            </a-col>
            <a-col :span="21">
              <a-input v-model="formInfo.zmaktxLong" :disabled="!formRights[currNodeId]||!formRights[currNodeId].basicView.canEdit" />
            </a-col>
          </a-row>
          <!-- <a-row :gutter="24">
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zzmaktxTaxen')"></a-form-model-item>
            </a-col>
            <a-col :span="9">
              <a-input v-model="formInfo.zzmaktxTaxen" :disabled="!formRights[currNodeId]||!formRights[currNodeId].basicView.canEdit" />
            </a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zzmaktxTaxzh')"></a-form-model-item>
            </a-col>
            <a-col :span="9">
              <a-input v-model="formInfo.zzmaktxTaxzh" :disabled="!formRights[currNodeId]||!formRights[currNodeId].basicView.canEdit" />
            </a-col>
          </a-row> -->
          <!--<a-row :gutter="24">
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zzaffect')" required prop="zzaffect"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <j-dict-select-tag v-model="formInfo.zzaffect" dictCode="COMMON_FLAG" :disabled="!formRights[currNodeId]||!formRights[currNodeId].basicView.canEdit" />
            </a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zzaffecttlist')"></a-form-model-item>
            </a-col>
            <a-col :span="13">
              <a-input v-model="formInfo.zzaffecttlist" :disabled="!formRights[currNodeId]||!formRights[currNodeId].basicView.canEdit" />
            </a-col>
          </a-row>-->
          <a-row :gutter="24">
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.meins')" required prop="meins"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <j-dict-select-tag v-model="formInfo.meins" dictCode="MEINS"
                                 :triggerChange="true" @change="val=>{formInfo.meins=val;zzcorateCalculator()}"
                                 :disabled="!formRights[currNodeId]||!formRights[currNodeId].basicView.canEdit" />
            </a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.meinh')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <j-dict-select-tag v-model="formInfo.meinh" dictCode="MEINS"
                                 :triggerChange="true" @change="val=>{formInfo.meinh=val;zzcorateCalculator()}"
                                 :disabled="!formRights[currNodeId]||!formRights[currNodeId].basicView.canEdit" />
            </a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zzdirate')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input v-model="formInfo.zzdirate" :disabled="!formRights[currNodeId]||!formRights[currNodeId].basicView.canEdit" />
            </a-col>
          </a-row>
          <a-row :gutter="24">
            <a-col :span="3">
              <a-form-model-item v-if="formInfo.meinh" :label="$t('matnr.form.umrez')" required prop="umrez"></a-form-model-item>
              <a-form-model-item v-else :label="$t('matnr.form.umrez')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input-number v-model="formInfo.umrez" :precision="0" :max="99999" @change="zzcorateCalculator" style="width:100%" :disabled="!formRights[currNodeId]||!formRights[currNodeId].basicView.canEdit" />
            </a-col>
            <a-col :span="3">
              <a-form-model-item v-if="formInfo.meinh" :label="$t('matnr.form.umren')" required prop="umren"></a-form-model-item>
              <a-form-model-item v-else :label="$t('matnr.form.umren')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input-number v-model="formInfo.umren" :precision="0" :max="99999" @change="zzcorateCalculator" style="width:100%" :disabled="!formRights[currNodeId]||!formRights[currNodeId].basicView.canEdit" />
            </a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zzcorate')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input v-model="formInfo.zzcorate" disabled />
            </a-col>
          </a-row>
          <a-row :gutter="24">
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.bismt')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input v-model="formInfo.bismt" :disabled="!formRights[currNodeId]||!formRights[currNodeId].basicView.canEdit" />
            </a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zm009')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input v-model="formInfo.zm009" :disabled="!formRights[currNodeId]||!formRights[currNodeId].basicView.canEdit" />
            </a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zm024')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input v-model="formInfo.zm024" :disabled="!formRights[currNodeId]||!formRights[currNodeId].basicView.canEdit" />
            </a-col>
          </a-row>
          <a-row :gutter="24">
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.mhdhb')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <!-- <a-input-number v-model="formInfo.mhdhb" :precision="0" :min="0" :max="9999" style="width:100%" :disabled="!formRights[currNodeId]||!formRights[currNodeId].basicView.canEdit" /> -->
              <a-input v-model="formInfo.mhdhb" :maxLength="75" style="width:100%" :disabled="!formRights[currNodeId]||!formRights[currNodeId].basicView.canEdit" />
            </a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.mhdrz')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <!-- <a-input-number v-model="formInfo.mhdrz" :precision="0" :min="0" :max="9999" style="width:100%" :disabled="!formRights[currNodeId]||!formRights[currNodeId].basicView.canEdit" /> -->
              <a-input v-model="formInfo.mhdrz" :maxLength="75" style="width:100%" :disabled="!formRights[currNodeId]||!formRights[currNodeId].basicView.canEdit" />
            </a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zm008')" required prop="zm008"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input v-model="formInfo.zm008" :disabled="!formRights[currNodeId]||!formRights[currNodeId].basicView.canEdit" />
            </a-col>
          </a-row>
          <a-row :gutter="24">
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zm028')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input v-model="formInfo.zm028" :disabled="!formRights[currNodeId]||!formRights[currNodeId].basicView.canEdit" />
            </a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zm029')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input v-model="formInfo.zm029" :disabled="!formRights[currNodeId]||!formRights[currNodeId].basicView.canEdit" />
            </a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zztypack')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input v-model="formInfo.zztypack" :disabled="!formRights[currNodeId]||!formRights[currNodeId].basicView.canEdit" />
            </a-col>
          </a-row>
          <a-row :gutter="24">
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zzecn')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input v-model="formInfo.zzecn" :disabled="!formRights[currNodeId]||!formRights[currNodeId].basicView.canEdit" />
            </a-col>
            <a-col :span="3">
            </a-col>
            <a-col :span="5">
            </a-col>
            <a-col :span="3">
            </a-col>
            <a-col :span="5">
            </a-col>
          </a-row>
        </a-card>

        <a-card :title="$t('matnr.form.mqeInfo')" style="margin-top:10px;" v-if="formRights[currNodeId]&&formRights[currNodeId].mqeInfo">
          <a-row :gutter="24">
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zm015')" required prop="zm015"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <j-dict-select-tag v-model="formInfo.zm015" dictCode="INSPECT_PERSON" 
                :triggerChange="true" @change="val=>{formInfo.zm015=val;isHUser=(val=='HXXXXXX');
                formInfo.insPerson=formInfo.zzuserid;formInfo.insPersonName=formInfo.zzusername;}"
                :disabled="!formRights[currNodeId]||!formRights[currNodeId].mqeInfo.canEdit" />
            </a-col>

            <a-col :span="3" v-if="isHUser">
               <a-form-model-item :label="$t('matnr.form.insPerson')"></a-form-model-item>
             </a-col>
             <a-col :span="5" v-if="isHUser">
              <a-input-group compact>
                <a-input v-model="formInfo.insPerson" style="width:40%" disabled />
                <a-input-search v-model="formInfo.insPersonName" style="width:60%" readOnly enter-button @search="() => $refs.selectUserModal.visible=true" />
              </a-input-group>
             </a-col>
            <!-- <a-col :span="3"> 
               <a-form-model-item :label="$t('matnr.form.zzrohs')"></a-form-model-item>
             </a-col>
             <a-col :span="5">
               <j-dict-select-tag v-model="formInfo.zzrohs" dictCode="COMMON_FLAG" :disabled="!formRights[currNodeId]||!formRights[currNodeId].mqeInfo.canEdit" />
             </a-col>-->
            <!--<a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zzfecp')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input v-model="formInfo.zzfecp" :disabled="!formRights[currNodeId]||!formRights[currNodeId].mqeInfo.canEdit" />
            </a-col>-->
            <!--</a-row>
            <a-row :gutter="24">
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zzecn')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input v-model="formInfo.zzecn" :disabled="!formRights[currNodeId]||!formRights[currNodeId].mqeInfo.canEdit" />
            </a-col>-->
          </a-row>
        </a-card>

        <a-card :title="$t('matnr.form.mrpInfo')" style="margin-top:10px;" v-if="formRights[currNodeId]&&formRights[currNodeId].mrpInfo">
          <a-row :gutter="24">
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.xchpf')" required prop="xchpf"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <j-dict-select-tag v-model="formInfo.xchpf" dictCode="COMMON_FLAG" :disabled="!formRights[currNodeId]||!formRights[currNodeId].mrpInfo.canEdit" />
            </a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.dismm')" required prop="dismm"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <j-dict-select-tag v-model="formInfo.dismm" dictCode="MRP_TYPE" :disabled="!formRights[currNodeId]||!formRights[currNodeId].mrpInfo.canEdit" />
            </a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.dispo')" required prop="dispo"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <j-dict-select-tag v-model="formInfo.dispo" dictCode="DISPO" :disabled="!formRights[currNodeId]||!formRights[currNodeId].mrpInfo.canEdit" />
            </a-col>
          </a-row>
          <a-row :gutter="24">
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.minbe')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input-number v-model="formInfo.minbe" :precision="3" :max="9999999999.999" style="width:100%" :disabled="!formRights[currNodeId]||!formRights[currNodeId].mrpInfo.canEdit" />
            </a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.eisbe')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input-number v-model="formInfo.eisbe" :precision="3" :max="9999999999.999" style="width:100%" :disabled="!formRights[currNodeId]||!formRights[currNodeId].mrpInfo.canEdit" />
            </a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.disls')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <j-dict-select-tag v-model="formInfo.disls" dictCode="DISLS" :disabled="!formRights[currNodeId]||!formRights[currNodeId].mrpInfo.canEdit" />
            </a-col>
          </a-row>
          <a-row :gutter="24">
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zm019')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input v-model="formInfo.zm019" :disabled="!formRights[currNodeId]||!formRights[currNodeId].mrpInfo.canEdit" />
            </a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.mtvfp')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <j-dict-select-tag v-model="formInfo.mtvfp" dictCode="MTVFP" :disabled="!formRights[currNodeId]||!formRights[currNodeId].mrpInfo.canEdit" />
            </a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.bstfe')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input-number v-model="formInfo.bstfe" :precision="3" :max="999999999.999" style="width:100%" :disabled="!formRights[currNodeId]||!formRights[currNodeId].mrpInfo.canEdit" />
            </a-col>
          </a-row>
        </a-card>

        <a-card :title="$t('matnr.form.eshInfo')" style="margin-top:10px;" v-if="formRights[currNodeId]&&formRights[currNodeId].eshInfo">
          <a-row :gutter="24">
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zm006')" required prop="zm006"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <j-dict-select-tag v-model="formInfo.zm006" dictCode="HAZARDOUS_TYPE" :disabled="!formRights[currNodeId]||!formRights[currNodeId].eshInfo.canEdit" />
            </a-col>
          </a-row>
        </a-card>

        <a-card :title="$t('matnr.form.purInfo')" style="margin-top:10px;" v-if="formRights[currNodeId]&&formRights[currNodeId].purInfo">
          <a-row :gutter="24">
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.ekgrp')" required prop="ekgrp"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input-search v-model="formInfo.ekgrp"  enter-button @search="dlgEkgrpClick" :disabled="!formRights[currNodeId]||!formRights[currNodeId].purInfo.canEdit" />
            </a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zm004')" required prop="zm004"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input-number v-model="formInfo.zm004" :precision="3" :min="0" :max="9999999999.999" style="width:100%" :disabled="!formRights[currNodeId]||!formRights[currNodeId].purInfo.canEdit" />
            </a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zm005')" required prop="zm005"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <j-dict-select-tag v-model="formInfo.zm005" dictCode="CURRENCY"
                                 :triggerChange="true"
                                 @change="currencyChange"
                                 :disabled="!formRights[currNodeId]||!formRights[currNodeId].purInfo.canEdit" />
            </a-col>
          </a-row>
          <a-row :gutter="24">
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.bstme')" required prop="bstme"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <j-dict-select-tag v-model="formInfo.bstme" dictCode="MEINS"
                                 :triggerChange="true" @change="val=>{formInfo.bstme=val;zzcorateCalculator()}"
                                 :disabled="!formRights[currNodeId]||!formRights[currNodeId].purInfo.canEdit" />
            </a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zzcoratePur')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input v-model="formInfo.zzcoratePur" disabled />
            </a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.bstmi')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input-number v-model="formInfo.bstmi" :precision="3" :max="9999999999.999" style="width:100%" :disabled="!formRights[currNodeId]||!formRights[currNodeId].purInfo.canEdit" />
            </a-col>
          </a-row>
          <a-row :gutter="24">
            <a-col :span="3">
              <a-form-model-item v-if="formInfo.meins==formInfo.zzmeins" :label="$t('matnr.form.zumrez')"></a-form-model-item>
              <a-form-model-item else :label="$t('matnr.form.zumrez')" required prop="zumrez"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input-number v-model="formInfo.zumrez" :precision="0" :max="99999" @change="zzcorateCalculator" style="width:100%" :disabled="!formRights[currNodeId]||!formRights[currNodeId].purInfo.canEdit" />
            </a-col>
            <a-col :span="3">
              <a-form-model-item v-if="formInfo.meins==formInfo.zzmeins" :label="$t('matnr.form.zumren')"></a-form-model-item>
              <a-form-model-item else :label="$t('matnr.form.zumren')" required prop="zumren"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input-number v-model="formInfo.zumren" :precision="0" :max="99999" @change="zzcorateCalculator" style="width:100%" :disabled="!formRights[currNodeId]||!formRights[currNodeId].purInfo.canEdit" />
            </a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.bstrf')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input-number v-model="formInfo.bstrf" :precision="3" :max="9999999999.999" style="width:100%" :disabled="!formRights[currNodeId]||!formRights[currNodeId].purInfo.canEdit" />
            </a-col>
          </a-row>
          <a-row :gutter="24">
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zpurtype')" required prop="zpurtype"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <j-dict-select-tag v-model="formInfo.zpurtype" dictCode="PUR_TYPE" :disabled="!formRights[currNodeId]||!formRights[currNodeId].purInfo.canEdit" />
            </a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.plifz')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input-number v-model="formInfo.plifz" :precision="0" :max="999" style="width:100%" :disabled="!formRights[currNodeId]||!formRights[currNodeId].purInfo.canEdit" />
            </a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zzcapacity')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input v-model="formInfo.zzcapacity" :disabled="!formRights[currNodeId]||!formRights[currNodeId].purInfo.canEdit" />
            </a-col>
          </a-row>
          <a-row :gutter="24">
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zzrepack')" required prop="zzrepack"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <j-dict-select-tag v-model="formInfo.zzrepack" dictCode="COMMON_FLAG" :disabled="!formRights[currNodeId]||!formRights[currNodeId].purInfo.canEdit" />
            </a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zzrescrap')" required prop="zzrescrap"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <j-dict-select-tag v-model="formInfo.zzrescrap" dictCode="COMMON_FLAG" :disabled="!formRights[currNodeId]||!formRights[currNodeId].purInfo.canEdit" />
            </a-col>
          </a-row>
        </a-card>

        <a-card :title="$t('matnr.form.legalInfo')" style="margin-top:10px;" v-if="formRights[currNodeId]&&formRights[currNodeId].legalInfo">
          <a-row :gutter="24">
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zm007')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-checkbox v-model="formInfo.zm007Chk" :disabled="!formRights[currNodeId]||!formRights[currNodeId].legalInfo.canEdit" />
            </a-col>
          </a-row>
        </a-card>

        <a-card :title="$t('matnr.form.whInfo')" style="margin-top:10px;" v-if="formRights[currNodeId]&&formRights[currNodeId].whInfo">
          <a-row :gutter="24">
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.lgfsb')" required prop="lgfsb"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input-search v-model="formInfo.lgfsb" enter-button @search="dlgLgortClick" :disabled="!formRights[currNodeId]||!formRights[currNodeId].whInfo.canEdit" />
            </a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.lgpro')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input v-model="formInfo.lgpro" />
            </a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.webaz')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input-number v-model="formInfo.webaz" :precision="0" :max="999" style="width:100%" :disabled="!formRights[currNodeId]||!formRights[currNodeId].whInfo.canEdit" />
            </a-col>
          </a-row>
        </a-card>

        <a-card :title="$t('matnr.form.ficoInfo')" style="margin-top:10px;" v-if="formInfo.mtart!='Z040'&&formRights[currNodeId]&&formRights[currNodeId].ficoInfo">
          <a-row :gutter="24">
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.bklas')" required prop="bklas"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <j-dict-select-tag v-model="formInfo.bklas" dictCode="VALUATION_CLASS" :disabled="!formRights[currNodeId]||!formRights[currNodeId].ficoInfo.canEdit" />
            </a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.eklas')" required prop="eklas"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <j-dict-select-tag v-model="formInfo.eklas" dictCode="SALE_ORD_STK" :disabled="!formRights[currNodeId]||!formRights[currNodeId].ficoInfo.canEdit" />
            </a-col>
          </a-row>
          <a-row :gutter="24">
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zplp1')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input v-model="formInfo.zplp1" :disabled="!formRights[currNodeId]||!formRights[currNodeId].ficoInfo.canEdit" />
            </a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zpld1')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-date-picker v-model="formInfo.zpld1" :format="G_CONST.dateFormat.YYYYMMDD" style="width:100%" :disabled="!formRights[currNodeId]||!formRights[currNodeId].ficoInfo.canEdit" />
            </a-col>
            <a-col :span="3">
              <a-form-model-item :label="$t('matnr.form.zzexchange')"></a-form-model-item>
            </a-col>
            <a-col :span="5">
              <a-input v-model="formInfo.zzexchange" disabled />
            </a-col>
          </a-row>
        </a-card>
      </div>
    </a-form-model>
    <br/>
    <!-- finished=附件上传完成后都会回调该方法 -->
	
	// 引用attachment页面展示部分， 冒号用于传值：formInfo、bpmType、filetype、showTips、attachment。showTips直接复制boolen型  一个回调事件finished
    <Attachment :formInfo="formInfo" :bpmType="bpmType" filetype="MMS_FILETYPE" :showTips="true" :view="G_CONST.actionType.view==actionType" @finished="handleAttachmentFinished" />
    <!-- save=保存数据，validate=表单数据验证方法(验证通过后回调 callback), submit=保存并提交数据, back=流程退回, close=关闭当前 tab页 -->
    <br/>
    <BpmApproval ref="bpmApprovalRef"
                 :formInfo="formInfo"
                 :nextNodeUrl="url.nextNodeUrl"
                 @receive="handleApprovalReceive"
                 @validate="validateForm"
                 @save="handleSave"
                 @submit="handleSubmit"
                 @back="handleBpmBack"
                 @delete="handleDeleteProcess"
                 @close="closeCurrent" />

    <DlgMatnr ref="dlgMatnr" @callback="dlgMatnrOk" />
    <DlgMatkl ref="dlgMatkl" @callback="dlgMatklOk" />
    <DlgEkgrp ref="dlgEkgrp" @callback="dlgEkgrpOk" />
    <DlgLgort ref="dlgLgort" @callback="dlgLgortOk" />

    <SelectUserModal ref="selectUserModal" @selectFinished="handleSelectUser" />
  </a-spin>
</template>

<script>
    import {getAction, postAction} from '@/api/manage'
    import moment from 'moment'
    import { Common } from '@/utils/common.js'
    import { Matnr } from '@/utils/matnr.js'
    import DlgMatnr from '@views/searchhelp/DlgMatnr'
    import DlgMatkl from '@views/searchhelp/DlgMatkl'
    import DlgEkgrp from '@views/searchhelp/DlgEkgrp'
    import DlgLgort from '@views/searchhelp/DlgLgort'
    import SelectUserModal from '@views/system/modules/SelectUserModal'

    import BpmApproval from '@views/bpm/BpmApproval'
    import Attachment from '@views/bpm/Attachment'

    export default {
        name: "MatnrApply",
        mixins: [ Common, Matnr ],
        components: {
            DlgMatnr,
            DlgMatkl,
            DlgEkgrp,
            DlgLgort,
            SelectUserModal,
            BpmApproval,
            Attachment,
        },
        data() {
            return {
                description: 'Matnr APPLY',
				// export default_data_return 中初始化bpmType
                bpmType: "PROC_MMS_MATERIAL",
                actionType: undefined,
                isHUser: false,
                rules: {
                    zzpurpose: [{ required: true, message: this.$t('message.required', {label:this.$t('matnr.form.zzpurpose')})}],
                    zm001: [{ required: true, message: this.$t('message.required', {label:this.$t('matnr.form.zm001')})}],
                    zm013: [{ required: true, message: this.$t('message.required', {label:this.$t('matnr.form.zm013')})}],
                    zm003: [{ required: true, message: this.$t('message.required', {label:this.$t('matnr.form.zm003')})}],
                    zm020: [{ required: true, message: this.$t('message.required', {label:this.$t('matnr.form.zm020')})}],
                    mtart: [{ required: true, message: this.$t('message.required', {label:this.$t('matnr.form.mtart')})}],
                    matkl: [{ required: true, message: this.$t('message.required', {label:this.$t('matnr.form.matkl')})}],
                    zmaktxEn: [{ required: true, message: this.$t('message.required', {label:this.$t('matnr.form.zmaktxEn')})}],
                    zmaktxZh: [{ required: true, message: this.$t('message.required', {label:this.$t('matnr.form.zmaktxZh')})}],
                    zzaffect: [{ required: true, message: this.$t('message.required', {label:this.$t('matnr.form.zzaffect')})}],
                    meins: [{ required: true, message: this.$t('message.required', {label:this.$t('matnr.form.meins')})}],
                    zm015: [{ required: true, message: this.$t('message.required', {label:this.$t('matnr.form.zm015')})}],
                    xchpf: [{ required: true, message: this.$t('message.required', {label:this.$t('matnr.form.xchpf')})}],
                    dismm: [{ required: true, message: this.$t('message.required', {label:this.$t('matnr.form.dismm')})}],
                    dispo: [{ required: true, message: this.$t('message.required', {label:this.$t('matnr.form.dispo')})}],
                    zm006: [{ required: true, message: this.$t('message.required', {label:this.$t('matnr.form.zm006')})}],
                    ekgrp: [{ required: true, message: this.$t('message.required', {label:this.$t('matnr.form.ekgrp')})}],
                    zm004: [{ required: true, message: this.$t('message.required', {label:this.$t('matnr.form.zm004')})}],
                    zm005: [{ required: true, message: this.$t('message.required', {label:this.$t('matnr.form.zm005')})}],
                    bstme: [{ required: true, message: this.$t('message.required', {label:this.$t('matnr.form.bstme')})}],
                    zpurtype: [{ required: true, message: this.$t('message.required', {label:this.$t('matnr.form.zpurtype')})}],
                    lgfsb: [{ required: true, message: this.$t('message.required', {label:this.$t('matnr.form.lgfsb')})}],
                    bklas: [{ required: true, message: this.$t('message.required', {label:this.$t('matnr.form.bklas')})}],
                    werks: [{ required: true, message: this.$t('message.required', {label:this.$t('matnr.form.werks')})}],
                    umrez: [{ required: true, message: this.$t('message.required', {label:this.$t('matnr.form.umrez')})}],
                    umren: [{ required: true, message: this.$t('message.required', {label:this.$t('matnr.form.umren')})}],
                    zumren: [{ required: true, message: this.$t('message.required', {label:this.$t('matnr.form.zumren')})}],
                    zumrez: [{ required: true, message: this.$t('message.required', {label:this.$t('matnr.form.zumrez')})}],
                    zm002: [{ required: true, message: this.$t('message.required', {label:this.$t('matnr.form.zm002')})}],
                    zzrepack: [{ required: true, message: this.$t('message.required', {label:this.$t('matnr.form.zzrepack')})}],
                    zzrescrap: [{ required: true, message: this.$t('message.required', {label:this.$t('matnr.form.zzrescrap')})}],
                    zm008: [{ required: true, message: this.$t('message.required', {label:this.$t('matnr.form.zm008')})}],
                    eklas: [{ required: true, message: this.$t('message.required', {label:this.$t('matnr.form.eklas')})}],
                    zm012: [{ required: true, message: this.$t('message.required', {label:this.$t('matnr.form.zm012')})}],
                },
                attachList: [],
                formInfo: {
                    id: undefined,
                    zzuserid: undefined,
                    zzusername: undefined,
                    zzorgid: undefined,
                    zzorgname: undefined,
                    zzbpmno: undefined,
                    matnr: undefined,
                    zzcretedate: undefined,
                    kostl: undefined,
                    kostlname: undefined,
                    zzpurpose: undefined,
                    werks: this.G_CONST.werks,
                    zzpirun: undefined,
                    zzpirunChk: false,

                    // sourceInfo: "Source Information",
                    zz1stsc: undefined,
                    zz1stscChk: false,
                    zm001: undefined,
                    zm002: undefined,
                    zm012: undefined,
                    zm021: undefined,
                    zm025: undefined,
                    zm013: undefined,
                    zm023: undefined,
                    zm027: undefined,
                    zm022: undefined,
                    zm026: undefined,
                    zm003: undefined,
                    zzagadr: undefined,
                    zm020: undefined,
                    zzmkadr: undefined,

                    // basicView: "Basic View",
                    mtart: undefined,
                    matkl: undefined,
                    wgbez: undefined,
                    zmaktxEn: undefined,
                    zmaktxZh: undefined,
                    zmaktxLong: undefined,
                    zzmaktxTaxen: undefined,
                    zzmaktxTaxzh: undefined,
                    zzaffect: undefined,
                    zzaffecttlist: undefined,
                    meins: undefined,
                    meinh: undefined,
                    zzdirate: undefined,
                    umrez: undefined,
                    umren: undefined,
                    zzcorate: undefined,
                    bismt: undefined,
                    zm009: undefined,
                    zm024: undefined,
                    mhdhb: undefined,
                    mhdrz: undefined,
                    zm008: undefined,
                    zm028: undefined,
                    zm029: undefined,
                    zztypack: undefined,
                    zzecn: undefined,

                    // mqeInfo: "MQE Information",
                    zm015: undefined,
                    zzrohs: undefined,
                    zzfecp: undefined,
                    insPerson: undefined,
                    insPersonName: undefined,

                    // mrpInfo: "MRP Information",
                    xchpf: undefined,
                    dismm: "ND",
                    // dismm: undefined,
                    dispo: undefined,
                    minbe: undefined,
                    eisbe: undefined,
                    disls: undefined,
                    zm019: undefined,
                    mtvfp: undefined,
                    bstfe: undefined,

                    // eshInfo: "ESH Information",
                    zm006: undefined,

                    // purInfo: "PUR Information",
                    ekgrp: undefined,
                    eknam: undefined,
                    zm004: undefined,
                    zm005: undefined,
                    bstme: undefined,
                    zzcoratePur: undefined,
                    bstmi: undefined,
                    zumrez: undefined,
                    zumren: undefined,
                    bstrf: undefined,
                    zpurtype: undefined,
                    plifz: undefined,
                    zzcapacity: undefined,
                    zzrepack: undefined,
                    zzrescrap: undefined,

                    // legalInfo: "Legal Information",
                    zm007: undefined,
                    zm007Chk: false,

                    // whInfo: "WH Information",
                    lgfsb: undefined,
                    lgpro: undefined,
                    webaz: undefined,

                    // ficoInfo: "FICO Information",
                    bklas: undefined,
                    eklas: undefined,
                    zplp1: undefined,
                    zpld1: null,
                    zzexchange: undefined,

                    // 标识为Material
                    type: this.G_CONST.materialType.createMaterial,

                    flowStatus: this.G_CONST.flowStatus.draft,
                },
                loading: false,

                url: {
                    save: window._CONFIG['poBaseUrl'] + '/matnr/save',
                    submit: window._CONFIG['poBaseUrl'] + '/matnr/submit',
                    back: window._CONFIG['poBaseUrl'] + '/matnr/back',
                    // 获取目标节点地址
                    nextNodeUrl: window._CONFIG['poBaseUrl'] + '/matnr/nextNodeInfo',
                    delete: window._CONFIG['poBaseUrl'] + '/matnr/delete',
                    search: window._CONFIG['poBaseUrl'] + '/matnr/search',
                    user: window._CONFIG['poBaseUrl'] + '/erp/bpm/user',
                    // 获取币种汇率
                    exrate: '/searchhelp/exchange/list',
                }
            }
        },
        created() {

        },

        watch: {
        },

        deactivated() {
            console.log("deactivated....", this.$options.name);
        },
        activated() {
            console.log("activated....", this.$options.name);
            // 激活窗口，重新加载数据
            // this.init();
        },

        methods: {
            moment,

            zzcorateCalculator() {
              debugger
              this.formInfo.zzcorate = undefined;
              this.formInfo.zzcoratePur = undefined;
              if(!this.formInfo.meinh) {
                this.formInfo.umrez = undefined;
                this.formInfo.umren = undefined;
              }
              if(!this.formInfo.bstme) {
                this.formInfo.zumren = undefined;
              }
              if (this.formInfo.meins && this.formInfo.meinh && (this.formInfo.meins == this.formInfo.meinh)) {
                this.formInfo.umrez = Number(1);
                this.formInfo.umren = Number(1);
              }
                if(this.formInfo.umrez && this.formInfo.meins &&  this.formInfo.umren && this.formInfo.meinh ) {
                    this.formInfo.zzcorate = this.formInfo.umrez + this.formInfo.meins + "=" + this.formInfo.umren + this.formInfo.meinh;
                }
                if(this.formInfo.zumrez && this.formInfo.meins && this.formInfo.zumren && this.formInfo.bstme) {
                    this.formInfo.zzcoratePur = this.formInfo.zumrez + this.formInfo.meins + "=" + this.formInfo.zumren + this.formInfo.bstme;
                }
            },

            init() {
                this.formInfo.id = this.$route.params.id;
                this.actionType =  this.$route.params.actionType;
                let bpmInfo = Object.assign({
                    procDefId: this.G_CONST.procDefId.material,
                }, this.$route.params);
                console.log("this.userInfo()", this.userInfo());
                if(!this.formInfo.id && !bpmInfo.procInstId) {
                    this.formInfo.zzuserid = this.userInfo().username;
                    this.formInfo.zzusername = this.userInfo().realname;
                    this.formInfo.zzorgid = this.userInfo().orgIdSap;
                    this.formInfo.zzcretedate = moment().format(this.G_CONST.dateFormat.YYYYMMDD);
                    getAction(this.url.user, {
                        userName: this.formInfo.zzuserid,
                    }).then((res) => {
                        if (res.success) {
                            this.formInfo.kostl = res.result.costCenter
                            this.formInfo.kostlname = res.result.costCenterDis;
                            this.formInfo.zzorgname = res.result.orgNameFull;
                        } else {
                            this.error(res.message);
                        }
                    })
                }
                this.loadData(bpmInfo);
            },

            /*
             * 附件上传完成回调函数
             * @param formInfo 携带附件信息的表单数据
             */
            handleAttachmentFinished(attachList) {
                console.log(this.$options.name, "上传的附件信息", attachList);
                this.attachList = attachList;
            },
            loadData(bpmInfo) {
                if(!this.formInfo.id && !bpmInfo.procInstId) {
                    this.$nextTick(() => {
                        this.$refs.bpmApprovalRef.init(bpmInfo);
                    });
                    this.loading = false;
                    return;
                }
                this.loading = true;
                getAction(this.url.search, {
                    id: this.formInfo.id,
                    procInstId: bpmInfo.procInstId
                }).then(res => {
                    console.log(this.$options.name, "loadData", res);
                    Object.assign(this.formInfo, res.result);
                    this.isHUser = (this.formInfo.zm015 == 'HXXXXXX');
                    this.loadCities(this.formInfo.zm003);
                    this.setCheckboxField();
                    this.$nextTick(() => {
                        this.$refs.bpmApprovalRef.init(bpmInfo);
                    });
                });
            },

            setCheckboxField() {
                this.formInfo.zm007Chk = (this.formInfo.zm007 == this.G_CONST.summary.checked);
                this.formInfo.zz1stscChk = (this.formInfo.zz1stsc == this.G_CONST.summary.checked);
                this.formInfo.zzpirunChk = (this.formInfo.zzpirun == this.G_CONST.summary.checked);
            },
            getCheckboxField() {
                this.formInfo.zm007 = (this.formInfo.zm007Chk ? this.G_CONST.summary.checked : this.G_CONST.summary.unchecked);
                this.formInfo.zz1stsc = (this.formInfo.zz1stscChk ? this.G_CONST.summary.checked : this.G_CONST.summary.unchecked);
                this.formInfo.zzpirun = (this.formInfo.zzpirunChk ? this.G_CONST.summary.checked : this.G_CONST.summary.unchecked);
            },

            // 接收当前流程实例信息
            handleApprovalReceive(procInstInfo) {
                if(procInstInfo && procInstInfo.curNodeId) {
                    this.currNodeId = procInstInfo.curNodeId;
                }
                if(this.actionType == this.G_CONST.actionType.view) {
                    this.currNodeId = this.G_CONST.detail; // 查看详情页
                    this.$route.meta.title = "Material Detail";
                } else if(this.currNodeId == this.G_CONST.ActivityId.first) {
                    this.$route.meta.title = "Material Apply";
                } else {
                    this.$route.meta.title = "Material Approval";
                }
                this.loading = false;
                // console.log("handleApprovalReceive this.currNodeId", this.currNodeId, procInstInfo);
            },

            // 表单验证
            validateForm(callback) {
                this.formInfo.attachList = this.attachList;
                this.$refs.formRef.validate(valid => {
                    if(!valid) {
                        this.$message.warning(this.$t('message.allRequired'));
                        return;
                    }
                    // 验证必填附件
                    if(!this.formInfo.zzpirunChk) {
                        let attachValid = [];
                        let attachList = this.attachList;
                        if(attachList && attachList.length >= 1) {
                            attachList.forEach(a => {
                                if(this.G_CONST.matnrAttachRequired.includes(a.fileType) && !attachValid.includes(a.fileType)) {
                                    attachValid.push(a.fileType);
                                }
                            });
                        }
                        // if(attachValid.length < this.G_CONST.matnrAttachRequired.length) {
                        //     this.warning(this.$t('message.required', {label: "File Type " + this.G_CONST.matnrAttachRequired.join(" / ")}));
                        //     return;
                        // }
                    }
                    callback();
                });
            },

            handleSave(formInfo, callback) {
                this.getCheckboxField();
                // 表单验证
                this.$refs.formRef.validate(valid => {
                    this.loading = true;
                    this.formInfo.attachList = this.attachList;
                    /*if(this.formInfo.createTime) {
                        this.formInfo.createTime = moment(this.formInfo.createTime).format(this.G_CONST.dateFormat.YYYYMMDDHHMMSS);
                    }
                    if(this.formInfo.submitDate) {
                        this.formInfo.submitDate = moment(this.formInfo.submitDate).format(this.G_CONST.dateFormat.YYYYMMDDHHMMSS);
                    }*/
                    postAction(this.url.save, this.formInfo).then(res => {
                        // console.log(res);
                        if(res.success) {
                            if(this.G_CONST.ActivityId.end == formInfo.bpmParam.nextNodeId) {
                                //审批结束 例Approve
                                this.success(this.$t('message.finishAction', {
                                    'menuName': "",
                                    option: formInfo.bpmParam.bpmAction,
                                    'number': res.result && res.result.zzbpmno,
                                }));
                            } else if(this.formInfo.flowStatus == this.G_CONST.flowStatus.active) {
                              this.success(this.$t('message.inflowAction', {
                                    'menuName': "",
                                    option: formInfo.bpmParam.bpmAction,
                                    'number': res.result && res.result.zzbpmno,
                                    nexStep: (res.result.currUser || formInfo.bpmParam.nextUser)
                                }));
                            } else {
                                this.success(this.$t('message.saveDraft', {
                                    'menuName': "",
                                    'number': res.result && res.result.zzbpmno,
                                }));
                            }
                            this.closeCurrent();
                        } else {
                            if(res.result && res.result.zzbpmno) {
                                this.formInfo.zzbpmno = res.result.zzbpmno;
                            }
                            this.error(res.message);
                        }
                        this.loading = false;
                    });
                });
            },

            handleSubmit(formInfo) {
                console.log("submit", formInfo);
                this.formInfo.bpmParam = formInfo.bpmParam;
                this.formInfo.flowStatus = this.G_CONST.flowStatus.active;
                this.handleSave(this.formInfo);
            },

            handleBpmBack(formInfo) {
                this.loading = true;
                postAction(this.url.back, formInfo.bpmParam).then(res => {
                    // console.log(res);
                    if(res.code == this.G_CONST.state.success) {
                        this.success({
                            content: this.$t('message.inflowAction', {
                                'menuName': "",
                                option: formInfo.bpmParam.bpmAction,
                                'number': res.result && res.result.ebeln
                            })
                        });
                        this.closeCurrent();
                    } else {
                        this.error(res.message);
                    }
                    this.loading = false;
                });
            },

            handleDeleteProcess(param) {
                this.loading = true;
                postAction(this.url.delete, param).then(res => {
                    // console.log(res);
                    if(res.code == this.G_CONST.state.success) {
                        this.success(this.$t('message.deleteDraft', {
                            'menuName': "",
                            'number': res.result && (res.result.ebeln || res.result.bpmNo)
                        }));
                        this.closeCurrent();
                    } else {
                        this.$message.error(res.message);
                    }
                    this.loading = false;
                });
            },

            currencyChange(value) {
                this.formInfo.zm005 = value;
                if(value == "CNY"){
                    this.formInfo.zzexchange = 1;
                    return;
                }
                this.formInfo.zzexchange = undefined;
                let params={
                    type:'M',
                    fromCurrency: value,
                    toCurrency: 'CNY',
                    currentDate: moment().format("yyyyMMDD"),
                };

                getAction(this.url.exrate, params).then((res) => {
                    if(res.success) {
                        if(res.result.records[0]) {
                            this.formInfo.zzexchange = res.result.records[0].toRate;
                        }
                    } else {
                        this.error(res.message);
                    }
                });
            },

            dlgMatnrClick() {
                this.$refs.dlgMatnr.loadPage({
                    matkl: "M"
                });
            },
            dlgMatnrOk(data) {
                console.log("dlgMatnrOk", data);
                this.formInfo.zm012 = data.matnr;
                // this.formInfo.zm013 = data.zm002;
                this.formInfo.zm013 = data.zrevs8;
            },

            dlgMatklClick() {
                this.$refs.dlgMatkl.loadPage({wgbez60: this.formInfo.mtart});
            },
            dlgMatklOk(data) {
                this.formInfo.matkl = data.matkl;
                this.formInfo.wgbez = data.wgbez;
            },

            dlgEkgrpClick() {
                this.$refs.dlgEkgrp.loadPage()
            },
            dlgEkgrpOk(data) {
                this.formInfo.ekgrp = data.ekgrp;
                this.formInfo.eknam = data.eknam;
            },

            dlgLgortClick() {
                this.$refs.dlgLgort.loadPage();
            },
            dlgLgortOk(data) {
                console.log("dlgLgortOk", data);
                this.formInfo.lgfsb = data.lgort;
                this.formInfo.lgpro = data.lgort;
            },
        }
    }
</script>

<style>
  @import "~@assets/css/style.css";
</style>
```


3 被引入的文件attachement

```html
<template>
  <a-card>
      <a-table
        size="middle"
        bordered
        rowKey="id"
        :pagination="false"
        :columns="columns"
        :dataSource="dataSource">

         <span slot="action" slot-scope="text, record, index">
           <a v-if="G_CONST.previewType.includes(record.fileServerName.substr(record.fileServerName.lastIndexOf('.') + 1).toUpperCase())" @click="handlePreview(record, index)">{{$t('btn.preview')}}</a>
           <a v-if="!G_CONST.previewType.includes(record.fileServerName.substr(record.fileServerName.lastIndexOf('.') + 1).toUpperCase())" @click="handleDownload(record, index)">{{$t('btn.download')}}</a>
           <a-divider v-if="!view && userInfo().username==record.createBy" type="vertical" />
           <a v-if="!view && userInfo().username==record.createBy" @click="handleDelete(record, index)">{{$t('btn.delete')}}</a>
        </span>
      </a-table>

    <template #title>
		
		// 直接使用 boolen型的showTips
        {{ $t('attachment.name') }} <a-icon v-if="showTips" @click="downloadAttachmentRule" :title="$t('matnr.attachrule')" type="info-circle" theme="twoTone" twoToneColor="#eb2f96" />
    </template>

    <template #extra v-if="!view">
      <a-input v-if="!hides||!hides.includes('remark')" :maxLength="150" v-model="attachInfo.fileDesc" :placeholder="$t('placeholder.input',{label:$t('business.remark')})" style="width:400px;margin-right:12px;" />

      <j-dict-select-tag v-if="!hides||!hides.includes('filetype')" size="small" v-model="attachInfo.fileType" :dictCode="filetype || 'FILETYPE'" style="width:300px;margin-right:12px;" />

      <a-upload name="file" size="small"
                :action="url.upload"
                :multiple="true"
                :showUploadList="false"
                :data="attachInfo"
                :before-upload="beforeUpload"
                @change="handleUploadChange"
      >
        <a-button class="level1Button" icon="upload" type="primary">
          {{$t('btn.upload')}}
        </a-button>
      </a-upload>
    </template>
  </a-card>
</template>

<script>
  import {getAction, postAction, deleteAction} from '@/api/manage'
  import { ACCESS_TOKEN } from "@/store/mutation-types"
  import Vue from 'vue'
  import { Common } from '@/utils/common.js'

  export default {
    name: "Attachment",
      mixins: [ Common ],
    components: {

    },
      // view=true: 不显示上传按钮
	  
	  // props获取页面传值
      props: ["view", "formInfo", "filetype", "hides", "showTips", "bpmType"],
    data() {
      return {
          description: 'Attachment List',
          loading: undefined,
          fileLength: -1,
          data: {}, // 接收表单数据
          attachInfo: {
              fileType: "",
          },
		  
		  // export default_data_return 中定义本页面使用的参数childBpmType
          childBpmType: this.bpmType,
          columns: [],
          dataSource: [],
          templateName: undefined,
          url: {
              list: window._CONFIG['poBaseUrl'] + '/erp/attachment/list',
              upload: window._CONFIG['poBaseUrl'] + '/erp/attachment/upload',
              delete: window._CONFIG['poBaseUrl'] + '/erp/attachment/delete',
              download: window._CONFIG['poBaseUrl'] + '/erp/attachment/download',
              preview: window._CONFIG['poBaseUrl'] + '/erp/attachment/preview',
              template: window._CONFIG['poBaseUrl'] + "/download/template"
          },
      }
    },

      watch: {
        "formInfo.id": function(nval) {
            console.log("watch formInfo.id", this.$options.name);
            if(nval) {
                this.attachInfo.formId = nval;
                this.loadData();
            }
          }
      },

    created() {
        console.log("created", this.$options.name, this.formInfo);

        let columns = [];
        if(!this.hides || !this.hides.includes('filetype')) {
            columns.push({
                title: this.$t('attachment.fileType'),
                align: "center",
                width: 200,
                dataIndex: 'fileType',
                ellipsis: true,
            });
        }
        columns = columns.concat({
            title: this.$t('attachment.fileName'),
            align: "center",
            width: 200,
            dataIndex: 'fileName',
            ellipsis: true,
        }, {
            title: this.$t('attachment.fileSize'),
            align: "center",
            width: 80,
            dataIndex: 'fileSize',
        }, {
            title: this.$t('attachment.createBy'),
            align: "center",
            width: 120,
            dataIndex: 'createBy',
        }, {
            title: this.$t('attachment.createDate'),
            align: "center",
            width: 120,
            dataIndex: 'createDate',
        });
        if(!this.hides || !this.hides.includes('remark')) {
            columns.push({
                title: this.$t('business.remark'),
                align: "center",
                width: 200,
                dataIndex: 'fileDesc',
                ellipsis: true,
            });
        }
        columns.push({
            title: this.$t('btn.action'),
            align: "center",
            width: 150,
            scopedSlots: { customRender: 'action' },
        });
        this.columns = columns;

        const token = Vue.ls.get(ACCESS_TOKEN);
        this.attachInfo.token = token;
        if(this.formInfo.id) {
            this.attachInfo.formId = this.formInfo.id;
            this.loadData();
        }
    },

    methods: {
        downloadAttachmentRule() {
		
		// 不直接使用bpmType，而是使用本页面改造化的childBpmType
            if(this.childBpmType == "PROC_MMS_PARTS"){
                this.templateName = "Parts需求资料.xlsx";
            }else if(this.childBpmType == "PROC_MMS_MATERIAL"){
                this.templateName = "原材料准备资料.pptx";
            };
            window.open(this.url.template + "?token=" + this.attachInfo.token + "&fileName=" + encodeURI(this.templateName));
        },

        loadData() {
            getAction(this.url.list, {
                formId: this.attachInfo.formId
            }).then(res => {
                console.log(this.$options.name, "loadData", res.result);
                if(res.code == this.G_CONST.state.success) {
                    this.dataSource = res.result;
                    this.emitFinished();
                } else {
                    this.$message.error(res.message);
                }
            });
        },

        // 上传附件前的验证
        beforeUpload(file, fileList) {
            return new Promise((resolve, reject) => {
                // console.log("beforeUpload", fileList.length);
                // 判断附件类型是否必填
                if(!this.attachInfo.fileType && (!this.hides || !this.hides.includes('filetype'))) {
                    this.$message.warning(this.$t('message.required', {label: this.$t('attachment.fileType')}));
                    reject();
                } else {
                    this.fileLength = fileList.length;
                    resolve();
                }
            });
        },

        // 手动上传附件
        uploadFile(file) {

        },

        handleUploadChange(info) {
            console.log("handleUploadChange", info);
            if(!this.attachInfo.fileType && (!this.hides || !this.hides.includes('filetype'))) {
                info.fileList = [];
                return;
            }
            let file = info.file;
            let res = file.response;
            if(info.fileList.length == 1 && !this.loading) {
                this.loading = this.$message.loading(this.$t("message.uploading"), 0);
            }
            if(res){
                this.fileLength = this.fileLength - 1;
                if(res.success) {
                    this.dataSource.push(res.result);
                } else {
                    this.error(file.name + ": " + res.message);
                    console.error(file.name + ": " + res.message);
                }
            }
            if(this.fileLength == 0 && this.loading) {
                this.loading();
            }
            if(this.fileLength == 0) {
                this.emitFinished();
            }
        },

        handleDownload(record) {
            window.open(this.url.download + "?token=" + this.attachInfo.token + "&id=" + record.id);
        },

        handlePreview(record) {
            window.open(this.url.preview + "?token=" + this.attachInfo.token + "&id=" + record.id);
        },

        handleDelete(record) {
            let that = this;
            this.$confirm({
                title: this.$t('message.confirm.title'),
                content: this.$t('message.confirm.delete'),
                onOk() {
                    deleteAction(that.url.delete, {
                        id: record.id
                    }).then(res => {
                        if(res.code == that.G_CONST.state.success) {
                            let dataSource = [...that.dataSource];
                            let index = dataSource.findIndex(d => d.id == record.id);
                            dataSource.splice(index, 1);
                            that.dataSource = dataSource;
                            that.emitFinished();
                        } else {
                            that.$message.error(res.message);
                        }
                    });
                },
                onCancel() {
                },
            });
        },
        emitFinished() {
            this.attachInfo.fileDesc = "";
            this.$emit("finished", JSON.parse(JSON.stringify(this.dataSource)));
        },
    }
  }
</script>

<style>
  @import "~@assets/css/style.css";
</style>
```


4 实现示例

![img](https://github.com/DrJasonLiu666/CXT_ERP_Microservice_System/blob/main/photos/Chapter%2010%20ERP%E9%A1%B9%E7%9B%AE%E4%B9%8B%E5%89%8D%E7%AB%AF%E9%83%A8%E5%88%86%E5%8A%9F%E8%83%BD%E7%9A%84%E6%80%BB%E7%BB%93%E2%91%A0/8.png)
