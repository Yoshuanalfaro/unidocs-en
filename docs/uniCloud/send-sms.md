## 发送短信

<!--
/// meta
keyword: 短信,sms
-->

> 自`HBuilderX 3.3.0`起，本接口支持传入phoneList参数批量发送短信，其他参数均于发送单条短信相同

> 自`HBuilderX 3.4.0`起云函数需启用扩展库uni-cloud-sms之后才可以调用sendSms接口，详细说明见：[云函数使用短信扩展库](#extension)

自HBuilderX 2.8.1起，uniCloud内置了短信发送API。给开发者提供更方便、更便宜的短信发送能力。

该服务类似小程序的模板消息，在一个固定模板格式的文字里自定义某些字段，而不是所有文字都可以随便写。

使用本功能需要在[DCloud开发者中心](https://dev.dcloud.net.cn/pages/sms/base)开通并充值，教程参考[短信服务开通指南](https://ask.dcloud.net.cn/article/37534)

因涉及费用，为保障安全，本能力应该在云函数中调用，而不是在前端调用。

云函数API名称：`uniCloud.sendSms`

**参数说明**

参数结构体为json格式。

|参数名			|类型		|必填							|说明																																											|
|:-:				|:-:		|:-:							|:-:																																											|
|appid			|String	|是								|DCloud appid，可以在项目manifest.json内看到																							|
|smsKey			|String	|是								|调用短信接口的密钥key，从 dev.dcloud.net.cn/uniSms 后台获取															|
|smsSecret	|String	|是								|调用短信接口的密钥secret，从 dev.dcloud.net.cn/uniSms 后台获取														|
|phone			|String	|和phoneList二选一|发送目标手机号，暂仅支持中国大陆手机号																										|
|phoneList	|Array	|和phone二选一		|发送目标手机号，暂仅支持中国大陆手机号，最多50个手机号码，`HBuilderX 3.3.0`起支持				|
|templateId	|String	|是								|模版Id，短信内容为固定模板，详见下方说明（应用开发阶段，可以使用 DCloud 提供的测试模板）	|
|data				|Object	|是								|模版里的各个变量字段，json格式																														|


**注意**

- 如果使用uni-id发送短信，无需自行开发，请参考[uni-id-pages](uni-id-pages.md)

#### 云函数使用短信扩展库@extension

自HBuilderX 3.4.0起，短信相关功能移至扩展库`uni-cloud-sms`内。在一段时间内无论开发者是否使用扩展库云函数都可以正常使用`uniCloud.sendSms`。HBuilderX 3.4.0及之后的版本上传云函数时如果没有指定使用`uni-cloud-sms`扩展库的云函数将无法调用uniCloud.sendSms接口。

关于扩展库的说明见：[云函数扩展库](cf-functions.md#extension)

在云函数的package.json内添加`uni-cloud-sms`的引用即可为云函数启用此扩展，无需做其他调整，完整的package.json示例如下：

```js
{
	"name": "uni-sms",
	"extensions": {
		"uni-cloud-sms": {} // 启用短信扩展，值为空对象即可
	}
}
```

#### 参数templateId说明@smstemplate

按照国家法律和运营商要求，每个要发送短信的应用，需要备案其短信模板，并且经过运营商的审核。通过审核的模板，会得到一个templateId。

短信内容规范：
1. 不能包含涉政、黄赌毒、暴力、房产、移民、贷款、代开发票等违法内容
2. 不能包含运营商禁止发送的内容
3. 不能包含侵犯第三方权益的内容（如侵犯他人商标或冒名行为）
4. 营销类短信不能违反广告法
5. 不能利用短信骚扰或诈骗用户

报备模板的方式：

1. 如果尚未添加签名，请在在开发者中心-[签名配置](https://dev.dcloud.net.cn/pages/sms/sign)内添加签名
2. 在开发者中心-[模板配置](https://dev.dcloud.net.cn/pages/sms/template)内申请自定义模板

- 短信签名：
即短信内容开头的【xxx】，可选内容为App或小程序名称、网站名称、企业名称（可使用简称，但需具备辨识度）、商标名称。如`【DCloud】`，即是DCloud官方发送短信的签名。签名的作用是明确告知用户该短信由什么样的主体发送。签名内容只允许包含中文、英文、数字，签名的长度限制为2-8位。

- 模板内容：
短信模板必然以短信签名作为开头，其内容中允许有一定的变量，以满足灵活性需求。变量用${}包裹。

例如：【hello uni-app】验证码：${code}，${expMinute}分钟内有效，请勿泄露并尽快验证。

在实际发送短信时，在短信API中传入该模板ID，然后传入合适的变量，最终发送的短信将变为：
`【hello uni-app】验证码：123465，用于注册，15分钟内有效，请勿泄露并尽快验证。`

- 短信类别：
分为3类，即验证码类短信、通知类短信、营销类短信。验证码类短信，其模板审核简单快速，只能单次发送。

**短信测试模板说明**

运营商目前审核比较严格，处于开发阶段的应用可能无法通过运营商的审核。为方便开发者测试短信功能，DCloud 提供了一个测试模板，该模板的templateId为：uni_sms_test，内容为：`【统一应用软件】尊敬的用户，您的验证码是：${code}。5分钟内有效，请尽快验证。请勿泄漏您的验证码。` 

使用该模板的限制：

1. 每日最多给10个手机号发送不超过100条短信；
2. 使用该模板也会正常收取费用，请保证账户有充足余额。


**返回值**

接口调用失败时会直接抛出错误，调用成功时才会有返回值。

注意接口调用成功不代表短信发送成功，比如目标手机关机会导致短信发送失败。真实的短信发送成功与否请在[https://dev.dcloud.net.cn/pages/sms/base](https://dev.dcloud.net.cn/pages/sms/base)后台查看报表。

|参数名	|类型	|说明			|
|:-:	|:-:	|:-:			|
|errCode|Number|成功返回0，调用失败错误码见下表	|
|errMsg|String|错误描述，调用失败时返回	|

**错误码说明**

|错误码	|错误																	|
|:-:		|:-:																	|
|1001		|参数校验未通过,errMsg内会给出详细信息|
|4000		|参数错误															|
|4001		|apiKey 不存在 或 templateId 不正确		|
|4002		|请检查smsKey、smsSecret是否有误			|
|4003		|服务空间或IP地址不在白名单中					|
|5000		|服务错误，请联系DCloud进行排查				|
|5001		|服务器异常，请重试！									|

**调用示例**

```js
// 发送单条短信示例
'use strict';
exports.main = async (event, context) => {
  try {
    const res = await uniCloud.sendSms({
      appid: '__UNI__xxxxxxx',
      smsKey: '****************',
      smsSecret: '****************',
      phone: '188********',
      templateId: '100**', // 请替换为自己申请的模板id
      data: {
        name: 'DCloud',
        code: '123456',
        expMinute: '3',
      }
    })
    // 调用成功，请注意这时不代表发送成功
    return res
  } catch(err) {
    // 调用失败
    console.log(err.errCode)
    console.log(err.errMsg)
    return {
      code: err.errCode,
      msg: err.errMsg
    }
  }
};

// 批量发送短信示例
'use strict';
exports.main = async (event, context) => {
  try {
    const res = await uniCloud.sendSms({
      appid: '__UNI__xxxxxxx',
      smsKey: '****************',
      smsSecret: '****************',
      phoneList: ['188********', '138********'],
      templateId: '100**', // 请替换为自己申请的模板id
      data: {
        name: 'DCloud',
        code: '123456',
        expMinute: '3',
      }
    })
    // 调用成功，请注意这时不代表发送成功
    return res
  } catch(err) {
    // 调用失败
    console.log(err.errCode)
    console.log(err.errMsg)
    return {
      code: err.errCode,
      msg: err.errMsg
    }
  }
};
```

本示例使用的模板为：
```
【uniID】“${name}”验证码：${code}，${expMinute}分钟内有效，请勿泄露并尽快验证。
```

本示例发送的短信，在手机上将显示为：
```
【uniID】“DCloud”验证码：123456，3分钟内有效，请勿泄露并尽快验证。
```


### 发送失败注意@fail

- data内如果有`测试`、`test`等字样，系统可能会被判定为测试用途，不会真正把短信下发到对应手机（此行为由运营商控制，可能真实发送，也可能不发送） 
- 短信内容不可包含★、 ※、 →、 ●等特殊符号，可能会导致短信乱码
- 如果本地运行提示`不支持的模板ID`，请更新到`2.9.9+`版本的HBuilderX 
- 使用同一短信模板给同一个手机号发送短信时，频率不能太高。如果1分钟内超过1次，会被运营商判定为骚扰或短信重发而被拦截，导致短信发送失败
- 尽量使用企业实名认证，个人实名认证的审核更严格，更容易发送失败


**其他注意事项**

- 在[DCloud开发者中心](https://dev.dcloud.net.cn/pages/sms/base)绑定`uniCloud`服务空间后，将会只允许绑定的服务空间调用此接口，绑定列表为空时表示不限制服务空间
- 如果是用于用户注册的短信验证码，那么强烈推荐使用uni-id，这是一套云端一体的、完善的用户管理方案，已经内置封装好的短信验证码功能，详见：[uni-id-pages](uni-id-pages.md)。
- 发送短信前，如果需要图形验证码来防止机刷，可以使用[uni-captcha图形验证码](https://ext.dcloud.net.cn/plugin?id=4048)。在[uni-id-pages](uni-id-pages.md)模板中已经集成了uni-id、uni-captcha
- Android手机在App端获取短信验证码，参考：[https://ask.dcloud.net.cn/article/676](https://ask.dcloud.net.cn/article/676)
- 短信内容超过70个字符时为长短信，需分条发送，每67个字按一条短信计算
- App平台的短信验证码需求，建议优先通过App一键登陆来替代，更便捷、更便宜。[详见](univerify.md)

更多问题：欢迎加入<a class="join-group-chat" target="_blank" href="https://web-assets.dcloud.net.cn/unidoc/zh/Dcloud-%E7%9F%AD%E4%BF%A1.png">DCloud短信技术交流群	<img src="https://web-assets.dcloud.net.cn/unidoc/zh/Dcloud-%E7%9F%AD%E4%BF%A1.png">
</a>咨询


### 短信费用说明@sms-fee

- 短信费用为：0.036元/条。

但在实际使用中需要依赖`uniCloud`云服务。如使用uniCloud阿里云商业版，每条大约需要多花0.0000139元，几乎可以忽略不计。您也可以粗略认为每条短信的费用为0.0360139元/条。费用计算规则如下：


`短信`业务涉及费用的部分主要是云函数/云对象的使用量、调用次数、和出网流量(如：使用`uni-id-co`或自定义的云函数/云对象来发送短信)。
接下来，我们对不同资源，分别进行费用评估。

我们按照uniCloud官网列出的[按量计费](https://uniapp.dcloud.net.cn/uniCloud/price.html#aliyun-postpay)规则，可以简单得出如下公式：

`云函数/云对象费用 = 资源使用量 * 0.000110592  + 调用次数 * 0.0133 / 10000 + 出网流量 * 0.8`

其中：
- 资源使用量 = 云函数内存（单位为G） * 云函数平均单次执行时长（单位为秒） * 调用次数
- 调用次数 = 发送短信条数（一般情况下发送条数 = 调用次数，特殊情况除外）


我们假设如下数据模型：

- 云函数内存：512M，即0.5G （云函数内存默认为512M，用户可以自定义设置，最低可设置为128M。如果您仅发送短信，没有其他复杂业务，那么内存设为128M可以进一步的降低费用）
- 云函数平均单次执行时长：200毫秒，即0.2秒
- 短信业务平均每日调用次数：10000次
- 出网流量：单次请求 2 KB

按照如上公式，其`短信`业务云函数每天的费用为：

```
云函数费用（天） = 资源使用量 * 0.000110592  + 调用次数 * 0.0133 / 10000 + 出网流量 * 0.8
			  = 云函数内存（单位为G） * 云函数平均单次执行时长（单位为秒） * 调用次数 + 调用次数 * 0.0133 / 10000 + 出网流量 * 0.8
			  = 0.5G * 0.2S * 10000 * 0.000110592 + 10000 * 0.0133/10000 + 10000 * 2 * 0.8 / (1024 * 1024) 
			  = 0.110592 + 0.0133 + 0.0152587890625
			  = 0.1391507890625（元）
			  ≈ 0.139（元）
```

结论：如果你的`短信`业务平均每天发送条数为10000条，使用阿里云正式版云服务空间后，对应云函数每天大概消耗0.139元，对比之前的短信费用，平均每次调用多花0.0000139元，几乎可忽略不计。


- 计费条数计算方法：短信内容少于70个字符（每个汉字、标点、空格、字母均算一个字符）算作1条短信，短信内容多于70个字符时，每67个字符算作一条短信，并向上取整（不足67个字符的部分也算做1条）。 例： 短信内容有 100个字符时计费短信条数应为 100 / 67 ≈ 1.49 向上取整后算作2条。
- 最终按照成功回执状态为"成功"的短信条数计费，成功回执状态可在"发送记录"页面查看。

特别注意：短信成功回执最长延迟为72小时。

## 营销短信群发@batch-sms
如有客户关怀、会员服务、电商活动、新品上线等场景需要给用户发送短信时，不再需要开发，在uni-admin控制台选择用户/标签即可向用户群发短信，省时高效。
同时支持动态替换短信模板变量，使短信更加个性化。

**步骤一：开通短信服务**

如您首次使用请登录[DCloud开发者中心](https://dev.dcloud.net.cn/)开通短信服务

**步骤二：添加签名与模板**

在[签名配置页面](https://dev.dcloud.net.cn/pages/sms/sign)添加短信签名

在[模板配置页面](https://dev.dcloud.net.cn/pages/sms/template)中添加短信模板

例如：`【测试】亲爱的${username}, 祝您生日快乐！感谢您长期以来对xx商城的信任与支持，会员生日月畅享购物双倍积分，期待您的光临！`

**步骤三：导出短信模板**

在短信模板页面-点击”导出模板“按钮，导出短信模板。
![导出短信模板](https://web-assets.dcloud.net.cn/unidoc/zh/20230107203307.png)

**步骤四：通过uni-admin控制台发送短信**

如您未部署过uni-admin，请在插件市场中安装[uni-admin](https://ext.dcloud.net.cn/plugin?id=3268)

首次使用，请在`uni-config-center/uni-sms-co/config.json`中配置短信`smsKey`与`smsSecret`，具体配置方式参考[uni-admin群发短信文档](uniCloud/admin.md#batch-sms)

配置完成后，登录uni-admin控制台，打开用户管理页面，请按照图示步骤上传短信模板（步骤三导出的短信模板）：
![上传短信模板](https://web-assets.dcloud.net.cn/unidoc/zh/20230107201145.png)
短信模板上传成功后，短信模板即可显示，如下：
![短信模板上传成功](https://web-assets.dcloud.net.cn/unidoc/zh/20230107202329.png)

选择要接收短信的用户，如下：
![群发用户](https://web-assets.dcloud.net.cn/unidoc/zh/20230107202752.png)
或者如果已经对用户进行了分组，可以在标签管理中选择标签后发送短信，如下：
![群发用户标签](https://web-assets.dcloud.net.cn/unidoc/zh/20230107203019.png)

目前短信支持固定文本发送与关联数据表字段发送，以下介绍两种方式如何发送

**固定文本发送**

选择短信模板，如果没有出现变量模板配置就是固定文本模式，如下：
![](https://web-assets.dcloud.net.cn/unidoc/zh/20230107204518.png)
可以在发送前点击预览，可以预览发送的第一条短信，用来检查短信内容是否正确，如下：
![](https://web-assets.dcloud.net.cn/unidoc/zh/20230107204807.png)
确认短信内容无误后，点击提交即可发送短信，发送短信之后可以在[DCloud开发者中心](https://dev.dcloud.net.cn/)-查看[短信发送记录](https://dev.dcloud.net.cn/pages/sms/sendLog)

**使用数据表字段作为模板变量发送**

选择短信模板，如果出现变量模板配置就是数据表查询模式，如下：
![](https://web-assets.dcloud.net.cn/unidoc/zh/20230107205208.png)
如上，短信变量字段为”username“，配置替换字段为uni-id-users表中username字段，在发送短信时会替换掉短信变量。

短信变量支持固定值和数据表查询两种方式；固定值如：各位同事，数据表查询如：{uni-id-users.username}；请注意，若使用数据表查询方式，目前仅支持查询 uni-id-users 表；并注意确保数据库中查询字段值不为空，否则短信将发送失败。

在发送之前可以点击预览，查看第一条短信的内容，确保变量模板配置正确，如下，username将替换为“张三”：
![](https://web-assets.dcloud.net.cn/unidoc/zh/20230107205823.png)

确认短信内容无误后，点击提交即可发送短信，发送短信之后可以在[DCloud开发者中心](https://dev.dcloud.net.cn/)-查看[短信发送记录](https://dev.dcloud.net.cn/pages/sms/sendLog)
![](https://web-assets.dcloud.net.cn/unidoc/zh/20230107210406.png)

如有任何问题可在[论坛发帖](https://ask.dcloud.net.cn)咨询或加uniCloud短信服务交流QQ群(695645208)咨询


<style>
	.join-group-chat{
		position: relative;
	}
	.join-group-chat img{
		display: none;
	}
	.join-group-chat:hover img{
		position: absolute;
                background: #FFF;
		top: 25px;
		right: 0;
		display: block;
		width: 150px;
		height: 150px;
		box-shadow:#999 0px 0px 20px;
		padding: 3px;
	}
</style>


