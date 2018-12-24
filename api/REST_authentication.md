# Signature Verification

## Valid request structure

For security reasons, all API requests, except for the API, must run signature computation. A valid request consists of the following elements:  

- Method requests address, that is the access server address: api.newdex.io followed by the method name, such as api.newdex.io/v1/order/orders.

- API access key (secret_key), the SECRET_KEY of API_KEY that you apply for. 

- Signature method, a hash-based protocol for the user to compute the signature. We use HmacSHA256.

- Timestamp, the time when you make the request (UTC time zone). Including this value in a query request helps to prevent third parties from intercepting your request. The timestamp is made up of 10 digits. 

- Required parameter and optional parameter. Each method has a set of required and optional parameters to define API calling. You can view these parameters and their meanings in the description of each method. Be sure to note: For a GET request, each method has its own parameters that need signature computation. For the POST request, each method has parameters that do not need the signature verification, that is, only api_key and timestamp two parameters are needed to perform the signature computation in the POST request, and the other parameters are put in the body.
y.

- Signature, the value come out with signature computation, to ensure that the signature is valid and not tampered with.

Example：
```
https://api.newdex.io/v1/order/orders?
api_key=abcdefghijk12345
&symbol=eosblackteam-black-eos
&timestamp=1544121678
&sign=calculated_value
```

## Signature Computation

An API request is most likely to be tampered with while it is being sent over the Internet. To ensure that the request has not been changed, we require the user to contain a signature in each request to verify that if the parameter or parameter value has been changed during the transmission.

### Steps for signature computation:

Specify the signature computation request. When running signature computation using HMAC, with different content the result of computing will be completely different. Therefore before running the signature computation, please standardize the request first. Let’s explain based on the request above  
https://api.huobi.pro/v1/order/orders

-  Sort the request parameters in the order of the ASCII codes and remove the sing field to get the following results

```
api_key: abcdefghijk12345
symbol: eosblackteam-black-eos
timestamp: 1544121678
```

- Use the character' &' to connect the parameters in above order

```
api_key=abcdefghijk12345&symbol=eosblackteam-black-eos&timestamp=1544121678
```

- λ	Use secret_key to get through HmacSHA256 signature, return

```
sign = SHA256('api_key=abcdefghijk12345&symbol=eosblackteam-black-eos&timestamp=1544121678', secret_key);
```

- Finally, reassemble sign, then the API request sent to the server should be

```
https://api.newdex.io/v1/order/orders?api_key=abcdefghijk12345&symbol=eosblackteam-black-eos&timestamp=1544121678&sign=${hash}
```
