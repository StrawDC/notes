---
title: JS学习记录
tags:
  - 学习
index_img: 'https://image.dcaoao.com/image/202210282111277.webp'
banner_img: 'https://image.dcaoao.com/image/202210282111277.webp'
abbrlink: 902688608
date: 2022-10-27 10:00:00
---

## 10月27号 交换两个变量值笔记 ##
## 交换思路 ##
首先是交换前的思路：需要把A1变量值交换到A2变量值，A2变量值交换到A1内，那就需要有个第三者来辅助这俩交换



## 实际操作 ##


```
#首先声明三个变量：A1,A2,kong
# kong变量只声明 不赋值
var A1 = 1,
	A2 = 2;
var kong;


#然后将A1内的值，先交换到kong内
kong = A1
#此时A1是空出来的状态，那就把A2塞到A1里边去
A2 = A1
#现在A2空出来了 kong里边还蹲着原先A1的值，把他送进A2里边
A2 = kong

#最后输出到控制台看看

console.log(A1)
console.log(A2)
```
## 结果 ##

结果图：
![](http://image.dcaoao.com/image/202210281458332.webp)



## 笔记 变量名命名规范:     ##

     严格区分大小写
     不能以数字开头
     只能大写小写下划线和$
     不能是关键词或者保留字 var for之类
     变量名必须有意义 实在不行用翻译网站吧
     遵循驼峰命名法 首字母小写 后边的统统大写 nameTopRight
     name有特殊含义，尽量不要使用


    为什么需要变量：因为有数据需要保存
    变量是什么：变量是一个容器，存放数据，方便调用
    变量的本质是什么：申请内存中的一块空间
    变量怎么使用：先声明，再赋值
    什么是变量的初始化：声明并赋值就是初始化
    变量命名规范？：看上边
    交换两个变量的思路？，需要一个空变量来辅助，1交换到2 3交换到1 最后2交换到3来实现1和3的变量值互换


```
#JS的变量数据类型，只有在程序运行中才可以确定类型，根据变量值来确定的

var A1 = 10；  #这是一个数字型
var A2 = '阿巴阿巴'; #这是一个字符串类型
```

但是，在JS中，JS是动态语言，变量的数据类型是可以变化的
```
var A1 = 10；  #这是一个数字型
A1 = '阿巴阿巴';
```
这样A1变量就会更改为字符串类型


## 10.29号笔记

## 字符串拼接和检测字符串长度 ##

首先是检测字符串的长度,使用的是 `length` 变量
```
#首先声明并赋值一个变量
var my1 = '我的天哪,看看这句话'
#然后检测变量长度并输出
console.log (my1.length)
#这样会把这句话的字符串长度输出至控制台
```

## 字符串拼接 ##

```
console.log('1' + '1')  #字符串与字符串相加,还是字符串  结果为11
console.log('1' + 1)  #字符串与数字相加,还是字符串  结果为11
console.log(1 + 1)  #两者都是数值型 数值型相加   结果为2
console.log('学习' + 'JS')  #字符串与字符串相加 结果为学习JS
console.log('学习' + 66)  #字符串与数值型数据相加,还是字符串类型 结果为 学习66
```

字符串拼接小结:字符串与任何类型数据拼接,结果都是字符串类型



## 数据类型 ##

```
#首先是八进制在JS中的写法,八进制在JS中默认为0开头的就是八进制数值
var my1 = 010;
console.log(my1)   #这样输出的结果为8


#十六进制的写法和八进制稍有不同  只要变量值为0x开头的,默认就是十六进制
var my2 = 0xa
console.log(my2)  #这样输出的结果为10

#JS中最大值与最小值 仅做了解
console.log(Number.MAX_VALUE)  #最大值
console.log(Number.MIN_VALUE)  #最大值

#无穷大与无穷小  Infinity
console.log(Infinity)  #无穷大
console.log(-Infinity)  #无穷小
console.log('字符串类型' - 100)  #需要注意的是字符串类型与数值型数据进行计算,会得到结果 NaN 代表非数值

#判断是否非数字 isNaN
console.log(isNaN(12))  #如果发现是数字,那就返回值false
console.log(isNaN('12'))  #如果发现不是是数字,那就返回值true

#字符串类型

var my3 = '这是一个字符串类型 \n 的文字'   #字符串类型的文字一般使用单引号 '  或者双引号 " 来包裹
                                    #可以使用换行符等转义符,引号包裹内单外双,或者外双内单

#转义符：
    #换行符：\n
    #斜杠：\\
    #单引号：\'
    #双引号:\"
    #TAB缩进：\t
    #空格:\b 

#一个小案例
 alert('酷热难耐\n 审视四周\n豪气冲天\n“收狗，收大狗，收大猫"\n"收鸡，收鸭，收鹅，收扁嘴"')

 ```
 案例结果:
 ![](https://image.dcaoao.com/image/202210292014727.webp)

 ```
##接下来就是true和false
var my1 = true  #声明true和false两个变量值
var my2 = false

#在JS计算当中,true的值默认为1 false的值默认为0
console.log(my1+ 1)  #结果为2
console.log(my2+ 1)  #结果为1

#null 存储为空
var my3 = null;
console.log (my3 + 1)   #空值与+相加 结果为1
#如果是字符串与空值相加,那还是字符串
#同理,与上方true相加的话,结果为2

#只声明 不赋值 也是空值
var my5;
console.log(my5)  #这样输出的结果为undefined
console.log(my5 + '拼接')  #这样输出的结果为 undefined拼接 因为是字符串与空值拼接
console.log(my5 + 1)  #至于空值与数值型数据相加 那就会返回结果为 NaN 非数值
 ```


 ## 获取变量的数据类型 typeof ##
使用`typeof`来判断数据类型

```
console.log(typeof 10 ) #输出 number 数值型
console.log(typeof '10') #输出 string 字符串类型
console.log(typeof true) #输出 boolean 布尔型
console.log(typeof undefined) # 空值还是输出空值 undefined
console.log(typeof null)  //输出 objest  这个null比较特殊
```
结果:
![](https://image.dcaoao.com/image/202210292114372.webp)


需要注意的是 `prompt`输入过来的数据,默认是字符串类型的


控制台输出的数据颜色代表着不同的数据类型,可以通过控制台数据不同颜色来判断数据的类型
控制台输出的颜色
浅蓝色：数值型
黑色：字符串型
蓝色：布尔型
灰色：空值
![](https://image.dcaoao.com/image/202210292118055.webp)


## 变量数据的类型转换 ##

### 数值型转换为字符串 ###

```
# 使用变量 .toString  需要严格遵守大小写
var my1 = 1;  #现在它是数值型
var my1 = my1.toString();   #现在就不是了,被残忍的更改为了字符串类型

#或者使用 String();  可强制转换为字符串类型
console.log(String(my1))

#再或者使用拼接字符串的特性,字符串与任何数据拼接都是字符串类型
console.log(my1 + '')  #直接拼接一个空的字符串
```
![](https://image.dcaoao.com/image/202210292126988.webp)
之前学习过,数值型在控制台的颜色是浅蓝色,现在是灰色,证明是字符串类型


### 将字符串转换为数值型 ###

```
#1.使用变量parseInt
console.log(parseInt('123px阿巴阿巴')) #输出120,只能取整数
console.log(parseInt('123.6')) #如果带有小数,则只输出123 小数直接舍弃,不四舍五入
console.log(parseInt('a123.6')) #如果是字母开头那就拉胯了,不会取值 直接输出结果为 NaN 非数值

#2.使用变量parseFloat 也是需要注意大小写
console.log(parseFloat('123.6'))  #输出结果123.6
#使用结果与parseInt几乎相同,不同的地方就是可以输出小数 浮点数

#3.使用Number() 
console.log(Number(123.6))  #可以完整输出小数浮点数

#4.使用算数运算符来隐形更改为数值型
console.log('123.6' - 0)    #添加运算符后,会被转换为数值型
console.log('123.6' * 1)    #减法使用0即可,乘法和除法使用1
console.log('123.6' / 1)
```

## 10.30号笔记 ##
### 将字符串转换为布尔型 ###

使用函数 Boolean() 代表空的值 否定的值都会被转换为false 其他的都会被转换为true

```
#空值会被输出为false
console.log(Boolean(0))
console.log(Boolean(''))
console.log(Boolean(NaN))
console.log(Boolean(null))
console.log(Boolean(undefined))

#只要有数据,就会被转换为true
console.log(Boolean(1))
console.log(Boolean('123'))

#小案例

var my2 = prompt('请输入您的姓名')
var my3 = prompt('请输入您的性别')
var my5 = prompt('请输入您的年龄')
alert( '您的姓名是:' + my2 + "\n您的年龄是:" + my5 + "\n您的性别是:" + my3 )
    
```


## 算数运算符 ##

```
#算数运算符 遵循先乘除 后加减,优先括号内的原则
console.log(1 + 1)   #结果 2
console.log(1 - 1)   #结果 0
console.log(1 * 1)   #结果 1
console.log(1 / 1)   #结果 1

#取余操作  除法运算后余下的数
console.log(8 % 4)  #0
console.log(8 % 7)  #1
console.log(7 % 8)  #7

// 浮点数 算数运算中的小数奇数运算会有问题 JS中小数最高精度为17位
console.log(0.1 + 0.2)  //0.30000000000000004
console.log(0.07 * 100) //7.000000000000001

//比较  不能拿浮点数进行比较 尽量避免
var my1 = 0.1 + 0.2;
console.log(my1 ==0.3)  //询问my1是否等于0.3  答案是false

```

### 表达式和返回值 ###
表达式就是由数字 运算符 变量等组成的式子叫表达式
在程序中，结果在左，表达式在右

```
    console.log(1 + 1)
    //在程序中，结果在左，表达式在右
    var my2 = 1 + 1;
```


### 前置自增运算符 ###

```
//首先是传统的做法
var my1 = 1
my1 = my1 + 1
console.log(my1)  //结果等于2

```

这样的写法不仅麻烦还繁琐

```
    // 前置自增运算符   先自加1，后出结果
    var my5 = 1
    ++my5;  //与上方的my1 = my1+1效果相同   这里等于my5 = my5 + 1
    console.log(my5)  //结果为2
    --my5;   //这是前置递减用法，用法与前置递增相同
    console.log(my5)

    //小例子
    var my6 = 1
    console.log(++my6 + 10)  //12
```

### 后置自增运算符 ###
```
//后置自增运算符 先返回原值，在自加1
var my7 = 1
my7++;
console.log(my7)  //此时,结果为2

//但是如果参与了运算

    var my8 = 1
    console.log(my8++ + 10)  //这样的结果为11 因为先返回了原值 1
```

自增运算符案例
```
//前置自增案例
var a = 10;
++a;      //前置自增,当前a等于11
var b = ++a + 2  //a再次自增  ++a当前为 12   12+2=14
console.log(b)    //结果为14

//后置自增案例
var c = 10;
c++;        //后置自增 ,当前值为11
var d = c++ + 2;   //再次后置自增  先输出原值:11  11+2 结果为13
console.log(d)      //13


//综合案例
var e = 10;
var f = e++ + ++e;  //先后置自增, e++输出原值:10 加上前置自增,到++e时原值已经变为11 再次+1   ++e输出值为12
console.log(f)      //输出结果 10+12=22

```

## 比较运算符 ##

比较运算符只会输出布尔值 true与false
```
大于 >
小于 <
大于等于 >=
小于等于 <=
不等于 !=
等于 ==      //有隐形转换,会将字符串类型转换为数值型
全等于 ===   //意思是数据类型与数值需要完全相等


console.log(3 >= 5)  //false
console.log(3 <= 5)  //true
console.log(3 == 3)  //true
console.log(3 == 5)  //false
console.log(3 == '3') //true  判断是否相等有隐形转换 将字符串类型转换为数值型
console.log(3 != 3)  //判断3是否不等于3 返回false
console.log(3 === 3)  //全等于 要求数据类型 数值完全相同
console.log(3 === '3') //false
console.log('吴彦祖' == '刘德华') //false


//案例
var num1 =10;
var num2 = 100;
var res1 = num1 > num2;   //输出false
var res2 = num1 == 11;    //输出false
var res3 = num1 != num2;   //输出true
```


## 逻辑运算符 ##
逻辑运算符与比较运算符一样,只会输出布尔值

### 逻辑与 ###
```
    //逻辑与  &&  一假全假，全真为真
    console.log(1 > 2 && 2 > 1) //false && true  结果为false
    console.log(3 > 2 && 2 > 1) //true && true  结果为true
```

### 逻辑或 ###
```
//逻辑或 ||  一真全真 全假则假
console.log(1 > 2 || 2 > 1) //false || true  结果为true
console.log(1 > 2 || 0 > 1) //false || true  结果为false
```

### 逻辑非 ###
```
//逻辑非 not ！   取反符，布尔值的
console.log(!true);    //不是true  输出结果为false
console.log(!false);    //同理 不是false 输出true
```

## 10.31笔记 ##

## 短路运算 逻辑中断 ##
### 短路运算 逻辑与 ###
在逻辑与的短路运算中，如果表达式1为真，则返回表达式2
```
    console.log(true && false)  //这样的结果是false
    console.log(123 && 456)  //这样的结果是456
```

如果表达式1为假，则返回表达式1，空值同理
```
    console.log(0 && 456)  //返回0
    console.log(0 && 132 * 456 - 789)  //这样的结果也是0
```

### 短路运算 逻辑或 ###
逻辑或的短路运算  如果表达式1为真，则直接返回表达式1，后面的表达式不参与运算
如果表达式1为假,那后面的表达式则参与运算,返回表达式2
```
    console.log(123 || 456)  //结果123
    console.log(0 || 456 + 1)  //结果457
```


逻辑或短路运算案例

```
    var my1 = 0;
    console.log(123 || my1++)  //因为表达式1为真，则表达式2直接不参与运算，此时输出123
    console.log(my1)            //0
```


## 赋值运算符 ##

自增运算符,每次自增只能自增1 
my1++   ++my1 之类
```
var my1 = 1;  #这个叫直接赋值
```

设定赋值运算符,可以做到每次 + - * / 后再赋值

```
var my2 = 1;

my2 += 5;         #自增5   my2 = my2 + 5
console.log(my2)  #结果为6
my2 -= 5          #自减5  my2 = my2 -5
console.log(my2)  #结果为1
my2 *= 6;         #每次乘6后赋值 my2 = my2 * 6
console.log(my2)  #结果为6
my2 /=2;          #每次除2   my2 = my2 / 2
console.log(my2)  #结果为3
my2 %=2;          #以2取余  my2 = my2 % 2
console.log(my2)  #结果为1

```


## 运算符优先级 ##
简单来说还是先乘除 后加减 括号优先 逻辑与在前 逻辑或在后

![](https://image.dcaoao.com/image/202210311303456.webp)

运算符优先级

1. 小括号 `()`
2.一元运算符  `++ -- !`
3.算数运算符  先 `* / % `后 `+ -`
4.关系运算符  `> >= < <=num`
5.相等运算符  `== != === !==`
6.逻辑运算符  先 `&&` 后` ||`
7.赋值运算符  `=`
8.逗号运算符  `, `

    
```
    // 运算符优先级案例
    console.log(false ||         true     &&         true    && true)
    console.log(4 >= 6 || '人' != '阿凡达' && !(12 * 2 ==144) && true)  //结果为true，因为逻辑与优先级比逻辑或高

    var num = 10;
    console.log(5 == num / 2 && (2 + 2 * num).toString() === '22')
    console.log(   true      &&             true                 )      //结果为true
```

## IF语法的结构 ##
if语句中 如果表达式为真,则运行if大括号内的语句
如果表达式为假,则直接跳过该if语句内的表达式运行
if语句后面可以跟一个 else语句,意思是if表达式为否时,改语句执行

### if与else ###
```
    var age = prompt('请输入您的年龄')
    if (age >= 18) {    //如果 age大于等于18
        alert('恭喜您,允许进入网吧')
    } else {        //else的意思是 否则
        alert('未成年不准进入网吧')
    }
```
## 11.01笔记 ##
### if else if ###
如果第一个if没有满足条件,则跳过这个if语句,去执行下一个,如果还是不满足,则继续下一个if

多选一的关系
如果条件表达式1不满足,则检查条件表达式2,如果条件表达式2也不满足,则执行条件表达式3

如果所有条件表达式都不满足,那执行结尾的else

```
    if (1 == 2) {
        alert('1不等于2')
    } else if (2 == 3) {
        alert('2等于2')
    } else {
        alert('都不满足')
    } 

```

## 三元表达式 ##
三元表达式中的条件判断如果为true 则返回表达式1 ,如果判断为false 则返回表达式2
也是多选一的关系

```
var num = 10;
var res num > 5 ? '是的' : '不是'
alert (res)    //因为num大于10,结果为true 所以返回  是的

```

## Switch语句 ##
Switch语句也是多选一的关系,但是适合条件比较多的时候
如果switch中的值与case后的结果符合,则执行符合的那一条表达式
如果都不符合，则执行最后的default
switch表达式的值与case的值为全等的关系 === 也就是说数据类型和内容必须完全相等才可以
如果没有写break来进行结束，则会连带执行下一条表达式，不管符不符合
在实际开发中，switch表达式一般单独写成一个值

```
var my1 = prompt('请输入水果名称')
switch (my1) {
    case '苹果':
        alert ('苹果一块大批发啦')
    break;
    case '香蕉': 
        alert('香蕉包邮到家门口啦')
    break;
    case '菠萝':
        alert('菠萝白送啦')
    break;
    case a1:
        alert('这是一个al')
    break;

    default:alert('没有符合条件的,下次一定')
}

```

运行效果
![](https://image.dcaoao.com/image/202211012203507.gif)



## for循环 ##
循环分为四大部分
for (初始化变量;条件表达式;操作表达式) { 循环体 }

初始化变量:在循环中只会执行一次,使用var声明的一个普通变量 一般作为计数器使用
条件表达式:决定每一次循环后,循环是否会继续执行,也就是结束条件
操作表达式:每次循环都会执行一次,注意是每次循环,配合初始化变量进行更新(一般递增或递减)

执行顺序:
1.首先执行一次`初始化变量`
2.检查`条件表达式`来确定是否要执行循环
3.如果`条件表达式`符合条件,则执行一次`循环体`
4.执行过`循环体`后,再去执行一次`操作表达式`
5.一套循环已经完成,接下来继续检查`条件表达式`是否满足条件,满足条件则继续循环
```
    //解析 执行i等于1 然后检查i是否小于等于100
    //如果小于100 执行一次控制台输出123 
    //然后再为i变量后置自增一次 */
    for (var i = 1; i <= 100;i++) {
        console.log('123')

    }
```

### for循环案例 ###
做一个学生成绩查询的案例,需要最后输出班级人数,班级总分数,班级平均分

```
//首先要求用户输入班级总人数
var total = prompt ('请输入班级总人数')
//然后使用for循环弹出相应的输入框要求输出每个人的成绩
//然后声明一个总成绩空值
var totalresults = 0
for (var i = 1;i <= total ;i++) {
    var results = prompt ('请输入第' + i +'个学生的成绩')
    //然后总成绩将每次循环的成绩相加保存,但是prompt输入过来的字符是字符串格式,还需要转换为数值
    totalresults += Number(results)
} 

// 然后输出平均分,总成绩,班级人数
alert('班级的总人数是' + total + '人')
alert('班级的总成绩是' + totalresults + '分')
alert('班级的平均分是' + totalresults / total + '分')
```
效果图
![](https://image.dcaoao.com/image/202211082124607.gif)
## 11.07记录 ##
## for循环执行不同的代码 ##
for循环可以使用if else 来执行不同的代码,输出不同的值
```
    for (var i = 1 ; i <= 100 ; i++) {
        if (i == 1) {
            console.log('这是第1圈循环')
        } else if (i == 100) {
            console.log('这是第100圈循环')
        } else {
            console.log('循环次数' + i)
        }
    }
```
## 双重for循环 ##
for循环可以嵌套,外层循环一次,内层循环全部

```
for (var i = 1 ; i <= 10 ;i++) { 
    for (var k = 1 ;k <= 10 ; k++) ( 
        console.log('内层的输出')
    )
}
```

结果就是,内层循环先在控制台输出十遍`内层的输出`,然后再回到外循环,然后再输出十遍`内层的输出`,往返10次,直到外层循环完成

### 双重for循环案例 ###
#### 案例,输出五行五列的星星符号 ####
```
//首先定义一个空值
var xing = ''
//外循环
for (var i = 1;i <= 5 ;i++) {
    //内循环
    for (var k = 1;k <= 5 ; k++ ) {
        xing += '☆'
    }
    xing += '\n'
}
console.log(xing)

```

解读:首先看内循环,内循环因为for双重循环的特性,外循环执行一次,内循环就要执行五次
现在内循环给出的是一颗`☆`,循环五次过后变为 `☆☆☆☆☆` 也就是一行
那继续执行下去,外循环执行五次后,得到了25颗星星,但是效果不对
![](https://image.dcaoao.com/image/202211082041137.webp)
要求的是五行五列,但是现在为一列,说明缺少换行符号
那就在内循环出五颗星星后,在其后方添加一个换行符
`xing = xing + '\n'`
`xing += '\n'`
两者皆可,最后在循环外输出结果,得到想要的答案
![](https://image.dcaoao.com/image/202211082044473.webp)

#### 案例,输出倒三角的星星图案 ####
首先是示例图
![](https://image.dcaoao.com/image/202211082046226.webp)
第一层十颗星星,第二层九颗星星,以此类推
```
//声明空值,方便调用
var xing = ''
            for (var i = 1 ;i <= 10 ;i++) {
                for (var k = i ;k <= 10; k++) {
                    xing += '☆'
                }
                xing += '\n'
            }
            console.log (xing)
```

解读:第一层需要十颗星,那就叫内层循环首次循环直接输出一排十颗的星星,所以`k <= 10`
内层循环的`k`值是取外层循环的`i`值,也就是说,外层第一次循环,内层会循环十遍,也就输出一排10颗星,在内循环其后面添加一句`xing += '\n'`达到每次内循环完成后换行的目的

外层第二次循环后,i值变为了2,那内循环的`k`值是取的`i`,则内循环这次会循环九次,输出九颗`☆`,再次换行,以此类推

至于正三角的话更简单,首次内循环只可循环一次,然后按照循环次数增加
将内循环更改为
```
                for (var k = 1 ;k <= i; k++) {
                    xing += '☆'
                }
```
这样内循环首次循环时,一次便会停止,外循环第二次循环后,内循环便会循环两次,以此类推
![](https://image.dcaoao.com/image/202211082108719.webp)

## 11.10记录 ##

## while循环 与 do while循环 ##

### while循环 ###
`while`循环与for循环稍有不同
`while`的循环,先声明一个`计数器`,循环停止条件在小括号内,计数器循环写在循环内
当条件表达式为`true`,则执行循环,如果为`false`,则退出循环
```
        var i = 1
        while (i <= 100) {
            console.log('输出语句')
            i++;
        }
```

while循环案例,可以执行判断条件比较复杂的语句

```
        var a = prompt('请输入前端二字')
        while (a !== '前端') {
            a = prompt('请输入前端二字')
        }
        alert('好滴很')
```

### do while循环 ###
`do while` 会先执行一次循环体,然后再判断条件表达式,
如果为`true`,则继续循环,如果为`false`,则退出循环
格式:
```
        var a = 1
        do {
            console.log ('这是循环体')
            a++
        } while (a <= 100)
```

do while 案例 打印1-100的整数和
```
         var b = 1
         var c = 0
         do {
            c += b
            b++;
         } while (b <= 100)
         console.log (c)
```

## continue跳出当前循环 ##
continue,只要出现,则跳过本次循环,执行下一次循环
```
        for (var i = 1;i <= 5;i++) {
            if (i == 3 ) {  //使用IF语句，表明只要i等于3的时候，就跳出当前循环
                continue;   //跳出当前循环，执行下一次循环
            }
            console.log ('这是第' + i + '次循环')
        }
```
结果:第三次循环被跳过,直接执行第四次循环
![](https://image.dcaoao.com/image/202211111913091.webp)

### continue 跳出循环案例 ###
案例，求1-100之间，除了能被7整除以外的整数和
使用if语句，如果取余7结果后为0的,一律跳过当前循环
```
        var num = 0
        for (var k = 1;k <= 100;k++) {
            if (k % 7 ==0) {
                continue;
            }
            
            num += k;
        }
        console.log(num)
```

## break 跳出整个循环##
直接跳出整个循环,不在执行下一次的循环,整个循环直接结束

```
        for (var a = 1;a <= 5 ;a++) {
            if (a == 3) {
                break;  //当a等于3,直接退出整个循环,不再执行循环任务
            }
            console.log('循环' + a + '次')
        }
```

结果:只循环了两次
![](https://image.dcaoao.com/image/202211111916830.webp)

## 数组的使用 ##
数组，是一组数据的集合，可将多个数据储存在单个变量下
创建数组有两种方式 new与数组字面量

### 创建数组 ###
使用new创建数组
```
var arr = new Array();  //创建一个空数组,A要大写,使用Array
```

使用数组字面量创建数组
```
var abb = [];  //使用方括号
```

声明数组并赋值被称为数组的初始化
```
var abb = [1,2,3,'字符串类型',true];  //数组内和存在多个不同的值，被称为数组元素，使用逗号分隔
```

### 获取数组内的元素 ###
格式 `console.log(数组名[数组索引号])`
```
        console.log(abb[0])  //会输出数组内第一个值
        console.log(abb[1])  //会输出数组内第二个值，以此类推，索引号从0开始
        console.log(abb[3])  //会输出数组内第三个值，以此类推，索引号从0开始
        console.log(abb[5])  //因为没有这个值，所以会输出空值
```

### 遍历数组，将数组内的元素全部输出出来 ###
```
        var acc = ['刘备','张飞','关羽','马超','赵云','诸葛亮','吕蒙']
        for (var i = 0 ;i < 7 ; i++){  //因为数组索引从0开始，所以i = 0，因为从0开始，输出小于7的，所以 < 7 
            console.log(acc[i])
        }
```
![](https://image.dcaoao.com/image/202211111934846.webp)
### 动态获取数组内的元素长度/个数 ###
```
        var add = ['刘备','张飞','关羽','马超','赵云','诸葛亮','吕蒙']
        console.log(add.length)  //输出为7
        //数组的长度是元素格式，并非元素索引号，而且可以动态检测数组的元素个数
```

### 案例，求数组元素的和及其平均值 ###
```
        var aee = [6,6,1,7,6]
        var num = 0
        for (var a = 0;a < aee.length ;a++) {
            num += aee[a]
        }
        console.log('数组和:' + num)
        console.log('数组平均值:' + num / aee.length) 
        //如果想要输出多个变量，使用逗号分隔即可
        console.log(num,num / aee.length)
```
![](https://image.dcaoao.com/image/202211111935787.webp)
### 案例，求数组中的最大值 ###
```
        var aff = [6,9,8,12,66,33,99,100,69]
        var max = aff[0] //首先声明数组内第一个值
        for (var b = 0; b < aff.length ; b++) {
            if (aff[b] > max ) {
                max = aff[b]
            }
        }
        console.log('数组内最大值为' + max)
```

![](https://image.dcaoao.com/image/202211111935706.webp)
### 案例，将数组转换为字符串类型，并且使用 | 符号分隔 ###
```
        var str = ''  //首先声明一个空值用来存储
        var aee = ['red','blue','green','skyblue']
        for (var c = 0;c < aee.length ;c++) {
        str += aee[c]  + '|';
        }
        console.log(str)
```
![](https://image.dcaoao.com/image/202211111935583.webp)
### 新增数组元素 ###
有两种方法 修改length的长度与修改索引号
1.修改length长度
```
        var agg = ['刘','关','张']
        agg.length = 5
        console.log(agg[3])  //会输出空值 undefined
```
2.修改索引号
```
        var ahh = ['刘','关','张']
        ahh[3] = '李'
        console.log(ahh[3])   //数组内没有索引号为3的，追加过后出现了

        //注意，如果直接给数组或者已有的数组索引赋值，则原有数据会被覆盖
        ahh[3] = '秦'
        console.log(ahh[3])  //输出：秦
```

### 案例 数组使用循环存放1-100的数值 ###
核心原理：使用for循环来追加数组
```
        var aii = []
        for (var d = 0;d < 101;d++) {
            aii[d] = d
        }
        console.log(aii)
```

结果:
![](https://image.dcaoao.com/image/202211122103158.webp)

追加 筛选大于10的数放入新数组

```
        var ajj = []
        var h = 0
        for (var f = 0 ; f < aii.length ;f++) {
            if (aii[f] < 10) {
                continue;
            } else {
                ajj[h] = aii[f]  //数组需要从0开始，循环外声明一个新值 h ，依次递增
                h++
            }
        }
```

![](https://image.dcaoao.com/image/202211122116897.webp)

```
        //筛选方法2
        var ajj = []
       
        for (var f = 0 ; f < aii.length ;f++) {
            if (aii[f] < 10) {
                continue;
            } else {
                ajj[ajj.length] = aii[f] //不使用新数值，直接使用新数组的length长度，从0开始
            }
        }
        console.log(ajj)
```

### 案例 数组去除指定重复值 要求去掉重复值 0 ###
```
        var akk = [66,33,88,0,55,2,0,56,96,58,96,36,0]
        var all = []
        for (var k = 0 ;k < akk.length ; k++) {
            if (akk[k] != 0) {
                all[all.length] = akk[k]
            }
        }
        console.log(all)
```
![](https://image.dcaoao.com/image/202211122116695.webp)

### 案例 将数组翻转/倒序显示 ###
```
        var akk = ['刘','关','张']
        var amm = []  //声明一个空数组
        var k1 = akk.length - 1
        for (k = 0 ;k < akk.length;k++) {
            amm[k] = akk[k1]
            k1--;
        }
        console.log(amm)
```
翻转另一种写法 简练
```
        var akk = ['刘','关','张','李','铠甲勇士','豌豆射手']
        var ann = [] 
        for (var l = akk.length - 1;l >= 0;l--) {
            ann[ann.length] = akk[l]
        }
        console.log(ann)
```
结果:![](https://image.dcaoao.com/image/202211122115609.webp)

### 冒泡排序 ###
冒泡排序是指将数值从大到小/从小到大排列起来
```
        var amm = [5,4,9,6,3,2,5,6,9,5,6]
        for (var m = 0;m <= amm.length -1 ;m++) {  //外层的循环需要比数组的个数少一次
            for (var m1 = 0 ;m1 <= amm.length - m - 1;m1++) {  //内层的循环数依次递减并减1
                //开始交换两个变量值
                if (amm[m1] < amm[m1 + 1]) {  //这里控制是从小到大还是从大到小
                    var temp = amm[m1]
                    amm[m1] = amm[m1 + 1]
                    amm[m1 + 1] = temp
                }
            }
        }
        console.log(amm)
```

## 函数的使用 ##
函数的封装将一个或者多个功能通过函数的方式封装起来，对外只提供一个简单的接口
函数的使用分为两步 声明函数与调用函数、
作用: 重复执行的代码可重复利用，减少重复率

使用步骤:
```
//1.声明函数
         function 函数名 ( ) {
            条件表达式
         }

//2.调用函数 格式 ： 函数名（）
```

### 函数的参数 ###
函数的参数分为形参与实参

原理 实参的值会传递给形参，然后进行函数调用输出，实参可以任意改变
作用：在函数内部不固定，可以通过参数在调用函数的时候将不同的值传递进去
参数与参数之间需要用逗号与空格隔开

```
         // 1.先声明函数  格式：function can (形参)
         function can (say) {
            console.log (say)
         }

         //2.调用函数 格式 can（'实参'）  
         can ('66')


         //函数案例 求两个数的累加和
         function Sum (one1, one2) {
            console.log(one1 + one2)
         }
         Sum(1, 3)



        //函数案例 求两个数之间的累加和
         function getSum (start, end) {
            var sum = 0
            for (var a = start;a <= end;a++) {
                sum += a
            }
            console.log(sum)
         }
         getSum(1, 100)  //求1到100之间的累加和
         getSum(1, 10)   //求1到10之间的
```
如果形参与实参个数不相等
实参 = 形参  结果正常输出
实参 > 形参  只输出形参的数量
实参 < 形参  缺少的形参为undefined 
所以,两者数量要尽量匹配
### 函数的返回值 ###
上面缩写的函数封装,条件表达式都写在了封装内,这样是不合适的,需要将封装后的函数结果,直接输出到函数的调用处,方便取值使用
这里使用 `return` 只要函数遇到它,就会将函数的结果,返回给函数的调用者

案例:
```
         function he (he1, he2) {
            return he1 + he2;  //使用return
         }
         //使用return后,封装的函数会将结果输出到调用处

         console.log(he(1, 2)) //输出结果为3
```

需要注意的是 return也有结束的含义，在其后面的代码将不会被执行，并且返回其后面的值
return只能返回一个值，如果有多个值，则以最后一个值为准，如果雀食要返回多个值，可以使用数组
如果函数内没有return 则返回的是空值

### 11.13笔记 ###
### 案例 return返回多个值 数组  求两个数的加减乘除结果 ###
```
         function day1 (num1,num2) {
            return [num1 + num2,num1 - num2,num1 * num2,num1 / num2]
         }
         var day = day1(3,6)
         console.log(day)
```

![](https://image.dcaoao.com/image/202211132023679.webp)

可以直接返回数组,数组默认被看做为一个值
### 函数案例 任意两个数的算数运算 ###
```
function mya (mya1,mya2) {
            return Number(mya1) + Number(mya2)
         }
         var mya1 = prompt('请输入第一个数')
         var mya2 = prompt('请输入第二个数')
         alert(mya(mya1,mya2)) 
```
![](https://image.dcaoao.com/image/202211132027902.gif)

### 函数案例 输入任意两个数，求最大值，弹出运算结果 ###
```
function myb (myb1,myb2) {
    var max = 0
    if (myb1 > myb2) {
        max = myb1
    } else {
        max = myb2
    }
    return max
}
alert(myb(prompt('请输入第一个值'),prompt('请输入第二个值')))

//另一种写法
      function myb(myb1, myb2) {
         if (myb1 > myb2) {
            return myb1;
         } else {
            return myb2
         }
      }
      var myb1 = prompt('请输入第一个数')
      var myb2 = prompt('请输入第二个数')
      alert(myb(myb1, myb2))
```

### 函数案例 输入三个不同数字的最大值 ###
```
      function myc(myc1) {
         var max = myc1[0] //声明一个数组第一位的值
         for (var i = 0; i < myc1.length; i++) {
            if (myc1[i] > max) {  //如果数组值大于了数组第一位,则将大于的值赋值于自身,然后循环下去,第二位,第三位...
               max = myc1[i]
            }
         }
         return max
      }
      var ra = myc([prompt('请输入第一个数'), prompt('请输入第二个数'), prompt('请输入第三个数')])  //prompt来进行取值
      console.log(ra)
```

### 函数对象 `arguments` 的使用 ###
1.`arguments`为函数内置的对象，只有`函数`才可以使用
2.使用 `arguments` 存储了所有传递过来的实参，适用于`不确定到底多少个实参`时使用
3.使用`伪数组`的方式进行存储，可以使用`arguments[0]`之类来进行取值使用
4.也具有`length`属性，但并不是真正意义上的数组
```
      function myd() {
         console.log(arguments)  //输出实参值
         console.log(arguments.length)  //可输出数组长度/个数
         console.log(arguments[3])
      }
      myd(1, 2, 3, 4, 5, 6)
```
结果:
![](https://image.dcaoao.com/image/202211132047866.webp)

### `arguments` 案例 求任意个数数值的最大值 ###
```
      function mye() {
         var myemax = arguments[0]
         for (var i = 0; i < arguments.length; i++) {
            if (myemax < arguments[i]) {
               myemax = arguments[i]
            }
         }
         return myemax
      }

      var saymye = mye(1, 2, 3, 4, 5, 6, 8, 6, 3, 2, 1)
      console.log(saymye)
```

### 案例 利用函数翻转任意数组 ###
```
      function array() {
         var yarra = [] //空数组
         var arri = arguments.length - 1  //声明要翻转数组的计数器
         var k = 0
         for (var i = arri; i >= 0; i--) {
            yarra[yarra.length] = arguments[i]  //声明数组的第0个变量等于旧数组的最后一个变量
            k++
         }
         return yarra
      }
      var sayarray = array([1, 2, 3, 4, 5])
      console.log(sayarray)
```

### 案例 函数判断是否闰年 ###
判断闰年的条件是:能被4整除,与不能被100整除,或者能被400整除
这里使用逻辑与运算 一假全假,全真为真    和 逻辑或运算 一真全真 全假则假
```
      function year(years) {
         var falses = false
            //能被4整除与整除100不等于0,或者除以400为0
         if (years % 4 == 0 && years % 100 != 0 || years % 400 == 0) {  //如果为真,则执行if内语句,如果为假,则不执行,导致falses = false
            falses = true
         }
         return falses
      }
      console.log(year(2000))  //true
      console.log(year(1999))  //false
```

### 函数可以互相调用 ###
```
      function fn1() {
         console.log(1) //2.输出fn1内的 1
         fn2()    //3.然后去找fn2函数 输出fn2喊数内的 2和666
         console.log(3) //4.然后回到fn1函数内 返回3
      }

      function fn2() {
         console.log(2)
         console.log('666')
      }
      fn1()//1.先回去找fn1函数


//判断是否闰年
      function year(years) {
         var falses = false
            //能被4整除与整除100不等于0,或者除以400为0
         if (years % 4 == 0 && years % 100 != 0 || years % 400 == 0) {  //如果为真,则执行if内语句,如果为假,则不执行,导致falses = false
            falses = true
         }
         return falses
      }
      console.log(year(2000))  //true
      console.log(year(1999))  //false

      //函数互相调用案例 输入年份,通过是否闰年来告知2月份天数
      function backDay () {
         var backyear = prompt('请输入年份')
         if (year(backyear)) {  //调用上方判断闰平年函数,必须要加小括号在内
            alert('当前年份为闰年,2月天数为29天')
         } else {
            alert('当前年份为平年,2月天数为28天')
         }
      }
      backDay()
      
```
![](https://image.dcaoao.com/image/202211152126085.gif)

### 函数表达式 ###

```
      //函数表达式案例
      var hanshu = function(hanshu1){
         console.log(hanshu1)
      }

      //输出 hanshu 内的值
      console.log(hanshu(666,1))
```


## JS的作用域 ##
作用域的作用是代码名字在某个范围内起作用和效果，目的是提高程序的可靠性，减少命名冲突
s作用域分为全局作用域和局部作用域
全局作用域：整个script标签内 或者是一个单独的js文件
```
var num = 1 //这就是全局作用域
console.log(num)  //输出1
```
局部作用域:在函数内部就是局部作用域 整个代码的名字只在函数内部起效果
函数的形参也可以看做是局部变量
```
 function fn () {
        //局部作用域
        var num = 2 
        
        console.log(num) //输出2  只能在函数内部调用

        var num3 = 3   //局部作用域 只能在函数内部调用
        num5 = 5
        //需要注意的是，在函数内部，没有声明，直接赋值的函数，也属于全局变量
    }
    num5 = 5
    //console.log(num3)  //因为在函数内部调用局部作用域,会报错
    console.log(num5)  //输出5 因为函数内部,没有声明,直接赋值的函数,属于全局变量
```

####作用域 小结 ####
全局变量:`任何地方地方`都可以使用,但是只有在浏览器关闭时才会被销毁,比较`占内存`
局部变量:只能在`函数内部`使用 代码执行时会被初始化,代码结束后会被销毁,更加`节省内存`

### 作用域链 就近原则 ###
内部函数可以访问外部函数的值,内部函数寻找值,先去上一级寻找是否有符合条件的值,如果没有,则继续向上一级取值
直到找到符合条件的值为止
```
    function fn () {
        var num = 1

        function fnn () {
            console.log (num)
            return num
        }
        fnn()
    }
    var num = 666
    console.log(fn())  //因为就近原则,所以还是输出 1
```

## JS预解析 ##
js引擎分为两步运行js 预解析 代码执行
`预解析`: 预解析会将js内的所有var 和function提升到当前作用域的最前面
比如说 `var = num`
       `function aum () {}`
然后就开始进行代码执行,按照书写顺序从上到下执行

预解析分为 变量预解析`(变量提升)`和 函数预解析`(函数提升)`
1.变量提升:把所有的`变量声明`提升到当前作用域的最前面
2.函数提升:把所有`函数的声明`提升到当前作用域的最前面
3.然后赋值操作`留在原来的位置`

```
console.log(num)  //输出空值 undefined
        var num = 1
        //相当于执行了
        var num;
        console.log(num)
        num = 1


        say()   //会报错 ,没有这个函数
        var say = function () {
            console.log('说')
        }

        //相当于执行了
        var say;
        say()
        function say() {
            console.log('说')
        }



        //预解析案例1
        var my1 = 10
        fun();
        function fun() {
            console.log(num)
            var num = 20
        }

        // 相当于执行了
        var my1;

        function fun() {
            var num;
            console.log(num)
            num = 20
        }

        fun();  //输出空值 undefined
        my1 = 10


        //预解析案例2
        var my2 = 10;
        function fn() {
            console.log(my2)
            var my2 = 20;
            console.log(my2)
        }
        fn()

        //相当于执行了
        var my2;

        function fn() {
            var my2
            console.log(my2)  //输出空值 undefined
            my2 = 20;
            console.log(my2)  //作用域链,就近原则, 输出20

        }
        fn()
        my2 = 10


        //预解析案例3
        fn1();
        console.log(c)
        console.log(b)
        console.log(a)
        function fn1() {
            var a = b = c = 9
            console.log(a)
            console.log(b)
            console.log(c)
        }

        //相当于执行了
        function fn1() {   //函数提升
            var a = 9
            b = 9
            c = 9
            console.log(a)  //9
            console.log(b)  //9
            console.log(c)  //9
        }

        console.log(a)  //报错  
        console.log(b)  //9
        console.log(c)  //9
        fn1();
```

## 创建对象 ##
创建函数有两种方法: `利用对象字面量创建对象{}`  `使用 new Object();`

利用对象字面量创建对象:
```
        var obj = {
            uname:'张三',
            age:18,
            sex:'男',
            sayHi:function() {
                console.log('你好')
            }
        }
```
对象里的属性或者方法采用键值对的方法   键 属性名:属性值  值   值可以是任何数据，布尔，字符串，数值
多个属性使用逗号分隔，不然会报错


使用 new Object()创建对象

利用等号赋值,使用分号分隔结束
```
var obj1 = new Object();   //创建一个空对象
        obj1.uname = '鸣人';
        obj1.sex = '男';
        obj1.age = '19'
        obj1.skill = function() {
            console.log('影分身')
            console.log('瞬闪')
        }
```


调用对象里的属性
```
//第一种方法
        console.log('姓名:' + obj.uname)
        console.log('年龄:' + obj.age)
        console.log('性别:' + obj.sex)
//第二种方法
        console.log('姓名:' + obj['uname'])
```

![](https://image.dcaoao.com/image/202211152147923.webp)


调用对象里的方法  对象名.方法名()    方法可以看做就是函数
```
obj.sayHi()
```

总结
变量:单独赋值,单独使用
属性:对象里边的变量称为属性,不需要声明
函数:单独存在,通过 函数名() 来调用
方法:对象里面的函数称为方法,不需要声明  对象名.方法名()  来调用

### 创建对象练习 ###
```
        var dog = {
            name:'可可',
            type:'阿拉斯加犬',
            age:'5岁',
            color:'棕红色',
            skill:function() {
                console.log('汪汪汪')
                console.log('演电影')
            }
        }
        console.log('姓名:' + dog.name +' 品种:' +  dog.type + ' 年龄:' + dog.age +' 颜色:' + dog.color )
        dog.skill()
```
![](https://image.dcaoao.com/image/202211152149890.webp)

## 构造函数创建对象 ##
创建构造函数:  格式
```
//构造函数名字首字母要大写
        function 构造函数名() {
            this.属性 = 值;
            this.方法 = function() {}
        }
```
调用:  调用构造函数必须使用new，而且不需要return
```
 new 构造函数名()
 ```

```
        function Four (uname,age,sex) {
            this.uname = uname
            this.age = age
            this.sex = sex
            this.sing = function(music) {
                console.log(music)
            }
        }
        var san = new Four('张三',18,'男')  //使用声明的方式生成函数
        console.log(san.uname)  //取声明的函数内的值  输出正三
        san.sing ('大风车')  //调用构造函数内的方法


        console.log(typeof(san))  //返回object
        console.log(new Four('张三',18,'男'))


        //构造函数案例

              function Wang(name,xue,xing) {
            this.name = name
            this.xue = xue
            this.xing = xing
            this.gong = function (gong) {
                console.log(gong)
            }
        }
        var lianpo = new Wang('廉颇','500血','力量型')
        console.log(lianpo)
        lianpo.gong('近战')

        var houyi = new Wang('后羿','100血','射手型')
        console.log(houyi)
        houyi.gong('远程')  
```

1.构造函数 ：泛指某一大类 类似java里的class
2.对象： 特指 是一个具体的事物  廉颇 == {name: '廉颇', xue: '500血', xing: '力量型'}
```
        var lianpo = new Wang('廉颇','500血','力量型')
        console.log(lianpo)
```
3.利用构造函数创建对象的过程称为对象的实例化


关于 new调用构造函数 执行的过程
1.new 构造函数 可以在内存中创建一个空的对象
2.this就会指向刚才创建的空对象
3.执行构造函数里的代码 给这个空对象添加属性和方法
4.然后即可返回这个对象,所以不需要return

## for in循环遍历对象 ##

首先创建一个对象
```
        var my = {
            name:'名字',
            age:'18',
            sex:'未知',
            fn:function() {
                console.log('123')
            }
        }


//平常输出对象内的属性值
        console.log(my.name)
        console.log(my.age)
        console.log(my.sex)
        my.fn()

//使用for in 遍历 my 对象  但是 很少用来遍历方法 因为遍历方法会输出很奇怪,如下图
        for (var k in my) {
            console.log(k)    //单独输出k,得到的是变量内的属性名
            console.log(my[k])    //对象名[变量名]  得到的是变量内的属性值
        }
```
![](https://image.dcaoao.com/image/202211182249927.webp)

小结 
对象可以使代码结构更清晰
对象复杂数据类型是object
本质:对象就是一组无序相关属性的方法的集合
构造函数泛指某一大类,苹果,不管红苹果还是绿苹果
对象实例特指某一事物 比如这个苹果,这个人
 for in 语句用于遍历对象的属性,进行循环操作


 ## JS对象 ##
JS中,对象分为三种:自定义对象,内置对象,浏览器对象

### 内置对象 ###
内置对象指JS语言自带的一些对象,供开发者使用,提供了一些基本而且必要的功能(属性和方法)
内置对象的最大优点就是快速开发
提供了多个对象 :Math Date Array String
https://developer.mozilla.org/zh-CN/
内置对象调用时不需要 new 直接使用属性和方法即可

```
 var a16 = Math.max(1, 2, 3, 4, 5, 6)  //求最大值
        console.log(a16)
```


封装数学对象 求PI   最大值 最小值

```
 var myMate = {
            PI: 3.1415929,
            max: function () {
                var max = arguments[0]
                for (var a = 0; a < arguments.length; a++) {
                    if (max < arguments[a]) {
                        max = arguments[a]
                    }
                }
                return max
            },
            min: function () {
                var min = arguments[0]
                for (var a = 0; a < arguments.length; a++) {
                    if (min > arguments[a]) {
                        min = arguments[a]
                    }
                }
                return min
            },

        }

        console.log(myMate.PI)
        console.log(myMate.max(1, 2, 3, 4, 5))
        console.log(myMate.min(1, 2, 3, 4, 5))
```
输出结果:
![](https://image.dcaoao.com/image/202211182252776.webp)



### 取绝对值 ###
```
        console.log(Math.abs(1))  //1
        console.log(Math.abs(-1))  //1
        console.log(Math.abs('-1'))  //隐式转换，会转变为数字型绝对值1
        console.log(Math.abs('这是嘛'))  //无法转换 NaN
```
### 向下取整 ###
```
        console.log(Math.floor(1.1))   //1
        console.log(Math.floor(2.9))   //2
```
### 向上取整 ###
```
        console.log(Math.ceil(1.1)) //2
        console.log(Math.ceil(1.9)) //2
```
### 四舍五入 ###
```
        console.log(Math.round(1.1))  //1
        console.log(Math.round(1.5))  //2
        console.log(Math.round(-1.5))  //-1  需要注意的是负值 5 会想向大值取值
```

### 案例 去两数之间的随机整数 ###
```
        function getRandomInt(min, max) {  //封装函数,给予开始与结束值
            min = Math.ceil(min);  //使用构造函数,并将两个值进行取整 最小值向下取整
            max = Math.floor(max); //最大值向上取整
            return Math.floor(Math.random() * (max - min)) + min; //不含最大值，含最小值
        }

        console.log(getRandomInt(1,10))
```
### 案例 随机点名器 ###
```
        var banji = ['张三','李四','王五','李六','六七']
        console.log(banji[getRandomInt(0,banji.length - 1)])
```

### 案例 踩数字 ###
```
        var shuzi = getRandomInt(1,10)
        console.log(shuzi)
        
        while (true) {  //死循环
            var cai = prompt('请输入您猜测的数字,在1-10之间')
            if (shuzi > cai) {
                alert('猜小了')
            } else if (shuzi < cai) {
                alert('猜大了')
            } else {
                alert('刚刚好')
                break;  //满足条件 退出循环
            }
        }

```

### 案例 踩数字2 ###
```

        //要求用户猜出1-50之间的数字 只能猜10次
        var shuzi50 = getRandomInt(1,50)
        console.log(shuzi50)

        for (var i = 1;i <= 10 ;i++) { 
            //console.log(i)
            var shengyu =   Number(11) - Number(i)  //获取剩余循环次数
            console.log('您还有' + shengyu +  '次机会')
            var cai = prompt('请输入您猜测的数字,在1-10之间' + '\n' + '您还有' + shengyu +  '次机会')
            
            if (i == 10) {  //限定循环十次就退出
                break;
            }
            if (shuzi50 > cai) {
                alert('猜小了')
            } else if (shuzi50 < cai) {
                alert('猜大了')
            } else {
                alert('刚刚好')
                break;  //满足条件 退出循环
            }
        }
```

## Date 日期对象 ##

输出时间使用 new Date对象,
```
        var time = new Date();  //当前时间
        console.log(time)

        var time2 = new Date('2019-10-1 8:8:8');  //输出这个时间
        console.log(time2)
```
![](https://image.dcaoao.com/image/202211182307533.webp)
日期对象的使用
```
        var time3 = new Date();
        console.log(time3.getFullYear())  //返回日期当前年份
        console.log(time3.getMonth())  //返回日期当前月份当前是11月份 会返回10 因为从0开始的 0-11
        console.log(time3.getMonth() + 1)  //  直接+1即可正常获取月份
        console.log(time3.getDate())  // 获取号数 几号 
        console.log(time3.getDay())  // 获取周几 周一返回1 周六返回6 但周日返回0 
        console.log(time3.getHours())  //时
        console.log(time3.getMinutes())  //分
        console.log(time3.getSeconds())  //秒
```

![](https://image.dcaoao.com/image/202211182307174.webp)

返回当前时间案例
```
        //年
        var year = time3.getFullYear()
        //月
        var month = time3.getMonth()
        //日
        var data = time3.getDate()
        //周几
        var day = time3.getDay()
        var zhou = ['星期日','星期一','星期二','星期三','星期四','星期五','星期六']

        //最后输出
        console.log('当前时间为: ' + year + '年' + month + '月' + data + '日 ' + zhou[day])


    //输出时分秒
        function shijian () {
            var time3 = new Date()
            var s = time3.getHours()
            var f = time3.getMinutes()
            var m = time3.getSeconds()
            if (m < 10) {   //使1 2 3 变为 01 02 03
                m = '0' + m
            }
            return s  + ':' + f + ':' + m
        }

        console.log(shijian())
```

![](https://image.dcaoao.com/image/202211182306998.webp)

获取时间戳  时间戳的意义是 1970年1月1号至今过了多少毫秒数
```
        console.log(time3.valueOf())  //时间戳
        console.log(time3.getTime())  //时间戳

        //简写
        var date1 = +new Date()
        console.log(date1)
        //H5新增的
        console.log(Date.now())
```

倒计时案例:
```
        //倒计时案例
        function count(time) {
            var nowTime = +new Date()  //获取当前时间戳
            var inputTime = +new Date(time)  //获取用户输入的时间戳
            var timeMiao = (inputTime - nowTime)  / 1000;   //获取倒计时时间,并由毫秒转换为秒 
            var d = parseInt(timeMiao / 60 / 60 / 24) //天
            var h = parseInt(timeMiao / 60 / 60 % 24) //时
            var m = parseInt(timeMiao / 60 % 60) //分
            var s = parseInt(timeMiao % 60) //秒
            return d + '天' + h + '时' + m + '分' + s + '秒'  //输出倒计时
        }
        console.log(count('2022-11-18 23:07:00'))
```
记录一下当前时间:1668783992332
结果:![](https://image.dcaoao.com/image/202211182306813.webp)

## 数组对象 ##
### 创建数组 ###
1.字面量创建数组
```
        var arr = [1, 2, 3]
        console.log(arr[0])
```
2.new Array() 创建数组  
```
        var arr1 = new Array() //创建空数组
        var arr1 = new Array(2) //创建长度为2的数组
        var arr1 = new Array(2, 3) //等价于 var arr1 = [2,3]
```

### 判断是否为数组 ###

3.1 参数名 instanceof Array
```
console.log(arr1 instanceof Array)   //如果是数组，则返回true，如果不是数组 则返回false
```
3.2 Array.isArray(参数)
```
console.log(Array.isArray(123))  //返回同上，返回true或者false
```

### 添加数组元素的方法 ###
老办法:
```
var arr2 = [1, 2, 3, 4, 5]
var arr2[5] = 6
```

新方法:

#### 在末尾添加一个或者多个数组元素 ： `push() ` ####
1.push 可以为数组尾部添加新的数组元素
2.push() 括号内直接写新增的数组元素即可
3.push返回的结果是新数组的长度
4.原数组也会发生变化
```
var arr2 = [1, 2, 3, 4, 5]
arr2.push(6, 7, 8, '这啥啊名记不住')
console.log(arr2) //输出数组12345678这啥啊名记不住

        //push() 也有返回值
        console.log(arr2.push(6, 7, 8, '这啥啊名记不住'))  // 13  返回的是新数组的长度


```
![](https://image.dcaoao.com/image/202211182311679.webp)

#### 在数组前方添加数组元素 使用 `unshift()`  其他的与`push()`相同 ####
```
        var arr3 = [1, 2, 3]
        arr3.unshift(4, 5, '啊这样不就记住了')
        console.log(arr3)  //返回数组 [4, 5, '啊这样不就记住了', 1, 2, 3]
```
![](https://image.dcaoao.com/image/202211182313896.webp)


### 删除数组元素的方法 ###

#### 删除数组末尾的数组元素  `pop()` ####
```
        var arr5 = [1, 2, 3]
        arr5.pop()  //返回值为被删掉的值，每次只能删掉一个
        console.log(arr5)   //3会被删掉，只剩下1和2 
```

#### 删除数组开头的数组元素  `shift()` ####
```
        var arr5 = [1, 2, 3]
        arr5.shift()  //返回值为被删掉的值，每次只能删掉一个
        console.log(arr5)   //1会被删掉，只剩下2和3
```

### 数组元素案例 筛选出小于2000的数值，大于2000的删除 ###
核心思想:声明一个空数组,如果小于2000,则把这个数添加到新数组当中,使用push从尾部添加

```
        var shu = [1500,1600,1700,1800,1900,2000,2100,1300]
        var newShu = []
        for (var i = 1;i < shu.length;i++) {
            if (shu[i] < 2000) {
                newShu.push(shu[i])
            }
        }
        console.log(newShu)
```
![](https://image.dcaoao.com/image/202211182315704.webp)


### 翻转数组 `reverse` ###
使用格式 数组名.reverse
```
        var arr6 = [1,2,3,4,5]
        arr6.reverse()
        console.log(arr6)//[5, 4, 3, 2, 1]
```

### 数组排序(简易版冒泡排序) ###
这个写法比较固定,记住即可
```
        var arr7 = [5,8,66,33,22,11,5,2,9,5,3,666,8]
        arr7.sort(function(a,b) {
            // return a - b;  //升序
            return b - a;  //降序序
        })
        console.log(arr7)
```

### 返回数组元素索引号，查找指定数组元素的索引号 ###
格式:
`数组名.indexOf()`从头查抄
`数组名.lastIndexOf()`从尾部查抄
只返回第一个满足的值，如果没有找到则返回-1
```
        var arr8 = [1,2,3,4,5,6]
        console.log(arr8.indexOf(6),[0])  //从前方第0个索引号的开始查找 返回 5   两者的起始位置参数都可以省略
        console.log(arr8.lastIndexOf(1),[5])  //从后方索引号为5的开始查找 返回 1 
```

### 案例 筛选重复值 ###
核心算法 ：遍历旧数组，拿旧数组元素去查询新数组，如果该元素在新数组没出现过，就添加
```
        function unique(chongfu){
            var newchongfu = []
            for (var a = 0;a < chongfu.length;a++) {  //首先遍历旧数组
                if (newchongfu.indexOf(chongfu[a]) === -1) {  //如果新数组中没有旧数组内的第a个值，则在新数组后方添加该值
                    newchongfu.push(chongfu[a])
                }
            }
            return newchongfu
        }
        // var repeat = unique(['a','a','b'])
        var repeat = unique([1,1,2,3,4,5,66,6,6,8,5,6,2,5,1,2,5,4,2])
        console.log(repeat)
```
![](https://image.dcaoao.com/image/202211182322969.webp)


## 字符串元素 ##
### 将数组转换为字符串 ###
1.使用toString()
```
        var arr9 = [1,2,3,4,5,6]
        console.log(arr9)  //此刻输出，为字符串类型
        console.log(arr9.toString())  //输出1,2,3,4,5,6字符串
```

2.使用join(‘分隔符)
```
        var arr10 = [1,2,3,4,5,6]
        console.log(arr10.join('-'))  //join()内的分隔符需要使用字符串符号包裹  1-2-3-4-5-6
```
![](https://image.dcaoao.com/image/202211182321758.webp)

### 案例 查找字符串内某一字符出现的位置以及次数 ###
```
        var my12 = 'sokjashdsfuayweuokjsdfuiheasoirfhw'  //声明字符串
        var index = my12.indexOf('s')  //声明要查找的字符第一次出现的位置
        var num = 0
        while (index !== -1) {
            console.log(index)   //输出每次字符串所在的位置
            index = my12.indexOf('s',index + 1)  //设定index下一次循环的位置，在每个查找的字符后面 +1 防止死循环
            num++  //保存循环次数，循环次数等于出现次数
        }
        console.log('字符出现了' + num + '次')
```
![](https://image.dcaoao.com/image/202211182324172.webp)

### 根据索引号位置返回字符 ###
格式`变量名.charAt(索引号)`
```
 var my15 = 'dcaoao'
        console.log(my15.charAt(2))  //返回索引号为2的值 a
        //使用charAt遍历整个字符
        for (var a = 0;a < my15.length;a++) {
            console.log(my15.charAt(a))
        }
        //使用 变量名[]   H5新增元素,需要考虑兼容性
        console.log(my15[0])  //返回d
```
### 根据索引号返回改字符的ASCII码 ###
格式: `变量名.charCodeAt(索引号)`
```
        var my16 = 'dcaoao'
        console.log(my16.charCodeAt(0))  //返回my16中索引号0的值的ASCII值
```

### 判断对象内是否拥有某一属性  ###
格式: `对象['属性名']`  内部单引号可带和不带,看数据格式
```
        var my17 = {
            age:'18'
        }
        if (my17['age']) {
            console.log('有该属性名')
        } else {
            console.log('没有该属性名')
        }
```
![](https://image.dcaoao.com/image/202211192224227.webp)

### 案例 判断一个字符串内出现次数最多的字符 ,并统计出现次数 ###
核心: 首先使用charAt()遍历这个字符串,把每个字符都存储给对象,如果对象没有这个值,则这个值就为1,如果对象内已经存在这个值,则将这个值+1
```
var my18 = 'clkjsmeoitjrolksrjpwojroksdgj'  //字符串
var my18_1 = {}         //声明一个空对象用于存放出现次数
for (var i = 0;i < my18.length;i++) {
    var bianli = my18.charAt(i)  //遍历字符串
    //如果遍历的字符串在新对象中没有,则赋值为1次,如果在新对象中存在,则在原有的基础上+1
    if (my18_1[bianli]) {
        my18_1[bianli]++      //原有基础上+1
    } else {
        my18_1[bianli] = 1    //直接赋值
    }
}
console.log(my18_1)  //输出新对象看看
//然后使用for in 来进行遍历对象,来查询出现最多的字符以及次数
var max = 0 //声明一个空值用来存放最大值
var max_name = ''  //声明一个空值用来存放最大值的名字
for (var a in my18_1) {
    if(max < my18_1[a]) {
        max = my18_1[a]
        max_name = a
    }
}
console.log('最大循环次数为' + max)
console.log('出现最多的字符为为' + max_name)
```
(这个要多练习)
![](https://image.dcaoao.com/image/202211192245951.webp)
## 字符串操作方法 ##

### 拼接字符串  ###
格式:`concat('字符串1','字符串2',......)`
```
        var my19 = '123'
        console.log(my19.concat('456','789'))  //把字符串123拼接456和789  输出123456789
```


### 截取字符串  ###
格式:
`substr('截取的起始位置的索引号,截取多少个字符')`
```
        var my20 = '123456789'
        console.log(my20.substr(2,5))  //从索引号为3开始截取5个
```
![](https://image.dcaoao.com/image/202211192247788.webp)

### 替换字符串   ###
格式: `replace('被替换的字符串','要替换的字符串')`  //但是它只会替换第一个字符,多次替换可以上循环
```
        var my21 = 'aabaavesf'
        console.log(my21.replace('a','6'))  //6abaavesf
```
把全部a替换为6,上循环  方法1
```
        for (var i = 0;i < my21.length;i++) {
            my21 = my21.replace('a','6')
        }
        console.log(my21)
```
方法2 :
```
        var my22 = 'aabaavesf'
        while (my22.indexOf('a') !== -1) {
            my22 = my22.replace('a','6')
        }
        console.log(my22)
```
![](https://image.dcaoao.com/image/202211192250971.webp)

### 将字符转换为数组  ###
格式: `split('分隔符')`  与`join` 将数组转换为字符串相对应
```
        var my23 = '1,2,3,4,5,6'
        var my25 = '1&2&3&4&5&6'
        console.log(my23.split(','))  //['1', '2', '3', '4', '5', '6']
        console.log(my25.split('&'))  //['1,2,3,4,5,6']
```
![](https://image.dcaoao.com/image/202211192251924.webp)

        //案例 给定一个字符串,做出以下操作
        //1.获取字符串的长度
        //2.去除指定位置的字符,如0,3,5,9
        //3.查找指定字符是否在字符串中存在 i,v,b等
        //4.替换指定的字符 g替换为22
        //5.截取指定开始位置到结束位置的字符串
        //6.找出以上字符串中出现最多的字符和次数


## 堆和栈的理解与区别 ##
1.栈 用于存储简单数据类型，里面直接开辟一个空间，存放值
`var age = 18  //存放18`
2.堆 用于存储复杂类型（对象） 用new创建的之类
首先在栈里面存放地址，十六进制地址，地址指向堆中的数据
![](https://image.dcaoao.com/image/202211192204264.webp)

### 复杂数据类型传参###
```
        //1.首先两个函数，不调用不执行
        function Person(name) {
            //3.p函数接收 '刘德华' 参数，此刻p.name输出为 '刘德华'
            this.name = name;
        }
        function f1(x) {
            console.log(x.name)  //6.此刻输出还为刘德华
            x.name = '张学友'   //7.修改了p的形参内容为 '张学友' 
            console.log(x.name) //8.输出张学友
        }

        //2.此处调用了Person函数，并且传递参数 '刘德华'
        var p = new Person('刘德华')
        console.log(p.name)  //4.输出刘德华
        f1(p)   //5.此刻又调用了f1函数,并且传参为p  这么看 p = f1函数内的形参x
        console.log(p.name)  //9.输出张学友
```


## DOM树 ##
文档:一个页面就是一个文档,DOM中使用`document`表示
元素:页面中所有的标签都是元素,DOM中使用e`lement`表示
节点:网页中所有的内容都是节点(标签 属性 文本 注释等),DOM中使用`node`表示

html:
```
    <!-- getElementById根据id来获取元素 -->
    <div id="time">2019-9-9</div>

    <!--getElementsByTagName 根据标签名来获取元素 -->
    <ul>
        <li>1</li>
        <li>2</li>
        <li>3</li>
        <li>4</li>
        <li>5</li>
    </ul>

    <!-- 获取某个父元素内指定标签名的子元素 -->
    <ol id="ol_id">
        <li>6</li>
        <li>6</li>
        <li>6</li>
        <li>6</li>
        <li>6</li>
    </ol>

    <div class="leiName">
        <div class="red">红色</div>
    </div>
```
### getElementById('')根据id来获取元素 ###
getElementById('') 的参数是大小写敏感的字符串，严格区分
getElementById可以找到这个元素,通过id获取，必须以document开头  文档里的某个元素
使用方法:`document.getElementById('ID名')`
```
        var timer = document.getElementById('time')   
        console.log(timer)
        console.log(typeof timer)   //返回结果是一个元素对象
        //console.dir()  打印我们返回的元素对象，更好的查看里面的属性和方法
        console.dir(timer)
```
![](https://image.dcaoao.com/image/202211202040446.webp)

### getElementsByTagName('') 根据标签名获取元素 ###
使用方法:`document.getElementsByTagName('li')`
1.根据标签名来获取元素  使用伪数组来存储，所以可以使用数组的索引号来输出
2.返回获取到的元素是对象的集合
3.得到的元素是动态的，跟随html变化而变化，可以遍历里面的元素对象
4.如果页面中只有一个符合条件的标签，返回的还是伪数组
5.如果没有符合条件的标签，返回的是一个空的伪数组
```
var list = document.getElementsByTagName('li')
        console.log(list)  //HTMLCollection(5) [li, li, li, li, li]
        console.log(list[1])   //<li>2</li>

        //获取某个父元素内指定标签名的子元素
                //document.getElementById('父元素ID')
        var olde = document.getElementById('ol_id')   //文档中的ol,确定父元素名字,必须是指定的单个元素
                //父元素变量名.getElementsByTagName('要获取的子元素标签')  可以看做是ol内的.li
        console.log(olde.getElementsByTagName('li'))
```
![](https://image.dcaoao.com/image/202211202044777.webp)
### document.getElementsByClassName('') 根据类名获取元素  ###
使用方法: `document.getElementsByClassName('类名')`
```
        var lei = document.getElementsByClassName('leiName')
        console.log(lei)  
```
![](https://image.dcaoao.com/image/202211202046497.webp)

### H5新增的选择器,一选择器多用 ###
H5新增 `document.querySelector('选择器类型')`   只能返回指定选择器的`第一个对象`
```
var red = document.querySelector('.red')  //.类名 是类选择器
var ol_id = document.querySelector('#ol_id')  //#ID 是ID选择器
var li_biaoqian = document.querySelector('li')  //直接写,是标签选择器,只会返回第一个
```
![](https://image.dcaoao.com/image/202211202048568.webp)


H5新增 返回指定选择器的`所有元素`对象的集合,是一种伪数组
```
var all = document.querySelectorAll('li')
```
![](https://image.dcaoao.com/image/202211202049302.webp)

### 获取特殊标签 body与html ###
获取`body`
```
        var bodyELe = document.body   //返回body元素对象
        console.log(bodyELe)
        console.dir(bodyELe)
```

获取`html`
```
        var htmlEle = document.documentElement;  //返回html元素对象
        console.log(htmlEle)
```
![](https://image.dcaoao.com/image/202211202050390.webp)


### 事件三要素 ###
事件由三部分组成 事件源 事件类型 事件处理程序 被称为事件三要素
1.事件源：事件被触发的对象， 谁 按钮
`var bthid = document.getElementById('btn')`
2.事件类型：如何触发，什么时间 比如是鼠标点击(onclick)还是鼠标经过，或者键盘按下
3.事件处理程序 通过一个函数赋值的方式完成

```
        //ID为btn的按钮被点击后，弹出提示框
        bthid.onclick = function () {
            alert('这个按钮被点击了')
        }



        //点击div，控制台输出 '我被选中了'
        //1.获取事件源
        var div = document.querySelector('div')
        //2.绑定事件 3.添加时事件处理程序
        div.onclick = function () {
            console.log('我被选中了')
            alert('被选中了')
        }
```
常见的鼠标事件
`onclick `鼠标点击左键触发
`onmouseover ` 鼠标经过自身或者子盒子都会触发
`onmouseout`  鼠标离开触发
`mouseenter`   鼠标经过自身盒子触发
`mouseleave`   鼠标离开自身盒子触发
`onfocus`     获得鼠标焦点触发
`onblur `     失去鼠标焦点触发
`onmousemove `鼠标移动触发
`onmouseup `  鼠标弹起触
`onmousedown` 鼠标按下触发




### 改变元素(标签内)内容 ###
1. element.innerText  改变从起始到终止的内容,但是它不识别html标签,同时空格与换行也被去掉
2. element.innerHtml  改变从起始到终止的内容,识别 html标签,空格与换行被保留
```
    <button class="xianshi">显示当前系统时间</button>
    <div class="time">某个时间</div>
    <p></p>
    <script>
        //改变元素(标签内)内容
        //1. element.innerText  改变从起始到终止的内容,但是它不识别html标签,同时空格与换行也被去掉
        //2. element.innerHtml  改变从起始到终止的内容,识别 html标签,空格与换行被保留


        //1.获取元素
        var btn = document.querySelector('.xianshi')
        var time = document.querySelector('.time')
        //2.添加事件
        btn.onclick = function () {
            //xianshi按钮被点击后，改变time标签内的值
            time.innerText = shijian()
        }

        //封装一个时间函数
        function shijian() {
            var time3 = new Date()
            var n = time3.getFullYear()  //年
            var y = time3.getMonth()    //月
            var r = time3.getDate()     //日
            var s = time3.getHours()    //时
            var f = time3.getMinutes()  //分
            var m = time3.getSeconds()  //秒
            var z = time3.getDay()  //周
            var zhou = ['星期日', '星期一', '星期二', '星期三', '星期四', '星期五', '星期六']
            var day = zhou[z]
            if (m < 10) {   //使1 2 3 变为 01 02 03
                m = '0' + m
            }
            return '当前时间为' + n + '年' + y + '月' + r + '日' + s + '时' + f + '分' + m + '秒 ' + day
        }


        //元素可以不添加事件直接使用  这样的效果就是p标签在页面被加载的时候就显示当前时间
        var timer = document.querySelector('p')
        timer.innerText = shijian()

    </script>
```
![](https://image.dcaoao.com/image/202211212033513.webp)

### innerText与innerHtml的区别  ###
innerText会直接输出 `<b>这是一段文字</b>`  不识别html标签
innerHtml会输出 这是一段文字 并且加粗,是识别html标签的
在实际开发中,innerHtml使用的比较多
```
    <div class="a1"></div>
    <div class="a2"></div>
    <p class="a3">
        第一行
        <b>第二行</b>
    </p>
```
```
        var a1 = document.querySelector('.a1')
        var a2 = document.querySelector('.a2')
        a1.innerText = '<b>这是一段文字</b>'   //innerText会直接输出 <b>这是一段文字</b>  不识别html标签
        a2.innerHTML = '<b>这是一段文字</b>'   //innerHtml会输出 这是一段文字 并且加粗,是识别html标签的
        //innerText与innerHtml可读可写，可以获取其中的内容
        var p = document.querySelector('.a3')
        console.log(p.innerText)
        console.log(p.innerHTML)
```
![](https://image.dcaoao.com/image/202211212034387.webp)


### 案例 使用按钮切换两张图片 ###
```
        <!-- 案例,操作元素 修改元素属性  使用按钮切换两张图片 -->
        <button class="a5">第一张</button>
        <button class="a6">第二张</button>
        <img src="https://image.dcaoao.com/image/202211211301097.webp" alt="" class="img" title="这是第一张图片">



        <script>
            //1.获取元素
            var a5 = document.querySelector('.a5')
            var a6 = document.querySelector('.a6')
            var img = document.querySelector('.img')
            //2.注册事件  处理程序
            a6.onclick = function() {
                img.src = 'https://image.dcaoao.com/image/202211211301077.webp'
                img.title = '这是第二张图片'
            }
            a5.onclick = function() {
                img.src = 'https://image.dcaoao.com/image/202211211301097.webp'
                img.title = '这是第一张图片'
            }

            // 可供更改的元素属性由很多 src href id alt title innerText与innerHtml改变元素内容
        </script>
```
![](https://image.dcaoao.com/image/202211212037110.gif)

### 操作元素 表单的属性设置 ###
`元素名.表单属性`
```
<body>
    <button class="genggai">更改表单默认值</button>
    <button class="jinyong">禁用此按钮</button>
    <button class="jiechu">解除禁用按钮</button>
    <input class="biaodan" type="text" value="这是一个表单">

</body>

<script>
    //获取元素
    var genggai = document.querySelector('.genggai')
    var jinyong = document.querySelector('.jinyong')
    var jiechu = document.querySelector('.jiechu')
    var biaodan = document.querySelector('.biaodan')

    //添加事件
    genggai.onclick = function() {
        biaodan.value = '这个默认值被更改了'
    }
    jinyong.onclick = function() {
        jinyong.disabled = true
        jinyong.innerHTML = '啊我被禁用了'
        jiechu.innerHTML = '有按钮被禁用'
    }
    jiechu.onclick = function () {
        //需要注意的是，函数内使用this 效果也是一样的
        this.disabled = false
        this.innerHTML = '啊我被你救了,感谢你'
        this.innerHTML = '已经解除禁用按钮'
    }
</script>
```
![](https://image.dcaoao.com/image/202211212040766.gif)

### 操作元素 修改样式属性 ###
可以更改颜色,大小,字体,字体大小等等等等....
格式 
`element.style`     行内样式操作
`element.className` 类名样式操作


`element.style`  
```
<style>
    /* 需要这个div的颜色可以点击来回切换 */
    div {
        width: 200px;
        height: 200px;
        background-color: skyblue;
    }
</style>

<body>
    <div></div>
</body>

<script>

    // 格式 
    // element.style       行内样式操作
    // element.className   类名样式操作

    //1.获取元素
    var div = document.querySelector('div')
    //2.注册事件与处理程序
    var flag = 0
    div.onclick = function () {
        if (flag == 0) {
            //采用驼峰命名法
            div.style.backgroundColor = 'red'
            div.style.width = '300px'
            flag = 1
        } else {
            div.style.backgroundColor = 'skyblue'
            flag = 0
        }
    }

    // 这样修改的style样式,产生的是行内样式,权重较高
</script>
```
![](https://image.dcaoao.com/image/202211212043232.gif)


`element.className` 

`element.className`适用于修改样式比较繁琐复杂的时候使用
首先需要在CSS中写好需要更改的样式
`element.className`会直接更改元素的类名，会覆盖掉之前的类名
如果需要保留原先的类名样式，可以使用 `this.className = 'a1 a2'`
```
<style>
    /* 这是原先的样式 */
    .a1 {
        width: 100px;height: 100px;
        background-color: cornflowerblue;
    }
    /* 这是变换的样式 */
    .a2 {
        width: 150px;height: 150px;
        background-color: teal;
        font-size: 18px;
        border: 1px solid red;
    }
</style>
<body>
    <div class="a1">123</div>
</body>


<script>
    //首先获取元素
    var a1 = document.querySelector('.a1')
    //注册事件
    a1.onclick = function() {
        //使用className更换为变换样式类名即可
        this.className = 'a2'
    }

    
</script>
```
![](https://image.dcaoao.com/image/202211221244444.png)


### 案例 开关灯 ###
要求:按钮控制页面颜色,并且在切换颜色后切换开灯关灯选项
```
<body>
    <button>关灯</button>
</body>
<script>
    var button = document.querySelector('button')
    var body = document.body
    var flag = 0
    button.onclick = function () {
        if (flag == 0) {
            body.style.backgroundColor = '#000'
            button.innerHTML = '开灯'
            flag = 1
        } else {
            body.style.backgroundColor = '#fff'
            button.innerHTML = '关灯'
            flag = 0
        }
    }
</script>
```
![](https://image.dcaoao.com/image/202211222234739.gif)

### 排他思想(算法) ###
首先是操作演示:![](https://image.dcaoao.com/image/202211222236106.gif)
思路:点击按钮的同时先将所有的按钮去除掉颜色,然后为点击的按钮上颜色
所有的按钮获取事件使用`for`循环
```
//首先获取所有按钮，得到的是一个伪数组
    var btns = document.querySelectorAll('button')
    //然后使用for循环将所有按钮添加事件
    for (var i = 0;i < btns.length;i++) {
        btns[i].onclick = function() {

            // 变色之前,去除所有按钮的颜色,使其恢复默认
            for (var i = 0;i < btns.length;i++) {
                //这里使用 btns[i] 是为了去除所有按钮颜色
                btns[i].style.backgroundColor = ''
            }
            //然后使被点击的按钮变为red颜色
            //这里使用this是为了选中那个被点击的按钮
            this.style.backgroundColor = 'red'
        }
    }
```

### 案例 密码框验证 ###
这是案例:
![](https://image.dcaoao.com/image/202211222245046.gif)
思路:输入框获得焦点时,显示提示文本,失去焦点时,判断文本是否符合要求,如果符合要求则显示正确,如果不符合要求则显示错误
```
<style>
    div {
        position: relative;
    }

    img {
        width: 20px;
        height: 20px;
        display: none;
        position: absolute;
        top: 3px;
    }

    span {
        color: #ccc;
        position: absolute;
        left: 200px;
        top: 3px;
        font-size: 12px;
    }

    .wenzi_dui {
        color: #11aa66 ;
    }
    .wenzi_cuo {
        color: #d81e06;
    }
</style>

<body>
    <div>
        <form action="">
            <!-- <span>请输入密码</span> -->
            <input type="text" name="" id="" class="input">
            <img class="imgs" src="https://image.dcaoao.com/image/202211221153736.png" alt="">
            <span class="wenzi"></span>
        </form>
    </div>
</body>
<script>
    //1.获取事件
    var input = document.querySelector('.input')
    var imgs = document.querySelector('.imgs')
    var wenzi = document.querySelector('.wenzi')
    //2.处理程序
    //获得焦点,显示要求文本
    input.onfocus = function () {
        imgs.style.display = 'inline'
        imgs.src = 'https://image.dcaoao.com/image/202211221153736.png'
        wenzi.innerHTML = '请输入6~16位密码,区分大小写'
    }
    //失去焦点,判断密码是否符合,使用if语句
    input.onblur = function () {
        if (input.value.length < 6 || input.value.length > 18) {
            imgs.src = 'https://image.dcaoao.com/image/202211221214145.png'
            wenzi.innerHTML = '请输入至少6-18位的密码'
            wenzi.className = 'wenzi_cuo'
        } else {
            imgs.src = 'https://image.dcaoao.com/image/202211221232480.png'
            wenzi.innerHTML = '密码符合规范'
            wenzi.className = 'wenzi_dui'
        }
    }

</script>
```

### H5新增 获取属性值 ###
获取元素的属性值:
有两种办法
1.`Element.属性` 这种只能获取到`内置属性`,id,value,之类
2.`Element.getAttribute('属性')` 这种可以获取到`自定义属性`的值,也就是程序员自己添加的属性
```
<div id="a1" class="a" index="1" data-list="自定义属性值List" data-get-name="自定义属性getName"></div>

 <script>
// 1.Element.属性 这种只能获取到内置属性,id,value,之类
            var a = document.querySelector('.a')
            console.log(a.id)  //返回id值  a1

// 2.Element.getAttribute('属性') 这种可以获取到自定义属性的值,也就是程序员自己添加的属性
console.log(a.getAttribute('index'))  //返回index自定义属性值
</script> 
```
自定义属性值 需要注意的是，自定义属性值规范以 data 开头，方便辨认
data-index  data-list 等
获取自定义属性值有两种方法，
第一种是上方的 Element.getAttribute('自定义属性值')，兼容性较好
第二种为 Element.dataset.自定义属性值  只能取data开头的自定义属性，兼容性只在IE11开始支持
```
console.log(a.dataset.list)  //取data-list的自定义属性值
```
如果碰上data-get-name这种较长的属性名  后面需要遵循驼峰命名法
```
console.log(a.dataset.getName)
```

### H5新增 修改属性值 ###
修改元素的属性值
1.`Element.属性 = '属性值'`
2.`Element.setAttribute('属性','要修改的属性值')`

```
            //1.Element.属性 = '属性值'
            a.id = 'a2'   //直接赋值,只能修改内置属性
            a.className = 'b'  //className这个比较特殊
            console.log(a.id)   //返回a2

                // 2.Element.setAttribute('属性','要修改的属性值')
              //可以修改自定义属性,也可以修改内置属性
            a.setAttribute('index',2)
            // console.log(a.getAnimations('index'))
            console.log(a.getAttribute('index'))
```

移除元素的属性 removeAttribute(属性)
```
a.removeAttribute('index')  //index属性被移除  <div id="a2" class="b"></div>
```

### 节点操作 ###
节点操作一般比较方便
 #### 获取父节点 ####
 父节点操作使用 : `parentNode`
 ```
     <!-- 获取父节点  parentNode -->
    <div class="box">
        <span class="erweima">123</span>
    </div>


    //获取父节点  parentNode
    //首先声明一个子节点用于'定位'
    var erweima = document.querySelector('.erweima')
    //然后获取最近的父节点
    console.log(erweima.parentNode)
    // 返回父级div标签  如果找不到父级节点，则 返回为空

```

 #### 获取子节点 ####
 ```
     <ul>
        <li>ul内的li</li>
        <li>ul内的li</li>
        <li>ul内的li</li>
        <li>ul内的li</li>
        <li>ul内的li</li>
    </ul>

    //获取子节点  
    //1.childNodes 可获取到所有的子节点 元素节点 文本节点等，一般不提倡使用，获取的数据需要单独处理
    var ul = document.querySelector('ul')
    console.log(ul.childNodes)  //明明ul内只有五个li,却获取到了11个节点,因为换行符等也包括在内
    //2.children 获取所有子元素节点 兼容性较好  返回伪数组样式
    console.log(ul.children)  //[li, li, li, li, li]  五个li被全部获取
```


#### 获取第一个子元素和最后一个子元素 ####
```
    <ol>
        <li>ol内第一个</li>
        <li>ol内的li2</li>
        <li>ol内的li3</li>
        <li>ol内的li4</li>
        <li>ol内最后一个</li>
    </ol>


    //1.firstChild 与lastChild  获取的是 第一个/最后一个 子节点，不管是文本还是元素节点 
    var ol = document.querySelector('ol')
    console.log(ol.firstChild)  //返回第一个子节点，不论类型
    console.log(ol.lastChild)  //返回最后一个子节点，不论类型
    //2. firstElementChild 与 lastElementChild 获取第一个元素节点与最后一个元素节点
    //兼容性需要注意，IE9才开始支持 
    console.log(ol.firstElementChild)
    console.log(ol.lastElementChild)
    //获取开头与结尾的实际开发写法 没有兼容性问题 使用children伪数组获取
    console.log(ol.children[0])  //获取开头
    console.log(ol.children[ol.children.length - 1])  //获取结尾
```

#### 获取兄弟节点 ####
```
    <div class="xiongdi">兄弟一号</div>
    <span>兄弟二号</span>


    var xiongdi = document.querySelector('.xiongdi')
    //1. nextSibling 获取下一个兄弟节点 包含元素节点与文本节点
    console.log(xiongdi.nextSibling)  //返回文本节点
    //2.previousSibling 获取上一个兄弟节点 包含元素节点与文本节点
    console.log(xiongdi.previousSibling)
    //3. nextElementSibling  获取下一个兄弟元素节点
    console.log(xiongdi.nextElementSibling)  //返回 <span>兄弟二号</span>
    //4.previousElementSibling 获取上一个兄弟元素节点
    console.log(xiongdi.previousElementSibling)  //同上
    //需要注意的是,3和4有兼容性问题需要注意,在IE9才开始支持,如果需要考虑兼容性问题获取兄弟元素,可以封装一个兼容性函数
    function xiongdi(canshu){
        while (canshu = canshu.nextSibling) {
            //如果节点类型等于1 那就输出这个节点  元素节点的类型为1
            if(canshu.nodeType === 1) {
                return canshu
            }
        }
        return null
    }
```

#### 创建元素节点 ####
```
<ul class="chuangjian"></ul>

    // 如果想要在页面中添加新元素,分两步  1.创建元素  2.添加元素
    //1.创建元素子节点  document.createElement('标签')
    var li = document.createElement('li')
    var div = document.createElement('div')
    
    //2.添加节点 node.appendChild(child)    node为父级元素  child为刚刚创建的子级元素  在其最后方追加元素
    var chuangjian = document.querySelector('.chuangjian')  //声明父节点
    chuangjian.appendChild(li)
    chuangjian.appendChild(div)

    //3.在指定位置前面添加字元素 node.insertBefore(child,指定元素)
    var span = document.createElement('span')
    chuangjian.insertBefore(span,chuangjian.children[1])  //在div前面添加了span标签

    //innerHTML创建多个元素效率更高，采用数组形式
    // createElement() 创建多个元素效率稍微低一点点,但是结构更加清晰
```

需要注意的是,创建一个元素节点,只能插入一次,如果需要多个,则使用for循环
#### 删除元素节点 ####
```
    <button class="delan">删除按钮</button>
    <ul class="del">
        <li>熊大</li>
        <li>熊二</li>
        <li>光头强</li>
        <li>又来砍树</li>
        <li>咧</li>
    </ul>



    //node.removeChild(child)   父节点.removeChild(要删除的子节点)  
    var del = document.querySelector('.del')
    var delan = document.querySelector('.delan')  //获取删除按钮
    delan.onclick = function() {
        //添加if判断是否还有空余字段 如果没有则禁用按钮并且提示
        if (del.children.length == 0) {
            delan.disabled = true
            alert('没得可以删的了')
        } else {
            del.removeChild(del.children[0])
        }
    }
```

#### 复制节点   ####
`node.cloneNode()`  `要复制的节点.cloneNode()  `
如果cloneNode()内的值为空或者为false 则是浅拷贝 仅克隆节点本身,不克隆里面的内容以及子节点
如果cloneNode()内参数为true 则是深拷贝 会复制节点本身以及里面所有的子节点

```

    <!-- 复制节点 -->
    <ul class="copyf">
        <li class="copy">1</li>
        <li>2</li>
        <li>3</li>
    </ul>


    var copy = document.querySelector('.copy')
    var copyf = document.querySelector('.copyf')
    copyf.appendChild(copy.cloneNode())  //浅拷贝,仅拷贝了li标签
    copyf.appendChild(copy.cloneNode(true))  //深拷贝,连带li的内容一起拷贝
```

### DOM重点核心 ###
 DOM主要就是 创建 增 删 改 查 属性操作 事件操作
#### 创建: #### 
 ```
        document.write
        innerHTML
        createElement
```
#### 增: #### 
```
        appendChild
        insertBefore
```
#### 删: #### 
```
removeChild
```
#### 改: #### 
主要修改dom的元素属性，dom元素的内容 属性，表单的值
修改元素属性 ：`src` `href` `title`
修改普通元素内容： `innerHTML` `innerText`
修改表单元素： `value` `type` `disabled`
修改元素样式： `style` `className`

#### 查: #### 
主要获取查询DOM元素
DOM提供的API方法 `getElementById`   `getElementByTagName`    用法古老不推荐
H5新增的方法： `querySelector`  `querySelectorAll`   提倡
利用节点操作获取元素  父`(parenNode)` 子`(children)` 兄`(previousElementSibling)`   (`nextElementSibling)`  提倡

#### 属性操作 : #### 
设置DOM的属性值：`setAttribute`
得到DOM的属性值：`getAttribute`
移除属性：`removeAttribute`


#### 事件操作:   目前学习的是鼠标类事件 经过点击离开移动之类 #### 
事件源.事件类型 = 事件处理程序.


## DOM事件高级导读 ##
 注册事件概述
给元素添加事件,称为注册事件或者绑定事件
注册事件由两种方式:`传统方式`  `方法监听注册方式`

`传统注册方式`: 利用`on开头`的事件  `onclick`
特点: 注册事件的`唯一性`
同一个元素同一个事件`只能设置一个处理函数`,最后的处理函数会`覆盖`掉前面的处理函数


`方法监听注册方式`:
w3c标准推荐模式
`addEventListener()`   是一个`方法`
IE9之前不支持  可以使用 `attachEvent()` 代替其兼容性问题
特点:同一个元素同一个事件可以注册多个处理函数,并且按照注册顺序`依次执行`
格式: `eventTarget.addEventListener(type,listener[,useCapture])`
接收三个参数: 
`type`: 事件类型字符串 比如 click mouseover 不需要带on
`listener`:事件处理程序 事件被触发时,调用该函数  就是 function() {}
`useCapture`: 可选参数 `布尔值` 默认false

案例: HTML代码
```
<body>
    <button>传统事件注册方式</button>
    <button>事件侦听注册事件</button>
    <button>传统事件删除方式</button>
    <button>事件侦听删除事件</button>
</body>
```

### 传统事件注册方式 ###
```
    var btns = document.querySelectorAll('button')
    btns[0].onclick = function() {
        alert('这是第一次注册')
    }
    btns[0].onclick = function() {
        alert('这是第二次注册')
    }
    //后注册的事件会将第一次注册的事件覆盖掉
```
`alert('这是第一次注册')`会被直接覆盖掉,无法显示
![](https://image.dcaoao.com/image/202211252046325.png)


### 事件侦听注册事件   ###
需要注意的是，事件类型是字符串类型,而且不带on
`btns[1].addEventListener('事件类型',function(){}`
```
    btns[1].addEventListener('click',function() {
        alert('事件侦听注册一次')
    })
    btns[1].addEventListener('click',function() {
        alert('事件侦听注册二次')
    })
```
会依次执行,不会覆盖掉前面的事件
![](https://image.dcaoao.com/image/202211252049374.gif)

### 传统方式删除事件 ###
使事件直接等于 `null`即可
```
    btns[2].onclick = function () {
        alert('事件已被删除')
        btns[2].onclick = null
    }
```

### 事件侦听删除事件 ###

```
    btns[3].addEventListener('click' , fn)  //这里注册事件，直接填写函数名

    function fn () {
        alert('首先注册事件')
        btns[3].removeEventListener('click',fn) //然后函数内删除事件
    }
```

### 事件对象 ###

1.e 就是一个事件对象 写到侦听函数的小括号内 当形参来看
2.事件对象只有存在事件后才会存在,是系统自动创建的,不需要传递参数
3.事件对象是事件一系列相关数据的集合,跟事件相关的,比如鼠标点击 鼠标坐标 如果是键盘事件则就包含键盘事件的信息,比如判断按下了哪个键
4.事件对象可以自己命名 event evt e都可以 随便写
5.当然,也有兼容性问题 IE678只能通过windows.event来获取 可以使用 e = e || windows.event 来解决兼容性问题

事件对象
`document.onclick = function(事件对象名) {}`
传统方式获取事件对象
```
    var div = document.querySelector('div')
    div.onclick = function(e) {
        e = e || windows.event  //解决IE678的兼容性问题
        console.log(e)   //返回的是一个对象  事件对象
    }
```

使用事件监听方法进行获取事件对象
```
    div.addEventListener('click',function(e) {
        console.log(e)
    }) 
```

#### 常见事件对象的属性和方法 ####

1.`e.target`  返回的是触发事件的对象(元素)   `this` 返回的是绑定事件的元素
2. e.srcElement  也是返回触发事件的对象 但是为非标准 IE678使用 一般不使用
两者的区别在于 `e.target` 只会谁触发就返回谁  `this`只能返回绑定了事件的元素

```
var ul = document.querySelector('ul')
//此处给ul绑定了事件
ul.onclick = function(e) {
    e = e || windows.event
    console.log(e.target)
    console.log(this)
}
//输出可以看到 点击li, e.target会返回 li元素  this只能返回绑定了事件的 ul
```
![](https://image.dcaoao.com/image/202211252100544.gif)

#### 返回事件类型  ####
`e.type`
```
var ol = document.querySelector('ol')
ol.addEventListener('click' , fn)
ol.addEventListener('mouseover' , fn)
ol.addEventListener('mouseout' , fn)

function fn (e) {
    console.log(e.type)  //会返回事件触发对象类型
}
```
![](https://image.dcaoao.com/image/202211252101483.png)

#### 阻止默认行为(事件) ####
比如说链接不跳转  按钮不提交

事件监听写法阻止默认事件:
1.`preventDefault()`

```
<body>
    <!-- 阻止默认行为(事件)  比如说链接不跳转  按钮不提交 -->
    <a href="www.baidu.com">跳转链接</a>
    <form action="www.baidu.com">
        <button>提交</button>
    </form>
</body>


var a = document.querySelector('a')

//为a标签注册事件
a.addEventListener('click',function(e){
    //然后阻止其默认行为,也就是跳转
    e.preventDefault()
})

```

传统注册方式阻止默认事件:
```
 var button = document.querySelector('button')
 button.onclick = function(e) {
    //普通浏览器
    e.preventDefault()
    //低版本浏览器 兼容性问题 IE678
    e.returnValue;
    //最简单的写法,无需考虑兼容性问题  但是其后方的代码就无法执行了,需要注意
    return false
 }
 ```

 preventDefault()还有其他用法:
 比如禁用右键菜单contextmenu ，禁止选中文字selectstart

 ```
 //禁用右键菜单contextmenu
document.addEventListener('contextmenu',function(e){
    e.preventDefault()
})
//禁止选中文字selectstart
document.addEventListener('selectstart',function(e){
    e.preventDefault()
})
```

### 阻止冒泡&冒泡排序 ###
冒泡排序:
 当 addEventListener 的第三个参数为 `true`时,事件会按照`捕获顺序`进行执行 document > father > son  其平时默认为false
 在其值为false时 在父,子元素都拥有事件的时候,程序会按照`冒泡排序`进行依次传递执行 son > father > document 

 因为有冒泡排序的存在,点击son后,father与document都被执行了
 ![](https://image.dcaoao.com/image/202211252108377.gif)

 这时候就需要阻止冒泡排序 使用 `e.stopPropagation()`或者 `e.cancelBubble = true`
 `e.stopPropagation()` IE678无法使用,这时候就需要使用  `e.cancelBubble = true` 来解决兼容性问题

 ```
 <body>
     <div class="father">father
        <div class="son">son</div>
    </div>
</body>

<script>
 var son = document.querySelector('.son')
 son.addEventListener('click',function(e) {
    alert('son')
    e.stopPropagation()  //在son处阻止冒泡排序
    // e.cancelBubble = true
 })

  var father = document.querySelector('.father')
 father.addEventListener('click',function(e) {
    alert('father')
 })

  document.addEventListener('click',function(e) {
    alert('document')
 })
</script>
```
 在son处阻止冒泡排序后,如果点击其父元素,发现冒泡排序操作还可以继续进行,如果需要继续阻止,则在父元素添加 `e.stopPropagation`即可


### 事件委托(代理 委派) ###
要求点击任意一个li就可以出现弹窗,如果一个个的为li单独设置事件监听器就很麻烦,可以利用冒泡排序,在其父元素上设置节点,然后利用冒泡排序影响每个子节点
给ul注册点击事件,然后利用事件对象的`target`获取当前点击的li,因为点击了li 事件会冒泡到ul上
```
<body>
    <ul class="weituo">
        <li>我弹框呢1</li>
        <li>我弹框呢2</li>
        <li>我弹框呢3</li>
        <li>我弹框呢4</li>
        <li>我弹框呢5</li>
        <li>我弹框呢6</li>
        <li>我弹框呢7</li>
        <li>我弹框呢8</li>
        <li>我弹框呢9</li>
    </ul>
</body>
<script>
var weituo = document.querySelector('.weituo')
weituo.addEventListener('click',function(e) {
    alert('弹窗')  //不管点击哪个li，都会出现弹窗
    console.log(e.target.innerHTML)  //获取当前点击的li的内容 输出到控制台
    e.target.style.backgroundColor = 'red'   //点击谁就将谁变为红色
})
</script>
```
事件委托的作用: 只操作了一次DOM 提高了程序的性能
![](https://image.dcaoao.com/image/202211252113738.gif)


### 鼠标事件对象  ###
获取鼠标在可视区的X Y 轴坐标:`e.clientX` `e.clientY`
获取鼠标在页面文档的x和y轴坐标: `e.pageX` `e.pageY`
获取鼠标相对于电脑屏幕的X Y轴坐标 :`e.screenX` `e.screenY`
```
    document.addEventListener('click',function(e) {
        //client 获取鼠标在可视区的X Y 轴坐标  可视区是指浏览器可见页面
        console.log(e.clientX)
        console.log(e.clientY)
        //page  获取鼠标在页面文档的x和y轴坐标 IE9+支持
        console.log(e.pageX)
        console.log(e.pageY)
        //screen  获取鼠标相对于电脑屏幕的X Y轴坐标  从屏幕最边处开始计算
        console.log(e.screenX)
        console.log(e.screenY)
    })
```

`MouseEvent`  只要鼠标移动就会被触发

```
<style>
    img {
        position: absolute;
        width: 100px;height: 100px;
    }
</style>
<body>
    <img src="https://image.dcaoao.com/image/202211261535451.jpg" alt="">
</body>
<script>

    var img = document.querySelector('img')
    document.addEventListener('mousemove',function(e) {
        console.log('X坐标为:' + e.pageX + 'Y坐标为:' + e.pageY)
        img.style.top = e.pageY + 'px'
        img.style.left = e.pageX + 'px'
    })
```

![](https://image.dcaoao.com/image/202211262211812.gif)


### 键盘事件对象 ###

`onkeyup` 任意按键被松开时触发  `不区分大小写`
```
    document.onkeyup = function (e) {
        console.log('被松开了')
    }
```

`onkeydown`任意按键被按下时触发  只要不松开就会被一直触发 不区分大小写
```
    document.onkeydown = function (e) {
        console.log('被按下了')
    }
```

`onkeypress` 按键被按下时触发  只要不松开就会被一直触发  但是不识别功能键 ctrl shift之类
```
    document.onkeypress = function (e) {
        console.log('被按下了-')
    }
```

这三个事件如果都存在,则执行的顺序是 `keydown` -> `keypress` -> `keyup`


获取按键的ASCII码 并且区分大小写
`onkeypress`可以获取键盘按下事件,并且区分大小写
`keyCode`可以输出被按下键的ASCII值
```
    document.onkeypress = function (e) {
        console.log(e.keyCode)
    }
```


### 案例 当按下键盘s键时,输入框获得焦点 并且在输入框下方显示放大输入的内容 ###

```

<style>
    div {
        /* display:inline-block; */
        margin-top: 3px;
        border: 1px solid #ccc;
        width: 200px;
        height: 30px;
        font-size: 20px;
        display: none;
        box-shadow: 0.2px 0.2px 15px #666;
    }
</style>

<body>
    <input type="text"><br>
    <div></div>
</body>
<script>
    var input = document.querySelector('input')
    var div = document.querySelector('div')
    document.addEventListener('keyup', function (e) {
        //使文本框获得焦点
        if (e.keyCode === 83) {
            input.focus()
        }
    })
    input.addEventListener('keyup', function (e) {
        //当输入框内有键盘事件 则显示放大框 
        div.innerText = input.value
        div.style.display = 'block'
    })
    // 文本框失去焦点时,隐藏放大框
    input.onblur = function () {
        div.style.display = 'none'
    }
    //判断输入框是否为空,如果为空则不显示放大框,如果已经存在内容,则显示放大框
    input.onclick = function () {
        if (input.value != '') {
            div.style.display = 'block'
        }
    }
</script>
```

结果:
![](https://image.dcaoao.com/image/202211262216022.gif)


## BOM ##
### BOM的构成 ###

 window对象是浏览器最顶级的对象,具有双重角色
1.他是JS中访问浏览器窗口的一个`接口`
2.它是一个全局对象,定义在`全局作用域`中的变量 函数 都会变成window对象的属性和方法

在调用的时候可以省略window,比如 `alert()  prpompt()`等  也可以写成`window.alert()  window.prpompt()`   效果相同
window下有一个特殊属性 `window.name`  一般变量命名不要使用


### window的常见事件 ###
1.窗口加载事件 `onload`  当文档内容完全加载完成后会被触发 包括图片 脚本 css等
`window.onload`可以把JS代码写到页面元素的上方 因为onload是页面`全部加载完毕`再去执行处理函数

```
<script>
        //传统方式注册 只能写一次，后面的onload会覆盖掉前面的  使用事件监听方式注册即可
        window.onload = function() {
            var button = document.querySelector('button')
            button.addEventListener('click' ,function() {
                alert('加载完毕1')
            })
        }
        //事件监听方式注册
        window.addEventListener('load',function() {
            var button = document.querySelector('button')
            button.addEventListener('click' ,function() {
                alert('加载完毕2')
            })
        })
</script>
<body>
    <button>按钮</button>
</body>
```

2.DOM加载事件 `DOMContentLoaded` 是DOM加载完毕 不包含图片 falsh css 等就可以执行 比 load更快一些
```
        document.addEventListener('DOMContentLoaded' ,function() {
            alert('DOM加载完毕')
        })
```


3.调整窗口大小事件查询  
```
//onresize 当窗口大小改变时就会被触发  一般用来使用响应式布局 配合window.innerWidth获取当前屏幕宽度
        window.onresize = function () {}
        window.addEventListener('resize',function(){})

        window.onresize = function () {
            console.log('窗口大小改变')
            console.log(window.innerWidth)

            //搭配window.innerWidth来响应式布局 
            var div = document.querySelector('div')
            // 当窗口宽度小于800px,则隐藏div元素  反之则显示
            if(window.innerWidth < 800) {
                div.style.display = 'none'
            } else {
                div.style.display = 'block'
            }
        }
```


### 定时器 ###
1.`setTimeout()` 一次性定时器
语法： `windows.setTimeout(调用函数,延迟的毫秒数)`
延时单位是毫秒 可以省略 省略默认为0
调用函数可以直接写函数  也可以直接写函数名 也可以 `'函数名()'`
页面中有很多的定时器时 可以给定时器命名
setTimeout() 其中的函数被称为回调函数 `callback`
普通函数式按照代码顺序直接调用，而回调函数，需要等待时间到了之后才会被执行
意思就是由前置条件 前置条件完成才会调用执行这个函数
`element.onclick = function(){}`  或者 `element.addEventListener('click',fn)` 里面的函数也是回调函数.


定时器内直接写函数:
```
    var time1 = setTimeout(function() {
        console.log('延迟函数被执行')
    },5000)
```

定时器调用外置函数:
```
//创建一个函数
    function say () {
        console.log('外置函数调用')
    }
    //调用函数
    var time2 = setTimeout(say,6000)
```

1.1 停止定时器 `clearTimeout(停止的定时器名称)`
```
    var timeout = document.querySelector('.timeout')
    timeout.addEventListener('click',function(){
        clearTimeout(time2)
    })
```



2.`setInterval()` 重复调用函数定时器
语法： `setInterval(调用函数，延时时间)`
语法与`setTimeout`相同，时间到了之后便会去调用函数，重复调用
```
    var Interval = setInterval(function() {
        console.log('setInterval 执行一次')
    },1000)
```


2.1  停止`setInterval`定时器  `clearInterval(停止的函数名)`
```
    var Interval_btn = document.querySelector('.Interval')
    Interval_btn.addEventListener('click',function(){
        clearInterval(Interval)
    })
```



### JS执行机制 ###
IS执行的时候,会将任务分为`同步任务`与`异步任务`,同步任务会先被执行,异步任务则等待同步任务执行完毕后才会被执行
JS中异步任务一般是通过`回调函数`来执行
1.普通事件 `click` `resize`等
2.资源加载 `load` `error`等
3.定时器 `setInterval` `SetTimeout`等

`同步任务`相当于主线程，会不断的去异步任务线程池查看有没有新的任务，然后执行 这种机制被称为`事件循环`(event loop)

![](https://image.dcaoao.com/image/202211271509704.png)


### location对象的属性 ###

        location.href  //获取或者设置整个URL  如果给予一个新的地址，则会跳转到新的页面
        location.host  //返回主机域名
        location.port //返回端口号 如果未写则返回空字符串
        location.pathname  //返回路径
        location.search //返回参数
        location.hash //返回片段 #后面内容 常见于锚点
        location.assign()   //与href一样 可以跳转页面 
        location.replace()  //替换当前页面 但是不记录历史 因此不能后退页面
        location.reload()  //刷新当前页面 相当于F5 如果参数为true则为 ctrl + F5


`www.baidu.com:80/index.html?name=1&age=2#nov`
主机域名:端口/路径?参数#片段

```
    var button = document.querySelector('button')
    button.addEventListener('click',function() {
        // location.assign()  重定向页面 可以后退
        location.assign('http://baidu.com')
        // location.replace() 替换页面 不可后退
        location.replace('http://baidu.com')
        // location.reload()  刷新页面 相当于f5
        location.reload(true)
    })
```

附带 `navigator对象` 包含了浏览器的相关信息 可以查看UA

#### 案例 5秒后自动返回主页 ####
```
   //案例 5秒后自动返回主页
    var time = 5
    var div = document.querySelector('div') 
    setInterval(fn, 1000)
    function fn() {
        time--
        div.innerHTML = '您将在' + time + '秒后返回主页'
        if (time == 0) {
            location.href = 'http://baidu.com'
        }
    } 
```


### history对象 ###
`history`对象可以为浏览器提供前进 后退 的功能
`history.back()`  //后退页面
`history.forward()`  //前进页面
`history.go(数字)`  //正数前进，负数后退 


## PC网页特效 ##

### 元素偏移量 offset系列 ###
offset用来获取子元素距离父级元素的距离 前提是父级元素带有定位，如果没有父级元素或者没有定位 则以`body为准`
    `element.offsetParent`  返回该元素带有定位的父级元素 如果找不到则返回body
    `element.offsetTop`    返回带有`定位`的父级元素上方的距离
    `element.offsetLeft`    返回带有`定位`的父级元素左方的距离
    `element.offsetWidth`   返回包括自身padding 边框 内容区的宽度 返回值`不带单位`
    `element.offsetHeight`  返回包括自身padding 边框 内容区的高度 返回值`不带单位`

```
<style>
    .fu {
        width: 200px;height: 300px;
        background-color: red;
        margin: 150px;
        position: relative;
        padding: 10px;
    }
    .zi {
        width: 50px;height: 50px;
        margin: 100px;
        background-color: skyblue;
    }
</style>
<body>
    <div class="fu">
        <div class="zi"></div>
    </div>
    
</body>
<script>
    var fu = document.querySelector('.fu')
    var zi = document.querySelector('.zi')
    //offsetTop
    console.log(fu.offsetTop)   //因为 fu 的上层父元素是body 所以获取了body距离自己的距离
    //offsetLeft
    console.log(zi.offsetLeft)   //因为 zi 的上层父元素是fu 还带有定位  获取了fu距离自己的距离
    //offsetWidth
    console.log(fu.offsetWidth)  //返回 fu 的宽度  220
    //offsetHeight
    console.log(fu.offsetHeight)  //返回 fu 的高度  320
    //offsetParent
    console.log(zi.offsetParent)  //zi 的父级元素是 fu 所以返回  fu标签
</script>
```

`offset`与`style`的区别

`offset`:
`offset`可以得到任意样式表中的样式值
`offset`系列获取到的值没有单位
`offsetWidth`获取到的值包含padding+border+width
`offset`获取到的值是只读属性,只能获取不能赋值
所以,获取元素的位置或者大小 使用`offset`更加合适


`style`:
`style`只能获取行内样式表的值
`style.width` 获得的是带有单位的字符串
`style.width` 获取到的值不包含padding+border
`style.width` 是可读可写  可以取值也可以赋值
所以给元素更改数值 使用`style`更加合适


### 案例 鼠标拖拽 ###
```
<style>
    form {
        position: absolute;
        top: 30%;
        left: 50%;
        width: 700px;
        height: 300px;
        transform: translate(-50%);
        border: 1px solid #ccc;
    }
</style>

<body>
    <div>
        <form action="#">
            账号:<input type="text">
            密码:<input type="text">
            <button>登录</button>
        </form>
    </div>
</body>
<script>
    var form = document.querySelector('form')
    form.addEventListener('mousedown', function (e) {
        //获取当前鼠标在移动框的坐标
        var x = e.pageX - form.offsetLeft
        var y = e.pageY - form.offsetTop

        //开始设置盒子坐标
        var XY =  form.addEventListener('mousemove', shubiaoXY)

        function shubiaoXY(e) {
            //使用鼠标距离页面的坐标减去鼠标在移动框中的坐标，获取到的是盒子的坐标，进而附加设置
            form.style.left = e.pageX - x + 'px'
            form.style.top = e.pageY - y + 'px'
        }

        //鼠标弹起,移除，也就是停止设置盒子坐标
        //鼠标弹起后执行
        form.addEventListener('mouseup',function() {
            //鼠标弹起后，只要鼠标移动，就移除设置盒子坐标函数
            form.removeEventListener('mousemove',shubiaoXY)
        })

    })
</script>
```
![](https://image.dcaoao.com/image/202211282058979.gif)


### 元素可视区 client 系列 ###

`client`翻译过来就是客户端 使用client系列来获取元素可视区的相关信息 可以动态获取到该元素的相关属性 边框大小 元素大小
`element.clientTop`   获取元素上边框的大小
`element.clientLeft`  获取元素左边框的大小
`clcmcnt.clientWidth`  获取自身包括 padding 内容区的宽度 不包含边框 不带单位
`clcmcnt.clientHeight`  获取自身包括 padding 内容区的高度 不包含边框 不带单位


### 元素scroll 属性
`Element.scroll` 属性可以获取或设置一个元素的内容垂直滚动的像素数。
`scroll`可以获取元素的大小 滚动间距等
`scrollY `  返回文档在垂直方向已滚动的像素值
`element.scrollTop`  获取元素被卷上去的上侧距离 返回值不带单位
`element.scrollLeft` 获取元素被卷去左侧的距离 返回值不带单位
`element.scrollWidth` 获取元素自身实际的宽度 不含边框 不带单位
`element.scrollHeight` 获取元素自身实际的高度 不包含边框 不带单位  实际高度是指内容的高度,而不是容器的高度


`scroll`是滚动事件，只要有滚动条就会被触发
```
var div = document.querySelector('div')
scroll是滚动事件，只要有滚动条就会被触发
div.addEventListener('scroll',function(){
//获取被滚动上去的距离
    console.log('获取被滚动上去的距离' + div.scrollTop)
    console.log('获取实际高度' + div.scrollHeight)
                })
```

### 三大系列总结 ###
  `element.offsetWidth`  返回自身包括padding 边框 内容区的宽度 不带单位      常用于获取元素位置
  `element.clientWidth`  返回自身包括padding 内容区的宽度 不含边框 不带单位  常用于获取元素大小
  `element.scrollWidth`  返回自身职级宽度 不含边框 不带单位                  常用于获取滚动距离
  页面的滚动可以使用`window.pageXOffset` 或者 `scrollY`

![](https://image.dcaoao.com/image/202211291948201.png)
### 案例 淘宝侧边栏 ###
```
<style>
    .a1 {
        width: 80%;
        height: 100px;
        margin: 0 auto;
        background-color: skyblue;
    }
    .a2 {
        width: 80%;
        height: 500px;
        margin: 0 auto;
        background-color: steelblue;
    } 
    .a3 {
        width: 80%;
        height: 800px;
        margin: 0 auto;
        background-color: yellow;
    }
    .a5 {
        width: 30px;
        height: 100px;
        background-color: royalblue;
        position: absolute;
        top: 150px;
        right: 103px;
    }
    .a6 {
        width: 30px;
        height: 50px;
        background-color: red;
        position: absolute;
        top: 150px;
        right: 103px;
        display: none;
        font-size: 10px;
        color: #fff;
        line-height: 50px;
    }
</style>
<body>
    <!-- 页面内容 -->
    <div class="a1"></div>
    <div class="a2"></div>
    <div class="a3"></div>
    <div class="a5"></div>
    <div class="a6">返回顶部</div>
</body>

<script>
    //获取页面被卷去的头部大小
    var a1 = document.querySelector('.a1')
    var a5 = document.querySelector('.a5')
    var a6 = document.querySelector('.a6')
    console.log(a5.offsetTop - a1.scrollHeight)
    //使用侧边栏距离顶部的距离 减去第一栏的高度  获取变化定位变化时的数据
    var fixedTop = a5.offsetTop - a1.scrollHeight

    window.addEventListener('scroll',function() {
        console.log(window.scrollY)   //window.pageYOffset 获取页面被卷上去的高度  同等于 scrollY 
        
        if (window.scrollY >= a1.scrollHeight) {
            a5.style.position = 'fixed'
            // 设置下拉时参数变化
            a5.style.top = fixedTop + 'px'
            
            // 返回顶部框显示
            a6.style.display = 'block'
            a6.style.position = 'fixed'
        } else {
            a5.style.position = 'absolute'
            a5.style.top = '150px'
            // 返回顶部框恢复
            a6.style.display = 'none'
            a6.style.position = 'absolute'
        }
    })
</script>
```

![](https://image.dcaoao.com/image/202211292001305.gif)
### 立即执行函数 ###
立即执行函数有两种
1. `(function(){})()`  可以看做一个小括号包含了匿名函数,然后最外部的一个小括号可以看做是调用了函数 可以写实参
2. `(function(){}())`  一个小括号包含了匿名函数 花括号 小括号 最后一个小括号看做调用 可以写实参

```
        // 第一种写法
        (function name1(a,b){
            console.log(a + b)  //结果为3
        })(1,2);//传入实参  如果有多个立即执行函数 需要结尾处写分号来结束，不然会报错
    
        // 第二种写法
        (function name2(z,x){
            console.log(z * x)
        }(6,3))
```
立即执行函数的最大作用是 创建了第一独立的作用域 里面所有的变量都是局部变量 不会有命名冲突的情况,也是页面加载后第一个加载的函数


### 动画的原理 ###
1.获取当前盒子位置 offset
2.让盒子在当前位置加移动距离
3.使用定时器重复这个流程
4.添加一个定时器结束条件
5.元素记得定位
6.封装动画函数前，首先结束一次这个函数，防止多次触发
7.顺便为了避免小数的出现 使用向上取整Math.ceil  与向下取整 Math.floor

```
   <style>
        div {
            width: 100px;
            height: 100px;
            background-color: skyblue;
            position: absolute;
        }

        span {
            width: 100px;
            height: 100px;
            background-color: red;
            display: block;
            position: absolute;
            margin-top: 150px;
        }
    </style>
</head>

<body>
    <div></div>
    <span></span>
    <button class="d500">按钮到500</button>
    <button class="d800">按钮到800</button>
</body>
<script>
    var div = document.querySelector('div')
    var span = document.querySelector('span')
    var d500 = document.querySelector('.d500')
    var d800 = document.querySelector('.d800')
    //动画函数封装

    function yidong(name, zhi ,huidiao) {
        //封装动画函数前，首先结束一次这个函数，防止多次触发
        clearInterval(name.gif)

        // 使用定时器重复这个流程，并且利用函数 给不同对象添加不同定时器
        name.gif = setInterval(function () {
            //获取当前盒子位置 offset  让盒子在当前位置加移动距离
            // 匀速动画
            // name.style.left = name.offsetLeft + 3 + 'px'

            // 缓动动画:
            //如果需要缓动动画，公式 ： （目标值 - 现在的位置） / 10   意义是先快后慢，到地方后停止
            //顺便为了避免小数的出现 使用向上取整Math.ceil  与向下取整 Math.floor

            //首先确定缓动动画的的变化值
            var bianhuazhi = (zhi - name.offsetLeft) / 10
            //查清是正数还是负数，正数向上取整 负数向下取整
            bianhuazhi = bianhuazhi > 0 ? Math.ceil(bianhuazhi) : Math.floor(bianhuazhi)

            //然后赋值给缓动动画
            name.style.left = name.offsetLeft + bianhuazhi + 'px'



            //添加一个定时器结束条件
            if (name.offsetLeft == zhi) {
                clearInterval(name.gif)
                //回调函数一般写在定时器结束条件内
                if(huidiao) {
                    huidiao()
                }
            }
        }, 50)
    }


    // 动画函数调用
    yidong(div, 300)

    d500.addEventListener('click', function () {
        yidong(span, 500)
    })

    d800.addEventListener('click', function () {
        yidong(span, 800)
    })

    //封装的动画函数添加 回调函数  可以看做是第三个参数内直接添加了一个匿名函数
    yidong(span, 800,function() {
        span.style.backgroundColor = 'blue'
    })
    //匀速动画:盒子当前位置 + 固定的值
    //缓动动画:盒子当前位置 + 变化的值   (目标值 - 当前位置) / 10
</script>


window.scroll(x,y)  用于返回顶部使用 添加点击事件,返回x,y坐标 不带单位
```


## 移动端特效 ##
### classList的使用 ###
`classList`可以为元素 追加类名 删除类型 以及切换类名
```
    var div =  document.querySelector('div')
    //追加类名
    div.classList.add('one')
    //删除类名
    div.classList.remove('one')
    //切换类名 如果元素没有这个类名 则为其添加 如果有，则删除
    div.classList.toggle('one')
```

### 移动端触摸事件 ###
1.点击事件 `touchstart`
只要手指点击了屏幕,动作就会被触发

```
    div.addEventListener('touchstart', function () {
        console.log('点击事件触发')
    })
```
![](https://image.dcaoao.com/image/202212022004185.gif)
2.移动事件 `touchmove`

手指点击了屏幕不放,并且在移动,就会被触发

```
    div.addEventListener('touchmove', function (e) {
       console.log('移动事件触发')
    })
```
![](https://image.dcaoao.com/image/202212022004284.gif)


3.离开事件 `touchend`
手指离开屏幕即可被触发
```
    div.addEventListener('touchend', function (e) {
        console.log('离开事件触发')
    })
```
![](https://image.dcaoao.com/image/202212022006691.gif)


### 获取移动端元素事件 ###

```
    div.addEventListener('touchstart', function (e) {
        console.log(e)  //获取元素事件
    })
```
其拥有以下属性
![](https://image.dcaoao.com/image/202212022008866.png)
`touches` 获取正在触摸屏幕的手指列表的相关信息
![](https://image.dcaoao.com/image/202212022010573.png)
`targetTouches` 正在触摸DOM元素的手指列表的相关信息
![](https://image.dcaoao.com/image/202212022011214.png)
`changedTouches` 手指状态发生了改变的列表 从点击到离开 或者点击后移动的信息
![](https://image.dcaoao.com/image/202212022012701.png)
一般都是触摸元素 使用的最多的是`targetTouches`

### 案例 拖动盒子 ###
拖动元素三部曲 
1.触摸元素:获取手指初始坐标 获取盒子当前位置
2.移动手指:获取手指移动的距离 用当前坐标减去初始坐标 并且将值赋给盒子进行移动   盒子初始坐标 + 手指移动距离
3.离开手指

第一步,在点击事件中,获取点击的初始值以及盒子的初始位置
```
    //点击事件 touchstart
    div.addEventListener('touchstart', function (e) {
        //获取正在触摸dom元素的第一个点击坐标的相关信息
        x = e.targetTouches[0].pageX
        y = e.targetTouches[0].pageY
        //获取初始盒子位置
        boxX = div.offsetLeft
        boxY = div.offsetTop
    })
```
第二步,在移动事件中,获取移动中的坐标,减去点击事件中的初始坐标,就是移动的距离

```
//移动事件 touchmove
    div.addEventListener('touchmove', function (e) {
//获取手指移动的距离 使用移动坐标减去初始坐标,求出移动距离
        x1 = e.targetTouches[0].pageX - x
        y2 = e.targetTouches[0].pageY - y


//更改盒子位置   盒子原来的位置 + 手指移动的距离 = 盒子移动至当前距离
        div.style.left = boxX + x1 + 'px'
        div.style.top = boxY +  y2  + 'px'
//最后阻止屏幕滚动的默认行为
    e.preventDefault()
    })
```

效果图:
![](https://image.dcaoao.com/image/202212022019953.gif)

### css3的图片过渡效果 ###
```
  document.style.transition = 'all 0.3s'
```

### 解决移动端click的300毫秒延迟 ###
第一个解决办法
禁止缩放
第二个解决办法 使用fastclick插件
插件地址 https://github.com/ftlabs/fastclick
直接引入该js，然后正常写即可

禁止缩放:
```
<meta name="viewport" content="width=device-width, initial-scale=1">
```


### 轮播图的神 Swipe插件使用 ###
Swipe插件可以快速创建轮播图,并且有许多样式可选
下载地址 https://www.swiper.com.cn/download/index.html

第一步 ，引入相关样式:
```
<link rel="stylesheet" href="css/swiper-bundle.min.css">
<script src="js/swiper-bundle.min.js"></script>
```

第二步,去demo文件夹里的案例 中,挑选轮播图 并复制其HTML结构 也就是 Swiper  其下面的
![](https://image.dcaoao.com/image/202212032213995.png)

![](https://image.dcaoao.com/image/202212032213701.png)

```
    <!-- Swiper -->
    <div class="swiper mySwiper">
        <div class="swiper-wrapper">
          <div class="swiper-slide">Slide 1</div>
          <div class="swiper-slide">Slide 2</div>
          <div class="swiper-slide">Slide 3</div>
          <div class="swiper-slide">Slide 4</div>
          <div class="swiper-slide">Slide 5</div>
          <div class="swiper-slide">Slide 6</div>
          <div class="swiper-slide">Slide 7</div>
          <div class="swiper-slide">Slide 8</div>
          <div class="swiper-slide">Slide 9</div>
        </div>
        <div class="swiper-button-next"></div>
        <div class="swiper-button-prev"></div>
        <div class="swiper-pagination"></div>
      </div>
  
</body>
```

第三步.拷贝 `swiper` 类名的CSS样式至页面CSS样式表

![](https://image.dcaoao.com/image/202212032214828.png)

```
      .swiper {
        width: 100%;
        height: 100%;
      }

      .swiper-slide {
        overflow: hidden;
      }
```


第四步,拷贝其`JS`代码,可以写进js文件内

![](https://image.dcaoao.com/image/202212032215603.png)
```
      var swiper = new Swiper(".mySwiper", {
        zoom: true,
        navigation: {
          nextEl: ".swiper-button-next",
          prevEl: ".swiper-button-prev",
        },
        pagination: {
          el: ".swiper-pagination",
          clickable: true,
        },
      });
```

效果图:
![](https://image.dcaoao.com/image/202212032224994.gif)



### bootstrap轮播图 ###
bootstrap是一个JS框架,其拥有很多功能
轮播图功能是其其中一个
地址:https://v3.bootcss.com/javascript/#carousel

引入相关文件
```
//引入jquery js  因为bootstrap依赖它
<script src="https://code.jquery.com/jquery-3.6.1.min.js"></script>
//引入 bootstrap js
<script src="https://image.dcaoao.com/image/202212032156066.js"></script>
//引入 bootstrap css
<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/3.4.1/css/bootstrap.min.css"
    integrity="sha384-HSMxcRTRxnN+Bdg0JdbxYKrThecOKuH5zCYotlSAcp1+c8xmyTe9GYg1l9a69psu" crossorigin="anonymous">
```

然后直接复制其HTML结构,到轮播图内
![](https://image.dcaoao.com/image/202212032221073.png)
![](https://image.dcaoao.com/image/202212032222388.png)

```
<style>
    .lunbo {
        width: 800px;
        height: 300px;
        background-color: skyblue;
        margin: 100px auto;

    }
</style>

<body>
    <div class="lunbo">
        <div id="carousel-example-generic" class="carousel slide" data-ride="carousel">
            <!-- Indicators -->
            <ol class="carousel-indicators">
                <li data-target="#carousel-example-generic" data-slide-to="0" class="active"></li>
                <li data-target="#carousel-example-generic" data-slide-to="1"></li>
                <li data-target="#carousel-example-generic" data-slide-to="2"></li>
            </ol>

            <!-- Wrapper for slides -->
            <div class="carousel-inner" role="listbox">
                <div class="item active">
                    <img src="https://image.dcaoao.com/image/202212032145174.png" alt="...">
                    <div class="carousel-caption">
                        ...
                    </div>
                </div>
                <div class="item">
                    <img src="https://image.dcaoao.com/image/202212032145207.png" alt="...">
                    <div class="carousel-caption">
                        ...
                    </div>
                </div>

                <div class="item">
                    <img src="https://image.dcaoao.com/image/202212032146306.png" alt="...">
                    <div class="carousel-caption">
                        ...
                    </div>
                </div>
                ...
            </div>

            <!-- Controls -->
            <a class="left carousel-control" href="#carousel-example-generic" role="button" data-slide="prev">
                <span class="glyphicon glyphicon-chevron-left" aria-hidden="true"></span>
                <span class="sr-only">Previous</span>
            </a>
            <a class="right carousel-control" href="#carousel-example-generic" role="button" data-slide="next">
                <span class="glyphicon glyphicon-chevron-right" aria-hidden="true"></span>
                <span class="sr-only">Next</span>
            </a>
        </div>
    </div>
</body>
```


效果图:
![](https://image.dcaoao.com/image/202212032226920.gif)


## 本地存储 ##
### 本地存储   `sessionStorage` ###

生命周期为关闭浏览器窗口
在同一个页面下 数据可以共享
使用键值对的形式存储

前提数据
```
<body>
    <input type="text" class="ipt1">
    <input type="text" class="ipt2">
    <button class="set">存储数据</button>
    <button class="get">获取数据</button>
    <button class="remove">删除数据</button>
    <button class="del">清空数据</button>
</body>

<script>
    //获取元素
    var ipt1 = document.querySelector('.ipt1')
    var ipt2 = document.querySelector('.ipt2')
    var set = document.querySelector('.set')
    var get = document.querySelector('.get')
    var remove = document.querySelector('.remove')
    var del = document.querySelector('.del')
</script>
```

`sessionStorage.setItem('数据名',数据值)`存储数据
```
    set.addEventListener('click',function(){
        var va1 = ipt1.value
        var va2 = ipt2.value
        // sessionStorage.setItem('数据名',数据值)
        sessionStorage.setItem('value1',va1)
        sessionStorage.setItem('value2',va2)
    })
```
![](https://image.dcaoao.com/image/202212052002455.gif)

`sessionStorage.setItem('数据名')`读取数据
```
    get.addEventListener('click',function(){
        // sessionStorage.setItem('数据名')
        console.log(sessionStorage.getItem('value1'))
        console.log(sessionStorage.getItem('value2'))
    })
```
![](https://image.dcaoao.com/image/202212052003414.gif)
`sessionStorage.setItem('数据名')`清除数据
```
    remove.addEventListener('click',function(){
        // sessionStorage.removeItem('数据名')
        sessionStorage.removeItem('value1')
        sessionStorage.removeItem('value2')
    })
    
```

![](https://image.dcaoao.com/image/202212052004272.gif)

`sessionStorage.clear()`清除全部数据
```
    del.addEventListener('click',function(){
        // sessionStorage.clear()
        sessionStorage.clear()
    })
```
![](https://image.dcaoao.com/image/202212052004906.gif)


### 本地存储   `localStorage` ###
生命周期永久生效 除非手动删除 否则关闭页面也会存在
可以多窗口共享 同一浏览器
使用键值对的形式存储


前提数据:
```
<body>
    <input type="text" class="ipt1">
    <input type="text" class="ipt2">
    <button class="set">存储数据</button>
    <button class="get">获取数据</button>
    <button class="remove">删除数据</button>
    <button class="del">清空数据</button>
</body>
<script>

    //生命周期永久生效 除非手动删除 否则关闭页面也会存在
    //可以多窗口共享 同一浏览器
    //使用键值对的形式存储

    //获取元素
    var ipt1 = document.querySelector('.ipt1')
    var ipt2 = document.querySelector('.ipt2')
    var set = document.querySelector('.set')
    var get = document.querySelector('.get')
    var remove = document.querySelector('.remove')
    var del = document.querySelector('.del')
</script>
```

`localStorage..setItem('数据名',数据值)`存储数据
```
    set.addEventListener('click',function(){
        var va1 = ipt1.value
        var va2 = ipt2.value
        // localStorage..setItem('数据名',数据值)
        localStorage.setItem('value1',va1)
        localStorage.setItem('value2',va2)
    })
```
![](https://image.dcaoao.com/image/202212052010421.gif)
`localStorage..setItem('数据名')`读取数据
```
    get.addEventListener('click',function(){
        // localStorage..setItem('数据名')
        console.log(localStorage.getItem('value1'))
        console.log(localStorage.getItem('value2'))
    })
```
![](https://image.dcaoao.com/image/202212052011764.gif)
`localStorage.removeItem('数据名')`清除数据
```
    remove.addEventListener('click',function(){
        // localStorage.removeItem('数据名')
        localStorage.removeItem('value1')
        localStorage.removeItem('value2')
    })
```
![](https://image.dcaoao.com/image/202212052011430.gif)
`localStorage.clear()`清除全部数据
```
    del.addEventListener('click',function(){
        // localStorage.clear()
        localStorage.clear()
    })
```
![](https://image.dcaoao.com/image/202212052012152.gif)

### 本地存储案例 记住用户名 ###
如果本地存储内有数据,则直接取出给输入框
如果记住密码变为了勾选状态,则写入本地存储并且将值赋值输入框
如果未被选中,则清除本地数据

![](https://image.dcaoao.com/image/202212052015499.gif)
```
<body>
    用户名:<input type="text" class="uname">
    <input type="checkbox" class="remember"> 记住用户名
</body>

<script>
    //获取元素 
    var uname = document.querySelector('.uname')
    var remember = document.querySelector('.remember')

    //如果本地存储内有数据，则直接取出来赋值给输入框
    if(localStorage.getItem('uname')) {
        uname.value = localStorage.getItem('uname')
        //同时将复选框改为选中状态
        remember.checked = true
    }
    remember.addEventListener('change',function(){  //change 为状态发生改变就会被触发
        //如果复选框为选中 则将本地存储的值赋值给复选框
        if(remember.checked) {
            localStorage.setItem('uname',uname.value)
        } else {
            //如果未被选中，则删除本地数据
            localStorage.removeItem('uname')
        }
    })
</script>
```

需要注意的是: `change`为状态发生改变时就会被触发,这里用作于复选框被勾选触发事件


## 数据可视化 ##
常见的数据可视化库
`D3.js`   目前Web端评价最高的Javascript可视化工具 上手难
`ECharts.js`  百度出品的一个Javascript数据化可视库
`Highcharts.js`  国外的前端数据可视化库 商用免费
`AntV` 蚂蚁金服新一代数据可视化解决方案


数据可视化的目的:借助于图形化手段 清洗有效的传达与沟通信息
在互联网公司中经常用于通用数据报表 移动端图标 大屏可视化 图编辑等

### 数据可视化 ECharts 插件 ###
ECharts插件可以快速生成各种数据可视化表单

官网链接: https://echarts.apache.org/zh/index.html

使用分五步:

1.下载并引入echarts.js
2.准备一个具备大小的Dom容器
3.初始化echart示例对象
4.指定配置项和数据
5.将配置项设置给echarts实例对象 


```

<!-- 1.下载并引入echarts.js -->
<script src="js/echarts.js"></script>
<style>
    /* 2.准备一个具备大小的Dom容器 */
    .box {
        width: 1000px;
        height: 400px;
        background-color: #fff;
    }
</style>

<body>
    <div class="box">

    </div>
</body>
<script>
    // 3.初始化echart示例对象
    var mychart = echarts.init(document.querySelector('.box'))
    //   4. 指定配置项和数据
    var option = {
  title: {
    text: '哇去，牛逼'
  },
  tooltip: {
    trigger: 'axis'
  },
  legend: {
    data: ['Email', 'Union Ads', 'Video Ads', 'Direct', 'Search Engine']
  },
  grid: {
    left: '3%',
    right: '4%',
    bottom: '3%',
    containLabel: true
  },
  toolbox: {
    feature: {
      saveAsImage: {}
    }
  },
  xAxis: {
    type: 'category',
    boundaryGap: false,
    data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
  },
  yAxis: {
    type: 'value'
  },
  series: [
    {
      name: 'Email',
      type: 'line',
      stack: 'Total',
      data: [120, 132, 101, 134, 90, 230, 210]
    },
    {
      name: 'Union Ads',
      type: 'line',
      stack: 'Total',
      data: [220, 182, 191, 234, 290, 330, 310]
    },
    {
      name: 'Video Ads',
      type: 'line',
      stack: 'Total',
      data: [150, 232, 201, 154, 190, 330, 410]
    },
    {
      name: 'Direct',
      type: 'line',
      stack: 'Total',
      data: [320, 332, 301, 334, 390, 330, 320]
    },
    {
      name: 'Search Engine',
      type: 'line',
      stack: 'Total',
      data: [820, 932, 901, 934, 1290, 1330, 1320]
    }
  ]
};
    //5.将配置项设置给echarts
    mychart.setOption(option)
</script>
```


效果图:
![](https://image.dcaoao.com/image/202212052020561.png)


其中,指定配置项和数据可以从 https://echarts.apache.org/examples/zh/index.html 处获取
ECharts官网提供了非常多的案例,可以直接获取使用

其中的配置和数据也不相同,可以查阅文档获知其作用
https://echarts.apache.org/zh/option.html
```
title  标题组件
tooltip 提示框组件
legend 图例组件
toolbox 工具栏
grid 直角坐标系内绘图网格
xAxis grid中的x轴
yAxis grid中的y轴
series 系列列表 通过type决定使用什么图标 
color 数组形式 控制颜色  color:[red,blue,ye]
```
![](https://image.dcaoao.com/image/202212052024703.png)