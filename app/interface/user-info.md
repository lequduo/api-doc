###查询账户基本信息
* 请求方式：POST
* 请求地址：http://api.qwtong.me/v1/user/info
* 数据格式：JSON
* 请求参数：

参数名称|类型|是否必须|注释
:------------|:------------|:------------
app_id|string|必须|客户端用户ID
timestamp|int|必须|接口调用时间戳
sign|string|必须|参数签名


* 请求报文样例

```
POST http://api.qwtong.me/v1/member/info HTTP/1.1
Host: api.xunion.me
Content-Type: application/json

{
	"app_id": "iotbf42fef8f3bkgfjtxjzy",
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
		"name": "张三",
		"truename": "李四",
		"rank": "1",
		"balance": "10000.00"
	}
}
```
* 返回说明：

参数名称|类型|注释
:------------|:------------|:------------
name|string|用户名
truename|string|真实姓名
rank|string|会员等级["1"-黄金代理 "2"-白银代理 "3"-青铜代理 "4"-VIP代理 "5"-钻石代理]
balance|string|账户余额

---