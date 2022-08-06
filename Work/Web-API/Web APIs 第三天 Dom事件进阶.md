# Web APIs 第三天 Dom事件进阶

## 一、事件流

### 1. 事件流与两个阶段说明

事件流是对事件执行过程的描述，了解事件的执行过程有助于加深对事件的理解，提升开发实践中对事件运用的灵活度。

![image-20220726095003900](Web%20APIs%20%E7%AC%AC%E4%B8%89%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E8%BF%9B%E9%98%B6.assets/image-20220726095003900.png)

### 2. 事件捕获

![image-20220726095134552](Web%20APIs%20%E7%AC%AC%E4%B8%89%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E8%BF%9B%E9%98%B6.assets/image-20220726095134552.png)

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <style>
    .father {
      width: 500px;
      height: 500px;
      background-color: pink;
    }

    .son {
      width: 200px;
      height: 200px;
      background-color: purple;
    }
  </style>
</head>

<body>
  <div class="father">
    <div class="son"></div>
  </div>
  <script>

    // 1. 概念 
    // 事件流 指的是 事件完整执行过程中的流动路径.
    // 描述的是 元素在页面中接收事件的顺序.

    // Eg1. 北京的朋友来成都请我吃饭
    // 四川 成都 金牛区 目标(我) 捕获阶段
    // 找到目标了 达到目标阶段(处于目标阶段)
    // 金牛 成都  四川  (回去了)   冒泡阶段 

    // Eg2. 抓鱼 跳到水里去抓鱼 
    // 从外到内, 跳到水里去  
    // 抓到鱼了 
    // 鱼冒泡泡   冒泡阶段 (从内到外)

    // Eg.3 联想按压手机屏幕, 从外层钢化膜,到内部传感器, 这个按压事件, 有一个传播的过程, 顺序.

    // 2. DOM事件流三个阶段 
    // 1. 捕获阶段  (从外到内)
    // 2. 达到目标阶段 
    // 3. 冒泡阶段  (从内到外)

    // addEvenListener 有三个参数, 第三个参数 我们一般省略, 默认为false
    // 如果第三个参数 传 true , 表示 使用捕获!
    // useCapture 是一个boolean值, true / false
    // target.addEventListener(type, listener, useCapture)

    const son = document.querySelector('.son')
    const father = document.querySelector('.father')
    const body = document.body
    const html = document.documentElement

    // 事件捕获：document  ->  html -> body -> father -> son

    // 事件捕获：addEventListener第三参数为 true
    son.addEventListener('click', function(){
        console.log('我是子盒子,我被点击了')
    }, true)

    father.addEventListener('click', function(){
        console.log('我是父盒子, 我被点击了')
    }, true)

    body.addEventListener('click', function(){
        console.log('我是body, 我被点击了')
    }, true)

    html.addEventListener('click', function(){
        console.log('我是html, 我被点击了')
    }, true)

    document.addEventListener('click', function(){
        console.log('我是document, 我被点击了')
    }, true)
  </script>
</body>

</html>
```

### 3. 事件冒泡

![image-20220726095428673](Web%20APIs%20%E7%AC%AC%E4%B8%89%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E8%BF%9B%E9%98%B6.assets/image-20220726095428673.png)

### 4. 阻止冒泡

![image-20220726095510501](Web%20APIs%20%E7%AC%AC%E4%B8%89%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E8%BF%9B%E9%98%B6.assets/image-20220726095510501.png)

![image-20220726095526566](Web%20APIs%20%E7%AC%AC%E4%B8%89%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E8%BF%9B%E9%98%B6.assets/image-20220726095526566.png)

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <style>
    .father {
      width: 500px;
      height: 500px;
      background-color: pink;
    }

    .son {
      width: 200px;
      height: 200px;
      background-color: purple;
    }
  </style>
</head>

<body>
  <div class="father">
    <div class="son"></div>
  </div>
  <script>
    // 事件冒泡
    // 事件从最具体的元素（文档树中最深的节点）开始触发，然后向上传播至没有那么具体的元素（文档）(---JS高程)

    // 事件冒泡： son ->  father -> body -> html -> document
    const son = document.querySelector('.son')
    const father = document.querySelector('.father')
    const body = document.body
    const html = document.documentElement

    // 事件冒泡：addEventListener第三个参数省略，或者为false
    son.addEventListener('click', function(e){
        console.log('我是子盒子,我被点击了')
        
    })

    father.addEventListener('click', function(e){
        
        console.log('我是父盒子, 我被点击了')
        e.stopPropagation()
    })

    body.addEventListener('click', function(){
        console.log('我是body, 我被点击了')
    })

    html.addEventListener('click', function(){
        console.log('我是html, 我被点击了')
    })

    document.addEventListener('click', function(){
        console.log('我是document, 我被点击了')
    })

    // 默认就是 事件冒泡, 
    // 事件的传播方式: 要么是事件捕获, 要么是事件冒泡

    // 1. 阻止事件冒泡:
    //      e.stopPropagation() 
    // 它阻止事件冒泡, 阻止的是事件的传播,
    // 不会阻碍函数内代码的执行.
    // 前提, 需要先写上 e 事件对象.
  </script>
</body>

</html>
```

### 5. 解绑事件

![image-20220726095635329](Web%20APIs%20%E7%AC%AC%E4%B8%89%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E8%BF%9B%E9%98%B6.assets/image-20220726095635329.png)

![image-20220726095645826](Web%20APIs%20%E7%AC%AC%E4%B8%89%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E8%BF%9B%E9%98%B6.assets/image-20220726095645826.png)

````html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>

<body>
  <button>点击</button>
  <script>
    // 事件解绑
    const btn = document.querySelector('button')
    // 1. 传统的方式
    // btn.onclick = function(){
    //   console.log('不要犯困哈~~')
    //   // 传统的方式, 事件解绑
    //   btn.onclick = null
    // }

    // 2. 监听的方式
    const fn = function(){
      console.log('事件监听的方式')

      btn.removeEventListener('click', fn)
    }
    btn.addEventListener('click', fn)

    // btn.removeEventListener('click', fn)


    // 3.注意 匿名函数, 无法解绑
    // btn.addEventListener('click', function(){
    //   console.log('哇哈哈哈')
    // })
    // // 
    // btn.removeEventListener('click', fn)
   

    // 4. 定义的函数的两种 
    // 变量提示, 函数提升, 预解析

    // 声明式
    function foo(){
      console.log(1)
    }
    btn.addEventListener('click', foo)
    // 表达式
    const bar = function(){
      console.log(2)
    }
    btn.addEventListener('click', bar)

    
    // 结论， 
    // 1. 表达式方式 定义的函数， 一定要写在调用的前面。
    // 2. 用声明式定义的函数， 可以写在调用的后面，但是，还是建议，写在调用的前面

  </script>
</body>

</html>
````

### 6. 鼠标经过事件的区别

![image-20220726095731286](Web%20APIs%20%E7%AC%AC%E4%B8%89%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E8%BF%9B%E9%98%B6.assets/image-20220726095731286.png)

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <style>
    .dad {
      width: 400px;
      height: 400px;
      background-color: pink;
    }

    .baby {
      width: 200px;
      height: 200px;
      background-color: purple;
    }
  </style>
</head>

<body>
  <div class="dad">
    <div class="baby"></div>
  </div>
  <script>
    // mouseenter / mouseleave 鼠标经过/鼠标离开
    // 没有事件冒泡
    const dad = document.querySelector('.dad')
    const baby = document.querySelector('.baby')
    // dad.addEventListener('mouseenter', function(){
    //   console.log('鼠标经过了')
    // })
    // dad.addEventListener('mouseleave', function(){
    //   console.log('鼠标离开了')
    // })

    // mouseover / mouseout  鼠标经过 / 鼠标离开 
    // 他们有事件冒泡, 也就是 
    // 当鼠标经过到son盒子的时候, son盒子接收到鼠标经过事件, 
    // 然后这个事件又会向上传播, dady这个盒子 也能监听到鼠标经过事件.
    dad.addEventListener('mouseover', function(){
      console.log('鼠标经过了')
    })
    dad.addEventListener('mouseout', function(){
      console.log('鼠标离开了')
    })

    // 两种方式 , 都可以用. 推荐用mouseenter / mouseleave 
  </script>
</body>

</html>
```



### 7. 两种注册事件的区别

![image-20220726095754867](Web%20APIs%20%E7%AC%AC%E4%B8%89%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E8%BF%9B%E9%98%B6.assets/image-20220726095754867.png)

## 二、事件委托

### 1.事件委托的好处

![image-20220726100012357](Web%20APIs%20%E7%AC%AC%E4%B8%89%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E8%BF%9B%E9%98%B6.assets/image-20220726100012357.png)

### 2.总结

![image-20220726100035905](Web%20APIs%20%E7%AC%AC%E4%B8%89%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E8%BF%9B%E9%98%B6.assets/image-20220726100035905.png)

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
  <ul>
    <li>第1个孩子</li>
    <li>第2个孩子</li>
    <li>第3个孩子</li>
    <li>第4个孩子</li>
    <li>第5个孩子</li>
    <p>我不需要变色</p>
  </ul>
  <script>
    // 鼠标点击li标签, 给当前的那个li标签, 改变字体颜色
    // const lis = document.querySelectorAll('li')
    // for (let i = 0; i < lis.length; i++) {
    //   lis[i].addEventListener('click', function(){
    //     console.log(this) // 指向的是当前的那个li标签
    //     this.style.color = 'orange'
    //   })
    // } 

    // 事件委托: 把事件委托给父元素, 代为处理

    // 1. 先获取公共的父元素
    const ul = document.querySelector('ul')
    // 2. 给父元素绑定事件
    ul.addEventListener('click', function(e){
      // console.log(this) // ul
      // 重要： e.target 
      // e.target  当前触发事件的元素  点的谁，e.target代表谁
      // this   绑定事件的元素 
      // e.currentTarget  绑定事件的元素
      console.log(e.currentTarget === this)

      // 点击li标签， li标签就是目标元素， 它先接受到点击事件，
      // 然后这个点击事件， 有事件冒泡， 向上传播， ul也能接受到点击事件。

      if (e.target.tagName === 'LI') {
        console.dir(e.target) // 打印一个对象的所有属性和方法
        e.target.style.color = 'orange'
      }
    })

    // 背下来！
    // 1. 事件委托的原理
    // 利用事件冒泡，将事件监听绑定到父元素上， 通过父元素来监听子元素的事件。
    // 2. 事件委托的好处
    // 减少事件注册的次数， 提高程序性能

    // e.target 触发事件的元素
    // this  绑定事件的元素
    // e.currentTarget 同this
  </script>
</body>

</html>
```

### 3.案例

#### 3.1 tab栏切换改造

![image-20220726100200845](Web%20APIs%20%E7%AC%AC%E4%B8%89%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E8%BF%9B%E9%98%B6.assets/image-20220726100200845.png)

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8" />
  <meta http-equiv="X-UA-Compatible" content="IE=edge" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>tab栏切换</title>
  <style>
    * {
      margin: 0;
      padding: 0;
    }

    .tab {
      width: 590px;
      height: 340px;
      margin: 20px;
      border: 1px solid #e4e4e4;
    }

    .tab-nav {
      width: 100%;
      height: 60px;
      line-height: 60px;
      display: flex;
      justify-content: space-between;
    }

    .tab-nav h3 {
      font-size: 24px;
      font-weight: normal;
      margin-left: 20px;
    }

    .tab-nav ul {
      list-style: none;
      display: flex;
      justify-content: flex-end;
    }

    .tab-nav ul li {
      margin: 0 20px;
      font-size: 14px;
    }

    .tab-nav ul li a {
      text-decoration: none;
      border-bottom: 2px solid transparent;
      color: #333;
    }

    .tab-nav ul li a.active {
      border-color: #e1251b;
      color: #e1251b;
    }

    .tab-content {
      padding: 0 16px;
    }

    .tab-content .item {
      display: none;
    }

    .tab-content .item.active {
      display: block;
    }
  </style>
</head>

<body>
  <div class="tab">
    <div class="tab-nav">
      <h3>每日特价</h3>
      <ul>
        <li><a class="active" href="javascript:;" data-id="0">精选</a></li>
        <li><a href="javascript:;" data-id="1">美食</a></li>
        <li><a href="javascript:;" data-id="2">百货</a></li>
        <li><a href="javascript:;" data-id="3">个护</a></li>
        <li><a href="javascript:;" data-id="4">预告</a></li>
      </ul>
    </div>
    <div class="tab-content">
      <div class="item active"><img src="./images/tab00.png" alt="" /></div>
      <div class="item"><img src="./images/tab01.png" alt="" /></div>
      <div class="item"><img src="./images/tab02.png" alt="" /></div>
      <div class="item"><img src="./images/tab03.png" alt="" /></div>
      <div class="item"><img src="./images/tab04.png" alt="" /></div>
    </div>
  </div>
  <script>
    // 1. 获取ul 父元素
    const ul = document.querySelector('.tab-nav ul')
    const items = document.querySelectorAll('.item')
    // 2. 给父元素绑定事件
    ul.addEventListener('click', function(e){
      console.dir(e.target)
      console.log(e.target)
      // 我们只有点击了 a 才会 进行后续的逻辑， 这里判断点的是不是a
      if (e.target.tagName === 'A') {
        // 排他思想
        // 干掉别人， 先移除原来的active
        document.querySelector('.tab-nav .active').classList.remove('active')
        // 让当前点击的那个li 添加active
        e.target.classList.add('active')

        // 下面大盒子显示 让对应的item 显示
        const i = e.target.dataset.id 
        console.log(i)
        // 干掉别人 移除类
        document.querySelector('.tab-content .active').classList.remove('active')
        // 给自己添加
        items[i].classList.add('active')
      }
    })
  </script>
</body>

</html>
```

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
  <form action="http://www.itcast.cn">
    <input type="submit" value="免费注册">
  </form>
  <a href="http://www.baidu.com">百度一下</a>
  <script>

      const form = document.querySelector('form')
      form.addEventListener('click', function(e){
        // 阻止默认行为
        // 现在阻止的是表单的默认点击提交的这个行为
        e.preventDefault()
      })

      const a = document.querySelector('a')
      a.addEventListener('click', function(e){
        // 阻止 a标签, 点击后 默认跳转的行为
        e.preventDefault()
      })

      // 阻止事件冒泡 : e.stopPropagation()
      // 阻止默认行为 : e.preventDefault()
  </script>
</body>

</html>
```



## 三、其他事件

### 1.页面加载事件

![image-20220726100253731](Web%20APIs%20%E7%AC%AC%E4%B8%89%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E8%BF%9B%E9%98%B6.assets/image-20220726100253731.png)

![image-20220726100302534](Web%20APIs%20%E7%AC%AC%E4%B8%89%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E8%BF%9B%E9%98%B6.assets/image-20220726100302534.png)

![image-20220726100314425](Web%20APIs%20%E7%AC%AC%E4%B8%89%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E8%BF%9B%E9%98%B6.assets/image-20220726100314425.png)

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <script>
    // 1. 页面加载事件  load 
    // 等待页面所有资源加载完毕, 就会去执行回调函数.
    window.addEventListener('load', function(){

      // const btn = document.querySelector('button')
      // btn.addEventListener('click', function(){
      //   console.log('大家饿了吗?')
      // })
    })

    // 2. DOMContentLoaded
    // 当DOM元素加载完成时, 就会去执行至回调函数. 不包括图片, 样式表等.
    document.addEventListener('DOMContentLoaded', function(){
      // const btn = document.querySelector('button')
      // btn.addEventListener('click', function(){
      //   console.log('大家饿了吗?')
      // })
    })

    // 1. window  load
    // 2. document  DOMContentLoaded

    // DOM加载完了之后, 才是所有的资源加载完呀

  </script>
</head>

<body>
  <button>点击</button>

  <script>
    // 推荐 : js 写在body闭标签前面 
    
  </script>
</body>

</html>
```

### 2.元素滚动事件

![image-20220726100703556](Web%20APIs%20%E7%AC%AC%E4%B8%89%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E8%BF%9B%E9%98%B6.assets/image-20220726100703556.png)

![image-20220726100710148](Web%20APIs%20%E7%AC%AC%E4%B8%89%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E8%BF%9B%E9%98%B6.assets/image-20220726100710148.png)

#### 2.1 页面滚动事件-获取位置

![image-20220726100746766](Web%20APIs%20%E7%AC%AC%E4%B8%89%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E8%BF%9B%E9%98%B6.assets/image-20220726100746766.png)

![image-20220726100758997](Web%20APIs%20%E7%AC%AC%E4%B8%89%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E8%BF%9B%E9%98%B6.assets/image-20220726100758997.png)

![image-20220726100808989](Web%20APIs%20%E7%AC%AC%E4%B8%89%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E8%BF%9B%E9%98%B6.assets/image-20220726100808989.png)



#### 2.2 页面滚动事件-滚动到指定的坐标

![image-20220726101144239](Web%20APIs%20%E7%AC%AC%E4%B8%89%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E8%BF%9B%E9%98%B6.assets/image-20220726101144239.png)



#### 2.3 案例

![image-20220726101206200](Web%20APIs%20%E7%AC%AC%E4%B8%89%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E8%BF%9B%E9%98%B6.assets/image-20220726101206200.png)

![image-20220726101212785](Web%20APIs%20%E7%AC%AC%E4%B8%89%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E8%BF%9B%E9%98%B6.assets/image-20220726101212785.png)

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
      padding-top: 100px;
      height: 3000px;
    }

    div {
      display: block;
      margin: 100px;
      /* overflow: scroll; */
      overflow-x: hidden;
      width: 200px;
      height: 200px;
      border: 1px solid #000;
    }
  </style>
</head>

<body>
  <div>
    我里面有很多很多的文字
    我里面有很多很多的文字
    我里面有很多很多的文字
    我里面有很多很多的文字
    我里面有很多很多的文字
    我里面有很多很多的文字
    我里面有很多很多的文字
    我里面有很多很多的文字
    我里面有很多很多的文字
    我里面有很多很多的文字
    我里面有很多很多的文字
    我里面有很多很多的文字
    我里面有很多很多的文字
    我里面有很多很多的文字

  </div>
  <script>
    const div = document.querySelector('div')
    // 1. 页面滚动事件  scroll  (window/document)
    // window.addEventListener('scroll', function(){
    //   // 我想知道页面滚动了多少像素, 被卷去了多少
    //   // scrollTop
    //   // html标签 : document.documentElement
    //   console.log(document.documentElement.scrollTop)

    //   // 页面滚动的距离
    //   const n = document.documentElement.scrollTop
    //   // 当页面滚动的距离大于100px的时候, 让div显示
    //   if (n >= 200) {
    //     div.style.display = 'block'
    //   } else {
    //     div.style.display = 'none'
    //   }

    // })

    // 2. 应用场景
    // 我们想要页面滚动到某个位置, 就让某些元素显示或隐藏
    // 这个时候, 就要用scroll事件来监听页面的滚动
    
    // 3. 思考? 怎么知道某个元素滚动了多少距离呢?
    // 元素被卷去的头部  
    // 元素.scrollTop  向上滚动,元素被卷去的头部  (常用)
    // 元素.scrollLeft  向左滚动, 元素被卷去的左侧距离(用得少一些)

    // 4. 对元素监听scroll事件
    div.addEventListener('scroll', function(){
      console.log(div.scrollTop)
      // scrollTop 返回的是number 不带单位
    })
    console.log(div.scrollHeight)
  </script>
</body>

</html>
```

### 3. 页面尺寸事件

![image-20220726101407377](Web%20APIs%20%E7%AC%AC%E4%B8%89%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E8%BF%9B%E9%98%B6.assets/image-20220726101407377.png)

#### 3.1 页面尺寸事件-获取元素宽高

![image-20220726101535488](Web%20APIs%20%E7%AC%AC%E4%B8%89%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E8%BF%9B%E9%98%B6.assets/image-20220726101535488.png)

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
      display: inline-block;
      width: 200px;
      height: 200px;
      background-color: pink;
      padding: 10px;
      border: 20px solid red;
    }
  </style>
</head>

<body>
  <div>123123123123123123123123123123123123123123123123123123123123123</div>
  <script>
        // 1. resize事件 
        // 可以监听浏览器窗口大小发生变化的时候, 执行回调函数
        window.addEventListener('resize', function(){
          console.log('窗口大小变化了')
        })

        // 2. clientWidth 
        // 动态的获取元素的大小 clientWidth = width + padding ;  
        // 注意: 不包含border, 返回值不带单位
        const div = document.querySelector('div')
        console.log(div.clientWidth)

  </script>
</body>

</html>
```

#### 3.1.1 案例

![image-20220726102025355](Web%20APIs%20%E7%AC%AC%E4%B8%89%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E8%BF%9B%E9%98%B6.assets/image-20220726102025355.png)

```js
// 小括号包含完整的function(){}() 刚讲的第一种写法
(function flexible(window, document) {
    // flexible.js 就是实时监听我们页面的大小,动态修改html根元素的字体大小

    // 获取 html 根元素
    var docEl = document.documentElement   // html
    
    // dpr 物理像素比, 是物理像素与逻辑像素的比 (DevicePixelRatio  [ˈreɪʃioʊ])
    // 物理像素: 设备分辨率, 硬件真实存在的像素点
    // 逻辑像素(咱们的css像素)：document.documentElement.clientWidth
    // 可查看 移动端html --> 375 iphone6
    var dpr = window.devicePixelRatio || 1

    //! 1. adjust body font size  设置我们 body 的字体大小
    function setBodyFontSize() {
        // 如果页面中有body 这个元素 就设置body的字体大小
        if (document.body) {  // 1 2 3
            document.body.style.fontSize = (12 * dpr) + 'px'
        } else {
            // 如果页面中没有body 这个元素，则等着 我们页面主要的DOM元素加载完毕再去设置body
            // 的字体大小
            document.addEventListener('DOMContentLoaded', setBodyFontSize)
        }
    }
    setBodyFontSize();

    //! 2. set 1rem = viewWidth / 10  设置我们html元素的字体大小, 即设置rem的基本单位像素
    // rem是相对单位，是相对html根元素。
    // 通过它既可以做到只修改根元素就成比例地调整所有字体大小
    function setRemUnit() {
        var rem = docEl.clientWidth / 10
        docEl.style.fontSize = rem + 'px'
    }

    setRemUnit()

    //! 3.当页面尺寸变化时, 重新设置rem
    // reset rem unit on page resize  当我们页面尺寸大小发生变化的时候，要重新设置下rem 的大小
    window.addEventListener('resize', setRemUnit)
        // pageshow 重新加载页面触发的事件 load事件 看视频
        // pageshow 兼容火狐  load
    window.addEventListener('pageshow', function(e) {
        // e.persisted 返回的是true 就是说如果这个页面是从缓存取过来的页面，也需要从新计算一下rem 的大小
        if (e.persisted) {
            setRemUnit()
        }
    })

    //! 4. 兼容0.5px处理 
    // detect 0.5px supports  有些移动端的浏览器不支持0.5像素的写法
    if (dpr >= 2) {
        // https://zhuanlan.zhihu.com/p/371898337
        var fakeBody = document.createElement('body')
        var testElement = document.createElement('div')
        testElement.style.border = '.5px solid transparent'
        fakeBody.appendChild(testElement)
        docEl.appendChild(fakeBody)
        if (testElement.offsetHeight === 1) {
            // 真正生效的是hairlines这个样式
            // 无法兼容安卓设备、 iOS 8 以下设备 // 2014
            docEl.classList.add('hairlines')
        }
        docEl.removeChild(fakeBody)
    }
}(window, document))

//flexible作用:  我们可以用flexible 配合rem来做页面自适应.
```

### 4.元素尺寸与位置

#### 4.1使用场景

![image-20220726102055628](Web%20APIs%20%E7%AC%AC%E4%B8%89%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E8%BF%9B%E9%98%B6.assets/image-20220726102055628.png)

#### 4.2元素尺寸于位置-尺寸

![image-20220726102245644](Web%20APIs%20%E7%AC%AC%E4%B8%89%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E8%BF%9B%E9%98%B6.assets/image-20220726102245644.png)

![image-20220726102257277](Web%20APIs%20%E7%AC%AC%E4%B8%89%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E8%BF%9B%E9%98%B6.assets/image-20220726102257277.png)

#### 4.3总结

![image-20220726102328027](Web%20APIs%20%E7%AC%AC%E4%B8%89%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E8%BF%9B%E9%98%B6.assets/image-20220726102328027.png)

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
        position: relative;
        width: 300px;
        height: 300px;
        background: pink;
        margin: 300px auto;
        /* overflow: hidden; */
        /* padding: 20px; */
        /* border: 10px solid orange; */
    }

    .son {
        width: 100px;
        height: 100px;
        background-color: palegreen;
        /* margin: 10px; */
    }

  </style>
</head>

<body>
  <div class="box">
    <div class="son"></div>
</div>
  <script>

    // 获取元素
    const box = document.querySelector('.box')
    const son = document.querySelector('.son')

    // 1. offsetLeft / offsetTop 
    // 获取元素距离最近一级带有定位父元素的位置
    // 如果父元素没有定位, 获取的是相对于body的位置
    // console.log(box.offsetLeft)
    // console.log(box.offsetTop)

    console.log(son.offsetLeft)
    console.log(son.offsetTop)
    // 重点: 是距离带有定位父元素的位置! 它只读属性, 不可以设置

    // 2. offsetWidth / offsetHeight
    // 可以得到元素的大小, offsetWidth 包含border
    // offsetWidth = width + padding + border
    // offsetHeight = height + padding + border
    // console.log(box.offsetWidth)
    // 
    // 元素的大小  不包含border
    // clientWidth = width + padding
    

  </script>
</body>

</html>
```

#### 4.4案例

##### 4.4.1仿京东固定导航栏案例

##### ![image-20220726102509123](Web%20APIs%20%E7%AC%AC%E4%B8%89%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E8%BF%9B%E9%98%B6.assets/image-20220726102509123.png)`

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        .content {
            overflow: hidden;
            width: 1000px;
            height: 3000px;
            background-color: pink;
            margin: 0 auto;
        }

        .backtop {
            display: none;
            width: 50px;
            left: 50%;
            margin: 0 0 0 505px;
            position: fixed;
            bottom: 60px;
            z-index: 100;
        }

        .backtop a {
            height: 50px;
            width: 50px;
            background: url(./images/bg2.png) 0 -600px no-repeat;
            opacity: 0.35;
            overflow: hidden;
            display: block;
            text-indent: -999em;
            cursor: pointer;
        }

        .header {
            position: fixed;
            top: -80px;
            left: 0;
            width: 100%;
            height: 80px;
            background-color: purple;
            text-align: center;
            color: #fff;
            line-height: 80px;
            font-size: 30px;
            transition: all .3s;
        }

        .sk {
            width: 300px;
            height: 300px;
            background-color: skyblue;
            margin-top: 500px;
        }
    </style>
</head>

<body>
    <div class="header">我是顶部导航栏</div>
    <div class="content">
        <div class="sk">秒杀模块</div>
    </div>
    <div class="backtop">
        <img src="./images/close2.png" alt="">
        <a href="javascript:;"></a>
    </div>
    <script>
        // 获取元素
        const box = document.querySelector('.sk')
        const header = document.querySelector('.header')

        // 1. 页面滚动事件
        window.addEventListener('scroll', function(){
            // 当页面滚动到秒杀模块的时候， 就改变 header 的 top， ==> 0
            // const n = document.documentElement.scrollTop
            const n = window.pageYOffset
            // if (n >= box.offsetTop) {
            //     header.style.top = 0
            // } else {
            //     // style一定不要忘了px
            //     header.style.top = '-80px'
            // }
            header.style.top = n >= box.offsetTop ? 0 : '-80px'
        })
    </script>
</body>

</html>
```



##### 4.4.2实现 bilibili 点击小滑块移动效果

```js
  <script>
    // 1. 事件委托的方式, 给父元素绑定
    const list = document.querySelector('.tabs-list')
    const line = document.querySelector('.line')

    // 2. 给list注册点击事件
    list.addEventListener('click', function(e){
      // 判断, 只有点击了A标签的时候, 才执行后面的逻辑
      console.log(this)
      // e.target  触发事件的元素
      console.dir(e.target)
      if (e.target.tagName === 'A') {
        //  把当前点击a标签距离左侧的位置, 给line的translateX
        // console.log(e.target.offsetLeft)
        line.style.transform = `translateX(${e.target.offsetLeft}px)`
      }
      
    })
  </script>
```

#### 4.5获取元素大小位置的另外方法

![image-20220726102729656](Web%20APIs%20%E7%AC%AC%E4%B8%89%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E8%BF%9B%E9%98%B6.assets/image-20220726102729656.png)

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
      height: 2000px;
    }

    div {
      width: 200px;
      height: 200px;
      background-color: pink;
      margin: 100px;
      padding: 10px;
      border: 10px solid red;
    }
  </style>
</head>

<body>
  <div></div>
  <script>
    const div = document.querySelector('div')
    console.log(div.getBoundingClientRect())
    // y / top 元素 相对于视口顶部的位置
    // x / left  相对于视口左侧的位置

    // width / height  ==> width + padding + border
    // 同： offsetWidth
  </script>
</body>

</html>
```

#### 4.6总结

![image-20220726102813006](Web%20APIs%20%E7%AC%AC%E4%B8%89%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E8%BF%9B%E9%98%B6.assets/image-20220726102813006.png)

## 四、属性选择器

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <style>
    /* input[value] {
      color: red;
    } */
    input[type=text] {
      color: red;
    }
  </style>
</head>

<body>
  <input type="text" value="123" data-id="0" data-name="andy">
  <input type="password">
  <script>
    const input = document.querySelector('input[data-id]')
    console.log(input)
    
    // 属性选择器
    const pwd = document.querySelector('input[type="password"]')
    console.log(pwd)

    const input = document.querySelector('input[value]')
    // console.log(input)
    console.log(input.dataset) // 自定义属性集合
    console.log(input.dataset.name) // 自定义属性集合

  </script>
</body>

</html>
```

## 五、立即执行函数

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
        // 立即执行函数   (IIFE) , 也叫做自执行函数
        // Immdiately-Invoked Function Expression

        // 1. 普通函数 , 先声明, 后调用
        function fn(){
            console.log('我很平凡')
        }
        fn()

        // 2. 立即执行函数, 不需要调用, 立马执行的函数
        // 方式一
        ;(function(){/* code */})()

        // 方式二
        ;(function(){/* code */}())

        // 3. 多个立即执行函数之间, 分号隔开

        // 4. 立即执行函数 也可以传入参数
        ;(function(a, b){
            console.log(a + b)
        })(1, 2)

        // 5. 立即执行函数的作用
        // 创建独立的作用域， 不会有命名冲突的情况. 
        // 一些插件， 老的一些库， 就是用立即执行函数包裹起来的。 


        
        // 什么时候需要加分号? 
        // ;()
        // ;[]

    </script>
</body>
</html>
```



## 五、综合案例

![image-20220726102856105](Web%20APIs%20%E7%AC%AC%E4%B8%89%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E8%BF%9B%E9%98%B6.assets/image-20220726102856105.png)

![image-20220726103302806](Web%20APIs%20%E7%AC%AC%E4%B8%89%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E8%BF%9B%E9%98%B6.assets/image-20220726103302806.png)

![image-20220726103309022](Web%20APIs%20%E7%AC%AC%E4%B8%89%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E8%BF%9B%E9%98%B6.assets/image-20220726103309022.png)

![image-20220726103318320](Web%20APIs%20%E7%AC%AC%E4%B8%89%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E8%BF%9B%E9%98%B6.assets/image-20220726103318320.png)

![image-20220726103325763](Web%20APIs%20%E7%AC%AC%E4%B8%89%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E8%BF%9B%E9%98%B6.assets/image-20220726103325763.png)

![image-20220726103331737](Web%20APIs%20%E7%AC%AC%E4%B8%89%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E8%BF%9B%E9%98%B6.assets/image-20220726103331737.png)

![image-20220726103340941](Web%20APIs%20%E7%AC%AC%E4%B8%89%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E8%BF%9B%E9%98%B6.assets/image-20220726103340941.png)

```js
 <script>

    // 第一个模块, 页面滑动, 显示隐藏右侧的电梯导航
    ;(function(){
          // 1. 获取元素
          const elevator = document.querySelector('.xtx-elevator')
          const entry = document.querySelector('.xtx_entry')
          // 2. 给页面注册滚动事件
          window.addEventListener('scroll', function(){
            // 3. 判断， 当页面滚动的距离 大于等于 300px 就让 elevator显示
              // const n = document.documentElement.scrollTop
              const n = window.pageYOffset
              elevator.style.opacity = n >= entry.offsetTop ? 1 : 0
          })

          // 点击返回页面顶部
          const backTop = document.querySelector('#backTop')
          backTop.addEventListener('click', function(){
            // 1. scrollTop 可读写
            // document.documentElement.scrollTop = 0

            // 2. window.scroll() / window.scrollTo()
            //   window.scroll(x, y)
            // window.scroll(0, 0)

            // 3. 设置滚动行为改为平滑的滚动
              // window.scrollTo({
              //     top: 0,
              //     behavior: "smooth" // 平滑 safari 不支持平滑
              // })
              window.scroll({
                  top: 0,
                  behavior: "smooth" // 平滑 safari 不支持平滑
              })
          })
    })()

  // 2. 点击右侧的电梯导航, 让页面滚动到对应的模块
  ;(function(){
      // 获取a标签的公共父元素 ul
      const list = document.querySelector('.xtx-elevator-list')
      list.addEventListener('click', function(e){
        // 判断是否点击的是A标签
        if (e.target.tagName === 'A' && e.target.dataset.name) {
          // 排他思想, 
          // 1.如果原来有active类名, 就移除类,
          const old = document.querySelector('.xtx-elevator-list .active')
          // 简写==> 如果if后面只有一句话, 可以省略括号 {}
          if (old) old.classList.remove('active')
          // 2. 给自己添加
          // 让当前点击的那个a标签, 添加active
          e.target.classList.add('active')

					// 获取自定义属性
					console.log()
					const id = e.target.dataset.name
					// 利用点击的那个元素的自定义属性, 我们可以找到对应的大盒子
					const top = document.querySelector(`.xtx_goods_${id}`).offsetTop
					// 让页面滚动到对应的位置
					document.documentElement.scrollTop = top
        }
      })
  }())

	// 3. 页面滚动, 可以根据大盒子 选择哪个a标签高亮
	;(function(){
		// 获取4个大盒子
		const news = document.querySelector('.xtx_goods_new')
		const popular = document.querySelector('.xtx_goods_popular')
		const brand = document.querySelector('.xtx_goods_brand')
		const topic = document.querySelector('.xtx_goods_topic')

		window.addEventListener('scroll', function(){
					// 3.1 先移除类
			    // 1.如果原来有active类名, 就移除类,
					const old = document.querySelector('.xtx-elevator-list .active')
          // 简写==> 如果if后面只有一句话, 可以省略括号 {}
          if (old) old.classList.remove('active')
					// 3.2 判断页面滑动的位置, 处于某两个中间, 让对应的小盒子高亮
					// 页面被卷去的头部
					const n = document.documentElement.scrollTop
					
					if (n >= news.offsetTop && n < popular.offsetTop) {
						// 让第一个a标签高亮
						document.querySelector('[data-name="new"]').classList.add('active')
					} else if (n >= popular.offsetTop && n < brand.offsetTop) {
						document.querySelector('[data-name=popular]').classList.add('active')
					} else if (n >= brand.offsetTop && n < topic.offsetTop) {
						document.querySelector('[data-name=brand]').classList.add('active')
					} else if (n >= topic.offsetTop) {
						document.querySelector('[data-name=topic]').classList.add('active')
					}

		})
	})()
  </script>
```

## 六、作业

 PC： https://ks.wjx.top/vj/wmkituU.aspx

![image-20220726103436472](Web%20APIs%20%E7%AC%AC%E4%B8%89%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E8%BF%9B%E9%98%B6.assets/image-20220726103436472.png)

