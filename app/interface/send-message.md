###发送短信
* 请求方式：POST
* 请求地址：http://api.qwtong.me/v1/send/message
* 数据格式：JSON
* 请求参数：

参数名称|类型|是否必须|注释
:------------|:------------|:------------
app_id|string|必须|客户端用户ID
serial_no|string|必须|卡号/自定义卡号/iccid后10位
content|string|必须|短信内容
format|int|必须|短信格式（0:ASCLL串 8:UCS2编码）
timestamp|int|必须|接口调用时间戳
sign|string|必须|参数签名


* 请求报文样例

```
POST http://api.qwtong.me/v1/send/message HTTP/1.1
Host: api.xunion.me
Content-Type: application/json

{
	"app_id" : "iotbf42fef8f3bkgfjtxjzy",
	"serial_no" : "87000001",
	"content" : "接口测试",
	"format" : 0,
	"timestamp" : 1488189436,
	"sign" : "1CB005822179219AC4FD07320941AA9B3E45AAA9"
}
```

* 返回JSON数据：

```
{
	"errcode": 0,
	"errmsg": "success",
	"data": {
		"transaction_id": "201705081115233958611336",
		"serial_no" => "87000001",
		"custom_no" => "1000000000",
		"iccid_suffix" => "1000000000",
	}
}
```
* 返回说明：

参数名称|类型|注释
:------------|:------------|:------------
transaction_id|string|业务流水号
serial_no|string|卡号
custom_no|string|自定义卡号
iccid_suffix|string|iccid后10位

* <font color='red'>特别说明</font>：

>该接口返回成功表示成功加入短信发送队列，发送结果将推送至接口回调地址（发送结果推送请查看左侧<font color='red'>2.10短信推送</font>）

---