# QueryDevicePropertyStatus {#reference_rgh_nrz_wdb .reference}

调用该接口查询指定设备的属性快照。

## 请求参数 {#section_rdp_hct_xdb .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|要执行的操作，取值：QueryDevicePropertyStatus。|
|IotId|String|否| 要查询的设备ID。

 **说明：** 如果传入该参数，则无需传入ProductKey和DeviceName。IotId作为设备唯一标识符，与ProductKey & DeviceName组合是一一对应的关系。如果您同时传入IotId和ProductKey&DeviceName组合，则以IotId为准。

 |
|ProductKey|String|否| 要查询的设备所隶属的产品Key。

 **说明：** 如果传入该参数，需同时传入DeviceName。

 |
|DeviceName|String|否| 要查询的设备的名称。

 **说明：** 如果传入该参数，需同时传入ProductKey。

 |

## 返回参数 {#section_ibj_pct_xdb .section}

|名称|类型|描述|
|:-|:-|:-|
|RequestId|String|阿里云为该请求生成的唯一标识符。|
|Success|Boolean|表示是否调用成功。ture表示调用成功，false表示调用失败。|
|ErrorMessage|String|调用失败时，返回的出错信息。|
|List|PropertyStatusInfo|调用成功时，返回的属性集合信息。详情参见[PropertyStatusInfo](#table_slw_ddt_xdb)。|

|名称|类型|描述|
|:-|:-|:-|
|Identifier|String|属性标识符。|
|Name|String|属性名称。|
|DataType|String| 属性格式类型，取值：

 int：整型。

 float：单精度浮点型。

 double：双精度浮点型。

 enum：枚举型。

 bool：布尔型。

 text：字符型。

 date：时间型（String类型的UTC时间戳，单位是毫秒）。

 array：数组型。

 struct：对象型。

 |
|Time|String|属性修改的时间，UTC时间戳，单位是毫秒。|
|Value|String|属性值。|
|Unit|String|属性单位。|

## 示例 {#section_gqj_ndt_xdb .section}

**请求示例** 

```
https://iot.cn-shanghai.aliyuncs.com/?Action=QueryDevicePropertyStatus
&IotId=...
&ProductKey=...
&DeviceName=...
&公共请求参数
```

**返回示例**

-   JSON格式

    ```
    {
        "RequestId":"57b144cf-09fc-4916-a272-a62902d5b207",
        "Success": true，
        "Data": {
            "List": {
                "PropertyStatusInfo": [
                    {
                        "Name": "doublePropertyName",
                        "Value": "50.0",
                        "Time": "1517553572362",
                        "DataType": "double",
                        "Identifier": "doubleProperty",
                        "Unit": "C"
                    }
                ]
            }
        }
    ```

-   XML格式

    ```
    <?xml version='1.0' encoding='utf-8'?>
    <QueryDevicePropertyStatusResponse>
        <RequestId>57b144cf-09fc-4916-a272-a62902d5b207</RequestId>
        <Success>true</Success>
        <Data>
            <List>
                <PropertyStatusInfo>
                    <Time>1517553572362</Time>
                    <Name>1212</Name>
                    <DataType>int</DataType>
                    <Identifier>ab</Identifier>
                    <Value>1</Value>
                    <Unit>km</Unit>
                </PropertyStatusInfo>
                <PropertyStatusInfo>
                    <Time>1517553572362</Time>
                    <Name>LightAdjustLevel</Name>
                    <DataType>int</DataType>
                    <Identifier>LightAdjustLevel</Identifier>
                    <Value></Value>
                    <Unit>dm</Unit>
                </PropertyStatusInfo>
                <PropertyStatusInfo>
                    <Time>1517553572362</Time>
                    <Name>12313312</Name>
                    <DataType>int</DataType>
                    <Identifier>12312</Identifier>
                    <Value></Value>
                    <Unit></Unit>
                </PropertyStatusInfo>
            </List>
        </Data>
    </QueryDevicePropertyStatusResponse>
    ```


