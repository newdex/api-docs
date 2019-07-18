## API说明

### 交易所

https://newdex.io

### API请求路径

https://api.newdex.io

### 申请APP_KEY

Newdex的api_key需要和EOS账号绑定，[申请Newdex交易行情API_KEY](https://api.newdex.io/signup)  

### 如何下单

因为Newdex是去中心化交易所，下单需要使用用户私钥签名，Newdex不会触碰用户的私钥，所以交易API中并不包括下单的API，用户需要自己去实现下单逻辑。具体如何下单请可以参考[如何通过编程在Newdex下单](/api-for-cn/how_to_make_order.md)  

### 如何取消订单

取消订单需要通过执行合约来完成
cleos push action newdexpublic cancelorder '{"pair_id": "$pair_id","order_id": $order_id}' -p $your_account


## REST行情、交易API

* [签名认证](/api-for-cn/REST_authentication.md)
* [请求及返回格式说明](/api-for-cn/REST_request_response.md)
* [API Reference](/api-for-cn/REST_api_reference.md)
* [错误代码](/api-for-cn/REST_error_code.md)


## WebSocket行情、交易API

敬请期待
