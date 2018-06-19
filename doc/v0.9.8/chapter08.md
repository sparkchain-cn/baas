
### <a name="8. 系统管理接口">8. 系统管理接口</a>   


该类接口让用户进行系统管理，用户可以到docker hub下载Docker镜像，本地设定。Docker地址脚本 ：  

---
docker run -d --name moac_node_java_mysql_redis -p 8545:8545 -p 3306:3306 -p 6379:6379   --env TESTNET="--testnet"  -v /root/:/root/ sparkchain/moac_node_java_mysql_redis:0.8.2  
---  
  
  
详细到[www.sparkda.com](www.sparkda.com)进行提问  


### <a name="8.1. 注册区块链[可选，待实现]">8.1. 注册区块链[可选，待实现]</a>  

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




- 返回的结果信息：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|请求结果|
|data|Object|返回数据|  



- 返回示例：  

### <a name="8.2. 新增通证[可选]">8.2. 新增通证[可选]</a>   
  在某区块链上，创建非原生的通证，该接口目前可支持MOAC区块链，不支持在Jingtum区块链。  

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

- 请求示例：  

---
![image](./pics/8.2.jpg?raw=true)
---

- 返回的结果信息：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功）|
|data|Object|返回数据|
|hash|String|通证发布上链返回的hash值|  

- 返回示例：  

```
{
    "code":"200",
    "data":{
        "hash":"0x4754cfba8841b5a2b4d1fc0ceb31383d8e7366240b699c603f9114e7704e2b98"
    },
    "message":"",
    "success":true
}
```

### <a name="8.3. 添加通证[可选，待实现]">8.3. 添加通证[可选，待实现]</a>  
 
添加一个区块链上已存在的通证。  

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


- 请求示例： 

--- 
![image](./pics/8.3.jpg?raw=true)
---


- 返回的结果信息：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功）|
|data|Object|返回数据|  

- 返回示例：  

```
{
    "code": "200",
    "data": null,
    "message": "",
    "success": true
}
```