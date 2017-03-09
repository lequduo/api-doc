###查询充值订单基本信息
* 请求方式：POST
* 请求地址：http://api.qwtong.me/v1/order/info
* 数据格式：JSON
* 请求参数：

参数名称|类型|是否必须|注释
:------------|:------------|:------------
app_id|string|必须|客户端用户ID
order_no|string|必须|订单号
timestamp|int|必须|接口调用时间戳
sign|string|必须|参数签名


* 请求报文样例

```
POST http://api.qwtong.me/v1/order/info HTTP/1.1
Host: api.xunion.me
Content-Type: application/json

{
	"app_id": "iotbf42fef8f3bkgfjtxjzy",
	"order_no": "201702281435579209569730",
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
		"order_no": "201702281435579209569730",
		"serial_no": "86000000",
		"product_no": "110100_1024",
		"eft_month": "0",
		"status": "1",
		"fee": "3.00"
	}
}
```
* 返回说明：

参数名称|类型|注释
:------------|:------------|:------------
order_no|string|订单号
serial_no|string|卡号
product_no|string|套餐编码
eft_month|string|生效类型 ["0"-马上生效 "1"-次月生效]
status|string|订单状态 ["0"-未处理 "1"-处理中 "2"-失败 "3"-成功]
fee|string|费用

---
