# 行情API

## GET /v1/common/symbols  
获取所有交易对列表

请求参数： 无  

返回参数： Object，结构如下  

参数名 | 类型 | 描述 
------------ | ------------ | ------------
id | int | symbol id = pair id
symbol | string | 交易对名称，如：eosblackteam-black-eos
contract | string | 合约名称，如：eosio.token
currency | string | 币种名称，如：EOS
price_precision | int | 在Newdex的最小价格精度
currency_precision | int | 此币种的最小精度

## GET /v1/ticker  
获取单个交易对行情

请求参数:  

参数名 | 类型 | 描述 
------------ | ------------ | ------------
symbol | string | 交易对名称

返回参数: Object，结构如下  

参数名 | 类型 | 描述 
------------ | ------------ | ------------
symbol | string | 交易对名称
last | double | 最新价格
change | double | 价格变化（从 08:00 GMT 起到现在的价格变化）
high | double | 24小时最高价
low | double | 24小时最低价
amount | double | 24小时成交量
volume | double | 24小时成交额（转成计价币种，如EOS、USDT）

## GET /v1/tickers

获取所有交易对的行情

请求参数:  无  

返回参数: Object数组，结构如下 

参数名 | 类型 | 描述 
------------ | ------------ | ------------
symbol | string | 交易对名称
last | double | 最新价格
change | double | 价格变化（从 08:00 GMT 起到现在的价格变化）
high | double | 24小时最高价
low | double | 24小时最低价
amount | double | 24小时成交量
volume | double | 24小时成交额（转成计价币种，如EOS、USDT）


## GET /v1/price

获取所有交易对的价格

请求参数:  

参数名 | 类型 | 描述 
------------ | ------------ | ------------
symbol | string | 交易对名称

返回参数: Object，结构如下  


参数名 | 类型 | 描述 
------------ | ------------ | ------------
symbol | string | 交易对名称
price | double | 最新价格

## GET /v1/depth

获取交易订单簿（交易深度）

请求参数:  

参数名 | 类型 | 描述 
------------ | ------------ | ------------
symbol | string | 交易对名称

返回参数: Object，结构如下  

参数名 | 类型 | 描述 
------------ | ------------ | ------------
asks | array | 卖单深度
bids | array | 买单深度

示例数据：
```
/* GET /v1/depth?symbol=eosblackteam-black-eos */
{
  "code":200,
  "data":{
      "bids":[
       [0.035,1299.1857],
       [0.03493,11400],
       [0.0344,1612.4186],
       [0.0335,24299.6626],
       [0.0315,95103.6126],
       [0.03046,6744.3959],
       [0.03002,316.439],
       [0.03,3333.3333],
       [0.02961,31.9587],
       [0.02926,17.7101]
     ],
     "asks":[
       [0.068,549.1971],
       [0.067,18106.8275],
       [0.06666,3000],
       [0.066,15373.3999],
       [0.06539,20.6],
       [0.065,9347.6336],
       [0.064,6767.0784],
       [0.06398,676.949],
       [0.063,6265.8133],
       [0.062,92.3191]
     ]
   }
 }
```

## GET /v1/trades

获取交易对的成交记录

请求参数:  

参数名 | 类型 | 描述 
------------ | ------------ | ------------
symbol | string | 交易对名称

返回参数: Object数组，结构如下  

参数名 | 类型 | 描述 
------------ | ------------ | ------------
id | array | 交易ID
price | double | 交易价格
amount | double | 成交量
volume | double | 成交额（转成计价币种，如EOS、USDT）
time | int | 10位数字时间戳

## GET /v1/candles

获取交易对的K线数据

请求参数:  

参数名 | 类型 | 描述 
------------ | ------------ | ------------
symbol | string | 交易对名称
time_frame | string | （可选）时间间隔，默认1hour，可选值:1min,5min,15min,30min,1hour,4hour,6hour,1day,1week,1month,1year
size | int | （可选）数量，默认100，最大2000

返回参数: Object数组，结构如下  

参数名 | 类型 | 描述 
------------ | ------------ | ------------
0 | int | k线ID
1 | double | 开盘价
2 | double | 收盘价
3 | double | 24小时最高价
4 | double | 24小时最低价
5 | double | 成交量
6 | double | 成交额（转成计价币种，如EOS、USDT）

示例数据
```
/* GET /v1/candles?symbol=eosblackteam-black-eos&time_frame=1hour&size=10 */
{
  "code":200,
  "data":[
    [1544140800,0.04075,0.046,0.046,0.04075,100882.9715,4518.451],
    [1544144400,0.046,0.043,0.046,0.04271,8857.6799,381.6711],
    [1544148000,0.043,0.04441,0.046,0.043,63614.3411,2811.6175],
    [1544151600,0.04441,0.04444,0.046,0.04354,5183.5131,234.7778],
    [1544155200,0.04444,0.04257,0.04444,0.04255,12290.0635,528.4927],
    [1544158800,0.04257,0.04599,0.04599,0.04257,1160.6585,53.2085],
    [1544162400,0.04599,0.04531,0.0469,0.04416,129433.0583,5809.5475],
    [1544166000,0.04531,0.0445,0.0469,0.0445,14117.186,631.1711],
    [1544169600,0.0445,0.0456,0.04684,0.0445,469.2888,21.2106],
    [1544173200,0.0456,0.04777,0.04777,0.0456,4895.7245,231.3036]
  ]
}
```

# 交易API

## GET /v1/order/orders

获取用户的订单列表

请求参数:  

参数名 | 类型 | 描述 
------------ | ------------ | ------------
state | string | 状态，可选值:pending（挂单中,默认），filled（已成交），canceled（已撤单），history（包括filled以及canceled）
symbol | string | （可选）交易对名称
size | int | （可选）数量，默认20，最大50

返回参数: Object数组，结构如下  

参数名 | 类型 | 描述 
------------ | ------------ | ------------
id | int | 订单ID
trx_id | string | 链上的入账ID
side | string | 交易方向：sell（卖单）,buy（买单）
type | string | 交易类型：sell-limit（限价卖单）,sell-market（市价卖单）,buy-limit（限价买单）,buy-market（市价卖单）
price | double | 订单价格
amount | double | 订单数量
price | double | 订单价格
amount | double | 订单数量
deal_price | double | 成交价（均价）
deal_amount | double | 成交量
deal_volume | double | 成交额（转成计价币种，如EOS、USDT）
state | double | 状态：new（未成交），partially-filled（部分成交），filled（已成交），canceled（已撤单），partial-canceled（已撤单有部分成交）
created_at | int | 创建时间，10位数字时间戳
updated_at | int | 更新时间，10位数字时间戳

## GET /v1/order/cancel

用户撤单

请求参数:  

参数名 | 类型 | 描述 
------------ | ------------ | ------------
trx_id | string | 链上trx_id

返回参数: 字符串，如果成功，返回 "Order successfully canceled"

**注意：此接口只支持委托账号是newdexpocket的订单，委托账号是newdexpublic的订单只能通过执行合约来取消**
