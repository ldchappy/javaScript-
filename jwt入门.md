##jwt
###跨域认证
####一般流程
~~~
1、用户向服务器发送用户名和密码。
2、服务器验证通过后，在当前对话（session）里面保存相关数据，比如用户角色、登录时间等等。
3、服务器向用户返回一个 session_id，写入用户的 Cookie。
4、用户随后的每一次请求，都会通过 Cookie，将 session_id 传回服务器。
5、服务器收到 session_id，找到前期保存的数据，由此得知用户的身份。
~~~

问题：服务器集群，或者是跨域的服务导向架构，就要求 session 数据共享，每台服务器都能够读取 session。上面的就不好弄了
解决：
一种解决方案是 session 数据持久化，写入数据库或别的持久层。
另一种方案是服务器不保存 session 数据了，所有数据都保存在客户端，每次请求都发回服务器。JWT 就是这种方案的一个代表。

###JWT 的原理
~~~
服务器认证以后，生成一个 JSON 对象，发回给用户。
{
  "姓名": "张三",
  "角色": "管理员",
  "到期时间": "2018年7月1日0点0分"
}
以后，用户与服务端通信的时候，都要发回这个 JSON 对象。服务器完全只靠这个对象认定用户身份。为了防止用户篡改数据，服务器在生成这个对象的时候，会加上签名
~~~

###JWT 的数据结构
~~~
它是一个很长的字符串，中间用点（.）分隔成三个部分。注意，JWT 内部是没有换行的
wlkfjwewflajlfjWKFJJDL.QWLKFASJdsjalfjASDFalsdjflj7739847.aslkdjsjdlfASLKDASD
JWT 的三个部分依次如下：
Header（头部）
Payload（负载）
Signature（签名）
~~~

###Header 部分是一个 JSON 对象，描述 JWT 的元数据
~~~
{
  "alg": "HS256",
  "typ": "JWT"
}
alg属性表示签名的算法（algorithm），默认是 HMAC SHA256（写成 HS256）；typ属性表示这个令牌（token）的类型（type），JWT 令牌统一写为JWT。

最后，将上面的 JSON 对象使用 Base64URL 算法（详见后文）转成字符串。
~~~

###Payload 部分也是一个 JSON 对象，用来存放实际需要传递的数据。
~~~
除了官方字段，你还可以在这个部分定义私有字段，下面就是一个例子。
{
  "sub": "1234567890",
  "name": "John Doe",
  "admin": true
}
注意，JWT 默认是不加密的，任何人都可以读到，所以不要把秘密信息放在这个部分。
这个 JSON 对象也要使用 Base64URL 算法转成字符串。
~~~

###Signature 部分是对前两部分的签名，防止数据篡改。
~~~
首先，需要指定一个密钥（secret）。这个密钥只有服务器才知道，不能泄露给用户。然后，使用 Header 里面指定的签名算法（默认是 HMAC SHA256），按照下面的公式产生签名。

HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  secret)
算出签名以后，把 Header、Payload、Signature 三个部分拼成一个字符串，每个部分之间用"点"（.）分隔，就可以返回给用户。
~~~

###JWT 的使用方式
~~~
客户端收到服务器返回的 JWT，可以储存在 Cookie 里面，也可以储存在 localStorage。
此后，客户端每次与服务器通信，都要带上这个 JWT。你可以把它放在 Cookie 里面自动发送，但是这样不能跨域，所以更好的做法是放在 HTTP 请求的头信息Authorization字段里面。

Authorization: Bearer <token>
另一种做法是，跨域的时候，JWT 就放在 POST 请求的数据体里面。
~~~