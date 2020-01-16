# 9-6 ajax

标签（空格分隔）： ajax

---

json
----

从后端响应的数据，流行的数据格式是json数据格式，是一个字符串，是json字符串。
官网：http://json.org/
JSON(JavaScript Object Notation) 是一种轻量级的数据交换格式

JSON格式的结构：

1. “名称/值”对的集合  '{"key":0,"key2":"string"}'
	key值必须写双引号、值是任意类型，不能是函数
2. 值的有序列表    '[ ]'
	值不能是函数

类似对象，但不是对象
JSON字符串 -> 可用的对象,专门用来处理JSON数据格式的

    let json = '{"username":"leo","age":30}';
	let obj = JSON.parse(json);
	console.log(obj);//把json字符串转为相应的对象

	let obj2 = {abc:1,miaov:'ketang'};
	let str = JSON.stringify(obj2);// 把对象转成json字符串
	console.log(typeof str);
    console.log(JSON.stringify(obj,null,1));
    //第三个参数为数字，代表有多少的空格，上限为10，若第三个参数为字符串，该字符串将作为空格；
 
    
请求返回的json数据：
console.log( JSON.parse(xhr.responseText) );
    
---------------------------
标准浏览器下：全局对象JSON 
低版本浏览器：https://github.com/douglascrockford/JSON-js  引入json2.js

JSON.parse(JSON字符串)

下载和上传
---------------------
js不能读取文件，只有服务器的语言才能读取


上传：
---

 1. 使用form表单做上传

    <form 
		action="http://localhost:8088/backend/post_file.php"
		method="post"
		enctype="multipart/form-data"
	>
		<input type="file" name="file">
		<input type="submit" value="上传" />
	</form>
上传的时候，会把读到的文件转成二进制的，form表单设置一个enctype="multipart/form-data"

 2. ajax
 找到要上传的文件，把文件转成二进制的
元素.files属性；
高版本浏览器formData():
可以异步上传二进制文件；
创建空的formData对象，使用append（）方法向该对象添加字段，send()方法把数据发送出去；

    	<body>
    		<input type="file" id="inputFile" name="file">
    		<input type="button" id="btn" value="上传" />
    		<div id="box">
    			<p id="text">0%</p>
    			<div id="bar"></div>
    		</div>
    		<script>
    			btn.onclick  =function (){
    				// 上传
    				let xhr = new XMLHttpRequest();
    
    				xhr.open(
    					'post',
    					'http://192.168.2.53:3000/miaov/2017-09-05/backend/post_file.php',
    					true
    				);
    
    				// 监控上传进度
    				xhr.upload.onprogress = function (ev){
    					console.log(ev.loaded); // 上传大小	
    					console.log(ev.total); //  总大小	
    					console.log(Math.round(ev.loaded/ev.total*100)+'%');
    
    					let scale = ev.loaded/ev.total;
    
    					text.innerHTML = Math.round(ev.loaded/ev.total*100)+'%';
    					bar.style.width = scale * 500 + 'px';
    
    				}
    
    
    				xhr.onload = function (){
    					console.log(xhr.responseText);	
    				};
    
    				// 找到要上传的文件，把文件转成二进制的
    
    				console.log(inputFile.value);  // 图片所在的地址
    				// 真正上传的资源，放在元素的files属性中
    				console.dir(inputFile.files[0]);
    
    				// 高版本浏览器 FormData
    
    				let f = new FormData();
    				f.append('file',inputFile.files[0]);
    
    				xhr.send(f);
    
    			};
    		</script>
    		
    	</body>
    </html>

修改上传大小
---------------------
wamp\bin\apache\Apache2.2.21\bin\php.ini

upload_max_filesize 			上传大小
post_max_size 					post发送的数据







