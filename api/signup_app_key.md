## Explanation on Applying for API_KEY

Newdex is a decentralized exchange, it applies EOS account system, therefor you need to have an EOS account to use the API that provided by Newdex.

### 1.Generate api_key and secret_key

Use your account name and email address to generate your api_key and secret_key through the port /api/generate. For example:  
account: newdexiotest  
email: test@newdex.io  
Use the information above to form a link, and request: https://api.newdex.io/v1/api/generate?account=newdexiotest&email=test@newdex.io, if it returns {"code":200,"data":"success"} it means that you have generated api_key and secret_key and had them sent to your email (at the port, each account could only be used once per minute).

### 2.Verify email address and EOS account

Please log in the email address that you use in the last step, you should receive an email sent by Newdex. The email concludes your api_key and secret_key, meanwhile there would be a 16-digit code (verification code, expired in 1 day). Then please use the EOS account that you provided in last step to transfer EOS in any amount to Newdex verifying account (it is recommended to transfer 0.0001 EOS since it won’t be returned).  
Receive Account: newdexverify  
Memo: [Your 16-digit code]  
Wait for 10-20s after transfer your api_key will be activated.

### 3.Reset api_key and secret_key

Repeat Step 1 and Step 2. 
