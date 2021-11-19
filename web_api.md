# Web SDK API

## SDK 初始化

window.JVerificationInterface.init(Object)

### 接口说明

初始化接口。

### 参数说明：

初始化参数 Object 说明:

| 参数名称 | 参数类型 | 参数说明 |
|:-------:|:------:|:-------:|
| appkey | string |极光后台分配的 appkey(必填) |
| debugMode | boolean | 是否打开 debug 模式,默认 false |
| success | function | 接口调用成功的回调函数 |
| fail | function | 接口调用失败的回调函数 |

回调 Object data 说明:

| 参数名称 | 参数类型 | 参数说明 |
|:-------:|:------:|:-------:|
| code | number |返回码，0 代表成功，其他失败，参考错误码 |
| message | string | 结果描述 |

### 调用示例：
	
~~~			
window.JVerificationInterface.init({
    appkey: "极光后台注册的 appkey",
    debugMode: true,
    success: function(data) { 
        //TODO 初始化成功回调
    }, 
    fail: function(data) { 
        //TODO 初始化失败回调
    }
  });
~~~

## 获取 SDK 初始化是否成功标识

window.JVerificationInterface.isInitSuccess()

### 接口说明

获取 SDK 是否整体初始化成功的标识。
SDK 未初始化，正在初始化和初始化失败时均返回 false。

### 返回结果：

boolean : true - 成功，false - 失败

### 调用示例：
	
~~~			
var isSuccess = window.JVerificationInterface.isInitSuccess();
~~~

 
## SDK 判断网络环境是否支持

window.JVerificationInterface.checkVerifyEnable()

### 接口说明

判断当前的设备环境是否可以使用认证。
当前设备环境为移动设备，且网络环境不是 wifi 时才支持。

### 返回结果：

boolean : true - 成功，false - 失败

### 调用示例：
	
~~~			
var verifyEnable = window.JVerificationInterface.checkVerifyEnable();
if(!verifyEnable){
    console.log("当前网络环境不支持认证");
    return;
}
~~~

## SDK 获取号码认证 token

window.JVerificationInterface.getToken(Object)

### 接口说明

获取当前在线的 sim 卡所在运营商及 token。
如果获取成功代表可以用来验证手机号，多次尝试获取失败后建议转短信验证，单运营商默认超时时长为 5000ms。

### 参数说明：

获取 token 参数 Object 说明:

| 参数名称 | 参数类型 | 参数说明 |
|:-------:|:------:|:-------:|
| operater | string | 设置优先尝试获取 token 运营商，CM 代表中国移动，CU 代表中国联通，CT 代表中国电信|
| success | function | 接口调用成功的回调函数 |
| fail | function | 接口调用失败的回调函数 |

回调 Object data 说明:

| 参数名称 | 参数类型 | 参数说明 |
|:-------:|:------:|:-------:|
| code | number |返回码，0 代表成功，其他失败，参考错误码 |
| message | string | 结果描述 |
| operater | string |成功时才有此参数，代表对应运营商，CM 代表中国移动，CU 代表中国联通，CT 代表中国电信 |
| content | string | 成功时为对应运营商 token |

### 调用示例：
	
~~~			
window.JVerificationInterface.getToken({
    operater:"CM"
    success: function(data)  { 
      //TODO 获取token成功回调
      var operater =data.operater;
      var token =data.content;
      
    }, fail: function(data)  { 
      //TODO 获取token失败回调
    } 
    })
~~~

### 其他说明：
移动在获取 token 时会验证网页请求 origin 以及 referer（在申请移动账号时填写的配置），如果移动验证不一致将返回 “500|取号失败”，请在您配置的对应网址中使用获取移动 token 功能。
- origin：网页域名。
- referer：网页来源，通常为当前网址，iOS safari 可能会截取网址，以真实携带的 referer 为准。


## SDK 一键登录

window.JVerificationInterface.loginAuth(Object)

### 接口说明

一键登录接口

### 参数说明：

获取 token 参数 Object 说明:

| 参数名称 | 参数类型 | 参数说明 |
|:-------:|:------:|:-------:|
| operater | string | 设置优先尝试获取 token 运营商，CM 代表中国移动，CU 代表中国联通，CT 代表中国电信|
| type | string | 设置页面登录模式，全屏：full，弹窗：dialog，不填默认全屏|
| success | function | 接口调用成功的回调函数 |
| fail | function | 接口调用失败的回调函数 |

回调 Object data 说明:

| 参数名称 | 参数类型 | 参数说明 |
|:-------:|:------:|:-------:|
| code | number |返回码，0 代表成功，其他失败，参考错误码 |
| message | string | 结果描述 |
| operater | string |成功时才有此参数，代表对应运营商，CM 代表中国移动，CU 代表中国联通，CT 代表中国电信 |
| content | string | 成功时为对应运营商一键登录 token |

### 调用示例：
	
~~~			
window.JVerificationInterface.loginAuth({
    operater:"CM",
    type:"full",
    success: function(data)  { 
      //TODO 一键登录获取 token 成功回调
      var operater =data.operater;
      var token =data.content;
      
    }, fail: function(data)  { 
      //TODO 一键登录获取 token 失败回调
    } 
    })
~~~

### 其他说明：

- 本地仅支持调整联通一键登录页的logo和应用名，其他无法调整。
- 电信和移动为运营商固定样式，如需调整请联系对接商务或技术支持，同运营商申请样式变更，不支持本地调整。

## SDK 一键登录UI设置

window.JVerificationInterface.setCustomUIWithConfig(Object)

### 接口说明

设置一键登录UI接口

### 参数说明：

获取 token 参数 Object 说明:

| 参数名称 | 参数类型 | 参数说明 |
|:-------:|:------:|:-------:|
| logo | string | 设置一键登录logo|
| appName | string | 设置一键登录应用名|


### 调用示例：
	
~~~			
 window.JVerificationInterface.setCustomUIWithConfig({
      logo:"https://opencloud.wostore.cn/h5netauth/h5auth_demo/img/logo3.png",
      appName:"测试应用名称"
    })
~~~

## 错误码

|code	|message	|备注
|------|---------|---|
|0|  success |调用成功	
|1000|  unknown error | 未知错误
|1001|  initing , please try again later | 正在初始化，稍后再试
|1002|  empty appkey	| appkey 为空
|1003|	init failed	| 初始化失败，详情参考控制台打印
|1004|	init timeout	| 初始化超时
|1005|	no internet	| 当前无网络连接
|2001|	please call init correctly first	|SDK 尚未初始化，应先成功调用 init() 方法
|2002|	getToken faild	| 获取 token 失败，此错误对应 content 会携带各运营商错误信息
|2003|	token requesting, please try again later	| 正在获取 token 中，稍后再试
|2004|  not support	| 当前环境不支持获取 token
|2005|  operater has to be one of CM,CT,CU | 获取 token operater 传参错误

当 code 为 2002 时，content 参数说明：

| 参数名称 | 参数类型 | 参数说明 |
|:-------:|:------:|:-------:|
| CM | string | 移动获取 token 失败描述 |
| CU | string | 联通获取 token 失败描述 |
| CT | string | 电信获取 token 失败描述 |
