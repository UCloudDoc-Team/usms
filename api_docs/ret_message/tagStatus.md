# 短信使用状态上报 - upUSMSCustomerStatus

您在使用国际及港澳台短信服务的过程中，通过该接口主动将验证码使用率上报至我们平台，我们将持续为您提供更好的服务。



## 请求说明

您可以选择以下方式中的任意一种，发起 API 请求：

- 多语言 OpenSDK / [Python](https://github.com/ucloud/ucloud-sdk-python3) / [Java](https://github.com/ucloud/ucloud-sdk-java) /
- [UAPI 浏览器]({{consoleURL}}/uapi/detail?id=SendUSMSMessage)
- [CloudShell 云命令行](https://shell.{{domainName}}/)



## 定义

### 公共参数

| 参数名        | 类型   | 描述信息                                                     | 必填    |
| ------------- | ------ | ------------------------------------------------------------ | ------- |
| **Action**    | string | 对应的 API 指令名称，当前 API 为 `SendUSMSMessage`           | **Yes** |
| **PublicKey** | string | 用户公钥，可从 [控制台]({{consoleURL}}/uapi/apikey) 获取 | **Yes** |
| **Signature** | string | 根据公钥及 API 指令生成的用户签名，参见 [签名算法](https://docs.{{domainName}}/api/summary/signature) | **Yes** |



### 参数说明

| 参数名             | 类型   | 描述信息                                                     | 举例                           | 必填 |
| ------------------ | ------ | ------------------------------------------------------------ | ------------------------------ | ---- |
| **ProjectId**      | string | 项目ID。不填写为默认项目，子帐号必须填写。 请参考[GetProjectList接口](https://docs.{{domainName}}/api/summary/get_project_list) | org-bXXXXry                    | Yes  |
| **SessionNoSet.N** | string | [短信发送](https://docs.{{domainName}}/api/usms-api/send_usms_message) 返回的SessionNo序列号集合，参数格式 SessionNoSet.0，SessionNoSet.1 .... | xddd-xx-ss-ss-ss               | Yes  |
| **PhoneNumbers.N** | string | 电话号码数组，电话号码格式为(60)1xxxxxxxx，()中为国际长途区号(如中国为86或0086，两种格式都支持)，后面为电话号码.若不传入国际区号，如1851623xxxx，则默认为国内手机号 | (86)185XXXX9057                | No   |
| **CustomerStatus** | string | 客户主动上报的短信使用情况                                   | 0代表短信已使用，非0表示未使用 | No   |



### 响应字段

| 字段名      | 类型                  | 描述信息                                             | 必填    |
| ----------- | --------------------- | ---------------------------------------------------- | ------- |
| **Action**  | string                | 操作指令名称                                         | **Yes** |
| **Message** | string                | 返回错误消息，当 `RetCode` 非 0 时提供详细的描述信息 | No      |
| **RetCode** | int                   | 返回状态码，为 0 则为成功返回，非 0 为失败           | **Yes** |
| **Data**    | array[customerStatus] | 信息集合                                             | **Yes** |



### 请求示例

```json
{{apiURL}}/?Action=upUSMSCustomerStatus
&ProjectId=org-XXXXqi
&SessionNoSet.0=497XXXX4-eXXXXc-4XXX
&PhoneNumber.0=185XXXX9057
&CustomerStatus=0
```



### 响应示例

```json
{
  "Action": "upUSMSCustomerStatus",
  "Message": "submit success",
  "RetCode": 0,
  "Data": 
   [
  	    {
   	  		 "MessageNo": "497XXXX4-eXXXXc-4XXX"
  	 	 }
   ]
}
```

