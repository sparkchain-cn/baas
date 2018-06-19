
### <a name="7. 用户钱包密码接口">7. 用户钱包密码接口</a>  
### <a name="7.1 修改查询密码">7.1 修改查询密码</a>   
- 通过该接口，可以修改钱包的查询密码。  
- 接口地址：/v1/wallet/modifyPassword  
- 请求方式：GET/POST  
- 接口参数：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|accessToken|String|访问凭证|
|walletAddr|String|【二选一】钱包地址walletAddr和userId二选一|
|userId|String|【二选一】用户IdwalletAddr和userId二选一|
|oldPassword|String|旧的查询密码|
|newPassword|String|新的查询密码|  
 
- 提交示例：
---  
![image](./pics/7.1.jpg?raw=true)
---  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功）|
|data|Object|返回数据|
|walletAddr|String|钱包地址|
|userId|String|用户Id|  

- 返回示例：  

```
{
    "code": "200",
    "data": {
        "success": true,
        "walletAddr": "3226d31d-5d3f-4c1c-802f-909b60772c05",
        "userId": "999540864483065856"
    },
    "message": "",
    "success": true
}
```  



### <a name="7.2. 重置查询密码">7.2. 重置查询密码</a>  


- 通过该接口，可以重置钱包的查询密码，返回新的查询密码，然后调用“修改查询密码”接口，对查询密码进行修改。  

- 接口地址：/v1/wallet/resetPassword  

- 请求方式：GET/POST  

- 接口参数：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|accessToken|String|访问凭证|
|walletAddr|String|【二选一】钱包地址walletAddr和userId二选一|
|userId|String|【二选一】用户IdwalletAddr和userId二选一|  
- 提交示例： 
 
---
![image](./pics/7.2.jpg?raw=true)
---  

- 返回的结果信息：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功)|
|data|Object|返回数据|
|walletAddr|String|钱包地址|
|newPwd|String|新的查询密码|
|userId|String|用户Id|  

- 返回示例：  
  
```
{
    "code": "200",
    "data": {
        "walletAddr": "3226d31d-5d3f-4c1c-802f-909b60772c05",
        "newPwd": "1000206015276253184",
        "userId": "999540864483065856"
    },
    "message": "",
    "success": true
}
```  


### <a name="7.3. 验证查询密码">7.3. 验证查询密码</a>  
- 通过该接口，校验查询密码的正确性。  

- 接口地址：/v1/wallet/validPassword  

- 请求方式：GET/POST  

- 接口参数：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|accessToken|String|访问凭证|
|walletAddr|String|【二选一】钱包地址walletAddr和userId二选一|
|userId|String|【二选一】用户Id walletAddr和userId二选一|
|password|String|查询密码|  

- 提交示例：  

---
![image](./pics/7.3.jpg?raw=true)
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

```
{
    "code": "200",
    "data": {
        "walletAddr": "3226d31d-5d3f-4c1c-802f-909b60772c05",
        "userId": "999540864483065856"
    },
    "message": "",
    "success": true
}
```

### <a name="7.4. 修改支付密码">7.4. 修改支付密码</a>  

- 通过该接口，设置钱包的支付密码。 
 
- 接口地址：/v1/wallet/updatePayPassword  

- 请求方式：GET/POST  

- 接口参数：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|accessToken|String|访问凭证|
|walletAddr|String|【二选一】钱包地址walletAddr和userId二选一|
|userId|String|【二选一】用户IdwalletAddr和userId二选一|
|oldPayPassword|String|旧的支付密码|
|newPayPassword|String|新的支付密码|  

- 请求示例：  
---
![image](./pics/7.4.jpg?raw=true)
---  
- 返回的结果信息：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功）|
|data|Object|返回数据|
|walletAddr|String|钱包地址|
|userId|String|用户ID|  
- 返回示例:  

```
{
    "code": "200",
    "data": {
        "walletAddr": "3226d31d-5d3f-4c1c-802f-909b60772c05",
        "userId": "999540864483065856"
    },
    "message": "",
    "success": true
} 
```  

### <a name="7.5. 重置支付密码">7.5. 重置支付密码</a>   

- 通过该接口，重置钱包的支付密码。  

- 接口地址：/v1/wallet/resetPayPassword  

- 请求方式：GET/POST  

- 接口参数：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|accessToken|String|访问凭证|
|walletAddr|String|【二选一】钱包地址walletAddr和userId二选一|
|userId|String|【二选一】用户Id walletAddr和userId二选一|

- 请求示例：  

---
![image](./pics/7.5.jpg?raw=true)
---

- 返回的结果信息：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功）|
|data|Object|返回数据|
|walletAddr|String|钱包地址|
|newPwd|String|新支付密码|
|userId|String|用户ID|  

- 返回示例：  

```
{
    "code": "200",
    "data": {
        "walletAddr": "3226d31d-5d3f-4c1c-802f-909b60772c05",
        "newPwd": "1000207735158996992",
        "userId": "999540864483065856"
    },
    "message": "",
    "success": true
}
```

### <a name="7.6. 验证支付密码">7.6. 验证支付密码</a>  

- 通过该接口，验证钱包支付密码的正确性。  

- 接口地址：/v1/wallet/validPayPassword  

- 请求方式：GET/POST  

- 接口参数：  
 
| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|accessToken|String|访问凭证|
|walletAddr|String|【二选一】钱包地址walletAddr和userId二选一|
|userId|String|【二选一】用户IdwalletAddr和userId二选一|
|payPassword|String|支付密码|  

- 请求示例：  


---
![image](./pics/7.6.jpg?raw=true)
---

- 返回的结果信息：  


| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功）|
|data|Object|返回数据|
|walletAddr|String|钱包地址|
|userId|String|用户ID|  

- 返回示例：  

```
{
    "code": "200",
    "data": {
        "walletAddr": "3226d31d-5d3f-4c1c-802f-909b60772c05",
        "userId": "999540864483065856"
    },
    "message": "",
    "success": true
}
```
