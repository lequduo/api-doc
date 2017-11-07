###开关机（暂不对外开放）
* 请求方式：POST
* 请求地址：http://api.qwtong.me/v1/member/startshut
* 数据格式：JSON
* 请求参数：

参数名称|类型|是否必须|注释
:------------|:------------|:------------
app_id|string|必须|客户端用户ID
serial_no|string|必须|卡号/自定义卡号/iccid后10位
action|int|必须|操作类型[1-开机 2-关机]
timestamp|int|必须|接口调用时间戳
sign|string|必须|参数签名


* 请求报文样例

```
POST http://api.qwtong.me/v1/member/startshut HTTP/1.1
Host: api.xunion.me
Content-Type: application/json

{
	"app_id": "iotbf42fef8f3bkgfjtxjzy",
	"serial_no": "87000001",
	"action": 1,
	"timestamp": 1488247264,
	"sign": "D227338B98CFEFB5B4753012E92564BF202C23FE",
}
```

* 返回JSON数据：

```
{
	"errcode": 0,
	"errmsg": "success"
}
```
* 返回说明：

>“errcode”为0表示成功加入操作队列，<font color='blue'>操作结果以回调方式返回</font>，回调地址请联系客服配置。

* 回调数据样例（JSON格式）

```
{
	"action_type": 2,
	"serial_no": "86000000",
	"operate_value": "1",
	"status": "2",
	"errmsg": "卡已过期,无法执行复机指令"
}
```
* 回调数据说明：

参数名称|类型|注释
:------------|:------------|:------------
action_type|int|回调类型 [1-充值回调 2-开关机回调]
serial_no|string|卡号
operate_value|string|操作类型 ["1"-开机 "2"-关机]
status|string|操作状态 ["0"-未处理 "1"-处理中 "2"-失败 "3"-成功]
errmsg|string|错误信息

* 请在接收到回调后返回：

```
{
	"errcode": 0,
	"errmsg": "success",
}
```
><font color='red'>返回上面数据以便确认接收到回调</font>，如未收到回调将重复回调三次


---
