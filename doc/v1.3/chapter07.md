#### <a href="./index.md#top">返回上一级目录</a>      

## 目录
===========================  

<a href="./chapter07.md#7. 用户钱包密码接口">7. 用户钱包密码接口</a>  <br>
* <a href="./chapter07.md#7.1 修改查询密码">7.1 修改查询密码</a>  <br>
* <a href="./chapter07.md#7.2. 重置查询密码">7.2. 重置查询密码</a>  <br>
* <a href="./chapter07.md#7.3. 验证查询密码">7.3. 验证查询密码</a>  <br>
* <a href="./chapter07.md#7.4. 修改支付密码">7.4. 修改支付密码</a>  <br>
* <a href="./chapter07.md#7.5. 重置支付密码">7.5. 重置支付密码</a>  <br>
* <a href="./chapter07.md#7.6. 验证支付密码">7.6. 验证支付密码</a>  <br>

## <a name="7. 用户钱包密码接口">7. 用户钱包密码接口</a>  
### <a name="7.1 修改查询密码">7.1 修改查询密码</a> 
[回到顶部](#目录)

通过钱包的“旧查询密码”设置钱包的“新查询密码”。

- 接口地址：/v1/wallet/modifyPassword

- 请求方式：GET/POST  

- 接口参数：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|accessToken|String|访问凭证|
|walletAddr|String|【二选一】钱包地址，walletAddr和userId二选一|
|userId|String|【二选一】用户Id，walletAddr和userId二选一|
|oldPassword|String|旧的查询密码|
|newPassword|String|新的查询密码|  
 
- 请求示例图：
---  
![image](./pics/wallet_modifyPassword.jpg?raw=true)

- 请求示例代码：
---  
```
/v1/wallet/modifyPassword?accessToken=1e43fe43-bf65-4180-8242-fbf4a30dd29b&walletAddr=4ed93afd-47bf-43cb-8fd9-ed8ed3c7affe&oldPassword=1009273874782617600&newPassword=123456
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
![image](./pics/wallet_modifyPassword_result.jpg?raw=true)

- 返回示例代码：
--- 
```json
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


### <a name="7.2. 重置查询密码">7.2. 重置查询密码</a>  
[回到顶部](#目录)

重置钱包的查询密码，会返回一个随机的查询密码，然后可以调用“修改查询密码”接口，对查询密码进行修改。

- 接口地址：/v1/wallet/resetPassword  

- 请求方式：GET/POST  

- 接口参数：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|accessToken|String|访问凭证|
|walletAddr|String|【二选一】钱包地址，walletAddr和userId二选一|
|userId|String|【二选一】用户Id，walletAddr和userId二选一|  
- 请求示例图： 
 
---
![image](./pics/wallet_resetPassword.jpg?raw=true)

- 请求示例代码：
---
```
/v1/wallet/resetPassword?accessToken=1e43fe43-bf65-4180-8242-fbf4a30dd29b&walletAddr=4ed93afd-47bf-43cb-8fd9-ed8ed3c7affe
```

- 结果返回参数：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功)|
|data|Object|返回数据|
|data.walletAddr|String|钱包地址|
|data.newPwd|String|新的查询密码|
|data.userId|String|用户Id|  

- 返回示例图：
---
![image](./pics/wallet_resetPassword_result.jpg?raw=true)

- 返回示例代码：
```json
{
    "code": "200",
    "data": {
        "walletAddr": "4ed93afd-47bf-43cb-8fd9-ed8ed3c7affe",
        "newPwd": "1009318545693081600",
        "userId": "1009273874782617600"
    },
    "message": "",
    "success": true
}
```  


### <a name="7.3. 验证查询密码">7.3. 验证查询密码</a>  
[回到顶部](#目录)

通过该接口，校验查询密码的正确性。  

- 接口地址：/v1/wallet/validPassword  

- 请求方式：GET/POST  

- 接口参数：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|accessToken|String|访问凭证|
|walletAddr|String|【二选一】钱包地址，walletAddr和userId二选一|
|userId|String|【二选一】用户Id，walletAddr和userId二选一|
|password|String|查询密码|  

- 请求示例图：  

---
![image](./pics/wallet_validPassword.jpg?raw=true)

- 请求示例代码：
---  
```
/v1/wallet/validPassword?accessToken=1e43fe43-bf65-4180-8242-fbf4a30dd29b&walletAddr=4ed93afd-47bf-43cb-8fd9-ed8ed3c7affe&password=123456
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
![image](./pics/wallet_validPassword_result.jpg?raw=true)


- 返回示例代码：  
---
```json
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

### <a name="7.4. 修改支付密码">7.4. 修改支付密码</a>  
[回到顶部](#目录)

通过钱包的“旧支付密码”设置钱包的“新支付密码”。 
 
- 接口地址：/v1/wallet/updatePayPassword  

- 请求方式：GET/POST  

- 接口参数：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|accessToken|String|访问凭证|
|walletAddr|String|【二选一】钱包地址，walletAddr和userId二选一|
|userId|String|【二选一】用户Id，walletAddr和userId二选一|
|oldPayPassword|String|旧的支付密码|
|newPayPassword|String|新的支付密码|  

- 请求示例图：
---
![image](./pics/wallet_updatePayPassword.jpg?raw=true)

- 请求示例代码：
---  
```
/v1/wallet/updatePayPassword?accessToken=1e43fe43-bf65-4180-8242-fbf4a30dd29b&walletAddr=4ed93afd-47bf-43cb-8fd9-ed8ed3c7affe&oldPayPassword=1009321244299886592&newPayPassword=654321
```

- 结果返回参数：

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功）|
|data|Object|返回数据|
|data.walletAddr|String|钱包地址|
|data.userId|String|用户ID|  

- 返回示例图：
---  
![image](./pics/wallet_updatePayPassword_result.jpg?raw=true)

- 返回示例代码：
---  
```json
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

### <a name="7.5. 重置支付密码">7.5. 重置支付密码</a>   
[回到顶部](#目录)

重置钱包的支付密码，会返回一个随机的支付密码，然后可以调用“修改支付密码”接口，对支付密码进行修改。

- 接口地址：/v1/wallet/resetPayPassword  

- 请求方式：GET/POST  

- 接口参数：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|accessToken|String|访问凭证|
|walletAddr|String|【二选一】钱包地址，walletAddr和userId二选一|
|userId|String|【二选一】用户Id，walletAddr和userId二选一|

- 请求示例图：

---
![image](./pics/wallet_resetPayPassword.jpg?raw=true)

- 请求示例代码：
---
```
/v1/wallet/resetPayPassword?accessToken=1e43fe43-bf65-4180-8242-fbf4a30dd29b&walletAddr=4ed93afd-47bf-43cb-8fd9-ed8ed3c7affe
```

- 结果返回参数：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功）|
|data|Object|返回数据|
|data.walletAddr|String|钱包地址|
|data.newPwd|String|新支付密码|
|data.userId|String|用户ID|  

- 返回示例图：
---
![image](./pics/wallet_resetPayPassword_result.jpg?raw=true)

- 返回示例代码：
---
```json
{
    "code": "200",
    "data": {
        "walletAddr": "4ed93afd-47bf-43cb-8fd9-ed8ed3c7affe",
        "newPwd": "1009321244299886592",
        "userId": "1009273874782617600"
    },
    "message": "",
    "success": true
}
```

### <a name="7.6. 验证支付密码">7.6. 验证支付密码</a>  
[回到顶部](#目录)

通过该接口，验证钱包支付密码的正确性。  

- 接口地址：/v1/wallet/validPayPassword  

- 请求方式：GET/POST  

- 接口参数：  
 
| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|accessToken|String|访问凭证|
|walletAddr|String|【二选一】钱包地址，walletAddr和userId二选一|
|userId|String|【二选一】用户Id，walletAddr和userId二选一|
|payPassword|String|支付密码|  

- 请求示例图：
---
![image](./pics/wallet_validPayPassword.jpg?raw=true)

- 请求示例代码：
---
```
/v1/wallet/validPayPassword?accessToken=1e43fe43-bf65-4180-8242-fbf4a30dd29b&walletAddr=4ed93afd-47bf-43cb-8fd9-ed8ed3c7affe&payPassword=654321
```

- 结果返回参数： 


| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功）|
|data|Object|返回数据|
|data.walletAddr|String|钱包地址|
|data.userId|String|用户ID|  

- 返回示例图：
---
![image](./pics/wallet_validPayPassword_result.jpg?raw=true)

- 返回示例代码：
---
```json
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