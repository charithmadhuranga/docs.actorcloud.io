# 设备

## 查看设备列表

!#!GET_/api/v1/devices?_page={page}&_limit={pageSize}!#!




## 查看设备详情

!#!GET_/api/v1/devices/{id}!#!




## 创建设备

!#!POST_/api/v1/devices!#!


### 创建说明

支持创建多种类型设备，请求参数根据所选产品的云端协议有所不同，除去基础信息之外，下表给出相关差异：

| 云端协议     | 必填项        | 锁定项   |
| --------------- | ----------------- | ------- |
| MQTT、CoAP、HTTP、WebSocket | 认证方式：`authType` | -- |
| LwM2M | 接入 IEMI：`IMEI` 、自动订阅： `autoSub` | -- |
| LoRa | LoRa 协议相关信息，入网方式：`lora.type` 、DevEUI：`deviceID`、AppEUI： `lora.appEUI`、AppKey： `lora.appKey` 、FCnt Check： `lora.fcntCheck`、允许加入：`lora.canJoin` | 入网方式：`lora.type`等于 `otaa` 时 |
| LoRa | LoRa 协议相关信息，入网方式：`lora.type` 、所属网关：`gateway`、DevAddr： `deviceID`、发射频率： `lora.region` 、NwkSKey： `lora.nwkSKey`、AppSKey：`lora.appSKey`、FCnt Up：`lora.fcntUp`、FCnt Down： `lora.fcntDown`、FCnt Check：`lora.fcntCheck` | 入网方式：`lora.type`等于 `abp` 时 |





## 编辑设备

!#!PUT_/api/v1/devices/{id}!#!




## 删除设备

!#!DELETE_/api/v1/devices?ids={ids}!#!




## 导出设备

!#!GET_/api/v1/devices_export!#!




## 导入设备

!#!POST_/api/v1/devices_import!#!




## 设备事件

!#!GET_/api/v1/devices/{id}/events?_page={page}&_limit={pageSize}!#!




## 设备控制

!#!POST_/api/v1/device_publish!#!




## 新建设备定时任务

!#!POST_/api/v1/device_schedule_publish!#!




## 删除设备定时任务

!#!DELETE_/api/v1/device_schedule_publish?ids={ids}!#!




## 查看设备指标数据

!#!GET_/api/v1/metrics_data?deviceID={deviceID}&metricType=1!#!




## 查看设备原始数据

!#!GET_/api/v1/original_data?deviceID={deviceID}&metricType=2&time_unit=day!#!



