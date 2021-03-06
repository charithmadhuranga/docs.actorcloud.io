# 消息规则

**ActorCloud** 消息规则能将某个产品/分组下的设备上报的数据转发至外部的 Webhook 接口、数据库、消息队列等，在**规则管理** -> **消息规则**中可进行相关配置。


### Webhook

Webhook 支持将相关设备上报数据以 HTTP POST 方法推送到服务器，HTTP 服务器配置如下：

#### 认证

新建 Webhook 消息规则时，**ActorCloud** 会根据填入的 URL 地址与 token 进行认证，服务器将发送 GET 请求到填写的服务器地址 URL 上，请求携带参数如下:

- timestamp 时间戳；
- nonce 随机数；
- signature 加密签名，signature 为 token、 timestamp、nonce 变量值拼接并进行 sha1 加密后的值。。

请求地址为：`{{url}}?signature=xxx&?timestamp=yyy&nonce=zzz`


Webhook 接口收到请求后，需要进行校验，校验规则如下：

- 按 token、timestamp、nonce 顺序，将三个变量的值拼接为一个字符串，并用 sha1 进行加密；
- 将加密后的字符串与请求中的 signature 字符串对比。

若相等则验证通过，直接以 JSON 格式返回 nonce 随机数：

```json
{
  "nonce": "zzz"
}
```

#### 接入

完成消息规则创建后， 平台会将相关设备上报消息以 JSON 形式推送到填入的 Webhook URL 地址中，
该 HTTP 请求头中会以 Bearer Token 形式携带 token 信息以便 Webhook 服务器进行合法性认证。

- 请求数据如下：

```bash
# Bearer Token 请求头
Authorization: Bearer eyJhbGciOiJIUzI1NiIsImV4cCI6MTUyNDkwMDEwNywiaWF0IjoxNTI0N
```

```json
{ "deviceID": "f50b69da0f2e5686be3413e29151aacd",
  "productID": "oUZSzN",
  "groupID": "",
  "topic": "/temperature",
  "qos": 1,
  "retain": false,
  "payload": "{\"temperature\": 77}",
  "ts": 1524635104
}
```

- 数据定义：

| 字段名             | 说明            |
| --------------- | ----------------- |
| deviceID      | 设备编号 |
| productID      | 产品标识符（关联对象为产品时携带） |
| groupID      | 分组标识符（关联对象为分组时携带） |
| topic      | 消息主题 |
| qos      | 消息QoS |
| retain      | 是否 retain |
| payload      | 消息内容 |
| ts      | 消息时间戳 |
