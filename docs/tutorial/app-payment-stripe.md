### 开通  
### open
- [登录Stripe](https://dashboard.stripe.com/login)注册账号
- [Login to Stripe](https://dashboard.stripe.com/login) to register an account
* 注册账号后可获取开发测试的API密钥（公钥、私钥），注意：需[激活账户](https://dashboard.stripe.com/account/onboarding)获取正式的API密钥
* After registering an account, you can get the API key (public key, private key) for development and testing. Note: you need to [activate the account](https://dashboard.stripe.com/account/onboarding) to obtain the official API key
* 设置[支付方式](https://dashboard.stripe.com/settings/payment_methods)
* Set [Payment Methods](https://dashboard.stripe.com/settings/payment_methods)

更多信息详见[申请开通Stripe操作指南](https://uniapp.dcloud.io/app-payment-stripe-open)
For more information, see [Operation Guide for Applying for Stripe](https://uniapp.dcloud.io/app-payment-stripe-open)

**注意**
**Notice**
- iOS系统仅支持iOS13.0及以上版本
- iOS system only supports iOS13.0 and above

### 配置  
### configuration
在manifest.json文件“App模块配置”项的“Payment(支付)”下，勾选“paypal支付”项并配置相关参数
![](https://native-res.dcloud.net.cn/images/uniapp/payment/stripe_setup_manifest_info.png)

**参数说明**  
**Parameter Description**  
- returnURL  
Android平台使用，格式为"your-app://stripe"(示例 io.dcloud.test://stripe)，'your-app'为应用的bundle id或其它自定义scheme，参考:[配置一个自定义页面内跳转协议 (URL Scheme)](https://ask.dcloud.net.cn/article/64)
Used on the Android platform, the format is "your-app://stripe" (example io.dcloud.test://stripe), 'your-app' is the bundle id of the application or other custom schemes, refer to:[Configure a custom Define the page jump protocol (URL Scheme)](https://ask.dcloud.net.cn/article/64)


### 服务器生成订单
### The server generates the order
在 App 端调用支付前，需在业务服务器生成[PaymentIntent](https://stripe.com/docs/api/payment_intents)，详情可参考Stripe官方文档：[Add an endpoint](https://stripe.com/docs/payments/accept-a-payment?platform=android&ui=payment-sheet#add-server-endpoint)
Before invoking payment on the App side, [PaymentIntent](https://stripe.com/docs/api/payment_intents) needs to be generated on the business server. For details, please refer to the official Stripe document: [Add an endpoint](https://stripe. com/docs/payments/accept-a-payment?platform=android&ui=payment-sheet#add-server-endpoint)

激活账户前可通过POST请求Stripe官方沙盒服务器[https://stripe.com/docs/payments/accept-a-payment](https://stripe.com/docs/payments/accept-a-payment)，生成测试PaymentIntent，示例如下：
Before activating the account, you can request the official Sandbox server of Stripe via POST [https://stripe.com/docs/payments/accept-a-payment](https://stripe.com/docs/payments/accept-a-payment) , generate a test PaymentIntent, the example is as follows:

```  js
uni.request({
    url: 'https://stripe-mobile-payment-sheet.glitch.me/checkout',//仅为示例
    method: "POST", 
    success:(res) => {
        console.log("订单信息" + res.data);
        var publishKey = res.data.publishableKey;
        var paymentIntent = res.data.paymentIntent; 
        var customer = res.data.customer;
        var ephemeralKey = res.data.ephemeralKey;
        var billingDetails = res.data.billingDetails,
    }
});
```


### 应用内发起支付
### Initiate payment within the app

- uni-app项目  
- uni-app project
调用 [uni.requestPayment(OBJECT)](https://uniapp.dcloud.io/api/plugins/payment?id=requestpayment) 发起支付，OBJECT参数中provider属性值固定为`stripe`、orderInfo属性值为订单对象
Call [uni.requestPayment(OBJECT)](https://uniapp.dcloud.io/api/plugins/payment?id=requestpayment) to initiate a payment, the value of the provider attribute in the OBJECT parameter is fixed to `stripe`, and the value of the orderInfo attribute is an order object
- 5+ App项目  
- 5+ App projects
调用 [plus.payment.request(channel, orderInfo, successCB, errorCB)](https://www.html5plus.org/doc/zh_cn/payment.html#plus.payment.request) 发起支付, channel参数为stripe支付对象，orderInfo参数为订单对象
Call [plus.payment.request(channel, orderInfo, successCB, errorCB)](https://www.html5plus.org/doc/zh_cn/payment.html#plus.payment.request) to initiate payment, channel parameter is stripe payment object, the orderInfo parameter is the order object


#### 订单对象参数说明  
#### Order object parameter description
Object对象类型
Object object type

| 属性 | 类型 | 必填 | 说明 |
| Attribute | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| customer | String | 否 | Stripe的[Customer](https://stripe.com/docs/api/customers)对象，如为同一用户执行定期重复性收款，并跟踪多笔收款 |
| customer | String | No | Stripe's [Customer](https://stripe.com/docs/api/customers) object, such as performing regular recurring payments for the same user and tracking multiple payments |
| ephemeralKey | String | 否 | Stripe的Customer Ephemeral Key，用于临时访问Customer |
| ephemeralKey | String | No | Stripe's Customer Ephemeral Key, used for temporary access to Customer |
| isAllowDelay | String | 否 | 是否支持延迟支付,默认不支持(将 isAllowDelay 设置为 true 后可使用一些较慢的支付方式，例如 SEPA 借记和 Sofort 对于这些支付方式，只有当 PaymentSheet 完成后才能知道最终的付款状态是成功还是失败。如果您允许这样，则通知客户您已确认他们的订单，但收到付款后才能履行（例如，发货）订单。) |
| isAllowDelay | String | No| Whether to support delayed payment, not supported by default (set isAllowDelay to true to use some slower payment methods, such as SEPA debit and Sofort For these payment methods, the final payment can only be known after the PaymentSheet is completed The status of the payment is successful or failed. If you allow this, the customer is notified that you have confirmed their order, but the order cannot be fulfilled (eg, shipped) until payment is received.) |
| merchantName | String | 是 | 商户名称 |
| merchantName | String | yes | merchant name |
| paymentIntent | String | 是 | Stripe的[PaymentIntent](https://stripe.com/docs/api/payment_intents)对象，对应服务器生成的支付订单 |
| paymentIntent | String | Yes | Stripe's [PaymentIntent](https://stripe.com/docs/api/payment_intents) object, corresponding to the payment order generated by the server |
| publishKey | String | 是 | 公钥，在Stripe注册账号后可获取 |
| publishKey | String | Yes | Public key, which can be obtained after registering an account with Stripe |
| billingDetails | Object | 否 | 银行卡账单信息(包含姓名、手机号码、邮箱地址、账单地址等)|
| billingDetails | Object | No | Bank card billing information (including name, mobile phone number, email address, billing address, etc.)|

> 注意：customer与ephemeralKey必须成对出现，只传其一无效
> Note: customer and ephemeralKey must appear in pairs, only one of them is invalid


#### 示例代码  
#### Sample code
- uni-app项目  
- uni-app project
``` js
//订单对象
//order object
var orderInfo = {
    "customer": "Stripe的Customer",                    //Customer
    "ephemeralKey": "Stripe的Customer Ephemeral Key",  //临时访问Customer的Key
    "isAllowDelay": true,                              //是否支持延迟支付  默认false
    "merchantName": "DCloud",                          //商户名
    "paymentIntent": "Stripe的PaymentIntent",          //订单信息
    "publishKey": "Public Key",                        //公钥
    "billingDetails":{         //账单信息(可选)
        "name":"",
        "email":"",
        "phone":"",
        "address":{
            "city":"",
            "country":"CN",//国家代码(ISO 3166-1 alpha-2)
            "line1":"",
            "line2":"",
            "postalCode":"",
            "state":""
        }
    }                      
};
// 从Stripe测试服务器获取订单数据
// Get order data from Stripe test server
uni.request({
    url: 'https://stripe-mobile-payment-sheet.glitch.me/checkout',
    method: "POST",
    success: (res) => {
        orderInfo = {
            "customer": res.data.customer,
            "ephemeralKey": res.data.ephemeralKey,
            "isAllowDelay": true,
            "merchantName": "DCloud",
            "paymentIntent": res.data.paymentIntent,
            "publishKey": res.data.publishableKey,
            "billingDetails": res.data.billingDetails
        };
    }
});
//...
//发起支付
//Initiate payment
uni.getProvider({
    service: 'payment',
    success: function(res) {
        if (~res.provider.indexOf('stripe')) {
            uni.requestPayment({
                "provider": "stripe",
                "orderInfo": orderInfo,
                success(res) {
                    console.log("requestPayment Success: "+JSON.stringify(res));
                },
                fail(e) {
                    console.log("requestPayment failed: "+JSON.stringify(e));
                }
            });
        }
    }
});
```  

- 5+ App项目  
- 5+ App projects
``` js
//订单对象，从服务器获取
//Order object, obtained from the server
var orderInfo = {
    "customer": "Stripe的Customer",                    //Customer
    "ephemeralKey": "Stripe的Customer Ephemeral Key",  //临时访问Customer的Key
    "isAllowDelay": true,                              //是否支持延迟支付  默认false
    "merchantName": "DCloud",                          //商户名
    "paymentIntent": "Stripe的PaymentIntent",          //订单信息
    "publishKey": "Public Key",                        //公钥
    "billingDetails":{         //账单信息(可选)
        "name":"",
        "email":"",
        "phone":"",
        "address":{
            "city":"",
            "country":"CN",//国家代码(ISO 3166-1 alpha-2)
            "line1":"",
            "line2":"",
            "postalCode":"",
            "state":""
        }
    }
};
//获取支付渠道
//Get the payment channel
var stripeSev = null;
plus.payment.getChannels(function(channels){
    for (var i in channels) {
        var channel = channels[i];
        if (channel.id === 'stripe') {
            stripeSev = channel;
        }
    }
    //发起支付
    //Initiate payment
    plus.payment.request(stripeSev, orderInfo, function(result) {
         var rawdata = JSON.parse(result.rawdata);
         console.log("支付成功");
    }, function(e) {
         console.log("支付失败：" + JSON.stringify(e));
    });
  }, function(e){
      console.log("获取支付渠道失败：" + JSON.stringify(e));
});
```

