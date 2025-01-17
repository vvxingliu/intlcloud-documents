## 操作背景

该任务以 Python 客户端为例指导您使用公网网络接入消息队列 CKafka 并收发消息。

## 前提条件

- [安装 Python](https://www.python.org/downloads/)
- [安装 pip](https://pip-cn.readthedocs.io/en/latest/installing.html)
- [配置 ACL 策略](https://intl.cloud.tencent.com/document/product/597/39084)
- [下载 Demo](https://github.com/TencentCloud/ckafka-sdk-demo/tree/main/pythonkafkademo/gongwang)

## 操作步骤

### 步骤一：添加 Python 依赖库

执行以下命令安装：
```bash
pip install kafka-python
```

### 步骤二：生产消息

1. 修改生产消息程序 producer.py 中配置参数。

```python
#coding:utf8
from kafka import KafkaProducer
import json
producer = KafkaProducer(
bootstrap_servers = ['$domainName:$port'],
ssl_check_hostname = False,
security_protocol = "SASL_PLAINTEXT",
sasl_mechanism = "PLAIN",
sasl_plain_username = "$instance_id#$username",
sasl_plain_password = "$password",
api_version = (0,10,0)
)
message = "Hello World! Hello Ckafka!"
msg = json.dumps(message).encode()
producer.send('topic_name',value = msg)
print("produce message " + message + " success.");
producer.close()
```

| 参数                | 描述                                                         |
| ------------------- | ------------------------------------------------------------ |
| bootstrap_servers   | 接入网络，在控制台的实例详情页面【接入方式】模块的网络列复制。<br/>![img](https://main.qcloudimg.com/raw/afc2a197f4e0646f40aa6280c5f6414d.png) |
| sasl_plain_username | 用户名，格式为 `实例 ID` + `#` + `用户名`。实例 ID 在 [CKafka 控制台](https://console.cloud.tencent.com/ckafka) 的实例详情页面的基本信息获取，用户在【用户管理】创建用户时设置。 |
| sasl_plain_password | 用户密码，在 CKafka 控制台实例详情页面的【用户管理】创建用户时设置。 |
| topic_name          | Topic 名称，您可以在控制台上【topic管理】页面复制。<br/>![img](https://main.qcloudimg.com/raw/1b34ab83490f228ba0683609e0202c54.png) |

2. 编译并运行 producer.py。
3. 查看运行结果。
   ![](https://main.qcloudimg.com/raw/312d264676c655838e398ab9fa03b491.png)
4. 在 [CKafka 控制台](https://console.cloud.tencent.com/ckafka) 的【topic管理】页面，选择对应的 Topic ， 点击【更多】>【消息查询】，查看刚刚发送的消息。
   ![](https://main.qcloudimg.com/raw/417974c1d8df4a5ff409138e7c6b3def.png)





### 步骤三：消费消息

1. 修改消费消息程序 consumer.py 中配置参数。

```python
#coding:utf8
from kafka import KafkaConsumer

consumer = KafkaConsumer(
'$topic_name',
group_id = "$group_id",
bootstrap_servers = ['$domainName:$port'],
security_protocol = "SASL_PLAINTEXT",
sasl_mechanism = 'PLAIN',
sasl_plain_username = "$instance_id#$username",
sasl_plain_password = "$password",
api_version = (0,10,0)
)

for message in consumer:
    print ("Topic:[%s] Partition:[%d] Offset:[%d] Value:[%s]" % (message.topic, message.partition, message.offset, message.value))
```

| 参数                | 描述                                                         |
| ------------------- | ------------------------------------------------------------ |
| bootstrap_servers   | 接入网络，在控制台的实例详情页面【接入方式】模块的网络列复制。<br/>![img](https://main.qcloudimg.com/raw/afc2a197f4e0646f40aa6280c5f6414d.png) |
| group_id            | 消费者的组 ID，根据业务需求自定义。                          |
| sasl_plain_username | 用户名，格式为 `实例 ID` + `#` + `用户名`。实例 ID 在CKafka 控制台的实例详情页面的基本信息获取，用户在【用户管理】创建用户时设置。 |
| sasl_plain_password | 用户名密码，在 CKafka 控制台实例详情页面的【用户管理】创建用户时设置 |
| topic_name          | Topic 名称，您可以在控制台上【topic管理】页面复制。<br/>![img](https://main.qcloudimg.com/raw/1b34ab83490f228ba0683609e0202c54.png) |

2. 编译并运行 consumer.py。

3. 查看运行结果。
   ![](https://main.qcloudimg.com/raw/479f3b14e67a5f50f9d49781ab4df39f.png)

4. 在  [CKafka 控制台](https://console.cloud.tencent.com/ckafka) 的【Consumer Group】页面，选择对应的消费组名称，在主题名称输入 Topic 名称，单击【查询详情】，查看消费详情。
   ![](https://main.qcloudimg.com/raw/22b1e4dd27a79cb96c76f01f2aa7e212.png)
