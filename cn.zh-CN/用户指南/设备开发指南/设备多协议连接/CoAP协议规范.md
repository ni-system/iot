# CoAP协议规范 {#concept_tcf_yq5_wdb .concept}

## 协议版本 {#section_rpv_zq5_wdb .section}

支持 RFC 7252 Constrained Application Protocol协议，具体请参考：[RFC 7252](http://tools.ietf.org/html/rfc7252)。

## 通道安全 {#section_gvl_br5_wdb .section}

使用 DTLS v1.2保证通道安全，具体请参考：[DTLS v1.2](https://tools.ietf.org/html/rfc6347)。

## 开源客户端参考 {#section_fc5_cr5_wdb .section}

[http://coap.technology/impls.html](http://coap.technology/impls.html)。

**说明：** 若使用第三方代码, 阿里云不提供技术支持

## 阿里CoAP约定 {#section_m5z_fr5_wdb .section}

-   不支持？号形式传参数。
-   暂时不支持资源发现。
-   仅支持UDP协议，并且目前必须通过DTLS。
-   URI规范，CoAP的URI资源和MQTT TOPIC保持一致，参考[MQTT规范](https://help.aliyun.com/document_detail/30540.html)。

