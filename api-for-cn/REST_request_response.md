## 请求说明
- Newdex API的服务地址是：https://api.newdex.io。
- POST请求头信息中必须声明 Content-Type:application/json;
- 所有请求参数请按照 API 说明进行参数封装。
- 将封装好参数的 API 请求通过 POST 或 GET 的方式提交到服务器，Newdex处理并返回相应的 JSON 格式结果。
- 请使用 https 请求。
- 账号限制频率为10秒50次（单个APIKEY维度限制，如果不加签名，只允许访问行情接口，且频率会被限制为10秒10次）。

## 返回格式说明
- Newdex返回都是 JSON 格式，且一定会包含code字段
- 如果请求错误，会返回 code 及 msg 字段，示例如下：
```json
{
  "code": 1003,
  "msg": "Invalid signature"
}
```
- 如果请求成功，会返回 code 及 data 字段，示例如下：
```json
{
  "code": 200,
  "data": "response data..."
}
```
- 错误代码请参考[错误代码](/api-for-cn/REST_error_code.md)
