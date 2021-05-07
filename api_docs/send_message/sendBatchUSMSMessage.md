

# 批量发送短信-SendBatchUSMSMessage

> 支持在一次请求中向多个不同的手机号码发送不同内容的短信；在一次批量请求中，最多支持200个号码；下述各参数仅为参考，详见 [批量发送短信API明细](https://docs.ucloud.cn/api/usms-api/send_batch_usms_message)

# Request Parameters

| Parameter name | Type   | Description                                                  | Required | Remark   |
| -------------- | ------ | ------------------------------------------------------------ | -------- | -------- |
| Action         | String | 对应的 API 名称，SendBatchUSMSMessage                        | Yes      | 公共参数 |
| PublicKey      | String | 对应的 API公钥                                               | Yes      | 公共参数 |
| Signature      | String | 根据API公私钥及API指令生成的用户签名，参见 [签名算法](https://docs.ucloud.cn/api/summary/signature) | Yes      | 公共参数 |
| ProjectId      | string | 项目 ID，主账号与财务账号为空时为 默认项目；子账号为必填字段，参见 [获取 项目ID](https://docs.ucloud.cn/api/summary/get_project_list) | Yes      | 公共参数 |
| TaskContent    | string | 批量发送参数，base64编码后的json数组，编码前后的json数组参考下述示例：<br> [Base64编码前的TaskContent示例](usms/api_docs/send_message/sendBatchUSMSMessage?id=taskcontent示例（base64编码前）)、 [Base64编码后的TaskContent示例](https://docs.ucloud.cn/usms/api_docs/send_message/sendBatchUSMSMessage?id=TaskContent%E7%A4%BA%E4%BE%8B%EF%BC%88Base64%E7%BC%96%E7%A0%81%E5%90%8E%EF%BC%89) | Yes      |          |



- TaskContent（Base64编码前）

| Parameter name | Type   | Description            | Case            | Required |
| -------------- | ------ | ---------------------- | --------------- | -------- |
| TemplateId     | string | 短信模板ID             | UTB20092XXXXD02 | Yes      |
| SigContent     | string | 短信签名               | UCloud          | Yes      |
| Target         | Array  | 号码及短信内容组合列表 |                 | Yes      |



- Target（Base64编码前）

| Parameter name | Type   | Description                                                  | Case               | Required |
| -------------- | ------ | ------------------------------------------------------------ | ------------------ | -------- |
| TemplateParams | Array  | 短信模板中的变量（数组格式）                                 | ["UCloud","13455"] | Yes      |
| Phone          | string | 手机号码，手机号码格式为(60)1xxxxxxxx，()中为国际长途区号(如中国为86或0086，两种格式都支持)，后面为电话号码.若不传入国际区号，如185XXXX0507，则默认为国内手机号 | 185XXXX0507        | Yes      |
| UserId         | string | 自定义的业务标识ID，字符串（ 长度不能超过32 位）             | ucloud-uhost-001   | No       |
| ExtendCode     | string | 短信扩展码，格式为阿拉伯数字串，默认不开通，如需开通请联系 UCloud技术支持 | 123                | No       |



#### TaskContent示例（Base64编码前）

```json
[
    {
        "TemplateId":"UTA20212831C85C",
        "SigContent":"UCloud",
        "Target":[
            {
                "TemplateParams":[
                    "顶级钻石用户刘大锤",
                    "24680"
                ],
                "Phone":"185XXXX0507",
                "UserId":"you man c define the content by yrself"
            },
            {
                "TemplateParams":[
                    "开心果挖土机",
                    "13579"
                ],
                "Phone":"185XXXX0608",
                "ExtendCode":"123",
                "UserId":"catch the big fish"
            }
        ]
    }
]
```



#### TaskContent示例（Base64编码后）

```json
WwogICAgewogICAgICAgICJUZW1wbGF0ZUlkIjoiVVRBMjAyMTI4MzFDODVDIiwKICAgICAgICAiU2lnQ29udGVudCI6IlVDbG91ZCIsCiAgICAgICAgIlRhcmdldCI6WwogICAgICAgICAgICB7CiAgICAgICAgICAgICAgICAiVGVtcGxhdGVQYXJhbXMiOlsKICAgICAgICAgICAgICAgICAgICAi6aG257qn6ZK755+z55So5oi35YiY5aSn6ZSkIiwKICAgICAgICAgICAgICAgICAgICAiMjQ2ODAiCiAgICAgICAgICAgICAgICBdLAogICAgICAgICAgICAgICAgIlBob25lIjoiMTg1WFhYWDA1MDciLAogICAgICAgICAgICAgICAgIlVzZXJJZCI6InlvdSBtYW4gYyBkZWZpbmUgdGhlIGNvbnRlbnQgYnkgeXJzZWxmIgogICAgICAgICAgICB9LAogICAgICAgICAgICB7CiAgICAgICAgICAgICAgICAiVGVtcGxhdGVQYXJhbXMiOlsKICAgICAgICAgICAgICAgICAgICAi5byA5b+D5p6c5oyW5Zyf5py6IiwKICAgICAgICAgICAgICAgICAgICAiMTM1NzkiCiAgICAgICAgICAgICAgICBdLAogICAgICAgICAgICAgICAgIlBob25lIjoiMTg1WFhYWDA2MDgiLAogICAgICAgICAgICAgICAgIkV4dGVuZENvZGUiOiIxMjMiLAogICAgICAgICAgICAgICAgIlVzZXJJZCI6ImNhdGNoIHRoZSBiaWcgZmlzaCIKICAgICAgICAgICAgfQogICAgICAgIF0KICAgIH0KXQ==
```



# Response Elements

| Parameter name | Type   | Description                                                  | Required |
| -------------- | ------ | ------------------------------------------------------------ | -------- |
| RetCode        | int    | 返回码                                                       | **Yes**  |
| Action         | string | 操作名称                                                     | **Yes**  |
| Message        | string | 发生错误时表示错误描述                                       | **Yes**  |
| TaskId         | string | 本次提交发送任务的唯一ID，可根据该值查询本次发送的短信列表。注：成功提交短信数大于0时，才返回该字段 | No       |
| ReqUuid        | string | 本次请求Uuid                                                 | No       |
| SuccessCount   | int    | 成功提交短信（未拆分）条数                                   | No       |
| FailContent    | array  | 未发送成功的详情，返回码非0时该字段有效，可根据该字段数据重发 | No       |

## BatchInfo

| Parameter name | Type   | Description                                             | Required |
| -------------- | ------ | ------------------------------------------------------- | -------- |
| TemplateId     | string | 短信模板ID                                              | **Yes**  |
| SigContent     | string | 短信签名                                                | **Yes**  |
| Target         | array  | 具体手机号码、模板变量等信息组合                        | **Yes**  |
| FailureDetails | string | 未能成功发送的详情。注：模板/签名检验失败时，该字段有效 | No       |

## FailPhoneDetail

| Parameter name | Type   | Description                                       | Required |
| -------------- | ------ | ------------------------------------------------- | -------- |
| TemplateParams | array  | 短信模板参数                                      | **Yes**  |
| Phone          | string | 手机号                                            | **Yes**  |
| ExtendCode     | string | 扩展号码                                          | No       |
| UserId         | string | 用户自定义ID                                      | No       |
| FailureDetails | string | 发送失败原因。注：若模板/签名校验失败，该字段为空 | No       |

# Request Example

```http
https://api.ucloud.cn/?Action=SendBatchUSMSMessage
&PublicKey=vsRhB0Qzo9elXXXXXkw8o/vmss8Tb0vxi74A=
&Signature=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
&ProjectId=org1234
&TaskContent=WwogICAgewogICAgICAgICJUZW1wbGF0ZUlkIjoiVVRBMjAyMTI4MzFDODVDIiwKICAgICAgICAiU2lnQ29udGVudCI6IlVDbG91ZCIsCiAgICAgICAgIlRhcmdldCI6WwogICAgICAgICAgICB7CiAgICAgICAgICAgICAgICAiVGVtcGxhdGVQYXJhbXMiOlsKICAgICAgICAgICAgICAgICAgICAi6aG257qn6ZK755+z55So5oi35YiY5aSn6ZSkIiwKICAgICAgICAgICAgICAgICAgICAiMjQ2ODAiCiAgICAgICAgICAgICAgICBdLAogICAgICAgICAgICAgICAgIlBob25lIjoiMTg1WFhYWDA1MDciLAogICAgICAgICAgICAgICAgIlVzZXJJZCI6InlvdSBtYW4gYyBkZWZpbmUgdGhlIGNvbnRlbnQgYnkgeXJzZWxmIgogICAgICAgICAgICB9LAogICAgICAgICAgICB7CiAgICAgICAgICAgICAgICAiVGVtcGxhdGVQYXJhbXMiOlsKICAgICAgICAgICAgICAgICAgICAi5byA5b+D5p6c5oyW5Zyf5py6IiwKICAgICAgICAgICAgICAgICAgICAiMTM1NzkiCiAgICAgICAgICAgICAgICBdLAogICAgICAgICAgICAgICAgIlBob25lIjoiMTg1WFhYWDA2MDgiLAogICAgICAgICAgICAgICAgIkV4dGVuZENvZGUiOiIxMjMiLAogICAgICAgICAgICAgICAgIlVzZXJJZCI6ImNhdGNoIHRoZSBiaWcgZmlzaCIKICAgICAgICAgICAgfQogICAgICAgIF0KICAgIH0KXQ==
```

# Response Example

```json
{
    "RetCode":0,
    "Action":"SendBatchUSMSMessageResponse",
    "Message":"submit success",
    "TaskId":"abcd-dadd-dafs-dadfa-dafdsa",
    "ReqUuid":"abcd-dadd-dafs-dadfa-dafdsa",
    "SuccessCount":2,
    "FailContent":[
        {
            "TemplateId":"UTA20212831C85C",
            "SigContent":"UCloud",
            "Target":[
                {
                    "TemplateParams":[
                        "开心果挖土机",
                        "13579"
                    ],
                    "Phone":"185XXXX0608",
                    "ExtendCode":"123",
                    "UserId":"catch the big fish"
                }
            ],
            "FailureDetails":"phone in the black list"
        }
    ]
}
```