这里是主流科学上网的优化集成配置示例。如是不太了解科学上网，建议先依次从简单到复杂参考及部署。

单一应用集成服务器端配置示例  
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++  
1、v2ray(vless\vmess+kcp+seed) （若网络极度差，推荐部署。）  
2、v2ray(vless\vmess+ws)+caddy2\nginx （ws的caddy2或nginx反向代理；之前推荐部署。）  
3、v2ray(vless\vmess+h2c)+caddy2 （h2的caddy2反向代理，自带链路复用。）  
4、v2ray(SS+v2ray-plugin)+caddy2\nginx （兼容shadowsocks的ws应用，caddy2或nginx反向代理。）  
5、v2ray(vless+tcp+tls)+caddy2 （回落给caddy2，支持http/1.1与h2回落。）  
6、v2ray(vless+tcp+tls)+nginx （回落给nginx，支持http/1.1与h2回落。）  
7、v2ray(trojan+tcp+tls)+caddy2 （兼容trojan应用，支持http/1.1与h2回落给caddy2。）  
8、v2ray(trojan+tcp+tls)+nginx （兼容trojan应用，仅支持http/1.1回落给nginx。）  
9、v2ray(trojan+ws)+caddy2\nginx （兼容trojan-go的ws应用，caddy2或nginx反向代理。）  
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++  
1、trojan\trojan-go+caddy2 （trojan或trojan-go应用，回落给caddy2。）  
2、trojan\trojan-go+nginx （trojan或trojan-go应用，回落给nginx。）  
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++  
1、naiveproxy(caddy2+forwardproxy) （naiveproxy应用，http/2或http/3正向代理。）  
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++  

综合应用集成服务器端配置示例  
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++  
1、v2ray为主，caddy2为辅。（推荐，功能多。）  
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++  
1）、v2ray(complete+h2c-tcp)+caddy2 （caddy2前置，反向代理ws与h2的综合应用。之前推荐部署。）  
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++  
1）、v2ray(vless+tcp+tls+ws)+caddy2 （目前推荐部署，同时支持vless+tcp与ws类应用，回落给caddy2。）  
2）、v2ray(trojan+tcp+tls+ws)+caddy2 （兼容trojan与兼容trojan-go的ws应用，回落给caddy2。）  
3）、v2ray(complete+h2c)+caddy2 （v2ray综合应用+反向代理h2应用。）  
4）、v2ray(complete+h2c)+naiveproxy （上一项应用+naiveproxy应用。）  
5）、v2ray(complete+h2c)+naiveproxy+trojan （上一项应用+trojan应用及共用端口。）  
6）、v2ray(complete+h2c)+naiveproxy+trojan+haproxy （用haproxy对上一项应用进行SNI分流，共用端口。）  
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++  
1）、v2ray(vless&trojan+tcp+tls+ws)+caddy2 （caddy2回落终极部署/套娃方式，或共用端口。）  
2）、v2ray(complete+trojan+h2c)+naiveproxy （v2ray全部应用+naiveproxy应用及共用端口。）  
3）、v2ray(complete+trojan+h2c)+naiveproxy+haproxy （用haproxy对上一项应用进行SNI分流，共用端口。）  
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++  
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++  
2、v2ray为主，nginx为辅。（以网站为主，且要求高（如稳定等）才推荐。）  
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++  
1）、v2ray(complete-tcp)+nginx （nginx前置，反向代理ws的综合应用。之前推荐部署。）  
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++  
1）、v2ray(vless+tcp+tls+ws)+nginx （目前推荐部署，同时支持tcp与ws，回落给nginx。）  
2）、v2ray(trojan+tcp+tls+ws)+nginx （兼容trojan与兼容trojan-go的ws应用，回落给nginx。）  
3）、v2ray(complete)+nginx （v2ray综合应用。）  
4）、v2ray(complete)+nginx+trojan （上一项应用+trojan应用及共用端口。）  
5）、v2ray(complete+h2c)+nginx+trojan+naiveproxy （上一项应用+naiveproxy+反向代理h2应用及共用端口。）  
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++  
1）、v2ray(vless&trojan+tcp+tls+ws)+nginx （nginx回落终极部署/套娃方式，或共用端口。）  
2）、v2ray(complete+trojan+h2c)+nginx+naiveproxy （v2ray全部应用+naiveproxy应用及共用端口。）  
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++  
注意：  
1、naiveproxy=caddy2+forwardproxy。此程序文件已编译好，本github下载即可。  
2、complete表示包含v2ray的vless+tcp+tls、vless\vmess+ws+tls、SS+v2ray-plugin+tls、vless\vmess+kcp+seed的综合应用。  

client  
客户端配置示例目录，目录内包含对应服务端应用的客户端配置示例。

service  
程序service文件目录，目录内包含各个程序service配置示例。

使用/贡献指南  
1、若程序增加新功能，开始主要单一应用集成服务器端配置示例中添加；过一段时间稳定后才会全部配置示例中添加。如除trojan+tcp套娃外，vless+tcp及trojan+tcp的xtls已全部加上。  
2、欢迎你提交 PR ,如对现行配置示例优化修订，或将自己使用的配置制作模板提交等。
