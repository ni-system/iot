# DeleteTopicRouteTable {#reference_vs2_2jd_xdb .reference}

调用该接口删除指定的Topic路由关系。

## 请求参数 {#section_avh_1l5_xdb .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|要执行的操作，取值：DeleteTopicRouteTable。|
|SrcTopic|String|是|源Topic，即被订阅的Topic。|
|DstTopics|List|是|目标Topic列表，即从SrcTopic订阅消息的Topic列表。|

## 返回参数 {#section_njn_hl5_xdb .section}

|名称|类型|描述|
|:-|:-|:-|
|RequestId|String|阿里云为该请求生成的唯一标识符。|
|Success|Boolean|表示是否调用成功。ture表示调用成功，false表示调用失败。|
|ErrorMessage|String|调用失败时，返回的出错信息。|
|FailureTopics|List|未能成功删除路由关系的Topic列表。|

## 示例 {#section_mf5_ll5_xdb .section}

**请求示例**

```
https://iot.cn-shanghai.aliyuncs.com/?Action=DeleteTopicRouteTable
 &SrcTopic=/CXi4***/device1/get
 &DstTopics=[{/CXi4***/device2/get},{/CXi4***/device3/get}]
 &公共请求参数
```

**返回示例**

```
{
    "RequestId":"FCC27691-9151-4B93-9622-9C90F30542EC",
    "Success":true,
    "FailureTopics":[]
}
```

