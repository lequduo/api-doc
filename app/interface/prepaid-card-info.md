###查询卡密基本信息
* 请求方式：POST
* 请求地址：http://api.qwtong.me/v1/prepaid/card/info
* 数据格式：JSON
* 请求参数：

参数名称|类型|是否必须|注释
:------------|:------------|:------------
app_id|string|必须|客户端用户ID
serial_no|string|必须|卡密号
timestamp|int|必须|接口调用时间戳
sign|string|必须|参数签名


* 请求报文样例

```
POST http://api.qwtong.me/v1/member/info HTTP/1.1
Host: api.xunion.me
Content-Type: application/json

{
	"app_id": "iotbf42fef8f3bkgfjtxjzy",
	"serial_no": "170222734322000000",
	"timestamp": 1488247264,
	"sign": "D227338B98CFEFB5B4753012E92564BF202C23FE",
}
```

* 返回JSON数据：

```
{
	"errcode": 0,
	"errmsg": "success",
	"data": {
		"serial_no": "170222734322000000",
		"password": "88888888",
		"data_value": "1024",
		"name": "移动（全国）1G卡密(1个月有效期)",
		"fee": "2.00",
		"state": "0"
	}
}
```
* 返回说明：

参数名称|类型|注释
:------------|:------------|:------------
serial_no|string|卡密号
password|string|密码
data_value|string|流量值
name|string|卡密名称
fee|string|费用
state|string|状态["0"-未使用 "1"-已使用 "2"-冻结]

---