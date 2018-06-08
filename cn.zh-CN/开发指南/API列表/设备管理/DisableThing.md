# DisableThing {#reference_kqs_crz_wdb .reference}

调用该接口禁用指定设备。

## 接口说明 {#section_nlw_y5m_xdb .section}

使用该接口可以禁用一个设备。设备被禁用后将不能接入物联网平台，您将无法执行与设备有关的操作，但与设备关联的信息依然保留。您可以调用EnableThing接口重新接入被禁用的设备。

## 请求参数 {#section_q3r_fvm_xdb .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|要执行的操作，取值：DisableThing。|
|IotId|String|否| 要禁用的设备ID。

 **说明：** 如果传入该参数，则无需传入ProductKey和DeviceName。IotId作为设备唯一标识符，与ProductKey和DeviceName组合是一一对应的关系。如果您同时传入IotId和ProductKey&DeviceName组合，则以IotId为准。

 |
|ProductKey|String|否| 要禁用的设备所隶属的产品Key。

 **说明：** 如果传入该参数，需同时传入DeviceName。

 |
|DeviceName|String|否| 指定禁用的设备的名称。

 **说明：** 如果传入该参数，需同时传入ProductKey。

 |

## 返回参数 {#section_b5f_svm_xdb .section}

|名称|类型|描述|
|:-|:-|:-|
|RequestId|String|阿里云为该请求生成的唯一标识符。|
|Success|Boolean|表示是否调用成功。ture表示调用成功，false表示调用失败。|
|ErrorMessage|String|调用失败时，返回的出错信息。|

## 示例 {#section_erh_zvm_xdb .section}

**请求示例**

```
https://iot.cn-shanghai.aliyuncs.com/?Action=DisableThing
 &IotId=MpEKNuEUJzIORNANAWJX0010929900*****
 &公共请求参数
```

**返回示例**

-   JSON格式

    ```
    {
      "RequestId":"57b144cf-09fc-4916-a272-a62902d5b207",
      "Success": true
    }
    ```

-   XML格式

    ```
    <?xml version='1.0' encoding='utf-8'?>
    <DisableThingResponse>
        <RequestId>57b144cf-09fc-4916-a272-a62902d5b207</RequestId>
        <Success>true</Success>
    </DisableThingResponse>
    ```


