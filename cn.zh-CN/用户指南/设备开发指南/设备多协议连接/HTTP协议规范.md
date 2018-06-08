# HTTP协议规范 {#concept_l14_nt5_wdb .concept}

## HTTP协议版本 {#section_qjt_4t5_wdb .section}

-   支持 Hypertext Transfer Protocol — HTTP/1.0 协议，具体请参考：[RFC 1945](https://tools.ietf.org/html/rfc1945)
-   支持 Hypertext Transfer Protocol — HTTP/1.1 协议，具体请参考：[RFC 2616](https://tools.ietf.org/html/rfc2616)

## 通道安全 {#section_l45_qt5_wdb .section}

使用HTTPS\(Hypertext Transfer Protocol Secure协议\)保证通道安全。

-   不支持？号形式传参数。
-   暂时不支持资源发现。
-   仅支持HTTPS。
-   URI规范, HTTP的URI资源和MQTT TOPIC保持一致，参考[MQTT规范](https://help.aliyun.com/document_detail/30540.html?spm=5176.doc57699.2.4.fVbU8T)。

