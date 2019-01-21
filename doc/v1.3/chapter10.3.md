#### <a href="./chapter10.md#top">返回上一级目录</a>      
---
## 3. 墨客公链（moac）


### **（1）浏览器**

正式链：[http://explorer.moac.io/home](http://explorer.moac.io/home)

测试链：[http://47.75.144.55:3000/home](http://47.75.144.55:3000/home)

### **（2）保留的小数位数**：18

### **（3）该公链上gas相关名词的说明**：

![image](./pics/moacchain_block.png?raw=true)
* Gas Price：gas单价

	根据公链情况设置的一个gas单价，价格越高，就会越快写入区块（上链更快）。可价格较低，就可能需要等待较长时间才能写入区块，至于等待的时长要视各公链的实际情况决定。当然价格过低，也会导致直接上链失败。
* Gas Used：实际使用的gas个数

	公链根据上链内容计算出来的gas个数。memo内容较多，使用代币转账等，都需要更多的gas数。

* Gas Limit：预估gas数上限值

	实际使用的gas个数（gasUsed）不能超过这个值，否则将导致交易或上链失败。所以当memo较大，或者使用发行代币进行转账或上链时，gasLimit需要设置大一些。

* gasFee：实际消耗的gas费用

	gas费用=gasPrice*gasUsed


### **（4）火花平台接口的参数，使用条件和限制**：

* **参数：chainCode（公链编码）**

	* 正式链（使用正式币）：moac

	* 测试链（使用测试币）：moacTest

* **参数：tokenCode（通证编码）**

	* 原生的通证（币）：MOAC

	* 非原生的通证（币）
	
    	已发行的代币（通过ERC20智能合约发行的代币）。

		`注意：火花平台提供了在该公链上发行代币的接口，详见“8.2. 新增通证”。也可以把该公链上已存在的代币加入火花平台，然后用“2.6. 选择通证”接口，让接入的应用绑定该代币。`

* **参数：gasLimit（预估gas数上限值）**

	默认值：40000
	
	`注意：可以自行设置。代币的转账时，gasLimit需要设置更大，比如设置为200000。`

* **参数：gasPrice（gas单价）**
	默认值：25000000000

	`注意：可以自行设置,一般单价设置越高，写入区块会更快些。`

* **转账上链的gas费用（gasFee）**
	
	* 所有的转账和上链，消耗的gas费用是原生币（MOAC）

	* gas费用不是固定值（`由公链收取`），由gasPrice和gasUsed值决定。gas费用=gasPrice*gasUsed，但是与gasLimit的值息息相关，gasUsed不能小于gasLimit。

* **转账上链成功的币数条件**

	* 转账币数>=0

	* 有足够币数

		* **原生的通证** 转账或上链：
		
			剩余币数>=转账币数+预估gas费用

		* **非原生的通证** 转账或上链：
			
			原生的剩余币数>=预估gas费用

			非原生的剩余币数>=转账币数
			
			`注意：预估gas费用=gasPrice*gasLimit`

* **memo长度限制**

	不限长度，字符数越多，gasUsed越多，gas费用就越高。当memo内容比较多时，为保证上链成功，gasLimit需要设置更大些。





## 官方联系方式

### 官方QQ群

![QQ群：594629943](../sp.png)

### 官方技术交流论坛
  欢迎大家到<a href="http://sparkda.com/">斯巴达论坛</a>进行提问及交流 

### 官方技术BAAS平台
  欢迎大家到<a href="http://baas.sparkchain.cn/">火花区块链BaaS平台</a>发现更多好玩的Dapp（目前正开发中）


## 第三方合作伙伴

 - <a href="https://www.jingtum.com/">井通科技</a>,github地址为：https://github.com/swtcpro ，开发者文档地址：http://developer.jingtum.com/  浏览器地址：http://state.jingtum.com

 - <a href="http://www.moac.io/">MOAC</a>,github地址为：ttps://github.com/MOACChain/,开发者文档地址：https://github.com/MOACChain/moac-core/wiki/Commands ,https://github.com/MOACChain/moac-core/wiki/Chain3 ,浏览器地址：http://explorer.moac.io/home

 - 南昌技术开发团队,github地址为:https://github.com/moacDapp/ ,QQ群：

 ![QQ群：805362142](../nc.png)

