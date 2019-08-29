# HTTP 介绍

## HTTP 概念
HTTP (HyperText Transfer Protocal) ,超文本传输协议。

## HTTP 原理
当我们在浏览器地址栏中输入一段地址后回车，一段时间后浏览器显示出页面，这背后发生了什么？
1、浏览器将输入的地址及请求参数拼装成 HTTP 请求报文，然后向服务器发起请求
2、服务器接收到请求之后处理请求，并返回响应报文
3、浏览器接收到响应报文后，处理，并由渲染引擎进行渲染

## URL 格式
如： http://api.qq.com/user/1
分为三部分：
1、协议类型             http：
2、服务器地址           //api.qq.com
3、路径                /user/1
其中，服务器地址的作用不是寻址目标主机的 IP，寻找 IP 是有 DNS (domain name system) 完成的，服务器地址仅用于找到目标主机后确认主机域名和端口

## HTTP 请求报文
包含三部分：
1、请求行
2、Headers
3、Body

其中请求行又包含以下部分：
1、method
2、path
3、HTTP Version

## HTTP 响应报文
包含三部分：
1、状态行
2、Headers
3、Body

其中 状态行又包含以下部分：
1、HTTP Version
2、状态码
3、状态信息
