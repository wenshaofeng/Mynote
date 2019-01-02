###基本格式
```
//1、创建XMLHttpRequest这个对象,这个步骤中需要注意兼容处理
    var xhr = new XMLHttpRequest()
    //var xhr;
  if(window.XMLHttpRequest){
      xhr = new XMLHttpRequest();
  }else{
      xhr = new ActiveXObject('Microsoft.XMLHTTP');
  }

//2、准备发送
      xhr.open("post","checkUsername.php",true);
     //xhr.open("get","checkUsername.php?username=" + username,true);
	//xhr.send(null);
//3、执行发送
    var param = "username=" + username;
//对于post请求来说的话，我们的参数应该放到请求体中
//设置xhr的请求头信息，这个步骤仅仅是针对于post请求才有的
	xhr.setRequestHeader("Content-type","application/x-www-form-urlencoded");
	xhr.send(param);
//4、设置回调函数
	xhr.onreadystatechange = function(){
		if(xhr.readyState == 4) {
			if(xhr.status == 200) {
				//得到数据
					//xhr.responseXML
		              var result = xhr.responseText;
					console.log(result);
					document.getElementById("result").innerText = result;
						}
					}
					
				}
```
- get 发送数据在 xhr.open('post','testlog.php?name='+this.value);

- post 发送数据在 xhr.send()中;
**格式：**
> //设置请求行
                xhr.open("post", "url", true);
                //设置请求头
                xhr.setRequestHeader("Content-type", "application/x-www-form-urlencoded");
                xhr.send('name=xxx&name2=xxx');

- 发送ajax请求时，如果参数是a=1&b=2格式，发送的是Form Data，此时contentType是application/x-www-form-urlencoded。
- 如果参数是字符串(json)，那么发送的是Request payload，contentType是application/json。
发送的参数决定是form data还是request payload。contentType和参数不一致，则以参数为准。
####Form Data
![](https://upload-images.jianshu.io/upload_images/9249356-d45388c07f797fec.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
####JSON
![](https://upload-images.jianshu.io/upload_images/9249356-dbbad4706b58bf65.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

发送了一个post请求，在后台\$_POST都获取不到数据时，
.研究完参数 发现参数是通过payload方式传递的
 \$request_body = file_get_contents('php://input');
    \$data = json_decode($request_body, true);
[图片上传中...(image.png-f68158-1540477724012-0)]

###readyState属性
![](https://upload-images.jianshu.io/upload_images/9249356-e4ef4d8a54167173.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###同步异步
![](https://upload-images.jianshu.io/upload_images/9249356-0caf063afeeb34db.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**一定在发送请求 send() 之前注册 readystatechange （不管同步或者异步）**
为了让这个事件可以更加可靠（一定触发），一定是先注册，否则事件里的函数不会执行

####超时
  >  XHR对象的timeout属性等于一个整数，表示多少毫秒后，如果请求仍然没有得到结果，就会自动终止。该属性默认等于0，表示没有时间限制
　　如果请求超时，将触发ontimeout事件
　　[注意]IE8-浏览器不支持该属性
```
xhr.open('post','test.php',true);
xhr.ontimeout = function(){
    console.log('The request timed out.');
}
xhr.timeout = 1000;
xhr.send();
```

