###接口返回说明
* 所有接口都会统一返回errcode和errmsg两个参数，errcode 不为 0 时 errmsg 代表错误信息，errcode 为 0 时返回 data 数据，内容为不同接口的业务数据
* 正常的返回demo：
```json
{
	"errcode": 0,
	"errmsg": "success",
	"data": []
}
```
* 错误的返回demo：
```json
{
	"errcode": 50000,
	"errmsg": "未知错误"
}
```