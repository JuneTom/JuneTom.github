# JavaScript 高级第一天 作用域&解构&箭头函数

## 一、作用域

作用域（scope）规定了变量能够被访问的“范围”，离开了这个“范围”变量便不能被访问， 

* 作用域分为：
  * 局部作用域
  * 全局作用域

### 1.局部作用域

局部作用域分为函数作用域和块作用域。

#### 1.1函数作用域：

![image-20220806183726451](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220806183726451.png)

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
        // 作用域: Scope  
        // 变量和函数的可访问范围. 即 作用域 控制着变量和函数的可见性 和 生命周期. 
        // 局部作用域
        // ES5以前, 局部作用域就是函数作用域
        // 在函数内部声明的变量, 只能在函数内部访问, 外部无法 直接 访问!

        // 可见性: 函数外部无法访问函数内部的变量
        // 生命周期: 函数执行完毕就销毁.

        function getSum(){
            // 函数作用域 局部作用域
            const num = 10
        }
        getSum()
        console.log(num)  // Error 函数外部无法访问函数内部的变量

    </script>
</body>
</html>
```



#### 1.2 块作用域：

![image-20220806183757046](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220806183757046.png)

注：开发中 `let` 和 `const` 经常不加区分的使用，如果担心某个值会不小被修改时，则只能使用 `const` 声明成常量。

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
        // 为什么需要块级作用域

        var temp = new Date()
        function fn(){
            var temp  // undefined
            console.log(temp)
            if(false) {
             temp = 'hello world'
            }
        }
        fn() // hello world

        // if , for 不是函数, 是语句!

        // var 声明的变量, 会提升到当前作用域的最顶层, 赋值没有提升
        // var 声明的变量, 不赋值, 初始为undefined


        // 3. 块级作用域
        // 定义: 使用 let 或者 const声明的变量, 在 {} 中会产生块级作用域
        var temp = new Date()
        function fn(){
            console.log(temp)

            if(false) {
             let temp = 'hello world'
            }
        }
        fn() 

        // 1. for,if 不是函数, 但是 {}, 能生成块级作用域
        // 2. var 声明的变量, 不会产生块级作用域
        // 3. let , const 不存在变量提升 


        // 相互不影响
        // for (let i = 0; i < 5; i++) {
        //     console.log(i)
        // }

        // for (let i = 0; i < 5; i++) {
        //     console.log(i)
        // }

        // if (true) {
        //     const i = 10
        // }
        // console.log(i)


        // let num = 10
        // window.num

        //==> var 声明的变量 会成为window对象的属性, let, const声明的不会
        // var num1 = 10
        // console.log(window.num1)

        let a1 = 10
        console.log(a1)
        console.log(window.a1)

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
    <button class="btn">click</button>
    <button class="btn">click</button>
    <button class="btn">click</button>
    <button class="btn">click</button>
    <button class="btn">click</button>
    <script>
        // for 不是函数, 是一个语句
        // var i;

        // for( i = 0; i < 5; i++) {
        //     console.log(i)
        // }
        // // 1 2 3 4  234 234 

        // console.log(i) // 5

        // for(let i = 0; i < 5; i++) {
        //     console.log(i)
        // }

        // console.log(i) // i is not defined

        

        // 0 - 4 给5个按钮绑定了点击事件 
        // for循环遍历绑定事件的时候, 函数没有执行, 回调函数
        // 当for循环执行完之后, i == > 5; 
        // 当我们去点击按钮的时候, for循环已经结束, i已经变为5;
        const btns = document.querySelectorAll('.btn')
        // var i;
        // for (var i = 0; i < 5; i++) {
        //     btns[i].addEventListener('click', function(){
        //         console.log(i)
        //     })
        // } 


        // 1. let 块级作用域  block块级作用域; 有点像闭包 closure 
        for (let i = 0; i < 5; i++) {
            btns[i].addEventListener('click', function(){
                console.log(i) // 0 1 2 3 4
            })
        } 
    </script>
</body>
</html>
```



#### 1.3 总结

1. 局部作用域分为哪两种？ 

   * 函数作用域 函数内部

   * 块级作用域 {} 

2. 局部作用域声明的变量外部能使用吗？
   * 不能

### 2.全局作用域

##### 2.1定义

![image-20220806184428001](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220806184428001.png)

##### 2.2总结

总结：

1. 为 `window` 对象动态添加的属性默认也是全局的，不推荐！
2. 函数中未使用任何关键字声明的变量为全局变量，不推荐！！！
3. 尽可能少的声明全局变量，防止全局变量被污染

JavaScript 中的作用域是程序被执行时的底层机制，了解这一机制有助于规范代码书写习惯，避免因作用域导致的语法错误。

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
        // 作用域: Scope  
        // 变量和函数的可访问范围. 即 作用域 控制着变量和函数的可见性 和 生命周期. 

        // 2. 全局作用域 
        // 直接写在script 或者js文件中的 代码, 属于全局作用域.
        // 可见性 : 全局做用域中声明的变量, 在代码任何地方都可以访问.
        // 生命周期: 关闭页面的时候结束.

        // Eg.举例
        // const num = 10  // 全局作用域中的变量, 
        // function fn () {
        //     // 函数内部可以访问
        //     console.log(num)
        // }
        // fn()

        // 不用任何关键字声明的变量, 会成为全局变量
        // function foo(){
        //     a = 10
        // }
        // foo() // 需要调用一下函数
        // console.log(a)

    </script>
</body>
</html>
```

### 3. 作用域链

##### 3.1定义

![image-20220806185806462](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220806185806462.png)

##### 3.2 总结

1. 作用域链本质是什么？ 
   * 作用域链本质上是底层的变量查找机制 

2. 作用域链查找的规则是什么？
   * 会优先查找当前函数作用域中查找变量
   * 查找不到则会依次逐级查找父级作用域直到全局作用域

3.嵌套关系的作用域串联起来形成了作用域链

4.相同作用域链中按着从小到大的规则查找变量

5.子作用域能够访问父作用域，父级作用域无法访问子级作用域

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
        // 全局作用域
        let a = 3 
        let b = 1
        function f(){
            // 局部作用域
            // let a = 1
            function g(){
                // 局部作用域
                a = 2
                console.log(a)
            }
            g() // 调用g
        }
        f() // 调用f

        // 作用域链: 本质就是底层变量的查找机制.
        // 查找规则
        // 1. 优先在当前作用域中查找变量
        // 2. 如果当前作用域找不到, 依次往上层作用域查找, 直到全局作用域
    </script>
</body>
</html>
```

### 4. JS垃圾回收机制

#### 4.1定义

- 垃圾回收机制(Garbage Collection) 简称 GC 
- **JS中内存的分配和回收都是自动完成的，内存在不使用的时候会被垃圾回收器自动回收。** 
- 正因为垃圾回收器的存在，许多人认为JS不用太关心内存管理的问题 
- 但如果不了解JS的内存管理机制，我们同样非常容易成内存泄漏（内存无法被回收）的情况 
- 不再用到的内存，没有及时释放，就叫做内存泄漏

**内存泄漏：不再用到的内存，没有及时释放**

#### 4.2内存的生命周期

JS环境中分配的内存, 一般有如下生命周期：

* **内存分配**：当我们声明变量、函数、对象的时候，系统会自动为他们分配内存 
*  **内存使用**：即读写内存，也就是使用变量、函数等 
* **内存回收**：使用完毕，由垃圾回收自动回收不再使用的内存 
*  说明： 
  *  **全局变量一般不会回收(关闭页面回收)；** 
  * **一般情况下局部变量的值, 不用了, 会被自动回收**

![image-20220806190519848](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220806190519848.png)

#### 4.3 垃圾回收算法说明

所谓垃圾回收, 核心思想就是如何判断内存是否已经不再会被使用了, 如果是, 就视为垃圾, 释放掉。 

下面介绍两种常见的浏览器垃圾回收算法: **引用计数法** 和 **标记清除法**

*  引用计数 
  * IE采用的引用计数算法, 定义“内存不再使用”的标准很简单，就是看一个对象是否有指向它的引用。
*  标记清除法 
  * 现代的浏览器已经不再使用引用计数算法了。 
  * 现代浏览器通用的大多是基于标记清除算法的某些改进算法，总体思想都是一致的。

##### 4.3.1引用计数 

 IE采用的引用计数算法, 定义“内存不再使用”的标准很简单，就是看一个对象是否有指向它的引用。 

算法：

* 跟踪记录每个值被引用的次数。
* 如果这个值的被引用了一次，那么就记录次数1
* 多次引用会累加。
* 如果减少一个引用就减1。
*  如果引用次数是0 ，则释放内存。

![image-20220806191543651](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220806191543651.png)

![image-20220806191553796](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220806191553796.png)

##### 4.3.2标记清除法 

现代的浏览器已经不再使用引用计数算法了。 

现代浏览器通用的大多是基于标记清除算法的某些改进算法，总体思想都是一致的。

核心：

* 标记清除算法将“不再使用的对象”定义为“无法达到的对象”。 
* 就是从根部（在JS中就是全局对象）出发定时扫描内存中的对象。 凡是能从根部到达的对象，都是还需要使用的。
* 那些无法由根部出发触及到的对象被标记为不再使用，稍后进 行回收。

**主要将GC的垃圾回收过程分为两个阶段**

- 标记阶段：把所有活动对象做上标记。
- 清除阶段：把没有标记（也就是非活动对象）销毁。

**标记阶段**

**根**可以理解成我们的全局作用域，GC从全局作用域的变量，沿作用域逐层往里遍历（对，是深度遍历），当遍历到堆中对象时，说明该对象被引用着，则打上一个标记，继续递归遍历（因为肯定存在堆中对象引用另一个堆中对象），直到遍历到最后一个（最深的一层作用域）节点。

![image-20220806191912183](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220806191912183.png)

**清除阶段**

​	**回收没有打上标记的对象**

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

        // function fn(){
        //     // 当函数执行完毕, 这个变量所占的内存空间会被 自动回收
        //     const str = 'hello'
        //     console.log(str)
        // }

        // fn() 
        

        // 垃圾回收机制  简称 GC
        // 内存在不使用的时候会被垃圾回收程序自动回收。（JS中内存的分配和闲置资源的回收都是自动完成的）

        // 内存泄漏: 不再用到的内存，没有及时释放

        // 内存的生命:
        // 1. 内存分配
        // 2. 内存使用
        // 3. 内存回收

        // 1. 引用计数
        let person = {
            age: 18,
            name: 'pink老师'
        }
        let p = person
        person = 1
        p = null

        // 引用计数缺陷：循环引用，无法回收; 造成内存泄漏

        // function problem () {
        //     // {}  ==》 new Object()
        //     let oA = {}
        //     let oB = {}
        //     oA.a = oB  //  oB被oA引用
        //     oB.a = oA  //  oA又被oB引用
        // }
        // problem()


    </script>
</body>
</html>
```

### 5.闭包

#### 5.1.定义

![image-20220806192314204](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220806192314204.png)

在 JavaScript 中，内部函数总是可以访问其外部函数中声明的变量，当通过调用一个外部函数返回一个内部函数后，即使该外部函数已经执行结束了，但是内部函数引用外部函数的变量依然保存在内存中，我们就把这些变量的集合称为闭包。比如外部函数是 foo，那么这些变量的集合就称为 foo 函数的闭包。

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

        // 定义 ： 内部函数引用外部函数的变量的集合
        // ==> 闭包 = 内层函数 + 外层函数的变量
        // 注意： 内层函数一定要引用外层函数的变量

        // 1. 首先要有内层函数
        // 2. 内层函数使用了外层函数的变量 

        // 简单的写法
        // closure 闭包
        function outer(){
            // 外层函数outer 把内存函数和这个被引用的变量 , 包起来.
            let a = 10
            function fn(){
                console.log(a)
            }
            fn()
        }
        outer()

        // scope 作用域  local 局部作用域 global 全局作用与 closure 闭包


    </script>
</body>
</html>
```



#### 5.2.作用

![image-20220806192411969](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220806192411969.png)

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
        // 闭包的常见形式
        // 作用: 通过闭包, 外部可以访问函数内部的变量
        // function outer(){
        //     let a = 10  // 局部变量
        //     function fn(){
        //         console.log(a)
        //     }
        //     // fn()
        //     return fn
        // }

        // // // outer() ===> fn  ==> fn(){console.log(a) }
        // const fun = outer()
        
        // fun() // 虽然看上去是外部函数, 本质上 还是调用了 fn() 这个函数

        // 1. 写法二
        function outer(){
            let a = 100  // 局部变量
            return function(){
                console.log(a)
            }
        }
        const fun = outer()

        fun()

        // function bar(){
        //     console.log(123)
        // }
        // bar()
        // // 函数调用, 都有返回值, 如果没有写return, 返回的是undefined
        // // 如果写了return , 就是return后面的那个值
    </script>
</body>
</html>
```







#### 5.3应用

![image-20220806193202562](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220806193202562.png)

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
        // 闭包的应用
        // 可以统计函数调用的次数

        // 普通的方式
        // let i = 0
        // function fn(){
        //     i++
        //     console.log(`函数调用了${i}多少次`)
        // }
        // fn()

        // 闭包的方式来写
        // 记录函数调用的次数, 外部不能修改这个i变量,但是可以访问.
        // 实现了数据的私有化 
        function count(){
            let i = 0 // 局部变量
            return function(){
                i++
                console.log(`函数调用了${i}多少次`)
            }
        }
        const fun = count()
        fun()
        // fun()

        // 引用计数
        // 标记清除

        // 闭包会产生的问题  : 内存泄漏
        // 1.本来 i 是函数内部的局部变量, 调用count()函数, 按理说, 应该释放这个i变量(内存)
        // 2.但是这里, 我们每次调用 fun() 都能访问到这个 i变量, i本来应该被释放, 而没被释放.
        // 所以会造成内存泄漏.
        //  (标记清除: 从全局作用域出发, 能访问到的变量都做上标记, 不回收) 

        // function bar(){
        //     const a = 1
        // }
        // bar()

        // 闭包应用 ：  节流， 防抖 (性能优化 ) 
        // 节流：throttle 减少事件的执行频率。 50ms 执行一次； 
        // 防抖：debounce 比如 点击按钮， 打印一句话。 500ms内，只让它触发一次。
        window.addEventListener('resize', function(){
            console.log(1)
        })
    </script>
</body>
</html>
```



#### 5.4总结

怎么理解闭包？

* 闭包 = 内层函数 + 外层函数的变量 

闭包的作用？

* 封闭数据，实现数据私有，外部也可以访问函数内部的变量

* 闭包很有用，因为它允许将函数与其所操作的某些数据（环境）关联起来 

闭包可能引起的问题？

* 内存泄漏

### 6.变量的提升

#### 6.1定义

JS初学者经常花很多时间才能习惯变量提升，还经常出现一些意想不到的bug，正因为如此，ES6 引入了块级作用域， 用let 或者 const声明变量，让代码写法更加规范和人性化。

![image-20220806193907037](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220806193907037.png)

#### 6.2总结

1. 用哪个关键字声明变量会有变量提升？ 
   * var 
2. 变量提升是什么流程？
   * 先把var 变量提升到当前作用域于最前面
   *  只提升变量声明， 不提升变量赋值
   * 然后依次执行代码 
   * 我们不建议使用var声明变量

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
    <script>

        // 1. var 声明的变量， 会提升到当前作用域的最顶层
        // 2. 只提升声明， 不提升赋值。
        var num
        console.log(num + '件')
        num = 10
        // var num
        // console.log(num + '件')
        // num = 10
        // console.log(num)

        function fn() {
            var num
            // 只提升到当前作用域的最前
            console.log(num)
            num = 10
        }
        fn()

    </script>
</body>
</html>
````

## 二、函数进阶

### 1.函数提升

#### 1.1定义

![image-20220807092853732](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220807092853732.png)

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
        // 定义函数有两种方式 
        // 1. function声明的函数， 会提升到当前作用域最顶层。

        // 声明式 
        // fn()
        // function fn(){
        //     console.log(123)
        // }

        // 表达式
        // 2. 用var声明的函数，会提升声明， 赋值不提升。
        var fn; // undefined
        fn()
        fn = function(){
            console.log(111)
        }
    </script>
</body>
</html>
```

###  2.函数参数

**函数参数的使用细节，能够提升函数应用的灵活度。**

#### 2.1动态参数

##### 2.1.1定义

![image-20220807093133188](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220807093133188.png)

##### 2.1.2总结

1. 当不确定传递多少个实参的时候，我们怎么办？
   * arguments 动态参数 
2. arguments是什么？ 
   * 伪数组 
   * 它只存在函数中

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

        // arguments 函数的动态参数

        // 1. 所有的函数都内置了（默认就存在，自带的）一个arguments对象
        // 2. arguments是一个伪数组， 存储了传递来的所有实参。
        // 3. 它只存在于函数中


        // function getSum(){
        //     console.log(arguments)
        //     let sum = 0 
        //     for (let i = 0; i < arguments.length; i++) {
        //         sum += arguments[i]
        //     }
        //     console.log(sum)
        // }
        // // getSum(1, 2, 3)
        // getSum(1, 2, 3, 4, 5)

        // 伪数组： 有length， 有索引号， 没有数组的pop， push一些方式， 可以遍历



    </script>
</body>
</html>
```



#### 2.2剩余参数

##### 2.2.1定义

![image-20220807093402129](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220807093402129.png)

##### 2.2.2语法

![image-20220807093730818](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220807093730818.png)

##### 2.2.3总结

1.剩余参数主要的使用场景是？ 

* 用于获取多余的实参 

2.剩余参数和动态参数区别是什么？开发中提倡使用哪一个？

- 动态参数是伪数组 
- 剩余参数是真数组 
- 开发中使用剩余参数想必也是极好的

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
        // rest参数， 剩余参数。 ES6新增。
        // 语法： ...变量
        // 1. rest剩余参数 是一个真实的数组， 存了剩余的实参
        // 2. 只能放到参数的最后一位。

        // function getSum(...arr) {
        //     console.log(arr)
        //     let sum = 0; 
        //     for (let i = 0; i < arr.length; i++) {
        //         sum += arr[i]
        //     }
        //     console.log(sum)
        // }
        // 不能写到参数的中间， 只能是最后一位
        // function getSum(a, b, ...arr ) {
        //     console.log(arr)
        // }
        
        // getSum(1, 2, 3, 4, 5)

        // 箭头函数的写法
        // 1. 箭头函数没有arguments动态参数， 但是有rest剩余参数。
        const getSum = (...arr) => {
            console.log(arr)
            let sum = 0; 
            for (let i = 0; i < arr.length; i++) {
                sum += arr[i]
            }
            console.log(sum)
        }

        getSum(1, 2, 3, 4, 5)


    </script>
</body>
</html>
```

##### 2.3.4展开运算符

![image-20220807094643964](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220807094643964.png)

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
        // 剩余参数， 剩余的参数列表放到数组里

        // spread 
        // 扩展运算符(...arr) 将一个数组进行展开, 变为参数列表
        // const arr = [1, 5, 3, 8, 2]
        // console.log(...arr)
        // 注意: 不会修改原数组

        // 主要应用 
        // 1. 求数组最大最小值
        const arr = [1, 3, 5, 9, 8]
        console.log(Math.max(...arr)) // Math.max() 接收的是参数列表
        console.log(Math.min(...arr))

        // 2. 合并数组
        const arr1 = [1, 2, 3]
        const arr2 = [5, 6, 7]

        const arr3 = [...arr1, ...arr2]
        console.log(arr3)
    </script>
</body>
</html>
```



##### 2.3.5展开运算符 or 剩余参数

![image-20220807094740348](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220807094740348.png)

##### 2.3.6总结

1.展开运算符主要的作用是？ 

* 可以把数组展开,可以利用求数组最大值以及合并数组等操作 

2.展开运算符和剩余参数有什么区别？

* 展开运算符主要是 数组展开 
* 剩余参数 在函数内部使用

### 3.箭头函数

#### 3.1定义

![image-20220807095140950](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220807095140950.png)

#### 3.2语法

##### 3.2.1基本写法

![image-20220807095324686](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220807095324686.png)

##### 3.2.2只有一个参数可以省略小括号

![image-20220807100022652](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220807100022652.png)

##### 3.2.3如果函数体只有一行代码，可以写到一行上，并且无需写 return 直接返回值

![image-20220807100045839](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220807100045839.png)

##### 3.2.4加括号的函数体返回对象字面量表达式

![image-20220807100114911](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220807100114911.png)

##### 3.2.5总结

![image-20220807100150688](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220807100150688.png)

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
        // 表达式的方式
        const fn = function(){
            console.log(1)
        }

        // 箭头函数 =>  来定义一个函数
        const fn1 = () => {
            console.log(1)
        }
        fn1()

        // 1. 传参 
        const fn2 = (x) => {
            console.log(x)
        }
        fn2(8)

        // 2. 只有一个形参的时候，可以省略小括号 ()
        const fn3 = x => {
            console.log(x)
        }
        fn3(9)

        // 3. 只有一行代码的时候， 可以省略花括号 {} 大括号   ()小   []中（方）  {} 大（花） 
        const fn4 = x => console.log(x)
        fn4(6)

        // 4. 只有一行代码的时候， 可以省略return
        const fn5_ = x => {
            return x + x 
        }
        const fn5 = x => x + x 
        console.log(fn5(6))

        // 5. 箭头函数可以直接返回一个对象， 但必须在对象外面加上小括号
        const fn6_ = (name) => {
            return {user_name : name}
        }
        const fn6 = name => ({user_name : name})

        console.log(fn6('周杰伦'))

    </script>
</body>
</html>
```

#### 3.3箭头函数

![image-20220807101716281](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220807101716281.png)

##### 3.3.1箭头函数参数

![image-20220807101727789](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220807101727789.png)

![image-20220807101739531](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220807101739531.png)

##### 3.3.2箭头函数this

![image-20220807101921306](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220807101921306.png)

![image-20220807101931798](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220807101931798.png)

![image-20220807101942848](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220807101942848.png)

![image-20220807101959792](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220807101959792.png)

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
    <button class="btn"></button>
    <script>
        // this指向， 谁调用， 指向谁。
        // this 在定义的时候，不能确定this的指向，执行的时候才能确定。 

        // 普通函数，定时器
        // function fn(){
        //     console.log(this)  // window
        // }
        // fn()  // window.fn()

        // setTimeout(function(){
        //     console.log(this)  // window
        // }, 1000);
        // window.setTimeout()

        // 对象调用， 谁调用， 指向谁
        const obj = {
            name:'xd',
            age:18,
            sayHi:function(){
                // console.log(this)  // obj
                console.log(this.name)
            }
        }
        obj.sayHi() 
        
        const btn = document.querySelector('.btn')
        btn.addEventListener('click', function(e){
            console.log(this) // 绑定事件的元素
            console.log(e.target) // 触发事件的元素 点的谁指向谁
            console.log(e.currentTarget)  // 绑定事件的元素， 同this
        })


        // 1. 箭头函数的this是上层作用域中的this  
        // const fn = () => {
        //     // this
        //     console.log(this)
        // }
        // fn()

        // 2. 对象里面不建议写箭头函数！ 
        const obj2 = {
            user:'xx',
            sayHi: () => {
                console.log(this)  // window
                // 箭头函数里没有this, 会向上层作用域中找this
            }
        } 
        obj2.sayHi()
    </script>
</body>
</html>
```

#### 3.4总结

![image-20220807102046391](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220807102046391.png)

## 三、解构赋值

**解构赋值是一种快速为变量赋值的简洁语法，本质上仍然是为变量赋值。**



### 1.数组解构

**数组解构是将数组的单元值快速批量赋值给一系列变量的简洁语法。**

#### 1.1基本语法：

1. 赋值运算符 = 左侧的 [] 用于批量声明变量，右侧数组的单元值将被赋值给左侧的变量
2. 变量的顺序对应数组单元值的位置依次进行赋值操作

![image-20220808193001163](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220808193001163.png)

#### 1.2典型应用交互2个变量

![image-20220808193107592](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220808193107592.png)

#### 1.3 js 前面必须加分号情况

![image-20220808193130235](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220808193130235.png)



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
      // ES5 为变量赋值，只能直接指定值
      // let a = 1
      // let b = 1
      // let c = 1

      // ES6 解构赋值
      let [a, b, c] = [1, 2, 3]
      console.log(a, b, c) // 从数组中提取值，按照对应的位置，对变量赋值
      const arr = [100, 60, 80]
      const [max, min, avg] = arr
      console.log(max, min, avg) // 交换两个变量

      let e = 4
      let f = 8 // ES6 解构赋值 交换两个变量
      ;[f, e] = [e, f]
      console.log(e, f) // 注意 [] 前面需要加分号; // 需要加分号的情况 // 1.() 立即执行函数 // 2.[] 数组 // 得到一个新数组，新数组的元素的平方
      const arr1 = [1, 2, 3]
      const res = arr1.map((x) => x * x)
      console.log(res) // const res = arr1.map(function(x) { //     return x * x // }) // console.log(res)
      ;[1, 2, 3].forEach((item) => {
        console.log(item)
      })
    </script>
  </body>
</html>

```

#### 1.4解构赋值细节

![image-20220808193936986](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220808193936986.png)

![image-20220808193947082](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220808193947082.png)

![image-20220808193957087](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220808193957087-16599587978191.png)

![image-20220808194009163](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220808194009163.png)

![image-20220808194016538](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220808194016538.png)

![image-20220808194025600](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220808194025600.png)

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
      // 1.变量多，数组元素很少
      // const [a, b, c, d] = [1, 2, 3]  // d undefined
      // console.log(a, b, c, d)

      // 2.变量少，数组元素多
      // const [a, b] = [1, 2, 3, 4, 5]
      // console.log(a, b)

      // 3.变量少， 数组元素多，可以利用剩余参数接收多余的元素
      // const [a, b, ...c] = [1, 2, 3, 4, 5]
      // console.log(a, b, c)

      // 4.按照对应的位置， 依次对变量赋值
      // const [a, b, , d] = [1, 2, 3, 4]
      // console.log(a, b, d)

      // 5.解构赋值允许指定默认值
      // const [a = 0, b = 0] = [1, 2]
      // console.log(a, b)

      // 当数组对应位置不存在 或者 严格等于undefined时，默认值才生效
      // const [a = 0, b = 0] = []

      // 引号包起来的都是字符串 ==> '1'  'null'
      const [a = 0, b = 1] = ['undefined', undefined]
      console.log(a) // undefined
      console.log(b) // 1
      // 6.如果等号右边不是数组（不可遍历数组的结构），那么会报错
      // let [foo] = 1
      // let [foo] = false
      // let [foo] = NaN
      // let [foo] = null
      // let [foo] = undefined
      // let [foo] = {}
      //1. 变量的数量大于单元值数量时，多余的变量将被赋值为？
	  // undefined
	  //2. 变量的数量小于单元值数量时，可以通过什么剩余获取所有的值？
	  // 剩余参数... 获取剩余单元值，但只能置于最末位
  
    </script>
  </body>
</html>

```

#### 1.5多维数组

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
      // 多维数组： 数组嵌套数组
      const arr = [1, 2, [3, 4]] // 二维数组
      console.log([arr[2]])
      console.log(arr[2][0])
      console.log(arr[2][1]) // 多维数组的解析

      const arr1 = [1, 2, [3, 4]] // const [a, b, c] = arr1 // console.log(a, b, c)
      const [a, b, [c, d]] = [1, 2, [3, 4]]
      console.log(a, b, c, d)
    </script>
  </body>
</html>

```

#### 1.6总结

![image-20220808193359793](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220808193359793.png)

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
      // 本质上, 解构赋值的写法属于模式匹配, 只要等号两边的模式相同
      // 左边的变量就会被赋予对应的值
      let [foo, [[bar], baz]] = [1, [[2], 3]]
      console.log(foo, bar, baz)

      let [, , third] = ['foo', 'bar', 'baz']
      console.log(third)

      // let [x, , y] = [1, 2, 3]
      // console.log(x, y)

      let [head, ...tail] = [1, 2, 3, 4]
      console.log(head, tail)

      let [x, y, ...z] = ['a']
      console.log(x) // 'a'
      console.log(y) // undefined
      console.log(z) // []

      let [fn] = [] //
      console.log(fn) // undefined
      let [fn1, fn2] = [1]
      console.log(fn1, fn2) // 1, undefined
    </script>
  </body>
</html>

```

#### 1.7练习(独立完成数组解构赋值)

![image-20220808193655890](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220808193655890.png)

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
      const pc = ['惠普', '联想', '苹果', '小米']
      const [hp, lx, ap, mi] = pc
      console.log(hp, lx, ap, mi)

      function getValue() {
        return [100, 60]
      }
      const [max, min] = getValue()
      console.log(max, min)
    </script>
  </body>
</html>

```



### 2.对象解构

**对象解构是将对象属性和方法快速批量赋值给一系列变量的简洁语法**

#### 2.1. 基本语法

1. 赋值运算符 = 左侧的 {} 用于批量声明变量，右侧对象的属性值将被赋值给左侧的变量 
1.  对象属性的值将被赋值给与属性名相同的变量 
1.  注意解构的变量名不要和外面的变量名冲突否则报错 
1. 对象中找不到与变量名一致的属性时变量值为 undefined

![image-20220808194243907](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220808194243907.png)

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
        const obj = {
            uname:'周杰伦',
            age: 18
        }
        // obj.uname 
        // obj.age

        // >>> 数组的解构 按着位置依次赋值  []

        // 对象的解构, 是按着属性名解构， 可以交换位置。

        //==> 要求变量名必须和属性名一致才可以解构
        const {age, uname} = { uname:'周杰伦', age: 18 }
        
        // 等价于 const age = obj.age
        console.log(uname, age)

    </script>
</body>
</html>
```



#### 2.2给新的变量名赋值：

 可以从一个对象中提取变量并同时修改新的变量名

![image-20220808194311520](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220808194311520.png)

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
        // 1. 对象的解构赋值， 可以重新命名
        // 旧变量名: 新变量名

        // const {uname:username, age} = {uname:'周杰伦', age: 18}

        // console.log(username, age)

        // const obj = {first:'Hello', last: 'world'}
        // const {first: f, last: l} = obj
        
        // console.log(f, l )

        // 结论: 
        // 对象解构的内部机制, 是先找到同名属性
        // 然后再赋值给对应的变量, 真正被赋值的是冒号后面那个.

        // 2. 解构数组对象
        // const pig = [
        //     {
        //         uname:'佩奇',
        //         age: 6
        //     }
        // ]
        // const [{uname, age}] = pig

        // console.log(uname, age)
        

        // 练习 
        // 1. 
        const pig = {name:'佩奇', age: 6}
        // const {name, age} = pig
        console.log(name, age)
        // 2. 
        const {name:uname, age} = pig
        // 3. 
        const goods = [{
            goodsName:'小米',
            price: 1999
        }]
        const [{goodsName, price}] = goods

        </script>
</body>
</html>
```



#### 2.3数组对象解构

![image-20220808194401807](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220808194401807.png)

#### 2.4练习

![image-20220808194426311](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220808194426311.png)

```js
 		<script>
 		// 练习 
        // 1. 
        const pig = {name:'佩奇', age: 6}
        // const {name, age} = pig
        console.log(name, age)
        // 2. 
        const {name:uname, age} = pig
        // 3. 
        const goods = [{
            goodsName:'小米',
            price: 1999
        }]
        const [{goodsName, price}] = goods

        </script>
```

#### 2.5 多级对象解构

![image-20220808201454521](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220808201454521.png)

![image-20220808201544018](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220808201544018.png)

![image-20220808201552916](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220808201552916.png)

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
        // const pig = {
        //     name: '佩奇',
        //     family: {
        //         mother: '猪妈妈',
        //         father: '猪爸爸',
        //         sister: '乔治'
        //     },
        //     age: 6
        // }

        // 多级对象的解构
        // name , mother, father, sister
        // const {name, family} = pig  // 单独解构family
        // console.log(name, family)
        // const {name, family:{mother, father, sister}} = pig
        // console.log(family)
        // console.log(name,mother, father, sister)



        // 思考 2
        const pig = [{
            name: '佩奇',
            family: {
                mother: '猪妈妈',
                father: '猪爸爸',
                sister: '乔治'
            },
            age: 6
        }]

        // 冒号左边的family不是解构， 是模式匹配， 匹配到pig里面family。
        const [{name, family:{mother, father, sister}}] = pig


    </script>
</body>
</html>
```



#### 2.6多级对象解构案例

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
    // 1. 这是后台传递过来的数据
    const msg = {
      "code": 200,
      "msg": "获取新闻列表成功",
      "data": [
        {
          "id": 1,
          "title": "5G商用自己，三大运用商收入下降",
          "count": 58
        },
        {
          "id": 2,
          "title": "国际媒体头条速览",
          "count": 56
        },
        {
          "id": 3,
          "title": "乌克兰和俄罗斯持续冲突",
          "count": 1669
        },

      ]
    }

    // 需求1： 请将以上msg对象  采用对象解构的方式 只选出  data 方面后面使用渲染页面
    const { data } = msg
    console.log(data)

    // 需求2： 上面msg是后台传递过来的数据，我们需要把data选出当做参数传递给 函数
    function render({ data }) {
      // 我们只要 data 数据
      // 内部处理
      console.log(data)
    }
    render(msg)

    // 需求3， 为了防止msg里面的data名字混淆，要求渲染函数里面的数据名改为 myData
    function render({ data: myData }) {
      // 要求将 获取过来的 data数据 更名为 myData
      // 内部处理
      console.log(myData);
    }
    render(msg)


  </script>
</body>

</html>
```

#### 2.7渲染商品列表案例

![image-20220808201750923](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220808201750923.png)

![image-20220808201743142](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220808201743142.png)

![image-20220808201717193](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220808201717193.png)

![image-20220808201726636](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220808201726636.png)

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>商品渲染</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    .list {
      width: 990px;
      margin: 0 auto;
      display: flex;
      flex-wrap: wrap;
      padding-top: 100px;
    }

    .item {
      width: 240px;
      margin-left: 10px;
      padding: 20px 30px;
      transition: all .5s;
      margin-bottom: 20px;
    }

    .item:nth-child(4n) {
      margin-left: 0;
    }

    .item:hover {
      box-shadow: 0px 0px 5px rgba(0, 0, 0, 0.2);
      transform: translate3d(0, -4px, 0);
      cursor: pointer;
    }

    .item img {
      width: 100%;
    }

    .item .name {
      font-size: 18px;
      margin-bottom: 10px;
      color: #666;
    }

    .item .price {
      font-size: 22px;
      color: firebrick;
    }

    .item .price::before {
      content: "¥";
      font-size: 14px;
    }
  </style>
</head>

<body>
  <div class="list">
    <!-- <div class="item">
      <img src="" alt="">
      <p class="name"></p>
      <p class="price"></p>
    </div> -->
  </div>
  <script>
    const goodsList = [
      {
        id: '4001172',
        name: '称心如意手摇咖啡磨豆机咖啡豆研磨机',
        price: '289.00',
        picture: 'https://yanxuan-item.nosdn.127.net/84a59ff9c58a77032564e61f716846d6.jpg',
      },
      {
        id: '4001594',
        name: '日式黑陶功夫茶组双侧把茶具礼盒装',
        price: '288.00',
        picture: 'https://yanxuan-item.nosdn.127.net/3346b7b92f9563c7a7e24c7ead883f18.jpg',
      },
      {
        id: '4001009',
        name: '竹制干泡茶盘正方形沥水茶台品茶盘',
        price: '109.00',
        picture: 'https://yanxuan-item.nosdn.127.net/2d942d6bc94f1e230763e1a5a3b379e1.png',
      },
      {
        id: '4001874',
        name: '古法温酒汝瓷酒具套装白酒杯莲花温酒器',
        price: '488.00',
        picture: 'https://yanxuan-item.nosdn.127.net/44e51622800e4fceb6bee8e616da85fd.png',
      },
      {
        id: '4001649',
        name: '大师监制龙泉青瓷茶叶罐',
        price: '139.00',
        picture: 'https://yanxuan-item.nosdn.127.net/4356c9fc150753775fe56b465314f1eb.png',
      },
      {
        id: '3997185',
        name: '与众不同的口感汝瓷白酒杯套组1壶4杯',
        price: '108.00',
        picture: 'https://yanxuan-item.nosdn.127.net/8e21c794dfd3a4e8573273ddae50bce2.jpg',
      },
      {
        id: '3997403',
        name: '手工吹制更厚实白酒杯壶套装6壶6杯',
        price: '99.00',
        picture: 'https://yanxuan-item.nosdn.127.net/af2371a65f60bce152a61fc22745ff3f.jpg',
      },
      {
        id: '3998274',
        name: '德国百年工艺高端水晶玻璃红酒杯2支装',
        price: '139.00',
        picture: 'https://yanxuan-item.nosdn.127.net/8896b897b3ec6639bbd1134d66b9715c.jpg',
      },
    ]

    // // 字符串拼接  声明一个字符串变量
    // let str = ''

    // // 2.遍历数据
    // goodsList.forEach(item => {
    //   const { picture, name, price } = item
    //   str += `
    //   <div class="item">
    //   <img src="${picture}" alt="">
    //   <p class="name">${name}</p>
    //   <p class="price">${price}</p>
    // </div>
    // `
    // })

    // // 3.把生成的字符串  添加给list
    // document.querySelector('.list').innerHTML = str


    // 方法2:map方式渲染
    const list = document.querySelector('.list')
    // map方法返回一个数组,同时map一般要写return
    const res = goodsList.map(({ picture, name, price }) => {
      return `
      <div class="item">
      <img src="${picture}" alt="">
      <p class="name">${name}</p>
      <p class="price">${price}</p>
    </div>
    `
    })

    // 数组转换成字符串    arr.join('')
    list.innerHTML = res.join('')
  </script>
</body>

</html>
```

## 四、综合案例(商品列表价格筛选)

![image-20220808202053485](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220808202053485.png)

### 1.Filer()

![image-20220808202107165](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220808202107165.png)

![image-20220808202116634](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220808202116634.png)

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
        // Array.filter()  filter 筛选,过滤的意思
        // 创建一个新的数组, 新数组的元素是 通过筛选后的元素

        // filter() 接收一个函数作为参数, 一般需要写return 返回true或者false
        // true: 表示通过测试, 保留当前元素, false, 不保留;

        // 函数的第一个参数  当前处理的元素  item
        // 函数的第二个参数  当前处理的元素的索引号 index, 可选

        // 返回值, 一个新的数组, 由通过测试的元素组成.

        const arr = [10, 20, 30, 40]

        const newArr = arr.filter(function(item){
            console.log(item)
            return item >= 20 
        })
        console.log(arr)
        console.log(newArr)

        // 改写成箭头函数
        const newArr2 = arr.filter(x => x > 10)
        console.log(newArr2)


    </script>
</body>
</html>
```

### 2.案例实战

![image-20220808202150528](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220808202150528.png)

![image-20220808202159485](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220808202159485.png)

![image-20220808202207431](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220808202207431.png)

![image-20220808202215019](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220808202215019.png)

```html
<body>
  <div class="filter">
    <a data-index="1" href="javascript:;">0-100元</a>
    <a data-index="2" href="javascript:;">100-300元</a>
    <a data-index="3" href="javascript:;">300元以上</a>
    <a href="javascript:;">全部区间</a>
  </div>
  <div class="list">
    <!-- <div class="item">
      <img src="" alt="">
      <p class="name"></p>
      <p class="price"></p>
    </div> -->
  </div>
  <script>
    // 2. 初始化数据
    const goodsList = [
      {
        id: '4001172',
        name: '称心如意手摇咖啡磨豆机咖啡豆研磨机',
        price: '289.00',
        picture: 'https://yanxuan-item.nosdn.127.net/84a59ff9c58a77032564e61f716846d6.jpg',
      },
      {
        id: '4001594',
        name: '日式黑陶功夫茶组双侧把茶具礼盒装',
        price: '288.00',
        picture: 'https://yanxuan-item.nosdn.127.net/3346b7b92f9563c7a7e24c7ead883f18.jpg',
      },
      {
        id: '4001009',
        name: '竹制干泡茶盘正方形沥水茶台品茶盘',
        price: '109.00',
        picture: 'https://yanxuan-item.nosdn.127.net/2d942d6bc94f1e230763e1a5a3b379e1.png',
      },
      {
        id: '4001874',
        name: '古法温酒汝瓷酒具套装白酒杯莲花温酒器',
        price: '488.00',
        picture: 'https://yanxuan-item.nosdn.127.net/44e51622800e4fceb6bee8e616da85fd.png',
      },
      {
        id: '4001649',
        name: '大师监制龙泉青瓷茶叶罐',
        price: '139.00',
        picture: 'https://yanxuan-item.nosdn.127.net/4356c9fc150753775fe56b465314f1eb.png',
      },
      {
        id: '3997185',
        name: '与众不同的口感汝瓷白酒杯套组1壶4杯',
        price: '108.00',
        picture: 'https://yanxuan-item.nosdn.127.net/8e21c794dfd3a4e8573273ddae50bce2.jpg',
      },
      {
        id: '3997403',
        name: '手工吹制更厚实白酒杯壶套装6壶6杯',
        price: '99.00',
        picture: 'https://yanxuan-item.nosdn.127.net/af2371a65f60bce152a61fc22745ff3f.jpg',
      },
      {
        id: '3998274',
        name: '德国百年工艺高端水晶玻璃红酒杯2支装',
        price: '139.00',
        picture: 'https://yanxuan-item.nosdn.127.net/8896b897b3ec6639bbd1134d66b9715c.jpg',
      },
    ]

    // 1.封装一个render函数

    function render(arr) {
      let str = ''
      // 1.forEach  字符串拼接
      arr.forEach(item => {
        const { name, price, picture } = item
        str += `<div class="item">
      <img src="${picture}" alt="">
      <p class="name">${name}</p>
      <p class="price">${price}</p>
    </div>`
      })
      document.querySelector('.list').innerHTML = str

      // 2.map 数组转字符串
      //   const res = arr.map(item => {
      //     const { name, price, picture } = item
      //     return `<div class="item">
      //   <img src="${picture}" alt="">
      //   <p class="name">${name}</p>
      //   <p class="price">${price}</p>
      // </div>`
      //   })
      //   document.querySelector('.list').innerHTML=res.join('')

      // 渲染
    }

    render(goodsList)


    // 绑定点击事件
    const filter = document.querySelector('.filter')
    filter.addEventListener('click', function (e) {
      // e.target.tagName  判断点击的是a标签
      // e.target.dataset.index   判断点击的哪个a标签
      console.dir(e.target)  //dir  打印一个对象的所有属性和方法
      const { tagName, dataset } = e.target
      if (tagName === 'A') {

        let arr = []

        // 1.  if else 方法
        // if (dataset.index == '1') {
        //   arr = goodsList.filter(item => item.price > 0 && item.price <= 100)
        // } else if (dataset.index == '2') {
        //   arr = goodsList.filter(item => item.price > 100 && item.price <= 300)
        // } else if (dataset.index == '3') {
        //   arr = goodsList.filter(item => item.price > 300)
        // } else {
        //   arr = goodsList
        // }


        // 2. switch 方法
        switch (dataset.index) {
          case'1':
            arr = goodsList.filter(item => item.price > 0 && item.price <= 100)
            break;
          case '2':
            arr = goodsList.filter(item => item.price > 100 && item.price <= 300)
            break;
          case '3':
            arr = goodsList.filter(item => item.price > 300)
            break;
          default:
            arr = goodsList
            break;
        }
        // 渲染页面
        render(arr)
      }
    })
  </script>
</body>
```

## 五、作业

 PC端地址： https://ks.wjx.top/vj/wOeHuEk.aspx

![image-20220808202329907](JavaScript%E9%AB%98%E7%BA%A7%E7%AC%AC%E4%B8%80%E5%A4%A9%E4%BD%9C%E7%94%A8%E5%9F%9F&%E8%A7%A3%E6%9E%84&%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.assets/image-20220808202329907.png)
