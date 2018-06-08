# 物联网平台对接大数据实践-DataHub流计算 {#task_ist_bpr_ydb .task}

-   场景

    实时统计某产品下活跃设备数量并生成实时图表。

    活跃设备指设备端在最近N分钟内发送过消息的设备。

-   为什么要用DataHub

    DataHub是大数据的存储入口，通过把数据流转到大数据平台，结合Streamsql即可实现实时流计算，再通过可视化产品DataV配置出大屏。

    传统关系型数据库需要存储大量的数据，加大了计算复杂度。

-   思路

    使用规则引擎，将该产品下所有设备发送的消息转发到DataHub，再经过流计算处理，在DataV可视化大屏实时展示设备数量。


实现流程如[图 1](#fig_lxz_1qr_ydb)所示。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7641/4212_zh-CN.png "流程图")

1.   开通DataHub服务。 
    1.   登录[DataHub控制台](https://datahub.console.aliyun.com/datahub)，选择项目管理。 
    2.   单击**创建Project**，创建Project。 
    3.   单击Project后的**查看**。 系统显示新建Project的详情页面。
    4.   单击**创建Topic**。 

        系统显示创建Topic页面，如[图 2](#fig_ons_wrr_ydb)所示。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7641/4213_zh-CN.png "创建Topic")

    5.   设置Topic参数，单击**创建**。 
2.   开通物联网平台服务。 
    1.   登录物联网平台的控制台。 
    2.   选择产品管理，单击**创建产品**，创建用于DataHub的产品。 
    3.   选择设备管理，选择用于DataHub的产品，单击**添加设备**。 
    4.   选择规则引擎，单击**创建规则**。 
    5.   单击新建规则后的**管理**，进入规则详情页面。 
    6.   单击处理数据页签下的**编写SOL**，编写处理数据，如[图 3](#fig_et3_35r_ydb)所示。 

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7641/4214_zh-CN.png "处理数据")

    7.   单击转发数据后的**添加操作**，配置规则动作，将创建的DataHub的topic作为规则的转发目的地，如[图 4](#fig_rxx_w5r_ydb)所示。 

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7641/4215_zh-CN.png "配置规则动作")

    8.   在规则引擎后，单击规则后的**启动**，启动规则。 
3.   使用模拟设备端，发送消息，具体参见[设备开发指南](../cn.zh-CN/用户指南/设备开发指南.md#)。 
    -   发送消息如下：

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7641/4216_zh-CN.png)

    -   返回信息如下：

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7641/4217_zh-CN.png)

4.   物联网平台跟DataHub对接检验。 

    检验设备发送的消息是否成功流转至DataHub中，可以通过日志服务，也可以直接去DataHub控制台对应的topic中，查看Shards中数据量的变化，数据抽样功能可以看到具体的消息内容。

    -   日志服务检查，消息的流转路径，全都能查询出来。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7641/4218_zh-CN.png)

    -   DataHub数据验证，消息内容跟设备发送的消息内容一致，物联网平台跟DataHub对接已经成功。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7641/4219_zh-CN.png)

5.   接入[流计算](https://stream.console.aliyun.com/)。 

    根据DataHub中，设备发送消息记录的流式数据表，需要计算出一个指标：截至到当前时间，发送了消息的设备数量。这个指标经过流计算，写入在线RDS系统中，并通过DataV大屏展示。

    RDS表设计如下：

    |字段名|类型|注释|
    |---|--|--|
    |d\_data|varchar\(32\)|时间|
    |device\_num|int|活跃设备数量|

    1.   登录RDS控制台。 
    2.   单击**登录数据库**，创建RDS表格。 
    3.   登录流计算控制台，单击**新建**，新建作业。 
    4.   在流计算控制台，选择**数据存储** \> **DataHub数据存储**，Project设置为申请的Project名称。 
    5.   在流计算控制台，选择**数据存储** \> **RDS数据存储**，设置RDS数据存储。 
    6.   作业开发引用数据存储。 
        -   DataHub的Topic作为数据输入源，单击**作为输入表引用**，流计算将自动解析Topic的Schema，并自动添加对应的SQL到IDE：

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7641/4220_zh-CN.png)

        -   RDS的表作为数据结果输出，单击选择作为结果表引用，流计算将自动解析RDS的表Schema，并自动添加对应的SQL到IDE：

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7641/4221_zh-CN.png)

    7.   编写streamSQL。 

        ```
        
        REPLACE INTO activity_device 
        SELECT 
        from_unixtime(FLOOR(dm.msgtime/1000), 'yyyy-MM-dd') as d_data,
        count(DISTINCT dm.devicename) as device_num
        FROM device_message dm
        group by from_unixtime(FLOOR(dm.msgtime/1000), 'yyyy-MM-dd');
        ```

    8.   在流计算控制台，单击**调试**，调试SQL，得到的结果跟数据预期一致，表示SQL正确。 
    9.   在流计算控制台，选择**开发** \> **上线**，启动作业。 
    10.  使用不同的设备登录，发送消息，查看RDS中数据变化，每使用一个新的设备发送消息，当天RDS中设备数量会加1，跟预期结果一致，表示iot-datahub-stream对接成功。 
6.   DataV可视化接入，开通DataV服务，登录[DataV控制台](http://datav.aliyun.com/)。 
    1.   单击**添加数据**，将RDS对应的数据库连接信息配置数据存储。 
    2.   新建可视化，配置数据。 

        DataV提供了很多的大屏模板，样式也都可以自己调节，这里以最简单的折线图为例。具体的配置说明请访问[DataV官网](https://data.aliyun.com/visual/datav?spm=a2c4g.750001.765261.376.NflAxo)，查看DataV官网文档。

        配置完成之后，使用不同的设备登录，并发送消息，大屏展示的活跃设备数会实时改变。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7641/4222_zh-CN.png "曲线图")


