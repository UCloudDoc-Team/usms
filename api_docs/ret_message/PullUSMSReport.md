# 拉取状态报告-PullUSMSReport

> 拉取短信发送状态报告



# 接口说明

此接口默认不开通，如需开通使用请联系技术支持申请开通；

此接口服务开通后，我们会将您账号下最新上报的状态报告单独保留72小时，期间您可通过此接口分批拉取状态报告；数据拉取成功后，平台将删除原始数据，请您及时保管及存储拉取的数据！



# 请求参数

| Parameter name | Type   | Description                                                  | Required | Remark   |
| -------------- | ------ | ------------------------------------------------------------ | -------- | -------- |
| Action         | String | 对应的 API 名称，PullUSMSReport                              | Yes      | 公共参数 |
| PublicKey      | String | 对应的 API公钥                                               | Yes      | 公共参数 |
| Signature      | String | 根据API公私钥及API指令生成的用户签名，参见 [签名算法](https://docs.{{domainName}}/api/summary/signature) | Yes      | 公共参数 |
| ProjectId      | string | 项目 ID，主账号与财务账号为空时为 默认项目；子账号为必填字段，参见 [获取 项目ID](https://docs.{{domainName}}/api/summary/get_project_list) | Yes      | 公共参数 |
| Limit          | int    | 单次拉取条数，默认100，最大200；                             | Yes      |          |



# 响应参数

| Parameter name | Type   | Description                                          |
| -------------- | ------ | ---------------------------------------------------- |
| RetCode        | int    | 返回状态码，为 0 则为成功返回，非 0 为失败           |
| Action         | string | 操作指令名称                                         |
| Message        | string | 返回错误消息，当 `RetCode` 非 0 时提供详细的描述信息 |
| ReqUuid        | string | 返回请求uuid                                         |
| ReportSet      | array  | 本次拉取的状态报告集合                               |



## ReportSet

| Parameter name | Type   | Description                                                  |
| -------------- | ------ | ------------------------------------------------------------ |
| SessionNo      | string | [短信发送](https://docs.{{domainName}}/api/usms-api/send_usms_message) 的发送序列号 |
| Phone          | string | 手机号码                                                     |
| CostCount      | int    | 短信拆分条数                                                 |
| ReceiptTime    | int    | 状态报告时间                                                 |
| ReceiptResult  | string | 回执状态结果，可根据该字段判断发送结果，枚举值：<br>> 发送成功 或 Success：代表短消息发送成功<br>> 发送失败 或 Fail：代表短消息发送失败<br>> 状态未知 或 Unknow：代表运营商未上报状态报告 |
| ReceiptCode    | string | 状态回执码                                                   |
| ReceiptDesc    | string | 状态回执描述                                                 |
| UserId         | string | 客户下发短信时自定义的业务标识ID                             |



# 示例(调用成功)

## 请求示例

```http
{{apiURL}}/?Action=PullUSMSReport
&PublicKey=vsRhB0Qzo***********************i74A=
&Signature=xxxxxxxxxxxxxxxxxxxxxxxxxxxx
&ProjectId=org***34
&Limit=100
```



## 返回示例

```json
{
    "RetCode":0,
    "Action":"PullUSMSReportResponse",
    "Message":"pull success",
    "ReqUuid":"abcd-da*********a-dafdsa",
    "ReportSet": [
      {
        "SessionNo": "d0*************6c6e",
        "Phone": "185****9057",
        "CostCount": 2,
        "ReceiptTime": 1563867000,
        "ReceiptResult": "发送成功",    //通过该字段判断发送结果，枚举值见参数说明
        "ReceiptCode": "0",
        "ReceiptDesc": "用户接收成功",
        "UserId": "ky*****pcm"  
      },
      {
        "SessionNo": "d1****************6c6e",
        "Phone": "135****5924",
        "CostCount": 2,
        "ReceiptTime": 1563867000,
        "ReceiptResult": "发送失败",
        "ReceiptCode": "MSBLACK",
        "ReceiptDesc": "手机在运营商防骚扰黑名单",
        "UserId": "ky*****pcm"  
      } 
    ]
}

```

*注：由于存在网络超时、客户拉取状态报告服务异常等因素，使用此接口可能会造成状态报告丢失情况；*

