#### <a href="./index.md#top">返回上一级目录</a>      

## 目录
===========================  

<a href="./chapter04.md#4. 用户账户接口">4. 用户账户接口</a>  <br> 
* <a href="./chapter04.md#4.1. 创建账户">4.1. 创建账户</a>  <br>
* <a href="./chapter04.md#4.2. 账户充值">4.2. 账户充值</a>  <br>
* <a href="./chapter04.md#4.3. 账户的支付请求">4.3. 账户的支付请求</a>  <br>
* <a href="./chapter04.md#4.4. 获取账户余额">4.4. 获取账户余额</a>  <br>
* <a href="./chapter04.md#4.5. 获取账户支付信息">4.5. 获取账户支付信息</a>  <br>
* <a href="./chapter04.md#4.6. 获取账户支付历史">4.6. 获取账户支付历史</a>  <br>
* <a href="./chapter04.md#4.7. 账户的文本上链">4.7. 账户的文本上链</a>  <br>

## <a name="4. 用户账户接口">4. 用户账户接口</a>  
用户账户与用户钱包对应，一个用户钱包包括多个用户账户，在一个公链上针对同一个用户，在火花接入平台创建一个账户，用来管理其在公链上的操作。这里提供了更底层的操作，接入应用可以直接使用这些账户接口对公链进行直接操作。

### <a name="4.1. 创建账户">4.1. 创建账户</a>  
[回到顶部](#目录)

在指定的公链上创建账户，返回其公钥和私钥。  
- 接口地址：/v1/account/createAccount

- 请求方式：GET/POST  

- 接口参数：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|accessToken|String|访问凭证|
|chainCode|String|区块链编码| 
- 请求示例图：
--- 
![image](./pics/account_createAccount.jpg?raw=true)
- 请求示例代码：
--- 
```
/v1/account/createAccount?accessToken=99810a20-aed7-47c8-8d00-454ae812518a&chainCode=jingtum
```

- 结果返回参数：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功）|
|data|Object|返回数据|
|data.privateKey|String|账户的私钥|
|data.addr|String|账户地址|

- 返回示例图：
--- 
![image](./pics/account_createAccount_result.jpg?raw=true)

- 返回示例代码：
--- 
```json
{
    "code": "200",
    "data": {
        "privateKey": "san2hPb8JpzGGKeMMWkgdzerNcRG9",
        "publicKey": "jLud3QQdheDSP9f4VnHEinXeEmg9LnLNWJ",
        "addr": "jLud3QQdheDSP9f4VnHEinXeEmg9LnLNWJ"
    },
    "message": "",
    "success": true
}
```


### <a name="4.2. 账户充值">4.2. 账户充值</a>   
[回到顶部](#目录)

外部账户向本平台的账户或平台的钱包进行充值，比如创建app钱包之后，就需要外部账户向其app钱包中充值，然后app钱包向用户钱包转账。  
- 接口地址：/v1/account/charge 

- 请求方式：GET/POST  

- 接口参数:  
 
| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|accessToken|String|访问凭证|
|chainCode|String|区块链编码|
|tokenCode|String|通证编码|
|srcAccount|String|充值方的账户|
|srcPrivateKey|String|充值方的账户私钥|
|destAccount|String|【三选一】接受方的账户 --- 当为空时，（1）可传入destWalletAddr（2）可传入appid,destUserId|
|destWalletAddr|String|【三选一】接收方的钱包地址|
|appid|Long|应用Id，和destUserId结合在一起使用|
|destUserId|String|【三选一】接受方的用户Id|
|bizId|String|业务ID（每次操作都不能重复，保证事务）|
|amount|String|充值金额|  
|gasLimit|Long|【可选】Gas数的上限值,该gas设置对jingtum公链不起效|
|gasPrice|Long|【可选】Gas单位价格,该gas设置对jingtum公链不起效|  

- 请求示例图：
---
![image](./pics/account_charge.jpg?raw=true)

- 请求示例代码：
---
```
/v1/account/charge?accessToken=99810a20-aed7-47c8-8d00-454ae812518a&chainCode=jingtum&tokenCode=SWT&srcAccount=jLud3QQdheDSP9f4VnHEinXeEmg9LnLNWJ&srcPrivateKey=san2hPb8JpzGGKeMMWkgdzerNcRG9&destWalletAddr=25616a76-f89c-4b04-b73e-72fc452a6f24&bizId=ac546908-6510-441d-91a5-b869ffa44a3f&amount=0.000001
```
- 结果返回参数：  
  
| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功）---链返回正确的结果，但交易可能还未写入区块，所以仍在执行中|
|data|Object|返回数据|
|data.hash|String|交易返回的hash值|  
- 返回示例图：
---
![image](./pics/account_charge_result.jpg?raw=true)

- 返回示例代码：
---
```json
{
    "code": "200",
    "data": {
        "hash": "9126DDC9DE6ABB0D6A4C13AD31555BB0D3B781850C1FB80F3A60126E9C6F442D"
    },
    "message": "",
    "success": true
}
```



### <a name="4.3. 账户的支付请求">4.3. 账户的支付请求</a>  
[回到顶部](#目录)

不同账户间充值。两个外部账户可以通过该接口进行转账，本平台中会保存它们转账的流水记录。  
- 接口地址：/v1/account/transfer  

- 请求方式：GET/POST  

- 接口参数：  
  
| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|accessToken|String|访问凭证|
|srcAccount|String|支付方的账户|
|privateKey|String|支付方的账户私钥|
|destAccount|String|接受方的账户|
|amount|String|支付金额|
|chainCode|String|区块链编码|
|tokenCode|String|通证编码|
|memo|String|【可选】记录内容（提供了敏感词过滤功能，上链时敏感词会转换为*）|
|bizId|String|业务Id（每次操作都不能重复，保证事务）|
|gasLimit|Long|【可选】Gas数的上限值,该gas设置对jingtum公链不起效|
|gasPrice|Long|【可选】Gas单位价格,该gas设置对jingtum公链不起效|  
- 请求示例图：
---
![image](./pics/account_transfer.jpg?raw=true)

- 请求示例代码：
---
```
/v1/account/transfer?accessToken=99810a20-aed7-47c8-8d00-454ae812518a&chainCode=jingtum&tokenCode=SWT&srcAccount=jLud3QQdheDSP9f4VnHEinXeEmg9LnLNWJ&srcPrivateKey=san2hPb8JpzGGKeMMWkgdzerNcRG9&destAccount=ja2pno5dP4B98aphgGNrKSAipDPV7sWFSf&bizId=1f39d266-d05a-49e8-a667-a98bb389428f&amount=0.000001
```

- 结果返回参数： 
  
| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功）---链返回正确的结果，但交易可能还未写入区块，所以仍在执行中|
|data|Object|数据|
|data.hash|String|交易返回的hash值|  
- 返回示例图：
---
![image](./pics/account_transfer_result.jpg?raw=true)

- 返回示例代码：
---
```json
{
    "code": "200",
    "data": {
        "hash": "52E7C1653C5ABD375D297C12E468AEEDCF210112BAA6896A81995B3C4C8CC721"
    },
    "message": "",
    "success": true
}
```



### <a name="4.4. 获取账户余额">4.4. 获取账户余额</a>  
[回到顶部](#目录)

获取账户的余额。  
- 接口地址：/v1/account/balance  

- 请求方式：GET/POST  

- 接口参数： 
 
| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|accessToken|String|访问凭证|
|account|String|账户|
|chainCode|String|区块链编码（比如：jingtum）|
|tokenCode|String|通证编码（比如：jingtum的通证是SWT）|
- 请求示例图：
--- 
![image](./pics/account_balance.jpg?raw=true) 
- 请求示例代码：
--- 
```
/v1/account/balance?accessToken=99810a20-aed7-47c8-8d00-454ae812518a&account=jLud3QQdheDSP9f4VnHEinXeEmg9LnLNWJ&chainCode=jingtum&tokenCode=SWT
```

- 结果返回参数：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功）|
|data|Object|返回数据|
|data.address|String|账户地址|
|data.balance|String|余额|
|data.tokenCode|String|通证编码|
|data.freezed|String|冻结金额|

- 返回示例图：
--- 
![image](./pics/account_balance_result.jpg?raw=true)

- 返回示例代码：
--- 
```json
{
    "code": "200",
    "data": {
        "tokenCode": "SWT",
        "address": "jLud3QQdheDSP9f4VnHEinXeEmg9LnLNWJ",
        "balance": "34.999978",
        "freezed": "20"
    },
    "message": "",
    "success": true
}

```

### <a name="4.5. 获取账户支付信息">4.5. 获取账户支付信息</a>  
[回到顶部](#目录)

直接从链上获取账户支付交易的详细信息。
- 接口地址：/v1/account/transInfo  

- 请求方式：GET/POST  

- 接口参数：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|accessToken|String|访问凭证|
|account|String|账户|
|chainCode|String|【可选】区块链编码（比如：jingtum）|
|tranHash|String|支付交易的hash|
- 请求示例图：
---
![image](./pics/account_transInfo.jpg?raw=true)

- 请求示例代码：
---
```
/v1/account/transInfo?accessToken=99810a20-aed7-47c8-8d00-454ae812518a&account=jLud3QQdheDSP9f4VnHEinXeEmg9LnLNWJ&chainCode=jingtum&tranHash=52E7C1653C5ABD375D297C12E468AEEDCF210112BAA6896A81995B3C4C8CC721
```

- 结果返回参数：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功）|
|data|Object|返回数据|
|data.tradeTime|Date|交易时间|
|data.tokenCode|String|通证编码|
|data.gasFee|String|交易费用|
|data.amount|String|支付金额|
|data.memos|String|记录内容|
|data.blockNumber|String|区块编号（交易记录一旦写入区块后才返回该字段）|
|data.state|String|状态（-1：失败；0：初始；1：等待；8：同步成功；9：成功）||
|data.tranHash|String|交易的hash|
|data.destAccount|String|接受方的账户|
|data.srcAccount|String|支付方的账户|
- 返回示例图：
---
![image](./pics/account_transInfo_result.jpg?raw=true)

- 返回示例代码：
---
``` json
{
    "code": "200",
    "data": {
        "tradeTime": 594459990000,
        "tokenCode": "SWT",
        "gasFee": "0.01",
        "amount": "0.000001",
        "memos": "",
        "blockNumber": "11130223",
        "destAccount": "ja2pno5dP4B98aphgGNrKSAipDPV7sWFSf",
        "state": "9",
        "tranHash": "52E7C1653C5ABD375D297C12E468AEEDCF210112BAA6896A81995B3C4C8CC721",
        "srcAccount": "jLud3QQdheDSP9f4VnHEinXeEmg9LnLNWJ"
    },
    "message": "",
    "success": true
}
```


### <a name="4.6. 获取账户支付历史">4.6. 获取账户支付历史</a>  
[回到顶部](#目录)

获取指定账户在链上的支付历史。  
- 接口地址：/v1/account/transInfoList  

- 请求方式：GET/POST  

- 接口参数：  
  
| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|accessToken|String|访问凭证|
|account|String|账户|
|pagesize|Integer|【可选】返回的每页数据量，默认每页10项|
|pagenum|Integer|【可选】返回第几页的数据，默认从1开始|
|starttime|String|【可选】开始时间，比如：2018-01-01 00:00:00|
|endtime|String|【可选】结束时间，比如： 2018-06-01 23:59:59|  
 
- 请求示例图：
---
![image](./pics/account_transInfoList.jpg?raw=true) 

- 请求示例代码：
---
```
/v1/account/transInfoList?accessToken=99810a20-aed7-47c8-8d00-454ae812518a&account=jLud3QQdheDSP9f4VnHEinXeEmg9LnLNWJ
```

- 结果返回参数： 

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功）|
|data|Object|返回数据|
|data.total|Integer|总记录数|
|data.pageSize|Integer|每页数据量|
|data.pageNum|Integer|第几页|
|data.results|list|结果数据|
|data.results.tokenCode|String|通证编码|
|data.results.tradeTime|Date|交易时间|
|data.results.amount|String|支付金额|
|data.results.gasFee|String|交易费用|
|data.results.chainCode|String|区块链编码|
|data.results.memos|String|记录内容|
|data.results.bizId|String|业务Id|
|data.results.destAccount|String|接受方的账户|
|data.results.state|String|状态（-1：失败；0：初始；1：等待；8：同步成功；9：成功）|
|data.results.srcAccount|String|支付方的账户|
|data.results.tranHash|String|交易的hash|
- 返回示例图： 
---
![image](./pics/account_transInfoList_result.jpg?raw=true) 

- 返回示例代码： 
---

```  json
{
    "code": "200",
    "data": {
        "total": 3,
        "pageSize": 10,
        "pageNum": 1,
        "results": [
            {
                "tokenCode": "SWT",
                "tradeTime": 1541144777000,
                "amount": "0.000001",
                "gasFee": "0.01",
                "chainCode": "jingtum",
                "memos": "",
                "bizId": "2346b665-bd1a-4b3a-a814-610c212a0bf8",
                "destAccount": "ja2pno5dP4B98aphgGNrKSAipDPV7sWFSf",
                "state": 9,
                "tranHash": "52E7C1653C5ABD375D297C12E468AEEDCF210112BAA6896A81995B3C4C8CC721",
                "srcAccount": "jLud3QQdheDSP9f4VnHEinXeEmg9LnLNWJ"
            },
            {
                "tokenCode": "SWT",
                "tradeTime": 1541144471000,
                "amount": "0.000001",
                "gasFee": "0.01",
                "chainCode": "jingtum",
                "memos": "",
                "bizId": "9f1ca3ca-8edb-48fa-8862-822ee1127697",
                "destAccount": "ja2pno5dP4B98aphgGNrKSAipDPV7sWFSf",
                "state": 9,
                "tranHash": "9126DDC9DE6ABB0D6A4C13AD31555BB0D3B781850C1FB80F3A60126E9C6F442D",
                "srcAccount": "jLud3QQdheDSP9f4VnHEinXeEmg9LnLNWJ"
            },
            {
                "tokenCode": "SWT",
                "tradeTime": 1541143825000,
                "amount": "35",
                "gasFee": "0.01",
                "chainCode": "jingtum",
                "memos": "SWT INIT",
                "bizId": "1541143824269",
                "destAccount": "jLud3QQdheDSP9f4VnHEinXeEmg9LnLNWJ",
                "state": 9,
                "tranHash": "2B345D6A245AC3131862AD3BEB5CD005B151672C71F2B20B431BC6A563DC7BAA",
                "srcAccount": "jhWyqDeKqjaNSrRgvKiU8pZrnavq2bPPqQ"
            }
        ]
    },
    "message": "",
    "success": true
}
```

### <a name="4.7. 账户的文本上链">4.7. 账户的文本上链</a>  
[回到顶部](#目录)

该接口提供账户的文本上链。
  

- 接口地址：/v1/account/record  

- 请求方式：POST  

- 接口参数：  
  
| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|accessToken|String|访问凭证|
|srcAccount|String|支付方的账户|
|srcPrivateKey|String|支付方的账户私钥|
|destAccount|String|接受方的账户|
|amount|String|支付金额|
|chainCode|String|区块链编码|
|tokenCode|String|通证编码|
|memo|String|记录内容（提供了敏感词过滤功能，上链时敏感词会转换为*）|
|bizId|String|业务Id（每次操作都不能重复，保证事务）|
|gasLimit|Long|【可选】Gas数的上限值,该gas设置对jingtum公链不起效|
|gasPrice|Long|【可选】Gas单位价格,该gas设置对jingtum公链不起效|  
- 请求示例图：
---
![image](./pics/account_record.jpg?raw=true)

- 请求示例代码：
---
```
accessToken:99810a20-aed7-47c8-8d00-454ae812518a
srcAccount:jLud3QQdheDSP9f4VnHEinXeEmg9LnLNWJ
srcPrivateKey:san2hPb8JpzGGKeMMWkgdzerNcRG9
destAccount:ja2pno5dP4B98aphgGNrKSAipDPV7sWFSf
amount:0.000001
chainCode:jingtum
tokenCode:SWT
memo:jingtum 文本上链
bizId:{{$guid}}
```

- 结果返回参数： 
  
| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功）---链返回正确的结果，但是交易有可能还在运行中|
|data|Object|数据|
|data.hash|String|交易返回的hash值|  
- 返回示例图：
---
![image](./pics/account_record_result.jpg?raw=true)

- 返回示例代码：
---
```json
{
    "code": "200",
    "data": {
        "hash": "BC88691A3AFB1C393C5CAD387589BFFAA5D84EDDB684080B8A0B68CEDB37CFB6"
    },
    "message": "",
    "success": true
}
```




## 官方联系方式

### 官方QQ群

![QQ群：594629943](../sp.png)

### 官方技术交流论坛
  欢迎大家到<a href="http://sparkda.com/">斯巴达论坛</a>进行提问及交流 

### 官方技术BAAS平台
  欢迎大家到<a href="http://baas.sparkchain.cn/">火花链BaaS平台</a>发现更多好玩的Dapp（目前正开发中）


## 第三方合作伙伴

 - <a href="https://www.jingtum.com/">井通科技</a>,github地址为：https://github.com/swtcpro ，开发者文档地址：http://developer.jingtum.com/  浏览器地址：http://state.jingtum.com

 - <a href="http://www.moac.io/">MOAC</a>,github地址为：ttps://github.com/MOACChain/,开发者文档地址：https://github.com/MOACChain/moac-core/wiki/Commands ,https://github.com/MOACChain/moac-core/wiki/Chain3 ,浏览器地址：http://explorer.moac.io/home

 - 南昌技术开发团队,github地址为:https://github.com/moacDapp/ ,QQ群：

 ![QQ群：805362142](../nc.png)

<a href="./index.md#top">返回主目录</a>  <br>
