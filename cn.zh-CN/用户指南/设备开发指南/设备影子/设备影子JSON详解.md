# 设备影子JSON详解 {#concept_w3l_41v_wdb .concept}

## 设备影子JSON格式 {#section_ssc_bcx_wdb .section}

格式为：

```

{
"state": {
"desired": {
"attribute1": integer2,
"attribute2": "string2",
...
"attributeN": boolean2
},
"reported": {
"attribute1": integer1,
"attribute2": "string1",
...
"attributeN": boolean1
}
},
"metadata": {
"desired": {
"attribute1": {
"timestamp": timestamp
},
"attribute2": {
"timestamp": timestamp
},
...
"attributeN": {
"timestamp": timestamp
}
},
"reported": {
"attribute1": {
"timestamp": timestamp
},
"attribute2": {
"timestamp": timestamp
},
...
"attributeN": {
"timestamp": timestamp
}
}
},
"timestamp": timestamp,
"version": version
}
```

JSON属性描述，如[表 1](#table_mwk_fcx_wdb)所示。

|属性|描述|
|--|--|
|desired|设备的预期状态。应用程序向desired部分写入数据更新事物的状态，无需直接连接到该设备。

|
|reported|设备的报告状态。设备可以在reported部分写入数据，报告其最新状态。应用程序可以通过读取该参数值，获取设备的状态。

|
|metadata|当用户更新State文档，设备影子服务会自动更新metadata的值。state 部分的元数据的信息，包括 state 部分中每个属性的时间戳，以 Epoch 时间表示，用来获取确定的更新时间。

|
|timestamp|影子文档的最新更新时间。|
|version|用户主动更新version，设备影子会检查请求中的version是否大于当前版本。如果大于当前版本，则更新设备影子，并将version更新到请求的版本中，反之拒绝更新设备影子。

该参数更新后，版本号会递增，用于确保正在更新的文档为最新版本。

|

示例影子JSON：

```

{
"state" : {
"desired" : {
"color" : "RED",
"sequence" : [ "RED", "GREEN", "BLUE" ]
},
"reported" : {
"color" : "GREEN"
}
},
"metadata" : {
"desired" : {
"color" : {
"timestamp" : 1469564492
},
"sequence" : {
"timestamp" : 1469564492
}
},
"reported" : {
"color" : {
"timestamp" : 1469564492
}
}
},
"timestamp" : 1469564492,
"version" : 1
}
```

## 空白部分 {#section_aly_cdx_wdb .section}

-   仅当设备影子文档具有预期状态时，才包含desired部分。没有desired部分的文档同样为有效影子JSON文档：

    ```
    
    {
    "state" : {
    "reported" : {
    "color" : "red",
    }
    },
    "metadata" : {
    "reported" : {
    "color" : {
    "timestamp" : 1469564492
    }
    }
    },
    "timestamp" : 1469564492,
    "version" : 1
    }
    ```

-   reported部分可以为空，没有reported部分的文档同样为有效影子JSON文档：

    ```
    
    {
    "state" : {
    "desired" : {
    "color" : "red",
    }
    },
    "metadata" : {
    "desired" : {
    "color" : {
    "timestamp" : 1469564492
    }
    }
    },
    "timestamp" : 1469564492,
    "version" : 1
    }
    ```


## 数组 {#section_chh_ldx_wdb .section}

设备影子支持数组，数组必须全量更新，不能只更新数组的某一部分。

-   初始状态：

    ```
    
    {
    "reported" : { "colors" : ["RED", "GREEN", "BLUE" ] }
    }
    ```

-   更新：

    ```
    
    {
    "reported" : { "colors" : ["RED"] }
    }
    ```

-   最终状态：

    ```
    
    {
    "reported" : { "colors" : ["RED"] }
    }
    ```


