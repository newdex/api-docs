## 申请API_KEY说明

Newdex是去中心化交易所，所使用的是EOS账户体系，所以您必需要有一个EOS账号才可以Newdex提供的API。

### 1、生成api_key及secret_key

提供您的账号名称及邮箱，通过接口 /api/generate 生成您的api_key及secret_key，例如：  
account: newdexiotest  
email: test@newdex.io  
使用上面信息组成链接，并请求：https://api.newdex.io/v1/api/generate?account=newdexiotest&email=test@newdex.io  
结果如果返回  {"code":200,"data":"success"}，表示您已经生成了api_key及secret_key，并发送至您的邮箱（此接口，每账号1分钟内只允许调用一次）。

### 2、验证邮箱和EOS账号
请登录您填写的邮箱，您将收到newdex给您发的邮件。邮件内容包括您的api_key及secret_key，同时还包括一个16位的code（验证码，有效期1天），接着请使用您填写的EOS账号往newdex的验证账号转任意数量的EOS（建议转账0.0001 EOS，此金额不会返还）  

> 接收账号：newdexverify  
> Memo：您的16位的code  

操作完后稍等10-20秒种，您的api_key将自动被激活。

### 3、重置api_key及secret_key
只需要重复第一和第二步骤即可
