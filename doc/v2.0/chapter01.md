#### <a href="./index.md#top">返回上一级目录</a>      

## 目录
=========================== 

<a href="./chapter01.md#1. 引言">1. 引言</a>  <br>
<a href="./chapter01.md#1.1. 概述">1.1. 概述</a>  <br>
<a href="./chapter01.md#1.2. 名词解释">1.2. 名词解释</a>  <br>
<a href="./chapter01.md#1.3. 统一说明">1.3. 统一说明</a>  <br>

### <a name="1. 引言">1. 引言</a>

引言部分主要包括概述、名词解释和统一说明三部分。

### <a name="1.1. 概述">1.1. 概述</a>

火花区块链接入平台是对接于各行各业应用和各大公链之间的接入平台，采用一系列技术来提高公链的接入TPS，并统一公链之间的接入差异，简化应用的区块链接入，使用一套接口就能快速在各种不同公链之间进行切换或跨链交易。

### <a name="1.2. 名词解释">1.2. 名词解释</a>

 
| 名词         | 英文       | 说明   |
| :------------- |:-------------| :-----|
| 钱包| wallet| 火花区块链接入平台中的钱包，一个钱包可以包括多个不同公链上的账户，把不同公链中的账户统一起来，实现跨链交易。|
| 钱包地址|walletAddr| 火花区块链接入平台中的钱包的地址，通过该地址可以查询其下所有账户的余额和流水，配置钱包支付密码，可以进行跨链转账。|
|密码| password |钱包的查询密码，用于设置钱包的支付密码。 |
|支付密码| payPassword | 钱包的支付密码，用于钱包的转账或者上链。|
|账户|account  | 账户对应着公链中的公钥地址（钱包）。|
|私钥 |privateKey | 账户的私钥 |
|App钱包|App wallet|每个在火花区块链接入平台注册的应用系统，都需要创建一个应用级别的钱包，该钱包就是APP钱包。|
|用户钱包|User wallet|接入的应用系统的用户也需要钱包来进行业务上的交易，该用户对应的火花区块链接入平台钱包就是用户钱包。|  
|公链|chain|公链的使用，请参看“<a href="./chapter10.md#top">附2：各公链的使用说明</a>”。|  

### <a name="1.3. 统一说明">1.3. 统一说明</a>  

- 1：接口地址    
系统域名:[https://dapi.sparkchain.cn](https://dapi.sparkchain.cn)，以下章节中所设计的接口地址都需要在访问时加上该测试系统域名，如接入系统初始化的接口地址为：/v1/app/init，  
那么在浏览器中则使用[https://dapi.sparkchain.cn/v1/app/init](https://dapi.sparkchain.cn/v1/app/init)即可。 

**注意：调用接口时，请务必使用https方式，保证传输内容不被篡改。**


<font color=Red> 
注意：如果需要运行在测试公链上，请在设置公链名称时，加上“Test”后缀，比如：公链名称(chainCode)为“jingtum”，那么设置为“jingtumTest”，通证编码（tokenCode）,仍为“SWT”不受影响。测试公链上使用的测试币，可以咨询管理员。
</font>

- 2：返回格式  
    接口返回格式统一，采用JSON格式返回，JSON格式中包括 success, code，message和data。如下图1所示：
  
 ![image](./pics/1528702150106.jpg?raw=true)
---  
图1 接口统一的格式  

Code：接口处理的标识，其中 成功：200, 请求失败: 400，未认证:401, 服务器内部错误:505。其它的code的代表业务错误编码。 
 
Message：返回的消息，主要是指错误的返回信息，对于正确的返回，也有可能会给出一些提示信息和警告信息。Data:返回的业务数据。  

- 3：问题及沟通
 火花区块链开发者QQ总群：594629943  
 火花区块链开发者微信群，扫下方二维码加好友，备注火花区块链开发，然后拉进群。  
![image](./pics/wechat.jpg?raw=true)
---




## 官方联系方式

### 官方QQ群

![QQ群：594629943](../sp.png)


## 第三方合作伙伴

 - <a href="https://www.jingtum.com/">井通科技</a>,github地址为：https://github.com/swtcpro ，开发者文档地址：http://developer.jingtum.com/  浏览器地址：http://state.jingtum.com

 - <a href="http://www.moac.io/">MOAC</a>,github地址为：ttps://github.com/MOACChain/,开发者文档地址：https://github.com/MOACChain/moac-core/wiki/Commands ,https://github.com/MOACChain/moac-core/wiki/Chain3 ,浏览器地址：http://explorer.moac.io/home

