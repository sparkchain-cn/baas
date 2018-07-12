#### <a href="./index.md#top">返回上一级目录</a>      

目录
===========================  
<a href="./chapter05.md#5. 用户钱包账户关联接口">5. 获取账户支付历史</a>  <br>
* <a href="./chapter05.md#5.1. 绑定单个账户">5.1. 绑定单个账户</a>  <br> 
* <a href="./chapter05.md#5.2. 绑定多个账户">5.2. 绑定多个账户</a>  <br> 

### <a name="5. 用户钱包账户关联接口">5. 获取账户支付历史</a>  
对于已经有的用户钱包，如果需要和账户的进行关联，或者把账户绑定到指定钱包中，可以调用这些接口进行处理


### <a name="5.1. 绑定单个账户">5.1. 绑定单个账户</a> 
[回到顶部](#目录)

钱包绑定一个当前系统不存在的账户，如果存在的账户会自动进行关联处理。

<font color=red>
注意：jingtum公链的账户在绑定到钱包之前，需要先对账户充值激活。 至于具体需要充值的金额，请联系管理员。</font>

- 接口地址：/v1/wallet/bindAccount  

- 请求方式：GET/POST  

- 接口参数： 
 
| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|accessToken|String|访问凭证|
|walletAddr|String|钱包地址|
|chainCode|String|区块链编码|
|account|String|账户|
|accountPrivatekey|String|账户的私钥（可选）当账户不属于当前平台，需要有私钥|
- 请求示例图（先创建一个空钱包）：  使用2.3和2.4中的接口新建空钱包(onlyWallet设置为true)
---
![image](./pics/app_emptyWallet.jpg?raw=true)

- 请求示例图（绑定一个moac公链账户）：  
---
![image](./pics/wallet_bindAccount.jpg?raw=true)

- 请求示例代码：
---
```
/v1/wallet/bindAccount?accessToken=256e10be-8172-4cfc-ae78-c543d8c38706&walletAddr=074ea814-b202-4469-a6c7-7efe10aa3e9d&chainCode=moac&account=0x11631df10e22410e1ac0d44ebc2aa21811ed645a&accountPrivatekey=a1da976cf6106c52365d463096d144a8ac8567323719e4a512143751579756a1
```

- 结果返回参数：

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功）|
|data|Object|返回数据|  
- 返回示例图：
---
![image](./pics/wallet_bindAccount_result.jpg?raw=true)

- 返回示例代码： 
---
``` json
{
    "code": "200",
    "data": null,
    "message": "",
    "success": true
}
```
### <a name="5.2. 绑定多个账户">5.2. 绑定多个账户</a>  
[回到顶部](#目录)

钱包绑定多个当前系统不存在的账户，如果存在的账户会自动进行关联处理。  

<font color=red>
注意：jingtum公链的账户在绑定到钱包之前，需要先对账户充值激活。 至于具体需要充值的金额，请联系管理员。</font>

- 接口地址：/v1/wallet/bindAccounts  

- 请求方式：GET/POST  

- 接口参数：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|accessToken|String|访问凭证|
|walletAddr|String|钱包地址|
|accounts|Array|多账户|
|chainCode|String|区块链编码|
|account|String|账户|
|accountPrivatekey|String|账户的秘钥（可选）|
- 请求示例图：
---
![image](./pics/wallet_bindAccounts.jpg?raw=true)

- 请求示例代码(入参值)：
---
```
accessToken:a7aff191-427a-4275-bf0a-f6f150b486a1
walletAddr:66f1326a-1c22-4ce3-903b-e8b7636017a1
accounts:[{chainCode:"moac",account:"0x194a45117c23bb2adca4ee51b7df3c12a2804c47",accountPrivatekey:"97dadf6c897cf042d7e2f279fac87635ef3e0c378b4f1bbf48acb23cd00c7e5b"},{chainCode:"jingtum",account:"jsG1CeTng2HJamTTjQiUsk1Jak9pn228Ey",accountPrivatekey:""}]
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
![image](./pics/wallet_bindAccounts_result.jpg?raw=true)


- 返回示例代码：
---
```json
{
    "code": "200",
    "data": {
        "accounts": [
            {
                "accountId": 1009366431797608448,
                "chainCode": "moac",
                "accountAddr": "0x194a45117c23bb2adca4ee51b7df3c12a2804c47"
            },
            {
                "accountId": 1009303128685674496,
                "chainCode": "jingtum",
                "accountAddr": "jsG1CeTng2HJamTTjQiUsk1Jak9pn228Ey"
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

<a href="./index.md#top">返回主目录</a>  <br>

