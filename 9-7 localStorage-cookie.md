# 9-7 localStorage/cookie

标签（空格分隔）： ajax

---

localStorage
------------
全局对象
数据持久化，数据存在本地
每个域名下都有localStorage
不同域名不能共享，可以存5兆大小的数据
把网站一些不变的数据存储在localStorage中
可以存文件数据，css,js

对本地存储的操作，类似于操作数据库，类似于操作DOM
增删改查
添加内容：
    localStorage.setItem(key,value)
查找内容
    localStorage.getItem(key)
改：
    localStorage改key重新赋值
删：
    localStorage.removeItem(key)
    
localStorage存的是文本，如果存数组会转成字符串

**Storage事件：**
对Storage对象进行任何修改，添加删除修改数据的时候，都会在文档上触发Storage事件。当前页面不会触发此事件，同一域名同一端口的页面触发此事件；


cookie
------
http本身无状态
localStorage没出现之前，用cookie存储数据，cookie存储量太小，各浏览器不统一，几kb之间，不到1M;
cookie与域名有关系，必须同源才能拿到cookie；
cookie生命周期：
	只有会话时间，浏览器会话结束，就删除
session会话

设置cookie的过期时间
    转为UTC 世界标准时间
    let d=new Date()
    d.setDate(d.getDate()+5)
    'expires='+**d.toUTCString**;
    
    <script>
        //设置cookie
        
    
        function setCookie(key,value,n){
            if(n){
                let d=new Date();
                d.setDate(d.getDate()+n)
                document.cookie=key+'='+value+';expires='+d.toUTCString()
            }else{
                 document.cookie=key+'='+value;
            }
        }
        
        
        setCookie('miaov',123)
        setCookie('miaov2',1231,5)
        
        //获取cookie
        function getCookie(key){
            let cookies=document.cookie;
            cookies=cookies.split('; ')
            for(let i=0;i<cookies.length;i++){
               let arr=cookies[i].split('=')
               if(arr[0]==key){
                   return arr[1]
               }
            }
        }
        console.log(getCookie('miaov'))
        
        //删除cookie 把过期时间设置为过去
        function removeCookie(key){
            setCookie(key,null,-1)
        }
        removeCookie('miaov')
    </script>