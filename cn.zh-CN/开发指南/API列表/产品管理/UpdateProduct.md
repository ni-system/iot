# UpdateProduct {#reference_g5d_54z_wdb .reference}

调用该接口修改指定产品的信息。

## 限制说明 {#section_dwh_m5f_xdb .section}

该接口的调用有限流，不得超过50次/秒。

## 请求参数 {#section_xm3_45f_xdb .section}

| | | | |
|:-|:-|:-|:-|
|Action|String|是|要执行的操作，取值：UpdateProduct。|
|ProductKey|String|是|要修改信息的产品的Key。|
|CatId|Long|否|产品类目信息。**说明：** 该字段是旧版本中遗留的字段，没有实际意义，您可以将其指定为任意的长整型数，例如10000。

|
|ProductName|String|否|修改后的产品名称。产品名应满足以下限制：由4-30位中文、英文字母、数字和下划线组成（一个中文字符占两位）。**说明：** 产品名在当前账号下应保持唯一。

|
|ProductDesc|String|否|指定修改后的产品描述信息。描述信息应在100字符以内。|

## 返回参数 {#section_lst_jvf_xdb .section}

|名称|类型|描述|
|:-|:-|:-|
|RequestId|String|阿里云为该请求生成的唯一标识符。|
|Success|Boolean|是否调用成功。ture表示调用成功，false表示调用失败。|
|ErrorMessage|String|调用失败时，返回的出错信息。|

## 示例 {#section_ujv_qvf_xdb .section}

**请求示例**

```
http://iot.cn-shanghai.aliyuncs.com/?Action=UpdateProduct
      &ProductKey=al*********
      &ProductName=TestProductNew
      &公共请求参数
```

**返回示例**

-   JSON格式

    ```
    {
          "RequestId":"C4FDA54C-4201-487F-92E9-022F42387458",
          "Success":true,
      }
    ```

-   XML格式

    ```
    <?xml version="1.0" encoding="UTF-8"?>
     <UpdateProductResponse>
          <RequestId>C4FDA54C-4201-487F-92E9-022F42387458</RequestId>
          <Success>true</Success>
      </UpdateProductResponse>
    ```


