# Web APIs 第四天 Dom节点&移动端滑动

## 一、日期对象

* 日期对象：用来表示时间的对象 

* 作用：可以得到当前系统时间

### 1. 实例化

![image-20220809194816505](Web%20APIs%20%E7%AC%AC%E5%9B%9B%E5%A4%A9%20Dom%E8%8A%82%E7%82%B9&%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%BB%91%E5%8A%A8.assets/image-20220809173359875.png)

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
      // 构造函数
      function Star(name, age) {
        this.name = name
        this.age = age
      }
      const ldh = new Star('刘德华', 20)
      console.log(ldh)
      // 实例化：new通过构造函数生成实例对象的过程

      // 1.new实例化一个日期对象
      // 不传参数，获取的是当前的时间
      const date = new Date()
      console.log(date)

      // 2.指定时间
      const date2 = Date('2022-7-25 08:30:00')
      console.log(date2)
    </script>
  </body>
</html>

```

### 2.日期对象方法

![image-20220726104400922](Web%20APIs%20%E7%AC%AC%E5%9B%9B%E5%A4%A9%20Dom%E8%8A%82%E7%82%B9&%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%BB%91%E5%8A%A8.assets/image-20220726104400922.png)

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
      // 1.先得到一个日期对象
      const date = new Date()
      // 2.使用里面的方法，获取年月日，时分秒
      console.log(date.getFullYear())
      console.log(date.getMonth() + 1)
      console.log(date.getDate())
      console.log(date.getDay())

      const h = date.getHours()
      const m = date.getMinutes()
      const s = date.getSeconds()
      console.log(h, m, s)
    </script>
  </body>
</html>

```

#### 2.1案例

![image-20220726104442433](Web%20APIs%20%E7%AC%AC%E5%9B%9B%E5%A4%A9%20Dom%E8%8A%82%E7%82%B9&%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%BB%91%E5%8A%A8.assets/image-20220726104442433.png)

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
      div {
        width: 300px;
        height: 40px;
        border: 1px solid pink;
        text-align: center;
        line-height: 40px;
      }
    </style>
  </head>

  <body>
    <div></div>
    <script>
      function getDate() {
        // 1.实例化日期对象
        const date = new Date()
        const year = date.getFullYear()
        let month = date.getMonth() + 1
        let day = date.getDay()

        let h = date.getHours()
        let m = date.getMinutes()
        let s = date.getSeconds()

        month = month < 10 ? '0' + month : month
        day = day < 10 ? '0' + day : day
        h = h < 10 ? '0' + h : h
        m = m < 10 ? '0' + m : m
        s = s < 10 ? '0' + s : s

        return `今天是:${year}年${month}月${day}日  ${h}时:${m}分:${s}秒`
      }
      const div = document.querySelector('div')
      setInterval(function () {
        div.innerHTML = getDate()
      }, 1000)
    </script>
  </body>
</html>

```

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
      div {
        width: 300px;
        height: 40px;
        border: 1px solid pink;
        text-align: center;
        line-height: 40px;
      }
    </style>
  </head>

  <body>
    <div></div>
    <script>
      const div = document.querySelector('div')
      setInterval(function () {
        const date = Date()
        div.innerHTML = date.toLocaleString()
      }, 1000)
      // 实际开发
      // 1. moment.js http://momentjs.cn/ ， 缺点：有点大
      // moment().format('YYYY-MM-DD HH:mm:ss');

      // 2. https://dayjs.fenxianglu.cn/  day.js  目前推荐
      // dayjs().format('YYYY-MM-DD HH:mm:ss');
    </script>
  </body>
</html>

```

### 3. 时间戳

* 目标：能够获得当前时间戳 
* 使用场景： 如果计算倒计时效果，前面方法无法直接计算，需要借助于时间戳完成 
* 什么是时间戳:
  * 是指1970年01月01日00时00分00秒起至现在的毫秒数，它是一种特殊的计量时间的方式
* 算法：
  *  将来的时间戳 - 现在的时间戳 = 剩余时间毫秒数
  * 剩余时间毫秒数 转换为 剩余时间的 年月日时分秒 就是 倒计时时间
  *  比如 将来时间戳 2000ms - 现在时间戳 1000ms = 1000ms 
  *  1000ms 转换为就是 0小时0分1秒

#### 3.1获取时间戳方式

![image-20220726104839115](Web%20APIs%20%E7%AC%AC%E5%9B%9B%E5%A4%A9%20Dom%E8%8A%82%E7%82%B9&%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%BB%91%E5%8A%A8.assets/image-20220726104839115.png)

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
      // 时间戳 1970/01/01 00:00:00     邮戳 盖章  独一无二
      // 按当前时间到1970那个时间点的毫秒数
      const date = new Date()
      console.log(date.getTime())

      console.log(+new Date())

      console.log(Date.now())

      // 注意+new Date() 可以指定具体的时间点
      let now = +new Date()
      let furture = +new Date('2022-08-25 08:00:00')
      console.log(furture - now)

      // 获取星期几
      const day = new Date()
      console.log(day.getDate())
      const arr = [
        '星期天',
        '星期一',
        '星期二',
        '星期三',
        '星期四',
        '星期五',
        '星期六',
      ]
      const i = day.getDay()
      console.log(arr[i])
    </script>
  </body>
</html>

```

### 4.总结

![image-20220726104927161](Web%20APIs%20%E7%AC%AC%E5%9B%9B%E5%A4%A9%20Dom%E8%8A%82%E7%82%B9&%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%BB%91%E5%8A%A8.assets/image-20220726104927161.png)

### 5.案例

![image-20220726104947888](Web%20APIs%20%E7%AC%AC%E5%9B%9B%E5%A4%A9%20Dom%E8%8A%82%E7%82%B9&%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%BB%91%E5%8A%A8.assets/image-20220726104947888.png)

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
      .countdown {
        width: 240px;
        height: 305px;
        text-align: center;
        line-height: 1;
        color: #fff;
        background-color: brown;
        /* background-size: 240px; */
        /* float: left; */
        overflow: hidden;
      }

      .countdown .next {
        font-size: 16px;
        margin: 25px 0 14px;
      }

      .countdown .title {
        font-size: 33px;
      }

      .countdown .tips {
        margin-top: 80px;
        font-size: 23px;
      }

      .countdown small {
        font-size: 17px;
      }

      .countdown .clock {
        width: 142px;
        margin: 18px auto 0;
        overflow: hidden;
      }

      .countdown .clock span,
      .countdown .clock i {
        display: block;
        text-align: center;
        line-height: 34px;
        font-size: 23px;
        float: left;
      }

      .countdown .clock span {
        width: 34px;
        height: 34px;
        border-radius: 2px;
        background-color: #303430;
      }

      .countdown .clock i {
        width: 20px;
        font-style: normal;
      }
    </style>
  </head>

  <body>
    <div class="countdown">
      <p class="next">今天是2222年2月22日</p>
      <p class="title">下班倒计时</p>
      <p class="clock">
        <span id="hour">00</span>
        <i>:</i>
        <span id="minutes">25</span>
        <i>:</i>
        <span id="scond">20</span>
      </p>
      <p class="tips">18:30:00下课</p>
    </div>
    <script>
      // 函数封装 getCountTime
      function getCountTime() {
        // const date = new Date()

        // 1. 得到当前的时间戳
        const now = +new Date()
        // 2. 得到将来的时间戳
        const last = +new Date('2022-8-8 18:30:00')
        // console.log(now, last)
        // 3. 得到剩余的时间戳 count  记得转换为 秒数
        const count = (last - now) / 1000

        // console.log(count)
        // 4. 转换为时分秒
        // h = parseInt(总秒数 / 60 / 60 % 24)   //   计算小时
        // m = parseInt(总秒数 / 60 % 60);     //   计算分数
        // s = parseInt(总秒数 % 60);
        // let d = parseInt(count / 60 / 60 / 24)               //   计算当前秒数
        // const year = date.getFullYear()
        // let month = date.getMonth() + 1
        // let day = date.getDay()
        let h = parseInt((count / 60 / 60) % 24)
        let m = parseInt((count / 60) % 60)
        let s = parseInt(count % 60)

        // month = month < 10 ? '0' + month : month
        // day = day < 10 ? '0' + day : day
        h = h < 10 ? '0' + h : h
        m = m < 10 ? '0' + m : m
        s = s < 10 ? '0' + s : s
        console.log(h, m, s)
        //  5. 把时分秒写到对应的盒子里面
        document.querySelector('#hour').innerHTML = h
        document.querySelector('#minutes').innerHTML = m
        document.querySelector('#scond').innerHTML = s
        // document.querySelector(
        //   '.next'
        // ).innerHTML = `今天是:${year}年${month}月${day}日`
      }
      // 先调用一次
      getCountTime()

      // 开启定时器
      setInterval(getCountTime, 1000)
    </script>
  </body>
</html>

```



## 二、节点操作

### 1.DOM 节点

* DOM节点
  * DOM树里每一个内容都称之为节点 
*  节点类型 
  *  元素节点 
    * 所有的标签 比如 body、 div 
    *  html 是根节点 
  *  属性节点
    * 所有的属性 比如 href 
  * 文本节点 
    *  所有的文本 
    *  其他

![image-20220726105145404](Web%20APIs%20%E7%AC%AC%E5%9B%9B%E5%A4%A9%20Dom%E8%8A%82%E7%82%B9&%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%BB%91%E5%8A%A8.assets/image-20220726105145404.png)

#### 1.2总结

- 什么是DOM 节点？ 
  - DOM树里每一个内容都称之为节点 
- DOM节点的分类？
  - 元素节点 比如 div标签
  - 属性节点 比如 class属性
  - 文本节点 比如标签里面的文字 
- 我们重点记住那个节点？ 
  - 元素节点
  -  可以更好的让我们理清标签元素之间的关系



### 2.查找节点

![image-20220726105614584](Web%20APIs%20%E7%AC%AC%E5%9B%9B%E5%A4%A9%20Dom%E8%8A%82%E7%82%B9&%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%BB%91%E5%8A%A8.assets/image-20220726105614584.png)

#### 2.1父节点查找

![image-20220726105635369](Web%20APIs%20%E7%AC%AC%E5%9B%9B%E5%A4%A9%20Dom%E8%8A%82%E7%82%B9&%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%BB%91%E5%8A%A8.assets/image-20220726105635369.png)

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
    <div class="grand-father">
      <div class="father">
        <!-- 123 -->
        <div class="son">x</div>
      </div>
    </div>
    <script>
      // 文档 : document  一个页面就是一个文档
      // 元素 : element 页面上所有的标签都叫元素
      // 节点 : node 页面上所有的内容都叫做节点 ； 元素节点，属性节点，文本节点，注释节点
      // node.parentNode  返回最近一级的父节点 找不到返回null
      const son = document.querySelector('.son')
      console.log(son.parentNode)
      console.log(son.parentNode.parentNode)
    </script>
  </body>
</html>

```

##### 2.1.1案例

![image-20220726105719011](Web%20APIs%20%E7%AC%AC%E5%9B%9B%E5%A4%A9%20Dom%E8%8A%82%E7%82%B9&%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%BB%91%E5%8A%A8.assets/image-20220726105719011.png)

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
      .box {
        position: relative;
        width: 1000px;
        height: 200px;
        background-color: pink;
        margin: 100px auto;
        text-align: center;
        font-size: 50px;
        line-height: 200px;
        font-weight: 700;
      }

      .box1 {
        position: absolute;
        right: 20px;
        top: 10px;
        width: 20px;
        height: 20px;
        background-color: skyblue;
        text-align: center;
        line-height: 20px;
        font-size: 16px;
        cursor: pointer;
      }
    </style>
  </head>

  <body>
    <div class="wrap">
      <div class="box">
        我是广告
        <div class="box1">X</div>
      </div>
      <div class="box">
        我是广告
        <div class="box1">X</div>
      </div>
      <div class="box">
        我是广告
        <div class="box1">X</div>
      </div>
    </div>

    <script>
      // // 获取元素
      // const btn = document.querySelector('.box1')
      // // 绑定事件
      // btn.addEventListener('click', function (e) {
      //   this.parentNode.style.display = 'none'
      //   console.log(this)
      //   console.log(e.currentTarget) //绑定事件元素

      //   console.log(e.target) //触发事件元素
      // })

      // 获取三个按钮
      // const closeBtns = document.querySelectorAll('.box1')
      // 给每个按钮绑定事件
      // for (let i = 0; i < closeBtns.length; i++) {
      //   closeBtns[i].addEventListener('click', function (e) {
      //     console.log(this)
      //     this.parentNode.style.display = 'none'
      //   })
      // }

      // 2.事件委托的方式
      // 找到一个公共父元素
      const wrap = document.querySelector('.wrap')
      wrap.addEventListener('click', function (e) {
        console.log(e.target)
        if (e.target.className === 'box1') {
          e.target.parentNode.style.display = 'none'
        }
      })
    </script>
  </body>
</html>

```

#### 2.2子节点查找

![image-20220726105814422](Web%20APIs%20%E7%AC%AC%E5%9B%9B%E5%A4%A9%20Dom%E8%8A%82%E7%82%B9&%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%BB%91%E5%8A%A8.assets/image-20220726105814422.png)



#### 2.3兄弟关系查找

![image-20220726105850120](Web%20APIs%20%E7%AC%AC%E5%9B%9B%E5%A4%A9%20Dom%E8%8A%82%E7%82%B9&%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%BB%91%E5%8A%A8.assets/image-20220726105850120.png)

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
    <ul>
      <li>1</li>
      <li>2</li>
      <li>3</li>
      <li>4</li>
      <li>5</li>
    </ul>
    <script>
      // Q: 获取ul下的所有li标签
      const lis = document.querySelectorAll('li')

      // 1. 子节点 (文本,注释,属性,元素)
      // 语法: node.childNodes ;  node表示父元素
      const ul = document.querySelector('ul')
      console.log(ul.childNodes) // 获取所有的子节点, 包含元素节点,文本节点等
      // 返回值 是一个伪数组  有索引, 有length, 但是没有数组的方法

      // 2.子元素节点
      // 语法 ：node.children
      // 获取父元素的所有子元素节点
      // 返回值也是一个伪数组，元素集合，实际开发中常用
      console.log(ul.children)
      // 2.1 获取第一个子元素节点
      console.log(ul.children[0])
      // 2.2 获取最后一个子元素节点
      console.log(ul.children[ul.children.length - 1])

      // 3.兄的元素节点
      const li2 = document.querySelector('ul li:nth-child(2)')
      console.log(li2)

      // 3.1 前一个兄弟元素节点
      console.log(li2.previousElementSibling)
      // 后一个兄弟节点
      console.log(li2.nextElementSibling)
    </script>
  </body>
</html>

```

#### 2.4 总结

- 查找父节点用那个属性？
  - parentNode 
-  查找所有子节点用那个属性？ 
  -  children
-  查找兄弟节点用那个属性？
  - nextElementSibling 
  - previousElementSibling

### 3.增加节点

- 目标：能够具备根据需求新增节点的能力
-  很多情况下，我们需要在页面中增加元素 
  - 比如，点击发布按钮，可以新增一条信息 
-  一般情况下，我们新增节点，按照如下操作：
  - 创建一个新的节点 
  -  把创建的新的节点放入到指定的元素内部 
- 学习路线：
  -  创建节点 
  - 追加节点

#### 3.1.创建节点

![image-20220726110258515](Web%20APIs%20%E7%AC%AC%E5%9B%9B%E5%A4%A9%20Dom%E8%8A%82%E7%82%B9&%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%BB%91%E5%8A%A8.assets/image-20220726110258515.png)

#### 3.2追加节点

![image-20220726110335713](Web%20APIs%20%E7%AC%AC%E5%9B%9B%E5%A4%A9%20Dom%E8%8A%82%E7%82%B9&%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%BB%91%E5%8A%A8.assets/image-20220726110335713.png)

```HTML
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>

  <body>
    <ul>
      <li>我是老大</li>
      <li>我是老大</li>
      <li>我是老大</li>
    </ul>
    <script>
      // // 创建元素节点
      // const li = document.createElement('li')
      // console.log(li)
      // 2.添加元素
      // 父元素.appendChild(要追加的元素)
      // appendChild 是在父元素最后追加
      const ul = document.querySelector('ul')
      const li = document.createElement('li')
      li.innerHTML = '我是新创建的li标签'
      ul.appendChild(li)

      // 3.父元素.insertBefore(插入的元素，放到那个元素的前面)
      const li2 = document.createElement('li')
      li2.innerHTML = '我也是'
      ul.insertBefore(li2, ul.children[0])
    </script>
  </body>
</html>

```

#### 3.3案例

![image-20220726110449232](Web%20APIs%20%E7%AC%AC%E5%9B%9B%E5%A4%A9%20Dom%E8%8A%82%E7%82%B9&%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%BB%91%E5%8A%A8.assets/image-20220726110449232.png)

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>学车在线首页</title>
    <link rel="stylesheet" href="./css/style.css" />
    <style></style>
  </head>

  <body>
    <!-- 4. box核心内容区域开始 -->
    <div class="box w">
      <div class="box-hd">
        <h3>精品推荐</h3>
        <a href="#">查看全部</a>
      </div>
      <div class="box-bd">
        <ul class="clearfix"></ul>
      </div>
    </div>
    <script>
      // 1. 重构
      let data = [
        {
          src: 'images/course01.png',
          title: 'Think PHP 5.0 博客系统实战项目演练',
          num: 1125,
        },
        {
          src: 'images/course02.png',
          title: 'Android 网络动态图片加载实战',
          num: 357,
        },
        {
          src: 'images/course03.png',
          title: 'Angular2 大前端商城实战项目演练',
          num: 22250,
        },
        {
          src: 'images/course04.png',
          title: 'Android APP 实战项目演练',
          num: 389,
        },
        {
          src: 'images/course05.png',
          title: 'UGUI 源码深度分析案例',
          num: 124,
        },
        {
          src: 'images/course06.png',
          title: 'Kami2首页界面切换效果实战演练',
          num: 432,
        },
        {
          src: 'images/course07.png',
          title: 'UNITY 从入门到精通实战案例',
          num: 888,
        },
        {
          src: 'images/course08.png',
          title: 'Cocos 深度学习你不会错过的实战',
          num: 590,
        },
      ]

      const ul = document.querySelector('.box-bd ul')

      //   根据数据的个数，创建对应多少个li
      for (let i = 0; i < data.length; i++) {
        const li = document.createElement('li')
        // 把内容创建好的li
        li.innerHTML = `
                    <a href="#">
                        <img src="${data[i].src}" alt="">
                        <h4>
                            ${data[i].title}
                        </h4>
                        <div class="info">
                            <span>高级</span> • <span>${data[i].num}</span>人在学习
                        </div>
                    </a> `

        // 将创建好的li 添加到ul中
        ul.appendChild(li)
      }
    </script>
  </body>
</html>

```

#### 3.4 增加节点

![image-20220726110549678](Web%20APIs%20%E7%AC%AC%E5%9B%9B%E5%A4%A9%20Dom%E8%8A%82%E7%82%B9&%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%BB%91%E5%8A%A8.assets/image-20220726110549678.png)

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
    <ul>
      <li>1</li>
      <li>2</li>
      <li>3</li>
    </ul>
    <script>
      // 1.语法
      // const dupNode = node.cloneNode()
      // node 将要克隆的节点
      // dupNode dup  dulicate的缩写, 复制, 表示克隆生成的副本节点

      // Q: 克隆ul下面第一个li标签
      const ul = document.querySelector('ul')
      // 获取了ul下第一个li标签
      const li_0 = ul.children[0]
      const dup_li = li_0.cloneNode(true)

      // 2. 传参
      // false : 默认为false, 不传就是false. 只复制标签, 不复制标签里面的内容
      // true  : 复制标签和标签内的内容.

      console.log(dup_li)

      // 3. 应用 : 将复制(克隆)的节点,往ul里面添加
      // ul.appendChild(dup_li)
      ul.insertBefore(dup_li, ul.children[ul.children.length - 1])
    </script>
  </body>
</html>

```

### 4.删除节点

![image-20220726110715688](Web%20APIs%20%E7%AC%AC%E5%9B%9B%E5%A4%A9%20Dom%E8%8A%82%E7%82%B9&%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%BB%91%E5%8A%A8.assets/image-20220726110715688.png)

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style></style>
  </head>

  <body>
    <button>删除</button>
    <ul>
      <li>熊大</li>
      <li>熊二</li>
      <li>光头强1</li>
      <li>光头强2</li>
      <li>光头强3</li>
      <li>光头强4</li>
    </ul>

    <ul class="ul-test">
      <li>
        <span>
          <button class="btn">删除</button>
        </span>
      </li>
    </ul>
    <script>
      // 删除节点 ：父元素.removeChild(child) child 要删除的节点
      // Q ：点击按钮 删除ul 下的第一个子元素节点 ul.li.children[0]
      const ul = document.querySelector('ul')
      const btn = document.querySelector('button')
      btn.addEventListener('click', function () {
        if (ul.children.length === 0) {
          // 禁用按钮
          this.disabled = true
        } else {
          ul.removeChild(ul.children[0])
        }
      })

      const ul_test = document.querySelector('.ul-test')
      const btn_test = document.querySelector('.btn')
      // node.removeChild 只能删除父节点下面的最近一层字节点 ，跨层级不能删除
      btn.addEventListener('click', function () {
        ul_test.removeChild(btn.btn_test.parentNode.parentNode)
      })
    </script>
  </body>
</html>

```



## 三、M端事件

![image-20220727160104632](Web%20APIs%20%E7%AC%AC%E5%9B%9B%E5%A4%A9%20Dom%E8%8A%82%E7%82%B9&%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%BB%91%E5%8A%A8.assets/image-20220727160104632.png)

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
      div {
        width: 300px;
        height: 300px;
        background-color: pink;
      }
    </style>
  </head>

  <body>
    <div></div>
    <script>
      // 在pc上模拟移动端事件，一定要切换成移动端的模式才可以!
      // 获取元素
      const div = document.querySelector('div')
      // 1. touchstart: 手指触摸到DOM元素时触发
      div.addEventListener('touchstart', function () {
        console.log('我触摸到了这个div----touchstart')
      })
      // 2. touchmove: 手指在DOM元素身上移动事件
      div.addEventListener('touchmove', function () {
        console.log('我在这个dom元素上移动-touchmove')
      })
      // 3. touchend: 手指在dom元素上离开时触发
      div.addEventListener('touchend', function () {
        console.log('轻轻的我走了-touchend')
      })
    </script>
  </body>
</html>

```



## 四、JS插件

* 插件: 就是别人写好的一些代码,我们只需要复制对应的代码,就可以直接实现对应的效果 
* 学习插件的基本过程 
  * 熟悉官网,了解这个插件可以完成什么需求 https://www.swiper.com.cn/  
  *  看在线演示,找到符合自己需求的demo https://www.swiper.com.cn/demo/index.html
  * 查看基本使用流程 https://www.swiper.com.cn/usage/index.html 
  *  查看APi文档,去配置自己的插件 https://www.swiper.com.cn/api/index.html 
  * 注意: 多个swiper同时使用的时候, 类名需要注意区分
* Swiper相关
  * 下载            https://www.swiper.com.cn/download/index.html
  * 使用方法    https://www.swiper.com.cn/usage/index.htmlSwiper
  * 配置            https://www.swiper.com.cn/api/autoplay/16.html

```js
var swiper = new Swiper(".mySwiper", {
  // 小圆点
  pagination: {
    el: ".swiper-pagination",
  },
  // 自动播放
  autoplay: {
    delay: 1000,//1秒切换一次
    disableOnInteraction: false,  // 鼠标点击 触摸之后，自动继续播放
  },
  // 可以键盘控制
  keyboard: {
    enabled: true,
    onlyInViewport: true,
  },
});

```



## 五、综合案例

### 1.游乐园轮播图

![image-20220727160551606](Web%20APIs%20%E7%AC%AC%E5%9B%9B%E5%A4%A9%20Dom%E8%8A%82%E7%82%B9&%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%BB%91%E5%8A%A8.assets/image-20220727160551606.png)

```css
<style>
      html,
      body {
        position: relative;
        height: 100%;
      }

      body {
        background: #eee;
        font-family: Helvetica Neue, Helvetica, Arial, sans-serif;
        font-size: 14px;
        color: #000;
        margin: 0;
        padding: 0;
      }

      .swiper {
        width: 100%;
        height: 100%;
      }

      .swiper-slide {
        text-align: center;
        font-size: 18px;
        background: #fff;

        /* Center slide text vertically */
        display: -webkit-box;
        display: -ms-flexbox;
        display: -webkit-flex;
        display: flex;
        -webkit-box-pack: center;
        -ms-flex-pack: center;
        -webkit-justify-content: center;
        justify-content: center;
        -webkit-box-align: center;
        -ms-flex-align: center;
        -webkit-align-items: center;
        align-items: center;
      }

      .swiper-slide img {
        display: block;
        width: 100%;
        height: 100%;
        object-fit: cover;
      }

      .swiper-pagination-bullet-active {
        background: rgb(192, 255, 206);
      }
    </style>
```

```html
    <!-- 轮播图模块 -->
      <div class="banner">
        <!-- 轮播图模块 -->
        <!-- Swiper -->
        <div class="swiper mySwiper">
          <div class="swiper-wrapper">
            <div class="swiper-slide">
              <img src="./images/nature-2.jpg" alt="" srcset="" />
            </div>
            <div class="swiper-slide">
              <img src="./images/nature-3.jpg" alt="" srcset="" />
            </div>
            <div class="swiper-slide">
              <img src="./images/nature-4.jpg" alt="" srcset="" />
            </div>
            <div class="swiper-slide">
              <img src="./images/nature-5.jpg" alt="" srcset="" />
            </div>
            <div class="swiper-slide">
              <img src="./images/nature-7.jpg" alt="" srcset="" />
            </div>
            <div class="swiper-slide">
              <img src="./images/nature-8.jpg" alt="" srcset="" />
            </div>
            <div class="swiper-slide">
              <img src="./images/nature-9.jpg" alt="" srcset="" />
            </div>
          </div>
          <div class="swiper-pagination"></div>
        </div>
```

```js
    <script>
      var swiper = new Swiper('.mySwiper', {
        pagination: {
          el: '.swiper-pagination',
        },
        autoplay: true,
      })
    </script>
```

### 2.学生信息表案例

![image-20220727160956109](Web%20APIs%20%E7%AC%AC%E5%9B%9B%E5%A4%A9%20Dom%E8%8A%82%E7%82%B9&%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%BB%91%E5%8A%A8.assets/image-20220727160956109.png)

![image-20220727161004807](Web%20APIs%20%E7%AC%AC%E5%9B%9B%E5%A4%A9%20Dom%E8%8A%82%E7%82%B9&%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%BB%91%E5%8A%A8.assets/image-20220727161004807.png)

![image-20220727161013887](Web%20APIs%20%E7%AC%AC%E5%9B%9B%E5%A4%A9%20Dom%E8%8A%82%E7%82%B9&%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%BB%91%E5%8A%A8.assets/image-20220727161013887.png)

![image-20220727161048436](Web%20APIs%20%E7%AC%AC%E5%9B%9B%E5%A4%A9%20Dom%E8%8A%82%E7%82%B9&%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%BB%91%E5%8A%A8.assets/image-20220727161048436.png)

![image-20220727161106127](Web%20APIs%20%E7%AC%AC%E5%9B%9B%E5%A4%A9%20Dom%E8%8A%82%E7%82%B9&%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%BB%91%E5%8A%A8.assets/image-20220727161106127.png)

![image-20220727161116650](Web%20APIs%20%E7%AC%AC%E5%9B%9B%E5%A4%A9%20Dom%E8%8A%82%E7%82%B9&%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%BB%91%E5%8A%A8.assets/image-20220727161116650.png)

![image-20220727161127169](Web%20APIs%20%E7%AC%AC%E5%9B%9B%E5%A4%A9%20Dom%E8%8A%82%E7%82%B9&%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%BB%91%E5%8A%A8.assets/image-20220727161127169.png)

```html
<body>
    <h1>新增学员</h1>
    <form class="info" autocomplete="off">
      姓名：<input type="text" class="uname" name="uname" /> 年龄：<input
        type="text"
        class="age"
        name="age"
      />
      性别:
      <select name="gender" class="gender">
        <option value="男">男</option>
        <option value="女">女</option>
      </select>
      薪资：<input type="text" class="salary" name="salary" /> 就业城市：<select
        name="city"
        class="city"
      >
        <option value="北京">北京</option>
        <option value="上海">上海</option>
        <option value="广州">广州</option>
        <option value="深圳">深圳</option>
        <option value="曹县">曹县</option>
      </select>
      <button class="add">录入</button>
    </form>

    <h1>就业榜</h1>
    <table>
      <thead>
        <tr>
          <th>学号</th>
          <th>姓名</th>
          <th>年龄</th>
          <th>性别</th>
          <th>薪资</th>
          <th>就业城市</th>
          <th>操作</th>
        </tr>
      </thead>
      <tbody>
        <!-- 
        <tr>
          <td>1001</td>
          <td>欧阳霸天</td>
          <td>19</td>
          <td>男</td>
          <td>15000</td>
          <td>上海</td>
          <td>
            <a href="javascript:">删除</a>
          </td>
        </tr> 
        -->
      </tbody>
    </table>

```

```js
<script>
      // 获取输入数据的那些元素
      const uname = document.querySelector('.uname')
      const age = document.querySelector('.age')
      const gender = document.querySelector('.gender')
      const salary = document.querySelector('.salary')
      const city = document.querySelector('.city')
      const tbody = document.querySelector('tbody')

      // 1.声明一个空数组，用来存放录入的数据
      const arr = []
      // 录入模块，获取表单
      const form = document.querySelector('.info')
      // 返回的是一堆伪数组
      const items = document.querySelectorAll('.info [name]')
      // 表单有个submit提交事件       form表单有个submit提交
      form.addEventListener('submit', function (e) {
        // 表单点击提交会跳转，阻止这个默认行为
        e.preventDefault()

        for (let i = 1; i < items.length; i++) {
          if (items[i].value === '') {
            return alert('输入的内容不能为空，请重新输入')
          }
        }
        // 创建一个对象
        const obj = {
          stuId: arr.length + 1,
          uname: uname.value,
          age: age.value,
          gender: gender.value,
          salary: salary.value,
          city: city.value,
        }
        // 追加到数组里面
        arr.push(obj)
        console.log(arr)
        // 清空表单，重置表单value=''很麻烦，需要挨个写
        this.reset()
        // 绑定事件元素
        console.log(this)

        render() //回调函数
      })

      // 2.渲染函数，因为录入和删除都需要重新渲染
      // 声明式
      // function render(){
      // }
      // const声明的变量不提升，var声明的变量才提升
      const render = function () {
        // 最新数据重新渲染前，清空以前的行
        tbody.innerHTML = ''
        // 遍历arr根据数组的元素个数，创建tr
        for (let i = 0; i < arr.length; i++) {
          const tr = document.createElement('tr')
          tr.innerHTML = `
          <td>${arr[i].stuId}</td>
          <td>${arr[i].uname}</td>
          <td>${arr[i].age}</td>
          <td>${arr[i].gender}</td>
          <td>${arr[i].salary}</td>
          <td>${arr[i].city}</td>
          <td>
            <a href="javascript:" data-id=${i}>删除</a>
          </td>
          `
          // 追加元素， tbody.appendChild(子元素)
          tbody.appendChild(tr)
        }
      }

      // 3.删除操作
      // 事件委托，给a标签的刚刚父元素，tbody绑定点击事件
      tbody.addEventListener('click', function (e) {
        console.log(e.target)
        if (e.target.tagName === 'A') {
          // 删除数组里面对应索引号的那个元素
          console.log(e.target.dataset.id)
          arr.splice(e.target.dataset.id, 1)
          // 删除之后，重新渲染数据
          render()
        }
      })
    </script>
```

### 3. 重绘和回流

#### 3.1浏览器是如何进行界面渲染的

![image-20220727161514695](Web%20APIs%20%E7%AC%AC%E5%9B%9B%E5%A4%A9%20Dom%E8%8A%82%E7%82%B9&%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%BB%91%E5%8A%A8.assets/image-20220727161514695.png)

![image-20220727161611318](Web%20APIs%20%E7%AC%AC%E5%9B%9B%E5%A4%A9%20Dom%E8%8A%82%E7%82%B9&%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%BB%91%E5%8A%A8.assets/image-20220727161611318.png)

#### 3.2 重绘和回流

![image-20220727161625596](Web%20APIs%20%E7%AC%AC%E5%9B%9B%E5%A4%A9%20Dom%E8%8A%82%E7%82%B9&%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%BB%91%E5%8A%A8.assets/image-20220727161625596.png)

#### 3.3 会导致回流（重排）的操作： 

* 页面的首次刷新 
  * 浏览器的窗口大小发生改变 
  * 元素的大小或位置发生改变 
  * 改变字体的大小
  *  内容的变化（如：input框的输入，图片的大小）
  * 激活css伪类 （如：:hover） 
  * 脚本操作DOM（添加或者删除可见的DOM元素）
*  简单理解影响到布局了，就会有回流

![image-20220727161839540](Web%20APIs%20%E7%AC%AC%E5%9B%9B%E5%A4%A9%20Dom%E8%8A%82%E7%82%B9&%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%BB%91%E5%8A%A8.assets/image-20220727161839540.png)

## 六、作业

PC端：https://ks.wjx.top/vj/hfanpNW.aspx

![image-20220727161918229](Web%20APIs%20%E7%AC%AC%E5%9B%9B%E5%A4%A9%20Dom%E8%8A%82%E7%82%B9&%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%BB%91%E5%8A%A8.assets/image-20220727161918229.png)