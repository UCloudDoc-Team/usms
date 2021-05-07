# 上行消息推送

通过HTTP批量推送的方式将上行消息推送至客户指定地址。



## 协议说明

| 类别 | 说明                                         |
| ---- | -------------------------------------------- |
| URL  | 用户配置的HTTP回调地址（当前需用户主动提供） |
| 方式 | POST                                         |
| 协议 | HTTP + JSON                                  |
| 编码 | UTF-8                                        |



## 请求说明

请求为 JSON Array 格式，单次请求可能会包含多个上行消息内容。

### 请求示例

```json
{
  MsgType: 0, 
  Data: [ 
    {
      ExtendCode: "12345",  
      UserId: "you man c define the content by yrself",     
      Phone: "185****9057",     
      ReplyContent: "好的，可以了",  
      ReplyTime: 1573552778       
    },
    {
      ExtendCode: "12346",
      UserId: "you man c define the content by yrself",  
      Phone: "185****9057",
      ReplyContent: "收到，谢谢",
      ReplyTime: 1573552778
    }
  ]
}
```



### 参数说明

| Parameter name | Type  | Description                 | Case | Required |
| -------------- | ----- | --------------------------- | ---- | -------- |
| MsgType        | int   | 推送消息类型，0代表上行消息 | 0    | Y        |
| Data           | Array | 批次列表                    |      | Y        |

- Data

| Parameter name | Type   | Description                                      | Case             | Required |
| -------------- | ------ | ------------------------------------------------ | ---------------- | -------- |
| ExtendCode     | string | 扩展码，默认不带                                 | 12345            | N        |
| UserId         | string | 自定义的业务标识ID，字符串（ 长度不能超过32 位） | ucloud-uhost-001 | N        |
| Phone          | string | 手机号码                                         | 18512345678      | Y        |
| ReplyContent   | string | 上行（回复）消息                                 | 好的，收到了     | Y        |
| ReplyTime      | int    | 回复时间                                         | 1563867000       | Y        |



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