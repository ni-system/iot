# QueryProduct {#reference_tts_44z_wdb .reference}

调用该接口查询指定产品的详细信息。

## 限制说明 {#section_knr_nlf_xdb .section}

该接口的调用有限流，不得超过50次/秒。

## 请求参数 {#section_e54_rlf_xdb .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|要执行的操作，取值：QueryProduct。|
|ProductKey|String|是|要查询的产品的ProductKey。ProductKey是物联网平台为新建产品颁发的产品Key，作为其全局唯一标识符。您可以在创建产品的返回结果中查看该信息。|

## 返回参数 {#section_jbf_mmf_xdb .section}

|名称|类型|描述|
|:-|:-|:-|
|RequestId|String|阿里云为该请求生成的唯一标识符。|
|Success|Boolean|是否调用成功。ture表示调用成功，false表示调用失败。|
|ErrorMessage|String|调用失败时，返回的出错信息。|
|DataFormat|Integer| 数据格式，指设备与云端之间的数据通信协议类型。取值：

 0：透传模式。使用自定义的串口数据格式。该模式下，设备可以上报原始数据（如二进制数据流）。阿里云IoT平台会运行您配置在云端的数据解析脚本，将原始数据转换成Alink JSON标准数据格式。

 1：Alink JSON。阿里云IoT平台定义的设备与云端的数据交换协议，采用 JSON 格式。

 **说明：** 此参数为高级版产品特有参数。

 |
|ProductKey|String|产品Key。新建产品时，IoT为该产品颁发的全局唯一标识。|
|NodeType|Integer| 产品的节点类型，取值：

 0：设备。设备不能挂载子设备，可以直连IoT Hub，也可以作为网关的子设备连接IoT Hub。

 1：网关。网关可以挂载子设备，具有子设备管理模块，维持子设备的拓扑关系，并且可以将拓扑关系同步到云端。

 |
|ProductName|String|产品名称。|
|DeviceCount|Integer|产品下的设备数量。|
|GmtCreate|String|产品的创建时间。|
|Description|String|产品的描述信息。|
|AliyunCommodityCode|String|取值： iothub 或 iothub\_senior。|

## 示例 {#section_tvz_rnf_xdb .section}

**请求示例**

```
https://iot.cn-shanghai.aliyuncs.com/?Action=QueryProduct
      &ProductKey=al*********
     &<[公共请求参]>
```

**返回示例**

-   JSON格式

    ```
    {
        "RequestId":"57b144cf-09fc-4916-a272-a62902d5b207",
        "Success": true，
        "Data": {
            "DataFormat": 1,
            "ProductKey": "a1rYuVFha9S",
            "NodeType": 0,
            "ProductName": "日常测试",
            "DeviceCount": 7221,
            "GmtCreate": 1516534408000,
    	"AliyunCommodityCode":"iothub_senior"
            "Description": "描述信息"
        }
    }
    ```

-   XML格式

    ```
    <?xml version='1.0' encoding='UTF-8'?>
    <QueryProductResponse>
        <RequestId>57b144cf-09fc-4916-a272-a62902d5b207</RequestId>
        <Success>true</Success>
        <Data>
            <DataFormat>1</DataFormat>
            <ProductKey>a1*********</ProductKey>
            <NodeType>0</NodeType>
            <ProductName>日常测试</ProductName>
            <DeviceCount>7221</DeviceCount>
            <GmtCreate>1516534408000</GmtCreate>
    		<AliyunCommodityCode>iothub_senior</AliyunCommodityCode>
            <Description>描述信息</Description>
        </Data>
    </QueryProductResponse>
    ```


