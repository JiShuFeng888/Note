### 1.php文件上传限制修改

```php
注意:*

*1.上传文件一般使用POST提交*

*2.上传文件必须设置enctype="multipart/form-data"*

*3.上传的文件在PHP中可以通过$_FILES获取*

*4.PHP中文件默认会上传到一个临时目录, 接收完毕之后会自动删除*



*默认情况下服务器对上传文件的大小是有限制的, 如果想修改上传文件的限制可以修改php.ini文件*

*file_uploads = On  ; 是否允许上传文件 On/Off 默认是On*

*upload_max_filesize = 2048M    ; 上传文件的最大限制*

*post_max_size = 2048M       ; 通过Post提交的最多数据*



*max_execution_time = 30000   ; 脚本最长的执行时间 单位为秒*

*max_input_time = 30000     ; 接收提交的数据的时间限制 单位为秒*

*memory_li*
*mit = 2048M      ; 最大的内存消耗
```



### 2.Ajax原生JS封装

```javascript
<script>
    window.onload=function(){
        let oBtn=document.querySelector("button");
        oBtn.onclick=function(){
             ajax({
                 type:"POST",
                 url:"03-ajax-get.php",
                 timeout:3000,
                 data:{
                 "userName":"qwe",
                 "userPwd":123,
                 "李四":"牛逼"
                },
                success:function(xhr){
                console.log(xhr.responseText);},
                error:function(xhr) {
                alert("请求数据失败");
             }
             }
             )
        }
    }
</script>

<?php
// sleep(5);
echo $_POST["userName"]; 
?>

function objToStr(data){
     /*
    {
        "userName":"lnj",
        "userPwd":"123456",
        "t":"3712i9471329876498132"
    }
    */
    data = data || {}; // 如果没有传参, 为了添加随机因子,必须自己创建一个对象
    let url=[];
    data.t=new Date().getTime(); 
    for(let key in data){
        // 在URL中是不可以出现中文的, 如果出现了中文需要转码
        // 可以调用encodeURIComponent方法
        // URL中只可以出现字母/数字/下划线/ASCII码
        url.push(encodeURIComponent(key)+"="+encodeURIComponent(data[key]));
    }
    return url.join("&");
}
// type,url,data,timeout,success,error
function ajax(option){
        // 将对象转化为字符串
    let str=objToStr(option.data);
        //生成异步对象
    let xmlhttp;
    if (window.XMLHttpRequest)
    {   // code for IE7+, Firefox, Chrome, Opera, Safari
        xmlhttp=new XMLHttpRequest();
    }else{// code for IE6, IE5
        xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
    }
        // 2.设置请求方式和请求地址
        /*
        method：请求的类型；GET 或 POST
        url：文件在服务器上的位置
        async：true（异步）或 false（同步）
        */
    if(option.type==="GET"){
        xmlhttp.open(option.type,option.url+"?"+str,true);
        // 3.发送请求
        xmlhttp.send();
    }else{
        xmlhttp.open(option.type,option.url,true);
        // 注意以下代码必须放到open和send方法之间
        xmlhttp.setRequestHeader("Content-type","application/x-www-form-urlencoded");
        xmlhttp.send(str);
    }
        // 4.监听状态变化
    xmlhttp.onreadystatechange=function(){
        // 5.处理返回的结果
          /*
            0: 请求未初始化
            1: 服务器连接已建立
            2: 请求已接收
            3: 请求处理中
            4: 请求已完成，且响应已就绪
        */
        if(xmlhttp.readyState===4){
            clearInterval(timer);
        if(xmlhttp.status>=200&&xmlhttp.status<=300||xmlhttp.status===304){
        // console.log("接收到服务器返回的数据");
            option.success(xmlhttp);
        // responseText	获得字符串形式的响应数据。      
        // responseXML	获得 XML 形式的响应数据。
        }else{
            option.error(xmlhttp);
        }
    }
  };
    // 限定时间内不返回结果就终止请求
    // 注意以下代码存放的位置
    if(option.timeout){
        timer=setInterval(function(){
            console.log("中断请求");
            xmlhttp.abort();
            clearInterval(timer);
        },option.timeout);
    }
}
```

### 3.Ajax-XML格式

```javascript
    oButtons[0].onclick=function(){
                let self=this;
                ajax({
                     type:"GET",
                     url:"04-ajax-test.php",
                     timeout:3000,
                     data:{
                     "name":this.getAttribute("name"),
                    },
                    success:function(xhr){
                    // console.log(xhr.responseText);
                    // let arr=xhr.responseText.split("|");
                    // oTitle.innerHTML=arr[0];
                    // oDes.innerHTML=arr[1];
                    // oImg.setAttribute("src",arr[2]);
                    
                    let name=self.getAttribute("name");
                    let res=xhr.responseXML;
                    let title=res.querySelector(name+">title");
                    let des=res.querySelector(name+">des");
                    oTitle.innerHTML=title.innerHTML;
                    oDes.innerHTML=des.innerHTML;
                    
                    },
                    error:function(xhr) { 
                    alert("请求数据失败");
                 }
                 }
                 )
            }

	
  <?php
    header("content-type:text/xml;charset=utf-8");
	// 注意书写格式
    echo file_get_contents("info.xml");
	?>


<?xml version="1.0" encoding="utf-8" ?>
<product>
    <nz>
        <title>甜美啥来着</title>
        <des>人见人爱,花间花开,甜美系列</des>
    </nz>
    <bb>
        <title>奢华驴包</title>
        <des>送女友,送情人,送学妹,一送一个准系列</des>
    </bb>
</product>
```

### 4.Ajax-JSON格式

```javascript
{
    "nz":{
            "title":"甜美啥来着",
            "des":"人见人爱,花间花开,甜美系列"
    }
    
}

<?php
echo file_get_contents("04-ajax-json.txt");
?>

 success:function(xhr){   
      let name=self.getAttribute("name");
      let res=xhr.responseText;
      let obj=JSON.parse(res);
      // 注意格式
     oTitle.innerHTML=obj[name].title;
     oDes.innerHTML=obj[name].des;
},
```

### 5.Cookie介绍

```javascript
 /*
            cookie: 会话跟踪技术 客户端
            session:  会话跟踪技术  服务端

            cookie作用:
            将网页中的数据保存到浏览器中

            cookie生命周期:
            默认情况下生命周期是一次会话(浏览器被关闭)
            如果通过expires=设置了过期时间, 并且过期时间没有过期, 那么下次打开浏览器还是存在
            如果通过expires=设置了过期时间, 并且过期时间已经过期了,那么会立即删除保存的数据

            cookie注意点:
            cookie默认不会保存任何的数据
            cookie不能一次性保存多条数据, 要想保存多条数据,只能一条一条的设置
            cookie有大小和个数的限制
            个数限制: 20~50
            大小限制: 4KB左右

            cookie作用范围:
            同一个浏览器的同一个路径下访问
            如果在同一个浏览器中, 默认情况下下一级路径就可以访问
            如果在同一个浏览器中, 想让上一级目录也能访问保存的cookie, 那么需要添加一个path属性才可以;
            document.cookie = "name=zs;path=/;";

            例如:
            保存到了www.it666.com/jQuery/Ajax/路径下,
            我们想在 www.it666.com/jQuery/Ajax/13-weibo/,
            和 www.it666.com/jQuery/ 路径下也能访问

            例如:
            我们在www.it666.com下面保存了一个cookie,
            那么我们在edu.it666.com中是无法访问的
            如果想在edu.it666.com中也能访问, 那么我们需要再添加一个domain属性才可以;
            document.cookie = "name=zs;path=/;domain=it666.com;";
```

### 6.Cookie封装

```javascript
window.onload=function(){
            // addCookie("score",98,1,domain="128.0.0.1");
            function addCookie(key,value,day,path,domain){
                // １.处理默认保存路径
                let index=window.location.pathname.lastIndexOf("/");
                let currentPath=window.location.pathname.slice(0,index);
                path= path||currentPath;
                // ２.处理默认保存的domain;
                domain= domain||document.domain;
                if(!day){
                    document.cookie = key+"="+value+";path="+path+";domain="+domain+";";
                }else{
                    let date=new Date();
                    date.setDate(date.getDate()+day);
                    document.cookie = key+"="+value+";expires="+date.toGMTString()+";path="+path+";domain="+domain+";";
                }
            }
            
            function getCookie(key) {
                // console.log(document.cookie);
                var res = document.cookie.split(";");
                // console.log(res);
                for(var i = 0; i < res.length; i++){
                    // console.log(res[i]);
                    var temp = res[i].split("=");
                    // console.log(temp);
                    if(temp[0].trim() === key){
                        return temp[1];
                    }
                }
            }
            console.log(getCookie("name"));

            // 默认情况下只能删除默认路径中保存的cookie, 如果想删除指定路径保存的cookie, 那么必须在删除的时候指定路径才可以
            function delCookie(key, path) {
                addCookie(key, getCookie(key), -1, path);
            }
            delCookie("score");
	}
```

