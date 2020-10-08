# Cookie

## 简介

用于客户端与服务器交互数据的凭证，便于登录等操作

## 大小、数目限制

数目：30~无限制
大小：4k

## 格式

cookie 是一个有键值对组成的字符串（不是 JSON 格式）

## 获取非 HTTPonly 的 cookie

document.cookie
或者使用开发者工具

## cookie 的选项

1.expires GMT 格式，失效日期，如果没有设置则关闭会话时 cookie 消失

2.domain 与 path：域名和路径，但是当发生跨域 xhr 请求时，默认不添加 cookie 到请求头部

3.size：大小

4.secure：安全性，当请求时 https 或其他安全协议时，才会发送 cookie

5.httponly:设置 cookie 是否能通过 js 来访问和修改。

## cookie 的设置、读取、删除

1.服务器端

修改请求头部

2.客户端

设置
document.cookie=str;开发者需要自己完成 cookie 的 str 拼接

读取
const arr=document.cookie.split(';')开发者需要自行对 arr 进行数据提取

删除
setCookie(name,"1",-1);name 为要删除的 cookie 名字

##
