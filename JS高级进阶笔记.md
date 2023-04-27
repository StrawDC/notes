
# 代码段的理解

一个script标签就是一个代码段,多个代码段之间不会互相影响
如果上方的代码段报错,则下方的代码段会继续执行,
声明的变量,下方的代码段可以调用上方代码段的数据

# 什么是预解析

 预解析分为两步  声明提升与代码执行
 `1.`声明提升:
 加了var的变量,需要提升  只提升声明 没有赋值,function内的函数 声明提升至函数最上方  提升至代码段的最前面
 `2.`如果在函数内部的局部连着,则被提升至函数内部的最前面

 ```
 <script>
    console.log(a)
    var a = 1

    // 在预解析内为
    var a;
    console.log(a)  //输出空值
    a = 1
</script>
 ```

```
<script>
    // --------- 原题
    console.log(value);
    var value = 123;
    function value(){
        console.log("我是value函数...");
    }
    console.log(value);

    // 解析，因为变量与函数名同名，先提升
    // var value;
    // function value(){
    //     console.log("我是value函数...");
    // }
    // 然后输出
    // console.log(value);    此时为value函数
    //赋值 value = 123
    //再次输出console.log(value);   //123

</script>
```


# 创建类和函数

```
    // 1.创建类,使用class 创建一个类
    class Start {
        // class创建类后,其内部有一个 constructor函数 无需function声明，与普通函数一样，拥有形参和实参
        constructor(name,age){
            this.name = name
            this.age = age
        }
        //在类中添加方法/函数，无需function
        sing(music) {
            console.log(this.name + music)
            console.log(this.age + music)
        }
    }

    // 2.利用上方创建的类,来创建对象 new
    var lei = new Start('这是名字','这是年龄')
    console.log(lei) // 输出一个对象

    lei.sing('这是音乐')  //输出新增的函数
```
![](https://image.dcaoao.com/image/202212161923937.png)


1.通过class关键字来创建类,类名习惯性定义首字母大写
2.类创建后其内部有 一个 `constructor`函数 可以接收传递过来的参数,并且返回实例对象
3.`constructor`函数只要new生成实例时,会自动调用这个函数,如果不写这个函数,类也会自动生成函数
4.`new` 用于生成实例,不能省略
5.语法规范  class创建类后,其后面`直接加花括号`  生成实例后面跟小括号 类里面的所有函数`不需要function`
6.多个函数或者方法之间，不需要`逗号`分隔 


## 类的继承
```
<script>
        // 首先使用class创建一个父类
        class Start {
            constructor(x, y) {
                this.x = x
                this.y = y
            }
            sum() {
                console.log(this.x + this.y)
            }
            // 父类与子类中,有着一个相同的函数 say()
            say() { return '这是父类中的函数' }
        }

        // 然后再创建一个子类使用 extends 继承父类的属性
        class End extends Start {
            constructor(x, y) {
                super(x, y)  //super负责将传递到子类的参数传递至父类
            }

            say() {
                console.log(super.say())   //通过子类调用父类中的say函数 输出 这是父类中的函数
            }


            // 子类扩展自己的功能，在父类的有加法的基础上，自己添加一个减法
            subtraction(x,y){
                this.x = x
                this.y = y
                console.log(this.x - this.y)
            }
        }

        //向子类传递参数，达到父类的功能
        var zi = new End(1, 2)
        zi.sum()   // 调用sum函数，成功求值

        // 父类与子类中,有着一个相同的函数 say()

        zi.say()  //这样调用的是子类的say()   因为就近原则

        zi.subtraction(3,2)  //执行减法
        zi.sum(3,2)          //执行加法
</script>
```
类的继承使用 extends  类的传递使用 super
继承中的属性或者方法的查找原则为就近原则
继承中 如果实例化的子类输出一个方法 先看子类有没有这个方法 如果有，则执行子类的
如果子类内没有，则就去父类查找有没有，如果有则执行父类的（就近原则）
super()需要在任何this的最前面调用,确保参数传递至父类


## 使用类的注意事项

```
<script>
    var that;  // 声明一个空值
    // 定义类
    class Start {
        constructor(uname,age){
            that = this;   //这里的this指向实例对象
            this.uname = uname
            this.age = age
            // 添加按钮点击事件
            this.btn = document.querySelector('button')
            this.btn.onclick = this.sing  //需要注意的是，这里调用sing函数不要加括号，否则会被立即调用
        }
        sing(){
            console.log(this.uname)   //这里的this为bth所调用，所以指向了按钮，但是按钮没有uname 所以返回为空
            console.log(that.uname)   //最开始声明的全局变量获取到了constructor内的this值，所以可以直接使用

        }
    }

    // 声明类
    var shengming = new Start('声明')


</script>
```
![](https://image.dcaoao.com/image/202212161927840.png)


1.在ES6中没有变量提升，所以必须先定义类，才能通过类实例化对象
2.在类里面的共有的 属性 方法 一定要加this使用
3.constructor其中的this指向实例对象（new函数产生的对象），方法其中的this 为谁调用就指向谁



# 构造函数创建对象


首先是创建对象的三种方式

利用new Object() 创建对象
```
 var obj1 = new Object()
```

 利用对象字面量创建对象
 ```
 var boj2 = {}
 ```

 利用构造函数创建对象
 ```
         function obj3(uname, age) {
            this.uname = uname
            this.age = age

            // prototype  构造函数原型
            this.sing = function(){
                console.log(666)
            }
        }
 ```

实例化构造函数
```
        var one = new obj3('名字', '年龄')
        var two = new obj3('名字2', '年龄2')
        console.log(one.uname)
```
使用mew关键字调用函数行为被称为实例化
实例化啊构造函数时没有参数时可以省略 `()`
构造函数内部无需写`return` 返回值即为新创建的对象  函数内部的return也无效
## 构造函数拥有实例成员和静态成员
1.实例成员 就是构造函数中,通过`this`来添加的成员 `uname` `age` `sing`就是实例成员  只能通过实例化的对象来访问
```
        console.log(one.uname)
        console.log(one.age)
        one.sing()   //这些都是实例成员，使用实例访问
        console.log(obj3.uname)  // 不可访问 undefined
```

2.静态成员 在构造函数本身上 `添加` 的成员
静态成员只能通过 `构造函数` 来进行访问
```
        obj3.sex = '男'  //这就是一个静态成员 直接添加
        console.log(obj3.sex)   // 男
        // 不可使用实例化对象来访问
        console.log(one.sex)    // undefined
```
静态成员方法中的`this`指向构造函数`本身`
构造函数的属性和方法被称为静态成员

### `Object`静态方法
```
        // 放置一个对象
        const o = {uname:'名字',age:'年龄'}

        // 1.获取所有的属性名  以数组的形式返回 
        const shuxing = Object.keys(o)
        console.log(shuxing)  // ['uname', 'age']

        // 2.获取所有的属性值 以数组形式
        const shuxingzhi = Object.values(o)
        console.log(shuxingzhi)   // ['名字', '年龄']

        // 3.对象的拷贝/追加
        var p = {}   // 声明一个空对象
        // 将 o 对象拷贝至 p 空对象中
        Object.assign(p,o)
        console.log(p)  // {uname: '名字', age: '年龄'}
        // 追加新属性进到p对象中
        Object.assign(p,{sex:'女'})
        console.log(p)  // {uname: '名字', age: '年龄', sex: '女'}
```

## 构造函数原型 `prototype`

每个构造函数都有一个`prototype`属性,  这个`prototype`其实就是一个`对象`,这个对象所拥有的属性和方法,都会被构造函数所拥有,相当于`共享`属性和方法的一个对象

原型的作用是:共享属性和方法  节省内存空间

```
        obj3.prototype.sing = function () {
            console.log('姓名输出')
        }
        // 此刻再次调用方法sing
        one.sing()   //成功输出 姓名输出
        two.sing()   //成功输出 姓名输出
```

原型属性扩展:
每个对象都会有一个属性, `__proto__` 负责指向构造函数中的`prototype`原型对象,相当于起到了一个`转发`的作用
```
console.log(one.__proto__ === obj3.prototype)  // 输出true
```
但是__proto__对象不能直接拿来使用，只能起到一个转发作用

## 构造函数原型 `constructor`

```
// 创建构造函数
        function Start(uname, age) {
            this.uname = uname
            this.age = age
        }

        // 使用构造函数原型共享属性和方法
        Start.prototype.sing = function () {
            console.log(this.uname + '第一个')
        }
        Start.prototype.sing2 = function () {
            console.log(this.uname + '第二个')
        }

        // 实例化构造函数
        var StartOne = new Start('Start名字1', '年龄1')
        var StartTwo = new Start('Start名字1', '年龄2')


        StartOne.sing()  // 名字1第一个


        // 使用constructor获取指向的构造函数
        console.log(Start.prototype.constructor)    // 目前还是指向 Start构造函数
        console.log(Start.prototype)
```
![](https://image.dcaoao.com/image/202212172058526.png)

```
 // 创建构造函数第二个
        function End(uname, age) {
            this.uname = uname
            this.age = age
        }

        // 使用构造函数原型共享属性和方法   与上方不同，这里使用对象来进行存储

        End.prototype = {
            // 使用construction将指向调回
            // constructor:End,
            sing:function(){
                console.log(this.uname + '第一个')
            },
            sing2:function(){
                console.log(this.uname + '第二个')
            }
        }

        // 实例化构造函数
        var EndOne = new End('End名字1', '年龄1')
        var EndTwo = new End('End名字1', '年龄2')


        EndOne.sing()  // End名字1第一个


        // 使用constructor获取指向的构造函数
        console.log(End.prototype.constructor)    
        // 出现异常，因为使用对象存储属性和方法，这里指向了  Object() { [native code] }  并不是End构造函数
```
![](https://image.dcaoao.com/image/202212172113981.png)

需要在`prototype`处,添加`constructor:End`,重新将其指回End函数
![](https://image.dcaoao.com/image/202212172115613.png)

指向恢复正常
![](https://image.dcaoao.com/image/202212172115881.png)


如果我们修改了原来的原型对象,给原型对象赋值的是一个对象,则必须使用 `constructor`来指回原来的构造函数


构造函数 实例 原型对象三者之间的关系图
![](https://image.dcaoao.com/image/202212171535063.png)

原型链示意图
![](https://image.dcaoao.com/image/202212171553618.png)


## JavaScript 的成员查找机制
1.当访问一个对象的属性/方法时,首先查找这个对象自身有没有该属性/方法
2.如果没有查找到,则按照原型链向上查找,也就是` __prtot__ `指向的`prototype`原型对象
3.如果还是没有查找到,继续向上,`Object原型对象`,直至顶部null
4.遵循就近原则


## 关于this的指向问题
在原型对象函数里面的this,指向的是实例对象 谁调用,就指向谁


## call方法 改变this的指向
使用方法:
`函数名.call(要指向的函数,实参,实参)`

`call`方法可以使this的指向改变为另一个函数

```
        // 创建一个函数
        function Start (x,y) {
            console.log('这是一句话')
            console.log(this)
            console.log(x + y)
        }

        var o = {
            name:'名字',
            age:'年龄'
        }
        
        Start.call()   // call调用函数

        console.log('使用call改变this指向对象-------------------')

        Start.call(o,1,2)
```

![](https://image.dcaoao.com/image/202212172121053.png)

### 利用call,使子类继承父类的属性
```
        // 创建父类
        function Father (uname,age) {
            this.uname = uname
            this.age = age
        }


        // 创建子类
        function Son (uname,age,sex) {
            // 利用call,使父类的this,指向子类
            Father.call(this,uname,age)
            this.sex = sex
        }
        var son = new Son('名字','年龄18','男')
        console.log(son)   // Son {uname: '名字', age: '年龄18', sex: '男'}   不仅拥有父类的uname和age，也有自己的sex属性
```
![](https://image.dcaoao.com/image/202212172127740.png)


# 数组方法
## forEach
`forEach`可以迭代/遍历数组 与for循环相比更加简洁

```
        var arr = ['a','b','c','d']    // 创建一个数组

        arr.forEach(function(value,index,array){
            console.log('数组的单独内容' + value)
        })

        arr.forEach(function(value,index,array){
            console.log('数组的索引号' + index)
        })

        arr.forEach(function(value,index,array){
            console.log('数组的所有内容' + array)
        })
```
![](https://image.dcaoao.com/image/202212182302733.png)
## filter
`filter` 可以遍历/筛选数组  将符合条件的数组值取出，重新整合为一个新的数组
如果在数组中查询一个唯一的元素，`filter`比较合适

```
        var abb = [1,2,55,66,99,65,32,68,75]
        var filterAbb = abb.filter(function(value,index){
            console.log(value)   // 数组值
            console.log(index)   // 索引号
            return value > 20    // 筛选出符合条件的数据，整合为新数组  此处筛选出大于20的数值
        })
        console.log(filterAbb)
```
![](https://image.dcaoao.com/image/202212182303788.png)

## some
`some` 查找数组中是否有满足条件的元素 返回`布尔值`  查找到第一个满足条件的元素时，则直接停止循环

```
        var acc = [1,2,55,66,99,65,32,68,75]

        var accSome = acc.some(function(value,index){
            return value > 50   // 查找是否有大于50的数值
        })
        console.log(accSome)   //true
```
## find 
查找数组中第一个符合条件要求的值，如果没有符合要求的则返回为空
```
        const add = [{name:'小米',price:1999},{name:'华为',price:1999},{name:'苹果',price:1999},]
        var Apple = add.find(function(item){
            // console.log(item)  // 输出数组对象中的每一个对象
            // console.log(item.name)  // 输出数组对象中的名字
            return item.name === '苹果'   // 输出符合条件的第一个值
        })
        console.log(Apple)
        // find箭头函数写法
        var AppleJ = add.find(item => item.name === '华为')
        console.log(AppleJ)
```
![](https://image.dcaoao.com/image/202212241955331.png)


## every 
查找数组内的每一个数据是否都符合条件，都符合则返回`true`，不符合返回`false`  返回`布尔值`
```
        const aee = [10,20,30]
        const aeeTrue = aee.every(function(aeeTrue){
            return aeeTrue >= 10
        })
        console.log(aeeTrue)  // true
        // every箭头函数写法
        const aeeFalseJ = aee.every(aeeFalse => aeeFalse <=10)
        console.log(aeeFalseJ)
```

## Array.from()
`Array.from()` 将伪数组转换为真数组
```
        var li = document.querySelectorAll('li')
        console.log(li)
        // 将其转换为真数组
        var zhen = Array.from(li)
        console.log(zhen)
```
![](https://image.dcaoao.com/image/202212241957214.png)

剩下的还有 `map()`   `every()`  也可以做到循环数组，不同的作用
在 `forEach` `some` `filter`中,如果碰到 `return true`  `forEach与filter` 不会停止迭代,`some`会停止迭代

# 字符串方法

## trim,去除左右两侧空格
```
        var a = '          字符串         '
        console.log(a)
        // 去除左右空格
        console.log(a.trim())
```
![](https://image.dcaoao.com/image/202212182305060.png)

## `split` 将字符串转换为数组，需要有分隔符，返回数组

```
        const a1 = 'a-b-c-d-e'
        var a2 = a1.split('-')
        console.log(a2)  // ['a', 'b', 'c', 'd', 'e']
```

## `substring(开始的索引号,结束的索引号)`   截取字符串，不包含索引号的字符
```
        const b1 = '学习前端知识'    // 要求把前端两个字截取出来
        const b2 = b1.substring(2,4)
        console.log(b2)  // 前端
```

## `startsWith('')`  判断字符串是否以特定字符开头
```
        const c1 = '好好学习,天天向上'
        console.log(c1.startsWith('好好学习'))  // true
        console.log(c1.startsWith('学',2))  // true
```

## `includes(搜索的字符串，开始检测的索引号，可省略)`  搜索字符串中有没有特定字符,返回布尔值
```
        const d1 = '头有点疼,大概没羊'
        console.log(d1.includes('点疼'))  // true
        console.log(d1.includes('点羊'))  // false
        console.log(d1.includes('点疼',5))  // false
```

## `toFixed`方法可以让数字保留指定的小数位数,并且`四舍五入`,参数可省略，省略默认为保留0位
```
        const e1 = 100.935
        console.log(e1.toFixed(1))  // 100.9
        console.log(e1.toFixed(2))  // 100.94
        console.log(e1.toFixed())  // 101
```

# 修改或者添加对象值
新方法,使用`Object.defineProperty(obj,'prop',descriptor)`
`obj`:必须 目标对象
`prop` 必须 需要定义或者要修改的属性的名字
`descriptor`: 必须 目标属性所拥有的特性,以对象的形式进行书写 拥有四个值
`value`:设置属性的值,默认为空
`writable`:设置值是否可以重写 `true|false`  默认false
`enumerable`:目标属性是否可以被枚举   `true|false`  默认false
`configurable`:目标属性是否可以被删除,或者可以再次修改特性  ``true|false``  默认false */

```
        var a = {
            name:'名字',
            age:18,
            sex:'男'
        }

        console.log(a)

        Object.defineProperty(a,'name',{
            // 通过value设置属性值
            value:'这是个名字',
            // writable设定其不可被修改
            writable:false,
        })

        a.name = '名字啊'   // 其下方修改过后还是原来的值，不可被修改
        console.log(a)
```

![](https://image.dcaoao.com/image/202212182310817.png)


# 函数的定义以及调用方式

## 函数的定义方式

1.自定义函数(命名函数)
```
function fn() { }
```

2.函数表达式 (匿名函数)
```
        var fun = function () { }
```
3.利用 `new Function('参数1','参数2','函数体')`
```
        var f = new Function('a', 'b', 'console.log(a + b)')
        f(1, 2)
```

4.所有函数都是Function的实例(对象)
```
        console.log(f instanceof Object)  // true
```

## 函数的调用方式

1.普通函数
```
        function fn() { console.log('普通函数') }
        fn()
        fn.call()   //两种方式调用
```


2.对象的方法  在对象内部的函数被称为方法
```
        var o = {
            say: function () { console.log('对象的方法') }
        }
        // 调用
        o.say()
```

3.构造函数
```
        function Start() {console.log('构造函数')}
        // 调用
        new Start()
```

4.绑定函数事件 元素被点击后即可调用
```
btn.addEventListener('click',function(){console.log('绑定函数事件')})
```

5.定时器函数
定时器每隔1s自动调用一次
```
setInterval(function(){console.log('定时器函数')},1000)
```

 6.立即执行函数
 ```
 (function(){console.log('立即执行函数')})();
 ```

 # 函数内部的this指向
 ![](https://image.dcaoao.com/image/202212191334559.png)

 第一个 `call()`
 ## 第二个 `apply()`

 语法:  `函数.apply(指向函数的this值,传递数据)`   其中，传递的数据只能是`数组`形式  伪数组
 ```
         function fn(arr) {
            console.log(this)   //输出this
            console.log(arr)   //输出 apply
        }

        var o = {
            name: '这是个名字'
        }

        fn.apply(o)  //更改fn函数的this指向为o对象

        fn.apply(o, ['apply'])  //更改fn函数的this指向为o对象


        // apply方法的主要作用,取出数组中的最大值与最小值

        const numbers = [5, 6, 2, 3, 7];

        var max = Math.max.apply(null, numbers);
        var min = Math.min.apply(null, numbers);

        console.log(max);
        console.log(min);
 ```

## 第三个  bind()  
绑定 仅改变this指向，不调用函数
语法: `改变的函数.bind(要指向的函数,实参,实参)`

```
        var a1 = {
            name:'a1'
        }

        function afn (a,b){
            console.log(this)
            console.log(a + b)
        }

        var bind = afn.bind(a1)
        bind()   //bind后，实际称为了一个函数 ，使用其调用即可发现指向了a1
        bind(1,2)  //传递实参进去，发现可以正常使用 afn函数求和  得出结果3
```

## call apply bing 总结
call apply bing 总结
相同点:  都可以改变this函数内部指向

区别点:
call与apply会立即调用函数,并且改变函数内部this指向
call和apply传递的参数不同,call传递 字符串,数据等,  apply必须传递数组形式(伪数组)
bind不会调用函数 但是可以改变函数内部指向

主要应用场景:
call经常做传承
apply一般用于数组,比如取数组最大值最小值
bind不调用函数,但是还想改变this的指向,改变定时器内部的this指向之类


# 严格模式
严格模式是ES5之后出现的,寓意为JS代码进行更加严格的运行 比如说未声明,直接赋值,开启严格模式后就不可运行了
严格模式在IE10以上的版本浏览器中才会被支持,旧版本浏览器中会被忽略
1.消除了JS语法的一些不合理,不严谨的地方
2.消除代码运行的一些不安全的地方,包装运行
3.提高编译器效率,增加运行速度
4.禁用了ECMAScript的未来版本中会定义的一些语法,为新版的js做好铺垫 比如一些保留字 `class enum extends inport super`

## 为整个脚本(script标签)开启严格模式 
```
    <script>
        (function(){
            'use strict'
        })()
    </script>
```

## 为某个函数开启严格模式
```
        function fn(){
            'use strict'   //这个函数内的代码就会按照严格模式执行
        }
```

## 严格模式的变化
1.未声明的变量,无法使用
```
a = 1
console.log(a)  //a is not defined
```

2.不能随意删除已经声明的变量

```
var b = 1
delete b    // Delete of an unqualified identifier in strict mode.
```

3.全局作用域中的this,指向的是windows,但是在严格模式下,其指向的是 undefined
```
        function a1 () {
            console.log(this)
        }
        a1()  // undefined
        console.log(this) 
```

 4.严格模式下,如果构造函数不加new使用 this会报错 不加new使用的this，其实是指向了window，但在严格模式下又为空值，所以报错
 ```
         function A2 () {
            this.sex = '男'
            console.log(this.sex)
        }
        // 不加new调用
        // A2()  // Cannot set properties of undefined
        // 加 new 使用
        new A2() 
 ```

5.函数不能有重名的参数
```
        function a3 (a,a) {
            console.log(a + a)
        }
        a3(2,2)   // Duplicate parameter name not allowed in this context
```

### 严格模式扩展
https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Strict_mode 


# 高阶函数
高阶函数就是对其他函数进行操作的函数
它`接收函数作为参数`或者将`函数作为返回值`输出

## 接收函数作为参数:

```
        function fn1 (a,b,callback) {
            console.log(a + b)
            callback&&callback()
        }
        fn1(1,2,function(){
            console.log('函数')
        })

        // 此时 fn1函数就是高阶函数，第三个参数 callback 将函数作为参数操作
```

## 函数作为返回值:
```
        function fn2 () {
            return function() {console.log('函数2')}
        }
        fn2()

        // 这也是高阶函数，返回值为函数
```


# 什么是闭包
 闭包 指有权访问另一个函数作用域中的变量的函数
 一个作用域可以访问另外一个函数内部的局部变量
 ```
         function fn1 () {
            var num = 1

            function fn2 () {
                console.log(num)
            }
            fn2()
        }

        fn1()
 ```

被访问的局部变量所在的函数,被称为闭包函数,在这里,`fn1`为闭包函数

问题
怎么理解闭包:  内层函数 + 外层函数的变量的组合被称为闭包
闭包的作用: 实现数据私有 使内部数据可被外部所访问
闭包有可能引起的问题: 内存泄漏

# 作用域
 作用域分为`全局作用域`与`局部作用域`
 局部作用域又分为`函数作用域`和`块作用域`

 ## 1.函数作用域只能在函数内部声明访问，外部无法访问
 ```
         function hanshu () {
            var a1 = 10
        }
        console.log(a1)  //此处报错
 ```
函数内部声明的变量,函数外部无法访问
函数的参数也是函数内部的局部变量
不同函数内部声明的变量无法互相访问
函数执行完毕后,函数内部的变量实际上被清空了
需要注意的是，如果两个函数嵌套，子函数可以访问父函数的变量，父函数无法访问子函数的变量


## 2.块作用域 :在`javascript`中使用`{}`包裹的代码被称为代码块,
代码块内部声明的变量外部将`[有可能]` 无法访问
```
    for(let i = 1;i <= 3;i++) {
        console.log(i)   //正常输出
    }
    console.log(i)  // 报错
```
let与const声明的变量会产生块作用域,var不会产生块作用域
不同代码块之间的变量无法互相访问
推荐使用let或const

## 全局作用域
`script标签` 与 `.js文件` 就是`全局作用域`,在此声明的变量在函数`内部也可以访问`
为`window对象`动态添加的属性默认也是全局的,不推荐
函数中未使用任何关键字声明的变量为全局变量,也就是未声明,直接赋值的
尽可能少声明全局变量,防止全局变量污染


## 问答:
作用域链本质是什么?
    底层的变量查找机制
作用域链的查找规则是什么?
    就近原则,现在当前函数查找,找不到就去父级,直至全局


# JS垃圾回收机制
![](https://image.dcaoao.com/image/202212201344109.png)
什么是垃圾回收机制:
JS中的内存分配和回收都是自动完成,内存不使用的时候会被垃圾回收器自动回收

什么是内存泄漏:
不在用到的内存,没有及时释放,就叫做内存泄漏

内存声明周期是怎么样的:
内存分配-内存使用-内存回收
全局变量一般不会回收,局部变量使用完毕会被回收

# 动态参数
当不确定函数调用时,会传递多少个参数过来时,可以使用 arguments来实现动态获取参数,获取到的参数是一个`伪数组`形式
```
        function sum() {
            var s = 0
            for(var i = 0;i < arguments.length;i++) {
                s += arguments[i]
            }
            console.log(s)
            console.log(arguments)  // [1, 2, 3,]
        }

        sum(1,2,3)
        sum(1,2,3,4,5,6,7,8,9)
```
![](https://image.dcaoao.com/image/202212212055341.png)


## 问答:
当不确定传递多少个实参时,怎么办
使用 `arguments`获取动态参数

 什么是 arguments?
可以为函数动态的获取传递过来的实参,传递过来的是伪数组,`只存在于函数中`

# 剩余参数
剩余参数适用于至少传递多少个参数的时候,使用率较高
```
        function fn(a,b,c,...d) {
            console.log( a + b + c)
            console.log(d)
        }
        fn(1,2,3,4,5,6)
```
![](https://image.dcaoao.com/image/202212212057599.png)
写在`形参`中,多余的参数会按照`真数组`的形式被返回
`...`是语法符号 置于最末函数形参之前,用于获取多余的实参

问答: 剩余参数的主要使用场景是?
    用于获取多余的实参,组成数组

问答: 剩余参数和动态参数的区别是什么?开发中提倡使用哪一个
    动态参数获取的是伪数组
    剩余参数获取的是真数组
    提倡多使用剩余参数


# 展开运算符
展开运算符可以`展开数组`
```
        // 展开运算符可以展开数组
        const arr1 = [1,2,3]
        const arr2 = [4,5,6]
        console.log(...arr1)
```
![](https://image.dcaoao.com/image/202212212058422.png)

也可以利用数学对象来`求最大值/最小值`
```
        console.log(Math.max(...arr1))  // 得出 3
        console.log(Math.min(...arr1))  // 得出 1
```

也可以合并数组
```
        const arr1 = [1,2,3]
        const arr2 = [4,5,6]
        const arr = [...arr1,...arr2]
        console.log(arr)  // [1, 2, 3, 4, 5, 6]
```
![](https://image.dcaoao.com/image/202212212059134.png)

问答: 展开运算符的主要作用是
    可以把数组展开,利用数学对象 Math 来求最大值与最小值 展开的数组默认拥有逗号分隔
        
问答: 展开运算符与剩余参数有什么区别
    书写位置不同,在函数形参括号内,为剩余参数,在函数外部则为展开运算符
    展开运算符主要是 数组展开
    剩余参数用于在函数内部使用


# 箭头函数
箭头函数一般用于简化代码结构

## 箭头函数`基本语法`:
```
        const fn = (name, age) => {
            console.log(name, age)
        }
        fn('名字', 18)
```

## 当只有一个参数时,小括号可以省略
```
        const fn1 = name => {
            console.log(name)
        }
        fn1('只有一个参数')
```

## 当只有一行代码是,大括号可以省略，而且无需 return就可以返回值
```
        const fn2 = name => console.log('只有一行代码' + name)
        const fn3 = name => '可以直接输出结果,无需 return'
        fn2(' 对,只有一行')
        console.log(fn3())
```

## 箭头函数可以直接返回一个对象，使用小括号包含对象即可
```
        const fn5 = name => ({ uname: name })
        console.log(fn5('返回对象'))  // {uname: '返回对象'}
```
![](https://image.dcaoao.com/image/202212212102596.png)

    箭头函数属于表达式函数,所以不需要考虑函数提升
    箭头函数只有一个参数时可以省略圆括号()
    箭头函数体只有一行代码时可以省略花括号{},并自动作为返回值被返回
    加括号的函数体可以返回对象字面量表达式

## 利用箭头函数求和

```
        const fn6 = (...arr) => {
            var sum = 0
            for (var i = 0; i < arr.length; i++) {
                sum += arr[i]
            }
            return sum
        }
        var fnsum = fn6(1, 2, 3)
        console.log(fnsum)
```

## 箭头函数的this
 箭头函数`不会创建自己的this`,只会从自己的`作用域链的上一级`沿用this
 ```
         const fn7 = () => {
            console.log(this)  // 指向window
        }
        fn7()
 ```

## 对象方法箭头函数的this
```
        const obj1 = {
            uname: '名字',
            sayHi: () => {
                console.log(this)  // 指向obj，obj又其实指向window，所以指向window
            }
        }
        obj1.sayHi()
```

## 嵌套箭头函数this的指向
```
        const obj2 = {
            uname: 'OBJ2',
            log: function log() {
                const sayHi = () => {
                    console.log(this)  // 指向普通函数 log ，log是传统函数，谁调用就指向谁，所以指向obj2
                }
                sayHi()
            }

        }
        obj2.log()  
```

    问答: 箭头函数里面有this吗
    箭头函数不会创建自己的this,只会从自己的作用域链的上一次沿用this
        
    问答: DOM事件回调函数推荐使用箭头函数吗
    不推荐,特别是需要用到this时,事件回调函数使用箭头函数时,其指向的this是window

# 数组解构
数据解构,可以将多个变量批量赋值
```
        const arr = [1,2,3,4,5,6]
        const [max1,max2,max3, ,max5] = arr
        console.log(max1)  // 1
        console.log(max2) //2
        console.log(max3) //3
        console.log(max5) //5
```
## 多维数组解构
```
        const arr1 = [1,2,3,4,[5,6,7]]
        const [a,b,[c,d]] = [1,2,[3,4]]
        console.log(a)
        console.log(b)
        console.log(c)
```
## 使用数组解构交换两个变量值
```
        var a1 = 1
        var b1 = 2;   // 其中 数组解构的[]前面，必须要加分号分隔，与上行代码分开   ;[]
        [b1,a1] = [a1,b1]
        console.log(a1,b1)  // 2 1
```
问答: 数组解构的作用是什么
    将数组的值快速批量的赋值给元素
问答: JS前面有那两种情况需要加分号
    立即执行函数需要分号分隔
    数组解构前方需要分号分隔
问答: 变量的数量大于数组的数量是,多余的变量将被赋值为?
    赋值为空      
问答: 变量的数量小于数组的数量时,可以通过什么来获取剩余所有的值?
    剩余参数,但只能置于最末尾 

# 对象解构
 可将对象中的变量名批量赋值,但是要求属性名与变量名相同

 ```
        const obj = {uname:'名字',age:18}
        const {uname,age} = {uname:'名字',age:18}
        console.log(uname)
        console.log(age)
 ```
等价于 
const uname = obj.uname

## 给对象解构的变量名重新命名
```
        const {uname:username,age:ages} = {uname:'名字-重新命名',age:'18-重新命名'}
        console.log(username)
        console.log(ages)
```

## 对象数组解构
```
        const obj2 = [{a:'A1',b:'B1'}]
        const [{a,b}] = obj2
        console.log(a,b)
```

## 对象解构赋值案例
```
        const pig = {name:'佩奇',name2:'查理'}
        // 将其解构,并打印出值
        const {name,name2} = pig
        console.log(name,name2)

        //将pig对象中的name，通过对象解构改为unames，并且打印输出
        const {name:unames} = pig
        console.log(unames)
```

# 多级解构
## 多级对象解构
```
        const arr1 = {name1:'名字1',name2: {name3:'名字3'}}
        // 解构
        const {name1,name2:{name3}} = arr1
        console.log(name1,name3)
```

## 多级对象数组解构
```
        const arr2 = [{name5:'名字5',name6: {name7:'名字7'}}]
        // 解构
        const [{name5,name6:{name7}}] = arr2
        console.log(name5,name7)
```