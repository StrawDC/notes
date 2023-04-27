

![](https://image.dcaoao.com/image/202212292231924.png)

# 初识Vue
渐进式 JavaScript 框架

1.一个Vue实例只能接管一个容器，反之容器也只能被一个Vue实例接管，一对一的关系，容器内的内容被称为Vue模板
2.Vue实例内可以写JS表达式,比如 `Date.now()` 时间戳函数

JS表达式: 一个表达式会生成一个值,可以放在任何一个需要值的地方
            1. a
            2. a + b
            3. 函数()
            4. `x === y ? 'a' : 'b'`
        JS代码:语句
            1. if() {}
            2. for() {}

3.Vue要工作,必须要准备一个实例,一个容器,传入配置对象
4.一旦data中的数据发生改变,那么容器中用到该数据的地方会`自动更新`
5.{{xxx}}中的xxx要写js表达式,而且xxx可以自动读取到data中的所有属性 ` {{Vue.split(',')}} ` 比如将其转换为数组

```
    <!-- 为Vue准备一个容器 -->
    <div id="root">
        <h1>Hello, {{name}},{{Vue.split(',')}}</h1>    <!-- 插入Vue实例 也叫插值语法 -->
    </div>


    <script src="https://cdn.jsdelivr.net/npm/vue@2.7.14/dist/vue.js"></script>
    <script>
        Vue.config.productionTip = false  // 阻止 vue 在启动时生成生产提示。
    
    // 创建vue实例
    const x = new Vue({
        el:'#root',   // el用于执行当前vue实例为哪个容器服务，值通常为css选择器字符串 
        data:{
            name:'世界!,Vue!' , // data用于存储数据，对象形式，供el指定的容器使用
            Vue:'Vue,真好玩'
        }
    })
```

![](https://image.dcaoao.com/image/202212292237639.png)

# 模板语法

## Vue模板语法有两大类:
### 1.插值语法:
功能,用于解析标签体内容
写法: `{{xxx}}`  xxx是js表达式,且可以直接读取到data中的属性
### 2.指令语法:
功能,用于解析标签 标签属性,标签体内容 绑定事件....
举例: `v-bind:href="xxx"` 或者简写 `:href="xxx"`  xxx同样可以写js表达式,而且可以直接读取到`data中的所有属性`
扩展: Vue中有很多指令,而且形式都是 v-???

```
<body>
    <!-- 准备容器 -->
     <div class="root">
        <h1>插值语法</h1>
        <h1>你好,{{word}}</h1>
        <h1>你好,{{school.duo}}</h1>

        <h1>指令语法</h1>
        <a v-bind:href="url">点击去百度</a>
        <a :href="url">点击去百度-缩写</a>
        <a :href="school.url">点击去百度-缩写</a>
     </div>
     <script src="https://cdn.jsdelivr.net/npm/vue@2.7.14/dist/vue.js"></script>
     <script>
        new Vue({
            el:'.root',
            data:{
                word:'世界!',
                url:'https://www.baidu.com/',
                // 多结构语法
                school:{
                    url:'http://www.edu.cn',
                    duo:'这就是多结构'
                }
            }
        })
     </script>
</body>
```
![](https://image.dcaoao.com/image/202212292240552.png)


# 数据绑定
vue中有两种数据绑定的方式
    1.单向绑定,`(v-bind)` 数据只能从data流向页面
    2.双向绑定,`(v-model)` 数据不仅可以从data流向页面,还可以从页面流向data
    双向绑定一般用于表单元素上 比如input select等用于value属性的标签上
    `v-model:value`可以简写为v-model 因为其默认收集的就是value值 

## 普通写法
```
#单向数据绑定: <input type="text" v-bind:value="dan">
#单向数据绑定: <input type="text" v-model:value="shuang">
```
## 简写写法
```
#单向数据绑定: <input type="text" :value="dan">
#双向数据绑定: <input type="text" v-model="shuang">
```
```
<body>
    <!-- 准备容器 -->
    <div class="root">
    <!-- 简写写法 -->
    单向数据绑定: <input type="text" :value="dan"><br>
    双向数据绑定: <input type="text" v-model="shuang">
</div>
    <script>
        new Vue({
            el:'.root',
            data:{
                dan:'单向数据绑定',
                shuang:'双向数据绑定'
            }
        })
    </script>
</body>
```

![](https://image.dcaoao.com/image/202301011954466.gif)

<!-- 可以看到,单向数据绑定无法将新数据流向data,但是双向数据绑定可以 -->

# el与data的两种写法

## el有两种写法
1.new Vue时配置el对象
2.先创建vue实例，然后通过 x.$mount('.root') 指定el的值

## data有两种写法
1.对象式
2.函数式
目前哪种写法都可以,学习到组件时则必须使用函数式

重要事项
由vue管理的函数,一定不要写箭头函数,一旦书写了箭头函数,this不会指向vue,而是其他实例
## el的第一种写法
```
        const x = new Vue({
            el:'.root',    // el的第一种绑定方式
            data:{ 
                world:'世界!'
            }
        })
```
## el的第二种写法
```
x.$mount('.root')   // el的第二种绑定方式
```

## data的第一种写法
data的第一种写法 对象式
```
        const x = new Vue({
            el:'.root', 
            data:{   // data的第一种写法 对象式
                world:'世界!'
            }
        })
```

## data的第二种写法
 data的第二种写法 函数式
```
        const u = new Vue({
            el:'.root2', 
            data(){   // data的第二种写法 函数式
                return {
                    name:'你好世界世界世界'
                }
            }
        })
```

# 何为数据代理
数据代理,通过一个代理对象对另一个对象中的属性进行的操作(读/写)
Vue中的数据代理:
通过vm对象来代理data对象中属性的操作(读/写)
Vue中数据代理的好处:
更加方便的操作data中的数据
基本原理:
通过  `Object.defineProperty()` 把data对象中的所有属性添加到vm
为每一个添加上去的属性,都指定一个`getter/setter`
然后在getter/setter内部去操作(读/写)data中对应的属性
```
        // 创建两个对象
        let obj1 = {x:100,a:300}
        let obj2 = {y:200}

        Object.defineProperty(obj2,'x',{
            get(){
                console.log('有人访问了obj2中的 x 数据,在此返回了obj1的x值')
                return obj1.x
            },
            set(value){
                return '有人修改了obj1的x数据'
                obj1.x = value
            }
        })
```
![](https://image.dcaoao.com/image/202301012007794.gif)


# 事件的基本使用
## 事件的基本使用:
1.使用`v-on:xxx` 或者 `@xxx` 绑定事件,`xxx`是事件名 点击,经过,停留等...
2.事件的回调函数需要写在`methods`对象中,最终会在vm上
3.`methods`中配置的函数,其this指向vue实例,不要用箭头函数,否则this会被指向其他
4.`@click='demo' `和` @click="demo($event)"` 效果一致,但是后者可以传参
```
    <!-- 准备容器 -->
    <div class="root">
        <h1>你好,{{name}}</h1>
        <button @click="hanShu1">点击提示信息(不传参)</button>
        <button @click="hanShu2('传递参数')">点击提示信息(传参)</button>
    </div>
    <script>
        // 准备Vue实例
        const vm = new Vue({
            el:'.root',
            data:{
                name:"世界"
            },
            // 准备事件调用的函数 methods
            methods:{
                // 点击提示信息(不传参)
                hanShu1(){
                    alert('提示信息(不传参)')
                },
                // 点击提示信息(传参)
                hanShu2(a){
                    console.log(a)
                }
            }
        })
```
![](https://image.dcaoao.com/image/202301012011422.gif)

可以看到`@click="hanShu2('传递参数')"`传递的参数,hanShu2函数成功的接收到,并输出了出来

## 事件修饰符
@click.prevent
```
        <!-- prevent 阻止标签默认行为,等同与 e.preventDefault() -->
        <a href="http://BAIDU.COM" @click.prevent="showInof">点击提示信息</a>
```

@click.stop="showInof"
```
        <!-- 阻止事件冒泡  stop  等同于 e.stopPropagation() -->
        <div @click="showInof">
            <button @click.stop="showInof">阻止事件冒泡</button>
        </div>
```

@click.once="showInof"
```
        <!-- 事件只触发一次  once -->
        <button @click.once="showInof">事件只触发一次</button>
```

## 键盘事件

@click 鼠标点击
@scroll 滚动条滚动
@wheel 滚轮滚动
@keyup 键盘弹起触发
@keydown 键盘按下触发

## Vue中常用的按键别名
回车: enter
删除: delete  删除和退格键
退出: esc
空格: space
换行:tab   （特殊 需要配合 @keydown 使用）
上: up
下: down
左: left
右: right

Vue中未提供别名的按键, 可以使用按键原始的key值取绑定,但是需要转换,
比如 CapsLock 需要转换为caps-lock，驼峰全部小写，多个单词之间使用 - 链接  `console.log(e.key) `
## 系统修饰键(用法特殊): ctrl alt shift mata
1.配合`@keyup`使用: 按下修饰键的同时,再按下其他键,随后释放其他键,事件才被触发
2.配合 `@keydown`使用: 正常触发事件
3. `@keyup.down.ctrl.y ` 可以视为按下ctrl + y 触发,组合键

也可以使用keyCode去指定具体的按键,比如 `@keyup.down.13="show"`   13是回车的编码，也可以触发，但是编码以后可能会被弃用

`Vue.config.keyCode.自定义键名 = 键码`  可以定制按键别名
`Vue.config.keyCode.huiche = 13`     `@keyup.down.huiche="show"`   这样按下回车也可以触发事件

```
    <script src="https://cdn.jsdelivr.net/npm/vue@2.7.14/dist/vue.js"></script>

    <div class="root">
        <h2>欢迎来到{{name}}</h2>
        <input type="text" @keyup.down.enter="show">  // 按下回车
    </div>

    <script>
        const vm = new Vue({
            el:'.root',
            data:{
                name:'前端世界'
            },
            methods:{
                show(e){
                    console.log(e.key,e.keyCode)   // 获取按键原始key名以及键值
                    // console.log(e.target.value)
                }
            }
        })
```

# 使用 `methods`中的函数返回值进行插值语法

```
<script src="https://cdn.jsdelivr.net/npm/vue@2.7.14/dist/vue.js"></script>
<div class="root">
    姓 <input type="text" v-model:value="firstName"><br>
    名 <input type="text" v-model:value="lastName"><br>
    <!-- 模板使用methods函数返回值,必须加小括号调用 -->
    <span>{{firstLastName()}}</span>
    // 上方语法在methods处理,等同于下方
    <span>{{firstName}} - {{lastName}}</span>
</div>
    <script>
        const vm = new Vue ({
            el:'.root',
            data:{
                firstName:'张',
                lastName:'三',
            },
            methods:{
                firstLastName(){
                    // 可以直接使用return返回值到模板内
                    return this.firstName + '-' + this.lastName
                }
            }
        })
    </script>
```

模板使用`methods`函数返回值,必须加小括号调用
作用,是模板内更加简洁,方便观察

# 计算属性
计算属性:`computed`
1.定义 要用的属性不存在,需要已有的属性计算得来
2.原理 借助了 `Object.defineProperty` 方法提供的get和set
3.get函数什么时候执行?
当有人读取到 firstLastName 时 get就会被调用 返回值作为firstLastName的值
初次读取的时候  所依赖的数据发生变化
4.优势: 与`methods`相比,内部有`缓存`机制(可以复用),效率高,调试方便

5.备注 计算属性最终会出现在vm上,直接读取使用即可
如果计算属性需要被修改 那必须通过set函数去响应修改,而且set要引起计算时依赖的数据发生改变.
```
            const vm = new Vue ({
                el:'.root',
                data:{
                    firstName:'张',
                    lastName:'三',
                },
                // computed 计算属性
                computed:{
                    firstLastName:{
                        // get作用:当有人读取到 firstLastName 时 get就会被调用 返回值作为firstLastName的值
                        // get中的this,指向Vue vm实例 所以可以直接this.firstName 读取data中的属性
                        // get什么时候调用? 1.初次读取的时候 2.所依赖的数据发生变化
                        get(){
                            console.log('get被调用')
                            return this.firstName + '-' + this.lastName
                        },
                        // set作用:当firstLastName被修改,set就会被调用,而且接收被修改的参数
                            // 相同,其中的this与get一样,都被指向vue实例

                        set(value){
                            console.log('set被调用')
                            let arr = value.split('-')
                            this.firstName = arr[0]
                            this.lastName = arr[1]
                        }
                    }
                }
            })
```

get被调用,页面初次加载读取了data内的数据,其数据为firstLastName依赖数据,所以会被调用
![](https://image.dcaoao.com/image/202301012031481.png)


set被调用,修改了firstLastName的数据后,因为所依赖的数据发生变化,get也被调用了一次
![](https://image.dcaoao.com/image/202301012030218.png)

## 简写:  如果`computed`中的属性,只需要读取(get) 不需要修改(set) 可以进行简写模式
```
        computed:{
                    firstLastName(){
                            console.log('get被调用')
                            return this.firstName + '-' + this.lastName
                        },
                    }
                }
```

### 天气属性案例
```
    <script src="https://cdn.jsdelivr.net/npm/vue@2.7.14/dist/vue.js"></script>
    
    <div class="root">
        <h2>今天天气很{{info}}</h2>
        <button @click="chuan">切换天气</button>
    </div>
    <script>
        const vm = new Vue({
            el:'.root',
            data:{
                isHot:true
            },
            computed:{
                // info负责修改天气
                info(){
                    console.log(666)
                    return this.isHot ? '炎热' : '凉爽'
                }
            },
            methods:{
                chuan(){
                    this.isHot = !this.isHot
                    console.log(this.isHot)
                }
            }
        })
    </script>
```
![](https://image.dcaoao.com/image/202301012035640.gif)

可以看到 按钮负责调用 `chuan()`函数,修改`isHot`不停取反
`computed`内的`info()`,根据`isHot`的值按照三元表达式修改输出的值,然后通过插值语法渲染到页面中
`isHot`每修改一次,都会重新进行一次渲染,重新执行一次`info()`

# 监视属性`watch`
1.当监视的属性发生变化时,其内部的回调函数自动调用,进行相关操作
2.监视的属性必须存在,才能进行监视

 监视的两种方法
 (1) new Vue时传入watch配置
 (2) 通过vm.$watch('监视属性名',handler(){})

 ## new Vue时传入watch配置
 ```
         const vm = new Vue({
            el:'.root',
            data:{
                isHot:true
            },
            computed:{
                info(){
                    return this.isHot ? '炎热' : '凉爽'
                }
            },
            methods:{
                chuan(){
                    this.isHot = !this.isHot
                }
            },
            // 新的配置项 watch 监视属性变化,如果变化，可以返回变化前的值与变化后的值
            watch:{
                // 需要监视的属性名
                isHot:{
                    immediate:true,  // immediate作用，初始化时，调用一下handler，默认为false，不调用
                    // handler函数，固定写法
                    handler(newValue,oldValue){
                        console.log('isHot被修改了,新的值是' + newValue + '旧值是' + oldValue)
                    }
                },
                // 也可以监视 computed 中的属性
                info:{
                    immediate:true, 
                    handler(a,b){
                        console.log('info被修改了,新值是  '+  a + '  旧值是  ' + b)
                    }
                }
            }
        })
 ```

## 通过vm.$watch('监视属性名',handler(){})
```
        vm.$watch('isHot',{
            handler(newValue,oldValue){
                        console.log('isHot2被修改了,新的值是' + newValue + '旧值是' + oldValue)
            }
        })
```

immediate作用: 在初始化时,调用一下handler，默认为false，不调用


## 深度监视
深度监视
(1).Vue中的watch默认不监测对象内部值的改变(一层)
(2).配置`deep:true` 可以检测对象内部值的改变(多层)

Vue自身可以检测对象内部值的改变,但是Vue提供的watch默认不监测 
使用watch根据数据的具体结构,决定是否采用深度监视
```
 <!-- 仅修改其内部值,无法触发深度监视 除非 deep:true,  -->
<button @click="shendu.a++">深度监视-修改内部数据值,a的数据为{{shendu.a}}</button>
<!-- 修改整个数据的值会触发深度监视 -->
<button @click="shendu = {a:1,b:2}">修改整个数据的值会触发深度监视</button>
```
深度监视 deep为false时,仅修改watch内的值,不会触发深度监控:
![](https://image.dcaoao.com/image/202301022123973.gif)

深度监视 deep为true时,仅修改watch内的值,深度监控被触发:
![](https://image.dcaoao.com/image/202301022125189.gif)
```
                shendu:{
                    deep:true,   // deep 开启深度监视，这样修改其内部的任意一个值都会触发深度监视
                    handler(){
                        console.log('深度监视被触发')
                    }
                }
```


## watch 监视属性的简写
简写的代价就是,无法使用`immediate`,`deep`等方法了,而且不可写为箭头函数,否则this会指向window
### 配置项内正常写法
```
        watch:{
            isHot:{
                    immediate:true,
                    handler(newValue,oldValue){
                        console.log('isHot被修改了,新的值是' + newValue + '旧值是' + oldValue)
                    }
                }, 
            }
```
### 配置项内简写写法
```
            watch:{
                isHot(newValue,oldValue){
                    console.log('isHot被修改了,新的值是' + newValue + '旧值是' + oldValue)
                }
            }
```

### 配置项外正常写法
```
vm.$watch('isHot',{
            handler(newValue,oldValue){
                        console.log('isHot2被修改了,新的值是' + newValue + '旧值是' + oldValue)
            }
        })
```

### 配置项外简写写法
```
        vm.$watch('isHot',function(newValue,oldValue){
            console.log('isHot2被修改了,新的值是' + newValue + '旧值是' + oldValue)
        })
```


## computed与watch之间的区别
1.computed可以完成的功能,watch都可以完成
2.watch可以完成的功能,computed不一定能完成,比如watch可以进行异步操作 定时器等

被vue管理的函数,最好写成普通函数,这样this指向的是vm或者组件实例对象
所有不被vue管理的函数(定时器,ajax回调,promise回调)最好写成箭头函数,这样this指向才是vm或者组件对象

# 绑定样式

## class绑定样式
 原理其实就是v-bind来进行class样式的切换
 写法: `:class="xxx"`  xxx可以是字符串 对象 数组
 字符串写法适用于 类名不确定 需要动态获取
 对象写法适用于 要绑定多个样式,个数不确定,名字不确定
 数组写法适用于 要绑定多个样式 个数 名字不确定 需要动态决定是否启用

 ### 绑定class样式 字符串写法
适用于样式类名的不确定,需要动态指定 如果原先就有class样式,则会与其融合
 ```
 <div id="root">
    <div  class="divBorder" v-bind:class="classColor">
        绑定class样式 字符串写法
        <button @click="listColor">点击切换样式</button>
    </div>
</div>
<script>
 const vm = new Vue({
            el:'#root',
            data:{
                // 绑定class样式 字符串写法
                classColor:'',
            },
            methods: {
                // 绑定class样式 字符串写法 
                listColor(){
                    const classA = ['a1','a2','a3','a4','a5']
                    const index = Math.floor(Math.random()*3)  // 获取随机数，用于数组切换
                    this.classColor = classA[index]  // 切换样式
                },
            },
        })
<script>
 ```
![](https://image.dcaoao.com/image/202301022134911.gif)

结果就是`v-bind:class="classColor"`获取到的类名,与class="divBorder"合并在了一起,达到了切换class或者新增的效果


### 绑定class样式 数组写法
适用于要绑定的样式个数不确定,名字也不确定
```
 <div id="root">
    <div  class="divBorder" :class="classArr">
        绑定class样式 数组写法 
        <button @click="ArrColorPush">点击添加样式</button>
        <button @click="ArrColorPop">点击删除样式</button>
    </div>
 </div>

<script>
  const vm = new Vue({
            el:'#root',
            data:{
                 // 绑定class样式 数组写法
                classArr:['a1','a2',],
            },
            methods: {
                // 绑定class样式 数组写法
                ArrColorPush(){
                    this.classArr.push('a3')
                },
                ArrColorPop(){
                    this.classArr.pop()
                },
            },
        })
</script>
```
![](https://image.dcaoao.com/image/202301022138071.gif)
可以看到,通过push与pop方法,可以进行数组中的添加与删除,达到切换class的效果,


### 绑定class样式 对象写法 
适用于要绑定的样式个数确定，名字确定，但是需要动态决定要不要使用
```
 <div id="root">
        <div  class="divBorder" :class="classObj">
            绑定class样式 对象写法
            <button @click="StartObj">点击启用样式</button>
            <button @click="EndObj">点击禁用样式</button>
        </div>
 </div>
 <script>
         const vm = new Vue({
            el:'#root',
            data:{
                // 绑定Class样式,对象写法
                classObj:{
                    a1:false,
                    a2:false,
                    a3:false
                },
            },
            methods: {
                // 绑定class样式 对象写法
                StartObj(){
                    this.classObj.a3 = true
                },
                EndObj(){
                    this.classObj.a3 = false
                }
            },
        })
 </script>
```
![](https://image.dcaoao.com/image/202301022143761.gif)

通过data内的样式对象,来调整其的 false与true来决定是否启用这个样式,从而渲染到页面中

## style 绑定行内样式
.style样式
`:style="{fontSize:xxx}"`  其中.xxx是动态值
`:style="[{a,b}]"`        其中,a b 是样式对象
其内部的行内样式,需要遵循驼峰命名法,比如 `font-size` 需要转换为`fontSize`
```
    <div id="root">
        <!-- 绑定style行内样式,对象写法 -->
        <div class="divBorder" :style="styleObj">绑定style行内样式,对象写法</div>
        <!-- 绑定style行内样式,数组写法 -->
        <div class="divBorder" :style="styleArr">绑定style行内样式,数组写法</div>
</div>
    <script>
        const vm = new Vue({
            el:'#root',
            data:{
                // 绑定style行内样式,对象写法
                styleObj:{
                    fontSize:'40px',
                    color:'red'
                },
                // 绑定style行内样式,数组写法
                styleArr:[{
                    fontSize:'40px',
                },{
                    color:'red'
                }]
            },
        })
    </script>
```

# 条件渲染
### `v-if` 写法
1. v-if="表达式"
2.v-else-if="表达式"
3.v-else="表达式"

v-if适用于`切换频率较低`的场景,不展示的DOM元素会被直接移除
v-if可以与v-else-if v-else一起使用,但是要求结构不能被打断


### `v-show` 写法
`v-show="表达式"`
适用于切换频率较高的场景
不展示的元素未被移除,仅仅是样式隐藏

使用v-if的时候,元素可能无法获取到,但是v-show一定可以获取到，两者都可以做到元素的隐藏与显示，表达式是布尔值即可

两者都可以使元素达到隐藏或者显示的效果
## v-show

```
<div id="root">
        <h2>当前n的值是{{n}}</h2>
        <button @click="n++">点击n+1</button>

        <!-- 使用v-show做条件渲染 -->
        <div v-show="false">v-show</div>
        <div v-show="n === 1">v-show</div>
    </div>


    <script>
        const vm = new Vue({
            el: '#root',
            data: {
                n: 0,

            }
        })
    </script>
```
![](https://image.dcaoao.com/image/202301032202760.gif)
可以看到,当n等于1时,表达式成立为true 使`v-show="n === 1"`的div盒子 从`display: none;`状态解除,从而显现了出来


## v-if

```
<div id="root">
        <h2>当前n的值是{{n}}</h2>
        <button @click="n++">点击n+1</button>

        <!-- 使用 v-if做条件渲染 -->
        <div v-if="false">v-if</div>
        <div v-if="n === 2">v-if</div>
    </div>


    <script>
        const vm = new Vue({
            el: '#root',
            data: {
                n: 0,

            }
        })
    </script>
```
![](https://image.dcaoao.com/image/202301032205491.gif)

当`v-if`的表达式不成立时,在页面中直接为不显示结构,与`v-show`不同的是,`v-if`是直接操作DOM元素


## v-if与 v-else-if与v-else
```
        <!--  v-if与 v-else-if与v-else -->
        <div v-if="false">v-if</div>
        <!-- v-else-if会在其上面的v-if不成立时被调用 -->
        <div v-else-if="n === 3">v-else-if</div>
        <!-- v-else会在所有v-if不成立时,被调用，不用写条件表达式 -->
        <div v-else="">v-else</div>
        <!-- v-if v-else-if  v-else  标签中间不能穿插其他的标签,否则会被打断无法使用 -->


    <script>
        const vm = new Vue({
            el: '#root',
            data: {
                n: 0,

            }
        })
    </script>
```
![](https://image.dcaoao.com/image/202301032210766.gif)
最开始,因为`v-if`与`v-else-if`都不成立,所以v-else被直接调用了
可以看到,当n为3  `v-else-if` 被成立时,v-else取消执行了
到了n为4,所有表达式都不成立,所以v-else被再次执行
`v-if v-else-if  v-else`  标签中间不能穿插其他的标签,否则会被`打断`无法使用

## v-if与template配合 批量操作元素,不影响DOM结构 template只能与V-if配合

```
        <template v-if="n === 5">
            <h3>你好</h3>
            <h3>世界</h3>
            <h3>Vue</h3>
        </template>
    <script>
        const vm = new Vue({
            el: '#root',
            data: {
                n: 0,

            }
        })
    </script>
```
在这里的:
```
        <template v-if="n === 5">
            <h3>你好</h3>
            <h3>世界</h3>
            <h3>Vue</h3>
        </template>
```
其实,等同于
```
<h3 v-if="n === 5">你好</h3>
<h3 v-if="n === 5">世界</h3>
<h3 v-if="n === 5">Vue</h3>
```
但是这样写过于繁琐,所以利用了一下`template`标签来进行包裹元素来进行批量操作,但是只能与`v-if`配合


![](https://image.dcaoao.com/image/202301032216366.gif)

可以看到在渲染出来的页面结构内,并没有发现`template`标签,也就是说这样不会影响页面结构

# 基本列表渲染

列表渲染使用`v-for`指令
1.用于列表展示数据,可以根据渲染类型创建多个标签
2.语法 `v-for=(item,index) in xxx :key="index"`
3.可遍历: 数组 对象(频繁)  字符串与指定次数(用的少)
key最好使用唯一标识数据，比如说p.id  而不是使用索引号

## 遍历数组
`v-for="(p,index) in Arr"`
语法:`v-for="(p,index) in 遍历的数组名"`
`p` 可以看做是形参 返回的是遍历数组的内容
`index`返回的是遍历的数组索引号
```
<body>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.7.14/dist/vue.js"></script>

    <!-- 准备容器 -->
    <div id="root">
        <!-- 遍历数组 -->
        <h2>遍历数组</h2>
        <!-- p 可以看做是形参 返回的是遍历数组的内容  index返回的是遍历的数组索引号 -->
        <li v-for="(p,index) in Arr" :key="index">{{p.name}} --- {{p.age}} --- {{index}}</li>
    </div>

    <script>
        const vm = new Vue({
            el: '#root',
            data: {
                // 遍历数组 
                Arr: [
                    { id: 001, name: '张三', age: '18' },
                    { id: 001, name: '李四', age: '18' },
                    { id: 001, name: '王五', age: '18' },
                ],
            }
        })
    </script>
</body>

```
![](https://image.dcaoao.com/image/202301032224821.png)

## 遍历对象

接收两个形参 `p`代表了对象值 `index`代表了对象名  唯一id key可以使用index

```
<body>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.7.14/dist/vue.js"></script>

    <!-- 准备容器 -->
    <div id="root">
         <!-- 遍历对象 -->
        <h2>遍历对象</h2>
        <!-- 接收两个形参 p代表了对象值 index代表了对象名  唯一id可以使用index -->
        <li v-for="(p,index) in Obj" :key="index">{{p}} --- {{index}}</li>
    </div>

    <script>
        const vm = new Vue({
            el: '#root',
            data: {
                // 遍历对象
                Obj: {
                    name: '赵六',
                    age: '19',
                    sex: '男'
                },
            }
        })
    </script>
</body>

```
![](https://image.dcaoao.com/image/202301032226788.png)


## 遍历字符串
接收两个形参 `p`代表了字符串内的`每一个内容` `index`代表了字符串`索引号`  唯一id可以使用index
```
<body>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.7.14/dist/vue.js"></script>

    <!-- 准备容器 -->
    <div id="root">
        <!-- 遍历字符串 -->
        <h2>遍历字符串</h2>
        <!-- 接收两个形参 p代表了字符串内的每一个内容 index代表了字符串索引号  唯一id可以使用index -->
        <li v-for="(p,index) in Str" :key="index">{{p}} --- {{index}}</li>
    </div>

    <script>
        const vm = new Vue({
            el: '#root',
            data: {
                // 遍历字符串
                Str: '你好,世界'
            }
        })
    </script>
</body>

```
![](https://image.dcaoao.com/image/202301032227257.png)

## 遍历指定次数
`v-for="(p,index) in 5`中的5,代表了遍历五次,并没有遍历的目标.只是单纯的遍历五次,也返回两个值
第一个遍历的次数,根据自然数计数,从1开始
第二个是遍历的索引号,从0开始

```
<body>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.7.14/dist/vue.js"></script>

    <!-- 准备容器 -->
    <div id="root">
        <!-- 遍历指定次数 -->
        <h2>遍历指定次数</h2>
        <!-- 接收两个形参 p代表从1开始计数的数值 index代表了字符串索引号  唯一id可以使用index 5则代表了循环五次 -->
        <li v-for="(p,index) in 5" :key="index">{{p}} --- {{index}}</li>>
    </div>

    <script>
        const vm = new Vue({
            el: '#root',
            data: {}
        })
    </script>
</body>

```
![](https://image.dcaoao.com/image/202301032230806.png)


## 额外注意项, key值

```
 <li v-for="(p,index) in Arr" :key="index">{{p.name}} --- {{p.age}} --- {{index}}</li>
```

 可以看到的是,使用 `v-for`进行遍历,其后方都跟随着一个`:key`,这个key值是作为遍历唯一属性值使用的,一般由后端处理返回,比如

```
{ id: 001, name: '张三', age: '18' },
{ id: 001, name: '李四', age: '18' },
{ id: 001, name: '王五', age: '18' },
```
其中的id就可以用作是key值,同理,手机号,邮箱,都可以用作遍历唯一值使用
![](https://image.dcaoao.com/image/202301031818905.png)
![](https://image.dcaoao.com/image/202301031818781.png)

# 列表过滤

## 用watch实现列表过滤

```
    <div id="root">
        <h2>列表过滤</h2>
        <input type="text" name="" id="" placeholder="请输入名字" v-model="keyWord">
        <li v-for="(p,index) in filterArr" :key="index">{{p.name}} --- {{p.age}} --- {{p.sex}}</li>
    </div>
<script>
        // 用watch实现
        const vm = new Vue({
            el: '#root',
            data: {
                // 收集用户输入的数据
                keyWord: '',
                // 遍历数组 
                Arr: [
                    { id: 001, name: '马冬梅', age: '18', sex: '女' },
                    { id: 002, name: '周冬雨', age: '18', sex: '女' },
                    { id: 003, name: '周杰伦', age: '18', sex: '男' },
                    { id: 004, name: '温兆伦', age: '18', sex: '男' },
                ],
                // 准备一个空数组,用于存放过滤后的数组
                filterArr: []
            },
            watch: {
                keyWord: {
                    immediate:true,
                    handler(val) {
                        this.filterArr = this.Arr.filter((p) => {
                            return p.name.indexOf(val) !== -1
                            console.log(p.name.indexOf(val) !== -1)
                        })
                    }
                }
            }
        })
</script>
```
![](https://image.dcaoao.com/image/202301032237528.gif)

## 用计算属性实现列表过滤
```
        const vm = new Vue({
            el: '#root',
            data: {
                // 收集用户输入的数据
                keyWord: '',
                // 遍历数组 
                Arr: [
                    { id: 001, name: '马冬梅', age: '21', sex: '女' },
                    { id: 002, name: '周冬雨', age: '18', sex: '女' },
                    { id: 003, name: '周杰伦', age: '20', sex: '男' },
                    { id: 004, name: '温兆伦', age: '19', sex: '男' },
                ],
            },
            computed:{
                filterArr(){
                    return this.Arr.filter((val)=>{
                        return val.name.indexOf(this.keyWord) !== -1
                    })
                }
            }
        })
```

两者效果相同


# 列表排序
效果展示：
![](https://image.dcaoao.com/image/202301032239264.gif)

```
<body>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.7.14/dist/vue.js"></script>

    <!-- 准备容器 -->
    <div id="root">
        <h2>列表排序</h2>
        <input type="text" name="" id="" placeholder="请输入名字" v-model="keyWord">
        <li v-for="(p,index) in filterArr" :key="index">{{p.name}} --- {{p.age}} --- {{p.sex}}</li>
        <button @click="sortType = 2">年龄升序</button>
        <button @click="sortType = 1">年龄降序</button>
        <button @click="sortType = 0">原顺序</button>
        <span>当前排序: {{sortType}}</span>
    </div>

    <script>
        const vm = new Vue({
            el: '#root',
            data: {
                keyWord: '',
                sortType: 0,  // 0原顺序 1降序 2升序
                Arr: [
                    { id: 001, name: '马冬梅', age: '21', sex: '女' },
                    { id: 002, name: '周冬雨', age: '18', sex: '女' },
                    { id: 003, name: '周杰伦', age: '20', sex: '男' },
                    { id: 004, name: '温兆伦', age: '19', sex: '男' },
                ],
            },
            computed: {
                filterArr() {
                    const arr = this.Arr.filter((val) => {
                        return val.name.indexOf(this.keyWord) !== -1
                    })
                    // 开始判断是否需要排序
                    if (this.sortType !== 0) {
                        // 如果是降序
                        if (this.sortType === 1) {
                            arr.sort(function (a, b) {
                                return b.age - a.age
                            })
                            // 如果是升序
                        }else {
                            arr.sort(function (a, b) {
                                return a.age - b.age
                            })
                        }

                    }
                    console.log(arr)
                    return arr
                }
            }
        })
    </script>
</body>
```


# Vue.set的使用


如果在控制台输入 `vm._data.sex.a = '女'` 页面不会有任何变化,也不会报错，因为事先没有`sex.a`这个属性，Vue检测不到,其不是响应式数据
但是使用 `Vue.set(vm._data.sex,'a','男')`，页面即可就可以检测到,将其添加为响应式数据,并重新渲染
`Vue.set(在哪添加,'添加的属性名','添加的属性值')`
此时执行第一步的 `vm._data.sex.a = '女'` 页面即可被响应,因为其已经被设置为响应式数据

第二种方法 `vm.$set(vm._data.sex,'a','女')`  效果相同

需要注意的是，这两种方法都有`局限性`，不能直接向 `vm实例内的data直接添加属性`，比如
`Vue.set(vm._data,'a','男')`  这样会报错
只能向 vm实例内的data内的对象添加属性
`Vue.set(vm._data.sex,'a','男')`

![](https://image.dcaoao.com/image/202301042103998.gif)
```
<body>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.7.14/dist/vue.js"></script>

    <!-- 准备容器 -->
    <div id="root">
        <h2>学校名称:{{school}}</h2>
        <h2>技能:{{skill}}</h2>
        <h2>性别:{{sex.a}}</h2>
        <button @click="addSex">点击添加性别属性</button>
    </div>

    <script>
        const vm = new Vue({
            el: '#root',
            data: {
                school: 'XX大学',
                name: 'Tom',
                skill: '全国捕鼠大赛冠军',
                sex: {

                }
            },
            methods: {
                addSex() {
                    Vue.set(this.sex, 'a', '男')
                }
            },
        })
    </script>
</body>
```

## 总结Vue数据监测

### Vue监视数据的原理:
1.Vue会监视data中所有层次的数据
2.如何检测对象中的数据?
### 通过setter实现监控 并且要在new Vue时就传入要监测的数据
2.1对象中后追加的属性,Vue默认不做响应式处理
2.2如需给后添加的属性做响应式,请使用以下API
`Vue.set(数据地址,要添加的数据名,数据值)`
`vm.$set(数据地址,要添加的数据名,数据值)`
### 3.如何监测数组中的数据?
通过包裹数组更新元素的方法
3.1调用远程数组方法进行数组更新 pop shift unshift之类
3.2重新解析模板,从而页面更新
### 4.在Vue中修改数组某个元素一定要用以下方法
4.1 使用API : `push() pop() shift() unshift() splice() sort() reverse()`
4.2 `Vue.set()` 或者 `vm.$set()`
需要注意的是,`Vue.set()` 与 `vm.$set()` 不能给vm,或者vm的`根数据对象`(比如data) 添加属性,直接赋值

```
<body>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.7.14/dist/vue.js"></script>

    <!-- 准备容器 -->
    <div id="root">
        <h1>学生信息</h1>

        <button @click="student.age ++">年龄 +1 岁</button>
        <button @click="AddSex">添加性别属性 默认男</button>
        <button @click="student.sex = '女'" v-if="student.sex">修改性别属性 女</button>
        <button @click.once="AddFriends">在列表首位添加一个朋友</button>
        <button @click="SetFriends">修改第一个朋友的名字为张三</button>
        <button @click="addHobby">添加一个爱好</button>
        <button @click="setHobby">修改第一个爱好为:开车</button>
        <button @click="delChou">去掉抽烟爱好</button>

        <h3>姓名:{{student.name}}</h3>
        <h3>年龄:{{student.age}}</h3>
        <h3 v-if="student.sex">性别:{{student.sex}}</h3>
        <h3>爱好:</h3>
        <li v-for="h in student.hobby">{{h}}</li>
        <h3>朋友:</h3>
        <li v-for="f in student.friends">{{f.name}} __{{f.age}}</li>
    </div>

    <script>
        const vm = new Vue({
            el:"#root",
            data:{
                student:{
                    name:'Tom',
                    age:18,
                    hobby:['抽烟','喝酒','烫头'],
                    friends:[
                        {name:'jerry',age:'18'},
                        {name:'tony',age:'19'},
                    ]
                }
            },
            methods:{
                AddSex(){
                    Vue.set(this.student,'sex','男')
                },
                AddFriends(){
                    this.student.friends.unshift({name:'朋友',age:'18'})
                },
                SetFriends(){
                    this.student.friends[0].name = '张三'
                },
                addHobby(){
                    this.student.hobby.push('一个爱好')
                },
                setHobby(){
                    // Vue.set(this.student.hobby,0,'开车')
                    this.student.hobby.splice(0,1,'开车')
                },
                delChou(){
                    this.student.hobby = this.student.hobby.filter((val) => {
                        return val !== '抽烟'
                    })
                }
            }
            
        })
    </script>
</body>
```

# 收集表单数据

表单收集数据:
如果 `<input type="text">` 则v-model收集的是value值  用户输入的就是value值
如果 `<input type="radio">` 则v-model收集的是value值 而且需要给标签配置value值
如果 `<input type="checkbox">` 没有配置value值,则收集的就是checked `(布尔值 勾选true 未勾选false)`
如果为其配置了value值 v-model初始值是非数组 则收集的就是checked `(布尔值 勾选true 未勾选false)`
如果为其配置了value值 v-model初始值是数组 则收集的就是value组成的数组
## v-model有三个修饰符
`lazy` 失去焦点时再收集数据
`number` 输入的字符串转换为数字
`trim` 过滤掉首尾空格过滤
例 `v-model.number=""`

```
    <script src="https://cdn.jsdelivr.net/npm/vue@2.7.14/dist/vue.js"></script>
    <div id="root">
        <form action="" @submit.prevent="">
            账号: <input type="text" v-model="UserData.UserName">
            密码: <input type="text" v-model="UserData.password"> <br><br>
            年龄: <input type="number" v-model.number="UserData.age">
            性别: 男<input type="radio" v-model="UserData.sex" value="男"> 女<input type="radio" v-model="UserData.sex" value="女"> <br><br>

            爱好:
            抽烟<input type="checkbox" v-model="UserData.hobby" value="抽烟">
            喝酒<input type="checkbox" v-model="UserData.hobby" value="喝酒">
            烫头<input type="checkbox" v-model="UserData.hobby" value="烫头"> <br><br>

            所属校区:
            <select name="" id="" v-model="UserData.area">
                <option value="beijing">北京</option>
                <option value="shandong">山东</option>
                <option value="shanghai">上海</option>
                <option value="tianjin">天津</option>
                <option value="sichuan">四川</option>
            </select><br><br>

            其他信息:
            <textarea name="" id="" cols="50" rows="5" v-model.lazy="UserData.other"></textarea><br><br>
            <input type="checkbox" v-model="UserData.agreement">阅读并接收<a href="https://www.baidu.com/">《用户许可协议》</a><br><br>

            <button @click="submitAdd">提交</button>

        </form>
    </div>

    <script>
        const vm = new Vue({
            el: '#root',
            data: {
                UserData: {
                    UserName: '',
                    password: '',
                    age:'',
                    sex: '',
                    hobby: [],
                    area: '',
                    other: '',
                    agreement: ''
                }

            },
            methods: {
                submitAdd() {
                    console.log(JSON.stringify(this.UserData))
                }
            },
        })
    </script>
```

# 内置指令

学过的内置指令
v-bind 单向绑定解析表达式 可简写 :xxx
v-model : 双向数据绑定
v-for : 遍历数组/对象/字符串
v-on : 绑定事件监听 可简写为 @ 
v-if : 条件渲染(动态控制节点是否存在)
v-else : 条件渲染(动态控制节点是否存在)
v-show : 条件渲染(控制节点是否存在)

## v-text
v-text指令
1.向所在的节点中`替换文本`
2.与插值语法的区别,v-text会替换掉节点中的内容,插值语法不会

```
    <div id="root">
        <div>{{world}}</div>
        <div v-text="text">123456</div>
        <div v-text="label"></div>
    </div>
    
    <script>
        const vm = new Vue({
            el:'#root',
            data:{
                world:'你好世界',
                text:'你好,v-text',
                label:'<h3>这是个标签</h3>'
            }
        })
```
![](https://image.dcaoao.com/image/202301052112460.png)


## v-html

v-html指令
1.作用 向指定节点中渲染`包含html标签`的内容
2. 与插值语法的区别
2.1 v-html会`替换掉节点中所有的内容` 插值语法不会
2.2 v-html可以识别html结构
3. 特别注意: v-html有安全性问题
3.1在网站上动态渲染html结构是非常危险的,容易导致XSS攻击
3.2 一定到在可信的内容上使用 v-html 永远`不要在用户提交的内容上使用html`
```
    <div id="root">
        <div>{{world}}</div>
        <div v-text="text">123456</div>
        <div v-html="label"></div>
    </div>
    
    <script>
        const vm = new Vue({
            el:'#root',
            data:{
                world:'你好世界',
                text:'你好,v-text',
                label:'<h3>这是个标签</h3>'
            }
        })
```

## v-cloak
v-cloak指令用于 vue没有被加载时使用的
    本质是一个特殊属性,vue实例创建完毕并接管容器后,会`删掉 v-cloak属性`
    使用css配合v-cloak可以解决网速慢时页面展现出的`{{xxx}}`问题

```
    <!-- Css配合 -->
    <style>
        /* 将所有带有v-cloak的标签全部隐藏,在Vue接管实例后悔删除v-cloak属性,从而使标签显示 */
        [v-cloak] {
            display: none;
        }
    </style>
```

## v-once
v-once指令
1.v-once所在节点在`初次动态渲染后`,就视为`静态内容`了
2.以后数据的改变不会引起v-once所在结构的改变,可以`优化性能`

```
    <script src="https://cdn.jsdelivr.net/npm/vue@2.7.14/dist/vue.js"></script>

    <div id="root">
        <h2 v-once>显示N的初始数值:{{n}}</h2>
        <h2>动态显示N的数值:{{n}}</h2>
        <button @click="n++">点击n+1</button>
    </div>

    <script>
        const vm = new Vue({
            el: '#root',
            data: {
                n: 1,
            }
        })
    </script>
```
![](https://image.dcaoao.com/image/202301052120108.gif)


## v-pre
v-pre指令
1.跳过所在节点的编译过程
2.可以利用其跳过:没有使用指令语法,没有使用插值语法的节点 会`加快编译`

```
    <div id="root">
        <h2 v-pre>显示N的初始数值:{{n}}</h2>
        <h2 v-pre>动态显示N的数值:{{n}}</h2>
        <button @click="n++">点击n+1</button>
    </div>

    <script>
        const vm = new Vue({
            el: '#root',
            data: {
                n: 1, 
            }
        })
    </script>
```
![](https://image.dcaoao.com/image/202301052121084.png)


# 自定义属性
配置自定义属性配置项: `directives`
```
const vm = new Vue({
            el:'#root',
            data:{},
            // 配置自定义属性配置项: directives
            directives:{}
            }
        })
```
## 自定义指令 函数式

自定义属性,函数式,函数有两个形参,第一个接收所在标签的Dom元素,第二个接收自定义指令中所用到的值 
big函数何时会被调用? 1.指令与元素成功绑定时 2.指令所在模板被重新解析时
```
    <script src="https://cdn.jsdelivr.net/npm/vue@2.7.14/dist/vue.js"></script>

    <!-- 准备容器 -->
    <div id="root">
        <h2>{{name}}</h2>
        <h2>当前的n值是:{{n}}</h2>
        <h2>放大十倍的n值是: <span v-big="n"></span> </h2>
        <button @click="n++">点击n+1</button>
    </div>

    <script>
        const vm = new Vue({
            el:'#root',
            data:{
                name:'你好,世界',
                n:1
            },
            directives:{
                v-big="n" 里的n,就是1
                big(a,b){
                    console.log(a,b)
                    a.innerText = b.value * 10
                }
            }
        })
    </script>
```

## 自定义指令 对象式

配置对象中常用的三个回调函数
1.`bind` 指令与元素成功绑定时执行
2 `inserted` 指令所在元素被插入页面时执行
3 `update` 所在的模板被重新解析时执行

```
    <script>
        const vm = new Vue({
            el: '#root',
            data: {
                name: '你好,世界',
                n: 1
            },
            // 配置自定义属性配置项: directives
            directives: {
                // 自定义属性,对象式
                fbing: {
                    // 指令与元素成功绑定时执行
                    bind(element, binding) {
                        console.log(element, binding)
                        element.innerText = binding.value * 10
                    },
                    // 指令所在元素被插入页面时执行
                    inserted(element, binding) {
                        element.value = binding.value * 10
                    },
                    // 所在的模板被重新解析时执行
                    update(element, binding) {
                        element.innerText = binding.value * 10
                    }

                }
            }
        })

    </script>
```

## 自定义指令小结
函数式与对象式的`this`,都指向了`window`, 而且都是`局部变量`,只能在当前Vue实例内使用,需要的话可以注册为全局变量

全局指令
`Vue.directive('指令名',配置对象)`
`Vue.directive('指令名',回调函数)`

指令定义时不加`v-`,但是使用时要加`v-`
指令名如果是多个单词,要使用 `a-b`的命名方法,`不要使用驼峰命名法`

### 全局变量注册方法
` Vue.directive('变量名',变量函数&对象)`

```
        // 这是对象式全局写法
        Vue.directive('fbing', {
            // 指令与元素成功绑定时执行
            bind(element, binding) {
                console.log(element, binding)
                element.innerText = binding.value * 10
            },
            // 指令所在元素被插入页面时执行
            inserted(element, binding) {
                element.value = binding.value * 10
            },
            // 所在的模板被重新解析时执行
            update(element, binding) {
                element.innerText = binding.value * 10
            }

        })

        // 这是函数式全局写法
        Vue.directive('big',function(a,b){
            a.innerText = b.value * 10
        })
```


# 生命周期

生命周期
1.又名 生命周期回调函数 生命周期函数 生命周期狗子
2. 是Vue在关键时刻帮忙调用的一些特殊名称的函数
3.生命周期函数的名字不可更改,但是函数的具体内容是程序员根据需求编写的
4.生命周期函数中的this指向的是vm或者组件实例对象


## 分析生命周期-流程

Vue声明周期分三步 挂载 - 更新 - 销毁

常用的声明周期钩子
1.`mounted` 发送ajax请求,启动定时器,绑定自定义事件,订阅消息等[初始化操作]
2.`beforeDestroy` 清除定时器,解绑自定义事件,取消订阅消息等[收尾工作]
关于销毁Vue实例
1.销毁后借助开发者工具看不到任何消息
2.销毁后自定义事件会失效,但是原生DOM依然有效
3.一般不会在`beforeDestroy`中操作数据,因为即便操作了,也不会执行更新流程了

```
    <script src="https://cdn.jsdelivr.net/npm/vue@2.7.14/dist/vue.js"></script>

    <div id="root">
        <h2>当前的N值是{{n}}</h2>
        <button @click="add">点击n+1</button>
        <button @click="kick">销毁VM实例</button>
    </div>


    <script>
        const vm = new Vue({
            el: '#root',
            data: {
                opacity: 1,
                n: 1
            },
            methods: {
                add() {
                    this.n++
                },
                // 销毁vm实例
                kick(){
                    vm.$destroy()
                }
            },
            // 挂载流程开始
            // beforeCreate 生命周期开始时执行，此时无法访问到 vm data等数据
            beforeCreate() {

            },
            // created 生命周期第二步，此时可以访问到vm与data数据
            created() {

            },
            // beforeMount 显示的是未经Vue编译的DOM结构，此时对DOM的任何操作，最终都不会奏效
            beforeMount() {

            },
            // mounted 生命周期函数 Vue完成模板的解析，并将初始的DOM元素放入页面后，会调用mounted函数，后续页面数据更新变化，不会被再次调用，只会页面加载调用一次
            // 页面中呈现的是经过Vue编译的DOM,此时对DOM的操作均有效(尽量避免直接操作DOM),一般进行开启定时器,发网络请求,自定义事件之类
            mounted() {
                 
            },
            // 挂载流程结束

            // 更新流程开始
            // beforeUpdate 此时，发现数据被改变，数据是新的，但是页面是旧的， 页面显示数据未和数据保持同步
            beforeUpdate() {
                
            },
            // updated 此时，数据是新的，页面也是新的，页面与数据保持同步
            updated() {
                
            },
            // 更新流程结束

            // 销毁流程开始,调用了 vm.$destroy 之后
            // beforeDestroy 销毁前的挣扎,此时vm中所有的data methods 指令等都处于可用状态,马上就要被销毁,此时一般进行关闭定时器,取消订阅消息,解绑自定义事件等首位操作
            beforeDestroy() {

            },
            // destroyed 销毁流程完全结束，vm被销毁，除了原生的事件  比如说点击事件
            destroyed() {
                
            },

        })
    </script>
```

# 非单文件组件的基本使用

创建组件 -> 注册组件 -> 编写组件标签（使用组件）

Vue中使用组件的三大步骤
一,定义组件(创建组件)
二,注册组件
三,使用组件(写组件标签)


## 一,如何定义一个组件?
使用 Vue.extend({}),其解构与 new Vue时相同,也稍微有些区别
1.el不需要写 最终所有组件都要经过vm管理,由vm的el决定服务哪个容器
2.data必须写成函数式, 避免组件被复用时,数据存在引用关系


## 二,如何注册组件?
1.局部注册 在new Vue中传入components配置项
2.全局注册 Vue.components('组件名',组件)


## 三,使用组件
在html结构中写入注册组件的名字标签即可  <school></school>


## 创建组件
使用 `Vue.extend({})`来创建一个组件

例:
```
const school = Vue.extend({
            // 使用 template 来创建模板结构
            template: `
            <div>
                <h2>学校:{{schoolName}}</h2>
                <h2>学校地址:{{address}}</h2>
                <button @click="schoolDe">点击显示学校名称</button>
            </div>`,

            // 组件中的data,必须要写成函数式
            data() {
                return {
                    schoolName: '学校名称',
                    address: '学校地址是XXXXX',
                }
            },
            methods: {
                schoolDe(){
                    console.log(this.schoolName)
                }
            },

        })
```
需要注意的是,组件与组件之间,数据是不会互相影响的,而且data需要写成`函数式`

```
            data() {
                return {
                    schoolName: '学校名称',
                    address: '学校地址是XXXXX',
                }
            },
```

## 注册组件

配置项 `components` 用于注册组件 

```
        const vm = new Vue({
            el: '#root',
            data: {},
            // components 第二步：注册组件配置项   局部注册
            components: {
                school: school,
                student: student,
            },
        })
```

## 编写组件标签（使用组件）
在模板结构中,使用第二步注册的组件名,直接写成标签形式放入HTML结构中
```
    <div id="root">
        <!-- 第三步,编写组件标签 -->
        <school></school>
        <school></school>
        <hr>
        <student></student>
    </div>
```

## 几个注意点

1.关于 ` 组件名  `
一个单词组成: 
(首字母小写) : `school`
(首字母大写) : `School`
多个单词组成:
第一种写法: `'my-school'`
第二 种写法: `MySchool` (需要Vue脚手架支持)

组件尽量回避Html中已有的元素名称 例如 h2 H2 都不行
可以在组件内部添加配置项,name 可以更改组件在开发者工具中呈现的名字

2.关于组件标签
第一种写法 `<school></school>`
第二种写法 `<school/>`
备注:不使用脚手架时,第二种写法不推荐,会导致后续组件不能渲染

3.一个简写方式
`const shcool = Vue.extend()`  可以简写为 `const school = {}`

## 组件的嵌套
组件内可以嵌套组件,vm下可以指明一个组件管理其他组件,一般为`App`组件,这个是标准化的

首先,创建三个组件
```

        // student组件
        const student = Vue.extend({
            name: 'student',
            template: `
            <div>
                <h2>学生姓名:{{studentName}}</h2>
                <h2>学生年龄:{{age}}</h2>
            </div>`,
            data() {
                return {
                    studentName: '学生姓名是XXX',
                    age: 18
                }
            }
        })

        // schoolShop组件

        const schoolShop = Vue.extend({
            template:`
            <div><h2>学校小卖铺:{{shop}}</h2></div>
            `,
            data(){
                return {
                    shop:'学校对面小卖铺'
                }
            }
        })

        // school组件
        const school = Vue.extend({
            name: 'school',
            template: `
            <div>
                <h2>学校:{{schoolName}}</h2>
                <h2>学校地址:{{address}}</h2>
                <schoolShop></schoolShop>
            </div>`,
            data() {
                return {
                    schoolName: '学校名称',
                    address: '学校地址是XXXXX',
                }
            },
            components:{
                schoolShop:schoolShop
            }
        })


```

然后在这三个组件的下方,创建一个App组件,用于管理这三个组件
其中,`school`组件嵌套了`schoolShop`组件
App组件使用`components`注册了`school`与`student`组件,从而在`template`中使用了他们
```
        // 创建一个标准化嵌套的组件 APP
        const app = Vue.extend({
            template:
            `
            <div>
                <school></school>
                <student></student>
            </div>
            `,
            components:{
                school:school,
                student:student,
            }
        })
```

![](https://image.dcaoao.com/image/202301071812284.png)

# 单文件组件

## 配置Vue脚手架环境
安装NPM后,执行命令
```
<!-- 更换NPM镜像源为淘宝镜像源 -->
npm config set registry https://registry.npm.taobao.org
<!-- 安装Vue脚手架 -->
npm install -g @vue/cli
<!-- 创建Vue项目 -->
vue create hello-world
```
创建Vue项目后,其目录结构如下
![](https://image.dcaoao.com/image/202301082006506.png)
![](https://image.dcaoao.com/image/202301082116026.png)


单文件组件,就是每个组件都是一个 `XXX.VUE`文件
`<template>` 代表结构标签
`<script>`  代表组件相关代码,也是JS的书写地址
`<style>`  书写样式

安装插件: `Vetur` 用于Vue文件内的语法高亮结构

创建 `School.vue`组件

```
<template>
  <!-- 结构标签 -->
  <div class="demo">
    <h2>学校:{{ schoolName }}</h2>
    <h2>学校地址:{{ address }}</h2>
    <button @click="schoolDe">点击显示学校名称</button>
  </div>
</template>

<script>
// 组件相关代码
// Vue文件内的script,需要使用默认暴露 export default  ES6讲的,需要学习
export default {
  // 此处定义组件名，建议与文件名保持一致
  name: "School",
  data() {
    return {
      schoolName: "学校名称",
      address: "学校地址是XXXXX",
    };
  },
  methods: {
    schoolDe() {
      console.log(this.schoolName);
    },
  },
};
</script>

<style>
/* 组件样式标签 */
.demo {}
</style>
```

需要注意的是,`<script>`标签内,需要使用 `export default {}` 进行`暴露`,为ES6知识,抽空学习一下 

## APP.vue

上方组件创建完毕后,使用APP组件进行管理

`import School from './School.vue'` 为引入组件 创建了两个组件 School与Student

并且在App的 `<template>`标签与 `components` 配置项中,分别注册与使用了这两个组件

```
<template>
    <div>
        <School></School>
        <Student/>
    </div>
</template>

<script>

// 引入组件
import School from './School.vue'
import School from './Student'
export default {
    name:'App',
    data() {
        return {
            
        }
    },
    components:{
        School,
        Student,
    }
}
</script>

<style>

</style>
```

## main.js

main.js 同等于vm,用来管理APP组件,APP组件再去管理其他组件

```
// 引入Vue
import Vue from 'vue'
// 引入App组件,是所有组件的父组件
import App from './App.vue'
// 关闭生产提示
Vue.config.productionTip = false
// 创建vm实例
new Vue({
  render: h => h(App),
}).$mount('#app')

```

关于不同版本的Vue
1.`vue.js`与`vue.runtime.xxx.js`的区别
vue.js是完整版的Vue,可以通过 `import Vue from 'vue/dist/vue'` 引入 核心功能 + 模板解析器
`vue.runtime.xxx.js` 是运行版的Vue 只包含核心功能 没有模板解析器
2.因为 `vue.runtime.xxx.js` 没有模板解析器 所以不能使用template作为配置项,需要使用 `render`函数接收到的`createElement`函数去指定具体内容

这个render函数,只会在main.js中使用一次


# ref属性
Ref属性 
1.被用来给元素或子组件注册引用信息(id的代替者)
2.如果ref在Html结构上,获取到的是真实的DOM元素 如果在组件的标签上,则获取到的是组件实例对象(vc)
3.使用语法:  打标识: `<h1 ref="refH1">ref测试</h1>`  获取 `this.$$refs.refH1`

```
<template>
  <div>
    <!-- 为组件标签添加 ref 可以获取组件对象 -->
    <School ref="zujian"></School>
    <Student />
    <!-- 为标签添加 ref 可以直接获取DOM元素 -->
    <div ref="test">
      <h1 ref="refH1">ref测试</h1>
    </div>
    <button @click="testRefDom">ref元素测试</button>
  </div>
</template>

<script>
// 引入组件
import School from "./components/School.vue";
import Student from "./components/Student.vue";
export default {
  name: "App",
  data() {
    return {};
  },
  components: {
    School,
    Student,
  },
  methods: {
    testRefDom() {
        // 输出DOM结构
      console.log(this.$refs.test);
      console.log(this.$refs.refH1);
      console.log(this.$refs.zujian);
    //   可直接更改DOM元素
      this.$refs.refH1.innerHTML = '666'
    },
  },
};
</script>

<style>
</style>
```

# props 配置项
配置项props

功能: 让组件接收外部传过来的数据
1.传递数据
`<Student name="李四" :age="18" />`
2.接收数据
2.1 `props:['name']`    (只接收)
2.2 `props:{name:String}`   (限制接收的数据类型)
2.3 
```
propo:{
  name:{
    type:String, // 限制接收类型
    required:true, // 必要性
    default:'xxx'  //默认值
  }
}
```
 props是`只读`的,不能修改,如果修改的话也可以修改,但是Vue会发出警告
 如果非要修改的话,可以在data内新建一个参数接收peops内的参数,然后进行修改即可

 ```
 <script>
// 组件相关代码

export default {
  name: "Student",
  data() {
    return {
      Vue: "Vue学习",
      // name: "张三",
      // sex:'男',
      // age:18,
      // 如果需要修改 props内的数据,可以在data内使用一个变量接收过来,用于修改与读取
      MyAge: this.age,
    };
  },
  // 配置项 props 其可使用数组/对象两种方式存储，名字可同等于data内的数据，传递参数在调用组件的标签内
  // 可以做到结构复用,数据动态的效果

  // 数组写法
  // props:['name','sex','age'],

  // 对象写法 对象写法可以限制接收的参数类型 在接收的同时对数据进行类型限制  比如字符串 数值等 如果不符合则报错，但是不耽误接收数据
  // 1.String 字符串
  // 2.Number 数字
  // 3.Boolean 布尔
  // 4.Array 数组
  // 5.Object 对象
  // 6.Date 日期
  // 7.Function 函数
  // 8.Symbol 独一无二的(ES6)
  // props: {
  //   name: String,
  //   sex: String,
  //   age: Number,
  // },

  // props 对象形式的另一种写法 接收数据的同时对数据进行 类型限制 默认值的指定 必要性的限制
  props: {
    // 接收数据的名字
    name: {
      // 对数据信息类型限制
      type: String,
      // 此参数 也就是 name 是否必须要传入
      required: true,
    },
    sex: {
      type: String,
      // 默认值的指定,如果该参数没有传入,则赋予一个默认的值
      default: "男",
    },
    age: {
      type: Number,
    },
  },
};

</script>
 ```

# mixin 混入方法

## 局部混入

在目录中新建一个`mixin.js`
```
// 在js中写入配置项, 需要使用export进行暴露(ES6知识)

export const hunhe1 = {
    methods: {
        consoleName() {
            console.log(this.name)
        }
    },
}

export const hunhe2 = {
    mounted() {
        console.log('mixin配置项')
    },
}
```
然后在组件内引入
`import { hunhe1 } from "./mixin";`
然后再使用配置项 mixin 来注册混入对象, 为数组形式
` mixins: [hunhe1, hunhe2],`

 注册后的组件即可使用这些配置项,如果与原有的配置项冲突,则以原有的配置项为主
 如果组件内与mixin.js内的配置项有重复, 则会与其混合, 而不是覆盖
 组件内引入与使用mixin配置项注册的混入对象都是局部混入, 之后注册了的对象才可以使用

 ## 全局混入
 全局混入需要在`main.js`内
使用 `import { hunhe1,hunhe2 } from "./mixin";` 来引入混入对象
然后在其下方使用 `Vue.mixin(hunhe1)` 来进行全局混入
需要注意，全局注册需要在`main.js`内，创建vm实例之前写入
全局注册之后,所有组件都可以使用`mixin.js`内的配置项与方法
```
// 引入Vue
import Vue from 'vue'
// 引入App组件,是所有组件的父组件
import App from './App.vue'
// 关闭生产提示
Vue.config.productionTip = false


import { hunhe1, hunhe2 } from './components/mixin';
Vue.mixin(hunhe1)
Vue.mixin(hunhe2)


new Vue({
  render: h => h(App),
}).$mount('#app')
```


# Vue插件
与`mixin.js` 类似
功能 用于增强Vue
本质 包含install方法的一个对象 install接收的第一个参数是Vue, 第二个及以后的参数是插件使用者传递的数据
新建一个`plugins.js`  可以写各种全局指令，需要使用暴露指令
```
export default {
    // 其内部写一个函数，然后去main.js 加载这个插件
    install(a, x, y, z) {
        console.log('Vue插件已被加载')
        console.log(a)
        console.log(x, y, z)

    }
}
```
```
export default {
    install(a, x, y, z) {
    //   1.添加全局过滤器
        Vue.filter(...)
    // 2.添加全局指令
        Vue.directive(...)
    // 3.配置全局混入
        Vue.mixin(...)
        4. 添加实例方法
    Vue.prototype.$my = function(){...}
    }
```
然后在`main.js`内引入插件js
```
import Vue from 'vue'
import App from './App.vue'
Vue.config.productionTip = false


// 引入插件
import plugins from './plugins'
// 使用插件  而且可以传递参数
Vue.use(plugins, 1, 2, 3)


new Vue({
  render: h => h(App),
}).$mount('#app')
```
引入插件 `import plugins from './plugins'`
使用插件: `Vue.use()  在main.js内`



# scoped样式
xxx.vue内的`style`标签,应用的Css样式如果与其他组件的类名有重复,会根据App.vue内的引用顺序产生影响
可以使用`scoped`属性,使当前组件的`</style>`标签只对当前组件的HTML结构生效

语法:`<style scoped></style>`
在`style`标签内加入 `scoped`属性,可以是样式只在当前组件生效,防止冲突
`lang="less"` 使style标签内使用less语法，需要完善环境 `npm i less-loader@7` 安装`less-loader`
`<style lang="less">`

# 本地存储
本地存储,按照域名区分,由浏览器负责保存,大小限制5MB左右,不同浏览器不一样
其内部,只能存储字符串,使用键值对方法存储数据,如果需要存储对象形式数据,需要在存入时将其转换为字符串格式,取用时将其转换为对象形式即可
![](https://image.dcaoao.com/image/202301121918746.png)
## 本地存储 localStorage

特性,关闭浏览器后不会消失,需要手动清除

添加数据:`localStorage.setItem('键值名', '添加的值')`
读取数据:`localStorage.getItem("键值名")`
删除数据:`localStorage.removeItem("键值名")`
清空数据:`localStorage.clear()`

```
<body>
    <h2>本地存储 localStorage 特性,关闭浏览器后不会消失,需要手动清除</h2>
    <button onclick="saveData()">添加数据</button>
    <button onclick="readData()">读取数据</button>
    <button onclick="delData()">删除数据</button>
    <button onclick="clearData()">清空数据</button>


    <script>

        const p = { name: "名字", age: 18 }
        // 添加一个数据
        function saveData() {
            localStorage.setItem('msg', '你好,世界')
            localStorage.setItem('json', JSON.stringify(p))  // JSON.stringify(p) 将对象转换为字符串类型
        }
        // 读取一个数据
        function readData() {
            console.log(localStorage.getItem("msg"))
            const JSONTest = localStorage.getItem('json')
            console.log(JSON.parse(JSONTest))  // JSON.parse(JSONTest) 将字符串转换为JSON格式
        }
        // 删除一个数据
        function delData() {
            localStorage.removeItem("msg")
        }
        // 清空数据
        function clearData() {
            localStorage.clear()
        }
    </script>
</body>
```
![](https://image.dcaoao.com/image/202301121922577.gif)

## 本地存储 sessionStorage 
特性,关闭浏览器数据清空
其他使用方式与localStorage完全相同

添加数据:`sessionStorage.setItem('键值名', '添加的值')`
读取数据:`sessionStorage.getItem("键值名")`
删除数据:`sessionStorage.removeItem("键值名")`
清空数据:`sessionStorage.clear()`

# 自定义事件
自定义事件与原生事件类似相同,但是执行的方式由程序员定义
组件的自定义事件
### 一.一种组件之间通信的方式 适用于子组件给父组件传递信息
### 二. 使用场景 A是父组件 B是子组件 B想给A传递数据 那么就要在A中给B绑定自定义事件(事件的回调函数写在父组件中)
### 三. 绑定自定义事件
1.第一种方式 在父组件中: `<Demo @shijian="test" /> 或者 <Demo v-on:shijian="test" />`
2.第二种方式 在父组件中: `<Demo ref="demoTest">`  `mounted() {this.$refs.demoTest.$on("refDemo",this.test)},`
这里的`this.test`指的是父组件中的回调函数 写在`methods`中  `refDemo`则需要在子组件中使用 `this.$emit("refDemo", this.name);` 接收

3.如果只想让自定义事件触发一次,可以使用once修饰符,或者$once方法

四. 触发自定义事件 `this.$emit("refDemo", 传递的数据);`
五. 解绑自定义事件 `this.$off('refDemo')` ,解绑多个自定义事件 `this.$off(['refDemo1','refDemo2'])`
六. 组件是可以绑定原生DOM事件 如果和自定义事件一起使用 需要在绑定的子标签上加上`native`  例: `<Student v-on:testDemo="demo" @click.native="dianji"/>`
七. 通过 `this.$refs.demoTest.$on("refDemo",回调函数名)` 绑定自定义事件时 回调函数要么配置值`methods`中 要么使用`箭头函数`直接写在里面 否则this指向会出现问题

## 自定义事件绑定
通过在父组件模板结构标签上进行绑定自定义事件,以此传递给子组件
```
    <Student v-on:testDemo="demo"/>
```
可以看做为  给Student组件绑定了一个 `"testDemo"` 事件 只要test被触发,`demo函数就会被调用`
父组件给子组件绑定一个自定义事件,实现子给父传递数据

父组件的demo函数,谁接收数据,回调函数就在谁的内部
```
  methods: {
    // 接收Student传递过来的参数
    demo(x) {
      console.log("demo被调用了,testDemo事件被触发", x);
    },
  },
```

### 然后是子组件
给按钮绑定一个点击事件来触发自定义事件
语法:`this.$emit("父组件传递的自定义事件名", 需要传递的子组件数据);`
```
<button @click="getStudentName">把学生名传递给APP(触发事件)</button>
```
```
  methods: {
    getStudentName() {
      // 利用点击事件触发该组件 app组件传递过来的 testDemo 事件 ，并且传递参数
      this.$emit("testDemo", this.name);
    },
```
![](https://image.dcaoao.com/image/202301121935069.png)
这里的this.name 为`名字`

以此,父组件中的demo函数接收到参数值:`'名字'`,就可以进行使用了


## 自定义事件绑定 ref方式
也是首先在父组件的模板标签中,为子组件传递自定义事件,使用`ref`方式
```
<Student ref="testStudent" />
```

然后在mounted配置项中,写入触发操作
在refs上的 `testStudent` 如果`testDemoRef`事件被触发,则调用`refDemo`函数
```
  methods: {
    refDemo() {
      console.log("refDemo函数被调用了,testDemoRef事件被触发");
    },
  },
  mounted() {
    this.$refs.testStudent.$on("testDemoRef", this.refDemo);
  },
```

  ### 子组件操作
语法:
`this.$emit("事件名称", 要传递的子组件参数);`

```
<button @click="getStudentName">Ref触发事件</button>
```
```
  methods: {
    getStudentName() {
      this.$emit("testDemoRef", this.name);
    },
```


## 解绑事件
函数被触发后,执行解绑事件 `$off('xxx')`
解绑`一个`自定义事件
`this.$off("testDemo");`
解绑`多个`自定义事件（数组字符串形式）
`this.$off(["testDemo", "testRef"]);`
解绑所有自定义事件
`this.$off();`

自定义事件被解绑之后,无法再次通过调用触发自定义事件,除非被再次绑定

# 全局事件总线
全局事件总线
一.一种组件之间的通信方式, 适用于`任意组件间通信`
二.安装全局事件总线 在main.js中, 创建vm实例之前 插入`Vue.prototype.$bus = new Vue()`
三.使用事件总线
1.接收数据 A组件接收数据 则在A组件中给$bus绑定自定义事件，事件的回调则留在A组件自身
```
methods: {
  demo(data){console.log(data)}
},
mounted() {
  this.$bus.$on('xxx',this.demo)
},
```
2.提供数据, B组件提供数据 则在B组件当中键入
  `this.$bus.$emit('xxx',数据)`

四.最好在beforeDestroy生命周期钩子中, 使用$off去解绑当前组件所用到的事件, 防止重名占用
  ```
  beforeDestroy() {
    this.$bus.$off("SendName");
  },
  ```

### 挂载全局事件总线
![](https://image.dcaoao.com/image/202301121948908.png)

##  使用全局事件总线$bus来传递参数到同级组件中
A组件要传参到B组件,两个组件之间是兄弟关系

A组件定义一个函数,使用全局事件总线传参到B组件
语法:`this.$bus.$emit("自定义事件名", 传递的数据);`

```
  methods: {
    // 使用全局事件总线$bus来传递参数到同级组件中
    send() {
      this.$bus.$emit("SendName", this.name);
    },
  },
```

B组件准备接收A组件传递过来的参数,最好写在`mounted`当中
语法: `this.$bus.$on("自定义事件名", 回调函数)`
这个回调函数可以写在`methods`当中,也可以直接使用箭头函数
```
  mounted() {
    this.$bus.$on("SendName", (data) => {
      console.log("我是School,收到Student传递来的参数:", data);
    });
  },
```

使用全局事件总线传递完毕后,最好销毁一下自定义事件,否则容易引起重名,导致事件错乱,因为全局事件总线是所有组件都可以使用的
使用生命周期钩子,销毁流程开始
```
  beforeDestroy() {
    this.$bus.$off("SendName");
  },
```


# 消息订阅与发布
一.一种组件间的通讯方式,适用于`任意组件`通信
二.安装步骤
1. `npm i pubsub-js`
2.引入 `import pubsub from "pubsub-js"`
3.接收数据 A组件
```
  mounted() {
    // 使用pubsub-js接收数据，其内部的箭头函数也可以写在methods中
    this.pubid = pubsub.subscribe("hello", (msgName, data) => {
      console.log("这是接收的数据名:" + msgName);
      console.log("这是接收的数据:" + data);
    });
  },  mounted() {
    // 使用pubsub-js接收数据，其内部的箭头函数也可以写在methods中
    this.pubid = pubsub.subscribe("hello", (msgName, data) => {
      console.log("这是接收的数据名:" + msgName);
      console.log("这是接收的数据:" + data);
    });
  },
```
  4.提供数据 B组件
  ```
   // 使用pubsub-js发送数据
      pubsub.publish("hello", this.Vue);
  ```

  5.与全局事件总线相同,最好在结束钩子内使用
  `pubsub.unsubscribe(this.pubid);` 取消订阅


  ## 发送数据
  ```
    data() {
    return {
      Vue: "Vue学习",
      name: "名字",
      age: 18,
    };
  },
  methods: {
    send() {
      // 使用pubsub-js发送数据
      pubsub.publish("hello", this.Vue);
    },
  ```
## 接收数据
```
  mounted() {
    // 使用pubsub-js接收数据，其内部的箭头函数也可以写在methods中
    this.pubid = pubsub.subscribe("hello", (msgName, data) => {
      console.log("这是接收的数据名:" + msgName);
      console.log("这是接收的数据:" + data);
    });
  },
  beforeDestroy() {
    // 取消订阅消息
    pubsub.unsubscribe(this.pubid);
  },
```

# Vue代理服务器
代理服务器用于解决ajax请求跨域问题,在vue中有两种开启方式

## 方式一
在`Vue.config.js`中添加如下配置
```
  //开启代理服务器（方式一） 简单开启
devServer: {
  // 需要代理的服务器地址
  proxy: 'http://localhost:5000'
}
```
然后组件中请求的地址改成本机地址即可
此刻请求 `http://localhost:8080/students`
等于请求 `http://localhost:5000/students`
```
      axios.get("http://localhost:8080/students").then(
        (response) => {
          console.log("请求成功", response.data);
        },
        (error) => {
          console.log("请求失败", error.message);
        }
      );
    },
```
1.配置简单 请求资源时直接发给前端即可
2.缺点: 不能配置多个代理 不能灵活的控制是否走代理
3.工作方式 如果请求了前端中已有的资源,则`优先返回前端的内容`,而不是代理服务器的内容

## 方式二
`Vue.config.js` 配置具体代理规则
```
  devServer: {
    proxy: {
      // 匹配所有/server1 开头的请求路径
      '/server1': {
        // 重要 正则表达式，将/server1替换为空，否则其会请求到目标服务器的 /server1路径下
        pathRewrite: { '^/server1': '' },
        // 代理目标的基础路径
        target: 'http://localhost:5000',
        // ws协议
        ws: true,
        // 是否欺骗请求服务器，如果开启，则欺骗服务器请求来自与其同源 ，关闭则规规矩矩本地
        changeOrigin: true
      },
    }
  }
```
此刻,组件内请求`http://localhost:8080/server1/students`的请求,会经过代理服务器
但是,`http://localhost:8080/server2/students`的请求则不会,而是直接请求本机

优点: 可以配置多个代理, 灵活的控制请求`是否走代理`
缺点: 配置略微繁琐, 请求资源时必须加`前缀`


# Vuex插件
一.vuex的概念
在vue中实现集中式数据的管理,是一个vue插件,对vue应用中的多个组件的共享状态进行集中式的管理(读,写数据) 也是一种`组件间通信`的方式,而且适用于任意组件通信
二.何时使用 ?
    多个组件需要共享数据时
## 安装Vuex
1.安装 vuex
```
    npm i vuex@3
```
需要注意的是,vue2只支持vuex3的版本  对应的  vue3只支持vuex4的版本,需要安装对应的vuex版本,否则会报错

2.创建 `src/store/index.js` 文件

该文件用于创建 Vuex 中最为核心的`store`

```
// 该文件用于创建 Vuex 中最为核心的store

// 引入Vue
import Vue from 'vue'
// 引入vuex
import Vuex from "vuex"

// 使用vuex插件
Vue.use(Vuex)

// 准备 actions 用于响应组件中的动作
const actions = {}

// 准备 mutations 用于操作数据
const mutations = {}

// 准备 state 用于存储数据
const state = {}


// 创建并暴露store
export default new Vuex.Store({
    actions,
    mutations,
    state,
})
```

3.在main.js中, 引入这个js

```
// 引入vuex所创建的store
import store from "./store/index"
```
并且在main.js创建实例的同时,将其引入
```
new Vue({
  render: h => h(App),
  // 创建实例的同时引入vuex的store
  store,
}).$mount('#app')
```


## Vuex的使用

模板内读取Vuex的$store的数据
`$store.state.xxx`

### 第一步
将数据传递到`$store`内
语法: `this.$store.dispatch("传递的方法名", 传递的值);`
```
    del() {
      this.$store.dispatch("jian", this.val);
    },
```
### 第二步
在store内的index.js文件内 `actions` 用于接收组件内传递过来的数据,并将其预处理,判断条件,延时请求之类

响应组件传递过来的: `jian` 动作
函数式,接收两个参数,`context.commit`用于将其推送到`mutations`内操作数据,`value`则就是组件传递过来的值

`context.commit('组件中传递过来的动作名', 组件传递过来的值，也就是 value所携带的值)`
```
const actions = {
    jian(context, value) {
        // 将其转发到mutations中,也可以在此写一些判断,ajax请求之类
        context.commit('jian', value)
    },
}
```
### 第三步
`mutations` 准备操作数据
准备操作state中的值,使用组件中传递过来的值，value也是接收的组件传递的值
```
const mutations = {
    jian(state, value) {
        state.sum -= value
    },
}
```

### 第四步
存储数据,这个要在第三步操作数据之前,将其提前准备好
```
// 准备 state 用于存储数据
const state = {
    sum: 0,
}
```

### 组件使用
模板内读取数据:`$store.state.sum`
组件函数传递数据: `this.$store.dispatch("传递的方法名", 传递的值);`
如果数据不需要处理，比如说判断条件，延时请求，发送ajax请求等，可以跳过 actions阶段
也就是:`this.$store.dispatch("传递的方法名", 传递的值);` 传递数据,`actions`数据预处理阶段

直接去 `mutations`操作数据，语法:  `this.$store.commit("传递的方法名", 传递的值);`


## 26 mapState与mapGetters

如果模板中要调用vuex中产生的值,则需要 `{{$store.state.sum}}`  `{{$store.getters.sumMax}}` 来调用,写在模板中,导致不美观而且不易观看

可以使用 mapState与mapGetters来生成计算属性,使模板中可以直接通过 `{{xxx}}` 来读取数据

### 第一步 .引入mapState与mapGetters
import { mapState, mapGetters } from "vuex";

###  mapState
 mapState 读取state中的数据,并生成计算属性(对象写法)  语法: `...mapState({生成的计算属性名:'State内的数据名'}) ` 模板内使用计算属性名读取数据即可

 mapState 读取state中的数据,并生成计算属性(数组写法)  语法: ...mapState(['State内的数据名']) 数组写法直接写State内的数据名即可，生成的计算属性名与读取的数据名相同

 例:`  computed: {...mapState(["sum"]),}`
 模板内则可以直接使用 `<h1>当前求和为:{{ sum }}</h1>` 访问到state中的数据
 ![](https://image.dcaoao.com/image/202301182157539.png)

### mapGetters
mapGetters读取getters内的数据,并生成计算属性
mapGetters对象式写法 语法：` ...mapGetters({生成的计算属性名:'State内的数据名'}),`

mapGetters数组式写法 语法： `...mapGetters(['State内的数据名']),`

例:`computed: {...mapGetters(["sumMax"]),}`

模板可以直接使用`<h1>处理后的数据为:{{ sumMax }}</h1>`访问到vuex中的getters数据


## mapState与mapGetters mapActions

### 第一步 .引入mapState与mapGetters mapActions
`import { mapState, mapGetters, mapActions, mapMutations } from "vuex";`

### mapActions
mapActions方法,生成与 `actions` 对话的方法 即 `this.$store.dispatch("ji", this.val);`
    对象写法
   ` ...mapActions({ 方法名: "actions内的数据名" }),`
    数组写法
    `...mapActions(["actions内的数据名"]),`
    mapMutations方法 用于生成与`mutations`对话的方法,即`$store.commit(xxx)`

### mapMutations
 mapMutations方法 用于生成与`mutations`对话的方法,即`$store.commit(xxx)`

  对象式写法
    `...mapMutations({方法名: "actions内的数据名"})`
    数组式写法
    `...mapMutations(["actions内的数据名"])`


mapActions与mapMutations使用时,如果需要传递参数,就像`this.$store.commit("jia", this.val);`与`this.$store.dispatch("jian", this.val);` 传递this.val值

则在模板中使用时,需要在绑定事件中传递参数: `<button @click="ji(val)">按钮</button>`


## 使用vuex后,多组件共享数据

```
  computed: {
    // mapState 读取state中的数据
    ...mapState(["sum", "personList"]),

    // mapGetters读取getters内的数据,并生成计算属性
    ...mapGetters(["sumMax"]),
  },
  methods: {
    ...mapActions(["ji", "timeadd"]),
    ...mapMutations(["jia", "jian"]),
  },
```

读取getters数据: `$store.getters.xxx`
读取state数据: `$store.state.xxx`
模板内读取需要加上this


## vuex 模块化编码
当store/index.js中的文件需要模块化分级时,可以将配置分为多个对象

![](https://image.dcaoao.com/image/202301182208546.png)

对象内又分别包含actions,mutations,state,getters等对象,用于响应动作,处理动作,存储数据,加工存储数据

![](https://image.dcaoao.com/image/202301182209763.png)

再将对象分别进行暴露操作,方便组件使用
```
// 模块暴露
export default new Vuex.Store({
    countAbout: countOptions,
    personAbout: personOptions
})

```

组件使用时,使用 mapState mapGetters mapActions mapMutations配置,在其数组前方添加暴露名称即可正常使用
语法:`...mapState("暴露配置项"["配置项内的属性"]),`
```
  computed: {
    // mapState 读取countOptions  中的数据
    ...mapState("countOptions"["sum"]),
    // mapState 读取personOptions  中的数据
    ...mapState("personOptions"["personList"]),

    // mapGetters读取getters内的数据,并生成计算属性
    ...mapGetters("countOptions"["sumMax"]),
  },
  methods: {
    // mapMutations方法 用于生成与`mutations`对话的方法,即$store.commit(xxx)
    ...mapActions("countOptions"[("ji", "timeadd")]),
    ...mapMutations("countOptions"[("jia", "jian")]),
  },
```

  接下来模板即可正常`{{sum}}` 调用store内的属性值了


# 路由的基本使用
  路由 一个路由(route)就是一组映射关系(key - value), 多个路由需要路由器(router) 进行管理
   前端路由 key是路径 value是组件

由路由进行管理的,叫路由组件,一般存放于 `src/pages` 文件夹中
普通调用的,叫一般组件或者普通组件 存放于 `components`文件夹中
## 一.基本使用
1.安装 `vue - router` 命令
Vue路由,是vue中的一个插件
vue-router3版本只能用作vue2版本中
vue-router4版本只能用作vue3版本中
安装vue-router
```
npm i vue-router@3
```

2.创建路由文件
在`src/components/router`文件夹中, 创建`index.js`文件

```
// 改文件用于创建整个应用的路由器

// 引入VueRouter路由插件
import Vue from 'vue'
import VueRouter from 'vue-router'

// 引入要路由的组件
import About from '../components/about'
import Home from '../components/home'

// 创建路由器
export default new VueRouter({
    routes: [
        // 创建路由规则
        {
            // 路由路径
            path: '/about',
            // 对应的路由组件
            component: About
        },
        {
            path: '/home',
            component: Home
        }
    ]
})
```

3.应用VueRouter路由插件

在`main.js`文件中,引入以下文件,并且创建vm实例时创建路由器
```
// 引入VueRouter路由插件
import VueRouter from 'vue-router'
// 引入路由器
import router from './router'
// 应用VueRouter路由插件
Vue.use(VueRouter)
-------------------

new Vue({
  render: h => h(App),
  store,
  // 创建实例的同时创建路由器
  router: router

}).$mount('#app')
```

4.在模板中, 应用路由标签

`<router-link>`标签 用于切换路由, 拥有两个配置项 to 与 active - class 本质渲染后为a标签
`active- class`配置项用于那个路由规则被激活, 该标签就应用某个class属性
例`<router - link class="list-group-item" to = "/about" active - class="active"> About</router - link>`

显示路由标签 router - view 指定组件显示的位置
`<router-view></router-view>`

```
    <div class="row">
      <div class="col-xs-2 col-xs-offset-2">
        <div class="list-group">
          <!-- <a class="list-group-item active" href="./about.html">About</a>
          <a class="list-group-item" href="./home.html">Home</a> -->

          <!-- 切换路由 router-link 标签  to属性为要跳转的路径 active-class属性为 谁被激活，谁就应用某个样式-->
          <router-link class="list-group-item" to="/about" active-class="active"
            >About</router-link
          >
          <router-link class="list-group-item" to="/home" active-class="active"
            >Home</router-link
          >
        </div>
      </div>
      <div class="col-xs-6">
        <div class="panel">
          <div class="panel-body">
            <!-- 显示路由标签 router-view 指定组件显示的位置 -->
            <router-view></router-view>
          </div>
        </div>
      </div>
    </div>
```

## 多级路由(嵌套路由)
1.配置路由规则
二级路由的配置项为 `children` 其内部与一级路由相同, 需要注意的是, `path` 不需要写 `/` 直接写路径即可
二级路由的跳转则是在一级路由的基础上, 直接添加二级路由内`path`的地址即可

`< router-link class="list-group-item" active-class="active" to = "/home/message"> Message </router-link>`
```

     routes: [
        // 创建路由规则
        {
            // 路由路径
            path: '/about',
            // 对应的路由组件
            component: About
        },
        // Home组件嵌套路由,也叫二级路由
        {
            path: '/home',
            component: Home,
            // 二级路由
            children: [
                {
                    path: 'message',
                    component: Message
                },
                {
                    path: 'news',
                    component: News
                }
            ]
        }
    ]
```

## 路由的query参数
适用于数据过多,创建多个组件不现实时,使用query传递参数,使接收参数的组件达到一个组件多个页面的效果
 一.传递参数
 跳转并携带query参数, 跳转路由并传递参数到路由组件 path参数负责跳转的路径组件，query参数负责要传递的参数，对象写法
```
        <router-link
          :to="{
            path: '/home/message/detail',
            query: {
              id: p.id,
              title: p.title,
            },
          }"
          >{{ p.title }}</router-link
```
二.接收参数
`$route.query.id`
`$route.query.title`

## 路由命名
路由命名
适用于跳转路径过长时, 进行简化书写, 需要跳转的`:to` 为对象形式才可以使用

一, 给路由命名
```
    routes: [
        // 创建路由规则
        {
            name:about
            path: '/about',
            component: About
        }]
```
二, 简化跳转
```
    <router-link :to="{path: 'about',}">简化跳转</router-link
```

直接在跳转标签内输入路由名字即可使用,字符串形式

## 路由的props配置项(传递参数)

A组件使用`query`传递参数时,B组件可以使用`$route.query.xxx` 来读取参数,显得过于冗杂

可以在A组件的路由配置中,使用props配置项来进行简化参数
然后在B组件中,使用props来接收简化过的参数名,达到使用简化参数读取数据的目的

## A组件路由配置
```
   routes: [
            {
                path: 'detail',
                component: detail,
                // 路由的props配置项 函数式  在此发送到接收参数的组件中 作用 让组件更方便的收到参数
                props($rouse) {
                    return {
                        id: $rouse.query.id,
                            title: $rouse.query.title
                                }
                            }

                        }
   ]
```

props配置项为函数式,可以接收到一个参数,`$rouse` 用于读取A组件传递过来的`query`内的数据,此刻id与title便可通过`组件内props配置项`接收

### B组件内配置项
```
<template>
  <div>
    <h2>消息ID:{{ id }}</h2>
    <h2>消息标题:{{ title }}</h2>
  </div>
</template>

<script>
export default {
  name: "About",
  // 组件使用props接收从路由发送过来的参数，模板内即可使用简写形式读取参数
  props: ["id", "title"],
};
</script>
```

## 路由的模块化编码

模块化编码是指,不使用`<router-link>`标签来进行路由的切换,使用button,div,img等标签都可以实现路由的切换

`this.$router.push`   `this.$router.replace`  使用二者就可以做到任意模块的路由跳转
```
      this.$router.replace({
        // name:XXX
        path: "要跳转的路由路径,或者配置项名字",
      });
```
实际代码展示
```
 methods: {
    pushShow(p) {
      this.$router.push({
        path: "/home/message/detail",
      });
    },
    replaceShow(p) {
      this.$router.replace({
        path: "/home/message/detail",
      });
    },
  },
```

  

## router-link标签的replace属性

`<router-link>`的replace属性

1.作用 控制路由跳转是操作浏览器历史记录的模式
2.浏览器的历史记录有两种写入方式,分别是`push与replace`
`push`是追加记录,也是默认行为,通过此行为浏览器跳转的路由可以正常前进,后退
`replace`则是替换当前记录,浏览器无法前进与后退,只能在当前页面停留
开启`replace`模式: `<router-link replace>News</router-link> `

## 缓存路由组件

### 1.作用,让不展示的路由组件保持挂载,不被销毁
比如用户在A组件输入框填写了某些内容,没有保存,然后切换至B组件
按照往常路由规则,离开A组件后,A组件会被销毁,再次切换回A组件时,输入框内的内容会消失

使用缓存路由标签包裹要挂载的路由组件,`<router-view>`标签即可使被包裹的组件保持挂载,不被销毁

### 2.语法:`<keep-alive include="组件名"></keep-alive>`

### 3.缓存多个组件
使用数组形式
<keep-alive linclude="['zujian1','zujian2']"></keep-alive>

实际代码演示
```
            <keep-alive>
              <router-view></router-view>
            </keep-alive>
```

## 路由组件生命周期钩子
路由组件独有的两个声明周期钩子,与methods配置项平级

分别在路由组件显示/隐藏 时被触发
`activated`与`deactivated`
可以用作于定时器在其内部 适用于使用` <keep-alive>`标签要求路由组件保持激活时使用
比如路由进组件,`activated`使某个定时器开启,路由出组件后,如果组件通过`<keep-alive>`标签保持激活,则定时器会继续运行,可以使用`deactivated`生命周期钩子使其结束运行


## 全局路由守卫

全局路由守卫,分为全局`前`置路由守卫与全局`后`置路由守卫

分别在路由切换前执行,与路由切换后执行,为全局事件

### 全局前置路由守卫

`beforeEach((to, from, next)=>{})` 初始化路由与路由组件被切换时执行 需要在暴露之前应用


```
// 首先创建路由器并给路由器命名
const luYou = new VueRouter({})

// 创建前置全局路由守卫
luYou.beforeEach((to, from, next)=>{})

// 创建后置全局路由守卫
luYou.afterEach((to, from, next)=>{})

// 暴露路由
export default luYou
```

beforeEach 接收三个参数(to, from, next)，分别是路由切换`终点`，路由切换`起点`，以及`允许路由切换`

to与from为对象形式，其中 path 为去往的路由路径 name为路由名字等  其中只要next执行了，路由就能成功切换

通过判断权限,设定`是否允许路由切换`
#### 第一种方法：
如果路由切换终点的路径是 `news` 与 `message` 两个组件,则开始判断,如果不是,则直接允许切换路由
```
luYou.beforeEach((to, from, next)=>{
 if (to.path === '/home/news' || to.path === '/home/message') {
        // 如果本地存储信息值为666，则允许切换路由，如果不是，则拒绝其切换
        if (localStorage.getItem('school') === '666') {
            next()
        } else {
            alert('本地信息不正确,无法切换')
        }
    } else {
        next()
    }
    })
```
#### 第二种方法 路由配置项`meta`
meta是路由配置项内专门为程序员准备的一片区域,可以随意放置一些内容
在这里可以放置一个配置项,来确认是否需要权限检测

```
 routes: [
            {
            path: '/about',
            component: About,
            meta: { isAuto:true,title: '首页' }
        },]
```

```
luYou.beforeEach((to, from, next) => {
    // 如果配置项内存在isAuto,并且为true,则开始权限判断,没有则跳过判断
    if (to.meta.isAuto === true) {
        // 如果本地存储信息值为666，则允许切换路由，如果不是，则拒绝其切换
        if (localStorage.getItem('school') === '666') {
            next()
        } else {
            alert('本地信息不正确,无法切换')
        }
    } else {
        next()
    }
})
```

### 后置路由守卫 `afterEach`
 初始化时被调用,每次路由组件切换之后被调用  一般用于修改网页标题，也拥有路由切换终点，路由切换起点
 ```
 luYou.afterEach((to, from) => {
    document.title = to.meta.title || '测试'
})

 ```

## 组件内路由守护
通过路由规则进入某组件时的调用，被模板调用并不会被调用，语法与全局前置路由组件语法相同，可以看做是单独路由守护的组件内部版，是一个配置项 与 methods等平级关系

### 通过路由规则，进入该组件时被调用 `beforeRouteEnter`
```
  beforeRouteEnter(to, from, next) {
    console.log("从About组件路由进入了");
    if (to.meta.isAuto) {
      if (localStorage.getItem("school") === "666") {
        next();
      } else {
        alert("本地信息不正确,无法切换");
      }
    } else {
      next();
    }
  },
```

### 通过路由规则，离开该组件时被调用 `beforeRouteLeave`

```
  beforeRouteLeave(to, from, next) {
    console.log("从About组件路由离开了");
    next();
  },
```

# Vue2学习完毕 
2023年1月25号,Vue2学习完毕,开始写第一个项目,以下是项目中遇到问题的笔记

## v-for渲染列表后,切换class样式

模板区域,模板先行渲染出来,使用点击事件传入数据内的唯一参数,方便进行比较
```
        <li v-for="p in ListImg" :key="p.Name" @click="pitchOnClick(p.id)">
          <el-avatar
            shape="circle"
            :size="50"
            :src="p.img"
            v-bind:class="{ pitchOn: p.id == idClass }"
          ></el-avatar>

          <span>{{ p.Name }}</span>
        </li>
```

事件区域
将接收过来的唯一值,赋值给data内的idClass
```
  methods: {
    // 快递列表被点击后动作
    pitchOnClick(id) {
      // 快递列表被选中class切换
      this.idClass = id;
      }}
```

然后模板利用class的原理,来控制样式是否显示
如果当前的id与data内存储的id相等,则显示该样式,不相等则不显示
 `v-bind:class="{ 类名: 唯一值 == data内数据 }"`
` v-bind:class="{ pitchOn: p.id == idClass }"`


## 为v-for渲染后的列表,不同列表绑定不同事件

还是先传递一个数据唯一值进事件内
```
        <li v-for="p in ListImg" :key="p.Name" @click="pitchOnClick(p.id)">
          <el-avatar
            shape="circle"
            :size="50"
            :src="p.img"
            v-bind:class="{ pitchOn: p.id == idClass }"
          ></el-avatar>

          <span>{{ p.Name }}</span>
        </li>
```

事件收到此唯一值后,进行事件的绑定
语法:`this[唯一值]();`

```
methods: {
    // 快递列表被点击后动作
    pitchOnClick(id) {
      //   为不同的按钮创建不同的事件绑定
      this[id]();
    },
    // 在下方写好事件,与事件名与唯一值对应
    ZN() {
      console.log("智能通道");
    },
    YT() {
      console.log("圆通快递");
    },
  },
};
```