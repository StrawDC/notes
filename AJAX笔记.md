---
title: AJAX学习记录
tags:
  - 学习
index_img: 'https://image.dcaoao.com/image/202212161928660.png'
abbrlink: 3210918941
date: 2022-12-11 20:00:00
---

# AJAX的优点:
    可以无需刷新页面与服务端进行通信
    允许根据用户事件来更新部分页面内容

# AJAX的缺点:
    没有浏览历史,无法回退
    存在跨域问题 (a.com向b.com发送请求 不被允许) 可以解决
    对SEO不友好


# http 超文本传输协议 
规定了浏览器与万维网服务器之间的通信规则
## 请求报文:
分为
请求行 ```GET /video/BV1WC4y1b78y?p=5& HTTP/1.1```
请求头 
 ``` 
:authority: api.vc.bilibili.com
            :method: GET
            :path: /dynamic_svr/v1/dynamic_svr/web_homepage?alltype_offset=0&video_offset=738044689246060700&article_offset=0
            :scheme: https 
```
空行
请求体
```
如果是GET请求,请求体为空 ,如果是POST请求,请求体可以不为空   spm_id_from=pageDriver&vd_source=00960caa5adc68e8bc3f39732ee0e72d
```

![](https://image.dcaoao.com/image/202212102331156.png)
![](https://image.dcaoao.com/image/202212102333845.png)


## 响应报文

响应行:   
     HTTP/1.1   200 ok     //200是响应状态码 同理还有 404  403 401 500 200   ok与响应状态码同步
响应头:    
    content-type: application/json
    cross-origin-resource-policy: cross-origin    等,与请求头一致
空行

响应体 :  HTML结构  服务端返回的结果等 
``` ```
![](https://image.dcaoao.com/image/202212102332671.png)


# AJAX发送GET请求

```
    btnget.addEventListener('click',function(){
        // 1.创建对象
        var xhr = new XMLHttpRequest()
        // 2.初始化 设置请求方法和URL
        xhr.open('GET','http://127.0.0.1:3000/server?a=100&b=200')
        // 3.发送
        xhr.send()
        // 4.事件绑定
        // on when  当...的时候
        // readyState   是xhr中的属性 表示状态 0 1 2 3 4     4代表服务器完全响应  3代表部分响应
        // change 发生了改变

        xhr.onreadystatechange = function() {
            if(xhr.readyState === 4) {  //当服务器完全响应
                if(xhr.status >= 200 && xhr.status < 300) {   //判断响应码 介于200-300之间的都是正常返回
                    divget.innerHTML = xhr.response  //修改标签内容
                }
            }
        }
    })
```
![](https://image.dcaoao.com/image/202212112103726.png)

```
console.log(xhr.status)     //返回状态码
console.log(xhr.statusText) //返回状态字符串
console.log(xhr.getAllResponseHeaders())      //返回所有响应头
console.log(xhr.response)   //返回响应体
```
![](https://image.dcaoao.com/image/202212112057483.png)

# AJAX 发起POST请求

```
  //设置点击事件
    bthpost.addEventListener('click',function(){
        //1.创建对象
        var xhr = new XMLHttpRequest()
        // 1.1 设置响应体数据的类型为json
        xhr.responseType = 'json'
        // 2.初始化
        xhr.open('POST','http://127.0.0.1:3000/json')

        // 2.2 设置请求头 xhr.setRequestHeader('请求头'，'请求头内容')
        xhr.setRequestHeader('Content-Type','application/x-www-form-urlencoded')
        // 3.发送,设置POST的请求体
        xhr.send('a=100&b=200')
        // 4.事件绑定
        xhr.onreadystatechange = function() {
            if(xhr.readyState === 4) {
                if (xhr.status >= 200 && xhr.status <300) {

                    /* 
                    //手动将服务器发送过来的字符串转换为JSON格式
                    let data = JSON.parse(xhr.response)
                    console.log(data)
                    div.innerHTML = data.age
                     */

                     console.log(xhr.response)
                    div.innerHTML = xhr.response.name
                }
            }
        }
    })
```
![](https://image.dcaoao.com/image/202212112102611.png)![](https://image.dcaoao.com/image/202212112102294.png)

其中,如果服务端发送过来的是字符串形式的数据,需要将其转换为JSON格式
```
//手动将服务器发送过来的字符串转换为JSON格式
let data = JSON.parse(xhr.response)
```

当然,也有自动的方法,可以将数据自动转换为JSON格式
```
xhr.responseType = 'json'
```
![](https://image.dcaoao.com/image/202212112102460.png)

设置请求头 `xhr.setRequestHeader('请求头'，'请求头内容')`
```
xhr.setRequestHeader('Content-Type','application/x-www-form-urlencoded')
```
![](https://image.dcaoao.com/image/202212112101762.png)


# 解决IE缓存问题

IE浏览器的AJAX请求,容易被缓存,使页面无法获取到服务器返回的最新数据
解决方法为使请求链接不停变化,使浏览器认为这是一个新的链接请求,则就不会缓存数据
每一次都是不同的链接,跟随时间戳
```
 xhr.open('POST','http://127.0.0.1:3000/ie?t=' + Date.now())     //核心点 在请求后面加上时间戳 这样每次都是不同的时间来进行请求，IE也不会缓存

```
![](https://image.dcaoao.com/image/202212112108554.png)


# 延时响应

使请求设置超时响应与断网响应,如果超出预订的时间,则按照事先写好的提示进行操作,这里服务端设置了3秒后进行响应
```
    //设置点击事件
    bthpost.addEventListener('click',function(){
        //1.创建对象
        var xhr = new XMLHttpRequest()
        // 2.初始化
        xhr.open('POST','http://127.0.0.1:3000/yanshi')     

        // 2.2 设置请求头
        xhr.setRequestHeader('Content-Type','application/x-www-form-urlencoded')
        // 3.发送,设置POST的请求体
        xhr.send('a=100&b=200')


        // 设置超时后的响应
        xhr.timeout = 2000  //设定事件2S
        xhr.ontimeout = function(){   //超时后执行的函数
            alert('链接超时')
        }
        //关于网络异常的回调函数
        xhr.onerror = function() {
            alert('网络链接失败')
        }

        // 4.事件绑定
        xhr.onreadystatechange = function() {
            if(xhr.readyState === 4) {
                if (xhr.status >= 200 && xhr.status <300) {
                     console.log(xhr.response)
                    div.innerHTML = xhr.response
                }
            }
        }
    })
```
![](https://image.dcaoao.com/image/202212112112176.gif)

# 取消请求
`abort()`用于取消AJAX的请求
```
   // 发送请求按钮
    btns[0].onclick = function() {
        x = new XMLHttpRequest()
        x.open('GET','http://127.0.0.1:3000/quxiao')
        x.send()
    }

    // 取消发送按钮
    btns[1].addEventListener('click',function(){
        x.abort()
    })
```
![](https://image.dcaoao.com/image/202212112116001.gif)

## 取消请求扩展 重复请求
如果用户多次重复请求,则会造成服务器压力过大
核心思想: 单独标识一个变量,如果其状态为未发送状态,则提交发送请求,变更状态为发送中
如果再次请求发送,检测其状态,如果是发送中,则取消上一次的请求,新提交一个请求
请求结果返回后,将其状态变更为未发送

```
    var btns = document.querySelectorAll('button')
    let x = null
    // 标识变量
    let onlist = false  //是否正在发送AJAX请求

    // 发送请求按钮
    btns[0].onclick = function () {
        if(onlist) {x.abort()}
        x = new XMLHttpRequest()
        onlist = true;  //修改标识变量为发送中
        x.open('GET', 'http://127.0.0.1:3000/quxiao');
        x.send();
        x.onreadystatechange = function () {
            if (x.readyState === 4) {
                onlist = false
                console.log(onlist)
            }
        }
    }
```


# axios请求
官网链接: https://www.axios-http.cn/docs/intro

Axios 是一个基于 promise 网络请求库，作用于node.js 和浏览器中。 它是 isomorphic 的(即同一套代码可以运行在浏览器和node.js中)。在服务端它使用原生 node.js http 模块, 而在客户端 (浏览端) 则使用 XMLHttpRequests。

JS调用
```
<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
```

## axios发送GET请求
```
    //axios发送GET请求
    btn[0].addEventListener('click',function(){
        axios.get('/api/getbooks',{
            // URL参数
            params:{id:1},
            // 请求头参数
            // headers:{name:1,name2:2}
        })
    })
```
![](https://image.dcaoao.com/image/202212161909552.png)

## axios发送POST请求
```
    btn[1].addEventListener('click',function(){
        console.log(123)
        axios.post('http://www.liulongbin.top:3006/api/addbook',{
           //请求体
           bookname:'牛鼻',
           author:'作者' ,
           publisher:'牛啊出版社'
        },{
            // 设置URL参数
            params:{id:1},
            // 设置请求头
            // headers:{}
        })
    })
```
![](https://image.dcaoao.com/image/202212161910167.png)![](https://image.dcaoao.com/image/202212161911426.png)

## axios发送请求
```
    btn[2].addEventListener('click',function(){
        axios({
            // 请求方法
            method:'POST',
            // URL
            url:'http://www.liulongbin.top:3006/api/addbook',
            // URL参数
            // params:{a:100,b:200},
            // 头信息
            Headers:{
                nb666:66666
            },
            // 请求体
            data:{
                bookname:new Date(),
                author:'作者',
                publisher:'牛啊出版社'

            }
        })
    })
```

# fetch发送AJAX请求

```
    var btn = document.querySelector('button')
    btn.addEventListener('click',function(){
        // fetch发送
        fetch('http://www.liulongbin.top:3006/api/addbook',{
            // 请求方法
            method:'POST',
            // 请求头
            headers:{name:666},
            // 请求体
            body:'bookname:牛鼻'
            // 回调函数
        }).then(Response => {
            return Response.json()  //将返回结果输出并转换为JSON格式
        }).then(Response => {
            console.log(Response)
        })
    })
```
![](https://image.dcaoao.com/image/202212161914928.png)![](https://image.dcaoao.com/image/202212161914765.png)


# 设置CORS响应头实现跨域

CORS响应头需要服务端设置,前端无需任何操作
```
//CORS响应头跨域
app.all('/CORS', (req, res) => {
    res.setHeader('Access-Control-Allow-Origin', '*')
    // 设置响应体
    res.send('你好! CORS')
})

app.listen(port, () => {
    console.log(`服务已经在 ${port}端口处运行`)
})
```

然后`node server.js`