# 1 String[ ]与List<String>相互转换

```
// String[ ] （ data.get(flag + 6) ）转换成  List<String>
import java.util.Arrays;
List<String> list = Arrays.asList(data.get(flag + 6));
String DescInEN = list.get(1);
```


# 2 String常用函数

## 2.1 String 按照逗号转换成List

```
String str ="1,2,3";
List<String> list = str.split("\\r?\\n")
// 排除String中有回车时的影响，详见：https://blog.csdn.net/v6543210/article/details/106499573#:~:text=java%20%E5%A4%84%E7%90%86%E5%AD%97%E7%AC%A6%E4%B8%B2%E7%9A%84%E6%97%B6%E5%80%99,%E9%9C%80%E8%A6%81%E5%B0%86%E6%96%87%E6%9C%AC%E6%8C%89%E8%A1%8C%E5%88%86%E5%89%B2%EF%BC%8C%E4%B8%80%E8%88%AC%E4%BD%BF%E7%94%A8string.split%20%28%22n%22%29%2C
```


# 3 QueryWrapper_Page_Service层_IPage或者List

```java
【顺序】
QueryWrapper ——》Page ——》Service层 ——》 IPage或者List

【方法简述】
①实例化一个QueryWrapper构造器【查询全部数据】：queryWrapper
②实例化一个Page构造器【分页要求】：page
③queryWrapper.in等方式查询【查询全部数据】
④实例化一个IPage构造器，并利用Service.page(page, queryWrapper) 获得分页后的数据
【Service.page(page, queryWrapper) 函数用于分页】——【Service层page函数用于自动分页】
【Service.page(page, queryWrapper).getRecords() 将分页数据赋给List】


【例一】
/**
 * PR 查询 (一般查询用)
 * 
 * @param para
 * @param pageNo
 * @param pageSize
 * @param req
 * @return
 */
@RequestMapping(value = "/list4Close", method = RequestMethod.GET)
public Result<IPage<ErpPRHeader>> list4Close(PRMainPage para,
	@RequestParam(name = "pageNo", defaultValue = "1") Integer pageNo,
	@RequestParam(name = "pageSize", defaultValue = "10") Integer pageSize, 
	HttpServletRequest req) 
	{
	Result<IPage<ErpPRHeader>> result = new Result<IPage<ErpPRHeader>>();
	QueryWrapper<ErpPRHeader> queryWrapper = new QueryWrapper<ErpPRHeader>();
		
	String username = JwtUtil.getUserNameByToken(req);
//	queryWrapper.eq("submit_User", username);
//	queryWrapper.eq("DEL_FLAG", "N");
//	queryWrapper.eq("status", FlowStatus.COMPLETED.getCode());
	
//	if (!StringUtils.isEmpty(username)) {
//		queryWrapper_EKGRP.like("ekgrp", para.getCode());
//	}
		
	// 查询所在采购组
	QueryWrapper<ErpHEkgrp> queryWrapper_EKGRP = new QueryWrapper<ErpHEkgrp>();
	Page<ErpHEkgrp> page_EKGRP = new Page<ErpHEkgrp>(1, 100);
	if (!StringUtils.isEmpty(username)) {
		queryWrapper_EKGRP.eq("ektel", username);
	}
	List<ErpHEkgrp> listEkgrp = ekgrpService.page(page_EKGRP, queryWrapper_EKGRP).getRecords();
	List<String> eKGRPList = new ArrayList<String>();
	for(ErpHEkgrp entity : listEkgrp) {
		eKGRPList.add(entity.getEkgrp());
	}
	// 按照采购组查询item表
	List<ErpPRDetail> itemsALL = new ArrayList<ErpPRDetail>();
	for(String ekgrp : eKGRPList) {
		List<ErpPRDetail> items = prService.getPRDetailByEKGRP(ekgrp);
		itemsALL.addAll(items);
	}
		
	// 查询用户对应采购组的PR单
	List<String> headerIDList = new ArrayList<String>();
	for(ErpPRDetail entity : itemsALL) {
		if(!headerIDList.contains(entity.getPrId())) {
			headerIDList.add(entity.getPrId());
		}
	}
		
//	QueryWrapper<ErpPRDetail> queryWrapper_Items = new QueryWrapper<ErpPRDetail>();
//	Page<ErpPRDetail> page_Items = new Page<ErpPRDetail>(pageNo, pageSize);
//	IPage<ErpPRDetail> pageList_Items = ekgrpService.page(page_Items, queryWrapper_Items);
		
	String[] strArrStrings = new String[headerIDList.size()];
	String resultString = "";
		
	for(int i=0;i<=headerIDList.size()-1;i++){
		strArrStrings[i] = (String) headerIDList.get(i);
	}

	for(int j=0;j<=strArrStrings.length-1;j++){
		if(j < strArrStrings.length-1){
			resultString += strArrStrings[j] + ",";
		}else{
			resultString += strArrStrings[j];	
		}
	}
		
		
	queryWrapper.eq("DEL_FLAG", "N");
	queryWrapper.eq("status", FlowStatus.COMPLETED.getCode());
	queryWrapper.in("ID", strArrStrings);
		

		
//	if(!HeaderIDList.isEmpty()) {
//		queryWrapper.in("ID", HeaderIDList);
//	};
		
	// PR No
	if (!StringUtils.isEmpty(para.getPrNo())) {
		queryWrapper.like("pr_No", para.getPrNo());
	}
		
	// Submit Date
	if (!StringUtils.isEmpty(para.getSubmitDateFrom())) {
		queryWrapper.ge("SUBMIT_DATE", StringUtils.replace(para.getSubmitDateFrom(), "-", ""));
	}
		
	// 获得
		
	queryWrapper.isNotNull("pr_No");

	queryWrapper.orderByDesc("pr_No");

	Page<ErpPRHeader> page = new Page<ErpPRHeader>(pageNo, pageSize);
	IPage<ErpPRHeader> pageList = prService.page(page, queryWrapper);

	result.setSuccess(true);
	result.setResult(pageList);
	return result;
	}


【例二】
@RequestMapping(value = "/anln1/list", method = RequestMethod.GET)
public Result<IPage<ErpHAnln1>> queryAnln1List(SearchHelpVO para,
	@RequestParam(name = "pageNo", defaultValue = "1") Integer pageNo,
	@RequestParam(name = "pageSize", defaultValue = "10") Integer pageSize, 
	HttpServletRequest req) {
	Result<IPage<ErpHAnln1>> result = new Result<IPage<ErpHAnln1>>();
	QueryWrapper<ErpHAnln1> queryWrapper = new QueryWrapper<ErpHAnln1>();
	if (!StringUtils.isEmpty(para.getCode())) {
		queryWrapper.like("anln1", para.getCode());
	}
	if (!StringUtils.isEmpty(para.getName())) {
		queryWrapper.like("mcoa1", para.getName());
	}
	queryWrapper.orderByAsc("anln1");
	Page<ErpHAnln1> page = new Page<ErpHAnln1>(pageNo, pageSize);
	IPage<ErpHAnln1> pageList = anln1Service.page(page, queryWrapper);
	result.setSuccess(true);
	result.setResult(pageList);
	return result;
}
```


# 4 泛型

可参考：https://blog.csdn.net/jiahao1186/article/details/91411606

```java
【实例代码，如：Result<String>】
	/**
	 * 给指定角色添加用户
	 *
	 * @param
	 * @return
	 */
	// @RequiresRoles({"admin"})
	@RequestMapping(value = "/addSysUserRole", method = RequestMethod.POST)
	public Result<String> addSysUserRole(@RequestBody SysUserRoleVO sysUserRoleVO) {
		Result<String> result = new Result<String>();
		try {
			String sysRoleId = sysUserRoleVO.getRoleId();
			for (String sysUserId : sysUserRoleVO.getUserIdList()) {
				SysUserRole sysUserRole = new SysUserRole(sysUserId, sysRoleId);
				QueryWrapper<SysUserRole> queryWrapper = new QueryWrapper<SysUserRole>();
				queryWrapper.eq("role_id", sysRoleId).eq("user_id", sysUserId);
				SysUserRole one = sysUserRoleService.getOne(queryWrapper);
				if (one == null) {
					sysUserRoleService.save(sysUserRole);
				}

			}
			result.setMessage("添加成功!");
			result.setSuccess(true);
			return result;
		} catch (Exception e) {
			log.error(e.getMessage(), e);
			result.setSuccess(false);
			result.setMessage("出错了: " + e.getMessage());
			return result;
		}
	}
```


# 5 后端查询数据库三种方式

```java
【实例来源：PRController.java文件中——url:  /list4Close】
方法一①使用QueryWrapper构造器（使用entity类对应相应表——entity.TableName）
	——实例化某类型QueryWrapper，如QueryWrapper<ErpHEkgrp> queryWrapper_EKGRP = new QueryWrapper<ErpHEkgrp>();
		// 查询所在采购组
		QueryWrapper<ErpHEkgrp> queryWrapper_EKGRP = new QueryWrapper<ErpHEkgrp>();
		Page<ErpHEkgrp> page_EKGRP = new Page<ErpHEkgrp>(1, 100);
		if (!StringUtils.isEmpty(username)) {
			queryWrapper_EKGRP.eq("ektel", username);
		}
		List<ErpHEkgrp> listEkgrp = ekgrpService.page(page_EKGRP, queryWrapper_EKGRP).getRecords();
		List<String> eKGRPList = new ArrayList<String>();
		for(ErpHEkgrp entity : listEkgrp) {
			eKGRPList.add(entity.getEkgrp());
		}
方法二②调用Service层——逐层查询（在Mapper.Impl层指定对应表，表名可用小写：select * from erp_t_pr_detail where ekgrp = #{ekgrp}）
【controller层】
注意导入全部所需文件
import org.jeecg.modules.erp.service.IPRService;

public class PRController {

	@Autowired
	private IPRService prService;

		// 按照采购组查询item表
		List<ErpPRDetail> itemsALL = new ArrayList<ErpPRDetail>();
		for(String ekgrp : eKGRPList) {
			List<ErpPRDetail> items = prService.getPRDetailByEKGRP(ekgrp);
			itemsALL.addAll(items);
		}
}

【Service层】
注意导入全部所需文件
package org.jeecg.modules.erp.service;

import java.util.ArrayList;
import java.util.List;

import org.jeecg.modules.erp.entity.ErpPRDetail;
import org.jeecg.modules.erp.entity.ErpPRHeader;
import org.jeecg.modules.erp.entity.ErpPRVendor;
import org.jeecg.modules.erp.vo.PRMainPage;

import com.baomidou.mybatisplus.core.metadata.IPage;
import com.baomidou.mybatisplus.extension.service.IService;

public interface IPRService extends IService<ErpPRHeader> {
	
	List<ErpPRDetail> getPRDetailByEKGRP(String ekgrp);
}
【ServiceImpl层】
注意导入全部所需文件
package org.jeecg.modules.erp.service.impl;

import org.jeecg.modules.erp.service.mapper.PRDetailMapper;

@Service
public class PRServiceImpl extends ServiceImpl<PRHeaderMapper, ErpPRHeader> implements IPRService {

	@Autowired
	PRDetailMapper detailMapper;

	@Override
	public List<ErpPRDetail> getPRDetailByEKGRP(String ekgrp) {
		return detailMapper.getPRDetailByEKGRP(ekgrp);
	}
【Mapper层】
注意导入全部所需文件
package org.jeecg.modules.erp.service.mapper;

import java.util.List;

import org.apache.ibatis.annotations.Param;
import org.jeecg.modules.erp.entity.ErpPRDetail;

import com.baomidou.mybatisplus.core.mapper.BaseMapper;

public interface PRDetailMapper extends BaseMapper<ErpPRDetail> {
	public List<ErpPRDetail> getPRDetailByEKGRP(@Param("ekgrp") String ekgrp);
}
【Mapper.Impl层】
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="org.jeecg.modules.erp.service.mapper.PRDetailMapper">
	<select id="getPRDetailByEKGRP" resultType="org.jeecg.modules.erp.entity.ErpPRDetail">
        select * from erp_t_pr_detail where ekgrp = #{ekgrp}
    </select>

</mapper>




方法三③QueryWrapper的exist写sql语句进行查询
	@GetMapping(value = "/print/list")
	public Result queryPagePrintList(BpmTPoHeader para,
			@RequestParam(name = "pageNo", defaultValue = "1") Integer pageNo,
			@RequestParam(name = "pageSize", defaultValue = "10") Integer pageSize, HttpServletRequest request) {
		QueryWrapper<BpmTPoHeader> queryWrapper = QueryGenerator.initQueryWrapper(para, request.getParameterMap());
		queryWrapper.eq("DEL_FLAG", Constant.DELETE_N);

		// 行项目查询条件 matnr knttp banfn;
		StringBuilder subSql = new StringBuilder();
		subSql.append("SELECT * FROM ERP_T_PO_ITEM WHERE DEL_FLAG='" + Constant.DELETE_N
				+ "' AND ERP_T_PO_HEADER.ID=ERP_T_PO_ITEM.HEAD_ID ");
		if (StringUtils.isNotBlank(para.getTxz01())) {
			subSql.append("AND TXZ01 like '%" + para.getTxz01() + "%' ");
		}
		if (StringUtils.isNotBlank(para.getMatnr())) {
			subSql.append("AND MATNR like '%" + para.getMatnr() + "%' ");
		}
		if (StringUtils.isNotBlank(para.getKnttp())) {
			subSql.append("AND KNTTP='" + para.getKnttp() + "' ");
		}
		if (StringUtils.isNotBlank(para.getBanfn())) {
			subSql.append("AND BANFN like '%" + para.getBanfn() + "%' ");
		}
		queryWrapper.exists(subSql.toString());

		queryWrapper.orderByDesc("nvl(SAP_CREATE_DATE,CREATE_TIME)");
		Page<BpmTPoHeader> page = new Page<>(pageNo, pageSize);
		IPage<BpmTPoHeader> pageList = poHeaderService.page(page, queryWrapper);

		// 查询行项目, 取第一条记录
		List<BpmTPoHeader> headerList = pageList.getRecords();
		headerList.forEach(e -> {
			QueryWrapper<BpmTPoItem> iqueryWrapper = new QueryWrapper<>();
			iqueryWrapper.eq("HEAD_ID", e.getId());
			iqueryWrapper.eq("DEL_FLAG", Constant.DELETE_N);
			iqueryWrapper.orderByAsc("TO_NUMBER(EBELP)");
			List<BpmTPoItem> items = poItemService.list(iqueryWrapper);
			if (CollectionUtils.isNotEmpty(items)) {
				e.setItem(items.get(0));
			}
		});
		return Result.OK(pageList);
	}
```


# 6 前后端的HttpServlet交互

可参考：https://blog.csdn.net/qq_28657369/article/details/77926481

后端接收到的前端请求：httpServletRequest

后端发送给前端的响应：HttpServletResponse 

# 7 后端传值给前端时，常用数据类型转换总结（Map与entity）

键值对集合 Map的使用：https://blog.csdn.net/Bangser/article/details/102235116

不指定函数return类型：return Return.ok(entity)

map与entity相互转换：https://www.cnblogs.com/zhainan-blog/p/12009523.html
