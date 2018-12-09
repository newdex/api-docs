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
特别说明：对于买单，您必须使用交易区的计价货币转账，比如symbol为eosblackteam-black-eos，则您必须转账EOS。您的转账金额除去价格即为购买数量。对于卖单，直接转您要卖的token即可。

## 如何发起转账

因为需要转账，所以就必须要与节点通讯，用户将组装好的转账信息通过私钥签名发送给节点广播出去便完成了一笔转账过程。下面介绍两种方式可以实现与节点的通讯和转账。

### 使用cleos发起转账

cleos是EOS官方发布的命令行工具，适合在Mac OS及Linux系统中使用。文档待完成...

### 通过nodejs发起转账

文档待完成...
