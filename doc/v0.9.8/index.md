<div align=center>
![image](https://github.com/codeboxcat/python/blob/master/image1.png?raw=true)
---
<font color=#0099ff size=48 face="黑体">**火花链接入平台**


**标准服务接口**</font> 
---

<font color=#0099ff size=4 face="黑体"><center>通用版</center></font> 


<img src="https://github.com/codeboxcat/python/blob/master/image2.png?raw=true" width="70" height="40" />

  
  <br /><br /><br /><br /><br /><font color=#0099ff size=4 face="黑体">烨链（上海）科技有限公司<br /><br /><br /><br /><br />
  



  

---
<font color=black size=2>**修改记录**</font>  

| 版本号         | 发布时间       | 内容   |
| :------------- |:-------------| :-----|
| V0.1          | 2018/3/28    | 初版             |
| V0.2          |2018/3/29     | 统一数据格式      |
|V0.3           | 2018/4/24     |   扩展文本上链接口 |
|V0.9           | 2018/5/20     |  重构及跨链支持    |
|V0.9.1          |2018/5/27   |   调整和优化部分接口参数，增加accessToken的使用方式 |
|V0.9.2         |2018/6/1   |   丰富大量接口，调整部分接口参数  |
  
  <br /><br /><br /> <br /><br /><br /><br /><br /><font color=black size=4>**目录**</font>
  
###<p align="left"><a href="#1. 引言">1. 引言</a>  
######<p align="left"><a href="#1.1. 概述">1.1. 概述</a>  
######<p align="left"><a href="#1.2. 名词解释">1.2. 名词解释</a>
######<p align="left"><a href="#1.3. 统一说明">1.3. 统一说明</a>

###<p align="left"><a href="#2. 接入系统接口">2. 接入系统接口</a>
######<p align="left"><a href="#2.1. 接入系统初始化">2.1. 接入系统初始化</a>
######<p align="left"><a href="#2.2. 生成访问凭证">2.2. 生成访问凭证</a>
######<p align="left"><a href="#2.3. 创建企业钱包">2.3. 创建企业钱包</a>
######<p align="left"><a href="#2.4. 创建用户钱包">2.4. 创建用户钱包</a>
######<p align="left"><a href="#2.5. 选择区块链[可选]">2.5. 选择区块链[可选]</a>
######<p align="left"><a href="#2.6. 选择通证[可选]">2.6. 选择通证[可选]</a>
######<p align="left"><a href="#2.7. 同步所有钱包[可选]">2.7. 同步所有钱包[可选]</a>
######<p align="left"><a href="#2.8. 获取系统消息[可选]">2.8. 获取系统消息[可选]</a>





   <font color=gray size=3>火花链接入平台标准服务接口</font>  
---  
#<p align="left"><a name="1. 引言">1. 引言</a>

<p align="left">引言部分主要包括概述、名词解释和统一说明三部分。 </p>  



**<p align="left"><a name="1.1. 概述">1.1. 概述</a>**

&ensp; &ensp;火花链接入平台是对接于各行各业应用和各大公链之间的接入平台，采用一系列技术来提高公链的接入TPS，并统一公链之间的接入差异，简化应用的区块链接入，使得一套接口能快速在各种不同公链之间进行切换或进行跨链交易。

**<p align="left"> <a name="1.2. 名词解释">1.2. 名词解释</a>**

 
| 名词         | 英文       | 说明   |
| :------------- |:-------------| :-----|
| 钱包| wallet| 火花链接入平台中的钱包，一个钱包可以包括多个不同公链上的账户，把不同公链中的账户统一起来，实现跨链交易。|
| 钱包地址|walletAddr| 火花链接入平台中的钱包的地址，通过该地址可以查询其下所有账户的余额和流水，配置钱包支付密码，可以进行跨链转账。|
|密码| password |钱包的密码，通过该密码，用户可以查询其下所有账户的余额和流水 |
|支付密码| payPassword | 钱包的支付密码|
|账户|account  | 账户对应着公链中的钱包，代表公链钱包中的公钥地址。|
|私钥 |c | 账户的私钥 |
|App钱包|App wallet|每个在火花链接入平台注册的应用系统，都需要创建一个应用级别的钱包，该钱包就是APP钱包。|
|用户钱包|User wallet|接入的应用系统的用户也需要钱包来进行业务上的交易，该用户对应的火花链接入平台钱包就是用户钱包。|  

 **<p align="left">	<a name="1.3. 统一说明">1.3. 统一说明</a>**  
 <p align="left">1：接口地址    
 &ensp; &ensp;测试系统域名:[https://tapi.sparkchain.cn](https://tapi.sparkchain.cn)，以下章节中所设计的接口地址都需要在访问时加上该测试系统，如接入系统初始化的接口地址为：/v1/app/init，  
那么在浏览器中则使用[https://tapi.sparkchain.cn/v1/app/init](https://tapi.sparkchain.cn/v1/app/init)即可。  
 <p align="left">2：返回格式  
    &ensp; &ensp;接口返回格式统一，采用JSON格式返回，JSON格式中包括 success,code，message和data。如下图1所示：
    <div align=center>
![image](./pics/1528702150106.jpg?raw=true)
---  
图1 接口统一的格式  
&ensp; &ensp;Code：接口处理的标识，其中 成功：200, 请求失败: 400，未认证:401, 服务器内部错误:505。其它的code的代表业务错误编码。 
 
&ensp; &ensp;Message：返回的消息，主要是指错误的返回信息，对于正确的返回，也有可能会给出一些提示信息和警告信息。Data:返回的业务数据。  

 <p align="left">3：问题及沟通
 火花链BaaS开发者QQ总群：594629943  
 &ensp; &ensp;火花链BaaS开发者微信群，扫下方二维码加好友，备注火花链BaaS开发，然后拉进群。  <div align=center>
![image](./pics/问题及沟通微信二维码.jpg?raw=true)
---

 
#<p align="left"> <a name="2. 接入系统接口">2. 接入系统接口</a>
  
  

接入系统接口为业务系统上链提供了一系列的接口，首先接入系统得在火花链接入平台进行注册初始化，换取接入应用系统的accessToken。然后就可以根据初始化的相关信息来创建应用系统级别的APP钱包，创建App钱包之后，根据业务所需，为其应用系统中用户在火花链接入平台中创建用户钱包。之后的上链或交易就发生在这些钱包之间。

**<p align="left"> <a name="2.1. 接入系统初始化">2.1. 接入系统初始化</a>**
   
 &ensp; &ensp;接入系统初始化对业务系统上链相关的信息进行初始化，主要传入业务系统编号、名称及回调地址,成功时返回appid和appsecret。  
 <p align="left">接口地址：/v1/app/init. 
 <p align="left">请求方式：GET/POST  
 提交参数：  
 
| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|appcode|String|业务系统编号,一般用业务系统的拼音缩写或英文|
|appname|String|业务系统名称，一般用中文名|
|transCallBackUrl|String|【可选】业务系统在进行交易时，不能立即返回状态，通过该地址进行回调，获取事务的返回状态|
|msgCallBackUrl|String|【可选】通过该地址进行回调，获取消息的返回值|
|userid|String|【可选】传入租户ID（针对租用平台和企业统一上链接入平台）|
<p align="left">请求示例：
---
![image](./pics/请求示例.jpg?raw=true)
---

<p align="left">返回的结果信息：

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功）|
|data|Object|返回数据|
|appid|String|业务系统ID|
|appsecret|String|业务系统的秘钥|
<p align="left">返回示例：
---
![image](./pics/返回示例.jpg?raw=true)
---
 
**<p align="left">	<a name="2.2. 生成访问凭证">2.2. 生成访问凭证</a></p>**  
 
<p align="left">调用其它接口时，一般都需要访问凭证。通过此接口就可以获取访问凭证accessToken，访问凭证有一定的时效性（目前2个小时）。  
<font color=Red >如果需要在代码中使用访问凭证，可以参考附1的简单示例（java语言）  
<p align="left"><font color=#0099ff >接口地址：/v1/app/access  
请求方式：GET/POST  
接口参数：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|appid|String|业务系统的ID|
|appsecret|String|业务系统的秘钥|  
<p align="left">请求示例： 
--- 
![image](./pics/请求示例2.jpg?raw=true)
---
<p align="left">返回的结果信息： 
 
| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功）|
|data|Object|返回数据|
|accessToken|String|访问凭证|
<p align="left">返回示例：
---
![image](./pics/返回示例3.jpg?raw=true)
  
**<p align="left"><a name="2.3. 创建企业钱包">2.3. 创建企业钱包</a></p>**  
  为当前的接入应用创建一个应用级别的钱包，所有用户钱包的激活及GAS的充值，都需要或者可以通过该钱包来进行转账。  
 <p align="left">接口地址：/v1/app/createAppWallet
 <p align="left">请求方式：GET/POST
 接口参数：
 
| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|accessToken|String|访问凭证|
|chainCodes|String|【可选】区块链编码（多个值，用逗号分隔），目前支持jingtum和moac。如果指定该参数，会在创建App钱包之前为当前的App应用系统关联上对应的公链。也可以使用2.5节中的选择区块链接口预先进行公链的关联。此参数值可为空|
|onlyWallet|boolean|【可选】是否仅生成钱包（默认值为false）,如果为true，那么只生成钱包，不到关联的公链上创建账户，默认会创建账户。|  

<p align="left">请求示例：
---
![](./pics/%E8%BF%94%E5%9B%9E%E7%A4%BA%E4%BE%8B4.jpg?raw=true)
---
<p align="left">返回的结果信息：

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

<p align="left">返回示例：

![](./pics/%E8%BF%94%E5%9B%9E%E7%A4%BA%E4%BE%8B5.jpg?raw=true)
---

**<p align="left"><a name="2.4. 创建用户钱包">2.4. 创建用户钱包</a></p>**  
 &ensp; &ensp;为注册的企业应用系统中的用户创建用户钱包，每个人仅可以创建一个用户钱包，以传入的用户名作为应用系统中的唯一标识，密码是用户用来查询其余额和交易记录等相关使用。  
<p align="left">接口地址：/v1/app/createWallet  
<p align="left">请求方式：GET/POST
<p align="left">接口参数：

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
| accessToken |String|访问凭证|
|userId|String|用户Id|
|password|String|查询密码|
|onlyWallet|boolean|【可选】是否仅生成钱包（默认值为false）,如果为true，那么只生成钱包，不到关联的公链上创建账户，默认会创建账户。|  


<p align="left">请求示例：
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

<p align="left">返回示例：
![iamge](./pics/%E8%BF%94%E5%9B%9E%E7%A4%BA%E4%BE%8B6.jpg?raw=true)  
**<p align="left"><a name="2.5. 选择区块链[可选]">2.5. 选择区块链[可选]</a>**  
&ensp; &ensp;接入系统在接入区块链时到底接入哪个或哪些公链呢？不像其它平台，在火花链接入平台中，把这个选择的权利完全交给接入系统自己，接入系统不仅能选择块链，同时还可以通过接口来注册相关的公链到火花链平台（未开放），然后进行选择。选择区域链的操作已经集成到创建企业钱包中，没有特殊的要求，不需要单独调用该接口来进行区域链的选择。  
<p align="left">接口地址：/v1/app/selectChain  
<p align="left">请求方式：GET/POST  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|accessToken|String|访问凭证|
|chainCodes|String|区块链编码（多个值时，用逗号分隔），目前支持jingtum和moac，可二选一|
<p align="left">请求示例：
---
![iamge](./pics/%E8%AF%B7%E6%B1%82%E7%A4%BA%E4%BE%8B6.jpg?raw=true)
---
<p align="left">返回的结果信息：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功）|
|data|Object|返回数据|  

<p align="left">返回示例：  
---
![image](./pics/%E8%BF%94%E5%9B%9E%E7%A4%BA%E4%BE%8B7.jpg?raw=true)  
---

**<p align="left"><a name="2.6. 选择通证[可选]">2.6. 选择通证[可选]</a></p>** 

&ensp; &ensp;接入不同的公链之后，接入系统需要关注的是在其接入系统中需要使用哪一些代币（通证）来进行交易，比如接入系统可以自己发行自己的币种，然后采用自己发行的币种在自己的接入系统中进行交易，这个时候就需要给不同接入系统选择不同的代币（通证）的权利。  
&ensp; &ensp;选择通证的前提是需要发布第三方通证，可以通过第五章的接口进行发布，也可以在交流群中联系管理员进行后台的发布。  
&ensp; &ensp;如果不发行代币的话或者不使用第三方代币的话，那么就没有必要使用该接口来选择通证，对于原生通证（如moac链对应的MOAC代币及jingtum链对应的SWT代币）在创建App钱包时就已经进行了关联，没有必要再进行选择。  
<p align="left">接口地址：/v1/app/selectToken  
<p align="left">请求方式：GET/POST
<p align="left">接口参数：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|accessToken|String|访问凭证|
|chainCode|String|区块链编码(目前支持jingtum和moac)|
|tokenCodes|String|通证编码（多个值时，用逗号分隔）|  
<p align="left">请求示例：
---
![image](./pics/%E8%AF%B7%E6%B1%82%E7%A4%BA%E4%BE%8B7.jpg?raw=true)  
---

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|success|boolean|是否成功（true：成功）|
|data|Object|返回数据|  
<p align="left">返回示例：
![image](./pics/%E8%BF%94%E5%9B%9E%E7%A4%BA%E4%BE%8B8.jpg?raw=true)
**<p align="left"><a name="2.7. 同步所有钱包[可选]">2.7. 同步所有钱包[可选]</a>**. 
&ensp; &ensp;接入应用系统已经创建了App钱包和用户钱包并进行交易，有可能需要在应用系统中增加新的公链支持或代币（通证）支持，那么就需要通过选择区块链和和选择通证来进行关联，这时需要为所有用户钱包和app钱包创建新加公链的账户及账户下面的各种不同的代币的余额。  
&ensp; &ensp这就需要采用当前的接口来同步所有钱包，为接入应用系统的所有钱包都加创建新链的账户和初始化新币种的余额。因为调用该接口需要较长时间，平台采用异步处理方式，处理完成之后调用2.1节中msgCallBackUrl参数指定的回调地址回写处理结果，也可能通过调用2.8节中的系统消息来查看其处理结果。  
&ensp; &ensp可见，使用火花链接入平台中接入的话，不需要在接入初始化时考虑过多的需求，可以先接入应用，然后再逐步完善所需要的上链处理。所有的技术细节都屏蔽在火花链接入平台，提供一个简单易用的区块链接入方式。  
<p align="left">接口地址：/v1/app/syncAllWallet
<p align="left">请求方式：GET/POST  
<p align="left">接口参数：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|accessToken|String|访问凭证|  
<p align="left">提交示例：
---
![image](./pics/%E6%8F%90%E4%BA%A4%E7%A4%BA%E4%BE%8B1.jpg?raw=true)
---
<p align="left">返回的结果信息：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|code|String|请求结果|
|message|String|返回信息|
|data|Object|数据|
|success|boolean|True:表明成功|
<p align="left">返回示例：  

![image](./pics/%E8%BF%94%E5%9B%9E%E7%A4%BA%E4%BE%8B9.jpg?raw=true)
**<p align="left"><a name="2.8. 获取系统消息[可选]">2.8. 获取系统消息[可选]</a>**  
&ensp; &ensp接入业务系统在使用火花链接入平台过程，会产生各种不同的系统消息，这些系统消息都保存在接入业务系统对应的消息库中。有的接口会调用注册的消息回调处理（2.1节中的参数）进行回写，有的接口会直接返回。也可以使用当前接口来获取其完整的系统消息列表。  
<p align="left">接口地址：/v1/app/sysMsg  
<p align="left">请求方式：GET/POST
<p align="left">接口参数：  

| 参数         | 类型       | 说明   |
| :------------- |:-------------| :-----|
|accessToken|String|访问凭证|
|msgType|String|【可选】消息类型|
|userId|String|【可选】用户Id|
|msgState|Integer|【可选】消息状态|
|pagesize|Integer|【可选】返回的每页数据量，默认每页10项|
|pagenum|Integer|【可选】返回第几页的数据，默认从1开始|  
<p align="left">提交示例：
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
<p align="left">返回示例：
![image](./pics/返回示例10.jpg?raw=true)
















 
 
 
  
  