## Request Explanation

-	Newdex API server address: https://api.newdex.io.
-	Content-Type:application/json must be declared in the POST request header information.
-	For all request parameters, please follow the API explanation for parameter encapsulation.
-	Submit the encapsulated API request to the server via POST or GET methods, and Newdex processes and returns the corresponding JSON format result.
-	Please use https request.
-	Account limit frequency is 50 times in 10 seconds (single APIKEY dimension limit, only allow access to the Market API if no signature contained, and the frequency will be limited to 10 times in 10 seconds).


## Return Format Explanation

- Newdex return all in JSON format, and will contain code fields.
- If request error raise, it will return code and msg fields, as follows:
```json
{
  "code": 1003,
  "msg": "Invalid signature"
}
```
- If request succeeded, it will return code and data fields, as follows:
```json
{
  "code": 200,
  "data": "response data..."
}
```
- Error code please see [Error Code](/api-for-cn/REST_error_code.md)
