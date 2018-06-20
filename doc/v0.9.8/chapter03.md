## <a name="3. 用户钱包操作接口">3. 用户钱包操作接口</a>   

接入业务系统上链的基本操作就是业务系统中用户进行转账等基本的操作，这些操作在发生在用户钱包之间。用户钱包操作接口主要对于用户之间的转账进行管理，以及对于转账之后的余额或交易流水进行查询。

 ### <a name="3.1. 设置支付密码">3.1. 设置支付密码</a>  

用户钱包在转账之前，首先需要设定支付密码，通过该接口，来设置钱包的支付密码。
- 接口地址：/v1/wallet/setPayPassword

- 请求方式：GET/POST

- 接口参数：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|accessToken|String|访问凭证|
|walletAddr|String|【二选一】钱包地址walletAddr和userId二选一|
|userId|String|【二选一】用户Id walletAddr和userId二选一|
|password|String|查询密码|
|payPassword|String|支付密码|
- 请求示例图：
---
![image](./pics/wallet_setPayPassword.jpg?raw=true)

- 请求示例代码：
---
```
/v1/wallet/setPayPassword/accessToken=1e43fe43-bf65-4180-8242-fbf4a30dd29b&walletAddr=4ed93afd-47bf-43cb-8fd9-ed8ed3c7affe&password=1009273874782617600&payPassword=654321
```

- 结果返回参数：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功）|
|data|Object|返回数据|
|data.walletAddr|String|钱包地址|
|data.userId|String|用户Id|
- 返回示例图：
---
![image](./pics/wallet_setPayPassword_result.jpg?raw=true)

- 返回示例代码：
---
```
{
    "code": "200",
    "data": {
        "walletAddr": "4ed93afd-47bf-43cb-8fd9-ed8ed3c7affe",
        "userId": "1009273874782617600"
    },
    "message": "",
    "success": true
}
```


### <a name="3.2. 钱包的支付请求">3.2. 钱包的支付请求</a> 
 
钱包的支付功能是业务系统上链的最基本也是核心的功能，通过该接口可以实现同链同币之间的支付转账，也可以实现不同链中不同币之间的支付转账（目前开发中）。实现同一钱包，跨越不同公链的之间的交易。屏蔽了上链的难度。  

<font color=Red>注意：如果使用已经创建的钱包进行支付，其支付方的钱包需要有足够的代币，默认情况下没有代币，支付方钱包需要通过外部来源充入代币，详细与管理员联系。
另外，钱包下的jingtum账户支付的成功与否，需要确保支付后，两方的余额都大于冻结的金额。
</font>  
- 接口地址：/v1/wallet/transfer  

- 请求方式：GET/POST  

- 接口参数：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|accessToken|String|访问凭证|
|srcWalletAddr|String|【三选一】支付方的钱包地址(srcWalletAddr、srcUserId 、srcAccount）|
|srcUserId|String|【三选一】支付方的用户Id（srcWalletAddr、srcUserId 、srcAccount）|
|srcAccount|String|【三选一】支付方的账户（srcWalletAddr、srcUserId和srcAccount）|
|payPassword|String|支付方的支付密码|
|chainCode|String|区块链编码|
|tokenCode|String|通证编码(比如：jingtum的SWT、moac的MOAC)|
|destWalletAddr|String|【三选一】接受方的钱包地址(destWalletAddr、destUserId和destAccount）|
|destUserId|String|【三选一】接受方的用户Id（destWalletAddr、destUserId和destAccount）|
|destAccount|String|【三选一】接受方的账户（destWalletAddr、destUserId和destAccount）|
|amount|String|支付金额|
|bizId|String|业务Id（每次操作都不能重复，保证事务）|
|memo|String|【可选】记录内容|
|gasLimit|Long|【可选】Gas的上限倍数,该gas设置对jingtum公链不起效|
|gasPrice|Long|【可选】Gas计费价格单位,该gas设置对jingtum公链不起效|


- 请求示例图：
---  
![image](./pics/wallet_transfer.jpg?raw=true)

- 请求示例代码：
---
```
/v1/wallet/transfer/accessToken=a7aff191-427a-4275-bf0a-f6f150b486a1&srcWalletAddr=4ed93afd-47bf-43cb-8fd9-ed8ed3c7affe&payPassword=654321&chainCode=moac&tokenCode=MOAC&destWalletAddr=4402fa2f-0f42-4fde-a736-5727d618b4c9&amount=0.000001&bizId=539482a2-ccff-42bb-9f4e-f212c4a89d94&memo=wallet+transfer+0.000001moac&gasLimit=40000&gasPrice=20000000000
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
![image](./pics/wallet_transfer_result.jpg?raw=true)

- 返回示例代码：
---
```
{
    "code": "200",
    "data": {
        "hash": "0x33697d81dd4b6cd3190ed9be54ecc7c2d660e4e930b3a50e9d127d3ec42d61b1"
    },
    "message": "",
    "success": true
}
```


### <a name="3.3. 获取钱包余额">3.3. 获取钱包余额</a>  
支付完成之后，通过该接口获取用户钱包中各账户的余额。

<font color=red>
注意：如果钱包中的账户，在其他平台进行了转账支付，会导致其账户余额与实际余额不一致，此时需要执行“钱包余额同步”接口使其相同。
</font>

- 接口地址：/v1/wallet/balances  

- 请求方式：GET/POST  

- 接口参数:  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|accessToken|String|访问凭证|
|walletAddr|String|【二选一】钱包地址walletAddr和userId二选一|
|userId|String|【二选一】用户IdwalletAddr和userId二选一|
|chainCode|String|【可选】区块链编码|
|tokenCode|String|【可选】通证编码（比如：jingtum的SWT、moac的MOAC）（为空时，可以查看该钱包下所有账户的余额）|
- 请求示例图：
---  
![image](./pics/wallet_balances.jpg?raw=true)

- 请求示例代码：
---
```
/v1/wallet/balances/accessToken=a7aff191-427a-4275-bf0a-f6f150b486a1&walletAddr=4ed93afd-47bf-43cb-8fd9-ed8ed3c7affe&chainCode=moac&tokenCode=MOAC
```
- 结果返回参数：
  
| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功）|
|data|Object|返回数据|
|data.walletAddr|String|钱包地址|
|data.userId|String|用户Id|
|data.balances|list|余额数据|
|data.balances.tokenCode|String|通证编码|
|data.balances.balance|String|余额|
|data.balances.chainCode|String|区块链编码|
|data.balances.freezed|String|冻结的金额|
- 返回示例图：  
--- 
![image](./pics/wallet_balances_result.jpg?raw=true)

- 返回示例代码：
--- 
```
{
    "code": "200",
    "data": {
        "balances": [
            {
                "tokenCode": "MOAC",
                "balance": "0.00095092",
                "chainCode": "moac",
                "freezed": "0"
            }
        ],
        "walletAddr": "4ed93afd-47bf-43cb-8fd9-ed8ed3c7affe",
        "userId": "1009273874782617600"
    },
    "message": "",
    "success": true
}
```


### <a name="3.4. 获得支付信息">3.4. 获得支付信息</a>   

通过该接口获取支付交易的详细信息。  
- 接口地址：/v1/wallet/transInfo

- 请求方式：GET/POST  

- 接口参数：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|accessToken|String|访问凭证|
|tranHash|String|交易hash|
|forceRefresh|boolean|【可选】强制刷新（默认为false，当为true时，会获取链上数据）|
- 请求示例图：
---
![image](./pics/wallet_transInfo.jpg?raw=true)

- 请求示例代码：
---
```
/v1/wallet/transInfo/accessToken=a7aff191-427a-4275-bf0a-f6f150b486a1&tranHash=0x33697d81dd4b6cd3190ed9be54ecc7c2d660e4e930b3a50e9d127d3ec42d61b1
```
- 结果返回参数：

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功），但交易有可能还在运行中，获取空的data|
|data|Object|返回数据|
|data.tokenCode|String|通证编码|
|data.tradeTime|Date|交易时间|
|data.amount|String|交易金额|
|data.gasFee|String|Gas费用|
|data.chainCode|String|区块链编码|
|data.memos|String|记录内容|
|data.destAccount|String|接受方的账户|
|data.srcAccount|String|支付方的账户|
|data.tranHash|String|交易的hash值|
- 返回示例图：
---
![image](./pics/wallet_transInfo_result.jpg?raw=true)
  
- 返回示例代码：
---
```
{
    "code": "200",
    "data": {
        "tokenCode": "MOAC",
        "tradeTime": 1529487709000,
        "amount": "0.000001",
        "gasFee": 0.0000726,
        "chainCode": "moac",
        "memos": "wallet transfer 0.000001moac",
        "destAccount": "0x9430e338712f4c1026ab181ef01409a06ab73eb7",
        "state": 9,
        "tranHash": "0x33697d81dd4b6cd3190ed9be54ecc7c2d660e4e930b3a50e9d127d3ec42d61b1",
        "srcAccount": "0x08bad40508a3169a3a2e9caa36fa20ef7bd98535"
    },
    "message": "",
    "success": true
}
```

### <a name="3.5. 获得支付历史">3.5. 获得支付历史</a>
通过该接口可以获取后用户通过火花链接入平台进行转账的所有流水。如果用户钱包中账户在接入平台外部进行转账，那么就需要通过账户的“同步流水”接口先做同步，然后获得钱包的所有流水（包括外部转账的流水)  
- 接口地址：/v1/wallet/transInfoList  

- 请求方式：GET/POST  

- 接口参数：

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|accessToken|String|访问凭证|
|walletAddr|String|【三选一】钱包地址 （walletAddr、userId、accounts）备注：可以看到该钱包下所有账户的支付历史|
|userId|String|【三选一】用户Id（walletAddr、userId、accounts）备注：可以看到该用户钱包下账户的支付历史|
|accounts|String|【三选一】账户（walletAddr、userId、accounts）备注：可以看到指定账户的支付历史|
|pagesize|Integer|【可选】返回的每页数据量，默认每页10项|
|pagenum|Integer|【可选】返回第几页的数据，默认从1开始|
|starttime|String|【可选】开始时间，比如:2018-01-01 00:00:00|
|endtime|String|【可选】结束时间，比如：2018-06-01 23:59:59|
- 请求示例图：
---
![image](./pics/wallet_transInfoList.jpg?raw=true)

- 请求示例代码：
---
```
/v1/wallet/transInfoList/accessToken=a7aff191-427a-4275-bf0a-f6f150b486a1&walletAddr=4402fa2f-0f42-4fde-a736-5727d618b4c9
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
|data.results.amount|String|记录金额|
|data.results.gasFee|Double|交易费用|
|data.results.chainCode|String|区块链编码|
|data.results.memos|String|记录内容|
|data.results.destAccount|String|接受方的账户|
|data.results.state|Integer|状态（-1：失败；0：初始；1：等待；8：同步成功；9：成功）|
|data.results.srcAccount|String|发起方的账户|
|data.results.tranHash|String|交易的hash|

- 返回示例图：
---
![image](./pics/wallet_transInfoList_result.jpg?raw=true)

- 返回示例代码：
---
```
{
    "code": "200",
    "data": {
        "total": 1,
        "pageSize": 10,
        "pageNum": 1,
        "results": [
            {
                "tokenCode": "MOAC",
                "tradeTime": 1529487709000,
                "amount": "0.000001",
                "gasFee": 0.0000726,
                "chainCode": "moac",
                "memos": "wallet transfer 0.000001moac",
                "destAccount": "0x9430e338712f4c1026ab181ef01409a06ab73eb7",
                "state": 9,
                "tranHash": "0x33697d81dd4b6cd3190ed9be54ecc7c2d660e4e930b3a50e9d127d3ec42d61b1",
                "srcAccount": "0x08bad40508a3169a3a2e9caa36fa20ef7bd98535"
            }
        ]
    },
    "message": "",
    "success": true
}
```
### <a name="3.6. 钱包余额同步">3.6. 钱包余额同步</a>

当外部账户直接在外部（或在调用本平台的账户充值）向本系统用户钱包中的账户进行转账，那么其流水和余额都没有记录在火花链接入平台中，这时需要进行相同同步，本接口是对其余额进行同步，促使火花链接入平台的用户余额和公链上的余额同步。

<font color=red>
注意：在支付交易未完成的情况下，执行该接口，可能会导致余额和冻结金额不正确。目前这个问题，后期会修复。请尽量在支付交易完成后，执行该接口。
</font>

- 接口地址：/v1/wallet/syncBalance  

- 请求方式：GET/POST  

- 接口参数：  
  
| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|accessToken|String|访问凭证|
|walletAddr|String|【二选一】钱包地址walletAddr和userId二选一|
|userId|String|二选一】用户IdwalletAddr和userId二选一|
|chainCode|String|区块链编码（目前支持jingtum和moac）|
|tokenCode|String|通证编码（比如：jingtum的默认通证为SWT)|

- 请求示例图：
---
![image](./pics/wallet_syncBalance.jpg?raw=true)

- 请求示例代码：
---
```
/v1/wallet/syncBalance/accessToken=a7aff191-427a-4275-bf0a-f6f150b486a1&walletAddr=4ed93afd-47bf-43cb-8fd9-ed8ed3c7affe&chainCode=moac&tokenCode=MOAC
```
- 结果返回参数：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功）|
|data|Object|返回数据|
|data.tokenCode|String|通证编码|
|data.address|String|账户地址|
|data.balance|String|余额|
|data.freezed|String|冻结的金额|

- 返回示例图：
---
![image](./pics/wallet_syncBalance_result.jpg?raw=true)

- 返回示例代码：
---
```
{
    "code": "200",
    "data": {
        "tokenCode": "MOAC",
        "address": "0x08bad40508a3169a3a2e9caa36fa20ef7bd98535",
        "balance": "0.00095092",
        "freezed": ""
    },
    "message": "",
    "success": true
}
```



###  <a name="3.7. 获取钱包的账户信息">3.7. 获取钱包的账户信息</a> 
获取钱包中各公链的账户信息 
- 接口地址：/v1/wallet/accounts  

- 请求方式：GET/POST  

- 接口参数：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|accessToken|String|访问凭证|
|walletAddr|String|【二选一】钱包地址:walletAddr和userId二选一|
|userId|String|【二选一】用户IdwalletAddr和userId二选一|
- 请求示例图：
---
![image](./pics/wallet_accounts.jpg?raw=true)
- 请求示例代码：
---
```
/v1/wallet/accounts/accessToken=a7aff191-427a-4275-bf0a-f6f150b486a1&walletAddr=4402fa2f-0f42-4fde-a736-5727d618b4c9
```

- 结果返回参数：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功）|
|data|Object|返回数据|
|data.accounts|list|账户信息|
|data.accounts.accountId|Long|账户Id|
|data.accounts.chainCode|String|区块链编码|
|data.accounts.accountAddr|String|账户地址|
- 返回示例图：
---
![image](./pics/wallet_accounts_result.jpg?raw=true)

- 返回示例代码：
---
```
{
    "code": "200",
    "data": {
        "accounts": [
            {
                "accountId": 1009300103439056896,
                "chainCode": "moac",
                "accountAddr": "0x9430e338712f4c1026ab181ef01409a06ab73eb7"
            },
            {
                "accountId": 1009303128782143488,
                "chainCode": "jingtum",
                "accountAddr": "jaCzKhPoY3diwRhEkpKsaeiUTgFfAF5EsA"
            }
        ]
    },
    "message": "",
    "success": true
}
```
