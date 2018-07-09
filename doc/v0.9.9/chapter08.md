目录
===========================
<a href="./chapter08.md#8. 系统管理接口">8. 系统管理接口</a>  <br>
* <a href="./chapter08.md#8.1. 注册区块链[可选，待实现]">8.1. 注册区块链[可选，待实现]</a>  <br>
* <a href="./chapter08.md#8.2. 新增通证[可选]">8.2. 新增通证[可选]</a>  <br>
* <a href="./chapter08.md#8.3. 添加通证[可选，待实现]">8.3. 添加通证[可选，待实现]</a>  <br>

### <a name="8. 系统管理接口">8. 系统管理接口</a>   


该类接口让用户进行系统管理，用户可以到docker hub下载Docker镜像，本地设定。Docker地址脚本 ：  

---
docker run -d --name moac_node_java_mysql_redis -p 8545:8545 -p 3306:3306 -p 6379:6379   --env TESTNET="--testnet"  -v /root/:/root/ sparkchain/moac_node_java_mysql_redis:0.8.2  

---  
  
  
详细到[www.sparkda.com](www.sparkda.com)进行提问  


### <a name="8.1. 注册区块链[待实现]">8.1. 注册区块链[待实现]</a>  
[回到顶部](#目录)

如果下载了docker镜像，其默认初始化moac和jingtum链，可以在本地的环境中注册其它区域链，当然需要实现其相关的接口  

- 接口地址：/v1/sys/registChain  

- 请求方式：GET/POST  

- 接口参数：  


| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|chainId|String|区块链Id|
|chainName|String|区块链名称|
|chainCode|String|区块链编码|
|apis|String|调用接口|
|tokenName|String|通证名称|
|tokenCode|String|通证编码|
|currency|String|货币单位|
|precisions|Integer|通证精度|
|units|String|通证单位|  

- 请求示例：  




- 结果返回参数： 

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|请求结果|
|data|Object|返回数据|  



- 返回示例：  

### <a name="8.2. 新增通证">8.2. 新增通证</a>  
[回到顶部](#目录)

  在某区块链上，创建非原生的通证，该接口目前可支持moac的Erc20通证的新增，不支持Jingtum。  

- 接口地址：/v1/sys/createToken  

- 请求方式：GET/POST  

- 接口参数:  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|String|String|chainCode|
|name|String|通证名称|
|code|String|通证编码|
|account|String|发行方（账户地址）|
|privateKey|String|发行方的私钥|
|precisions|String|通证精度|
|currency|String|货币单位|
|amount|String|发币的总量|  

- 请求示例图：  
---
![image](./pics/sys_createToken.jpg?raw=true)

- 请求示例代码：
---
```
/v1/sys/createToken?chainCode=moac&name=TT1&code=TT1&account=XXX&precisions=18&currency=TT1&amount=10000000000000&privateKey=XXX
```

- 结果返回参数：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功）|
|data|Object|返回数据|
|data.hash|String|通证发布上链返回的hash值|  

- 返回示例图：
---
![image](./pics/sys_createToken_result.jpg?raw=true)

- 返回示例代码：  
---
```json
{
    "code": "200",
    "data": {
        "hash": "0xe3cec55bfcb8e1204b312b3693b2a8684b96109b52b15d53c724cd7fd389a6e5"
    },
    "message": "",
    "success": true
}
```

### <a name="8.3. 添加通证">8.3. 添加通证</a>  
[回到顶部](#目录)
 
添加区块链上已存在的通证到本地平台，目前只支持添加moac的Erc20通证。

- 接口地址：/v1/sys/addToken  

- 请求方式：GET/POST  

- 接口参数：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|chainCode|String|区块链编码|
|name|String|通证名称|
|code|String|通证编码|
|issuer|String|发行方（账户地址）(可选)|
|precisions|String|通证精度|
|currency|String|货币单位|
|contractAbi|String|智能合约编译后的abi代码|
|contractAddr|String|代币合约地址|  


- 请求示例图：
--- 
![image](./pics/app_addToken.jpg?raw=true)

- 请求示例代码：
---
```
/v1/sys/addToken?chainCode=moac&name=TT1&code=TT1&precisions=18&currency=TT1&contractAddr=0xfe885bf0d8c98ae57e5c5bf359f0e35e178ca85c&contractAbi=XXX
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
![image](./pics/app_addToken_result.jpg?raw=true)
  

- 返回示例代码：
--- 
```json
{
    "code": "200",
    "data": null,
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