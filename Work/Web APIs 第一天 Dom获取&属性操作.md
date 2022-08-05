# Web APIs 第一天 Dom获取&属性操作

## 1. Web API 基本认知

### 变量声明

![image-20220721212649858](Web%20APIs%20%E7%AC%AC%E4%B8%80%E5%A4%A9%20Dom%E8%8E%B7%E5%8F%96&%E5%B1%9E%E6%80%A7%E6%93%8D%E4%BD%9C.assets/image-20220721212649858.png)

![image-20220721212815044](Web%20APIs%20%E7%AC%AC%E4%B8%80%E5%A4%A9%20Dom%E8%8E%B7%E5%8F%96&%E5%B1%9E%E6%80%A7%E6%93%8D%E4%BD%9C.assets/image-20220721212815044.png)

![image-20220721212837172](Web%20APIs%20%E7%AC%AC%E4%B8%80%E5%A4%A9%20Dom%E8%8E%B7%E5%8F%96&%E5%B1%9E%E6%80%A7%E6%93%8D%E4%BD%9C.assets/image-20220721212837172.png)

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>

<body>
  <script>
    // const声明变量的时候，不能再重新赋值
    // const=constant
    // 基本数据类型：Number String Boolean undefind null Symbol BigInt
    // 引用数据类型（复杂类型）只有对象
    // Object对象
    // -Array
    // -Function
    // -Math
    // -RegExp
    // -Date

    // 符号类型
    const num = 1
    num = 2
    console.log(num)

    for (const i = 0; i < 8; i++) {
      console.log('棒')
    }

    const arr = ['pink', 'red']
    arr.push('skyblue')
    console.log(arr)

    const person = {
      name: 'pink',
      age: 18
    }
    person.male = 'female'
    console.log(person)
    // 建议声明数组或者对象的时候优先使用const

    /*

      总结:
      1.以后声明变量,优先使用const
      2.建议数组和对象用const来声明 (修改对象的属性,不会报错)
      3.当声明的值,会发生改变的时候,用let 比如,for循环
      里面的;et i= 0;
    
      */

    // 对于引用类型来说:
    const obj = { name: 'pink', age: 18 }

  </script>
</body>

</html>
```



### 1.1 作用和分类

* 作用: 就是使用 JS 去操作 html 和浏览器

* 分类：DOM (文档对象模型)、BOM（浏览器对象模型）

  

  ![image-20220721213327671](Web%20APIs%20%E7%AC%AC%E4%B8%80%E5%A4%A9%20Dom%E8%8E%B7%E5%8F%96&%E5%B1%9E%E6%80%A7%E6%93%8D%E4%BD%9C.assets/image-20220721213327671.png)

### 1.2 什么是DOM

* DOM（Document Object Model——文档对象模型）是用来呈现以及与任意 HTML 或 XML文档交互的API
*  白话文：DOM是浏览器提供的一套专门用来 操作网页内容 的功能
* DOM作用 : 开发网页内容特效和实现用户交互

#### 1.2.1 总结

![image-20220721213552302](Web%20APIs%20%E7%AC%AC%E4%B8%80%E5%A4%A9%20Dom%E8%8E%B7%E5%8F%96&%E5%B1%9E%E6%80%A7%E6%93%8D%E4%BD%9C.assets/image-20220721213552302.png)

### 1.3 DOM树

DOM树是什么 

* 将 HTML 文档以树状结构直观的表现出来，我们称之为文档树或 DOM 树
*  描述网页内容关系的名词
* 作用：文档树直观的体现了标签与标签之间的关系

![image-20220721213716338](Web%20APIs%20%E7%AC%AC%E4%B8%80%E5%A4%A9%20Dom%E8%8E%B7%E5%8F%96&%E5%B1%9E%E6%80%A7%E6%93%8D%E4%BD%9C.assets/image-20220721213716338.png)

![image-20220721213727385](Web%20APIs%20%E7%AC%AC%E4%B8%80%E5%A4%A9%20Dom%E8%8E%B7%E5%8F%96&%E5%B1%9E%E6%80%A7%E6%93%8D%E4%BD%9C.assets/image-20220721213727385.png)

### 1.4 DOM对象

* DOM对象：浏览器根据html标签生成的 JS对象 
  * 所有的标签属性都可以在这个对象上面找到
  * 修改这个对象的属性会自动映射到标签身上
* DOM的核心思想 
  * 把网页内容当做对象来处理
* document 对象 
  * 是 DOM 里提供的一个对象 
  * 所以它提供的属性和方法都是用来访问和操作网页内容的
    * 例：document.write() 
  *  网页所有内容都在document里面

![image-20220721213902096](Web%20APIs%20%E7%AC%AC%E4%B8%80%E5%A4%A9%20Dom%E8%8E%B7%E5%8F%96&%E5%B1%9E%E6%80%A7%E6%93%8D%E4%BD%9C.assets/image-20220721213902096.png)

#### 1.4.1 总结

1.DOM 树是什么？ 

* 将 HTML 文档以树状结构直观的表现出来，我们称之为文档树或 DOM 树 
* 作用：文档树直观的体现了标签与标签之间的关系 

2.DOM对象怎么创建的？

* 浏览器根据html标签生成的 JS对象（DOM对象）
* DOM的核心就是把内容当对象来处理

 3. document 是什么？

* 是 DOM 里提供的一个对象
*  网页所有内容都在document里面

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>

<body>
  <div class="demo">123</div>
  <script>
    /* 
    
      API接口:    方法,函数
      
      文档:   一个页面就是文档 document
      元素:   页面上所i有的标签都叫元素 element
      节点:   页面上所有的内容都叫节点 node

      DOM对象:页面上的标签元素,都是一个对象
      */

    // 1.获取匹配的第一个元素    querySelector
    // document.querySelector('css选择器')
    // 获取DOM元素    /   DOM对象(
    const div = document.querySelector('div')
    // 获取的是第一个对象
    console.log(div)
    // 获取的标签,其实是一个对象   DOM对象
    console.log(typeof div)
    // 打印一个对象的所有属性和方法
    // console.log(div)
    // document也是对象

    // 伪数组
    const div2 = document.querySelectorAll('.demo')
    console.log(div2)
    console.log(typeof div2)
    // Object   array也是属于object类型的
    console.log('-----------------------');
    const obj = { name: 'zzz', age: 19 }
    console.log(typeof obj)   //Object
    console.log('-----------------------');
    const fn = function () {
      console.log(123)
    }
    console.log(typeof fn)   //function
    console.log('-----------------------');


    // 基本数据类型: Number String Boolean undefined null  Symbol BigInt
    // 引用类型(复杂类型) 只有对象

    // 1.检测基本数据类型 typeof ,但不能知道是array 有些缺陷
    //typeof null
    console.log(typeof null) //Object 这是一个Bug,特殊
    console.log(typeof 1)   //Number
    console.log(typeof undefined)    //undefined
    console.log(typeof true)     //Boolean
    console.log(typeof '123')     //String

    // 2.检测引用类型A instanceof B ,他不能检测基本数据类型

    // 3.既可以检测基本数据类型,又可以检测引用类型
    Object.prototype.toString.call()
  </script>
</body>

</html>
```



## 2. 获取DOM对象

![image-20220721214441912](Web%20APIs%20%E7%AC%AC%E4%B8%80%E5%A4%A9%20Dom%E8%8E%B7%E5%8F%96&%E5%B1%9E%E6%80%A7%E6%93%8D%E4%BD%9C.assets/image-20220721214441912.png)

### 2.1 根据CSS选择器来获取DOM元素

![image-20220721214507332](Web%20APIs%20%E7%AC%AC%E4%B8%80%E5%A4%A9%20Dom%E8%8E%B7%E5%8F%96&%E5%B1%9E%E6%80%A7%E6%93%8D%E4%BD%9C.assets/image-20220721214507332.png)

![image-20220721214552488](Web%20APIs%20%E7%AC%AC%E4%B8%80%E5%A4%A9%20Dom%E8%8E%B7%E5%8F%96&%E5%B1%9E%E6%80%A7%E6%93%8D%E4%BD%9C.assets/image-20220721214552488.png)

多参看文档：https://developer.mozilla.org/zh-CN/docs/Web/API/Document/querySelector

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <style>
    .box {
      width: 200px;
      height: 200px;
    }
  </style>
</head>

<body>
  <div class="box">123</div>
  <div class="box">abc</div>
  <p id="nav">导航栏</p>
  <ul class="nav">
    <li>测试1</li>
    <li>测试2</li>
    <li>测试3</li>
  </ul>
  <script>
    //1.获取匹配的第一个元素 document.querySelector('CSS选择器')\
    const box = document.querySelector('.box')
    console.log(box)

    const nav = document.querySelector('#nav')
    console.log(nav)

    // 1.2获取ul 下带一个li标签
    const li = document.querySelector('ul li:first:child')
    console.log(li)

    // 获取ul下的所有li标签
    // 获取匹配的所有元素   document.querySelectorAll('选择器')
    // 返回的是一个伪数组
    const lis = document.querySelectorAll('ul li')
    console.log(lis)

    // 伪数组: 有索引,有length,但是没有数组的方法,pop,push
    //哪怕只有一个元素，通过querySelectAll() 获取过来的也是一个伪数组，里面只有一个元素而已
    console.log(lis[0])
    console.log(lis[1])
    console.log(lis[2])

    /*
     
    通过querySelectorAll 获取的是一个伪数组,
    如果要获取里面的元素对象(DOM对象),可以使用下标
    
    */
    //获取每一个,遍历
    for (let i = 0; i < lis.length; i++) {
      console.log(lis)
    }

    // p是什么 伪数组
    const p = document.querySelectorAll('#nav')
    console.log(p)

    // 特殊的两个元素
    // 1.body标签/元素 document.body
    const body = document.querySelector('body')
    console.log(body)
    console.log(document.body)

    // 2.HTML document.documentElement
    console.log(document.documentElement)
  </script>
</body>

</html>
```

### 2.2 总结

1.获取一个DOM元素我们使用谁？能直接操作修改吗?

* querySelector()
* 可以 

2.获取多个DOM元素我们使用谁？能直接修改吗？ 如果不能可以怎么做到修改 ？

* querySelectorAll()
* 不可以， 只能通过遍历的方式一次给里面的元素做修改

3.获取页面中的标签我们最终常用那两种方式？

* querySelectorAll() 
*  querySelector() 

4.他们两者的区别是什么？ 

* querySelector() 只能选择一个元素， 可以直接操作 
*  querySelectorAll() 可以选择多个元素，得到的是伪数组，需要遍历得到 每一个元素 

5.他们两者小括号里面的参数有神马注意事项？

* 里面写css选择器 
* 必须是字符串，也就是必须加引

### 2.3 练习

![image-20220721215012315](Web%20APIs%20%E7%AC%AC%E4%B8%80%E5%A4%A9%20Dom%E8%8E%B7%E5%8F%96&%E5%B1%9E%E6%80%A7%E6%93%8D%E4%BD%9C.assets/image-20220721215012315.png)

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <style>
    .box {
      width: 200px;
      height: 200px;
    }
  </style>
</head>

<body>
  <div class="box">123</div>
  <div class="box">abc</div>
  <p id="nav">导航栏</p>
  <ul class="nav">
    <li>测试1</li>
    <li>测试2</li>
    <li>测试3</li>
  </ul>
  <script>
    //1.获取匹配的第一个元素 document.querySelector('CSS选择器')\
    const box = document.querySelector('.box')
    console.log(box)

    const nav = document.querySelector('#nav')
    console.log(nav)

    // 1.2获取ul 下带一个li标签
    const li = document.querySelector('ul li:first:child')
    console.log(li)

    // 获取ul下的所有li标签
    // 获取匹配的所有元素   document.querySelectorAll('选择器')
    // 返回的是一个伪数组
    const lis = document.querySelectorAll('ul li')
    console.log(lis)

    // 伪数组: 有索引,有length,但是没有数组的方法,pop,push
    console.log(lis[0])
    console.log(lis[1])
    console.log(lis[2])

    /*
     
    通过querySelectorAll 获取的是一个伪数组,
    如果要获取里面的元素对象(DOM对象),可以使用下标
    
    */
    //获取每一个,遍历
    for (let i = 0; i < lis.length; i++) {
      console.log(lis)
    }

    // p是什么 伪数组
    const p = document.querySelectorAll('#nav')
    console.log(p)

    // 特殊的两个元素
    // 1.body标签/元素 document.body
    const body = document.querySelector('body')
    console.log(body)
    console.log(document.body)

    // 2.HTML document.documentElement
    console.log(document.documentElement)
  </script>
</body>

</html>
```

### 2.3 其他获取DOM元素方法

![image-20220721215220271](Web%20APIs%20%E7%AC%AC%E4%B8%80%E5%A4%A9%20Dom%E8%8E%B7%E5%8F%96&%E5%B1%9E%E6%80%A7%E6%93%8D%E4%BD%9C.assets/image-20220721215220271.png)

## 3. 操作元素内容

1.目标：能够修改元素的文本更换内容

* DOM对象都是根据标签生成的,所以操作标签,本质上就是操作DOM对象。

* 就是操作对象使用的点语法。

* 如果想要修改标签元素的里面的内容，则可以使用如下几种方式：

* 2.学习路径：

  1.对象.innerText 属性

  2.对象.innerHTML 属性

### 3.1 元素innerText 属性

* 将文本内容添加/更新到任意标签位置 

* 显示纯文本，不解析标签

![image-20220721215926357](Web%20APIs%20%E7%AC%AC%E4%B8%80%E5%A4%A9%20Dom%E8%8E%B7%E5%8F%96&%E5%B1%9E%E6%80%A7%E6%93%8D%E4%BD%9C.assets/image-20220721215926357.png)

### 3.2 元素.innerHTML 属性

* 将文本内容添加/更新到任意标签位置
* 会解析标签，多标签建议使用模板字符

![image-20220721220000410](Web%20APIs%20%E7%AC%AC%E4%B8%80%E5%A4%A9%20Dom%E8%8E%B7%E5%8F%96&%E5%B1%9E%E6%80%A7%E6%93%8D%E4%BD%9C.assets/image-20220721220000410.png)

### 3.3 总结

1. 设置/修改DOM元素内容有哪2钟方式？
   * 元素.innerText 属性
   * 元素.innerHTML 属性 
2. 三者的区别是什么？ 
   * 元素.innerText 属性 只识别文本，不能解析标签 
   * 元素.innerHTML 属性 能识别文本，能够解析标签 
   * 如果还在纠结到底用谁，你可以选择innerHTML

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>

<body>
  <div class="box">我是文字的内容</div>
  <script>
    // 1.获取元素
    const box = document.querySelector('.box')
    console.log(box)

    /*
      2.1修改文字内容
      设置:对象.innerText = '值'
    */
    box.innerText = '大家还好吗?'

    // 获取:对象.innerText
    console.log(box.innerText)

    /*
        3.修改元素的内容,方式二
        设置元素内容 对象.innerHTML = '值'
    */
    box.innerHTML = '修改内容'
    box.innerHTML = '中午吃什么'

    //  获取元素的内容 : 对象.innerHTML
    console.log(box.innerHTML)

    /*
      区别:
      innerHTML 识别Html标签(可以解析)
      innerText 不识别html标签
    */

    box.innerHTML = '<strong>修改内容</strong>'
    box.innerText = '<strong>修改内容</strong>'
    console.log(box)
  </script>
</body>

</html>
```



### 3.4 练习

![image-20220721220331518](Web%20APIs%20%E7%AC%AC%E4%B8%80%E5%A4%A9%20Dom%E8%8E%B7%E5%8F%96&%E5%B1%9E%E6%80%A7%E6%93%8D%E4%BD%9C.assets/image-20220721220331518.png)

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8" />
  <meta http-equiv="X-UA-Compatible" content="IE=edge" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>年会抽奖</title>
  <style>
    .wrapper {
      width: 840px;
      height: 420px;
      background: url(./images/bg01.jpg) no-repeat center / cover;
      padding: 100px 250px;
      box-sizing: border-box;
    }
  </style>
</head>

<body>
  <div class="wrapper">
    <strong>传智教育年会抽奖</strong>
    <h1>一等奖：<span id="one">???</span></h1>
    <h3>二等奖：<span id="two">???</span></h3>
    <h5>三等奖：<span id="three">???</span></h5>
  </div>
  <script>
    // span 推荐使用innerHTML
    // 1.声明数组
    const personArr = ['周杰伦', '刘德华', '周星驰', 'Pink老师', '张学友']

    // 2.一等奖
    // 2.1随机数 数组的随机的一个下标
    const random = Math.floor(Math.random() * personArr.length)
    // [0, 1) * 5  ==> [0, 5)  ==> [0, 4.99999)  ==> [0, 4]
    // console.log(personArr[random])

    // 2.2. 获取one这个标签
    const one = document.querySelector('#one')
    // 2.3 把随机获得的名字给one
    one.innerHTML = personArr[random]
    // 2.4 删除数组中抽到过的元素
    personArr.splice(random, 1)



    // 二等奖
    // 2.1 随机数 数组的随机一个下标
    const random2 = Math.floor(Math.random() * personArr.length)
    // 2.2. 获取two这个标签
    const two = document.querySelector('#two')
    // 2.3把随机获得的名字给two
    two.innerHTML = personArr[random2]
    // 2.4删除数组中抽到的元素
    personArr.splice(random2, 1)


    // 三等奖
    // 2.1 随机数 数组的随机一个下标
    const random3 = Math.floor(Math.random() * personArr.length)
    // 2.2. 获取three这个标签
    const three = document.querySelector('#three')
    // 2.3把随机获得的名字给three
    three.innerHTML = personArr[random3]
    // 2.4删除数组中抽到的元素
    personArr.splice(random3, 1)


  </script>
</body>

</html>
```

## 4.操作元素属性

### 4.1 操作元素常用属性

![image-20220721220745188](Web%20APIs%20%E7%AC%AC%E4%B8%80%E5%A4%A9%20Dom%E8%8E%B7%E5%8F%96&%E5%B1%9E%E6%80%A7%E6%93%8D%E4%BD%9C.assets/image-20220721220745188.png)

![image-20220721220754533](Web%20APIs%20%E7%AC%AC%E4%B8%80%E5%A4%A9%20Dom%E8%8E%B7%E5%8F%96&%E5%B1%9E%E6%80%A7%E6%93%8D%E4%BD%9C.assets/image-20220721220754533.png)

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>

<body>
  <img src="./images/1.webp" alt="">
  <script>
    // 操作元素的常用属性
    // 1.获取属性值 element.属性名 = '值'
    // 2.设置属性（修改属性） element.属性名 = '值'

    // 1.获取图片元素

    const img = document.querySelector('img')

    // 修改图片对象的路径 src属性
    img.src = './images/2.webp'
    img.title = 'pink老师的艺术照'

    // 获取属性
    console.log(img.title);
  </script>
</body>

</html>
```

#### 4.1.1 练习

![image-20220721221029953](Web%20APIs%20%E7%AC%AC%E4%B8%80%E5%A4%A9%20Dom%E8%8E%B7%E5%8F%96&%E5%B1%9E%E6%80%A7%E6%93%8D%E4%BD%9C.assets/image-20220721221029953.png)

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>

<body>
  <img src="./images/1.webp" alt="">
  <script>
    // 取 N - M 的随机整数
    function getRandom(N, M) {
      return Math.floor(Math.random() * (M - N + 1)) + N
    }

    // 1.获取图片对象
    const img = document.querySelector('img')

    // 2.随机得到图片的序号
    const random = getRandom(1, 6)

    // 3.修改图片路径 src
    img.src = `./images/${random}.webp`

    // 扩展亿点点
    // 刷新页面   F5  / Ctrl + R (windows) / Cmd + R (Mac)
    // 强制刷新页面, 清空缓存  Ctrl + shift + R   /  CMD + shift + R 
  </script>
</body>

</html>
```

### 4.2 操作元素样式属性

![image-20220721221127217](Web%20APIs%20%E7%AC%AC%E4%B8%80%E5%A4%A9%20Dom%E8%8E%B7%E5%8F%96&%E5%B1%9E%E6%80%A7%E6%93%8D%E4%BD%9C.assets/image-20220721221127217.png)

#### 4.2.1 通过 style 属性操作CSS

![image-20220721221157918](Web%20APIs%20%E7%AC%AC%E4%B8%80%E5%A4%A9%20Dom%E8%8E%B7%E5%8F%96&%E5%B1%9E%E6%80%A7%E6%93%8D%E4%BD%9C.assets/image-20220721221157918.png)

![image-20220721221207537](Web%20APIs%20%E7%AC%AC%E4%B8%80%E5%A4%A9%20Dom%E8%8E%B7%E5%8F%96&%E5%B1%9E%E6%80%A7%E6%93%8D%E4%BD%9C.assets/image-20220721221207537.png)

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <style>
    .box {
      width: 200px;
      height: 200px;
      background-color: pink;
    }
  </style>
</head>

<body>
  <div class="box"></div>
  <script>
    // 修改样式属性(宽高，背景色，圆角，padding，margin,字体颜色)
    // 语法：对象.style.样式属性 = '值'

    // 1.获取元素 匹配获取到的第一个元素
    const box = document.querySelector('.box')
    console.log(box)

    // 2.修改样式属性 
    // 注意：宽高等带单位的属性，不要忘记加单位 px
    // 属性中- ， 复合属性，改驼峰式

    box.style.width = '300px'
    box.style.backgroundColor = 'skyblue'
    box.style.marginTop = '200px'
    box.style.borderRadius = '20px'
  </script>
</body>

</html>
```



##### 4.2.1.1总结

![image-20220721221226035](Web%20APIs%20%E7%AC%AC%E4%B8%80%E5%A4%A9%20Dom%E8%8E%B7%E5%8F%96&%E5%B1%9E%E6%80%A7%E6%93%8D%E4%BD%9C.assets/image-20220721221226035.png)

##### 4.2.1.2 练习

![image-20220721221351014](Web%20APIs%20%E7%AC%AC%E4%B8%80%E5%A4%A9%20Dom%E8%8E%B7%E5%8F%96&%E5%B1%9E%E6%80%A7%E6%93%8D%E4%BD%9C.assets/image-20220721221351014.png)

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <style>
    body {
      background: url(./images/desktop_1.jpg) no-repeat top center/cover;
    }
  </style>
</head>

<body>
  <script>
    // 随机函数
    function getRandom(N, M) {
      return Math.floor(Math.random() * (M - N + 1)) + N
    }

    // 随机数
    const random = getRandom(1, 10)

    // 更换body的背景图片
    const body = document.body
    body.style.backgroundImage = `url(./images/desktop_${random}.jpg)`
  </script>
</body>

</html>
```

#### 4.2.2 操作类名(className) 操作CSS

![image-20220721221603482](Web%20APIs%20%E7%AC%AC%E4%B8%80%E5%A4%A9%20Dom%E8%8E%B7%E5%8F%96&%E5%B1%9E%E6%80%A7%E6%93%8D%E4%BD%9C.assets/image-20220721221603482.png)

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <style>
    div {
      width: 200px;
      height: 200px;
      background-color: pink;
    }

    .nav {
      color: red;
    }

    .box {
      width: 300px;
      height: 300px;
      background-color: skyblue;
      margin: 100px auto;
      padding: 10px;
      border: 1px solid #000;
    }
  </style>
</head>

<body>
  <div class="nav">123</div>
  <script>
    // 1.获取元素
    const div = document.querySelector('div')
    console.log(div)

    // 2.添加类名
    // div.className = 'box'  原来的类名没有了
    div.classList = 'nav box'

    /*
      注意 
      1.class是关键字,元素.className = '类名'
      2.使用className的时候,会覆盖原来的类名
        如果想要多个类名都生效,都写上

      3.实际应用场景 
        3.1 适合,多个样式都要修改的情况
        3.2可以用来清空某个元素的所有类名
        元素.className = ''
        div.className = ''
    */

  </script>
</body>

</html>
```



##### 4.2.2.1 总结

![image-20220721221633568](Web%20APIs%20%E7%AC%AC%E4%B8%80%E5%A4%A9%20Dom%E8%8E%B7%E5%8F%96&%E5%B1%9E%E6%80%A7%E6%93%8D%E4%BD%9C.assets/image-20220721221633568.png)

#### 4.2.3 通过 classList 操作类控制CSS

![image-20220721221826298](Web%20APIs%20%E7%AC%AC%E4%B8%80%E5%A4%A9%20Dom%E8%8E%B7%E5%8F%96&%E5%B1%9E%E6%80%A7%E6%93%8D%E4%BD%9C.assets/image-20220721221826298.png)

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <style>
    .box {
      width: 200px;
      height: 200px;
      color: #333;
    }

    .active {
      color: red;
      background-color: pink;
    }
  </style>
</head>

<body>
  <div class="box active">文字</div>
  <script>
    // 1.获取元素
    const box = document.querySelector('.box')

    // 2.修改样式   style   className

    // 1.追加类名 类名不加点(' . ')
    // element.classList.add('类名')

    // box.classList.add('active')

    // 2.删除类名 
    // element.classList.remove('类名')

    box.classList.remove('active')

    // 3.切换类名 
    // element.classList.toggle('类名')

    box.classList.toggle('active')

    // classList className
    // 1.style 单独修改某个样式
    // 2.当我们需要修改很多样式属性的时候，用className,或者classList
    // 区别：className 有一个缺陷：会覆盖原来的类名
    //      classList不会覆盖，是追加，会保留原来的类名
  </script>
</body>

</html>
```

##### 4.2.3.1总结

![image-20220721222012662](Web%20APIs%20%E7%AC%AC%E4%B8%80%E5%A4%A9%20Dom%E8%8E%B7%E5%8F%96&%E5%B1%9E%E6%80%A7%E6%93%8D%E4%BD%9C.assets/image-20220721222012662.png)

##### 4.3.2.2练习

![image-20220721222039729](Web%20APIs%20%E7%AC%AC%E4%B8%80%E5%A4%A9%20Dom%E8%8E%B7%E5%8F%96&%E5%B1%9E%E6%80%A7%E6%93%8D%E4%BD%9C.assets/image-20220721222039729.png)

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8" />
  <meta http-equiv="X-UA-Compatible" content="IE=edge" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>轮播图点击切换</title>
  <style>
    * {
      box-sizing: border-box;
    }

    .slider {
      width: 560px;
      height: 400px;
      overflow: hidden;
    }

    .slider-wrapper {
      width: 100%;
      height: 320px;
    }

    .slider-wrapper img {
      width: 100%;
      height: 100%;
      display: block;
    }

    .slider-footer {
      height: 80px;
      background-color: rgb(100, 67, 68);
      padding: 12px 12px 0 12px;
      position: relative;
    }

    .slider-footer .toggle {
      position: absolute;
      right: 0;
      top: 12px;
      display: flex;
    }

    .slider-footer .toggle button {
      margin-right: 12px;
      width: 28px;
      height: 28px;
      appearance: none;
      border: none;
      background: rgba(255, 255, 255, 0.1);
      color: #fff;
      border-radius: 4px;
      cursor: pointer;
    }

    .slider-footer .toggle button:hover {
      background: rgba(255, 255, 255, 0.2);
    }

    .slider-footer p {
      margin: 0;
      color: #fff;
      font-size: 18px;
      margin-bottom: 10px;
    }

    .slider-indicator {
      margin: 0;
      padding: 0;
      list-style: none;
      display: flex;
      align-items: center;
    }

    .slider-indicator li {
      width: 8px;
      height: 8px;
      margin: 4px;
      border-radius: 50%;
      background: #fff;
      opacity: 0.4;
      cursor: pointer;
    }

    .slider-indicator li.active {
      width: 12px;
      height: 12px;
      opacity: 1;
    }
  </style>
</head>

<body>
  <div class="slider">
    <div class="slider-wrapper">
      <img src="./images/slider01.jpg" alt="" />
    </div>
    <div class="slider-footer">
      <p>对人类来说会不会太超前了？</p>
      <ul class="slider-indicator">
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
      </ul>
      <div class="toggle">
        <button class="prev">&lt;</button>
        <button class="next">&gt;</button>
      </div>
    </div>
  </div>
  <script>
    // const arr = [1, 3]
    // arr[0]
    // 1. 初始数据
    const sliderData = [
      { url: './images/slider01.jpg', title: '对人类来说会不会太超前了？', color: 'rgb(100, 67, 68)' },
      { url: './images/slider02.jpg', title: '开启剑与雪的黑暗传说！', color: 'rgb(43, 35, 26)' },
      { url: './images/slider03.jpg', title: '真正的jo厨出现了！', color: 'rgb(36, 31, 33)' },
      { url: './images/slider04.jpg', title: '李玉刚：让世界通过B站看到东方大国文化', color: 'rgb(139, 98, 66)' },
      { url: './images/slider05.jpg', title: '快来分享你的寒假日常吧~', color: 'rgb(67, 90, 92)' },
      { url: './images/slider06.jpg', title: '哔哩哔哩小年YEAH', color: 'rgb(166, 131, 143)' },
      { url: './images/slider07.jpg', title: '一站式解决你的电脑配置问题！！！', color: 'rgb(53, 29, 25)' },
      { url: './images/slider08.jpg', title: '谁不想和小猫咪贴贴呢！', color: 'rgb(99, 72, 114)' },
    ]


    // 1.需要一个随机数
    // [0, 1) * 8  ==>  [0, 8)  floor ==>  [0, 7]
    const random = Math.floor(Math.random() * sliderData.length)    // 闭区间[0, 7] 
    // const random = parseInt(Math.random() * sliderData.length)    // [0, 7]
    console.log(sliderData[random])

    //把对应的数据渲染到页面上
    // 2.获取图片
    const img = document.querySelector('.slider-wrapper img')
    console.log(img)

    // 2.2 修改图片的src 对象.src
    // sliderData[6]

    img.src = sliderData[random].url

    // 3.把p标签内容替换
    // 3.1 获取p标签(元素)
    const p = document.querySelector('.slider-footer p')
    // 3.2 修改内容 对象.innerHTML 
    p.innerHTML = sliderData[random].title

    // 4.修改footer颜色
    const footer = document.querySelector('.slider-footer')
    footer.style.backgroundColor = sliderData[random].color

    // 5.添加白色小圆点
    // 给ul下面的第二个li标签 添加小圆点
    // All 获取的是一堆,是伪数组
    // nth-child:   1 - 8
    // random: 0 - 7
    const li = document.querySelector(`.slider-indicator li:nth-child(${random + 1})`)
    console.log(li)
    // 添加active类名, 就是小圆点
    li.classList.add('active')

    // const lis = document.querySelectorAll(`.slider-indicator li:nth-child(${random + 1})`)
    // console.log(lis)
    // // 添加active类名, 就是小圆点
    // lis[0].classList.add('active')


  </script>
</body>

</html>
```

### 4.3 操作表单元素 属性

![image-20220721222450864](Web%20APIs%20%E7%AC%AC%E4%B8%80%E5%A4%A9%20Dom%E8%8E%B7%E5%8F%96&%E5%B1%9E%E6%80%A7%E6%93%8D%E4%BD%9C.assets/image-20220721222450864.png)

![image-20220721222509550](Web%20APIs%20%E7%AC%AC%E4%B8%80%E5%A4%A9%20Dom%E8%8E%B7%E5%8F%96&%E5%B1%9E%E6%80%A7%E6%93%8D%E4%BD%9C.assets/image-20220721222509550.png)

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>

<body>
  <!-- <input type="text" value="电脑"> -->
  <input type="checkbox" name="" id="">
  <button>点击</button>
  <script>
    //表单元素:input  textarea等

    // 1.获取元素
    const input = document.querySelector('input')
    // console.log(input.innerHTML)   不可

    //2.获取表单元素的值    input.value 
    console.log(input.value)

    // 3.设置表单元素的值   input.value = '值'
    input.value = '修改表单元素'

    // 修改Input的type类型
    // input.type = 'password'

    // input  checked
    // button disabled

    // checked disabled 在input button里面
    // 返回的是boolean值

    // 1.获取

    const ipt = document.querySelector('.demo')
    console.log(ipt.checked)
    ipt.checked = false

    // 2.按钮

    const btn = document.querySelector('button')
    // disable 失效
    // btn.disabled = true
    btn.disabled = false

  </script>
</body>

</html>
```

### 4.4自定义属性

![image-20220721222556857](Web%20APIs%20%E7%AC%AC%E4%B8%80%E5%A4%A9%20Dom%E8%8E%B7%E5%8F%96&%E5%B1%9E%E6%80%A7%E6%93%8D%E4%BD%9C.assets/image-20220721222556857.png)

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>

<body>
  <div data-id="1" data-spm="不知道">1</div>
  <div data-id="2" data-test-id="666">2</div>
  <div data-id="3">3</div>
  <div data-id="4">4</div>
  <div data-id="5">5</div>


  <script>
    // 自定义属性， 我们自己定义的一些属性

    const div = document.querySelector('div')
    console.log(div)
    console.log(div.dataset)    //Object
    console.log(typeof div.dataset)

    /*
      对象获取属性
      1.对象.属性名
      2.对象['属性名']
    */

    console.log(div.dataset.id)
    console.log(div.dataset['id'])
    console.log(div.dataset.spm)
    console.log(div.dataset[spm])
    console.log(div.dataset.tetsId)
    console.log(div.dataset['testId'])

    /*
      1.H5新增，  以data-   来定义自定义属性
      2.要获取自定义属性，通过dataset
        它获取的是一个对象，存放了所有的以data 开头的自定义属性
        element.dataset.属性名
        element.dataset['属性名']
      3.dataset内， 属性名从短横线变为了驼峰
    */

  </script>
</body>

</html>
```

## 5.定时器-间歇函数

![image-20220721222701718](Web%20APIs%20%E7%AC%AC%E4%B8%80%E5%A4%A9%20Dom%E8%8E%B7%E5%8F%96&%E5%B1%9E%E6%80%A7%E6%93%8D%E4%BD%9C.assets/image-20220721222701718.png)

### 5.1 开启定时器

![image-20220721222746995](Web%20APIs%20%E7%AC%AC%E4%B8%80%E5%A4%A9%20Dom%E8%8E%B7%E5%8F%96&%E5%B1%9E%E6%80%A7%E6%93%8D%E4%BD%9C.assets/image-20220721222746995.png)

### ![image-20220721222758169](Web%20APIs%20%E7%AC%AC%E4%B8%80%E5%A4%A9%20Dom%E8%8E%B7%E5%8F%96&%E5%B1%9E%E6%80%A7%E6%93%8D%E4%BD%9C.assets/image-20220721222758169.png)5.2关闭定时器

![image-20220721223124920](Web%20APIs%20%E7%AC%AC%E4%B8%80%E5%A4%A9%20Dom%E8%8E%B7%E5%8F%96&%E5%B1%9E%E6%80%A7%E6%93%8D%E4%BD%9C.assets/image-20220721223124920.png)

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>

<body>
  <script>
    // /*
    //   语法 ：setInterval(fn,wait)
    //   每隔一段时间，就会调用执行fn ,并且会重复执行，一直执行
    //   windows.setInterval()   它是windows对象给我们提供的方法
    //   windows可以省略
    //   ms 一秒等于1000ms
    // */

    // // 1.直接把函数写在setInterval()内部
    // setInterval(function fn() {
    //   console.log('你好呀！');
    // }, 1000)

    // // 2.声明或者表达式   先初始化一个函数，再传入
    // // 定义函数 有两种方式
    // function fn() {
    //   console.log('吃早饭了嘛？');
    // }
    // const foo = function () {
    //   console.log('喝牛奶嘛？');
    // }
    // setInterval(fn, 1000)
    // setInterval(foo, 2000)

    // // 3.忽略
    // setInterval('fn()', 1000)


    // 如何关闭定时器
    let timer1 = setInterval(function () {
      console.log('你好！')
    }, 1000)
    let timer2 = setInterval(function () {
      console.log('你好，世界！')
    }, 2000)
    console.log(timer1)
    console.log(timer2)           //每个定时器独一无二
    console.log(typeof timer1)    //number
    // 关闭timer1
    clearInterval(timer1)
    clearInterval(timer2)

    /*
      为啥用let 
      const 声明的变量 不能被修改
      const num = 10
      num = 20  Error  
    */

    // 回调函数 ： 回头再次调用的函数
    const fn = function () {
      console.log('这是回调函数')
    }

    // 1.开启定时器
    let n = setInterval(fn, 1000)
    // 2.关闭定时器
    clearInterval(n)
    // 3.重新开启定时器
    n = setInterval(fn, 1000)
    console.log(n)
  </script>
</body>

</html>
```

### 5.3 总结

![image-20220721223202938](Web%20APIs%20%E7%AC%AC%E4%B8%80%E5%A4%A9%20Dom%E8%8E%B7%E5%8F%96&%E5%B1%9E%E6%80%A7%E6%93%8D%E4%BD%9C.assets/image-20220721223202938.png)

### 5.4 练习

![image-20220721223227915](Web%20APIs%20%E7%AC%AC%E4%B8%80%E5%A4%A9%20Dom%E8%8E%B7%E5%8F%96&%E5%B1%9E%E6%80%A7%E6%93%8D%E4%BD%9C.assets/image-20220721223227915.png)

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <textarea name="" id="" cols="30" rows="10">
        用户注册协议
        欢迎注册成为京东用户！在您注册过程中，您需要完成我们的注册流程并通过点击同意的形式在线签署以下协议，请您务必仔细阅读、充分理解协议中的条款内容后再点击同意（尤其是以粗体或下划线标识的条款，因为这些条款可能会明确您应履行的义务或对您的权利有所限制）。
        【请您注意】如果您不同意以下协议全部或任何条款约定，请您停止注册。您停止注册后将仅可以浏览我们的商品信息但无法享受我们的产品或服务。如您按照注册流程提示填写信息，阅读并点击同意上述协议且完成全部注册流程后，即表示您已充分阅读、理解并接受协议的全部内容，并表明您同意我们可以依据协议内容来处理您的个人信息，并同意我们将您的订单信息共享给为完成此订单所必须的第三方合作方（详情查看
    </textarea>
    <br>
    <button class="btn" disabled>我已经阅读用户协议(60)</button>
    <script>
        // 1.获取元素
        const btn = document.querySelector('.btn')

        // 2.开启定时器
        let i = 60
        let timer = setInterval(function () {
            i--
            btn.innerHTML = `我已经阅读用户协议(${i})`
            if (i === 0) {
                // 3.关闭定时器
                clearInterval(timer)
                btn.disabled = false
                btn.innerHTML = '我同意'
            }
        }, 1000)
        console.log()
        
    </script>
</body>

</html>
```

## 6. 综合案例

![image-20220721223315620](Web%20APIs%20%E7%AC%AC%E4%B8%80%E5%A4%A9%20Dom%E8%8E%B7%E5%8F%96&%E5%B1%9E%E6%80%A7%E6%93%8D%E4%BD%9C.assets/image-20220721223315620.png)

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>轮播图点击切换</title>
    <style>
      * {
        box-sizing: border-box;
      }

      .slider {
        width: 560px;
        height: 400px;
        overflow: hidden;
      }

      .slider-wrapper {
        width: 100%;
        height: 320px;
      }

      .slider-wrapper img {
        width: 100%;
        height: 100%;
        display: block;
      }

      .slider-footer {
        height: 80px;
        background-color: rgb(100, 67, 68);
        padding: 12px 12px 0 12px;
        position: relative;
      }

      .slider-footer .toggle {
        position: absolute;
        right: 0;
        top: 12px;
        display: flex;
      }

      .slider-footer .toggle button {
        margin-right: 12px;
        width: 28px;
        height: 28px;
        appearance: none;
        border: none;
        background: rgba(255, 255, 255, 0.1);
        color: #fff;
        border-radius: 4px;
        cursor: pointer;
      }

      .slider-footer .toggle button:hover {
        background: rgba(255, 255, 255, 0.2);
      }

      .slider-footer p {
        margin: 0;
        color: #fff;
        font-size: 18px;
        margin-bottom: 10px;
      }

      .slider-indicator {
        margin: 0;
        padding: 0;
        list-style: none;
        display: flex;
        align-items: center;
      }

      .slider-indicator li {
        width: 8px;
        height: 8px;
        margin: 4px;
        border-radius: 50%;
        background: #fff;
        opacity: 0.4;
        cursor: pointer;
      }

      .slider-indicator li.active {
        width: 12px;
        height: 12px;
        opacity: 1;
      }
    </style>
  </head>

  <body>
    <div class="slider">
      <div class="slider-wrapper">
        <img src="./images/slider01.jpg" alt="" />
      </div>
      <div class="slider-footer">
        <p>对人类来说会不会太超前了？</p>
        <ul class="slider-indicator">
          <li class="active"></li>
          <li></li>
          <li></li>
          <li></li>
          <li></li>
          <li></li>
          <li></li>
          <li></li>
        </ul>
        <div class="toggle">
          <button class="prev">&lt;</button>
          <button class="next">&gt;</button>
        </div>
      </div>
    </div>
    <script>
      // 1. 初始数据
      const arr = [
        {
          url: './images/slider01.jpg',
          title: '对人类来说会不会太超前了？',
          color: 'rgb(100, 67, 68)',
        },
        {
          url: './images/slider02.jpg',
          title: '开启剑与雪的黑暗传说！',
          color: 'rgb(43, 35, 26)',
        },
        {
          url: './images/slider03.jpg',
          title: '真正的jo厨出现了！',
          color: 'rgb(36, 31, 33)',
        },
        {
          url: './images/slider04.jpg',
          title: '李玉刚：让世界通过B站看到东方大国文化',
          color: 'rgb(139, 98, 66)',
        },
        {
          url: './images/slider05.jpg',
          title: '快来分享你的寒假日常吧~',
          color: 'rgb(67, 90, 92)',
        },
        {
          url: './images/slider06.jpg',
          title: '哔哩哔哩小年YEAH',
          color: 'rgb(166, 131, 143)',
        },
        {
          url: './images/slider07.jpg',
          title: '一站式解决你的电脑配置问题！！！',
          color: 'rgb(53, 29, 25)',
        },
        {
          url: './images/slider08.jpg',
          title: '谁不想和小猫咪贴贴呢！',
          color: 'rgb(99, 72, 114)',
        },
      ]

      // 1.获取元素
      const img = document.querySelector('.slider-wrapper img')
      const p = document.querySelector('.slider-footer p')
      console.log(img, p)
      let i = 0 //数组下标（索引），控制显示那张图片

      // 2.开启定时器
      setInterval(function () {
        i++
        console.log(arr[i])
        // 当i=8时，无缝衔接，从第一张开始，继续轮播
        if (i >= arr.length) {
          i = 0
        }
        // 更换图片路径
        img.src = arr[i].url

        // 修改p内容
        p.innerHTML = arr[i].title

        // 5.小圆点
        // 比如 i=1；我们要取第二个li
        //排它思想
        // 1.去掉老的
        const li_old = document.querySelector('.slider-indicator .active')
        // 删除类名
        li_old.classList.remove('active')

        // 2.显示新的
        const li_new = document.querySelector(
          `.slider-indicator li:nth-child(${i + 1}`
        )
        li_new.classList.add('active')
      }, 1000)
    </script>
  </body>
</html>

```

## 7.测试

PC端：https://ks.wjx.top/vj/hwyC7n1.aspx



![image-20220721223412610](Web%20APIs%20%E7%AC%AC%E4%B8%80%E5%A4%A9%20Dom%E8%8E%B7%E5%8F%96&%E5%B1%9E%E6%80%A7%E6%93%8D%E4%BD%9C.assets/image-20220721223412610.png)