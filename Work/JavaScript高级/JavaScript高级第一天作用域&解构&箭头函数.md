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

