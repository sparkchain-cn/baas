## 火花区块链接入平台 2.0 文档

火花区块链接入平台是对接于各行各业应用和各大公链之间的接入平台，采用一系列技术来提高公链的接入TPS，并统一公链之间的接入差异，简化应用的区块链接入，使得一套接口能快速在各种不同公链之间进行切换或进行跨链交易。

   - 开始支持EOS、XRP链，只需要在使用过程中把其chainCode换成eos,xrp。它们对应的原生token分别为EOS,XRP。
   - 细化上链返回状态。
   - 为了限制某些应用不正常的访问，本版本对所有的访问加上次数的统计，在不久的将来采用经济手段来限制过大量的访问。
   - 添加各公链的使用说明。
   
### 火花区块链接入平台 2.0版API目录
<a href="./chapter01.md#1. 引言">1. 引言</a>  <br>
* <a href="./chapter01.md#1.1. 概述">1.1. 概述</a>  <br>
* <a href="./chapter01.md#1.2. 名词解释">1.2. 名词解释</a>  <br>
* <a href="./chapter01.md#1.3. 统一说明">1.3. 统一说明</a>  <br>

<a href="./chapter02.md#2. 接入系统接口">2. 接入系统接口</a>  <br>
* <a href="./chapter02.md#2.1. 接入系统初始化">2.1. 接入系统初始化</a>  <br>
* <a href="./chapter02.md#2.2. 生成访问凭证">2.2. 生成访问凭证</a>  <br>
* <a href="./chapter02.md#2.3. 选择区块链">2.3. 选择区块链</a>  <br>
* <a href="./chapter02.md#2.4. 创建企业钱包">2.4. 创建企业钱包</a>  <br>
* <a href="./chapter02.md#2.5. 创建用户钱包">2.5. 创建用户钱包</a>  <br>
* <a href="./chapter02.md#2.6. 选择通证">2.6. 选择通证</a>  <br>
* <a href="./chapter02.md#2.7. 同步所有钱包">2.7. 同步所有钱包</a><br>
* <a href="./chapter02.md#2.8. 获取系统消息[可选]">2.8. 获取系统消息[可选]</a><br>
* <a href="./chapter02.md#2.9. 获取应用的区块链信息">2.9. 获取应用的区块链信息</a><br>

<a href="./chapter03.md#3. 用户钱包操作接口">3. 用户钱包操作接口</a>  <br> 
* <a href="./chapter03.md#3.1. 设置支付密码">3.1. 设置支付密码</a>  <br> 
* <a href="./chapter03.md#3.2. 钱包支付请求">3.2. 钱包支付请求</a>  <br>
* <a href="./chapter03.md#3.2.1 钱包转账">3.2.1 钱包转账</a>  <br>
* <a href="./chapter03.md#3.2.2 用户转账">3.2.2 用户转账</a>  <br>
* <a href="./chapter03.md#3.2.3 账户转账">3.2.3 账户转账</a>  <br>
* <a href="./chapter03.md#3.2.4 多方式转账">3.2.4 多方式转账</a>  <br>
* <a href="./chapter03.md#3.3. 获取钱包余额">3.3. 获取钱包余额</a>  <br>
* <a href="./chapter03.md#3.4. 获得支付信息">3.4. 获得支付信息</a>  <br>
* <a href="./chapter03.md#3.5. 获得支付历史">3.5. 获得支付历史</a>  <br>
* <a href="./chapter03.md#3.6. 获取钱包账户的信息">3.6. 获取钱包账户的信息</a> <br>

<a href="./chapter04.md#4. 用户账户接口">4. 用户账户接口</a>  <br> 
* <a href="./chapter04.md#4.1. 创建账户">4.1. 创建账户</a>  <br>
* <a href="./chapter04.md#4.2. 账户充值">4.2. 账户充值</a>  <br>
* <a href="./chapter04.md#4.3. 账户的支付请求">4.3. 账户的支付请求</a>  <br>
* <a href="./chapter04.md#4.4. 获取账户余额">4.4. 获取账户余额</a>  <br>
* <a href="./chapter04.md#4.5. 获取账户支付信息">4.5. 获取账户支付信息</a>  <br>
* <a href="./chapter04.md#4.6. 获取账户支付历史">4.6. 获取账户支付历史</a>  <br>
* <a href="./chapter04.md#4.7. 账户的文本上链">4.7. 账户的文本上链</a>  <br>

<a href="./chapter05.md#5. 用户钱包账户关联">5. 用户钱包账户关联</a>  <br>
* <a href="./chapter05.md#5.1. 绑定单个账户">5.1. 绑定单个账户</a>  <br> 
* <a href="./chapter05.md#5.2. 绑定多个账户">5.2. 绑定多个账户</a>  <br> 

<a href="./chapter06.md#6. 文本上链接口">6. 文本上链接口</a>  <br>
* <a href="./chapter06.md#6.1. 文本上链">6.1. 文本上链</a>  <br>
* <a href="./chapter06.md#6.2. 查询文本内容">6.2. 查询文本内容</a>  <br>
* <a href="./chapter06.md#6.3. 查询文本列表">6.3. 查询文本列表</a>  <br>

<a href="./chapter07.md#7. 用户钱包密码接口">7. 用户钱包密码接口</a>  <br>
* <a href="./chapter07.md#7.1 修改查询密码">7.1 修改查询密码</a>  <br>
* <a href="./chapter07.md#7.2. 重置查询密码">7.2. 重置查询密码</a>  <br>
* <a href="./chapter07.md#7.3. 验证查询密码">7.3. 验证查询密码</a>  <br>
* <a href="./chapter07.md#7.4. 修改支付密码">7.4. 修改支付密码</a>  <br>
* <a href="./chapter07.md#7.5. 重置支付密码">7.5. 重置支付密码</a>  <br>
* <a href="./chapter07.md#7.6. 验证支付密码">7.6. 验证支付密码</a>  <br>

<a href="./chapter08.md#8. 系统管理接口">8. 系统管理接口</a>  <br>
* <a href="./chapter08.md#8.1. 注册区块链[可选，待实现]">8.1. 注册区块链[可选，待实现]</a>  <br>
* <a href="./chapter08.md#8.2. 新增通证">8.2. 新增通证</a>  <br>
* <a href="./chapter08.md#8.3. 添加通证">8.3. 添加通证</a>  <br>

<a href="./chapter09.md">附件1. AccessToken获取简单示例  </a> <br>
<a href="./chapter10.md">附件2. 各公链的使用说明  </a> <br>




## 官方联系方式

### 官方QQ群

![QQ群：594629943](../sp.png)


## 第三方合作伙伴

 - <a href="https://www.jingtum.com/">井通科技</a>,github地址为：https://github.com/swtcpro ，开发者文档地址：http://developer.jingtum.com/  浏览器地址：http://state.jingtum.com

 - <a href="http://www.moac.io/">MOAC</a>,github地址为：ttps://github.com/MOACChain/,开发者文档地址：https://github.com/MOACChain/moac-core/wiki/Commands ,https://github.com/MOACChain/moac-core/wiki/Chain3 ,浏览器地址：http://explorer.moac.io/home
