# 如何通过编程在Newdex下单

## 下单说明

Newdex的API不包括下单的API，Newdex订单是直接从链上读取的，本质上是用户下单是通过向Newdex转账来生成的。下单信息则是通过这笔转账memo中读取。

## memo字段说明

memo必须是标准的JSON字符串，否则不会生成订单。下面演示一个正确的memo格式（为了阅读方便，JSON做了换行及加空格处理，真实交易不建议换行及加多余空格）

```json
{
  "type": "buy-limit",
  "symbol": "eosblackteam-black-eos",
  "price": "0.03456",
  "channel": "API"
}
```
下面分别介绍各个字段的含意及内容：  
type：下单类型，有四种，分别是 buy-limit（限价买入），buy-market（市价买入），sell-limit（限价卖出），sell-market（市价卖出）  
symbol：交易对名称，是由“合约名+币种名+交易区名”组合而成  
price：交易价格，如果是市价单，此字段可以不填  
channel：渠道名，此字段值固定为“API”  
特别说明：对于买单，您必须使用交易区的计价货币转账，比如symbol为eosblackteam-black-eos，则您必须转账EOS。您的转账金额除以价格即为购买数量。对于卖单，直接转您要卖的token即可。

## 如何发起转账

因为需要转账，所以就必须要与节点通讯，用户将组装好的转账信息通过私钥签名发送给节点广播出去便完成了一笔转账过程。下面介绍两种方式可以实现与节点的通讯和转账。

### 1、使用cleos发起转账

cleos是EOS官方发布的命令行工具，建议使用包管理安装eos工具（目前只支持MacOS和Linux主流发行版本）,详细请参考：https://github.com/EOSIO/eos  
通过命令行方式调用cleos，常用命令如下：  
#### 创建钱包  
```
cleos wallet create
```
创建后会在屏幕上显示您的钱包密码，请务必保管好。

#### 解锁钱包  
```
cleos wallet unlock
```
通过密码解锁钱包，只有解锁后才能执行转账等操作

#### 导入私钥
```
cleos wallet import ${private_key}
```
private_key是您的eos账号私钥。

#### 发起转账
发起一转转账命令如下：
```
cleos push action ${contract} transfer '{"from":"${account}","to":"newdexpublic","quantity":"${quantity}","memo":"${memo}"}' -p ${account}
```
注意：我们的委托账号慢慢在切换成newdexpublic
account: 您的EOS账号名  
contract: 币种的合约名，eos的合约名是：eosio.token  
quantity: 转账数量，必须包括币种符号，且小数位数必须和此token的发行精度一致，如eos是4位，格式是：1.1000 EOS  
memo: memo必须按照上面介绍的写法填写  

#### 其它说明
如果您没有在本地搭建EOS节点，节点需要单独指定，如下：
```
cleos -u https://eos.newdex.one get info
cleos -u https://eos.newdex.one -p eosaccount push action eosio.token transfer ...
```
这边列一些常用节点，大家可以根据延迟自行选择：  
https://eos.newdex.one  
https://openapi.eos.ren  
https://api.eosbeijing.one  
https://mainnet.meet.one  
https://nodes.eos42.io  


更多的cleos命令，请参考：https://developers.eos.io/eosio-cleos/reference

### 2、通过nodejs发起转账

如果您的开发环境是Windows，建议您使用eos官方提供的eosjs(https://github.com/EOSIO/eosjs)。
如果您不是使用js做开发语言，您可以使用eosjs搭建一个简易的本地http服务器提供交易的中转。
  
  
最后，有更多问题，请联系 tech@newdex.io
