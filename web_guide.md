# 极光认证 Web SDK 集成指南

## 使用提示

本文是 JVerification Web SDK 标准的集成指南文档。

+ 如果您想要快速地测试、请参考本文在几分钟内跑通 Demo。
+ 极光推送文档网站上，有相关的所有指南、API、教程等全部的文档。包括本文档的更新版本，都会及时地发布到该网站上。

## 产品说明

极光认证整合了三大运营商的网关认证能力，为开发者提供了号码认证功能，优化用户注册/登录、号码验证体验，提高安全性。

### 主要场景：

	1.js号码认证
    2.js一键登录

### JVerification-web-example.zip 集成压缩包内容

+ example
	+ 是一个 web 页面，通过这个演示了 JVerification SDK 的基本用法，可以用来做参考。


## 创建应用

### 创建极光开发者帐号

请访问[极光官方网站](https://www.jiguang.cn/accounts/register) 注册您的极光账号。

![20200630111800.png](https://img.jiguang.cn//jver/hbuilder/plugin20200630111800.png)

### Portal上创建应用

使用注册账号登陆，进入极光控制台后，点击“创建应用”按钮，进入创建应用的界面。填上你的应用程序的名称就可以了，最后点击最下方的 “创建我的应用”按钮，创建应用完毕。

![20200630112141.png](https://img.jiguang.cn//jver/hbuilder/plugin20200630112141.png)

### 查看应用信息

创建应用之后返回用户主页面可以看到应用清单，点选你刚才创建的应用来查看应用信息。

![20200630112317.png](https://img.jiguang.cn//jver/hbuilder/plugin20200630112317.png)


## SDK 接入

每个页面接入下面 js

- 1. v1.0.0 - 动态嵌入meta标签
```
<script type="text/javascript" src="https://jverification.jiguang.cn/scripts/1.0.0/jverification-web.min.js"></script>
```
- 2. 需要手动添加meta标签
```
<script type="text/javascript" src="https://jverification.jiguang.cn/scripts/jverification-web.min.js"></script>
```

引入该 JS 后，就可以使用 Window 上的全局对象 JVerificationInterface。

### 额外js引入

- since v2.0.0

```
  <!-- 如需支持联通一键登录，请单独引入 h5auth1.min.js-->
  <script type="text/javascript"src="https://opencloud.wostore.cn/h5netauth/h5login/singleton/h5auth1.min.js"></script>
	
   <!-- 移动一键登录必须接入 crypto-js-->
  <script type="text/javascript" src="./crypto-js.js"></script>
```


## SDK 初始化

```
window.JVerificationInterface.init({
    appkey: "", // 极光官网中创建应用后分配的 appkey，必填
    debugMode: true, // 设置是否开启 debug 模式。true 则会打印更多的日志信息。设置 false 则只会输出 w、e 级别的日志。
    success: function(data) { 
        //TODO 初始化成功回调
    }, 
    fail: function(data) { 
        //TODO 初始化失败回调
    }
  });
```


### 更多 API

其他 API 的使用方法请参考接口文档：[Web SDK API](./web_api)

### 运行 demo

压缩包附带的 example 是一个 API 演示例子。你可以直接在浏览器运行测试。


## 技术支持

邮件联系：[support&#64;jiguang.cn](mailto:support&#64;jiguang.cn)
