
## <a name="2. 接入系统接口">2. 接入系统接口</a>
  
接入系统接口为业务系统上链提供了一系列的接口，首先接入系统得在火花链接入平台进行注册初始化，换取接入应用系统的accessToken。然后就可以根据初始化的相关信息来创建应用系统级别的APP钱包，创建App钱包之后，根据业务所需，为其应用系统中用户在火花链接入平台中创建用户钱包。之后的上链或交易就发生在这些钱包之间。

### <a name="2.1. 接入系统初始化">2.1. 接入系统初始化</a>
   
接入系统初始化对业务系统上链相关的信息进行初始化，主要传入业务系统编号、名称及回调地址,成功时返回appid和appsecret。  
- 接口地址：/v1/app/init
- 请求方式：GET/POST  
 提交参数：  
 
| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|appcode|String|业务系统编号,一般用业务系统的拼音缩写或英文|
|appname|String|业务系统名称，一般用中文名|
|transCallBackUrl|String|【可选】业务系统在进行交易时，不能立即返回状态，通过该地址进行回调，获取事务的返回状态|
|msgCallBackUrl|String|【可选】通过该地址进行回调，获取消息的返回值|
|userid|String|【可选】传入租户ID（针对租用平台和企业统一上链接入平台）|
- 请求示例：  
 
---
![image](./pics/请求示例.jpg?raw=true)  
---

- 返回的结果信息：  
 
| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功）|
|data|Object|返回数据|
|appid|String|业务系统ID|
|appsecret|String|业务系统的秘钥|
- 返回示例：
---
![image](./pics/返回示例.jpg?raw=true)
---
 
### <a name="2.2. 生成访问凭证">2.2. 生成访问凭证</a></p>  
 
- 调用其它接口时，一般都需要访问凭证。通过此接口就可以获取访问凭证accessToken，访问凭证有一定的时效性（目前2个小时）。  
<font color=Red >如果需要在代码中使用访问凭证，可以参考附1的简单示例（java语言）  
- <font color=#0099ff >接口地址：/v1/app/access  
请求方式：GET/POST  
接口参数：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|appid|String|业务系统的ID|
|appsecret|String|业务系统的秘钥|  
- 请求示例： 
--- 
![image](./pics/请求示例2.jpg?raw=true)
---
- 返回的结果信息： 
 
| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功）|
|data|Object|返回数据|
|accessToken|String|访问凭证|
- 返回示例：
---
![image](./pics/返回示例3.jpg?raw=true)
  
### <a name="2.3. 创建企业钱包">2.3. 创建企业钱包</a>

  为当前的接入应用创建一个应用级别的钱包，所有用户钱包的激活及GAS的充值，都需要或者可以通过该钱包来进行转账。  
- 接口地址：/v1/app/createAppWallet
- 请求方式：GET/POST
 接口参数：
 
| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|accessToken|String|访问凭证|
|chainCodes|String|【可选】区块链编码（多个值，用逗号分隔），目前支持jingtum和moac。如果指定该参数，会在创建App钱包之前为当前的App应用系统关联上对应的公链。也可以使用2.5节中的选择区块链接口预先进行公链的关联。此参数值可为空|
|onlyWallet|boolean|【可选】是否仅生成钱包（默认值为false）,如果为true，那么只生成钱包，不到关联的公链上创建账户，默认会创建账户。|  

- 请求示例：
---
![](./pics/%E8%BF%94%E5%9B%9E%E7%A4%BA%E4%BE%8B4.jpg?raw=true)
---
- 返回的结果信息：

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功）|
|data|Object|返回数据|
|walletAddr|String|钱包地址,通过该地址可以找到账户|
|userId|String|用户Id|
|password|String|查询密码|
|accounts|list|账户列表|
|chainCode|String |区块链的编码|
|account|String|账户|

- 返回示例：

![](./pics/%E8%BF%94%E5%9B%9E%E7%A4%BA%E4%BE%8B5.jpg?raw=true)
---

### <a name="2.4. 创建用户钱包">2.4. 创建用户钱包</a>  
为注册的企业应用系统中的用户创建用户钱包，每个人仅可以创建一个用户钱包，以传入的用户名作为应用系统中的唯一标识，密码是用户用来查询其余额和交易记录等相关使用。  
- 接口地址：/v1/app/createWallet  
- 请求方式：GET/POST
- 接口参数：

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
| accessToken |String|访问凭证|
|userId|String|用户Id|
|password|String|查询密码|
|onlyWallet|boolean|【可选】是否仅生成钱包（默认值为false）,如果为true，那么只生成钱包，不到关联的公链上创建账户，默认会创建账户。|  


- 请求示例：
---
![image](./pics/%E8%AF%B7%E6%B1%82%E7%A4%BA%E4%BE%8B5.jpg?raw=true)
---
| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功）|
|data|Object|返回数据|
|appId|String|应用Id|
|userId|String|用户Id|
|accounts|list|账户列表|
|chainCode|String|区块链编码|
|account|String|账户|  

- 返回示例：
![iamge](./pics/%E8%BF%94%E5%9B%9E%E7%A4%BA%E4%BE%8B6.jpg?raw=true)  

### <a name="2.5. 选择区块链[可选]">2.5. 选择区块链[可选]</a>  
 接入系统在接入区块链时到底接入哪个或哪些公链呢？不像其它平台，在火花链接入平台中，把这个选择的权利完全交给接入系统自己，接入系统不仅能选择块链，同时还可以通过接口来注册相关的公链到火花链平台（未开放），然后进行选择。选择区域链的操作已经集成到创建企业钱包中，没有特殊的要求，不需要单独调用该接口来进行区域链的选择。  
- 接口地址：/v1/app/selectChain  
- 请求方式：GET/POST  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|accessToken|String|访问凭证|
|chainCodes|String|区块链编码（多个值时，用逗号分隔），目前支持jingtum和moac，可二选一|
- 请求示例：
---
![iamge](./pics/%E8%AF%B7%E6%B1%82%E7%A4%BA%E4%BE%8B6.jpg?raw=true)
---
- 返回的结果信息：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功）|
|data|Object|返回数据|  

- 返回示例：  
---
![image](./pics/%E8%BF%94%E5%9B%9E%E7%A4%BA%E4%BE%8B7.jpg?raw=true)  
---

### <a name="2.6. 选择通证[可选]">2.6. 选择通证[可选]</a>

 接入不同的公链之后，接入系统需要关注的是在其接入系统中需要使用哪一些代币（通证）来进行交易，比如接入系统可以自己发行自己的币种，然后采用自己发行的币种在自己的接入系统中进行交易，这个时候就需要给不同接入系统选择不同的代币（通证）的权利。  
 选择通证的前提是需要发布第三方通证，可以通过第五章的接口进行发布，也可以在交流群中联系管理员进行后台的发布。  
 如果不发行代币的话或者不使用第三方代币的话，那么就没有必要使用该接口来选择通证，对于原生通证（如moac链对应的MOAC代币及jingtum链对应的SWT代币）在创建App钱包时就已经进行了关联，没有必要再进行选择。  
- 接口地址：/v1/app/selectToken  
- 请求方式：GET/POST
- 接口参数：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|accessToken|String|访问凭证|
|chainCode|String|区块链编码(目前支持jingtum和moac)|
|tokenCodes|String|通证编码（多个值时，用逗号分隔）|  
- 请求示例：
---
![image](./pics/%E8%AF%B7%E6%B1%82%E7%A4%BA%E4%BE%8B7.jpg?raw=true)  
---

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功）|
|data|Object|返回数据|  
- 返回示例：
![image](./pics/%E8%BF%94%E5%9B%9E%E7%A4%BA%E4%BE%8B8.jpg?raw=true)

### <a name="2.7. 同步所有钱包[可选]">2.7. 同步所有钱包[可选]</a>. 

 接入应用系统已经创建了App钱包和用户钱包并进行交易，有可能需要在应用系统中增加新的公链支持或代币（通证）支持，那么就需要通过选择区块链和和选择通证来进行关联，这时需要为所有用户钱包和app钱包创建新加公链的账户及账户下面的各种不同的代币的余额。  
这就需要采用当前的接口来同步所有钱包，为接入应用系统的所有钱包都加创建新链的账户和初始化新币种的余额。因为调用该接口需要较长时间，平台采用异步处理方式，处理完成之后调用2.1节中msgCallBackUrl参数指定的回调地址回写处理结果，也可能通过调用2.8节中的系统消息来查看其处理结果。  
可见，使用火花链接入平台中接入的话，不需要在接入初始化时考虑过多的需求，可以先接入应用，然后再逐步完善所需要的上链处理。所有的技术细节都屏蔽在火花链接入平台，提供一个简单易用的区块链接入方式。  
- 接口地址：/v1/app/syncAllWallet
- 请求方式：GET/POST  
- 接口参数：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|accessToken|String|访问凭证|  
- 提交示例：
---
![image](./pics/%E6%8F%90%E4%BA%A4%E7%A4%BA%E4%BE%8B1.jpg?raw=true)
---
- 返回的结果信息：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|data|Object|数据|
|success|boolean|True:表明成功|
- 返回示例：  

![image](./pics/%E8%BF%94%E5%9B%9E%E7%A4%BA%E4%BE%8B9.jpg?raw=true)

### <a name="2.8. 获取系统消息[可选]">2.8. 获取系统消息[可选]</a>  
 接入业务系统在使用火花链接入平台过程，会产生各种不同的系统消息，这些系统消息都保存在接入业务系统对应的消息库中。有的接口会调用注册的消息回调处理（2.1节中的参数）进行回写，有的接口会直接返回。也可以使用当前接口来获取其完整的系统消息列表。  
- 接口地址：/v1/app/sysMsg  
- 请求方式：GET/POST
- 接口参数：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|accessToken|String|访问凭证|
|msgType|String|【可选】消息类型|
|userId|String|【可选】用户Id|
|msgState|Integer|【可选】消息状态|
|pagesize|Integer|【可选】返回的每页数据量，默认每页10项|
|pagenum|Integer|【可选】返回第几页的数据，默认从1开始|  
- 提交示例：
---
![image](./pics/提交示例2.jpg?raw=true)
---

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|data|	Object |数据|
|result|list|结果信息|
|appid|Long|对应的appid|
|createtime|String|创建时间|
|id|String|消息id|
|msgs|String|消息内容|
|state|Integer|消息状态|
|type|String|消息类型|
|userid|String|用户id|
|viewtime|Long|查看时间|
- 返回示例：
![image](./pics/返回示例10.jpg?raw=true)

