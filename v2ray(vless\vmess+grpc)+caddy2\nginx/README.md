介绍：

通过 caddy2 前置 v2ray（Xray） server 实现 gRPC 反向代理，tls 由 caddy2 或 nginx 提供及处理；包括 vless+grpc+tls 与 vmess+grpc+tls 两种应用。

原理图： v2ray client <------ gRPC+tls ------> caddy2\nginx <- gRPC -> v2ray server

注意：

1、Xray 版本不小于 1.4.0 或 v2ray 版本不小于v4.36.2，才完美支持 grpc 应用。

2、caddy2 等于或大于 v2.2.0-rc.1 版才支持 h2c proxy，即支持 v2ray（Xray） 的 h2c（gRPC）反向代理。

3、caddy2 的 Caddyfile 配置与 caddy.json 配置二选一（效果一样）。支持自动 https，即自动申请与更新证书与私钥，自动 http 重定向到 https。

4、此示例中若采用 nginx 反向代理，如果系统版本过低，其对应发行版仓库自带 nginx 预编译程序包可能不支持 tls1.3；如需要支持 tls1.3，必须先升级 OpenSSl 版本大于 1.1.1，再进行 nginx 源代码编译和安装。

5、支持 grpc 的 CDN 加速。
