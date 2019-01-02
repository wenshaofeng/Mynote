get 发送数据在 xhr.open('post','testlog.php?name='+this.value);
post 发送数据在 xhr.send()中;

如果需要像 HTML 表单那样 POST 数据，请使用 setRequestHeader() 来添加 HTTP 头。然后在 send() 方法中规定您希望发送的数据：xmlhttp.setRequestHeader("Content-type","application/x-www-form-urlencoded");

发送ajax请求时，如果参数是a=1&b=2格式，发送的是Form Data，此时contentType是application/x-www-form-urlencoded。如果参数是字符串(json)，那么发送的是Request payload，contentType是application/json。
发送的参数决定是form data还是request payload。contentType和参数不一致，则以参数为准。

发送了一个post请求，在后台\$_POST都获取不到数据时，
.研究完参数 发现参数是通过payload方式传递的
 \$request_body = file_get_contents('php://input');
    \$data = json_decode($request_body, true);
