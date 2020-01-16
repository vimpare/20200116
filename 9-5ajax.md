# ajax  

标签（空格分隔）： ajax

---
异步javascript和xml
无需刷新页面就可以从服务器获取数据
ajax的请求和响应是需要时间
        如果写成异步的，无论ajax回来没回来，先执行ajax以下的代码
        如果写成同步的，等ajax回来之后，才能执行后面的代码
        
        同步
          在执行某个请求的时候，若该请求需要一段时间才能返回信息，那么这个执行将会一直等待下去，直到收到返回信息才继续执行下去

        异步
          
          不需要一直等下去，而是继续执行下面的操作，不管其他执行的状态。当有消息返回时系统会进行通知处理，这样可以提高执行的效率。


          jq的ajax有一个参数
            {
              async:true,  异步  false 同步
            }
NS:DNS（Domain Name System，域名系统），因特网上作为域名和IP地址相互映射的一个分布式数据库，能够使用户更方便的访问互联网，而不用去记住能够被机器直接读取的IP数串
当在浏览器打开html页面，浏览器有内核会把html解析并渲染（显示）网页，不是看的一堆的文本
get和post的区别
--------------------------------------------------
，讨论的范围的是浏览器 

**get 方式**
	http://192.168.2.53:3000/miaov/2017-09-05/backend/php/get.php?user='+username.value
	发送数据的方式
		在地址栏中?的后面，就是查询信息
			key=value&lkey2=value2&key3=value3 成为为queryString
	浏览器对地址有长度有限制
		所以get的数据会有限制
	不安全，发送一些无关紧要的
		浏览器好缓存地址

**post方式**
	http://192.168.2.53:3000/miaov/2017-09-05/backend/php/post.php
	发送数据的方式
		放在HTTP的请求body（主体）发送的
	理论上没有大小限制
		服务端会有限制
	理论上是安全的



设置请求头
-----

：

    xhr.setRequestHeader( 'Content-Type',
    			'application/x-www-form-urlencoded');


--------------------------------------------------------------

http://www.baidu.com/index.html

请求 request
-------------------------
post 119.75.213.61:443 1.1.1  请求行

cookie:                              请求信息、消息
Connection:Keep-Alive
Content-Encoding:gzip

body                                请求数据 主体


响应 response
---------------------------------
每个http请求和响应都会带有相应的头部信息，xhr对象提供了操作头部信息的方法；
setRequestHeader()设置自定义请求头部信息，两个参数，头部字段名称和头部字段的值；
getResponseHeader()传入头部字段名称，会取得对应的头部信息的长字符串；
getAllResponseHeader()返回多行文本
1.1.1 200 ok

cookie:                              响应信息、消息
Connection:Keep-Alive
Content-Encoding:gzip

body 主体

二进制的 文本
<百度的index.html的页面>

----------------------------
同步
	在执行某个请求的时候，若该请求需要一段时间才能返回信息，那么这个执行将会一直等待下去，直到收到返回信息才继续执行下去

异步
	不需要一直等下去，而是继续执行下面的操作，不管其他执行的状态。当有消息返回时系统会进行通知处理，这样可以提高执行的效率。





ajax工作流程
----------------------
ajax readystate五种状态：
初始化，未发送			**0**	UNSENT 
准备数据，连接地址		**1**	OPENED
返回响应头				**2**	HEADERS_RECEIVED   未返回内容，只返回了响应头
接收数据中				**3**	LOADING            返回内容，数据量大，分批返回
接收数据完毕			**4**	DONE               数据完全接受完成

只要readystate属性的值由一个值变成另一个值，都会触发readystatechange事件；

     var xhr = createXHR();        
        xhr.onreadystatechange = function(event){
            if (xhr.readyState == 4){
                if ((xhr.status >= 200 && xhr.status < 300) || xhr.status == 304){
                    alert(xhr.responseText);
                } else {
                    alert("Request was unsuccessful: " + xhr.status);
                }
            }
        };
        xhr.open("get", "example.txt", true);
        xhr.send(null);
此为高程设计例子，其中onreadystatechange事件处理程序中使用了xhr对象，没有使用this，原因是作用域问题，this在有的浏览器中会执行失败
只要触发onload，ajax的步骤已经进行到了第五步，也就是xhr.readyState = 4；
只要浏览器接收到服务器的响应，不管状态如何，都会出发onload事件，所以必须检查status属性，才能确定数据是否真的已经可用了；
**2 open 连接地址，准好数据**
	参数：
		1. 请求方式 get|post 不区分大小写
		2. 发送的地址
		3. 是否异步 true异步 false 同步
会启动一个.php的get请求，并不会真正发送请求，只是启动一个请求以备发送
要发送特定的请求，必须调用send方法，send方法接收参数，为作为请求主体发送的参数。
xhr相关属性：
responseText 作为响应主体被返回的文本。
statu 相应的http状态
statusText  http状态的说明
**3 send 发送**
**4 响应触发的事件**

**

enctype
-------

** enctype 属性规定在发送到服务器之前应该如何对表单数据进行编码。它有三个值，
	默认：**application/x-www-form-urlencoded**，表单数据被编码为名称/值对。在使用get方式提交时，把表单数据加到url后，以？分割。使用post 方式提交，把表单数据放在请求体中传输。
	**multipart/form-data**用来指定传输数据的特殊类型的，主要指上传的非文本内容，图片或MP3；
	**text/plain** 纯文本传输

状态码：
----
当浏览者访问一个网页时，浏览者的浏览器会向网页所在服务器发出请求。当浏览器接收并显示网页前，此网页所在服务器会返回一个包含http状态吗的信息头以相应浏览器的请求。
常见：
200 请求成功
301 资源被永久转移的其他url
404 请求的资源不存在
500 内部服务器错误
	https://baike.baidu.com/item/HTTP%E7%8A%B6%E6%80%81%E7%A0%81/5053660?fr=aladdin

200 ok 
304 Not Modified
404 Not found
502 Bad Gateway			
				
				
    <!DOCTYPE html>
    <html lang="en">
        <head>
            <title></title>
            <meta charset="UTF-8">
            <meta name="viewport" content="width=device-width, initial-scale=1">
            <!-- <link href="css/style.css" rel="stylesheet"> -->
        </head>
        <body>
        <h2>注册get-ajax</h2>
    			用户名：<input type="text" name="user" id="username" /><span id="tip"></span>
    			<br/>
    			密码：<input type="password" name="password" /><br/>
                <input type="submit" id="send" value="提交">
                <script>
                    send.onclick=function(){
                        let a=new XMLHttpRequest();
                        console.log(a)
                        a.open(
                            'post',
                            'http://192.168.2.53:3000/miaov/2017-09-05/backend/php/post.php',
                            true
                        )
                        a.onload=function(){
                            console.log(a.responseText)
                            tip.innerHTML=a.responseText;
                        }
                        a.setRequestHeader('content-Type','application/x-www-form-urlencoded')
                        a.send('user='+username.value)
                    }
                </script>
        </body>
    </html>

ajax封装函数
--------

    function ajax(options){
			let defaults =  Object.assign({
				url:'',
				method: 'get',
				data:''
			},options);

			if(defaults.url === ''){
				// 抛出错误
				throw new Error("地址不能为空")
			}

			let xhr = new XMLHttpRequest();

			// 是get请求要把data放在地址后面
			if(defaults.method.toLowerCase() === 'get'){
				defaults.url = defaults.url + '?'+defaults.data;
			}

			xhr.open(defaults.method,defaults.url,true);

			xhr.onload = function (){
				console.log(xhr.responseText);	
			};

			if(defaults.method.toLowerCase() === "get"){
				xhr.send();
			}else if(defaults.method.toLowerCase() === "post"){
				xhr.setRequestHeader( 'Content-Type',
			'application/x-www-form-urlencoded');
				xhr.send(defaults.data);

			}
		}