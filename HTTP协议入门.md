##HTTP入门
###HTTP是一个应用层协议，由请求和响应构成，是一个标准的客户端服务器模型。HTTP是一个无状态的协议。
###工作流程
~~~
1）首先客户机与服务器需要建立连接。
2）建立连接后，客户机发送一个请求给服务器。
    格式为：统一资源标识符（URL）、协议版本号，后边是MIME信息包括请求修饰符、客户机信息和可能的内容。
3）服务器接到请求后，给予相应的响应信息。
    格式为一个状态行，包括信息的协议版本号、一个成功或错误的代码，后边是MIME信息包括服务器信息、实体信息和可能的内容。
4）客户端接收服务器所返回的信息通过浏览器显示在用户的显示屏上，然后客户机与服务器断开连接。
~~~
### 一个页面的xhr
~~~
General
Request URL:https://re.csdn.net/csdnbi  ---请求地址
Request Method:POST                     ---请求方法
Status Code:200 OK                      ---请求状态
Remote Address:117.122.217.19:443       ---远程地址
Referrer Policy:unsafe-url              ---Referrer，用以指定该请求是从哪个页面跳转页来的，常被用于分析用户来源等信息。

Response Headers
Access-Control-Allow-Credentials:true   ---表示是否可以将对请求的响应暴露给页面。

Access-Control-Allow-Headers:DNT,X-CustomHeader,Keep-Alive,User-Agent,X-Requested-With,If-Modified-Since,Cache-Control,Content-Type,body   
---用于 preflight request （预检请求）中，列出了将会在正式请求的 Access-Control-Expose-Headers 字段中出现的首部信息。

Access-Control-Allow-Methods:GET, POST, OPTIONS    ---明确了客户端所要访问的资源允许使用的方法或方法列表。

Access-Control-Allow-Origin:https://blog.csdn.net   ---指定了该响应的资源是否被允许与给定的origin共享。
Connection:keep-alive      ---这是版本的新特性：持久连接。因为每个TCP连接只能发送一个请求。需要客户端和服务器三次握手，并且开始时发送速率较慢（slow start）。
Date:Fri, 12 Oct 2018 02:00:24 GMT          ---消息生成的日期和时间。
Keep-Alive:timeout=20               
---允许消息发送者暗示连接的状态，还可以用来设置超时时长和最大请求数。
Server:openresty        ---包含了处理请求的源头服务器所用到的软件相关信息。
Transfer-Encoding:chunked         --- 表明回应将由数量未定的数据块组成。

Request Headers
Accept:*/*                              ---用来告知客户端可以处理的内容类型
Accept-Encoding:gzip, deflate, br       --- 说明自己可以接受哪些压缩方法。
Accept-Language:zh-CN,zh;q=0.8,en;q=0.6  --- 接受的语言
Connection:keep-alive               ---这是版本的新特性：持久连接。
Content-Length:1619                 ---声明本次回应的数据长度。
Content-Type:text/plain;charset=UTF-8       ---告诉客户端，数据是什么格式

Cookie:uuid_tt_dd=10_20045677580-1521035083287-324148; dc_session_id=10_1539132590087.627506; Hm_ct_6bcd52f51e9b3dce32bec4a3997715ac=1788*1*PC_VC; smidV2=20180527135934deb9428974a5c30a8544affe2f17ea8700fa19bedeaf6f5a0; dc_tos=pggqwl; Hm_lvt_6bcd52f51e9b3dce32bec4a3997715ac=1539241395,1539241570,1539306618,1539309622; Hm_lpvt_6bcd52f51e9b3dce32bec4a3997715ac=1539309622
----含有先前由服务器通过 Set-Cookie  首部投放并存储到客户端的 HTTP cookies。

Host:re.csdn.net        
---明了服务器的域名（对于虚拟主机来说），以及（可选的）服务器监听的TCP端口号。
Origin:https://blog.csdn.net    ---指示了请求来自于哪个站点。
Referer:https://blog.csdn.net/qq_28846087/article/details/79421902
---包含了当前请求页面的来源页面的地址，即表示当前页面是通过此来源页面里的链接进入的。
User-Agent:Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36
---包含了一个特征字符串，用来让网络协议的对端来识别发起请求的用户代理软件的应用类型、操作系统、软件开发商以及版本号。
~~~

### Host头域
~~~
Host头域指定请求资源的Intenet主机和端口号，必须表示请求url的原始服务器或网关的位置。
~~~

### 
~~~

~~~