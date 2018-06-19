## <a name="4. 用户账户接口">4. 用户账户接口</a>  
用户账户与用户钱包对应，一个用户钱包包括多个用户账户，在一个公链上针对同一个用户，在火花接入平台创建一个账户，用来管理其公链的处理。这里提供了更底层的操作，接入应用可以直接使用这些账户接口对公链进行直接操作。

### <a name="4.1. 创建账户">4.1. 创建账户</a>  
根据指定的公链，在其公链上创建账户，返回其公钥和私钥。  
- 接口地址：/v1/account/creatAccount  
- 请求方式：GET/POST  
- 接口参数：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|chainCode|String|区块链编码（目前支持jingtum和moac，可选择其中一种）| 
- 提交示例： 
--- 
![image](./pics/4.1%E9%92%B1%E5%8C%85.jpg?raw=true)
---
- 返回的结果信息：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功）|
|data|Object|返回数据|
|privateKey|String|账户的私钥|
|publicKey|String|账户的公钥|
|addr|String|账户地址|

- 返回示例：  
![image](./pics/4.2%E9%92%B1%E5%8C%85.jpg?raw=true)

### <a name="4.2. 账户充值">4.2. 账户充值</a>   
外部账户向本平台的账户或平台的钱包进行充值，比如创建app钱包之后，就需要外部账户向其app钱包中充值，然后app钱包向用户钱包转账。  
- 接口地址：/v1/account/charge  
- 请求方式：GET/POST  
- 接口参数:  
 
| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|chainCode|String|区块链编码|
|tokenCode|String|通证编码|
|srcAccount|String|充值方的账户|
|srcPrivateKey|String|充值方的账户私钥|
|destAccount|String|【三选一】接受方的账户当为空时，（1）可传入destWalletAddr（2）可传入appid,destUserId|
|destWalletAddr|String|【三选一】接收方的钱包地址|
|appid|Long|应用Id，和destUserId结合在一起使用|
|destUserId|String|【三选一】接受方的用户Id|
|bizId|String|业务ID（每次操作都不能重复，保证事务）|
|amount|String|充值金额|  
- 提交示例：
![image](./pics/4.2%E9%92%B1%E5%8C%85.jpg?raw=true)

### <a name="4.3. 账户的支付请求">4.3. 账户的支付请求</a>  
不同其账户充值。两个外部账户可以通过该接口进行转账，本平台中会保存它们转账的流水记录。  
- 接口地址：/v1/account/transfer  
- 请求方式：GET/POST  
- 接口参数：  
  
| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|srcAccount|String|支付方的账户|
|privateKey|String|支付方的账户私钥|
|destAccount|String|接受方的账户|
|amount|String|支付金额|
|chainCode|String|区块链编码|
|tokenCode|String|通证编码|
|memo|String|【可选】记录内容|
|bizId|String|业务Id（每次操作都不能重复，保证事务）|
|gasLimit|Long|【可选】Gas的上限倍数jingtum公链对gas的设置不起效，默认是0.01SWT|
|gasPrice|Long|【可选】Gas计费单位jingtum公链对gas的设置不起效，默认是0.01SWT|  
- 提交示例：
---
![image](./pics/4.3%E6%94%AF%E4%BB%98%E8%AF%B7%E6%B1%82.jpg?raw=true)
---  
- 返回的结果信息：  
  
| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功）---链返回正确的结果，但是交易有可能还在运行中|
|data|Object|数据|
|gasFee|String|Gas费用|
|hash|String|交易返回的hash值|  
- 返回示例：
![image](./pics/4.3.3%E6%94%AF%E4%BB%98%E8%AF%B7%E6%B1%82.jpg?raw=true)


### <a name="4.4. 获取账户余额">4.4. 获取账户余额</a>  
- 根据账户的地址获取账户的余额。  
- 接口地址：/v1/account/balance  
- 请求方式：GET/POST  
- 接口参数： 
 
| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|account|String|账户|
|chainCode|String|区块链编码（目前支持jingtum和moac，选其一填写）|
|tokenCode|String|通证编码（比如：jingtum的通证是SWT）|
- 请求示例： 
--- 
![image](./pics/4.4%E8%8E%B7%E5%8F%96%E8%B4%A6%E6%88%B7%E4%BD%99%E9%A2%9D.jpg?raw=true) 
---
- 返回的结果信息：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功）|
|data|Object|返回数据|
|address|String|账户地址|
|balance|String|余额|
|tokenCode|String|通证编码|
|freezed|String|冻结金额|

- 返回示例：
![image](./pics/4.4.1获取账户余额.jpg?raw=true)


### <a name="4.5. 获取账户支付信息">4.5. 获取账户支付信息</a>   
获取账户支付的流水详细信息。
- 接口地址：/v1/account/transInfo  
- 请求方式：GET/POST  
- 接口参数：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|account|String|账户|
|chainCode|String|【可选】区块链编码（比如：jingtum）|
|tranHash|String|支付交易的hash|
- 提交示例：
---
![image](./pics/4.5获取账户支付信息.jpg?raw=true)
---
- 返回的结果信息：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功）|
|data|Object|返回数据|
|tradeTime|Date|交易时间|
|tokenCode|String|通证编码|
|gasFee|String|交易费用|
|amount|String|支付金额|
|memos|String|记录内容|
|tranHash|String|交易的hash|
|destAccount|String|接受方的账户|
|srcAccount|String|支付方的账户|
|issuer|String|发行方|
- 返回示例：  

```  
{
"code": "200",
"data": {
    "tradeTime": "1527306620",
    "tokenCode": "SWT",
    "gasFee": "0.01",
    "amount": "0.001",
    "memos": "[\"accout transfer 0.001swt\"]",
    "tranHash": "820ABB9C3CFAB6CF260FB277D2B1FE563FCF1B3B67A944E7B4826C1DA9C40BDF",
    "destAccount": "jJYv8v11eMSFHALHJgjLXwZwhMnzAK4kcZ",
    "srcAccount": "jhrSnysLGBz1xXgvSKf3evAc8yt4G4UPgR",
    "issuer": ""
    },
"message": "",
"success": true
}
```

### <a name="4.6. 同步流水">4.6. 同步流水</a>   
当链上的流水和接入平台的流水不同步时，主要发现在其账户在外部进行转入或转出的交易，这时需要调用同步流水，把链上的流水同步到火花接入平台中，然后就可以根据各种不同的条件来进行查询。
- 接口地址：/v1/account/syncWaterflow  
- 请求方式：GET/POST  
- 接口参数：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|account|String|账户|
|chainCode|String|区块链编码|
|tokenCode|String|通证编码|
|syncSize|Integer|【可选】同步大小 （默认为10）|  
- 提交示例：
---
![image](./pics/同步流水.jpg?raw=true)
---  
| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功）|
|data|list|返回数据|
|destinyPublicKey|String|目标方的公钥|
|tokenCode|String|通证编码|
|tradeTime|String|交易时间|
|createtime|String|创建时间|
|payTime|String|支付时间|
|chainCode|String|区块链编码|
|memos|Date|记录内容|
|dispAmount|Date|显示的转账金额|
|tradeHash|Date|交易的hash|
|srcPublicKey|String|发起方的公钥|

- 返回示例：  

```  
{
    "code": "200",
    "data": [
        {
            "destinyPublicKey": "jLoMncrtJzsi5FihFUrX2KgWRdPs8vpejT",
            "tokenCode": "SWT",
            "tradeTime": 1527322870000,
            "createtime": 1527322870000,
            "payTime": 1527322870000,
            "chainCode": "jingtum",
            "memos": "[]",
            "dispAmount": "9",
            "tradeHash": "11491457EC19A30EF40EC4BF0DA78B2819B3B91253BDFF921DDD3CE932B24F7D",
            "srcPublicKey": "jaXL8B92w3aGq1XDt2e5bRW7P3nkdtTViT"
        }
    ],
    "message": "",
    "success": true
}
```
### <a name="4.7. 获取账户支付历史">4.7. 获取账户支付历史</a>  
获取指定账户在链上的支付历史，获取之前需要调用同步流水操作，然后再调用该接口。  
- 接口地址：/v1/account/transInfoList  
- 请求方式：GET/POST  
- 接口参数：  
  
| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|account|String|账户|
|pagesize|Integer|【可选】返回的每页数据量，默认每页10项|
|pagenum|Integer|【可选】返回第几页的数据，默认从1开始|
|starttime|String|【可选】开始时间，比如：2018-01-01 00:00:00|
|endtime|String|【可选】结束时间，比如： 2018-06-01 23:59:59|  
 
- 提交示例：  
---
![image](./pics/4.7获取账户支付历史.jpg?raw=true) 
---

- 返回的结果信息： 

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功）|
|data|Object|返回数据|
|total|Integer|总记录数|
|pageSize|Integer|每页数据量|
|pageNum|Integer|第几页|
|results|list|结果数据|
|tokenCode|String|通证编码|
|tradeTime|Date|交易时间|
|amount|String|支付金额|
|gasFee|String|交易费用|
|chainCode|String|区块链编码|
|memos|String|记录内容|
|destAccount|String|接受方的账户|
|state|String|状态（-1：失败；0：初始；1：等待；8：同步成功；9：成功）|
|srcAccount|String|支付方的账户|
|hash|String|交易的hash|
- 返回示例：  

```  
{
    "code": "200",
    "data": {
        "total": 1,
        "pageSize": 10,
        "pageNum": 1,
        "results": [
            {
                "tokenCode": "SWT",
                "tradeTime": 1527298540000,
                "amount": "1",
                "gasFee": 0.01,
                "chainCode": "jingtum",
                "memos": null,
                "destAccount": "jhrSnysLGBz1xXgvSKf3evAc8yt4G4UPgR",
                "state": 9,
                "srcAccount": "j3pnSUaSbgJZ5UeqSwWjTAQWbbsjjY5GJ6",
                "hash": "F97B14CA578DC91DBDFEFDED159E4FA3CA380187BE9BE489069CB1CDA1BC3BA4"
            }
        ]
    },
    "message": "",
    "success": true
}
```
