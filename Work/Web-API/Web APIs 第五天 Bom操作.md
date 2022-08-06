# Web APIs 第五天 Bom操作

## 一、Window对象

### 1.BOM(浏览器对象模型)

* BOM(Browser Object Model ) 是浏览器对象模型  
* window对象是一个全局对象，也可以说是JavaScript中的顶级对象 
* 像document、alert()、console.log()这些都是window的属性，基本BOM的属性和方法都是window的。
* 所有通过var定义在全局作用域中的变量、函数都会变成window对象的属性和方法
* window对象下的属性和方法调用的时候可以省略window

![image-20220729144929381](Web%20APIs%20%E7%AC%AC%E4%BA%94%E5%A4%A9%20Bom%E6%93%8D%E4%BD%9C.assets/image-20220729144929381.png)

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>

  <body>
    <script>
      // BOM  browser object model 浏览器对象模型
      // 把浏览器看做是一个对象
      // window是浏览器的顶级对象, 通常可以省略

      // DOM  document object model 文档对象模型
      // 把一个页面看做是一个对象.
      console.log(document === window.document) // true

      // 1.在全局作用域中, 用var声明的变量, 会成为window的属性
      var anum = 10
      console.log(anum)
      console.log(window)

      // 但是 const let 声明的变量不会!
      const abc = 200
      console.log(window.abc)

      // 2. 全局作用域中声明的函数会成为window对象的方法
      function fn() {
        console.log('hi~BOM')
      }
      fn()

      // window.alert()
      // window.setInterval() 都是window对象的方法
    </script>
  </body>
</html>

```

### 2.定时器-延时函数

![image-20220729145212808](Web%20APIs%20%E7%AC%AC%E4%BA%94%E5%A4%A9%20Bom%E6%93%8D%E4%BD%9C.assets/image-20220729145212808.png)

* 两种定时器对比：执行的次数 
  * 延时函数: 执行一次 
  * 间歇函数:每隔一段时间就执行一次,除非手动清除

````html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>

  <body>
    <script>
      // 1. setTimeout
      // 语法 setTimeout(回调函数, 延迟时间)  省略了window
      // setTimeout(cb, wait)
      // 1. window可以省略
      // 2. 单位 毫秒, 延迟时间,这个参数可以省略, 省略的时候默认为0，最小延迟4ms
      // 3. 它只执行一次
      // 4. 可以直接写函数, 还可以写函数名, `函数名()` (谁写谁被锤)
      // 5. 页面中可以有很多个定时器, 我们经常给定时器加一个标记(方便清除或者说关闭它)

      setInterval(function () {
        console.log('你好！')
      }, 1000)
      function fn() {
        console.log('声明式')
      }
      const cb = function () {
        console.log('表达式')
      }
      setInterval(cb, 1000)
      // 2.给定时器加一个唯一的标记
      let timer1 = setInterval(cb, 1000)
      console.log(timer1)
      console.log(typeof timer1)
      // 清除，关闭定时器
      clearInterval(timer1)

      // 3. setTimeout / setInterval 区别
      // setTimeout(cb, wait)  只执行一次, 间隔时间到了后, 就会执行
      // setInterval(cb, wait) 每隔一段时间, 就会执行一次. 会重复执行, 一直执行. 直到清除定时器.
    </script>
  </body>
</html>

````

#### 2.1.案例（5秒钟之后消失的广告）

![image-20220729145504719](Web%20APIs%20%E7%AC%AC%E4%BA%94%E5%A4%A9%20Bom%E6%93%8D%E4%BD%9C.assets/image-20220729145504719.png)

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
      img {
        position: fixed;
        left: 0;
        bottom: 0;
      }
    </style>
  </head>

  <body>
    <img src="./images/ad.png" alt="" />
    <script>
      const img = document.querySelector('img')
      setTimeout(function () {
        img.style.display = 'none'
      }, 5000)
    </script>
  </body>
</html>

```

#### 2.2 this 指向问题

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <script>
      // this 指向  ===>  指向 可以理解为 等于 代表谁
      // this在定义的时候不能确定, 只有执行调用的时候才能确定.!!! 重要
      // 背下来!

      // 1. 全局作用域中 / 普通函数中 / 定时器里面  this 指向 window
      // 1.1 全局作用域
      console.log(this) // window

      // 1.2 普通函数调用
      function fn() {
        console.log('大家吃早饭了嘛?')
        console.log(this) // window
      }
      fn()

      // 1.3 定时器里面
      setTimeout(function () {
        console.log(this) // window
      }, 1000)

      // 2.1方法调用中，谁调用这个方法，this指向谁
      const obj = {
        name: '小平',
        age: 18,
        sayHi: function () {
          console.log(this)  // this指向的是调用这个方法的对象
        },
      }
      obj.sayHi()   // 谁调用,指向谁
      // 2.2 事件注册的时候，this指向被绑定的元素
      const btn = document.querySelector('button')
      btn.addEventListener('click', function (e) {
        console.log(this) //绑定事件的元素
        console.log(e.target) // 触发事件的元素
        console.log(e.currentTarget) //同this, 绑定事件的元素
      })

      console.Log('-------------------')
      // 3.构造函数中，this 指向的是构造函数的实例
      function Foo(name, age) {
        this.name = name
        this.age = age
        console.Log(this)	// 这个this不一定
      }
      const personl = new Foo('小红', 19)
      const person2 = new Foo(小白, 18)
      
      // !! this在定义的时候,并不能确定指向,只有执行的时候才能确定

		var person1 = new Foo('小王', 18)
		console.log(person1)

		var person2 = new Foo('小红', 19)
		console.log(person2)
    </script>
  </body>
</html>

```



### 3.JS执行机制

JavaScript 语言的一大特点就是单线程，也就是说，同一个时间只能做一件事。 

这是因为 Javascript 这门脚本语言诞生的使命所致——JavaScript 是为处理页面中用户的交互，以及操作 DOM 而诞生的。比如我们对某个 DOM 元素进行添加和删除操作，不能同时进行。 应该先进行添加，之后 再删除。 

单线程就意味着，所有任务需要排队，前一个任务结束，才会执行后一个任务。这样所导致的问题是： 如 果 JS 执行的时间过长，这样就会造成页面的渲染不连贯，导致页面渲染加载阻塞的感觉。

#### 3.1同步和异步

* 为了解决这个问题，利用多核 CPU 的计算能力，HTML5 提出 Web Worker 标准，允许 JavaScript 脚本创建多个线 程。于是，JS 中出现了同步和异步。 
* 同步 
  * 前一个任务结束后再执行后一个任务，程序的执行顺序与任务的排列顺序是一致的、同步的。比如做饭的同步 做法：我们要烧水煮饭，等水开了（10分钟之后），再去切菜，炒菜。 
* 异步
  *  你在做一件事情时，因为这件事情会花费很长时间，在做这件事的同时，你还可以去处理其他事 情。比如做饭的异步做法，我们在烧水的同时，利用这10分钟，去切菜，炒菜。 
* 他们的本质区别： 这条流水线上各个流程的执行顺序不同。

#### 3.2 同步任务和异步任务

* 同步任务 
  * 同步任务都在主线程上执行，形成一个执行栈。 
* 异步任务 
  * JS 的异步是通过回调函数实现的。 
  * 一般而言，异步任务有以下三种类型: 
    * 普通事件，如 click、resize 等 
    * 资源加载，如 load、error 等 
    * 定时器，包括 setInterval、setTimeout 等 异步任务相关添加到任务队列中（任务队列也称为消息队列）。

![image-20220729150449990](Web%20APIs%20%E7%AC%AC%E4%BA%94%E5%A4%A9%20Bom%E6%93%8D%E4%BD%9C.assets/image-20220729150449990.png)

![image-20220729150641709](Web%20APIs%20%E7%AC%AC%E4%BA%94%E5%A4%A9%20Bom%E6%93%8D%E4%BD%9C.assets/image-20220729150641709.png)

![image-20220729150656549](Web%20APIs%20%E7%AC%AC%E4%BA%94%E5%A4%A9%20Bom%E6%93%8D%E4%BD%9C.assets/image-20220729150656549.png)

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>

  <body>
    <script>
      // 一些基本的概念
      // 1. JS是单线程的语言, 也就是同一时间只能做一件事情 (同步), 所有的工作都顺序执行.
      // 为什么JS是单线程的呢?
      // JS设计之初, 是为了做网页交互, 那么就会操作DOM元素..那么就会有添加或者删除DOM节点的一些操作.这些操作不能同时执行.

      // 2. 线程 和 进程.
      // 进程是资源分配的最小单位, 线程是CPU调度的最小单位. 太抽象. 不好理解.
      // 进程(process) : 一个进程就是一个正在运行的程序 (任务管理器)
      // 线程(thread) :  一个进程内执行着的每个任务即为一个线程. 线程是允许应用程序并发执行多个任务的一种机制.

      // 想象(工厂里面好多流水线) 整个运行着的工厂 就做进程 . 每一条流水线, 叫做线程.

      // 进程 = 火车, 线程 = 车厢
      // 1. 线程必须依附于进程存在 (单纯的车厢无法运行)
      // 2. 一个进程可以包含多个线程(一个火车里,可以有多个车厢)

      // 3. 同步和异步
      // 3.1  同步: 同一个时间只能执行一个任务, 上一个任务执行完,才能执行下一个任务. (串联)
      // 3.2  异步: 可以同时执行多个任务, 提高了程序执行效率. (并联)

      // 同步任务
      // 所有的同步任务都在主线程上执行, 形成一个执行栈.

      // 异步任务
      // JS的异步任务是通过回调函数来实现的, 在做某个任务的同时可以处理其他任务
      // 常见的三种类型
      // 事件:click, resize监听
      // 资源加载: load, DOMContentLoaded
      // 定时器: setTimeout / setInterval

      const btn = document.querySelector('.btn')
      // 点击事件, 事件监听, 会交给异步进程.

      console.log(2)
      setTimeout(function () {
        console.log(4)
      }, 0)
      console.log(3)
      // 异步任务交给异步进程. 当满足触发条件, 将回调函数, 放到任务队列里面去.
      setTimeout(function () {
        console.log(6)
      }, 0)
      // btn.addEventListener('click', function(){
      //   console.log(1)
      // })

      // JS的执行机制  理解记忆, 背下来!
      // 1. 首先判断JS任务是同步任务还是异步任务, 同步任务会在主线程的执行栈中依次执行.
      // 2. 异步任务会提交给相应的异步进程处理, 当满足触发条件的时候, 异步进程会将异步任务(回调函数) 放到任务队列中.
      // 3. 当主线程执行完所有的(所有的,所有的)同步任务后, 会去任务队列里面查看是否有可以执行的异步任务.
      //    如果有, 就拿到主线程中执行难, 执行完之后再去任务队列里面查找, 依次循环.`
    </script>
  </body>
</html>

```

### 4.location对象

* location 的数据类型是对象，它拆分并保存了 URL 地址的各个组成部分
*  常用属性和方法：
  * href 属性获取完整的 URL 地址，对其赋值时用于地址的跳转
  * search 属性获取地址中携带的参数，符号 ？后面部分 
  * hash 属性获取地址中的啥希值，符号 # 后面部分
  * eload 方法用来刷新当前页面，传入参数 true 时表示强制刷新

#### 4.1Location.href

![image-20220729151013775](Web%20APIs%20%E7%AC%AC%E4%BA%94%E5%A4%A9%20Bom%E6%93%8D%E4%BD%9C.assets/image-20220729151013775.png)

#### 4.1.1案例（5秒钟之后跳转的页面）

![image-20220729151100753](Web%20APIs%20%E7%AC%AC%E4%BA%94%E5%A4%A9%20Bom%E6%93%8D%E4%BD%9C.assets/image-20220729151100753.png)

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
      span {
        color: red;
      }
    </style>
  </head>

  <body>
    <a href="http://www.itcast.cn">支付成功<span>5</span>秒钟之后跳转到首页</a>
    <script>
      //  location.href 可以获取完整的url地址，同时还可以设置跳转
      // 获取元素
      const a = document.querySelector('a')
      // 声明定时器，并开启
      let num = 5
      let timerId = setInterval(function () {
        num--
        a.innerHTML = `支付成功<span>${num}</span>秒钟之后跳转到首页`
        if (num === 0) {
          // 清楚定时器
          clearInterval(timerId)
          // 跳转页面
          location.href = 'http://www.itcast.cn'
        }
      }, 1000)
    </script>
  </body>
</html>

```

#### 4.2Location.search

![image-20220729151249973](Web%20APIs%20%E7%AC%AC%E4%BA%94%E5%A4%A9%20Bom%E6%93%8D%E4%BD%9C.assets/image-20220729151249973.png)

#### 4.3Location.hash

![image-20220729151314015](Web%20APIs%20%E7%AC%AC%E4%BA%94%E5%A4%A9%20Bom%E6%93%8D%E4%BD%9C.assets/image-20220729151314015.png)

#### 4.4Location.reload

![image-20220729151354111](Web%20APIs%20%E7%AC%AC%E4%BA%94%E5%A4%A9%20Bom%E6%93%8D%E4%BD%9C.assets/image-20220729151354111.png)

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>

  <body>
    <form action="">
      <input type="text" name="username" />
      <input type="password" name="pwd" />
      <button>提交</button>
    </form>

    <a href="#/my">我的</a>
    <a href="#/friend">关注</a>
    <a href="#/download">下载</a>
    <button class="reload">刷新</button>

    <script>
      // location 是一个对象, 三个属性

      // location.href  跳转 , 可读写
      // location.search 获取 "?xxxx"
      // location.hash  获取"#"

      // const btn = document.querySelector('button')
      // btn.addEventListener('click', function(){
      //   location.href = 'http://www.baidu.com'
      // })

      // 2. location.reload()
      const reload = document.querySelector('.reload')
      reload.addEventListener('click', function () {
        // f5 刷新页面
        // location.reload()
        // 强制刷新  ctrl+f5
        location.reload(true)
      })
    </script>
  </body>
</html>

```

#### 4.5总结

*  location.href 属性获取完整的 URL 地址，对其赋值时用于地址的跳转 
* search 属性获取地址中携带的参数，符号 ？后面部分
* hash 属性获取地址中的啥希值，符号 # 后面部分
*  reload 方法用来刷新当前页面，传入参数 true 时表示强制刷新

### 5.navigator对象

* navigator的数据类型是对象，该对象下记录了浏览器自身的相关信息 

* 常用属性和方法：

  *  通过 userAgent 检测浏览器的版本及平台

    ```html
    <!DOCTYPE html>
    <html lang="en">
      <head>
        <meta charset="UTF-8" />
        <meta http-equiv="X-UA-Compatible" content="IE=edge" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>Document</title>
        <script></script>
      </head>
    
      <body>
        这是pc端的页面
        <script>
          // (function () { })()
          // 检测 userAgent（浏览器信息）
          ;(function () {
            const userAgent = navigator.userAgent
            // 验证是否为Android或iPhone
            const android = userAgent.match(/(Android);?[\s\/]+([\d.]+)?/)
            const iphone = userAgent.match(/(iPhone\sOS)\s([\d_]+)/)
            // 如果是Android或iPhone，则跳转至移动站点
            if (android || iphone) {
              location.href = 'http://m.itcast.cn'
            }
          })()
        </script>
      </body>
    </html>
    
    ```

### 6.histroy对象

history 对象表示当前窗口首次使用以来用户的导航历史记录。因为 history 是 window 的属性，所以每个 window 都有自己的 history 对象。出于安全考虑，这个对象不会暴露用户访问过的 URL，但可以通过它在不知道实际 URL 的情况下前进和后退。

![image-20220729151855423](Web%20APIs%20%E7%AC%AC%E4%BA%94%E5%A4%A9%20Bom%E6%93%8D%E4%BD%9C.assets/image-20220729151855423.png)

**history.back()** 和 **history.forward()** 模拟了浏览器的后退按钮和前进按钮.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>

  <body>
    <button>后退</button>
    <button>前进</button>
    <script>
      const back = document.querySelector('button:first-child')
      const forward = back.nextElementSibling
      back.addEventListener('click', function () {
        // 后退一步
        // history.back()
        history.go(-1)
      })
      forward.addEventListener('click', function () {
        // 前进一步
        // history.forward()
        history.go(1)
      })
    </script>
  </body>
</html>

```



## 二、本地存储

### 1.本地存储介绍

* 以前我们页面写的数据一刷新页面就没有了，是不是？
* 随着互联网的快速发展，基于网页的应用越来越普遍，同时也变的越来越复杂，为了满足各种各样的需求，会经常 性在本地存储大量的数据，HTML5规范提出了相关解决方案。 
  *  数据存储在用户浏览器中 
  * 设置、读取方便、甚至页面刷新不丢失数据  
  * 容量较大，sessionStorage和localStorage约 5M 左右 
* 常见的使用场景： 
  *  https://todomvc.com/examples/vanilla-es6/ 页面刷新数据不丢失

### 2.本地存储分类

#### 2.1localStorage

* 目标： 能够使用localStorage 把数据存储的浏览器中 
*  作用: 可以将数据永久存储在本地(用户的电脑), 除非手动删除，否则关闭页面也会存在 
*  特性： 
  *  可以多窗口（页面）共享（同一浏览器可以共享）
  *  以键值对的形式存储使用

![image-20220729152352883](Web%20APIs%20%E7%AC%AC%E4%BA%94%E5%A4%A9%20Bom%E6%93%8D%E4%BD%9C.assets/image-20220729152352883.png)

![image-20220729152435941](Web%20APIs%20%E7%AC%AC%E4%BA%94%E5%A4%A9%20Bom%E6%93%8D%E4%BD%9C.assets/image-20220729152435941.png)

#### 2.1sessionStorage

* 特性：
  * 生命周期为关闭浏览器窗口
  * 在同一个窗口(页面)下数据可以共享
  * 以键值对的形式存储使用
  * 用法跟localStorage 基本相同

#### 2.3总结

1. localStorage 作用是什么？ 
   - 可以将数据永久存储在本地(用户的电脑), 除非手动删除，否则关闭页面也会存在 
2. localStorage 存储，获取，删除的语法是什么？ 
   - 存储：localStorage.setItem(key, value) 
   - 获取：localStorage.getItem(key) 
   - 删除：localStorage.removeItem(key）

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>

  <body>
    <input type="text" name="name" class="name" />
    <button class="set">存数据</button>
    <button class="get">取数据</button>
    <script>
      // 不同浏览器可能不同, 但基本都是5M大小
      // ;(function () {
      //   var test = '0123456789'
      //   var add = function (num) {
      //     num += num
      //     if (num.length == 10240) {
      //       test = num
      //       return
      //     }
      //     add(num)
      //   }
      //   add(test)
      //   var sum = test
      //   var show = setInterval(function () {
      //     sum += test
      //     try {
      //       window.localStorage.removeItem('test')
      //       window.localStorage.setItem('test', sum)
      //       console.log(sum.length / 1024 + 'KB')
      //     } catch (e) {
      //       alert(sum.length / 1024 + 'KB超出最大限制')
      //       clearInterval(show)
      //     }
      //   }, 0.1)
      // })()

      // 生命周期：一个对象从创建到清楚的过程，数据存在的周期
      // localStorage 本地存储
      // 1.生命周期永久生效，除非手动删除，否则页面关闭也会存在
      // 2.可以多窗口共享
      // 3.以键值对方式储存， key vulue

      // 储存数据
      // localStorage.setItem('user_nam', '小张')
      // // 获取数据
      // console.log(localStorage.getItem('user_name'))
      // // 删除数据
      // console.log(localStorage.removeItem('user_name'))
      // // 清空数据  localStorage.clear()
      // localStorage.clear()

      // sessionStorage 会话存储空间
      // 1.生命周期为关闭浏览器窗口
      // 2.在同一个窗口（页面，Tab下）数据可以共享（同一域名下）
      // 3.键值对的形式存储

      // 储存数据
      // sessionStorage.setItem(key, vulue)
      // // 获取数据
      // sessionStorage.getItem(key, vulue)
      // // 删除数据
      // csessionStorage.removeItem(key, vulue)
      // 清空数据  sessionStorage.clear()
      // sessionStorage.clear()

      const btnSet = document.querySelector('.set')
      const btnGet = document.querySelector('.get')
      const input = document.querySelector('.name')
      btnSet.addEventListener('click', function () {
        localStorage.setItem('name_test', input.value)
      })
      btnGet.addEventListener('click', function () {
        console.log(localStorage.getItem('name_test'))
      })
    </script>
  </body>
</html>

```

### 3.存储复杂数据类型

![image-20220729152816760](Web%20APIs%20%E7%AC%AC%E4%BA%94%E5%A4%A9%20Bom%E6%93%8D%E4%BD%9C.assets/image-20220729152816760.png)

![image-20220729152828015](Web%20APIs%20%E7%AC%AC%E4%BA%94%E5%A4%A9%20Bom%E6%93%8D%E4%BD%9C.assets/image-20220729152828015.png)

![image-20220729152838600](Web%20APIs%20%E7%AC%AC%E4%BA%94%E5%A4%A9%20Bom%E6%93%8D%E4%BD%9C.assets/image-20220729152838600.png)

![image-20220729152851386](Web%20APIs%20%E7%AC%AC%E4%BA%94%E5%A4%A9%20Bom%E6%93%8D%E4%BD%9C.assets/image-20220729152851386.png)

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>

  <body>
    <script>
      const obj = {
        uname: '小张',
        age: 18,
        gender: '男',
      }

      // ps.  JSON格式:属性和值，key和value 都有引号，并且是双引号（值是number可以不带）

      // 1.  localStorage /sessionStorage 只能存字符串格式的数据

      // localStorage.setItem('tast_obj', obj)  //[Object,Object]

      // 2.复杂数据类型（对象，数组）必须转为JSON格式的字符串
      // JSON.stringify()
      localStorage.setItem('test_obj', JSON.stringify(obj))

      const res = localStorage.getItem('test_obj')
      console.log(typeof res)
      console.log(JSON.parse(res))

      const result = JSON.parse(localStorage.setItem('test_obj'))
      console.log(result.uname)
      console.log(result.age)

      // 对于复杂数据类型，存的时候，要转JSON格式字符串；取出来，又要转对象才能用
      // 1. JSON.stringify() 将对象形式转换为JSON格式的字符串
      // 2. JSON.parse() 将JSON格式的字符串，转为对象
    </script>
  </body>
</html>

```



## 三、综合案例

![image-20220729152932887](Web%20APIs%20%E7%AC%AC%E4%BA%94%E5%A4%A9%20Bom%E6%93%8D%E4%BD%9C.assets/image-20220729152932887.png)

![image-20220729152940753](Web%20APIs%20%E7%AC%AC%E4%BA%94%E5%A4%A9%20Bom%E6%93%8D%E4%BD%9C.assets/image-20220729152940753.png)

![image-20220729152947235](Web%20APIs%20%E7%AC%AC%E4%BA%94%E5%A4%A9%20Bom%E6%93%8D%E4%BD%9C.assets/image-20220729152947235.png)

![image-20220729153003440](Web%20APIs%20%E7%AC%AC%E4%BA%94%E5%A4%A9%20Bom%E6%93%8D%E4%BD%9C.assets/image-20220729153003440.png)



### map方法

![image-20220729154128762](Web%20APIs%20%E7%AC%AC%E4%BA%94%E5%A4%A9%20Bom%E6%93%8D%E4%BD%9C.assets/image-20220729154128762.png)

![image-20220729154145617](Web%20APIs%20%E7%AC%AC%E4%BA%94%E5%A4%A9%20Bom%E6%93%8D%E4%BD%9C.assets/image-20220729154145617.png)

map 也称为映射。映射是个术语，指两个元素的集之间元素相互“对应”的关系

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>

  <body>
    <script>
      // Array.map()
      // 1. 作用: map() 方法创建一个新数组，
      //    这个新数组由原数组中的每个元素都调用一次提供的函数后的返回值组成。

      // 2. 参数 arr.map()方法接收一个函数,
      //   函数的第一个参数, 正在处理的当前元素   item , el
      //   函数的第二个参数, 正在处理的元素的索引号  index, i

      // 3. 返回值: 一个由原数组每个元素执行回调函数的结果组成的新数组

      // 4. 注意 : map() 中传入的函数 , 一般都需要写 return !

      const arr = ['red', 'pink', 'orange']

      const res = arr.map(function (item, index) {
        console.log(item)
        console.log(index)
        return item + '娃哈哈'
      })
      console.log(res)

      // 解释一下 回调函数
      // 回调函数 : 被作为实参传入另一函数，并在该外部函数内被调用，
      //           用以来完成某些任务的函数，称为回调函数。

      // 同步回调: 立即执行
      // 异步回调: 满足条件执行

      const arr1 = [10, 20, 30]
      const newArr1 = arr1.map(function (item) {
        return item + 10
      })
      console.log(newArr1)
    </script>
  </body>
</html>

```

### join方法

![image-20220729154251606](Web%20APIs%20%E7%AC%AC%E4%BA%94%E5%A4%A9%20Bom%E6%93%8D%E4%BD%9C.assets/image-20220729154251606.png)

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>

  <body>
    <script>
      // Array.join([分隔符])
      // 1.作用：将数组的所有元素链接成一个字符串，并返回这个字符串
      const arr = ['red', 'blue', 'green']
      // 把数组元素转换为字符串
      // 如果不传参数，逗号分隔
      console.log(arr.join())
    </script>
  </body>
</html>

```

![image-20220729154725817](Web%20APIs%20%E7%AC%AC%E4%BA%94%E5%A4%A9%20Bom%E6%93%8D%E4%BD%9C.assets/image-20220729154725817.png)

![image-20220729154738852](Web%20APIs%20%E7%AC%AC%E4%BA%94%E5%A4%A9%20Bom%E6%93%8D%E4%BD%9C.assets/image-20220729154738852.png)

![image-20220729154822291](Web%20APIs%20%E7%AC%AC%E4%BA%94%E5%A4%A9%20Bom%E6%93%8D%E4%BD%9C.assets/image-20220729154822291.png)

![image-20220729154843508](Web%20APIs%20%E7%AC%AC%E4%BA%94%E5%A4%A9%20Bom%E6%93%8D%E4%BD%9C.assets/image-20220729154843508.png)

![image-20220729154918599](Web%20APIs%20%E7%AC%AC%E4%BA%94%E5%A4%A9%20Bom%E6%93%8D%E4%BD%9C.assets/image-20220729154918599.png)

![image-20220729154925055](Web%20APIs%20%E7%AC%AC%E4%BA%94%E5%A4%A9%20Bom%E6%93%8D%E4%BD%9C.assets/image-20220729154925055.png)

![image-20220729154932099](Web%20APIs%20%E7%AC%AC%E4%BA%94%E5%A4%A9%20Bom%E6%93%8D%E4%BD%9C.assets/image-20220729154932099.png)

````js
  // 1. 读取本地存储的数据   student-data  本地存储的命名
      const data = localStorage.getItem('student-data')
      // console.log(data)
      // 2. 如果有就返回对象，没有就声明一个空的数组  arr 一会渲染的时候用的
      // const arr = data ? JSON.parse(data) : []

      // 获取 tbody
      const tbody = document.querySelector('tbody')
      // 3. 渲染模块函数
      const render = function () {
        const trArr = arr.map(function (item, i) {
          return `
        <tr>
          <td>${item.stuId}</td>
          <td>${item.uname}</td>
          <td>${item.age}</td>
          <td>${item.gender}</td>
          <td>${item.salary}</td>
          <td>${item.city}</td>
          <td>
            <a href="javascript:" data-id=${i}>删除</a>
          </td>
        </tr>
        `
        })
        // 因为 trArr 是个数组， 我们不要数组，我们要的是 tr的字符串 join()
        tbody.innerHTML = trArr.join('')
      }
      render()

      // 4. 录入模块
      const info = document.querySelector('.info')
      // 获取表单form 里面带有 name属性的元素
      const items = info.querySelectorAll('[name]')
      // console.log(items)
      info.addEventListener('submit', function (e) {
        // 阻止提交
        e.preventDefault()
        // 声明空的对象
        const obj = {}
        // obj.stuId = arr.length + 1
        // 加入有2条数据   2
        obj.stuId = arr.length ? arr[arr.length - 1].stuId + 1 : 1
        // 非空判断
        for (let i = 0; i < items.length; i++) {
          // console.log(items) // 数组里面包含 5个表单  name
          // console.log(items[i]) //  每一个表单 对象
          // console.log(items[i].name) //
          // item 是每一个表单
          const item = items[i]
          if (items[i].value === '') {
            return alert('输入内容不能为空')
          }
          // console.log(item.name)  uname  age gender
          // obj[item.name]   === obj.uname  obj.age
          obj[item.name] = item.value
        }
        // console.log(obj)
        // 追加给数组
        arr.push(obj)
        //  把数组 arr 存储到本地存储里面
        localStorage.setItem('student-data', JSON.stringify(arr))
        // 渲染页面
        render()
        // 重置表单
        this.reset()
      })

      // 5. 删除模块
      tbody.addEventListener('click', function (e) {
        if (e.target.tagName === 'A') {
          // alert(1)
          // console.log(e.target.dataset.id)
          // 删除数组对应的这个数据
          arr.splice(e.target.dataset.id, 1)
          // 写入本地存储
          localStorage.setItem('student-data', JSON.stringify(arr))
          // 重新渲染
          render()
        }
      })
````

## 四、作业

PC端地址： https://ks.wjx.top/vj/eKqRAy8.aspx

![image-20220729155113924](Web%20APIs%20%E7%AC%AC%E4%BA%94%E5%A4%A9%20Bom%E6%93%8D%E4%BD%9C.assets/image-20220729155113924.png)