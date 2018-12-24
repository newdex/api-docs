# Error Code
Code = 200, it means request succeeded, other situations mean error. See error code reference form below:

| Error Code | Explanation |
| ------ | -------- |
| -1001 | The request is beyond limit, if you don’t have API_KEY, please [apply for API_KEY](/api-for-cn/signup_app_key.md) as soon as possible. |
| -1002 | Invalid API_KEY  |
| -1003 | Invalid signature , pleas refer to [signature verification](/api-for-cn/REST_authentication.md) |
| -1004 | Request timestamp has expired |
| -1005 | No permission, request trade and order API need to verify API_KEY |
| -1101 | Invalid account |
| -1102 | Invalid email |
| -1103 | Invalid symbol |
| -1104 | Invalid trx_id |
| -1105 | Order has been canceled |
| -1106 | Order is dealt, cannot be cancel |
| -1500 | Unknown error |
