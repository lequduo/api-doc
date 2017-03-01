# \#大卡师开放平台对接文档

# 

# &gt;版本：v1.0.0.20170301

# &gt;爱上的机会撒

# &gt;作者：admin

# &gt;

# &gt;创建时间：2017-02-20 10:46:00

# 

# \#\#\#文档修订记录

# 版本号\|修订人\|修订日期\|修订描述

# :------------\|:------------\|:------------\|:------------

# v1.0.0.20170220\|admin\|2017-02-20\|创建文档

# 

# 

# \#\#一、通用参数说明

# 

# \#\#\#1.公共请求参数

# 参数名称\|类型\|注释

# :------------\|:------------\|:------------

# client\_id\| string \| 客户端ID

# timestamp\| int \| 接口调用当前时间的时间戳，误差在五分钟之内

# sign\| string \| 参数签名

# 

# \`\`\`json

# {

# "client\_id": "iotacc108b7305fhzljeux0",

# "timestamp": 1487560009,

# "sng": "E1F082F33F77A749D90631862A122A624ED04542"

# }

# \`\`\`

# 

# \#\#\#2.接口返回说明

# \* 所有接口都会统一返回errcode和errmsg两个参数，errcode 不为 0 时 errmsg 代表错误信息，errcode 为 0 时返回 data 数据，内容为不同接口的业务数据

# \* 正常的返回：

# \`\`\`json

# {

# "errcode": 0,

# "errmsg": "success",

# "data": \[\]

# }

# \`\`\`

# \* 错误的返回：

# \`\`\`json

# {

# "errcode": 50000,

# "errmsg": "未知错误"

# }

# \`\`\`

# 

# \#\#\#3.常见问题

# \* 所有POST请求http header设置Content-Type为application/json

# 

# 

# \#\#\#4.签名

# \* 在提交订单的时候需要将提交的数据加密签名

# \* sign 不参与加密

# \* 加密/校验流程如下：

# 

# &gt;1. 将提交的参数按照参数名进行字典序排序&lt;font color='red'&gt;\(参数排序中需要加入client\_id\)&lt;/font&gt;

# &gt;2. 将参数按 url query 方式拼接，拼接的方式样例：callback\_url=xxx&client\_id=xxx&serial\_no=xxx&timestamp=xxxx

# &gt;3. 拼接字符串最后加上 client\_secret

# &gt;4. 将最后字符串进行 sha1 加密并将字母转换成大写

# 

# \* 签名 php demo

# \`\`\`php

# /\*\*

# \* 作用：格式化参数，签名过程需要使用

# \*/

# protected function formatBizQueryParaMap\($paraMap\)

# {

# $buff = "";

# foreach \($paraMap as $k =&gt; $v\) {

# $buff .= $k . "=" . $v . "&";

# }

# $reqPar;

# if \(strlen\($buff\) &gt; 0\) {

# $reqPar = substr\($buff, 0, -1\);

# }

# return $reqPar;

# }

# 

# /\*\*

# \* 作用：生成签名

# \*/

# protected function getSign\(data, $secret\)

# {

# foreach \(data as $key =&gt; $val\) {

# $Parameters\[$key\] = $val;

# }

# //签名步骤一：按字典序排序参数并拼接

# ksort\($Parameters\);

# $string = formatBizQueryParaMap\($Parameters, false\);

# //签名步骤二：在$string后加入client\_secret

# $string = $string . $secret;

# //签名步骤三：sha1加密

# $string = sha1\($string\);

# //签名步骤四：所有字符转为大写

# $result = strtoupper\($string\);

# return $result;

# }

# 

# //调用

# $sign = getSign\(

# array\(

# 'client\_id' =&gt; $client\_id,

# 'serial\_no' =&gt; '87000001',

# 'timestamp' =&gt; 1487560009

# \),

# $secret

# \);

# 

# \`\`\`

# 

# ---

# 

# \#\#二、接口列表

# 

# \#\#\#1.查询流量卡基本信息

# \* 请求方式：POST

# \* 请求地址：[http://api.qwtong.me/v1/member/info](http://api.qwtong.me/v1/member/info)

# \* 数据格式：JSON

# \* 请求参数：

# 

# 参数名称\|类型\|是否必须\|注释

# :------------\|:------------\|:------------

# client\_id\|string\|必须\|客户端用户ID

# serial\_no\|string\|必须\|卡号

# timestamp\|int\|必须\|接口调用时间戳

# 

# 

# \* 请求报文样例

# \`\`\`

# POST [http://api.qwtong.me/v1/member/info](http://api.qwtong.me/v1/member/info) HTTP/1.1

# Host: api.xunion.me

# Content-Type: application/json

# 

# {

# "client\_id": "iot3355e802d44ay95yeev2",

# "serial\_no": "87000001",

# "timestamp": 1487560009

# }

# \`\`\`

# 

# \* 返回JSON数据：

# 

# \`\`\`

# {

# "errcode": 0,

# "errmsg": "success",

# "data": {

# "total\_data\_value" =&gt; "10"

# }

# }

# \`\`\`

# \* 返回说明：

# 参数名称\|类型\|注释

# :------------\|:------------\|:------------

# total\_data\_value\|string\|当月流量总量

# 

# 

# 

# ---

# 

# \#\#三、错误编码

# 

# 错误编码\|信息

# :------------\|:------------

# 0   \| 正常

# 50000   \|未知异常



