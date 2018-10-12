## token验证实现
### 大体思路
~~~
APP登录界面输入用户信息登录；

服务端验证登录信息，验证成功，向APP端发送token，将token保存到数据库或者缓存服务器中；

APP登录成功后，每次调用后端API时都需要带着token、时间戳、sign（token+时间戳的md5字符串，sign可以自己定义算法以防止被盗用）信息，以便后台验证访问API权限；

后端在接收到APP访问请求时，比对APP发送来的token与缓存服务器中已经存在的token是否一致，并验证token时效性。
~~~

### 代码
~~~
<input type="text" name="username" id="username" value="" />
<label>密码</label>
<input type="password" name="password" id="password" value="" />
<input type="button" name="login" id="login" value="登录" />

<script type="text/javascript">
    document.getElementById("login").addEventListener('click',function () {
        //ajax提交验证信息到后端
        var username = document.getElementById("username").value;
        var password = document.getElementById("password").value;
        var data = "{\"username\":\"" + username +"\",\"password\":\"" + password + "\"}";
        var url = "/AppTest/loginServlet";
        var wd = "123";
        var headData = ["123","123456789012345","gsfgfgbdf"];
        postData(url,data, headData,function (backdata) {
            if(backdata != null){
                console.log("返回的信息为：  " + backdata);
            }
        },wd);
        
    });
</script>
~~~
### ajax方法
~~~
/*对ajax进行简易封装，便于每次调用，省去参数设置*/
function postData(url, data, headData, callback, waitingDialog) {
    mui.ajax(url,{  
        data:data,  
        dataType:'json',  
        type:'post',
        headers: {
            "token" : headData[0],
            "timesamp" : headData[1],
            "sign" : headData[2]
        },
        contentType:"application/x-www-form-urlencoded; charset=utf-8",  
        timeout:20000,  
        success:callback,
        error:function(xhr,type,errorThrown){  
            //waitingDialog.close();
            alert("<网络连接失败，请重新尝试一下>", "错误", "OK", null);  
        }  
    });
}  
~~~