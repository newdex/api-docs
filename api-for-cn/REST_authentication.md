# 签名认证

## 合法请求结构
基于安全考虑，除行情API外的 API 请求都必须进行签名运算。一个合法的请求由以下几部分组成：

- 方法请求地址 即访问服务器地址：api.newdex.io 后面跟上方法名，比如api.newdex.io/v1/order/orders。

- API 访问密钥（secret_key） 您申请的API_KEY中的SECRET_KEY。

- 签名方法  用户计算签名的基于哈希的协议，我们使用 HmacSHA256。

- 时间戳（timestamp） 您发出请求的时间 (UTC 时区) 。在查询请求中包含此值有助于防止第三方截取您的请求。时间戳是由13位数字组成的。

- 必选和可选参数 每个方法都有一组用于定义 API 调用的必需参数和可选参数。可以在每个方法的说明中查看这些参数及其含义。 请一定注意：对于GET请求，每个方法自带的参数都需要进行签名运算； 对于POST请求，每个方法自带的参数不进行签名认证，即POST请求中需要进行签名运算的只有api_key、timestamp两个参数，其它参数放在body中。

- 签名 签名计算得出的值，用于确保签名有效和未被篡改。

例：
```
https://api.newdex.io/v1/order/orders?
api_key=abcdefghijk12345
&symbol=eosblackteam-black-eos
&timestamp=1544121678233
&sign=calculated_value
```

## 签名运算

API 请求在通过 Internet 发送的过程中极有可能被篡改。为了确保请求未被更改，我们会要求用户在每个请求中带上签名，来校验参数或参数值在传输途中是否发生了更改。

### 计算签名所需的步骤：

规范要计算签名的请求 因为使用 HMAC 进行签名计算时，使用不同内容计算得到的结果会完全不同。所以在进行签名计算前，请先对请求进行规范化处理。我们以上面请求为例进行说明
https://api.huobi.pro/v1/order/orders?

-  将请求参数按照ASCII码的顺序进行排序，并去除sing字段，得到下面的结果
```
api_key: abcdefghijk12345
symbol: eosblackteam-black-eos
timestamp: 1544121678233
```
- 按照以上顺序，将各参数使用字符’&’连接。
```
api_key=abcdefghijk12345&symbol=eosblackteam-black-eos&timestamp=1544121678233
```
- 使用secret_key通过HmacSHA256签名，得到
```
sign = SHA256('api_key=abcdefghijk12345&symbol=eosblackteam-black-eos&timestamp=1544121678233', secret_key);
```

- 最后将sign拼装回去， 最终，发送到服务器的 API 请求应该为：
```
https://api.newdex.io/v1/order/orders?api_key=abcdefghijk12345&symbol=eosblackteam-black-eos&timestamp=1544121678233&sign=64位的签名hash
```
