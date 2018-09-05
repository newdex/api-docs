# Public REST API for Newdex

# General API Information

* The base endpoint is: **https://api.newdex.io**
* All endpoints return either a JSON object or array.
* Any endpoint can return an ERROR; the error payload is as follows:
```javascript
{
  "code": -1121,
  "msg": "Invalid symbol."
}
```

# Public API Endpoints

## GET /v1/common/symbols

Get all the trading assets in Newdex

Request: None

Response: Array


Name | Data type | Description 
------------ | ------------ | ------------
symbol | string | 
price_precision | int | 
currency_precision | int | 


## GET /v1/ticker

Trade summary of a trading day for a symbol

Request: 


Parameter | Data type | Description
------------ | ------------ | ------------
symbol | string | 

Response: Object


Name | Data type | Description
------------ | ------------ | ------------
symbol | string | 
last | double | latest price
change | double | the price changes from 08:00 GMT
high | double | highest price
low | double | lowest price
amount | double | amount of this currency
volume | double | volume of eos


## GET /v1/ticker/price

The price of a symbol

Request: 


Parameter | Data type | Description
------------ | ------------ | ------------
symbol | string | 

Response: Object


Name | Data type | Description
------------ | ------------ | ------------
symbol | string | 
price | double | latest price
