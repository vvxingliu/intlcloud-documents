## 功能说明

本文为您介绍 API 请求出错时返回的错误码和对应错误信息。您可以根据 HTTP 的 StatusCode 和 Body 来确定问题。其中 Body 的格式如下：

```
{
    "errorcode" : "<ErrorCode>",
    "errormessage" : "<ErrorMessage>"
}
```

## 错误码列表

| HTTP 状态码（StatusCode） | 错误码（ErrorCode）  | 描述（ErrorMessage）                                         |
| ------------------------- | -------------------- | ------------------------------------------------------------ |
| 400                       | InvalidAuthorization | 签名串格式不合法                                             |
| 400                       | InvalidCompressType  | 指定的 x-cls-compress-type 不支持                            |
| 400                       | InvalidContent       | 消息体错误，解压失败或者解析失败                             |
| 400                       | InvalidContentType   | 指定的 Content-Type 不支持                                   |
| 400                       | InvalidParam         | 缺少必要参数或者个别参数不合法                               |
| 400                       | MissingAgentIp       | 缺少 x-cls-agent-ip                                          |
| 400                       | MissingAgentVersion  | 缺少 x-cls-agent-version                                     |
| 400                       | MissingAuthorization | 缺少 Authorization                                           |
| 400                       | MissingContent       | 消息体是空的                                                 |
| 400                       | MissingContentType   | 缺少 Content-Type                                            |
| 400                       | TopicClosed          | 指定的日志主题已经关闭收集功能                               |
| 400                       | IndexRuleEmpty       | 指定的日志主题没有设置索引规则                               |
| 400                       | LogsetNotEmpty       | 指定的日志集非空，含有日志主题                               |
| 400                       | SyntaxError          | 检索语法错误                                                 |
| 400                       | LogsetEmpty          | 指定的日志集为空，不包含任何日志主题                         |
| 400                       | LimitExceeded           | 并发查询超过限制                         |
| 401                       | AuthFailure.SecretIdNotFound        | 密钥不存在。 请在控制台检查密钥是否已被删除或者<br>禁用，如状态正常，请检查密钥是否填写正确，注意前后不得有空格 |
| 401                       | AuthFailure.SignatureFailure         | 签名错误。 签名计算错误，请对照调用方式中的签名<br>方法文档检查签名计算过程                    |
| 401                       | AuthFailure.SignatureExpire         | 签名过期                                 |
| 401                       | AuthFailure.MFAFailure         | MFA 错误                                 |
| 401                       | AuthFailure.UnauthorizedOperation         | 请求未授权。请参考 [CAM](https://intl.cloud.tencent.com/document/product/598) 文档对鉴权的说明       |
| 401                       | AuthFailure.InvalidSecretId         | 密钥非法（不是云 API 密钥类型）                                 |
| 401                       | AuthFailure.TokenFailure         | token 错误                                 |
| 401                       | AuthFailure.Unauthorized         | 鉴权内部错误                                 |
| 403                       | LogsetExceed         | 日志集数量超出限制，最多20个                                 |
| 403                       | LogSizeExceed        | 提交的日志超出最大限制，最大5MB                              |
| 403                       | MachineGroupExceed   | 机器组数量超出限制，最多200个                                |
| 403                       | NotAllowed           | 不允许此操作                                                 |
| 403                       | TopicExceed          | 日志主题数量超出限制，最多10个                               |
| 403                       | ShipperExceed        | 投递规则数量超出限制，最多10个                               |
| 403                       | TaskReadOnly         | 只有失败的投递任务才能重启，其他状态时不能被修改             |
| 403                       | AccountArrears          | 账户欠费             |
| 403                       | ServiceNotActivated          | 日志服务未开通              |
| 404                       | CursorNotExist       | 指定的位置没有可以下载的日志                                 |
| 404                       | TaskNotExist         | 指定的投递任务不存在                                         |
| 404                       | IndexNotExist        | 指定的索引规则不存在                                         |
| 404                       | LogsetNotExist       | 指定的日志集不存在                                           |
| 404                       | MachineGroupNotExist | 指定的机器组不存在                                           |
| 404                       | ShipperNotExist      | 指定的投递规则不存在                                         |
| 404                       | TopicNotExist        | 指定的日志主题不存在                                         |
| 404                       | ConsumerNotExist     | 指定的日志主题不存在消费任务                                 |
| 405                       | NotSupported         | 不支持此操作                                                 |
| 409                       | IndexConflict        | 相同的索引规则已存在                                         |
| 409                       | LogsetConflict       | 相同的日志集已存在                                           |
| 409                       | MachineGroupConflict | 相同的机器组已存在                                           |
| 409                       | ShipperConflict      | 相同的投递规则已存在                                         |
| 409                       | TopicConflict        | 相同的日志主题已存在                                         |
| 409                       | ConsumerConflict     | 日志主题的消费任务已存在                                     |
| 429                       | SpeedQuotaExceed     | 请求过于频繁                                                 |
| 500                       | InternalError        | 内部错误                                                     |
