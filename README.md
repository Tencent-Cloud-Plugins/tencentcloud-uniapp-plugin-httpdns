# 腾讯云移动解析（HTTPDNS）插件

## 1. 插件介绍
| 标题      | 名称    |
| ----     | ---------------- |
| 中文名称   | 腾讯云移动解析（HTTPDNS）插件 |
| 英文名称   | tencentcloud-plugin-httpdns |
| 最新版本   | v1.0.0 (2020.11.17) |
| 适用平台   | [DCloud uni-app](https://uniapp.dcloud.net.cn) |
| 适用产品   | [腾讯云移动解析（HTTPDNS）](https://cloud.tencent.com/product/httpdns) |
| GitHub项目| [tencentcloud-uniapp-plugin-httpdns](https://github.com/Tencent-Cloud-Plugins/tencentcloud-uniapp-plugin-httpdns) |
| 主创团队   | 腾讯云中小企业产品中心（SMB Product Center of Tencent Cloud） |
| 兼容平台   | H5、小程序、APP |

一款帮助开发者在uni-app项目开发中快捷使用腾讯云移动解析（HTTPDNS）产品功能的插件。

## 2. 功能特性

- 移动解析功能

## 3. 安装指引

本插件需要调用uniCloud云函数，而使用云函数的前提是：

- 使用DCloud官方开发工具HBuilderX 2.7+；
- 已注册DCloud开发者账号并通过实名认证；
- 开通了uniCloud并创建一个腾讯云的服务空间；

### 3.1. 新建或打开已有项目

1. 打开HBuilderX开发工具；
1. 新建或打开一个uni-app项目；

### 3.2. 导入云函数

1. 访问 DCloud 插件市场的 [腾讯云插件 - 云函数模板](https://ext.dcloud.net.cn/plugin?id=2139) 详情页；
2. 点击详情页右上角 **使用 HBuilderX 导入插件**，将云函数模板导入到您的项目中；
![](./images/guide/guide-1.png)
3. 在项目中打开 _cloudfunctions/tencentcloud-plugin/config.js_ 文件，将腾讯云的密钥信息配置进去，可以在腾讯云 [API 密钥管理](https://console.cloud.tencent.com/cam/capi) 中获取 SecretId、SecretKey 和 APPID；
![](./images/guide/guide-2.png)
4. 在[uniCloud控制台](https://unicloud.dcloud.net.cn/login)注册HBuild账号并登录，创建[云服务空间](https://uniapp.dcloud.net.cn/uniCloud/concepts/space)；
5. 如果想使用企业版API接入，在项目中打开 _cloudfunctions/tencentcloud-plugin/httpdns/config.js 文件，将HTTPDNS企业版本的授权id和密钥配置进去，可以在腾讯云 [控制台](https://console.cloud.tencent.com/httpdns) 中开通HTTPDNS服务,开通后会得到授权id和密钥；
![](./images/guide/guide-3.png)
6. 绑定云函数的云服务空间，将[云函数](https://uniapp.dcloud.net.cn/uniCloud/concepts/cloudfunction) [**上传部署**](https://uniapp.dcloud.net.cn/uniCloud/quickstart?id=rundebug) 到您的[云服务空间](https://uniapp.dcloud.net.cn/uniCloud/concepts/space)；
![](./images/guide/guide-4.png)

> 如果您之前在使用其它腾讯云产品的 uni-app 插件时已经导入过此云函数模板，则前 4 个步骤可以省略。

> 若导入失败或有其它疑问，请查看 [uniCloud帮助文档](https://uniapp.dcloud.io/uniCloud/README) 云函数相关章节。

### 3.3. 导入插件

1. 访问DCloud插件市场 [腾讯云移动解析（HTTPDNS）插件](https://ext.dcloud.net.cn/plugin?id=3451) 详情页；
2. 点击详情页右上角 **使用HBuilderX导入插件** ，将插件导入到您的项目中；
3. 在项目中通过 import 语法将插件提供的方法导入到相关业务组件并使用；

> 本插件的默认导入位置是在您项目的“js_sdk”目录下

## 4. 使用指引

### 4.1. 插件API导图

![](./images/httpdns-guide.png)

### 4.2. 插件API列表

| API名称          | API对应方法名 |
| ---------------- | ------------- |
| 获取移动解析结果 | describeDnsResult |

### 4.3. 插件使用示例

```javascript
// 移动解析使用示例
// 从js_sdk列表中导入需要的api
import {
  describeDnsResult
} from "@/js_sdk/tencentcloud-plugin-httpdns";

export default {
  data() {
    return {
      domainName: 'www.baidu.com', // 域名
    };
  },
  methods: {
    // 开始DNS解析
    async startResolution() {
      const params = {
        domainName: this.domainName，
        isEnc: true
      }
      const result = await describeDnsResult(params);
    }
  }
};
```

### 4.4 主要API 说明

#### startResolution(domainName, ip, ttl, clientip, id) ⇒ <code>Promise.&lt;string&gt;</code>
**Returns**: <code>Promise.&lt;string&gt;</code> - result 移动解析结果

| Param          | Type | Required |  Description |
| ---------------- | ------------- | ---- | ---- |
| domainName | <code>string</code> | <code>true</code> | 待解析的域名 |
| ip | <code>string</code> | <code>false</code> |   用户ip，不传则默认为HTTP报文的源IP |
| ttl | <code>number</code> | <code>false</code> |   是否返回递归服务器缓存时间, 1:返回 |
| clientip | <code>number</code> | <code>false</code> | 是否返回用户公网出口IP  1:返回 |
| isEnc | <code>boolean</code> |  <code>true</code> |  是否加密 true(调用企业版API): 加密 false:不加密(调用免费版API) |

### 4.5. 名词解释

服务空间：一个服务空间对应一整套独立的云开发资源，包括数据库、存储空间、云函数等资源。服务空间之间彼此隔离。更多详情请访问 [uniCloud开发文档](https://uniapp.dcloud.io/uniCloud/concepts/space)

云函数：云函数是运行在云端的JavaScript代码，更多详情请见 [uniCloud云函数文档](https://uniapp.dcloud.io/uniCloud/cf-functions)

## 5. 获取入口

| 插件入口       | 链接                                                                      |
| -------------- | ------------------------------------------------------------------------- |
| DCloud插件市场 | [腾讯云移动解析（HTTPDNS）插件](https://ext.dcloud.net.cn/plugin?id=3451) |

## 6. FAQ
> 暂无


## 7. GitHub版本迭代记录

### 7.1. tencentcloud-uniapp-plugin-httpdns v1.0.0

- 移动解析功能
  
## 8. 联系我们

&nbsp;&nbsp;&nbsp;扫码备注“云插件”来联络到我们</br>
![](./images/qrcode.png)
