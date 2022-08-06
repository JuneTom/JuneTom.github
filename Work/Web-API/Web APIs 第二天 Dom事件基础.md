# Web APIs 第二天 Dom事件基础

## 1.事件监听（绑定）

### 1.1 事件监听定义

![image-20220724144517166](Web%20APIs%20%E7%AC%AC%E4%BA%8C%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E5%9F%BA%E7%A1%80.assets/image-20220724144517166.png)

### 1.2 事件监听语法

![image-20220724144525809](Web%20APIs%20%E7%AC%AC%E4%BA%8C%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E5%9F%BA%E7%A1%80.assets/image-20220724144525809.png)

### 1.3 举例说明

![image-20220724144536859](Web%20APIs%20%E7%AC%AC%E4%BA%8C%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E5%9F%BA%E7%A1%80.assets/image-20220724144536859.png)

### 1.4总结

![image-20220722201048529](Web%20APIs%20%E7%AC%AC%E4%BA%8C%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E5%9F%BA%E7%A1%80.assets/image-20220722201048529.png)

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
  <button>点击</button>
  <script>
    // 需求： 点击了按钮，弹出一个对话框

    // 事件三要素:
    //   1. 事件源 : 谁, 谁被触发了
    //   2. 事件类型 : 什么事件, 比如click点击事件
    //   3. 事件处理程序 : 我们要干嘛

    // 获取元素
    const btn = document.querySelector('button')
    // 给按钮 btn 注册事件(绑定事件)
    btn.addEventListener('click', function(){
      // 事件处理程序  (我们要干嘛)
      alert('大家困不困, 困的话去洗洗脸~')
    })

    // 注意, 内部的函数, 一开始不执行, 当按钮被点击的时候才执行.
    // 回调函数 : 回头再调用


  </script>
</body>

</html>
```

### 1.5 练习

#### 1.5.1 京东点击关闭顶部广告

![image-20220722202604600](Web%20APIs%20%E7%AC%AC%E4%BA%8C%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E5%9F%BA%E7%A1%80.assets/image-20220722202604600.png)

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
  <div class="box">
    我是广告
    <div class="box1">X</div>
  </div>
  <script>
      // 需求：点击关闭按钮， 关闭父盒子
      // 核心：利用样式的显示和隐藏完成， display:none 隐藏元素 display:block 显示元素 

      // 1. 获取事件源
      const closeBtn = document.querySelector('.box1')
      // 2. 关掉的是大盒子
      const box = document.querySelector('.box')
      // 3. 注册事件
      closeBtn.addEventListener('click', function(){
          box.style.display = 'none'
      })

  </script>
</body>

</html>
```

#### 1.5.2 随机点名案例

![image-20220722202722557](Web%20APIs%20%E7%AC%AC%E4%BA%8C%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E5%9F%BA%E7%A1%80.assets/image-20220722202722557.png)

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        h2 {
            text-align: center;
        }

        .box {
            width: 600px;
            margin: 50px auto;
            display: flex;
            font-size: 25px;
            line-height: 40px;
        }

        .qs {

            width: 450px;
            height: 40px;
            color: red;

        }

        .btns {
            text-align: center;
        }

        .btns button {
            width: 120px;
            height: 35px;
            margin: 0 50px;
        }
    </style>
</head>

<body>
    <h2>随机点名</h2>
    <div class="box">
        <span>名字是：</span>
        <div class="qs">这里显示姓名</div>
    </div>
    <div class="btns">
        <button class="start">开始</button>
        <button class="end">结束</button>
    </div>

    <script>
        // // 数据
        const arr = ['马超', '黄忠', '赵云', '关羽', '张飞']
        // 0 - 4
        // 定义一个全局变量
        let timerId = 0
        let i = 0 // 随机下标
        // 1. 开始按钮的模块
        // 1.1 获取显示的div
        const person = document.querySelector('.qs')
        // 1.2 获取开始按钮
        const start = document.querySelector('.start')
        // 1.3 给start按钮, 注册事件
        start.addEventListener('click', function(){

           timerId = setInterval(function(){
                // 随机下标
                i = Math.floor(Math.random() * arr.length)
                // console.log(arr[i]) // 取到数组里的元素
                person.innerHTML = arr[i]
                // console.log(i)
            }, 30)
            // console.log(timerId)
            // 当数组只有一个值时, 让两个按钮禁用
            if (arr.length === 0) {
                start.disabled = true
                end.disabled = true
                // 赋值语句, 右结合性
                // start.disabled = end.disabled = true
                // 清除定时器
                clearInterval(timerId)
            }

        })

        // 2. 关闭按钮模块
        const end = document.querySelector('.end')
        end.addEventListener('click', function(){
            // 关闭定时器
            clearInterval(timerId)
            arr.splice(i, 1) // 传的是起始位置, 要删除元素的索引号. 
            console.log(arr)
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
  <button>点击</button>
  <script>
    const btn = document.querySelector('button')
    btn.addEventListener('click', function(){
      // 当我们这个函数执行完之后, 这里面的变量只在这个函数内部使用
      // 这个时候, 这个变量被当做垃圾回收了

      // 每次点击的时候, 都重新开辟了一个空间, 重新声明了这个变量
      const num = Math.random()
      console.log(num)
    })
  </script>
</body>

</html>
```



### 1.6 拓展阅读-事件监听版本

![image-20220722204754056](Web%20APIs%20%E7%AC%AC%E4%BA%8C%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E5%9F%BA%E7%A1%80.assets/image-20220722204754056.png)

![image-20220722204801370](Web%20APIs%20%E7%AC%AC%E4%BA%8C%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E5%9F%BA%E7%A1%80.assets/image-20220722204801370.png)

```js
const btn = document.querySelector('button')
// old版本:on --> 缺陷: 给同一个元素,绑定同一个事件, 后一个会覆盖前一个
btn.onclick = function () {
  console.log(1111)
}
btn.onclick = function () {
  console.log(2222)
}
// 像
// let num = 10
// num = 20   因为采取赋值的形式

// new版本 : addEventListener() 同一个元素可以绑定多次相同事件, 依次执行
btn.addEventListener('click', function () {
  console.log(1111)
})
btn.addEventListener('click', function () {
  console.log(2222)
})

```

## 2. 事件类型

### 1.事件类型

- 鼠标经过 / 离开 , 没有事件冒泡
  - mouseenter / mouseleave
- 鼠标离开 / 离开 , 有事件冒泡
  - mouseover / mouseout

![image-20220722210143197](Web%20APIs%20%E7%AC%AC%E4%BA%8C%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E5%9F%BA%E7%A1%80.assets/image-20220722210143197.png)

#### 1.1鼠标事件

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
  </style>
</head>

<body>
  <div></div>
  <script>
    // 获取元素
    const div = document.querySelector('div')
    
    // 鼠标经过
    div.addEventListener('mouseenter', function(){
      console.log('轻轻的我来了')
      div.style.backgroundColor = 'orange'
    })
    // 鼠标离开
    div.addEventListener('mouseleave', function(){
      console.log('轻轻的我走了, 不带走一片云彩')
      div.style.backgroundColor = 'pink'
    })

  </script>
</body>

</html>
```



#### 1.2焦点事件

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
  <input type="text">
  <script>
      // 焦点事件, 主要针对于 表单input textarea
      const ipt = document.querySelector('input')
      // 获取焦点  focus 
      ipt.addEventListener('focus', function(){
          console.log('获取了焦点')
      })
      // 失去焦点  blur
      ipt.addEventListener('blur', function(){
          console.log('失去了焦点')
      })
  </script>
</body>

</html>

```

#### focus选择器

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <style>
    input {
      /* width: 200px; */
      height: 40px;
      transition: all .3s;
      /* 过渡 */
    }

    /* focus伪类选择器  获得焦点 */
    /* ::after ::before  伪元素*/
    input:focus {
      /* width: 300px; */
      height: 80px;
    }
    /* 当某个动画, 能用CSS实现, 就不要用js实现, 因为CSS动画, 性能更好 */
  </style>
</head>

<body>
  <input type="text">
</body>

</html>
```



#### 1.3 键盘事件

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
  <input type="text">
  <script>
    const input = document.querySelector('input')

    // 1. 绑定事件  keydown 键盘按下  keyup 键盘抬起

    // keydown 如果按住, 会一直调用执行
    input.addEventListener('keydown', function(){
      console.log('键盘按下了')
    })

    // keyup 抬起不会一直执行, 只执行一次
    input.addEventListener('keyup', function(){
      console.log('键盘抬起了')
    })

    // 2. 表单用户输入事件 input
    input.addEventListener('input', function(){
       // 获取表单的内容 
       console.log(input.value)
    })
  </script>
</body>

</html>
```



### 2. 练习

#### 2.1 轮播图点击切换

![image-20220722210341622](Web%20APIs%20%E7%AC%AC%E4%BA%8C%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E5%9F%BA%E7%A1%80.assets/image-20220722210341622.png)

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
      { url: './images/slider01.jpg', title: '对人类来说会不会太超前了？', color: 'rgb(100, 67, 68)' },
      { url: './images/slider02.jpg', title: '开启剑与雪的黑暗传说！', color: 'rgb(43, 35, 26)' },
      { url: './images/slider03.jpg', title: '真正的jo厨出现了！', color: 'rgb(36, 31, 33)' },
      { url: './images/slider04.jpg', title: '李玉刚：让世界通过B站看到东方大国文化', color: 'rgb(139, 98, 66)' },
      { url: './images/slider05.jpg', title: '快来分享你的寒假日常吧~', color: 'rgb(67, 90, 92)' },
      { url: './images/slider06.jpg', title: '哔哩哔哩小年YEAH', color: 'rgb(166, 131, 143)' },
      { url: './images/slider07.jpg', title: '一站式解决你的电脑配置问题！！！', color: 'rgb(53, 29, 25)' },
      { url: './images/slider08.jpg', title: '谁不想和小猫咪贴贴呢！', color: 'rgb(99, 72, 114)' },
    ]

    // 获取元素
    const img = document.querySelector('.slider-wrapper img')
    const p = document.querySelector('.slider-footer p')
    const footer = document.querySelector('.slider-footer')

    // 1. 右侧按钮业务
    // 1.1 获取右侧按钮
    const next = document.querySelector('.next')
    let i = 0  // 控制图片播放的哪一张

    next.addEventListener('click', function(){
        i++
        // console.log(arr[i]) // 数组里面对应的对象
        // 如果i 大于等于8, 让i 恢复成第一张 0
        // if (i >= arr.length) {
        //   i = 0
        // }
        i = i >= arr.length ? 0 : i

        render()
    })

    // 2. 左侧按钮的业务
    const prev = document.querySelector('.prev')
    prev.addEventListener('click', function(){
        i--
        // 当 i 在 第一张图片时, 为0
        // 这个时候, 点击左键, i--之后, i就小于0了
        i = i < 0  ? arr.length - 1 : i
        render()
    })

    // 3. 抽取公共函数, render
    function render(){
        // 1.2 渲染对应的数据
        img.src = arr[i].url
        p.innerHTML = arr[i].title
        footer.style.backgroundColor = arr[i].color
        // 1.3 小圆点
        // 排他思想
        // 先找到原来active类名那个, 移除掉
        document.querySelector('.slider-indicator .active').classList.remove('active')
        // 让当前这个li添加active类名
        document.querySelector(`.slider-indicator li:nth-child(${i + 1})`).classList.add('active')
    }

    // 4. 自动播放
    let timerId = setInterval(function(){
      // 每过一秒, 自动点击一下右侧按钮
      // JS给我们提供了 自动调用点击事件的方法
      next.click()
    }, 1000)
    
    // 5. 鼠标经过大盒子, 停止定时器
    const slider = document.querySelector('.slider')

    slider.addEventListener('mouseenter', function(){
      // 关闭定时器
      clearInterval(timerId)
    })

    // 6. 鼠标离开大盒子, 重新开启定时器
    slider.addEventListener('mouseleave', function(){
      // 关闭定时器
      clearInterval(timerId)
      // 重新开启定时器
      timerId = setInterval(function(){
        next.click()
      }, 1000)
    })

  </script>
</body>

</html>
```

#### 2.2 小米搜索框案例

![image-20220722210702914](Web%20APIs%20%E7%AC%AC%E4%BA%8C%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E5%9F%BA%E7%A1%80.assets/image-20220722210702914.png)

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

        ul {

            list-style: none;
        }

        .mi {
            position: relative;
            width: 223px;
            margin: 100px auto;
        }

        .mi input {
            width: 223px;
            height: 48px;
            padding: 0 10px;
            font-size: 14px;
            line-height: 48px;
            border: 1px solid #e0e0e0;
            outline: none;
        }

        .mi .search {
            border: 1px solid #ff6700;
        }

        .result-list {
            display: none;
            position: absolute;
            left: 0;
            top: 48px;
            width: 223px;
            border: 1px solid #ff6700;
            border-top: 0;
            background: #fff;
        }

        .result-list a {
            display: block;
            padding: 6px 15px;
            font-size: 12px;
            color: #424242;
            text-decoration: none;
        }

        .result-list a:hover {
            background-color: #eee;
        }
    </style>

</head>

<body>
    <div class="mi">
        <input type="search" placeholder="小米笔记本">
        <ul class="result-list">
            <li><a href="#">全部商品</a></li>
            <li><a href="#">小米11</a></li>
            <li><a href="#">小米10S</a></li>
            <li><a href="#">小米笔记本</a></li>
            <li><a href="#">小米手机</a></li>
            <li><a href="#">黑鲨4</a></li>
            <li><a href="#">空调</a></li>
        </ul>
    </div>
    <script>
        // 1. 获取元素
        // const input = document.querySelector('[type=search]')  // 属性选择器
        const input = document.querySelector('.mi input')  // 属性选择器
        const ul = document.querySelector('.result-list')
        
        // 2. 监听事件 获取焦点
        input.addEventListener('focus', function(){
            // 让ul显示
            ul.style.display = 'block'
            // 给input框加上带颜色边框的类名
            input.classList.add('search')
        })

        // 3. 失去焦点
        input.addEventListener('blur', function(){
            // 让ul显示
            ul.style.display = 'none'
            input.classList.remove('search')
        })

        
    </script>
</body>

</html>
```

#### 2.3 评论字数统计

![image-20220722211204073](Web%20APIs%20%E7%AC%AC%E4%BA%8C%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E5%9F%BA%E7%A1%80.assets/image-20220722211204073.png)

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>评论回车发布</title>
  <style>
    .wrapper {
      min-width: 400px;
      max-width: 800px;
      display: flex;
      justify-content: flex-end;
    }

    .avatar {
      width: 48px;
      height: 48px;
      border-radius: 50%;
      overflow: hidden;
      background: url(./images/avatar.jpg) no-repeat center / cover;
      margin-right: 20px;
    }

    .wrapper textarea {
      outline: none;
      border-color: transparent;
      resize: none;
      background: #f5f5f5;
      border-radius: 4px;
      flex: 1;
      padding: 10px;
      transition: all 0.5s;
      height: 30px;
    }

    .wrapper textarea:focus {
      border-color: #e4e4e4;
      background: #fff;
      height: 50px;
    }

    .wrapper button {
      background: #00aeec;
      color: #fff;
      border: none;
      border-radius: 4px;
      margin-left: 10px;
      width: 70px;
      cursor: pointer;
    }

    .wrapper .total {
      margin-right: 80px;
      color: #999;
      margin-top: 5px;
      opacity: 0;
      transition: all 0.5s;
    }

    .list {
      min-width: 400px;
      max-width: 800px;
      display: flex;
    }

    .list .item {
      width: 100%;
      display: flex;
    }

    .list .item .info {
      flex: 1;
      border-bottom: 1px dashed #e4e4e4;
      padding-bottom: 10px;
    }

    .list .item p {
      margin: 0;
    }

    .list .item .name {
      color: #FB7299;
      font-size: 14px;
      font-weight: bold;
    }

    .list .item .text {
      color: #333;
      padding: 10px 0;
    }

    .list .item .time {
      color: #999;
      font-size: 12px;
    }
  </style>
</head>

<body>
  <div class="wrapper">
    <i class="avatar"></i>
    <textarea id="tx" placeholder="发一条友善的评论" rows="2" maxlength="200"></textarea>
    <button>发布</button>
  </div>
  <div class="wrapper">
    <span class="total">0/200字</span>
  </div>
  <div class="list">
    <div class="item" style="display: none;">
      <i class="avatar"></i>
      <div class="info">
        <p class="name">清风徐来</p>
        <p class="text">大家都辛苦啦，感谢各位大大的努力，能圆满完成真是太好了[笑哭][支持]</p>
        <p class="time">2022-10-10 20:29:21</p>
      </div>
    </div>
  </div>
  <script>
    //  获取元素
    const tx = document.querySelector('#tx')
    const total = document.querySelector('.total')

    // 1. 当我们文本域获取到焦点的时候, 让total显示  opacity = 1
    tx.addEventListener('focus', function(){
      total.style.opacity = 1
    })
    // 2. 当文本域失去焦点的时候, 让total 隐藏  opacity = 0
    tx.addEventListener('blur', function(){
      total.style.opacity = 0
    })

    // 3. 检测用户输入
    tx.addEventListener('input', function(){
      // console.log(tx.value.length)
      total.innerHTML = `${tx.value.length}/200字`
    })
  </script>
</body>

</html>
```

## 3.事件对象

### 3.1获取事件对象

#### 3.1.1 定义

**当事件发生的时候, 和这个事件相关的所有信息, 都存在这个对象中. 这个对象就叫做事件对象**

![image-20220722211749182](Web%20APIs%20%E7%AC%AC%E4%BA%8C%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E5%9F%BA%E7%A1%80.assets/image-20220722211749182.png)

#### 3.1.2 语法

![image-20220722211848009](Web%20APIs%20%E7%AC%AC%E4%BA%8C%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E5%9F%BA%E7%A1%80.assets/image-20220722211848009.png)

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
  <!-- <button>点击</button> -->
  <input type="text">
  <script>

    // 事件对象:
    // 当事件发生的时候, 和这个事件相关的所有信息, 都存在这个对象中, 这个对象就叫事件对象.
    // 书写位置:
    // 事件注册绑定的时候, 回调函数的第一个参数就是事件对象, 简写为 e

    const input = document.querySelector('input')

    input.addEventListener('keyup', function(e){
      console.log(e)
      // e是一个对象 
      // 常用的属性 
      // e.type  事件类型
      // e.key   针对键盘事件, 按的哪个键
      if (e.key === 'Enter') {
          console.log('我按下了Enter键')
      }
    })
  </script>
</body>

</html>
```

#### 3.1.3 总结

![image-20220722211933904](Web%20APIs%20%E7%AC%AC%E4%BA%8C%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E5%9F%BA%E7%A1%80.assets/image-20220722211933904.png)

### 3.2事件对象常用属性

#### 3.2.1 定义

![image-20220722212013286](Web%20APIs%20%E7%AC%AC%E4%BA%8C%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E5%9F%BA%E7%A1%80.assets/image-20220722212013286.png)

#### 3.2.2 练习

##### 3.2.2.1评论回车发布

![image-20220722212121345](Web%20APIs%20%E7%AC%AC%E4%BA%8C%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E5%9F%BA%E7%A1%80.assets/image-20220722212121345.png)

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>评论回车发布</title>
  <style>
    .wrapper {
      min-width: 400px;
      max-width: 800px;
      display: flex;
      justify-content: flex-end;
    }

    .avatar {
      width: 48px;
      height: 48px;
      border-radius: 50%;
      overflow: hidden;
      background: url(./images/avatar.jpg) no-repeat center / cover;
      margin-right: 20px;
    }

    .wrapper textarea {
      outline: none;
      border-color: transparent;
      resize: none;
      background: #f5f5f5;
      border-radius: 4px;
      flex: 1;
      padding: 10px;
      transition: all 0.5s;
      height: 30px;
    }

    .wrapper textarea:focus {
      border-color: #e4e4e4;
      background: #fff;
      height: 50px;
    }

    .wrapper button {
      background: #00aeec;
      color: #fff;
      border: none;
      border-radius: 4px;
      margin-left: 10px;
      width: 70px;
      cursor: pointer;
    }

    .wrapper .total {
      margin-right: 80px;
      color: #999;
      margin-top: 5px;
      opacity: 0;
      transition: all 0.5s;
    }

    .list {
      min-width: 400px;
      max-width: 800px;
      display: flex;
    }

    .list .item {
      width: 100%;
      display: flex;
    }

    .list .item .info {
      flex: 1;
      border-bottom: 1px dashed #e4e4e4;
      padding-bottom: 10px;
    }

    .list .item p {
      margin: 0;
    }

    .list .item .name {
      color: #FB7299;
      font-size: 14px;
      font-weight: bold;
    }

    .list .item .text {
      color: #333;
      padding: 10px 0;
    }

    .list .item .time {
      color: #999;
      font-size: 12px;
    }
  </style>
</head>

<body>
  <div class="wrapper">
    <i class="avatar"></i>
    <textarea id="tx" placeholder="发一条友善的评论" rows="2" maxlength="200"></textarea>
    <button>发布</button>
  </div>
  <div class="wrapper">
    <span class="total">0/200字</span>
  </div>
  <div class="list">
    <div class="item" style="display: none;">
      <i class="avatar"></i>
      <div class="info">
        <p class="name">清风徐来</p>
        <p class="text">大家都辛苦啦，感谢各位大大的努力，能圆满完成真是太好了[笑哭][支持]</p>
        <p class="time">2022-10-10 20:29:21</p>
      </div>
    </div>
  </div>
  <script>
    //  获取元素
    const tx = document.querySelector('#tx')
    const total = document.querySelector('.total')

    // 1. 当我们文本域获取到焦点的时候, 让total显示  opacity = 1
    tx.addEventListener('focus', function(){
      total.style.opacity = 1
    })
    // 2. 当文本域失去焦点的时候, 让total 隐藏  opacity = 0
    tx.addEventListener('blur', function(){
      total.style.opacity = 0
    })

    // 3. 检测用户输入
    tx.addEventListener('input', function(){
      // console.log(tx.value.length)
      total.innerHTML = `${tx.value.length}/200字`
    })
    //=================================== new Code

    // 4. 按下回车发布评论
    const item = document.querySelector('.item')
    const text = document.querySelector('.text')

    tx.addEventListener('keyup', function(e){
      // 判断用户按下的是否是回车键 
      if (e.key === 'Enter') {

        // trim 去掉输入的字符串左右两边的空格
        if (tx.value.trim()) {
          item.style.display = 'block'
          // tx.value 用户输入的内容
          text.innerHTML = tx.value 
        }
        // if ('123')  ==> if (true)
        // '', NaN, null, undefined, 0 
        // 这些会在if里面隐式转换为false, 其余的都会转为true

        // 按下回车后, 清空内容
        tx.value = ''
        // 字符统计, 也要重置
        total.innerHTML = '0/200字'
      }
    })

  </script>
</body>

</html>
```

##### 3.2.2.2 trim方法

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
  <textarea name="" id="" cols="30" rows="10"></textarea>
  <script>
    const str = '           hello world        '
    console.log(str.trim())
    str.trim() // 去掉字符串左右的空格

    const tx = document.querySelector('textarea')
    tx.addEventListener('keyup', function(e) {
      if (e.key === 'Enter'){
        if (tx.value.trim() !== '') {
           console.log(123123)
        }
      }
    })
  </script>
</body>

</html>
```



## 4.环境对象

#### 1.定义

![image-20220722212243764](Web%20APIs%20%E7%AC%AC%E4%BA%8C%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E5%9F%BA%E7%A1%80.assets/image-20220722212243764.png)

#### 2.总结

![image-20220722212338865](Web%20APIs%20%E7%AC%AC%E4%BA%8C%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E5%9F%BA%E7%A1%80.assets/image-20220722212338865.png)

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
  <button>点击</button>
  <script>
    // 每个函数里面都有this, 代表了当前函数运行时所处的环境.
    function fn(){
      // this 就是环境对象, 是函数内部的特殊变量
      console.log(this)  // window
    }
    fn()  // 相当于window.fn()
    window.fn() 
    // 粗略规则: 谁调用, this指向谁 .
    // 指向 可以理解为 等于

    // 普通声明的函数, 都会挂载到window对象上  
    // (挂载:作为window的一个属性或方法)
    window.fn() 


    // 2. 绑定注册事件的时候, this 代表的是 注册事件的元素
    const btn = document.querySelector('button')

    // 点击的click 的时候, 相当于 btn按钮去调用执行这个函数
    btn.addEventListener('click', function(){
      // btn.style.color = 'orange'
      // console.log(this)
      this.style.color = 'orange'
      // this 当前的
    })

    // 3. 怎么判断this代码谁呢 ? 
    // 粗略规则 谁调用, this就指向谁

  </script>
</body>

</html>
```

## 5. 回调函数

### 1.定义

![image-20220722212620074](Web%20APIs%20%E7%AC%AC%E4%BA%8C%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E5%9F%BA%E7%A1%80.assets/image-20220722212620074.png)

### 2.总结

![image-20220722212638856](Web%20APIs%20%E7%AC%AC%E4%BA%8C%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E5%9F%BA%E7%A1%80.assets/image-20220722212638856.png)

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
    <button>点击</button>
<script>
    // 回调函数: 作为函数的参数, 一开始不执行, 回头再调用的函数.
    // callback  ==> 简写 cb
    
    // 应用场景

    // 1. 定时器
    const cb = function(){
        console.log('我就是回调函数')
    }
    // setInterval(cb, 1000)

    // 2. 事件监听
    const btn = document.querySelector('button')
    btn.addEventListener('click', cb)

    // 注意, 作为参数传入的时候, 一定不要加括号, 加了括号表示调用执行!!!

    
</script>
</body>
</html>
```

## 6.综合案例

#### 6.1Tab栏切换

![image-20220722212810815](Web%20APIs%20%E7%AC%AC%E4%BA%8C%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E5%9F%BA%E7%A1%80.assets/image-20220722212810815.png)

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
        <li><a class="active" href="javascript:;">精选</a></li>
        <li><a href="javascript:;">美食</a></li>
        <li><a href="javascript:;">百货</a></li>
        <li><a href="javascript:;">个护</a></li>
        <li><a href="javascript:;">预告</a></li>
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

    // 1. a 模块的制作
    // 1.1 获取所有的a元素
    const as = document.querySelectorAll('.tab-nav a')
    // const items = document.querySelectorAll('.item')
    console.log(as)
    // 1.2 循环遍历， 给每一个a标签绑定事件
    for (let i = 0; i < as.length; i++) {
      // 鼠标经过的事件 mouseenter
      as[i].addEventListener('mouseenter', function(){
        console.log(i)
        // 上边tab栏， 鼠标经过哪个a标签，给它添加active类名，高亮
        // 排他思想
        // 先干掉别人 移除active类
        document.querySelector('.tab-nav .active').classList.remove('active')
        // 显示自己  这里， this 表示 当前鼠标经过的那个a标签。
        console.log(this)
        this.classList.add('active')

        // 下面5个盒子 和上面的a标签 一一对应的。
        document.querySelector('.tab-content .active').classList.remove('active')
        // 对应索引号的那个 item 显示， 添加active类
        // items[i].classList.add('active')

        // 重点是 nth-child(1)
        // 找到对应a标签 索引号的那个item 方式二
        document.querySelector(`.item:nth-child(${i + 1})`).classList.add('active')
      })
    }


    // // for 循环 === 》 
    // as[0].addEventListener('mouseenter', function(){
    //     console.log(this)
    // })
    // as[1].addEventListener('mouseenter', function(){
    //     console.log(this)
    // })
    // as[2].addEventListener('mouseenter', function(){
    //     console.log(this)
    // })

  </script>
</body>

</html>
```

#### 6.2 全选文本框案例

![image-20220722212904763](Web%20APIs%20%E7%AC%AC%E4%BA%8C%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E5%9F%BA%E7%A1%80.assets/image-20220722212904763.png)

```html
<!DOCTYPE html>

<html>
  <head lang="en">
    <meta charset="UTF-8" />
    <title></title>
    <style>
      * {
        margin: 0;
        padding: 0;
      }

      table {
        border-collapse: collapse;
        border-spacing: 0;
        border: 1px solid #c0c0c0;
        width: 500px;
        margin: 100px auto;
        text-align: center;
      }

      th {
        background-color: #09c;
        font: bold 16px '微软雅黑';
        color: #fff;
        height: 24px;
      }

      td {
        border: 1px solid #d0d0d0;
        color: #404060;
        padding: 10px;
      }

      .allCheck {
        width: 80px;
      }
    </style>
  </head>

  <body>
    <table>
      <tr>
        <th class="allCheck">
          <input type="checkbox" name="" id="checkAll" />
          <span class="all">全选</span>
        </th>
        <th>商品</th>
        <th>商家</th>
        <th>价格</th>
      </tr>
      <tr>
        <td>
          <input type="checkbox" name="check" class="ck" />
        </td>
        <td>小米手机</td>
        <td>小米</td>
        <td>￥1999</td>
      </tr>
      <tr>
        <td>
          <input type="checkbox" name="check" class="ck" />
        </td>
        <td>小米净水器</td>
        <td>小米</td>
        <td>￥4999</td>
      </tr>
      <tr>
        <td>
          <input type="checkbox" name="check" class="ck" />
        </td>
        <td>小米电视</td>
        <td>小米</td>
        <td>￥5999</td>
      </tr>
    </table>
    <script>
      // 1.获取全选框
      const checkAll = document.querySelector('#checkAll')
      // 2.获取所有单选框
      const cks = document.querySelectorAll('.ck')
      // 3.点击全选复选框,单选也变化
      checkAll.addEventListener('click', function () {
        // 4.遍历所有单选框,让单选框  checked 等于全选框  checked
        for (let i = 0; i < cks.length; i++) {
          cks[i].checked = this.checked
        }
      })

      // 5.单选框控制全选框
      for (let i = 0; i < cks.length; i++) {
        // 给每个单选框,绑定点击事件
        cks[i].addEventListener('click', function () {
          /*
            判断每次点击时,
            选中的单选框个数,等于所有单选框个数
          */
          //  被选中的单选框
          const checkedCks = document.querySelectorAll('.ck:checked')
          console.log(checkedCks)
          if (checkedCks.length === cks.length) {
            checkAll.checked = true
          } else {
            checkAll.checked = false
          }
        })
      }
    </script>
      
  </body>
</html>

```

## 7.作业

PC地址：https://ks.wjx.top/vj/PqGxVQT.aspx



![image-20220722213129058](Web%20APIs%20%E7%AC%AC%E4%BA%8C%E5%A4%A9%20Dom%E4%BA%8B%E4%BB%B6%E5%9F%BA%E7%A1%80.assets/image-20220722213129058.png)