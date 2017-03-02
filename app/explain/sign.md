###签名
* 在提交订单的时候需要将提交的数据加密签名
* sign 不参与加密
* 加密/校验流程如下：

>1. 将提交的参数按照参数名进行字典序排序<font color='red'>(参数排序中需要加入app_id)</font>
>2. 将参数按 url query 方式拼接，拼接的方式样例：callback_url=xxx&app_id=xxx&serial_no=xxx&timestamp=xxxx
>3. 拼接字符串最后加上 app_secret
>4. 将最后字符串进行 sha1 加密并将字母转换成大写

* 签名 php demo

```php
/**
* 作用：格式化参数，签名过程需要使用
*/
protected function formatBizQueryParaMap($paraMap)
{
	$buff = "";
	foreach ($paraMap as $k => $v) {
		$buff .= $k . "=" . $v . "&";
	}
	$reqPar;
	if (strlen($buff) > 0) {
		$reqPar = substr($buff, 0, -1);
	}
	return $reqPar;
}

/**
* 作用：生成签名
*/
protected function getSign($data, $secret)
{
	foreach ($data as $key => $val) {
		$Parameters[$key] = $val;
	}
	//签名步骤一：按字典序排序参数并拼接
	ksort($Parameters);
	$string = formatBizQueryParaMap($Parameters, false);
	//签名步骤二：在$string后加入app_secret
	$string = $string . $secret;
	//签名步骤三：sha1加密
	$string = sha1($string);
	//签名步骤四：所有字符转为大写
	$result = strtoupper($string);
	return $result;
}

```

* 生成签名 demo

```php
$sign = getSign(
	array(
		'app_id' => $app_id,
		'serial_no' => '87000001',
		'timestamp' => 1487560009,
	),
	$secret
);

```

---