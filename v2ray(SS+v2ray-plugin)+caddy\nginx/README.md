介绍：

1、本示例配置采用 Xray 或 V2Ray 自带 Shadowsocks 应用加 Dokodemo-Door 的 WebSocket 应用（dd+ws） 组合，直接实现原版 Shadowsocks 加 xray-plugin 或 v2ray-plugin 的 WebSocket 服务端应用。

2、利用 Caddy 或 Nginx 支持 WebSocket（WS） 代理，实现等同原版 shadowsocks+xray-plugin+tls 或 shadowsocks+v2ray-plugin+tls 的 WebSocket 反向代理应用，TLS 由 Caddy 提供及处理或由 Nginx 启用及处理。

原理：

默认流程：WEB client <-------- HTTPS（HTTP/1.1+TLS） -------> Caddy/Nginx（WEB server）  
反代流程：Shadowsocks client <------- WebSocket+TLS --------> Caddy/Nginx <-- WebSocket --> Xray/V2Ray server

注意：

1、Xray 或 V2Ray 的监听地址不支持 Dokodemo-Door 协议使用 UDS 监听。

2、v2ray_UDS_config.json 采用 UDS 实现 Shadowsocks 应用与 dd+ws 应用连接；v2ray_LL_config.json 采用 Local Loopback 实现 Shadowsocks 应用与 dd+ws 应用连接，根据情况二选一即可。

3、本示例 shadowsocks+xray-plugin+tls 或 shadowsocks+v2ray-plugin+tls 的 WebSocket 应用不等同 Xray 或 v2ray 的 [shadowsocks+ws+tls](https://github.com/lxhao61/integrated-examples/tree/main/v2ray(SS%2BWS)%2Bcaddy%5Cnginx) 应用，两者不兼容。

4、若采用 Caddy 反向代理，本示例 Caddy 支持自动 HTTPS，即自动申请与更新 TLS 证书，自动 HTTP 重定向到 HTTPS。

5、Nginx 支持 TLSv1.3，需要包含版本不小于 1.1.1 的 OpenSSL 软件库包和 http_ssl_module 模块。

6、若采用 Nginx 反向代理，不要使用 ACME 客户端在采用本示例的服务器上以 HTTP-01 或 TLS-ALPN-01 验证方式申请与更新 TLS 证书，因 HTTP-01 或 TLS-ALPN-01 验证方式申请与更新 TLS 证书需监听 80 或 443 端口，从而与当前应用端口冲突。
