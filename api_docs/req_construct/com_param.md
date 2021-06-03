# 公共参数

公共参数是用于标识用户和接口签名的参数。

`为避免重复，下列公共参数不会再在各API文档中进行重复说明，但每次请求均需携带这些参数，否则无法正常发起请求`。

| 参数名    | 必选  | 参数类型 | 说明                                                         |
| :---------     | :-----        | :--------         | :------------------------------------------------------------          |
| Action    | true  | String   | 对应的 API 名称，如 SendUSMSMessage                          |
| PublicKey | true  | String   | 对应的 API公钥                                               |
| Signature | true  | String   | 根据API公私钥及API指令生成的用户签名，参见 [签名算法](https://docs.ucloud.cn/api/summary/signature)          |
| ProjectId | false | String   | 项目 ID，主账号与财务账号为空时为默认项目；子账号为必填字段，参见 [获取 项目ID](https://docs.ucloud.cn/api/summary/get_project_list)       |

