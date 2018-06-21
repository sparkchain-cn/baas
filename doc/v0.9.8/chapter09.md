
---
- 附1：AccessToken获取简单示例  

```
public class SparkChainBaasUtils {
	public static String accessToken = "";
	public static String accessUrl = "https://tapi.sparkchain.cn";
	// todo:可以配置到配置文件中，然后通过其它方式获取到
	public static String chainAppId = "";
	public static String chainSecret = "";
	// 简单示例
	private String createWallet(String openId) throws IOException {
		String url = accessUrl + "/v1/app/createWallet";
		Map<String, String> params = new HashMap<>();
		params.put("userId", openId);
		params.put("password", "123456");

		Map<String, ?> map = invokeBaas(url, params);
		return (String) getDataValue(map, "walletAddr");
	}

	/**
	 * 调用火花链接入平台的统一调用方法，实现简单的accessToken的获取
	 * 
	 * @param url            api的地址
	 * @param params           调用的参数
	 * @return
	 */
	public static Map<String, ?> invokeBaas(String url, Map<String, String> params) throws IOException {
		preGetToken(params);
		Map<String, ?> map = doExec(url, params);
		// 5001说明是accessToken失败，需要重新获取accessToken，放到查询参数中
		if (containAndEq(map, "code", "5001")) {
			// 重新获取的accessToken
			String token = reTryGetToken(params);
			if (StringUtils.isNotNullOrEmpty(token)) {
				map = (Map<String, Object>) doExec(url, params);
			} else {
				// TODO:需要系统自行进行异常处理
			}
		}
		return map;
	}

	private static String getAccessTokenFromSystem() throws IOException {
		String url = accessUrl + "/v1/app/access";
		Map<String, String> params = new HashMap<>();
		// chainAppId和chainSecret是静态变量
		params.put("appid", chainAppId);
		params.put("appsecret", chainSecret);

		String result = HttpUtils.post(url, params);
		Map<String, Object> map = JSON.parseObject(result, Map.class);
		return (String) getDataValue(map, "accessToken");

	}

	private static String preGetToken(Map<String, String> params) throws IOException {
		if (accessToken == null || "".equals(accessToken.trim())) {
			accessToken = getAccessTokenFromSystem();
		}
		params.put("accessToken", accessToken);
		return accessToken;
	}

	private static String reTryGetToken(Map<String, String> params) throws IOException {
		String token = getAccessTokenFromSystem();
		if (StringUtils.isNullOrEmpty(token)) {
			// TODO:可以重试，可以抛出异常，进行相关处理
			return null;
		} else {
			accessToken = token;
			params.put("accessToken", accessToken);
			return accessToken;
		}
	}

	private static Map<String, ?> doExec(String url, Map<String, String> params) throws IOException {
		String result = HttpUtils.post(url, params);
		Map<String, Object> map = JSON.parseObject(result, Map.class);
		return map;
	}
	private static Object getDataValue(Map<String, ?> map, String dataKey) {
	if (map == null || map.get("data") == null) {	return null;}
		Map<String, ?> data = (Map<String, ?>) map.get("data");
		return data.get(dataKey);
	}

	public static boolean containAndEq(Map map, String key, Object value) {
		if (map == null) {		return false;	}
		if (!map.containsKey(key)) {	return false;	}
		if (value instanceof String) {return value.equals(map.get(key));}
		if (map.get(key) == value) {	return true;	}
		return false;
	}
}
```



## 官方联系方式

### 官方QQ群

![查看页面](../sp.png)

### 官方技术交流论坛
  欢迎大家到<a href="http://sparkda.com/">斯巴达论坛</a>进行提问及交流 

### 官方技术BAAS平台
  欢迎大家到<a href="http://baas.sparkchain.cn/">火花链BaaS平台</a>发现更多好玩的Dapp（目前正开发中）


## 第三方合作伙伴

 - <a href="https://www.jingtum.com/">井通科技</a>,github地址为：https://github.com/swtcpro ，开发者文档地址：http://developer.jingtum.com/  浏览器地址：http://state.jingtum.com

 - <a href="http://www.moac.io/">MOAC</a>,github地址为：ttps://github.com/MOACChain/,开发者文档地址：https://github.com/MOACChain/moac-core/wiki/Commands ,https://github.com/MOACChain/moac-core/wiki/Chain3 ,浏览器地址：http://explorer.moac.io/home

 - 南昌技术开发团队,github地址为:https://github.com/moacDapp/ ,QQ群：

 ![查看页面](../nc.png)

