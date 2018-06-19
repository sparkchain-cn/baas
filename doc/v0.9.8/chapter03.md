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
- 请求示例：
---
![image](./pics/%E8%AF%B7%E6%B1%82%E7%A4%BA%E4%BE%8B3.1.jpg?raw=true)
---

- 返回的结果信息：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功）|
|data|Object|返回数据|
|walletAddr|String|钱包地址|
|userId|String|用户Id|
- 返回示例：

![image](./pics/%E9%92%B1%E5%8C%853.1.2.jpg?raw=true)


### <a name="3.2. 钱包的支付请求">3.2. 钱包的支付请求</a> 
 
钱包的支付功能是业务系统上链的最基本也是核心的功能，通过该接口可以实现同链同币之间的支付转账，也可以实现不同链中不同币之间的支付转账（目前开发中）。实现同一钱包，跨越不同公链的之间的交易。屏蔽了上链的难度。  
<font color=Red>&ensp; &ensp;注意：如果使用已经创建的钱包进行支付，其支付方的钱包需要有足够的代币，默认情况下没有代币，支付方钱包需要通过外部来源充入代币，详细与管理员联系。</font>  
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
|gasLimit|Long|【可选】Gas的上限倍数|
|gasPrice|Long|【可选】Gas计费价格单位|


- 请求示例：
---  
![image](./pics/%E9%92%B1%E5%8C%853.2.jpg?raw=true)
---

- 结果返回参数：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功）---链返回正确的结果，但是交易有可能还在运行中|
|data|Object|返回数据|
|gasFee|String|交易费用|
|hash|String|交易返回的hash值|
- 结果示例：  

![image](./pics/3.2.2%E9%92%B1%E5%8C%85.jpg?raw=true)


- <a name="3.3. 获取钱包余额">3.3. 获取钱包余额</a>  
支付完成之后，通过该接口获取用户钱包中的余额  
接口地址：/v1/wallet/balances  
请求方式：GET/POST  
接口参数:  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|accessToken|String|访问凭证|
|walletAddr|String|【二选一】钱包地址walletAddr和userId二选一|
|userId|String|【二选一】用户IdwalletAddr和userId二选一|
|chainCode|String|【可选】区块链编码|
|tokenCode|String|【可选】通证编码（比如：jingtum的SWT、moac的MOAC）（为空时，可以查看该钱包下所有账户的余额）|
- 请求示例：
---  
![image](./pics/3.3%E9%92%B1%E5%8C%85.jpg?raw=true)
---
- 返回的结果信息：
  
| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功）|
|data|Object|返回数据|
|walletAddr|String|钱包地址|
|userId|String|用户Id|
|balances|list|余额数据|
|tokenCode|String|通证编码|
|balance|String|余额|
|chainCode|String|区块链编码|
|freezed|String|冻结的金额|
- 返回示例：  
![image](./pics/3.3.3.jpg?raw=true)

- <a name="3.4. 获得支付信息">3.4. 获得支付信息</a>   

&ensp; &ensp;通过该接口获取转几天交易的详细流水信息。  
- 接口地址：/v1/wallet/transInfo
- 请求方式：GET/POST  
- 接口参数：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|accessToken|String|访问凭证|
|tranHash|String|交易hash|
|forceRefresh|boolean|【可选】强制刷新（默认为false，当为true时，会获取链上数据）|
- 请求示例：
---
![image](./pics/3.4%E9%92%B1%E5%8C%85.jpg?raw=true)
---
- 返回的结果信息:  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功），但交易有可能还在运行中，获取空的data|
|data|Object|返回数据|
|tokenCode|String|通证编码|
|tradeTime|Date|交易时间|
|amount|String|交易金额|
|gasFee|String|Gas费用|
|chainCode|String|区块链编码|
|memos|String|记录内容|
|destAccount|String|接受方的账户|
|srcAccount|String|支付方的账户|
|hash|String|交易的hash值|
- 获取不到支付信息时，返回结果：
![image](./pics/3.4.3.jpg?raw=true)

- 获取到支付信息时，返回结果：
![image](./pics/3.4.4.jpg?raw=true)
  

- <a name="3.5. 获得支付历史">3.5. 获得支付历史</a>
&ensp; &ensp;通过该接口可以获取后用户通过火花链接入平台进行转账的所有流水。如果用户钱包中账户在接入平台外部进行转账，那么就需要通过账户接口中同步流水来先同步，然后可以获得钱包的所有流水（包括外部转账的流水)  
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
- 请求示例：
---
![image](./pics/3.5%E9%92%B1%E5%8C%85.jpg?raw=true)
---
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
|amount|String|记录金额|
|gasFee|Double|交易费用|
|chainCode|String|区块链编码|
|memos|String|记录内容|
|destAccount|String|接受方的账户|
|state|Integer|状态（-1：失败；0：初始；1：等待；8：同步成功；9：成功）|
|srcAccount|String|发起方的账户|
|hash|String|交易的hash|

- 返回的结果信息：
![image](./pics/3.5.1%E9%92%B1%E5%8C%85.jpg?raw=true)

- <a name="3.6. 钱包余额同步">3.6. 钱包余额同步</a>

&ensp; &ensp;当外部账户直接在外部（或在调用本平台的账户充值）向本系统用户钱包中的账户进行转账，那么其流水和余额都没有记录在火花链接入平台中，这时需要进行相同同步，本接口是对其余额进行同步，达到火花链接入平台的用户余额和公链上的余额同步。
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

- 提交示例：
---
![image](./pics/3.6%E9%92%B1%E5%8C%85.jpg?raw=true)
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
|freezed|String|冻结的金额|
- 返回示例：
![image](./pics/3.6.1%E9%92%B1%E5%8C%85.jpg?raw=true)


- <a name="3.7. 获取钱包的账户信息">3.7. 获取钱包的账户信息</a>  
- 接口地址：/v1/wallet/accounts  
- 请求方式：GET/POST  
- 接口参数：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|accessToken|String|访问凭证|
|walletAddr|String|【二选一】钱包地址:walletAddr和userId二选一|
|userId|String|【二选一】用户IdwalletAddr和userId二选一|
- 提交示例：
---
![image](./pics/3.7%E9%92%B1%E5%8C%85.jpg?raw=true)
---
- 返回的结果信息：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功）|
|data|Object|返回数据|
|accounts|list|账户信息|
|accountId|Long|账户Id|
|chainCode|String|区块链编码|
|accountAddr|String|账户地址|

<p align="left">返回示例：
![image](./pics/3.7.1.jpg?raw=true)
