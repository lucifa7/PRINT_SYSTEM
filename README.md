# 单证 标签 面单打印平台

服务器-172.20.70.32

## 一 登录接口

http://[server]/api/login/{username}/{password}

## 二 打印接口

http://[server]/api/submitTask

POST application/json

` {
    "msgid": "1234567890",
    "client": "ERP",
    "sysgroup": "ASIA",
    "busstype": "ORDER",
    "model": "SHIP",
    "printtype": "MAIL",
"maillist": "1539601747@qq.com",
"subject": "飞力达国际物流股份有限公司单证",
    "printername": "PDF",
    "orderkey": "12345678",
    "copies": 1,
    "template": "ORDER04",
    "xmldata": "<?xml version='1.0' encoding='UTF-8'?><!--Type:ORDER04 WHSEID=WMWHSE5--><labels ><label><WHSEID>WMWHSE5</WHSEID><STORERKEY>DEKJG0100</STORERKEY><COMPANY>达尔科技股份有限公司</COMPANY><SUSR3>达尔科技</SUSR3><ADDDATE>2020-08-04 10:52:23.0</ADDDATE><CONSIGNEEKEY>WCZTY0705</CONSIGNEEKEY><S1COMPANY>纬创资通（昆山）有限公司(F236)</S1COMPANY><REQUESTEDSHIPDATE>2020-08-04 17:00:00.0</REQUESTEDSHIPDATE><GNTYPE>G</GNTYPE><TRADINGPARTNER>W101-F236昆山经济技术开发区鸿雁路88号</TRADINGPARTNER><SKU>SMAJ26CA-13-F</SKU><LOTTABLE07>125-00332-S$AA</LOTTABLE07><SUSR1/><SUSR2>ZSTS    R2_SA;</SUSR2><ODSUSR3>14773901-00100-1</ODSUSR3><SUSR4/><QTY>5000</QTY><DESCR/><JINYONG/><UDF2>ROHS2+HF</UDF2><NOTES2/><SUSR20/><UDF11/><TAG/><ORDERKEY>0000769864</ORDERKEY><PUID>10000908</PUID></label><service><SERVICENAME>实际总箱/出仓</SERVICENAME></service><service><SERVICENAME>实际总托盘数/出仓</SERVICENAME></service><service><SERVICENAME>实际散箱数/出仓</SERVICENAME></service><service><SERVICENAME>实际MPQ数/拆拣</SERVICENAME></service><service><SERVICENAME>实际盘数/拆拣</SERVICENAME></service><service><SERVICENAME>标准操作/拆拣</SERVICENAME></service><service><SERVICENAME>标准操作/耗材提供</SERVICENAME></service><service><SERVICENAME>实际总箱/耗材提供</SERVICENAME></service><service><SERVICENAME>实际条数/D/C采集</SERVICENAME></service><service><SERVICENAME>实际条数/L/T采集</SERVICENAME></service><service><SERVICENAME>实际制标张数/制标</SERVICENAME></service><service><SERVICENAME>实际贴标张数/贴标</SERVICENAME></service><service><SERVICENAME>实际散箱数/贴标</SERVICENAME></service></labels>",
    "username": "ERP",
    "password": "04edb07870ca03aa3a049476b716e70c"
}` 

返回样例 

` {
    "result": "OK",
    "orderkey": "12345678",
    "client": "ERP",
    "id": 111,
    "message": "任务添加成功",
    "timestamp": 1597644469614
} ` 

其中id为系统任务序号

### 字段说明

序号|字段（是否必填）|	说明|	取值说明
---|----|----|---
1	| msgid	| 消息id(否) |	
2	| client |	系统代码（是）|	
3	| sysgroup |	区域组织（否）	|
4	| busstype	| 业务类型（否）	|
5	| model	| 模块（否）	|
6	| printtype	| 打印类型（否）|	邮件打印时:MAIL
7	| maillist |	收件人（否）|	MAIL打印时必填
8 |	subject	| 邮件主题（否）	|
9 |	printername	| 打印机名称（是）|	MAIL打印时：PDF
10 |	orderkey |	订单号（是）|	
11 |	copies |	份数（是）	|
12 |	template |	模板名称(是)	|
13 |	xmldata 	| 打印数据（是）|	Xpath:/labels/label
14 |	username	| 用户名（否）|	
15 |	password	| 密码（否）	|
16 |	token	|TOKEN（否）|	用户名+密码和token必须有一组

username 对应客户系统代码

password 对应客户系统识别码

## 三 XML打印

将文件投放到服务器扫描目录（使用FTP协议）
文件命名规则：xxxxx@[打印机名称].xml
labels属性必须包含如下
_FORMAT：模板名称
_ORDERKEY：单号
_PRINTERNAME：打印机注册名
_QUANTITY：份数
_CLIENT:系统代码
_TOKEN:TOKEN（或者使用_PASSWORD）
### 栗子：
12345678@PDF.xml

 ` <?xml version="1.0" encoding="UTF-8"?>
<labels _FORMAT="ORDER04" _ORDERKEY="0000769864" _PRINTERNAME="TOPDF" _MAILLIST="1539601747@qq.com" _PRINTTYPE="MAIL" _QUANTITY="1" _CLIENT="ERP" _TOKEN="47241f895f0ef85b258559fa1fdaf63e">
<label>
<WHSEID>WMWHSE5</WHSEID>
<STORERKEY>DEKJG0100</STORERKEY>
<COMPANY>达尔科技股份有限公司</COMPANY>
<SUSR3>达尔科技</SUSR3>
<ADDDATE>2020-08-04 10:52:23.0</ADDDATE>
<CONSIGNEEKEY>WCZTY0705</CONSIGNEEKEY>
<S1COMPANY>纬创资通（昆山）有限公司(F236)</S1COMPANY>
<REQUESTEDSHIPDATE>2020-08-04 17:00:00.0</REQUESTEDSHIPDATE>
<GNTYPE>G</GNTYPE>
<TRADINGPARTNER>W101-F236昆山经济技术开发区鸿雁路88号</TRADINGPARTNER>
<SKU>SMAJ26CA-13-F</SKU>
<LOTTABLE07>125-00332-S$AA</LOTTABLE07>
<SUSR1/>
<SUSR2>ZSTS    R2_SA;</SUSR2>
<ODSUSR3>14773901-00100-1</ODSUSR3>
<SUSR4/>
<QTY>5000</QTY>
<DESCR/>
<JINYONG/>
<UDF2>ROHS2+HF</UDF2>
<NOTES2/>
<SUSR20/>
<UDF11/>
<TAG/>
<ORDERKEY>0000769864</ORDERKEY>
<PUID>10000908</PUID>
</label>
<service>
<SERVICENAME>实际总箱/出仓</SERVICENAME>
</service>
<service>
<SERVICENAME>实际总托盘数/出仓</SERVICENAME>
</service>
<service>
<SERVICENAME>实际散箱数/出仓</SERVICENAME>
</service>
<service>
<SERVICENAME>实际MPQ数/拆拣</SERVICENAME>
</service>
<service>
<SERVICENAME>实际盘数/拆拣</SERVICENAME>
</service>
<service>
<SERVICENAME>标准操作/拆拣</SERVICENAME>
</service>
<service>
<SERVICENAME>标准操作/耗材提供</SERVICENAME>
</service>
<service>
<SERVICENAME>实际总箱/耗材提供</SERVICENAME>
</service>
<service>
<SERVICENAME>实际条数/D/C采集</SERVICENAME>
</service>
<service>
<SERVICENAME>实际条数/L/T采集</SERVICENAME>
</service>
<service>
<SERVICENAME>实际制标张数/制标</SERVICENAME>
</service>
<service>
<SERVICENAME>实际贴标张数/贴标</SERVICENAME>
</service>
<service>
<SERVICENAME>实际散箱数/贴标</SERVICENAME>
</service>
</labels>`

XPATH
Xml数据源请采用 /labels/label 结构
## 四 支持汉字字体

支持的字体
楷体|宋体|仿宋|隶书|黑体

##五 平台简介

### 1登录界面

![image](https://github.com/lucifa7/PRINT/raw/master/pic/%E7%99%BB%E5%BD%95.png)
 
### 2模板管理
 
### 3打印机管理
 
### 4 打印任务预览
 
 
### 5 系统配置
 
### 6 客户系统管理
 

### 7 Adobe PDF打印PDF
 
### 8 自动发送邮件预览
 

### 9部署说明

系统数据库初始化预置了一台PDF打印机和一个客户系统（ERP）和邮件发送任务和PDF路径。

如果以下项未设置，将使用与系统同目录路径

[pdfdir]  -PDF生成路径。

[tempdir] –模板路径（请将模板文件放置于此）。

[scandir] –XML文件扫描路径（FTP投递任务文件位置）。

[useadobe]-邮寄PDF或者打印电子档时是否使用Adobe 虚拟打印机（1是，0使用Jasper打印机）-注意Jasper打印机的中文字体支持情况。

### 10 windows 服务
使用PS或者命令行还启动程序
	Java –jar printcenter.jar
---使用nssm制作服务暂时打印异常。
## 六 打印客户端
### 1系统简介
软件结构
 
运行状况
 
### 2 系统管理
1.1 系统初始化
 
将软件工作目录初始化到当前目录（不允许带中文路径）
1.2 添加打印机
 
其中API|FTP选项是新增的打印机是否参与API或者FTP获取任务
如果使用Adobe PDF 打印机，请预先设置好打印路径和无人值守选项。

1.3 删除打印机
 
1.4 系统参数
 
1.4 打印模板
 
如果FTP路径包含模板管理功能，怎可使用同步模板功能，否则，请直接将打印模板放置到模板路径下。

1.5 打印服务（各状态见软件标题）
 

