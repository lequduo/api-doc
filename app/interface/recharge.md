###充值（暂不对外开放）
* 请求方式：POST
* 请求地址：http://api.qwtong.me/v1/recharge
* 数据格式：JSON
* 请求参数：

参数名称|类型|是否必须|注释
:------------|:------------|:------------
app_id|string|必须|客户端用户ID
serial_no|string|必须|卡号/自定义卡号/iccid后10位
product_no|string|必须|套餐编码
effective|int|必须|生效类型[0-当月生效 1-次月生效]
timestamp|int|必须|接口调用时间戳
sign|string|必须|参数签名


* 请求报文样例

```
POST http://api.qwtong.me/v1/recharge HTTP/1.1
Host: api.xunion.me
Content-Type: application/json

{
	"app_id": "iotbf42fef8f3bkgfjtxjzy",
	"serial_no": "87000001",
	"product_no": "100000_1024",
	"effective": 1,
	"timestamp": 1488247264,
	"sign": "D227338B98CFEFB5B4753012E92564BF202C23FE",
}
```

* 返回JSON数据：

```
{
	"errcode": 0,
	"errmsg": "success",
	"order_no": "201710171017017107051654"
}
```
* 返回说明：

参数名称|类型|注释
:------------|:------------|:------------
order_no|string|订单号

>“errcode”为0表示成功加入充值队列，充值结果根据订单号主动查询

---
