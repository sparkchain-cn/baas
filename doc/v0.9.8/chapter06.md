### <a name="6. 文本上链接口">6. 文本上链接口</a>   

文本上链接口可以实现各种类型的业务系统中的文本信息上传到区块链中，文本上链可以使得相关的信息永久保留在公链上。  

### <a name="6.1. 文本上链">6.1. 文本上链</a> 
- 把指定的文本上链  
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
|gasLimit|Long|【可选】Gas的上限倍数jingtum公链对gas的设置不起效，默认是0.01SWT|
|gasPrice|Long|【可选】Gas计费单位jingtum公链对gas的设置不起效，默认是0.01SWT|
  
- 请求示例：  

---
![image](./pics/6.1.jpg?raw=true)
---    


| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功）---链返回正确的结果，但是交易有可能还在运行中|
|data|Object|返回数据|
|gasFee|String|交易费用|
|hash|String|交易返回的hash值|



- 结果示例：  

```  
{
    "code": "200",
    "data": {
        "gasFee": "0.01",
        "hash": "0C38FC15B01E39837AF42508D6DDF6D85861E051326605390A43D2C032CD049B"
    },
    "message": "",
    "success": true
}
```  

### <a name="6.2. 查询文本内容">6.2. 查询文本内容</a>  
- 接口地址：/v1/text/recordInfo   
- 请求方式：GET/POST  
- 接口参数： 
 
| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|accessToken|String|访问凭证|
|tranHash|String|交易的hash|
|forceRefresh|boolean|【可选】强制刷新（默认为false，当为true时，会获取链上数据|  
- 请求示例： 
 
---
![image](./pics/6.2.jpg?raw=true)
---

- 返回的结果信息：  
  
| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功）|
|data|Object|返回数据|
|tokenCode|String|通证编码|
|tradeTime|Date|交易时间|
|amount|String|支付金额|
|gasFee|String|交易费用|
|chainCode|String|区块链编码|
|memos|String|记录内容|
|destAccount|String|接受方的账户|
|srcAccount|String|发起方的账户|
|hash|String|交易的hash|

- 结果示例：  

```
{
    "code": "200",
    "data": {
        "tokenCode": "SWT",
        "tradeTime": 1527322680000,
        "amount": "1",
        "gasFee": 0.01,
        "chainCode": "jingtum",
        "memos": "测试文本2",
        "destAccount": "jJYv8v11eMSFHALHJgjLXwZwhMnzAK4kcZ",
        "srcAccount": "jhrSnysLGBz1xXgvSKf3evAc8yt4G4UPgR",
        "hash": "32188ACB11D5B8E67E170A27105C916DD8975CB06C5202B2FF596EA44F06F6AE"
    },
    "message": "",
    "success": true
}
```  

### <a name="6.3. 查询文本列表">6.3. 查询文本列表</a>  
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

- 请求示例：  
---
![image](./pics/6.3.jpg?raw=true)
---  
- 返回的结果信息：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功|
|data|Object|返回数据|
|total|Integer|总记录数|
|pageSize|Integer|每页数据量|
|pageNum|Integer|第几页|
|results|String|结果数据|
|tokenCode|String|通证编码|
|tradeTime|String|交易时间|
|amount|String|记录金额|
|gasFee|String|交易费用|
|chainCode|String|区块链编码|
|memos|String|记录内容|
|destAccount|String|接受方的账户|
|state|Integer|状态（-1：失败；0：初始；1：等待；8：同步成功；9：成功|
|srcAccount|String|发起方的账户|
|hash|String|交易的hash|

- 结果示例：  

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
                "tradeTime": 1527298539000,
                "amount": "1",
                "gasFee": 0.01,
                "chainCode": "jingtum",
                "memos": "account transfer 1swt",
                "destAccount": "jJYv8v11eMSFHALHJgjLXwZwhMnzAK4kcZ",
                "state": 9,
                "srcAccount": "jhrSnysLGBz1xXgvSKf3evAc8yt4G4UPgR",
                "hash": "844AAAC62446CBC66EF2C96286FDE40BACE20F38ABBBE53021D0F78ECA207044"
            }
        ]
    },
    "message": "",
    "success": true
}
```
