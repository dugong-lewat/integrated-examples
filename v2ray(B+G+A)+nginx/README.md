介绍：

利用 Nginx 支持 WebSocket（WS）、gRPC 代理，实现除 Xray 或 V2Ray 的 mKCP 应用外，WebSocket（WS）、gRPC 两种类型的反向代理应用共用 443 端口，其应用如下：

1、B=vmess+ws+tls（TLS由Nginx启用及处理，不需配置。）

2、G=shadowsocks+grpc+tls（TLS由Nginx启用及处理，不需配置。）

3、A=vless+kcp+seed

注意：

1、Xray 或 V2Ray 的监听地址不支持 Shadowsocks（SS） 协议使用 UDS 监听。

2、Xray 版本不小于 v1.4.0 或 V2Ray 版本不小于 v4.36.2 才支持 gRPC 传输方式。

3、Nginx 支持 HTTP/2 server 及 gRPC proxy，需要 Nginx 包含 http_v2_module 和 http_ssl_module 模块。

4、Nginx 支持 TLSv1.3，需要包含版本不小于 1.1.1 的 OpenSSL 软件库包和 http_ssl_module 模块。

5、不要使用 ACME 客户端在采用本示例的服务器上以 HTTP-01 或 TLS-ALPN-01 验证方式申请与更新 TLS 证书，因 HTTP-01 或 TLS-ALPN-01 验证方式申请与更新 TLS 证书需监听 80 或 443 端口，从而与当前应用端口冲突。

6、配置1：使用 Local Loopback 连接。配置2：使用 UDS 连接（对应 shadowsocks+grpc+tls 除外）。
