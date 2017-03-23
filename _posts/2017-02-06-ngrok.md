---
author: yeyeli
title: 内网穿透-ngrok
featimg: http://upload-images.jianshu.io/upload_images/1271438-ac919bf5263a9eb0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240

layout: post-full
---

##### 导语:

>很多时候公司电脑是没有公网ip, 都连路由器去了.当我们在进行一些开发时候,比如,支付需要回调通知,就只能将代码拉到服务器去调试,不方便.
    有ngrok就可以让你在内网环境享受外网待遇.
    其实ngrok 他本是官方是提供这个服务的,但是访问速度特别的慢,所以很多人还是选择在自己的服务器上面搭建这项服务.
    这篇文章就是主要记录怎样去一步一步的操作.

##### 搭建环境: CentOS + mac

***
##### 详细步骤
###### 1.安装环境
`yum install golang`
`yum install supervisor`
###### 2.下载资源
`git clone https://github.com/inconshreveable/ngrok.git`

备用资源：`git clone https://github.com/tutumcloud/ngrok.git`
###### 3.生成证书（操作在ngrok目录下）
```
NGROK_DOMAIN="yeli.photo"
openssl genrsa -out rootCA.key 2048
openssl req -x509 -new -nodes -key rootCA.key -subj "/CN=$NGROK_DOMAIN" -days 5000 -out rootCA.pem
openssl genrsa -out device.key 2048
openssl req -new -key device.key -subj "/CN=$NGROK_DOMAIN" -out device.csr
openssl x509 -req -in device.csr -CA rootCA.pem -CAkey rootCA.key -CAcreateserial -out device.crt -days 5000
```
将资源自带的证书替换成刚刚生成的：
```
\cp rootCA.pem assets/client/tls/ngrokroot.crt -f
\cp device.crt assets/server/tls/snakeoil.crt  -f
\cp device.key assets/server/tls/snakeoil.key -f
```
###### 4.打包
服务端：`make release-server` ,生成的文件ngrokd就是我们需要的服务端文件。
客户端(Mac):  `GOOS=darwin GOARCH=amd64 make release-client`, ngrok就是我们需要的客户端文件。
其他平台:
```
Linux 平台 32 位系统：GOOS=linux GOARCH=386
Linux 平台 64 位系统：GOOS=linux GOARCH=amd64
Windows 平台 32 位系统：GOOS=windows GOARCH=386
Windows 平台 64 位系统：GOOS=windows GOARCH=amd64
MAC 平台 32 位系统：GOOS=darwin GOARCH=386
MAC 平台 64 位系统：GOOS=darwin GOARCH=amd64
ARM 平台：GOOS=linux GOARCH=arm
```

###### 5.配置运行
服务端:**tunnelAddr 是通道的端口号，这个端口是Ngrok用来通信的，所以这个端口在服务器上和客户端上设置必须要对应才可以正常的链接，默认不填写好像是4433**
```
#http:
NGROK_DOMAIN="yeli.photo"
bin/ngrokd -domain="$NGROK_DOMAIN" -httpAddr=“:8100" -httpsAddr=“:8101" -tunnelAddr=":8102"
#https设置了tls:
bin/ngrokd -domain="$NGROK_DOMAIN" -httpAddr=":8100" -httpsAddr=":8101" -tunnelAddr=":8102" -tlsKey=./device.key -tlsCrt=./device.crt
```
因为没有配https,所以就参考http的就行.完成之后在浏览器输入: yeli.photo:8100,便可以得到:
>Tunnel yeli.photo:8100 not found

服务器配置成功,接下来配置客户端
将打包好的ngrok文件scp到mac,  直接扔进 bin目录 或者你随便放哪里,再建一个链接到bin目录也行,那样就可以直接使用ngrok 命令,不然就是: command not found .
新建配置文件ngrok.cfg 内容：
```
server_addr: "yeli.photo:8102” #端口号务必于服务器配置的 -tunnelAddr=“:8102” 保持一致！！！
trust_host_root_certs: false
```
执行:`ngrok -proto=http -subdomain=ngrok -config=/Users/yetongxue/ngrok_client/ngrok.cfg 8009`,成功启动ngrok客户端

**备注: 8009端口是你本地服务的端口**

![](http://upload-images.jianshu.io/upload_images/1271438-cfb6407d7b0a7182.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

访问ngrok管理界面:`http://127.0.0.1:4040`
![](http://upload-images.jianshu.io/upload_images/1271438-46c07330e8f74fc3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
###### **点击下面的链接就大功告成啦!**
***
###### 附: ngrok工作流程
http://ngrok.yeli.photo 请求首先访问服务器的8100端口, 这个端口是ngrok 在监听,收到消息通过ngrok 的服务端客户端链接端口8102,转发到mac 上面的ngrok ,收到消息再转发给本地端口8009.
##### 就这样子的
