## 概述
## Overview

1. uniCloud为每个开发者提供一个免费的服务空间，更低门槛
2. 按量付费是serverless的特色，如果没有消耗硬件资源，就完全不用付款
3. serverless具有比传统的云主机更便宜
4. 传统云主机一旦被攻击，高防价格非常昂贵。而uniCloud无需支付高防费用，不惧DDoS攻击。

uniCloud的定价、套餐内容、服务SLA，是由云厂商直接公布的。DCloud公司不会加价。uniCloud已经上线近3年，DCloud一直以良心方式服务开发者，努力降低应用的开发门槛、提高应用的开发效率。
- 选择阿里云作为服务商时，有一个免费服务空间。更多服务空间需要付费。
- 选择腾讯云作为服务商时，需付费购买套餐，超出套餐后可开启按量计费，套餐详情参考[腾讯云基础套餐](uniCloud/price?id=tencent-package)。

付费用户享受阿里云和腾讯云提供的服务协议SLA，[详见](https://uniapp.dcloud.net.cn/uniCloud/agreement)

uniCloud提供包月、按量计费两种计费方式，具体说明如下：

|计费方式	|付费方式					|计费单位																									|
|:-:		|:-:						|:-:																										|
|包月		|预付费						|参考 [腾讯云包月套餐](uniCloud/price?id=price-month)、[阿里云包月套餐](uniCloud/price?id=aliyun-package)	|
|按量计费	|结算时冻结费用，每日结算	|参考 [阿里云按量计费](uniCloud/price?id=aliyun-postpay)													|


## 阿里云@aliyun
## Aliyun@aliyun

阿里云分公测版和正式版。正式版于2022年11月21日上线，同时公测版停止新建。
对现存的公测版服务空间，阿里云会提供**两个月的过渡期**，在此期间已创建的服务空间仍可继续使用，开发者需在2023年1月21日前完成迁移。
同时uniCloud控制台已增加公测版迁移正式版的功能以便开发者平滑迁移。

相关公告见：[https://ask.dcloud.net.cn/article/40144](https://ask.dcloud.net.cn/article/40144)

### 阿里云正式版@aliyun-business

阿里云正式版支持`包年包月`及`按量计费`两种计费模式，创建`按量计费`服务空间需先充值保证金及阿里云余额。

目前单个账号可创建20个正式版服务空间，更多额度我们会协调阿里云做调整提高。

**注意:**阿里云正式版版需要使用HBuilderX 3.6.5（正式版）或3.6.10（alpha版）或与此版本对应的uni-app cli项目才可正常使用。如果是cli创建的项目，可以通过执行`npx @dcloudio/uvm alpha`升级依赖

#### 免费额度
阿里云针对每个账号提供了一个有免费额度的服务空间，以方便产品开发测试及体验。具体额度请阅读下方[包年包月套餐](uniCloud/price.md?id=aliyun-package)中的开发者版。

**免费额度注意事项：**
- 单个账号只能创建一个阿里云免费服务空间
- 阿里云免费服务空间有效期默认一个月，到期时需主动续费（到期前15天可续费，续费时依旧免费），否则将会被停服释放
- 免费版如需升配，只能针对剩余有效期进行操作，无法自定义升配时间
- 免费版可以转换为按量计费
- 免费版升配或转为按量计费后，免费额度会释放，此时仍可再创建一个免费版

#### 包年包月套餐@aliyun-package
|资源分类			|资源细项								|开发者版（免费版）	|基础版	|标准版	|专业版	|企业版	|旗舰版	|
|:-:					|:-:										|:-:								|:-:		|:-:		|:-:		|:-:		|:-:		|
|云函数				|资源使用量（GBs/月）		|1000								|1万		|20万		|40万		|150万	|400万	|
|							|调用次数（万次/月）		|1.5								|15			|300		|600		|2400		|6000		|
|							|出网流量（GB/月）			|1									|1			|20			|40			|160		|500		|
|云数据库			|容量（GB）							|2									|2			|3			|5			|10			|10			|
|							|读操作数（万次/天）		|0.05								|5			|25			|50			|150		|500		|
|							|写操作数（万次/天）		|0.03								|3			|15			|30			|100		|300		|
|							|集合数量		|100								|100			|100			|100			|100		|100		|
|							|索引数量		|400								|400			|400			|400			|400		|400		|
|云存储				|容量（GB）							|5									|8			|10			|50			|100		|500		|
|							|下载操作次数（万次/月）|0.2								|10			|200		|750		|1500		|3750		|
|							|上传操作次数（万次/月）|0.1								|5			|100		|300		|600		|1500		|
|							|CDN流量（GB/月）				|1									|2			|10			|50			|150		|500		|
|前端网页托管	|容量（GB）							|5									|8			|10			|50			|100		|500		|
|							|CDN流量（GB/月）				|1									|2			|10			|50			|150		|500		|
|售价（元/月）|-											|免费								|5			|24			|82			|316		|688		|

套餐在有效期内可随时进行续费、升配，到期后只可续费，暂不支持降配。

如果你难以预估会消耗多少云资源，推荐使用下方的按量计费。很多情况下套餐模式被用于固定预算，业务量变大也不增加预算。按量计费有充足的弹性。

**关于计费项的额外说明**

- 数据库单次写入操作每1KB数据计算一次写操作数，向上取整
- 数据库单次读取操作每4KB数据计算一次读操作数，向上取整
- updateAndReturn操作只计算写次数，不计算读次数
- 云函数出网流量包含请求三方服务器发送的数据和返回给客户端的数据
- clientDB底层也是基于云函数实现，也会消耗云函数调用次数

#### 按量计费@aliyun-postpay

按量计费，意味着不是每个月支付固定套餐，而是根据使用量付费。

按量付费需要预存一定金额（余额），每日根据前一日资源消耗生成账单，从阿里云预存余额中扣除。

如果预存余额不足，则服务空间将不可用，需要立即充值。

阿里云按量计费服务空间定价如下：

|资源分类			|资源细项								|售价（元）		|
|:-:			|:-:								|:-:				|
|云函数			|资源使用量（GBs）						|0.000110592		|
|				|调用次数（万次）						|0.0133				|
|				|出网流量（GB）						|0.8				|
|云数据库			|容量（GB/天）						|0.07				|
|				|读操作数（万次）						|0.015				|
|				|写操作数（万次）						|0.05				|
|云存储			|容量（GB/天）						|0.0043				|
|				|下载操作次数（万次）					|0.01				|
|				|上传操作次数（万次）					|0.01				|
|				|CDN 流量（GB）						|0.18				|
|前端网站托管		|容量（GB/天）						|0.0043				|
|				|流量（GB）							|0.18				|

**注意**
- 按量计费是延迟结算，可能存在前一日消耗大于余额导致超支的情况。故创建按量付费服务空间时，需支付一定的**保证金**，用以抵消超支结算的情况。如果您不再使用uniCloud服务，可以申请退还保证金（目前需要发送邮件到service@dcloud.io）。

#### 现阶段系统限制@aliyun-system-limit

|资源分类	|限制项											|限额	|
|---			|---												|---	|
|云函数		|callFunction请求QPS				|1000	|
|					|url化请求QPS（自定义域名）	|1000	|
|					|url化请求QPS（默认域名）		|100	|
|					|固定IP代理请求QPS					|20		|
|					|最大实例数									|300	|
|					|函数数量限制								|50		|
|数据库		|QPS												|1000	|
|					|并发执行数									|100	|
|					|单次请求超时时间						|5秒	|
|							|集合数量		|100								|
|							|索引数量		|400								|
|云存储		|上传QPS										|300	|
|					|删除QPS										|300	|
|					|查询QPS										|300	|

#### 其他说明

**云存储数据处理**

图片裁剪、视频截帧等功能。在阿里云正式版初期，此功能仍免费提供给用户使用。后续数据处理功能可能会收费。

**违规图片检测**

正式版不再自动进行云存储违规检测，请开发者自行保证云存储文件合规。

**前端网页托管**

正式版不再自动根据文件修改刷新缓存，提供手动刷新缓存功能。

#### 欠费停服及资源销毁

包月套餐到期时开始停服，按量计费空间账户欠费时开始停服。服务空间资源在停服后保留15天。15天内可以充正、续费，15天后会销毁空间资源。

### 阿里云公测版@aliyun-public

阿里云公测版已经停止创建新服务空间，并将于2023年1月22日下线。本章节文档仅适用于老用户。

阿里云公测版的服务空间是纯免费的。但为避免资源滥用，有一些限制，见下。

|资源类目					|限制												|说明																																															|
|:-:						|:-:												|:-:																																															|
|云函数并发限制				|1000个实例/服务空间								|实际普通项目很难达到这个并发数，阿里云可以设置单实例多并发单实例最多100，理论最大并发量1000*100=100000 (10万)，关于单实例多并发请参考：[单实例多并发](uniCloud/cf-functions.md?id=concurrency)	|
|每个服务空间的云函数数量	|48个												|实际项目中由于clientDB和单路由云函数，只会用到几个云函数，达不到限制数字。[详见](https://uniapp.dcloud.net.cn/uniCloud/faq?id=merge-functions)													|
|云函数定时触发最小间隔		|1小时												|-																																																|
|云存储容量					|10GB												|-																																																|
|云数据库容量				|100GB												|-																																																|
|单次数据库执行时长限制		|5秒												|**不可申请调整**																																												|
|闲置停服时间										|30天无活跃服务空间会进行停服，在未销毁前可以恢复																																				|
|停服销毁时间										|自动销毁后15天后销毁服务空间，在未销毁前可以恢复																																				|

阿里云公测版不允许开发者使用这些免费的存储及CDN资源来开展图床类业务。正式版无此限制。

## 腾讯云@tencent
## Tencent Cloud @tencent

**使用腾讯云Nodejs12版本时，务必仔细阅读此文档：[keepRunningAfterReturn](uniCloud/cf-functions.md?id=keep-running)**
**Be sure to read this document carefully when using Tencent Cloud Nodejs12 version: [keepRunningAfterReturn](uniCloud/cf-functions.md?id=keep-running)**

腾讯云于2022年8月12日更新了计费方式。
新计费模式下，统一采用**基础套餐+按量计费**的模式，开发者可先购买带有一定配额的基础套餐，超出套餐配额部分按使用量付费。
Under the new billing model, the model of **basic package + pay-as-you-go** is uniformly adopted. Developers can purchase a basic package with a certain quota first, and the portion exceeding the quota of the package will be charged according to the usage.

### 基础套餐@tencent-package
### Basic Package @tencent-package

| 配额						| 个人版						| 入门版| 初创版	| 商用版	| 团队版	| 单位	|
| ---							| ---								| ---		| ---			| ---			|  ---		| ---		|
| QPS							| 500								| 500		| 500			| 800			| 1000		| -			|
| 调用次数				| 20								| 500		| 1000		| 2000		| 5000		| 万次	|
| 容量						| 2									| 30		| 100			| 200			| 300			| GB		|
| 云函数资源使用量| 10								| 30		| 45			| 60			| 100			| 万GBs	|
| 云函数出网流量| 2									| 8			| 10			| 15			| 25			| GB		|
| 云函数数量限制	| 150								| 150		| 150			| 150			| 150			| 个		|
| CDN流量					| 5									| 80		| 200			| 400			| 600			| GB		|
| CDN回源流量			| 5									| 40		| 100			| 200			| 300			| GB		|
| 价格						| **~~39.9~~ 19.9**	| **99**| **299**	| **499**	| **999**	| 元/月	|

1. 个人版5折折扣至少延续至2022年底，后续折扣如有变化将另行通知。
1. The 50% discount on the personal edition will be extended to at least the end of 2022, and further notices will be notified if the subsequent discount changes.
2. **调用次数**：包含云存储上传、下载操作；数据库读、写操作；云函数调用次数。
2. **Number of calls**: including cloud storage upload and download operations; database read and write operations; cloud function calls.
3. **容量**：包含云存储、数据库容量。
3. **Capacity**: Including cloud storage and database capacity.
4. **CDN流量**、**CDN回源流量**：仅包含云存储，不含前端网页托管
4. **CDN traffic**, **CDN back-to-source traffic**: only includes cloud storage, excluding front-end web hosting
5. 开通基础套餐时可以选择是否允许超量，开启后如果用量超出套餐配额将按照按量付费定价进行收费
6. 套餐在有效期内可进行续费、升配，到期当天可降配，到期后只可续费
7. 前端网页托管开通后即为按量计费，不管服务空间有没有开启允许超量使用，前端网页托管计费参考[高级功能按量计费](#tencent-advanced)

**关于计费项的额外说明**

- 数据库单次写入操作每1KB数据计算一次写操作数，向上取整
- 数据库单次读取操作每4KB数据计算一次读操作数，向上取整
- updateAndReturn操作只计算写次数，不计算读次数
- 云函数出网流量包含请求三方服务器发送的数据和返回给客户端的数据
- clientDB底层也是基于云函数实现，也会消耗云函数调用次数

### 按量付费/超量使用定价@tencent-postpay
### Pay-As-You-Go/Overage Pricing @tencent-postpay

| 计费项			| 定价				|
| ---				| ---				|
| 调用次数			| 0.5元/万次		|
| 容量				| 0.1元/GB/天		|
| 云函数资源使用量	| 0.00011108元/GBs	|
| 云函数外网出流量	| 0.8元/GB			|
| CDN流量			| 0.21元/GB			|
| CDN回源流量		| 0.15元/GB			|


### 高级功能按量计费定价@tencent-advanced
### Premium Features Pay-As-You-Go Pricing @tencent-advanced

以下条目的消耗不属于套餐内资源，会从账号的腾讯云余额进行扣除。

| 计费项		|计费项			|定价				|
| ---			| ---			|---				|
|前端网页托管	|容量			|0.005元/GB/天		|
|				|流量			|0.21元/GB			|
|日志服务		|标准索引存储	|0.0115元/GB/日		|
|				|标准日志存储	|0.0115元/GB/日		|
|				|标准索引流量	|0.35元/GB/日		|
|				|写流量			|0.18元/GB/日		|
|				|请求次数		|0.15元/百万次/日	|
|				|分区数量		|0.04元/个/日		|

- 在正式进行计费方式切换之日起，用户将不可继续续费或新购旧版套餐或按量计费服务空间。用户可选择是否切换新的计费方式，超时（2022.09.08）切换的服务空间将会停服释放。
- 新计费下腾讯云云函数日志保存时长为7天

**注：当包年包月服务空间升级新套餐时，如果已开通前端网页托管，则前端网页托管会自动转为按量计费，请确保账号余额充足！**
**Note: When the annual and monthly service space is upgraded to a new package, if the front-end web hosting has been activated, the front-end web hosting will be automatically converted to metered billing, please ensure that the account balance is sufficient! **

### 欠费停服及资源销毁

套餐到期时开始停服。服务空间资源保留7天。7天内可以充正、续费，7天后会销毁空间资源。

## 余额及保证金@balance

腾讯云余额可用于服务空间`按量计费`产生的费用扣款，如服务空间套餐资源用尽后`超限按量`、前端网页托管等服务产生的费用。

阿里云正式版服务空间没有`超限按量`功能，但是提供了`按量计费`的服务空间，阿里云余额适用于`按量计费`服务空间产生的费用扣款。

余额单次充值不低于10元，充值后不支持退款，**余额不支持购买腾讯云及阿里云包年包月套餐，请根据业务使用量合理选择充值金额**。

腾讯云购买基础套餐后，如果开启了`超限按量`功能；或开通了阿里云`按量计费`服务空间；在超出套餐资源用量后，每日的资源用量会在第二天按照按量计费结算并从余额中扣除。

由于存在上一日消耗大于余额导致超支的情况，使用按量计费服务需要缴纳保证金。

账户保证金在停止使用按量计费服务后可以申请退还，所以账户保证金不能申请开具发票。若需退还保证金，需满足以下条件：
1. 阿里云未开通`按量计费`服务空间
2. 腾讯云未开启`超限按量`功能且未开通`前端网页托管`

由于腾讯云包年包月前端网页托管已下线，新开通的前端网页托管均为按量计费，如果开通了上面两项功能，请先关闭，然后发邮件到 service@dcloud.io 申请退还。

## 发生故障时如何判断故障点
## How to judge the fault point when a fault occurs

当你的线上系统故障时，可以参考此文档判断责任归属：[如何判断是DCloud或阿里云或腾讯云的问题](https://uniapp.dcloud.io/uniCloud/faq?id=fault)
When your online system fails, you can refer to this document to determine the attribution of responsibility: [How to determine if it is a DCloud or Alibaba Cloud or Tencent Cloud problem](https://uniapp.dcloud.io/uniCloud/faq?id=fault)

## 云厂商之间的迁移@cross-provider
## Migration between cloud providers @cross-provider

### 数据库迁移@cross-provider-db
### Database Migration @cross-provider-db

目前可以使用云数据库的导入导出进行迁移，迁移数据库之前可以使用导出db_init.json功能将所有集合及索引导出。再使用数据导入导出功能进行迁移。导入导出请参考：[数据导入导出和备份](uniCloud/hellodb.md?id=dbmigration)
Currently, you can use the import and export of ApsaraDB for migration. Before migrating the database, you can use the export db_init.json function to export all collections and indexes. Then use the data import and export function to migrate. For import and export, please refer to: [Data import, export and backup](uniCloud/hellodb.md?id=dbmigration)

> 也可以直接使用第三方封装好的插件：[unicloud数据库一键搬家工具，支持阿里云与腾讯云互转。支持跨账号转。](https://ext.dcloud.net.cn/plugin?id=6089)
> You can also directly use third-party packaged plug-ins: [unicloud database one-click moving tool, which supports the mutual transfer between Alibaba Cloud and Tencent Cloud. Support cross-account transfer. ](https://ext.dcloud.net.cn/plugin?id=6089)

#### 腾讯云迁移到阿里云@tencent-to-aliyun-db
#### Tencent Cloud to Aliyun @tencent-to-aliyun-db

迁移数据可以通过在腾讯云服务空间导出数据表为json文件，在阿里云服务空间导入json文件到表的方式进行迁移。
Migrating data can be migrated by exporting the data table as a json file in the Tencent cloud service space and importing the json file into the table in the Alibaba cloud service space.

#### 阿里云迁移到腾讯云@aliyun-to-tencent-db
#### Aliyun migrated to Tencent Cloud @aliyun-to-tencent-db

由于此前腾讯云并未完全支持ObjectId类型的数据，在阿里云迁移到腾讯云时需要注意处理一下`ObjectId`类型的数据，包括自动生成的_id字段以及关联到其他表的_id的字段。简单来说就是将导出的数据内的ObjectId类型的数据处理成字符串且不满足ObjectId的格式。
Since Tencent Cloud does not fully support ObjectId type data before, you need to pay attention to handling `ObjectId` type data when Alibaba Cloud migrates to Tencent Cloud, including the automatically generated _id field and the _id field associated with other tables. To put it simply, the data of type ObjectId in the exported data is processed into a string that does not meet the format of ObjectId.

例：
example:

```js
// 原始数据
// Raw data
{"_id":{"$oid":"60fa6d25cd84d60001ec38a2"},"uid":{"$oid":"60fa6d1d2e5faa0001ade857"}}

// 调整后的数据
// adjusted data
{"_id":"60fa6d25cd84d60001ec38a2a","uid":"60fa6d1d2e5faa0001ade857a"} // 在结尾追加了一个“a”使其不满足ObjectId格式
```

以下为一个简单的脚本示例用于处理导出的json文件
The following is a simple script example for processing the exported json file

如果将此文件存储为`parse.js`，使用`node parse.js 输入文件相对或绝对路径 输出文件相对或绝对路径`即可处理导出的json文件
If you store this file as `parse.js`, use `node parse.js input file relative or absolute path output file relative or absolute path` to process the exported json file

```js
const fs = require('fs')
const path = require('path')
const readline = require('readline')

const cwd = process.cwd()
const inputPath = path.resolve(cwd, process.argv[2])
const outputPath = path.resolve(cwd, process.argv[3])

if (fs.existsSync(outputPath)) {
  throw new Error(`输出路径（${outputPath}）已存在`)
}

function getType(val) {
  return Object.prototype.toString.call(val).slice(8, -1).toLowerCase()
}
function parseRecord(obj) {
  const type = getType(obj)
  switch (type) {
    case 'object':
      if (obj.$oid) {
        return obj.$oid + 'a'
      }
      const keys = Object.keys(obj)
      for (let i = 0; i < keys.length; i++) {
        const key = keys[i];
        obj[key] = parseRecord(obj[key])
      }
      return obj
    case 'array':
      for (let i = 0; i < obj.length; i++) {
        obj[i] = parseRecord(obj[i])
      }
      return obj
    default:
      return obj
  }
}

async function parseCollection() {
  const inputStream = fs.createReadStream(inputPath)
  const outputStream = fs.createWriteStream(outputPath)

  const rl = readline.createInterface({
    input: inputStream
  });

  for await (const line of rl) {
    const recordStr = line.trim()
    if (!recordStr) {
      continue
    }
    const record = parseRecord(JSON.parse(recordStr))
    outputStream.write(JSON.stringify(record) + '\n')
  }
  rl.close()
  console.log(`处理后的文件已输出到${outputPath}`)
}

parseCollection()

```

#### 使用一键迁移功能迁移阿里云公测版到正式版@aliyun-beta-to-aliyun-biz

阿里云提供了公测版一键迁移到正式版的功能。执行一键迁移后云存储、云函数、数据库都会被迁移到新服务空间。迁移过程中云函数、数据库均可正常访问，云存储无法写入（删除或上传文件）,
详见：[阿里云公测版迁移正式版](uniCloud/aliyun-migrate-business.md)
