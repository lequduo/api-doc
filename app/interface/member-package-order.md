###查询流量卡订购套餐记录
* 请求方式：POST
* 请求地址：http://api.qwtong.me/v1/member/package/order
* 数据格式：JSON
* 请求参数：

参数名称|类型|是否必须|注释
:------------|:------------|:------------
app_id|string|必须|客户端用户ID
serial_no|string|必须|卡号/自定义卡号/iccid后10位
state|int|可选|套餐状态 [0-全部 1-正常 2-过期 3-未使用]（不填默认“正常”）
timestamp|int|必须|接口调用时间戳
sign|string|必须|参数签名


* 请求报文样例

```
POST http://api.qwtong.me/v1/member/info HTTP/1.1
Host: api.xunion.me
Content-Type: application/json

{
	"app_id": "iotbf42fef8f3bkgfjtxjzy",
	"serial_no": "87000001",
	"state": 1,
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
		"serial_no" => "87000001",
		"custom_no" => "1000000000",
		"iccid_suffix" => "1000000000",
		"packages": [
			{
				"product_no": "110100_2048",
				"name": "中国移动物联卡2G(3个月有效期)",
				"start_time": "2017-01-01",
				"end_time": "2017-03-31",
				"state": "1",
				"origin_price": "4.00",
				"fee": "3.00",
				"data_value": "2048",
				"month": "3",
				"level": "2",
				"eft_type": "0"
			},
			{
				"product_no": "110100_1024",
				"name": "中国移动物联卡1G(1个月有效期)",
				"start_time": "2016-10-01",
				"end_time": "2016-10-31",
				"state": "2",
				"origin_price": "2.00",
				"fee": "1.00",
				"data_value": "1024",
				"month": "1",
				"level": "2",
				"eft_type": "0"
			}
		]
	}
}
```
* 返回说明：

参数名称|类型|注释
:------------|:------------|:------------
serial_no|string|卡号
custom_no|string|自定义卡号
iccid_suffix|string|iccid后10位
product_no|string|套餐编码
name|string|套餐名称
start_time|string|套餐开始日期
end_time|string|套餐结束日期
state|string|套餐状态["1"-正常 "2"-过期 "3"-未使用]
origin_price|string|原价
fee|string|费用
data_value|string|流量值
month|string|有效月数
level|string|套餐级别["1"-基础包 "2"-叠加包 "3"-跨月包 "4"-加餐包]
eft_type|string|有效类型["0"-全国有效 "1"-省内有效]

---