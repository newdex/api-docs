## API Explanation

### Exchange

https://newdex.io

### API Request Path

https://api.newdex.io

### Apply for APP_KEY

Newdex api_key needs to be binded with EOS account. [Apply for Newdex Market API_KEY](https://api.newdex.io/signup)  

### How to Place Order

Since Newdex is a decentralized exchange and place order needs signature using user’s private key, while Newdex keeps clear of user’s private key, the Trade API does not include API of placing order. Users need to implement the order logic by their own. For more details please refer to [How to Place Order on Newdex through Coding](/api/how_to_make_order.md)  

### How to Cancel Order

Execute contract: cleos push action newdexpublic cancelorder '{"order_id": $order_id,"owner": $your_account,"pair_id": "$pair_id","auth_type": 1}' -p $your_account

## REST Market and Trade API

* [Signature Verification](/api/REST_authentication.md)
* [Request and Response Format Explanation](/api/REST_request_response.md)
* [API Reference](/api/REST_api_reference.md)
* [Error Code](/api/REST_error_code.md)


## WebSocket Market and Trade API

Please stay tuned 
  
   
[中文文档点击这里查看](/README_zh.md)
