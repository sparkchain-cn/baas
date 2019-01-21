#### <a href="./chapter10.md#top">返回上一级目录</a>      
---
## 4. 瑞波公链（xrp）
---

**（1）浏览器**

正式链（账户查询）：[https://xrpcharts.ripple.com/#/graph](https://xrpcharts.ripple.com/#/graph)
正式链（交易查询）：[https://xrpcharts.ripple.com/#/transactions](https://xrpcharts.ripple.com/#/transactions)

测试币获取地址：[https://developers.ripple.com/xrp-test-net-faucet.html](https://developers.ripple.com/xrp-test-net-faucet.html)

`注意：瑞波目前没有提供测试链的浏览器`

**（2）保留的小数位数**：6

**（3）激活账户**：

 该公链上的新账户，需要用20个XRP激活，否则公链视其为无效账户。

**（4）冻结费用**：

* 激活账户用的20个XRP，会冻结，不能消费。

（5）**火花平台接口的参数，使用条件和限制**：

* 参数：chainCode（公链编码）

	* 正式链（使用正式币）：xrp

	* 测试链（使用测试币）：xrpTest

* 参数：tokenCode（通证编码）

	* 原生的通证（币）：XRP

	
* 转账上链的gas费用（gasFee）

	所有的转账和上链，消耗的gas费用是原生币，且gas费用为固定值，目前是0.0001XRP（`由公链收取`）

* 转账上链成功的币数条件

	* 转账币数>0

	* 有足够币数

		* **原生的通证** 转账或上链：

			剩余币数>=转账币数+gas费用+冻结币数

* memo长度限制

	单字节文字数：900个

	双字节文字数：300个






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

