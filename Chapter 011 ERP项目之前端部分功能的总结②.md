# 1 前端调试的浏览器使用方法

可参考：[如何在chrome浏览器里面debug调试前端代码？_前端debug_代码狮的博客-CSDN博客](https://blog.csdn.net/weixin_45157527/article/details/119214561)

# 2 前端运行环境之node

node是前端中JS运行环境，提供了包管理器npm

Node.js是一个JavaScript的编译环境，当前端语言JavaScript在写完之后可以交给Node.js进行编译和解释，它的存在对于JavaScript有了质的飞跃

可参考：https://zhuanlan.zhihu.com/p/372855120#:~:text=Node.js%E9%80%9A%E5%B8%B8%E8%A2%AB%E7%94%A8%E6%9D%A5%E5%BC%80%E5%8F%91%E4%BD%8E%E5%BB%B6%E8%BF%9F%E7%9A%84%E7%BD%91%E7%BB%9C%E5%BA%94%E7%94%A8%EF%BC%8C%E4%B9%9F%E5%B0%B1%E6%98%AF%E9%82%A3%E4%BA%9B%E9%9C%80%E8%A6%81%E5%9C%A8%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%AB%AF%E7%8E%AF%E5%A2%83%E5%92%8C%E5%89%8D%E7%AB%AF%E5%AE%9E%E6%97%B6%E6%94%B6%E9%9B%86%E5%92%8C%E4%BA%A4%E6%8D%A2%E6%95%B0%E6%8D%AE%E7%9A%84%E5%BA%94%E7%94%A8%EF%BC%88API%E3%80%81%E5%8D%B3%E6%97%B6%E8%81%8A%E5%A4%A9%E3%80%81%E5%BE%AE%E6%9C%8D%E5%8A%A1%EF%BC%89%E3%80%82%20%E9%98%BF%E9%87%8C%E5%B7%B4%E5%B7%B4%E3%80%81%E8%85%BE%E8%AE%AF%E3%80%81Qunar%E3%80%81%E7%99%BE%E5%BA%A6%E3%80%81PayPal%E3%80%81%E9%81%93%E7%90%BC%E6%96%AF%E3%80%81%E6%B2%83%E5%B0%94%E7%8E%9B%E5%92%8C%20LinkedIn,%E9%83%BD%E9%87%87%E7%94%A8%E4%BA%86%20Node.js%20%E6%A1%86%E6%9E%B6%E6%90%AD%E5%BB%BA%E5%BA%94%E7%94%A8%E3%80%82


# 3 前后端间传值：VO、Entity、JSon

## 3.1 前端调用后端SAP接口进行实时查询

```
从前端完成一次调用API的接口，通过Java的工程的controller调到SAP的一个完整流程：
【以BPMWAN00801为例】

①先由对方提供SAP的接口。如果是纯后端开发，只需要在POSTMAN里面调用、调通，再完成Java实装即可。如果是全栈开发，需要从一整套配置开始。
【对方发送格式】
库存查询格式如下
URL: http://berptap03.cxtwh.local:50000/RESTAdapter/BPMWAN00801
入参JSON格式
{
    "reqJSON": "{\"MATNR\":\"FY010004\",\"WERKS\":\"1011\",\"LGORT\":\"\",\"CHARG\":\"\",\"ZREVS1\":\"\",\"ZREVS2\":\"\",\"ZREVS3\":\"\",\"ZREVS4\":\"\",\"ZREVS5\":\"\"}"
}


【POSTMAN测试调通】


【后端】
②S1配置文件层：【application-dev.yml文件】
sap:
  username: PO_IBMERP
  password: Ibmerp1111
  url: http://berptap03.cxtwh.local:50000/RESTAdapter/
  BPM00101: BPM00101
  BPM00201: BPM00201
  BPM00301: BPM00301
  BPM00401: BPM00401
  BPM00501: BPM00501
  BPM00601: BPM00601
  BPM00701: BPM00701
  BPM00801: BPM00801
  BPM00901: BPM00901
  BPM01001: BPM01001
  BPM01101: BPM01101
  BPM01201: BPM01201
  BPM01301: BPM01301
  BPMPR00101: BPMPR00101
  BPMPR00201: BPMPR00201
  BPMPR00301: BPMPR00301
  BPMPR00401: BPMPR00401
  BPMPR00601: BPMPR00601
  BPMWAN00101: BPMWAN00101
  BPMWAN00301: BPMWAN00301
  BPMWAN00401: BPMWAN00401
  BPMWAN00701: BPMWAN00701
  BPMWAN00201: BPMWAN00201
  BPMWAN00501: BPMWAN00501
  BPMWAN00601: BPMWAN00601
  BPMRSNUM00101: BPMRSNUM00101
  BPMWAN00801: BPMWAN00801
  BPMWAN00901: BPMWAN00901
  BPMRSNUM00201: BPMRSNUM00201
  BPMWAN01001: BPMWAN01001
③S2  Client层:  sapclient   【GISapClient.java文件】
/**
 * SAP接口调用客户端
 */
@Component
public class GISapClient {

	private final static Logger logger = LoggerFactory.getLogger(GISapClient.class);

	@Value("${sap.url}")
	private String url;
	@Value("${sap.username}")
	private String username;
	@Value("${sap.password}")
	private String password;
	@Value("${sap.connTimeout}")
	private int connTimeout;
	@Value("${sap.readTimeout}")
	private int readTimeout;

	// BPMRSNUM00101 预留单创建
	@Value("${sap.BPMRSNUM00101}")
	private String BPMRSNUM00101;
	@Value("${sap.BPMWAN00801}")
	private String BPMWAN00801;
	@Value("${sap.BPMRSNUM00201}")
	private String BPMRSNUM00201;
	@Value("${sap.BPMWAN01001}")
	private String BPMWAN01001;


	public JSONObject executeBPMMM038(GIMainPage para) {
		JSONObject params = new JSONObject();
		if (StringUtils.isNotBlank(para.getLgort())) {
			params.put("LGORT", para.getLgort());
		}
		if (StringUtils.isNotBlank(para.getCharg())) {
			params.put("CHARG", para.getCharg());
		}
		params.put("MATNR", para.getMatnr());
		params.put("WERKS", para.getWerks());
		JSONObject reqJson = new JSONObject();
		reqJson.put("reqJSON", params.toJSONString().replaceAll("\"", "\\\""));
		JSONObject jsonObject = execute(BPMWAN00801, reqJson);
		return jsonObject;
	}
}

④S3  Controller层:   【GIController文件】

    @RequestMapping(value = "/materHelper", method = RequestMethod.POST)
    public Result materHelper(@RequestBody GIMainPage para) {
        if (StringUtils.isBlank(para.getMatnr()) || StringUtils.isBlank(para.getWerks())) {
            return Result.OK();
        }
        JSONObject jsonObject = sapClient.executeBPMMM038(para);
        if (!jsonObject.containsKey("resJSON")) {
            return Result.error("SAP-查询物料库存失败。");
        }
        JSONObject resJSON = jsonObject.getJSONObject("resJSON");
        if (!StringUtils.equals("S", resJSON.getString("TYPE"))) {
            String message = resJSON.getString("MESSAGE");
            return Result.error(message);
        } else {
            Map<String, Object> resMap = new HashMap<>();
            resMap.put("labst", resJSON.getString("LABST"));
            resMap.put("slabs", resJSON.getString("SLABS"));
            return Result.OK(resMap);
        }
    }

⑤S4  VO层：定义GIMainPage类【ERP.VO.GIMainPage.java文件】
@Data
public class GIMainPage {

    private List<ErpGIDetail> detail;
    private ErpGIHeader header;
    private String bpmNo;
    private String flowStatus;
    private String submitUser;


    private String currentUser;
    private String userName;

    private String headerId;
    private String processId;
    private String sysCode;
    private String status;

    private Integer pageNo;
    private Integer pageSize;

    private String matnr;
    private String werks;
    private String lgort;
    private String charg;

}


【前端】【GIDetailModal文件——第三层查询页面】
【Script中】	
①Url中：
export default {
  name: "GDetailModal",
  components: {
    JDate,
    DlgMatnr,
    DlgLgort,
    DlgBatch
  },
  data() {
    return {
      url: {
        findMatnr: "/searchhelp/matnr/queryMatnrByMatnr",
        matnrHelper: "/erp/gi/materHelper"
      }
    }
  },
}

②methods中：
export default {
  methods: {
    materHelper() {
      if(this.itemInfo.matnr) {
        let params = {};
        params.lgort = '';
        params.charg = '';
        params.matnr = this.itemInfo.matnr;
        params.werks = this.werks;
        postAction(this.url.matnrHelper, params).then((res) => {
          if (res.code == 200 && res.result) {
            this.itemInfo.labst = res.result.labst;
            this.itemInfo.consignStock = res.result.slabs;
          }
        })
      }
    },
  }
}


【template中】
```


## 3.2 前端通过后端调用SAP接口并保存在数据库中【不在前端展示】

前后端：VO类

 后端调接口查询SAP：sapClient层——application层面
 
 后端对数据库的操作：Service层
 
 后端与数据库：entity类

## 3.3 前端通过后端进行数据库查询并分页展示

【以Business Setting——物料——Search为例】

 【前端】【MatnrModule.vue文件】

##
【后端】

 1、VO类【SearchHelpVO.java】
 
 【前后端传输的数据内容】
##
2、entity类【entity.ErpHMatnr.java文件】

 【指明TableName】
 
 【后端对数据库某表需要查询的字段，即后端与数据库数据交换的格式内容】

##
 3、Controller层【SearchMenuHelpController.java文件】
 
 【调用mybatisplus中的queryWrapper进行entity类封装操作，从而实现对数据库查询】
##
4、IPage、Page实现分页传输

# 4 vue中插槽Slot功能的使用

## 4.1 参考教程

[(47条消息) antd vue table组件中slots scopedSlots scopedSlots 的用法_antd vue scopedslots_北方爷们儿的博客-CSDN博客](https://blog.csdn.net/hxm2017jy/article/details/121927621)

## 4.2 使用方法（以CXTMMS中columns的插槽使用为例）

### 4.2.1 效果图

1）横向条某行中某一栏的单栏弹窗式插槽功能示例（无图标）_MMS

![img](https://github.com/DrJasonLiu666/CXT_ERP_Microservice_System/blob/main/photos/Chapter%2011%20ERP%E9%A1%B9%E7%9B%AE%E4%B9%8B%E5%89%8D%E7%AB%AF%E9%83%A8%E5%88%86%E5%8A%9F%E8%83%BD%E7%9A%84%E6%80%BB%E7%BB%93%E2%91%A1/1.png)

2）横向条某行中某一栏的下拉框插槽功能示例_MMS

![img](https://github.com/DrJasonLiu666/CXT_ERP_Microservice_System/blob/main/photos/Chapter%2011%20ERP%E9%A1%B9%E7%9B%AE%E4%B9%8B%E5%89%8D%E7%AB%AF%E9%83%A8%E5%88%86%E5%8A%9F%E8%83%BD%E7%9A%84%E6%80%BB%E7%BB%93%E2%91%A1/2.png)

### 4.2.2 代码

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
      <a-card :title="$t('parts.form.applyInfo')">
        <a-row :gutter="24">
          <a-col :span="3">
            <a-form-model-item :label="$t('parts.form.zzuserid')"></a-form-model-item>
          </a-col>
          <a-col :span="5">
            <a-input-group compact>
              <a-input v-model="formInfo.zzuserid" style="width:35%" disabled />
              <a-input v-model="formInfo.zzusername" style="width:65%" disabled />
            </a-input-group>
          </a-col>
          <a-col :span="3">
            <a-form-model-item :label="$t('parts.form.zzorgid')"></a-form-model-item>
          </a-col>
          <a-col :span="5">
            <a-input-group compact>
              <a-input v-model="formInfo.zzorgid" style="width:35%" disabled />
              <a-input v-model="formInfo.zzorgname" style="width:65%" disabled />
            </a-input-group>
          </a-col>
          <a-col :span="3">
            <a-form-model-item :label="$t('parts.form.zzbpmno')"></a-form-model-item>
          </a-col>
          <a-col :span="5">
            <a-input v-model="formInfo.zzbpmno" disabled />
          </a-col>
        </a-row>
        <a-row :gutter="24">
          <a-col :span="3">
            <a-form-model-item :label="$t('matnr.form.werks')" required prop="werks"></a-form-model-item>
          </a-col>
          <a-col :span="5">
            <j-dict-select-tag v-model="formInfo.werks" dictCode="WERKS" />
          </a-col>
          <a-col :span="3">
            <a-form-model-item :label="$t('parts.form.eshGuardian')"></a-form-model-item>
          </a-col>
          <a-col :span="5">
            <a-tooltip placement="right" :title="$t('parts.form.eshGuardianTip')">
              <a-checkbox v-model="formInfo.eshChk" />
            </a-tooltip>
          </a-col>
          <a-col :span="3">
            <a-form-model-item :label="$t('parts.form.zzcretedate')"></a-form-model-item>
          </a-col>
          <a-col :span="5">
            <a-input v-model="formInfo.zzcretedate" disabled />
          </a-col>
        </a-row>
        <a-row :gutter="24">
          <a-col :span="3">
            <a-form-model-item :label="$t('parts.form.zzpurpose')" required prop="zzpurpose"></a-form-model-item>
          </a-col>
          <a-col :span="21">
            <a-textarea v-model="formInfo.zzpurpose" :autoSize="{minRows:2}" />
          </a-col>
        </a-row>
      </a-card>

      <a-card :title="$t('parts.crForm.partsInfo')" style="margin-top:10px;">
        <a-row :gutter="24">
          <a-col :span="3">
            <a-form-model-item :label="$t('parts.crForm.zcctype')" required prop="zcctype"></a-form-model-item>
          </a-col>
          <a-col :span="9">
            <j-dict-select-tag v-model="formInfo.zcctype" dictCode="PARTS_CLEAN_REPAIR" />
          </a-col>
          <a-col :span="3">
            <a-form-model-item :label="$t('parts.crForm.zzdemo')" required prop="zzdemo"></a-form-model-item>
          </a-col>
          <a-col :span="9">
            <j-dict-select-tag v-model="formInfo.zzdemo" dictCode="COMMON_FLAG" />
          </a-col>
        </a-row>
        <a-row :gutter="24">
          <a-col :span="3" v-if="formInfo.zcctype==G_CONST.cleanParts">
            <a-form-model-item :label="$t('parts.crForm.zzcleantyp')"></a-form-model-item>
          </a-col>
          <a-col :span="9" v-if="formInfo.zcctype==G_CONST.cleanParts">
            <j-dict-select-tag v-model="formInfo.zzcleantyp" dictCode="PARTS_CLEAN_TYPE" />
          </a-col>
          <a-col :span="3" v-if="formInfo.zcctype==G_CONST.repairParts">
            <a-form-model-item :label="$t('parts.crForm.zzecb')"></a-form-model-item>
          </a-col>
          <a-col :span="9" v-if="formInfo.zcctype==G_CONST.repairParts">
            <j-dict-select-tag v-model="formInfo.zzecb" dictCode="COMMON_FLAG" />
          </a-col>
        </a-row>
      </a-card>

      <a-card :title="$t('parts.form.sourceInfo')" style="margin-top:10px;">
        <a-row :gutter="24">
          <a-col :span="3">
            <a-form-model-item :label="$t('parts.form.zm002')" required prop="zm002"></a-form-model-item>
          </a-col>
          <a-col :span="9">
            <a-input v-model="formInfo.zm002" />
          </a-col>
          <a-col :span="3">
            <a-form-model-item :label="$t('parts.form.zm025')"></a-form-model-item>
          </a-col>
          <a-col :span="9">
            <a-input v-model="formInfo.zm025" />
          </a-col>
        </a-row>
        <a-row :gutter="24">
          <a-col :span="3">
            <a-form-model-item :label="$t('parts.form.zm027')"></a-form-model-item>
          </a-col>
          <a-col :span="9">
            <a-input v-model="formInfo.zm027" />
          </a-col>
          <a-col :span="3">
            <a-form-model-item :label="$t('parts.form.zm026')"></a-form-model-item>
          </a-col>
          <a-col :span="9">
            <a-input v-model="formInfo.zm026" />
          </a-col>
        </a-row>
        <a-row :gutter="24">
          <a-col :span="3">
            <a-form-model-item :label="$t('parts.form.zzagadr')"></a-form-model-item>
          </a-col>
          <a-col :span="21">
            <a-input v-model="formInfo.zzagadr" />
          </a-col>
        </a-row>
      </a-card>
    </div>
    </a-form-model>
    <br/>

    <a-card :title="$t('parts.crItem.name')">

      <!-- 操作按钮区域 -->
      <div class="table-operator">
        <a-button class="level2Button" @click="addRow" size="small" type="primary" icon="plus" :disabled="!formInfo.werks||columns.length==0">{{$t('btn.add')}}</a-button>
        <a-button class="level2Button" @click="deleteRows" size="small" type="danger" icon="delete" :disabled="!formInfo.werks||columns.length==0">{{$t('btn.delete')}}</a-button>
      </div>

      <!-- table区域-begin -->
      <div>
        <a-table
          ref="table"
          size="middle"
          bordered
          :rowKey="r => r.id || r.vid"
          :columns="columns"
          :dataSource="dataSource"
          :pagination="false"
          :loading="loading"
          :scroll="{x: 2000, y: 460}"
          :rowSelection="{selectedRowKeys: selectedRowKeys, onChange: onSelectChange}"
        >
          <template slot="matnr" slot-scope="text, record">
            <SearchHelperCell :text="text" :params="shcParams" type="matnr" @change="handleChangeCell(record.id||record.vid, 'matnr', $event)" @click="stopPropagation" />
          </template>

          <template :slot="slot" slot-scope="text, record" v-for="slot in editorCells">
            <SelectCell v-bind:key="slot" :text="text" dictCode="COMMON_FLAG" @change="handleChangeCell(record.id||record.vid, slot, $event)" @click="stopPropagation" />
          </template>

          <template slot="zzsnno" slot-scope="text, record">
            <InputCell :text="text" @change="handleChangeCell(record.id||record.vid, 'zzsnno', $event)" @click="stopPropagation" />
          </template>
        </a-table>
      </div>
    </a-card>

    <!-- finished=附件上传完成后都会回调该方法 -->
    <Attachment :formInfo="formInfo" filetype="MMS_FILETYPE" :view="G_CONST.actionType.view==actionType" @finished="handleAttachmentFinished" />

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

  </a-spin>
</template>

<script>
    import {getAction, postAction} from '@/api/manage'
    import moment from 'moment'
    import { Common } from '@/utils/common.js'
    import {randomUUID } from '@/utils/util'

    import BpmApproval from '@views/bpm/BpmApproval'
    import Attachment from '@views/bpm/Attachment'
    import InputCell from '@views/bpm/InputCell'
    import SearchHelperCell from '@views/bpm/SearchHelperCell'
    import SelectCell from '@views/bpm/SelectCell'

    import { ACCESS_TOKEN } from "@/store/mutation-types"
    import Vue from 'vue'

    export default {
        name: "CleanRepairPartsApply",
        mixins: [ Common ],
        components: {
            BpmApproval,
            Attachment,
            InputCell,
            SearchHelperCell,
            SelectCell
        },
        data() {
            return {
                description: 'CleanRepairPartsApply',
                loading: false,
                currNodeId: undefined, // 当前节点
                actionType: undefined,
                formInfo: {
                    id: undefined,
                    applyInfo: undefined,
                    zzuserid: undefined,
                    zzorgid: undefined,
                    kostl: undefined,
                    kostlname: undefined,
                    zzorgname: undefined,
                    zzbpmno: undefined,
                    zcctype: undefined,
                    zzdemo: undefined,
                    zm002: undefined,
                    zm025: undefined,
                    zm027: undefined,
                    zm026: undefined,
                    zzagadr: undefined,
                    zzcretedate: undefined,
                    zzpurpose: undefined,
                    werks: this.G_CONST.werks,
                },
                rules: {
                    zzpurpose: [{ required: true, message: this.$t('message.required', {label:this.$t('parts.form.zzpurpose')})}],
                    zcctype: [{ required: true, message: this.$t('message.required', {label:this.$t('parts.crForm.zcctype')})}],
                    zm002: [{ required: true, message: this.$t('message.required', {label:this.$t('parts.form.zm002')})}],
                    zzdemo: [{ required: true, message: this.$t('message.required', {label:this.$t('parts.crForm.zzdemo')})}],
                    werks: [{ required: true, message: this.$t('message.required', {label:this.$t('matnr.form.werks')})}],
                },
                attachList: [],

                allColumns: [], // 所有字段
                columns: [], // 当前页面要展示的字段
                dataSource: [],
                selectedRowKeys: [],
                selectedRows: [],
                editorCells: ["zzkeyparts", "zzexchange", "zztcparts", "zzitdevice"],
                shcParams: {
                    werks: undefined,
                    matkl: "P"
                },

                rights: [this.G_CONST.ActivityId.first], // 可导入行项目的节点
                url: {
                    test: window._CONFIG['poBaseUrl'] + '/crparts/test',
                    save: window._CONFIG['poBaseUrl'] + '/crparts/save',
                    submit: window._CONFIG['poBaseUrl'] + '/crparts/submit',
                    back: window._CONFIG['poBaseUrl'] + '/crparts/back',
                    // 获取目标节点地址
                    nextNodeUrl: window._CONFIG['poBaseUrl'] + '/crparts/nextNodeInfo',
                    delete: window._CONFIG['poBaseUrl'] + '/crparts/delete',
                    search: window._CONFIG['poBaseUrl'] + '/crparts/search',
                    user: window._CONFIG['poBaseUrl'] + '/erp/bpm/user',
                }
            }
        },
        created() {
            this.allColumns = [{
                title: this.$t('parts.crItem.matnr'),
                align: "center",
                width: 150,
                dataIndex: 'matnr',
                scopedSlots: {customRender: "matnr"},
            }, {
                title: this.$t('parts.crItem.zzkeyparts'),
                align: "center",
                width: 100,
                dataIndex: 'zzkeyparts',
                scopedSlots: {customRender: "zzkeyparts"},
            }, {
                title: this.$t('parts.crItem.zmatnrC'),
                align: "center",
                width: 100,
                dataIndex: 'zmatnrC',
                exclude: [this.G_CONST.repairParts]
            }, {
                title: this.$t('parts.crItem.zmatnrR'),
                align: "center",
                width: 100,
                dataIndex: 'zmatnrR',
                exclude: [this.G_CONST.cleanParts]
            }, {
                title: this.$t('parts.crItem.zmaktxEn'),
                align: "center",
                width: 150,
                dataIndex: 'zmaktxEn',
                ellipsis: true,
            }, {
                title: this.$t('parts.crItem.zmaktxZh'),
                align: "center",
                width: 150,
                dataIndex: 'zmaktxZh',
                ellipsis: true,
            }, {
                title: this.$t('parts.crItem.zm009'),
                align: "center",
                width: 100,
                dataIndex: 'zm009',
            }, {
                title: this.$t('parts.crItem.zm010'),
                align: "center",
                width: 100,
                dataIndex: 'zm010',
            }, {
                title: this.$t('parts.crItem.zm011'),
                align: "center",
                width: 100,
                dataIndex: 'zm011',
            }, {
                title: this.$t('parts.crItem.zm008'),
                align: "center",
                width: 100,
                dataIndex: 'zm008',
            }, {
                title: this.$t('parts.crItem.zm007'),
                align: "center",
                width: 100,
                dataIndex: 'zm007',
            }, {
                title: this.$t('parts.crItem.zzexchange'),
                align: "center",
                width: 150,
                dataIndex: 'zzexchange',
                exclude: [this.G_CONST.cleanParts],
                scopedSlots: {customRender: "zzexchange"},
            }, {
                title: this.$t('parts.crItem.zztcparts'),
                align: "center",
                width: 100,
                dataIndex: 'zztcparts',
                exclude: [this.G_CONST.cleanParts],
                scopedSlots: {customRender: "zztcparts"},
            }, {
                title: this.$t('parts.crItem.zzitdevice'),
                align: "center",
                width: 200,
                dataIndex: 'zzitdevice',
                exclude: [this.G_CONST.cleanParts],
                scopedSlots: {customRender: "zzitdevice"},
            }, {
                title: this.$t('parts.crItem.zzsnno'),
                align: "center",
                width: 150,
                dataIndex: 'zzsnno',
                exclude: [this.G_CONST.cleanParts],
                scopedSlots: {customRender: "zzsnno"},
            }, {
                title: this.$t('parts.item.ekgrp'),
                align: "center",
                width: 150,
                dataIndex: 'ekgrp',
                scopedSlots: {customRender: "ekgrp"},
            }, {
                title: this.$t('parts.item.zm004'),
                align: "center",
                width: 150,
                dataIndex: 'zm004',
                scopedSlots: {customRender: "zm004"},
            }, {
                title: this.$t('parts.item.zm005'),
                align: "center",
                width: 150,
                dataIndex: 'zm005',
                scopedSlots: {customRender: "zm005"},
            }, {
                title: this.$t('parts.item.bstme'),
                align: "center",
                width: 150,
                dataIndex: 'bstme',
                scopedSlots: {customRender: "bstme"},
            }, {
                title: this.$t('parts.item.zumrez'),
                align: "center",
                width: 150,
                dataIndex: 'zumrez',
                scopedSlots: {customRender: "zumrez"},
            }, {
                title: this.$t('parts.item.zumren'),
                align: "center",
                width: 150,
                dataIndex: 'zumren',
                scopedSlots: {customRender: "zumren"},
            }, {
                title: this.$t('parts.item.bstmi'),
                align: "center",
                width: 150,
                dataIndex: 'bstmi',
                scopedSlots: {customRender: "bstmi"},
            }, {
                title: this.$t('parts.item.bstrf'),
                align: "center",
                width: 150,
                dataIndex: 'bstrf',
                scopedSlots: {customRender: "bstrf"},
            }, {
                title: this.$t('parts.item.zpurtype'),
                align: "center",
                width: 150,
                dataIndex: 'zpurtype',
                scopedSlots: {customRender: "zpurtype"},
            }, {
                title: this.$t('parts.item.plifz'),
                align: "center",
                width: 150,
                dataIndex: 'plifz',
                scopedSlots: {customRender: "plifz"},
            }];
        },

        watch: {
            "formInfo.zcctype": function() {
                this.createColumns();
            },
            "formInfo.werks": function() {
                this.shcParams.werks = this.formInfo.werks;
            },
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

            init() {
                this.formInfo.id = this.$route.params.id;
                this.actionType =  this.$route.params.actionType;
                let bpmInfo = Object.assign({
                    procDefId: this.G_CONST.procDefId.crParts,
                }, this.$route.params);
                if(!this.formInfo.id && !bpmInfo.procInstId) {
                    this.formInfo.zzuserid = this.userInfo().username;
                    this.formInfo.zzusername = this.userInfo().realname;
                    this.formInfo.zzorgid = this.userInfo().orgIdSap;
                    this.formInfo.zzcretedate = moment().format(this.G_CONST.dateFormat.YYYYMMDD);
                    getAction(this.url.user, {
                        userName: this.formInfo.zzuserid,
                    }).then((res) => {
                      console.log("init user", res);
                        if (res.success) {
                            this.formInfo.kostl = res.result.costCenter;
                            this.formInfo.kostlname = res.result.costCenterDis;
                            this.formInfo.zzorgname = res.result.orgNameFull;
                        } else {
                            this.error(res.message);
                        }
                    })
                }
                this.loadData(bpmInfo);
            },

            onSelectChange(selectedRowKeys, selectionRows) {
                this.selectedRowKeys = selectedRowKeys;
                this.selectionRows = selectionRows;
            },

            handleChangeCell(key, dataIndex, value) {
                console.log("handleChangeCell", value);
                const dataSource = [...this.dataSource];
                const target = dataSource.find(d => (d.id || d.vid) === key);
                if(target) {
                    if(value.matnr) { // 物料搜索帮助
                        target.matnr = value.matnr;
                        target.zmaktxEn = value.zmaktxEn;
                        target.zmaktxZh = value.zmaktxZh;
                        target.zm009 = value.zm009;
                        target.zm010 = value.zm010;
                        target.zm011 = value.zm011;
                        target.zm008 = value.zm008;
                        target.zm007 = value.zm007;
                        // pur字段
                        target.ekgrp = value.ekgrp;
                        target.bstme = value.bstme;
                        target.zumrez = value.zumrez;
                        target.zumren = value.zumren;
                        target.bstmi = value.bstmi;
                        target.bstrf = value.bstrf;
                        target.zpurtype = value.zpurtype;
                        target.plifz = value.plifz;
                        // 生成 Clean/Repair编码
                        target["zmatnr" + this.formInfo.zcctype] = this.formInfo.zcctype + target.matnr.substr(1);
                    } else {
                        target[dataIndex] = value;
                    }
                    this.dataSource = dataSource;
                }
            },

            // 添加一行
            addRow() {
                let nitem = {
                    vid: randomUUID(),
                    matnr: undefined,
                    zzkeyparts: undefined,
                    zmatnrR: undefined,
                    zmatnrC: undefined,
                    zmaktxEn: undefined,
                    zmaktxZh: undefined,
                    zm009: undefined,
                    zm010: undefined,
                    zm011: undefined,
                    zm008: undefined,
                    zm007: undefined,
                    zzexchange: undefined,
                    zztcparts: undefined,
                    zzitdevice: undefined,
                    zzsnno: undefined,
                };
                this.dataSource.push(nitem);
            },

            deleteRows() {
                if(this.selectedRowKeys && this.selectedRowKeys.length >= 1) {
                    let dataSource = [];
                    this.dataSource.forEach(d => {
                        const target = this.selectedRowKeys.find(id => id == (d.id || d.vid));
                        if(!target) {
                            dataSource.push(d);
                        }
                    });
                    this.dataSource = dataSource;
                    this.selectedRowKeys = [];
                    this.selectedRows = [];
                }
            },

            handleSave(formInfo, callback) {
                // 表单验证
                this.$refs.formRef.validate(valid => {
                    this.loading = true;
                    this.formInfo.attachList = this.attachList;
                    this.formInfo.items = this.dataSource;
                    /*if(this.formInfo.createTime) {
                        this.formInfo.createTime = moment(this.formInfo.createTime).format(this.G_CONST.dateFormat.YYYYMMDDHHMMSS);
                    }
                    if(this.formInfo.submitDate) {
                        this.formInfo.submitDate = moment(this.formInfo.submitDate).format(this.G_CONST.dateFormat.YYYYMMDDHHMMSS);
                    }*/
                    this.getCheckboxField();
                    postAction(this.url.save, this.formInfo).then(res => {
                        // console.log(res);
                        if(res.code == this.G_CONST.state.success) {
                            if(this.formInfo.flowStatus == this.G_CONST.flowStatus.active) {
                                this.success(this.$t('message.inflowAction', {
                                    'menuName': "",
                                    option: formInfo.bpmParam.bpmAction,
                                    'number': res.result && res.result.zzbpmno,
                                    nexStep: this.formInfo.bpmParam.nextUser
                                }));
                            } else {
                                this.success(this.$t('message.saveDraft', {
                                    'menuName': "",
                                    'number': res.result && res.result.zzbpmno
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
            setCheckboxField() {
                this.formInfo.eshChk = (this.formInfo.esh == this.G_CONST.eshChk.checked);
            },
            getCheckboxField() {
                if(this.formInfo.eshChk){
                  this.formInfo.esh = this.G_CONST.eshChk.checked;
                } else {
                  this.formInfo.esh = this.G_CONST.eshChk.unchecked;
                }
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
                    this.setCheckboxField()
                    this.dataSource = res.result.items;
                    this.$nextTick(() => {
                        this.$refs.bpmApprovalRef.init(bpmInfo);
                    });
                });
            },

            // 接收当前流程实例信息
            handleApprovalReceive(procInstInfo) {
                console.log(this.$options.name, "handleApprovalReceive", procInstInfo);
                if(procInstInfo && procInstInfo.curNodeId) {
                    this.currNodeId = procInstInfo.curNodeId;
                } else {
                    this.currNodeId = this.G_CONST.ActivityId.first;
                }
                /*if(this.actionType == this.G_CONST.actionType.view) {
                    this.currNodeId = "detail";
                    this.$route.meta.title = "Mass Detail";
                } else if(this.currNodeId == this.G_CONST.ActivityId.first) {
                  this.$route.meta.title = "Mass Apply";
                } else {
                  this.$route.meta.title = "Mass Approval";
                }*/
                this.loading = false;
            },

            handleBeforeUpload(file) {
                Object.assign(this.importBusiData, this.formInfo);
                this.importBusiData.currNodeId = this.currNodeId;
                this.formInfo.currNodeId = this.currNodeId;
                console.log("this.importBusiData", this.importBusiData, "this.formInfo", this.formInfo);
            },

            handleUploadChange(info) {
                console.log(this.$options.name, "handleUploadChange", info);
                let file = info.file;
                let res = file.response;
                this.loading = true;

                if(file.status === 'uploading') {
                    console.log("handleUploadChange uploading res", res);
                }
                if(file.status === 'done') {
                    this.loading = false;
                    console.log("handleUploadChange Success", res);
                    if(res.success) {
                        this.dataSource = res.result;
                    } else {
                        this.error(res.message);
                    }
                } else if (file.status === 'error') {
                    this.loading = false;
                    this.error(res.message);
                }
            },
            getCheckboxField() {
                if(this.formInfo.eshChk){
                  this.formInfo.esh = this.G_CONST.eshChk.checked;
                } else {
                  this.formInfo.esh = this.G_CONST.eshChk.unchecked;
                }
            },

            createColumns() {
                let columns = [{
                    title: this.$t('seq'),
                    align: "center",
                    width: 50,
                    dataIndex: 'rowIndex',
                    customRender: function (t, r, index) {
                        return parseInt(index) + 1;
                    }
                }];
                const allColumns = this.allColumns;
                for(var i = 0; i < allColumns.length; i++) {
                    const col = allColumns[i];
                    if(!col.exclude || !col.exclude.includes(this.formInfo.zcctype)) {
                        columns.push(col);
                    }
                }
                this.columns = columns;
                // 更新物料号
                this.dataSource.forEach(d => {
                    d["zmatnr" + this.formInfo.zcctype] = this.formInfo.zcctype + d.matnr.substr(1);
                });
            },

            // 表单验证
            validateForm(callback) {
                this.formInfo.attachList = this.attachList;
                this.$refs.formRef.validate(valid => {
                    if(!valid) {
                        this.$message.warning(this.$t('message.allRequired'));
                        return;
                    }
                    var dataSource = [];
                    this.dataSource.forEach(item => {
                        if(item.matnr) {
                            dataSource.push(item);
                        }
                    });
                    if(!dataSource || dataSource.length == 0) {
                        this.$message.warning(this.$t('message.leastItem'));
                        return;
                    }

                    this.formInfo.items = dataSource;
                    postAction(this.url.test, this.formInfo).then(res => {
                        console.log(this.$options.name, "validateForm", res);
                        if(res.success) {
                            callback();
                        } else {
                            this.error(res.message);
                        }
                    });
                });
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
        }
    }
</script>

<style>
  @import "~@assets/css/style.css";
</style>
```


### 4.2.3 使用步骤（可参考MMS前端：CleanRepairPartsApply.vue）

1）在columns中对应列添加scopedSlots，并指明唯一的名称，如：

```html
{
                title: this.$t('parts.crItem.matnr'),
                align: "center",
                width: 150,
                dataIndex: 'matnr',
                scopedSlots: {customRender: "matnr"},
            }, {
                title: this.$t('parts.crItem.zzkeyparts'),
                align: "center",
                width: 100,
                dataIndex: 'zzkeyparts',
                scopedSlots: {customRender: "zzkeyparts"},
            },
```


2）template中定义插槽功能的实现方式，如:

```html
          <template slot="matnr" slot-scope="text, record">
            <SearchHelperCell :text="text" :params="shcParams" type="matnr" @change="handleChangeCell(record.id||record.vid, 'matnr', $event)" @click="stopPropagation" />
          </template>

          <template :slot="slot" slot-scope="text, record" v-for="slot in editorCells">
            <SelectCell v-bind:key="slot" :text="text" dictCode="COMMON_FLAG" @change="handleChangeCell(record.id||record.vid, slot, $event)" @click="stopPropagation" />
          </template>
```


注意：zzkeyparts使用的是 :slot="slot"的template，该template通过v-for="slot in editorCells"判断是否被允许使用。editorCells需在export default_data_return中定义：

```html
return{
    editorCells: ["zzkeyparts", "zzexchange", "zztcparts", "zzitdevice"],
}
```



即，注意插槽功能相同时，在同一个template中定义插槽功能的实现方式。

### 4.2.4 插槽UI问题处理

如【横向条某行中某一栏的下拉框插槽功能示例_MMS】中下拉框插槽受限于滚动条；

MMS系统解决该问题时，是在SelectCell.vue的<style>中添加如下css：

```css
  .ant-select-dropdown {
    position: fixed;
    z-index: 9998 !important;
  }
```
