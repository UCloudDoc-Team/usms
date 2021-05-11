# API错误码

> 调用 USMS短信服务 API接口失败时，会返回对应接口错误码。

常见接口错误码、错误提示和处理方案，可参考下述：

| **错误码**   | **错误提示及说明**                         | **处理措施**                                                 |
| ------------ | ------------------------------------------ | ------------------------------------------------------------ |
| 18001        | 请求参数有缺失                             | 检查请求参数是否有缺失                                       |
| 18000、18002 | 请求参数格式有误或请求JSON解析错误         | 检查请求参数格式是否有误                                     |
| 18003        | 请求参数无效                               | 检查请求参数是否有问题                                       |
| 18004、18007 | API或服务异常                              | 联系[技术支持](https://www.ucloud.cn/site/service.html)      |
| 18013        | 当前账号/项目中的短信剩余量不足            | 先检查账号是否有短信余量，若不足，需[重新购买](https://console.ucloud.cn/usms?package_type=0&purpose=1&buy_amount=10)；若有余量，则联系联系[技术支持](https://www.ucloud.cn/site/service.html)处理 |
| 18014        | 提交的部分手机号码无效                     | 剔除无效手机号码                                             |
| 18016        | 当前账号/项目未申请短信签名                | 需先申请短信签名                                             |
| 18017        | 当前短信模板不存在或未通过审核             | 需先申请短信模板 或 联系[技术支持](https://www.ucloud.cn/site/service.html)加速审核进度 |
| 18018        | 短信模板参数与短信模板不匹配               | 检查模板参数是否有误 或 是否与模板匹配                       |
| 18019        | 单次提交的手机号码超过1000个拦截发送       | 单次提交的手机号码数需在1000内                               |
| 18023        | 短信内容中含有禁发的敏感词                 | 修改短信内容（一般是短信模板中的变量传值有敏感词）           |
| 18033        | 变量内容不符合规范                         | 检查模板变量传值是否有误，规范可参考 [短信变量](https://docs.ucloud.cn/usms/introduction/2005/2105) |
| 151          | 网关缓存服务异常                           | API网关服务异常，联系[技术支持](https://www.ucloud.cn/site/service.html)处理 |
| 160          | 缺少关键参数Action                         | 检查参数是否完整                                             |
| 161          | Action 不存在                              | 检查参数是否完整                                             |
| 170          | 缺失API签名                                | 请确认API请求是否漏填API签名信息，可参考[API调用说明](https://docs.ucloud.cn/api/summary/README) |
| 171          | API签名错误                                | 检查API签名是否有误，可参考[API调用说明](https://docs.ucloud.cn/api/summary/signature) |
| 172          | 账号不存在This account does not exist      | 确认账号信息是否有误                                         |
| 173          | 账户限制Account restriction                | 账号受限，可联系[技术支持](https://www.ucloud.cn/site/service.html) 了解详情 |
| 174          | Token 不存在                               | 检查参数是否完整                                             |
| 180          | 缺少关键参数API version                    | 检查参数是否完整                                             |
| 200          | API公共服务不可用                          | 可联系[技术支持](https://www.ucloud.cn/site/service.html) 处理 |
| 290          | 项目未授权                                 | 项目未授权，需联系您的主账号管理员将项目授权给您账号         |
| 291          | 该账户没有执行对应 Action 和产品类型的权限 | 账号权限不足，需联系您的主账号管理员授权                     |
| 292          | 项目不存在                                 | 检查项目信息是否填写有误                                     |
| 294          | 访问 IP 被拒绝                             | 客户端 IP不在API白名单中，可在[API秘钥管理](https://console.ucloud.cn/uapi/apikey) 进行配置 |



## 2）短信状态回执错误码

短信发送状态回执错误码可通过调用 [获取短信发送回执信息](https://docs.ucloud.cn/api/usms-api/get_usms_send_receipt) 获取