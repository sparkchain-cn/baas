## <a name="6. 文本上链接口">6. 文本上链接口</a>   

文本上链接口可以实现各种类型的业务系统中的文本信息上传到区块链中，文本上链可以使得相关的信息永久保留在公链上。  

### <a name="6.1. 文本上链">6.1. 文本上链</a> 
把指定的文本上链  
- 接口地址：/v1/text/record  

- 请求方式：POST  

- 接口参数：  


| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|accessToken|String|访问凭证|
|srcWalletAddr|String|【三选一】支付方的钱包地址（srcWalletAddr、srcUserId 、srcAccount)|
|srcUserId|String|【三选一】支付方的钱包地址（srcWalletAddr、srcUserId 、srcAccount）|
|srcAccount|String|【三选一】支付方的用户Id（srcWalletAddr、srcUserId 、srcAccount）|
|payPassword|String|支付密码|
|chainCode|String|区块链编码|
|tokenCode|String|通证编码|
|destWalletAddr|String|【三选一】接受方的钱包地址（destWalletAddr、destUserId、destAccount）|
|destUserId|String|【三选一】接受方的用户Id（destWalletAddr、destUserId、destAccount|
|destAccount|String|【三选一】接受方的账户（destWalletAddr、destUserId、destAccount）|
|memo|String|记录内容|
|bizId|String|业务Id（每次操作都不能重复，保证事务）|
|amount|String|【可选】金额，执行该接口时，花费的金额，比如：jingtum在文本添加时，不填写该值，会花费1SWT|
|gasLimit|Long|【可选】Gas的上限倍数,该gas设置对jingtum公链不起效|
|gasPrice|Long|【可选】Gas计费单位,该gas设置对jingtum公链不起效|
  
- 请求示例图： 
---
![image](./pics/text_record.jpg?raw=true)

- 请求示例代码：
---    
```
/v1/text/record/accessToken=a7aff191-427a-4275-bf0a-f6f150b486a1&srcWalletAddr=4ed93afd-47bf-43cb-8fd9-ed8ed3c7affe&payPassword=654321&chainCode=moac&tokenCode=MOAC&destWalletAddr=4402fa2f-0f42-4fde-a736-5727d618b4c9&memo=moac_text_record&bizId=f313919a-56e8-49fc-b05b-865bc69056e0&amount=0&gasLimit=40000&gasPrice=20000000000
```
- 结果返回参数：

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功）---链返回正确的结果，但是交易有可能还在运行中|
|data|Object|返回数据|
|data.hash|String|交易返回的hash值|

- 返回示例图：
---
![image](./pics/text_record_result.jpg?raw=true)

- 返回示例代码： 
---
```  
{
    "code": "200",
    "data": {
        "hash": "0x740eb84c76ae1fec215917fda8431765ed5c7fafdf6a1653e7e544959dddaaff"
    },
    "message": "",
    "success": true
}
```  

### <a name="6.2. 查询文本内容">6.2. 查询文本内容</a>  
该接口用于查询上链的文本信息。
- 接口地址：/v1/text/recordInfo   

- 请求方式：GET/POST  

- 接口参数： 
 
| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|accessToken|String|访问凭证|
|tranHash|String|交易的hash|
|forceRefresh|boolean|【可选】强制刷新（默认为false，当为true时，会获取链上数据|  
- 请求示例图： 
 ---
![image](./pics/text_recordInfo.jpg?raw=true)

- 请求示例代码：
---
```
/v1/text/recordInfo/accessToken=a7aff191-427a-4275-bf0a-f6f150b486a1&tranHash=0x740eb84c76ae1fec215917fda8431765ed5c7fafdf6a1653e7e544959dddaaff
```

- 结果返回参数：  
  
| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功）|
|data|Object|返回数据|
|data.tokenCode|String|通证编码|
|data.tradeTime|Date|交易时间|
|data.amount|String|支付金额|
|data.gasFee|String|交易费用|
|data.chainCode|String|区块链编码|
|data.memos|String|记录内容|
|data.destAccount|String|接受方的账户|
|data.srcAccount|String|发起方的账户|
|data.tranHash|String|交易的hash|

- 返回示例图：
 ---
![image](./pics/text_recordInfo_result.jpg?raw=true)

- 返回示例代码：  
---
```
{
    "code": "200",
    "data": {
        "tokenCode": "MOAC",
        "tradeTime": 1529490361000,
        "amount": "0",
        "gasFee": 0.0000522,
        "chainCode": "moac",
        "memos": "moac_text_record",
        "destAccount": "0x9430e338712f4c1026ab181ef01409a06ab73eb7",
        "state": 9,
        "tranHash": "0x740eb84c76ae1fec215917fda8431765ed5c7fafdf6a1653e7e544959dddaaff",
        "srcAccount": "0x08bad40508a3169a3a2e9caa36fa20ef7bd98535"
    },
    "message": "",
    "success": true
}
```  

### <a name="6.3. 查询文本列表">6.3. 查询文本列表</a>  
获取该钱包下文本记录列表。
- 接口地址：/v1/text/recordInfoList

- 请求方式：GET/POST  

- 接口参数：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|accessToken|String|访问凭证|
|walletAddr|String|【三选一】钱包地址（walletAddr、userId、accounts）|
|userId|String|【三选一】用户Id（walletAddr、userId、accounts）|
|accounts|String|【三选一】账户（walletAddr、userId、accounts）|
|pagesize|Integer|【可选】返回的每页数据量，默认每页10项|
|pagenum|Integer|【可选】返回第几页的数据，从第1页开始，默认为1|
|starttime|String|【可选】开始时间，比如：2018-01-01 00:00:00|
|endtime|String|【可选】结束时间，比如： 2018-06-01 23:59:59|  

- 请求示例图：  
---
![image](./pics/text_recordInfoList.jpg?raw=true)

- 请求示例代码：
---  
```
/v1/text/recordInfoList/accessToken=a7aff191-427a-4275-bf0a-f6f150b486a1&walletAddr=4ed93afd-47bf-43cb-8fd9-ed8ed3c7affe&pagesize=1
```

- 结果返回参数： 

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功|
|data|Object|返回数据|
|data.total|Integer|总记录数|
|data.pageSize|Integer|每页数据量|
|data.pageNum|Integer|第几页|
|data.results|String|结果数据|
|data.results.tokenCode|String|通证编码|
|data.results.tradeTime|String|交易时间|
|data.results.amount|String|记录金额|
|data.results.gasFee|String|交易费用|
|data.results.chainCode|String|区块链编码|
|data.results.memos|String|记录内容|
|data.results.destAccount|String|接受方的账户|
|data.results.state|Integer|状态（-1：失败；0：初始；1：等待；8：同步成功；9：成功|
|data.results.srcAccount|String|发起方的账户|
|data.results.tranHash|String|交易的hash|

- 返回示例图：
---
![image](./pics/text_recordInfoList_result.jpg?raw=true)

- 返回示例代码：  
---
```
{
    "code": "200",
    "data": {
        "total": 4,
        "pageSize": 1,
        "pageNum": 1,
        "results": [
            {
                "tokenCode": "MOAC",
                "tradeTime": 1529490361000,
                "amount": "0",
                "gasFee": 0.0000522,
                "chainCode": "moac",
                "memos": "moac_text_record",
                "destAccount": "0x9430e338712f4c1026ab181ef01409a06ab73eb7",
                "state": 9,
                "tranHash": "0x740eb84c76ae1fec215917fda8431765ed5c7fafdf6a1653e7e544959dddaaff",
                "srcAccount": "0x08bad40508a3169a3a2e9caa36fa20ef7bd98535"
            }
        ]
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


