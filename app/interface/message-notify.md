###短信推送

>1. 短信推送分为发送结果回调推送和接收短信推送两种
>2. 推送地址为开放平台参数内的<font color='red'>接口回调地址</font>

1.发送结果回调推送
* 推送JSON数据：

参数名称|类型|注释
:------------|:------------|:------------
action|string|推送类型（固定值：'submit_resp'）
transaction_id|string|业务流水号
status|int|发送状态[2-发送失败 3-发送成功]
errmsg|string|错误信息


* 推送数据样例

```
{
	"action": "submit_resp",
	"data": {
		"transaction_id": "201705081115233958611336",
		"status" => 2,
		"errmsg" => "消息序号重复",
	}
}
```

2.接收短信推送
* 推送JSON数据：

参数名称|类型|注释
:------------|:------------|:------------
action|string|推送类型（固定值：'deliver_resp'）
transaction_id|string|业务流水号
serial_no|string|卡号
custom_no|string|自定义卡号
iccid_suffix|string|iccid后10位
msg_content|string|短信内容


* 推送数据样例

```
{
	"action": "deliver_resp",
	"data": {
		"transaction_id": "201705081115233958611336",
		"serial_no" => "87000001",
		"custom_no" => "1000000000",
		"iccid_suffix" => "1000000000",
		"msg_content" => "消息测试",
	}
}
```

---