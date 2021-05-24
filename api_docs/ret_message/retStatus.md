# 状态报告推送

通过HTTP批量推送的方式将短信回执状态报告推送至客户指定地址。



## 协议说明

| 类别 | 说明                                         |
| ---- | -------------------------------------------- |
| URL  | 用户配置的HTTP回调地址（当前需用户主动提供） |
| 方式 | POST                                         |
| 协议 | HTTP + JSON                                  |
| 编码 | UTF-8                                        |



## 请求说明

请求为 JSON Array 格式，单次请求可能会包含多个短信回执状态报告内容。

### 请求示例

```json
{
  "MsgType": 2,
  "Data": [
    {
      "SessionNo": "d0****f7-0fc3-****-****-9f73****6c6e",
      "Phone": "185****9057",
      "CostCount": 2,
      "ReceiptTime": 1563867000,
      "ReceiptResult": "发送成功",
      "ReceiptCode": "Delivrd",
      "ReceiptDesc": "用户接收成功",
      "UserId": "you man c define the content by yrself"  
    },
    {
      "SessionNo": "d1****f7-0fc3-****-****-9f73****6c6e",
      "Phone": "185****9057",
      "CostCount": 2,
      "ReceiptTime": 1563867000,
      "ReceiptResult": "发送失败",
      "ReceiptCode": "MSBLACK",
      "ReceiptDesc": "手机在运营商防骚扰黑名单",
      "UserId": "you man c define the content by yrself"  
    } ]
}
```



### 参数说明

| Parameter name | Type  | Description                      | Case | Required |
| -------------- | ----- | -------------------------------- | ---- | -------- |
| MsgType        | int   | 推送消息类型，2代表 回执状态报告 | 2    | Y        |
| Data           | Array | 批次列表                         |      | Y        |

- Data

| Parameter name | Type   | Description                                                  | Case             | Required |
| -------------- | ------ | ------------------------------------------------------------ | ---------------- | -------- |
| SessionNo      | string | [短信发送](https://docs.ucloud.cn/api/usms-api/send_usms_message) 的发送序列号 | xddd-xx-ss-ss-ss | Y        |
| Phone          | string | 手机号码                                                     | 18512345678      | Y        |
| CostCount      | int    | 短信拆分条数                                                 | 2                | Y        |
| ReceiptTime    | int    | 状态报告时间                                                 | 1563867000       | Y        |
| ReceiptResult  | string | 发送状态                                                     | 发送成功         | Y        |
| ReceiptCode    | string | 状态报告编码                                                 | Delivrd          | Y        |
| ReceiptDesc    | string | 状态报告说明                                                 | 用户接收成功     | Y        |
| UserId         | string | 自定义的业务标识ID，字符串（ 长度不能超过32 位），不支持 单引号、表情包符号等特殊字符 | ucloud-uhost-001 | N        |



## 响应说明

### 响应示例

```
{
    code: 0,
    message: "ok"
}
```



### 参数说明

| code | message  | Description |
| ---- | -------- | ----------- |
| 0    | ok       | 接收成功    |
| 非0  | 异常说明 | 未接收成功  |



## 重推说明

首次推送失败后（非成功响应），将每隔1秒进行重推，累计重推3次仍未成功，将停止推送。

