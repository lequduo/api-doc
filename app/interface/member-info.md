###查询流量卡基本信息
* 请求方式：POST
* 请求地址：http://api.qwtong.me/v1/member/info
* 数据格式：JSON
* 请求参数：

参数名称|类型|是否必须|注释
:------------|:------------|:------------
app_id|string|必须|客户端用户ID
serial_no|string|必须|卡号/自定义卡号/iccid后10位
timestamp|int|必须|接口调用时间戳
sign|string|必须|参数签名
data_update|bool|可选|向运营商更新流量 ["true"-更新 "false"-不更新]


* 请求报文样例

```
POST http://api.qwtong.me/v1/member/info HTTP/1.1
Host: api.xunion.me
Content-Type: application/json

{
	"app_id": "iotbf42fef8f3bkgfjtxjzy",
	"serial_no": "87000001",
	"timestamp": 1488247264,
	"sign": "D227338B98CFEFB5B4753012E92564BF202C23FE",
	"data_update": "true",
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
		"gprs_status" => "1",
		"sim_status" => "1",
		"resources_count" => "1024",
		"ieavings_count" => "1024",
		"used_res_count" => 0,
	}
}
```
* 返回说明：

参数名称|类型|注释
:------------|:------------|:------------
serial_no|string|卡号
custom_no|string|自定义卡号
iccid_suffix|string|iccid后10位
gprs_status|string|GPRS状态 ["0"-关闭 "1"-开启 "3"-正在关闭 "4"-正在开启]
sim_status|string|开机状态 ["0"-停机 "1"-开机 "2"-待激活 "3"-正在关机 "4"-正在开机]
resources_count|string|当月流量总量(M)
ieavings_count|string|当月剩余流量(M)
used_res_count|int|当月已用总量(M)

---