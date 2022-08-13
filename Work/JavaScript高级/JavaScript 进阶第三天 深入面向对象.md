# JavaScript 进阶第三天 深入面向对象

## 一、 编程思想

### 1.1 面向过程（POP）

**面向过程编程： Process-oriented Programming , 以过程为核心，强调事件的流程、顺序，如：C语言。**

![image-20220811191053785](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%B7%B1%E5%85%A5%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1.assets/image-20220811191053785.png)

### 1.2 面向对象（OOP）

**面向对象编程：Object-oriented Programming , 以对象为核心，强调事件的角色、主体，如：C++、Java。**

![image-20220811190703809](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%B7%B1%E5%85%A5%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1.assets/image-20220811190703809.png)

### 1.3 如何把大象装进冰箱

#### 1.3.1 面向过程

```js
为了把大象装进冰箱，需要3个过程。

1) 把冰箱门打开（得到打开门的冰箱）

2) 把大象装进去（得到打开着门的, 装着大象的冰箱）

3) 把冰箱门关上（打开门、装好大象后，获得关好门的冰箱）

每个过程有一个阶段性的目标，依次完成这些过程，就能把大象装进冰箱。

面向过程像是我们站在上帝视角, 为万物指定命运的轨迹……Copy to clipboardErrorCopied
```

#### 1.3.2 面向对象

```js
// 每个动作有一个执行者，它就是对象。
// 也就是谁(对象), 要做什么

为了把大象装进冰箱，对于冰箱这个对象来说, 需要做三个动作（或者叫行为）。

1) 冰箱，你给我把门打开

2) 冰箱，你给我把大象装进去（或者说，大象，你给我钻到冰箱里去） (大象, 滚进去~~~)

3) 冰箱，你给我把门关上  (大象,你帮我把冰箱门带上)

依次做这些动作，就能把大象装进冰箱。

冰箱.开门()
冰箱.装进(大象)
冰箱.关门()

===> 冰箱.开门().装进(大象).关门()

大象:吹个空调我容易么?

 // 求大象的心理阴影面积? 用面向对象的方式怎么写?
 大象.阴影面积()Copy to clipboardErrorCopied
```

**面向对象和面向过程不是互斥的, 也就是说, 面向对象的编程中, 也可以有面向过程的思想.**

比如求大象的心理阴影这个方法中, 是不是要计算长宽, 这样类似的步骤~~. 先计算长, 再计算宽, 再求和. 这是面向过程编程.

![image-20220811190640915](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%B7%B1%E5%85%A5%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1.assets/image-20220811190640915.png)

### 1.4 类

面向对象更贴近我们的实际生活, 可以使用面向对象来描述现实世界事物, 但是事物又分为具体的事物和抽象的事物.

比如, 手机, 就是一个大类 , 抽象的 泛指的. 汽车, 也是一个类.

比如, 小米手机, 苹果手机. 算是类还是对象? 宝马, 奔驰 算是类还是对象?

具体的 ,比如小米某个型号的手机, 是对象了吧? 但是, 这个型号的手机生产了100w台.

再具体点, 我手上的这台小米手机. 具体的一个对象.

#### 什么是类?

**类是用于创建对象的模板。**

它描述一类对象的行为和状态。(方法和属性)

比如, 中秋吃月饼, 月饼上都有一些图案花纹, 具有相同花纹的月饼, 都是 同一个月饼模具压出来的.. 那这个模具, 就相当是月饼的一个类. 用它压出来的月饼, 都具有相同的花纹.

#### 什么是对象

**对象是属性和方法的集合**

#### 面向对象思维

1. 抽取(抽象) 对象共有的属性和方法封装成一个模板 (类).
2. 用类实例化一个对象 (用这个类作为模板创建一个具有它的属性和方法的对象, 可以创建很多个对象)

### 1.5 面向对象的三大特征

![image-20220811190559363](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%B7%B1%E5%85%A5%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1.assets/image-20220811190559363.png)

1. **封装** : 封装是指隐藏对象的属性和实现细节，仅对外提供公共访问方式。(抽取公共的属性方法)
2. **继承** : 继承可以使得子类具有父类的属性和方法. 或者重新定义、追加属性和方法等。
3. **多态** : 属于同一个父类的实例对象，调用同一个方法，出来不同的效果，就是多态

#### 1.5.1 封装

我们程序设计追求“高内聚，低耦合”

高内聚：类的内部数据操作细节自己完成，不允许外部干涉

低耦合：仅对外暴露少量的方法用于使用。

隐藏对象内部的复杂性，只对外公开简单的接口。便于外界调用，从而提高系统的可扩展性、可维护性。通俗的说，把该隐藏的隐藏起来，该暴露的暴露岀来。这就是封装性的设计思想。

```js
// 构造函数 封装了人的姓名, 年龄, 打招呼等.
function Person(name, age){
    this.name = name
    this.age = age
    this.sayHi = function(){
        console.log('你好哇~ nice to meet u')
    }
}
var p1 = new Person('小张', 18)Copy to clipboardErrorCopied
```

#### 1.5.2 继承

**继承** : 继承可以使得子类具有父类的属性和方法. 或者重新定义、追加属性和方法等。

#### 1.5.2 多态

**多态**：属于同一个父类的实例对象，调用同一个方法，出来不同的效果，就是多态。

比如, 手机都有开机这个行为, 小米手机的开机动画是小米logo, 苹果手机开机动画是苹果logo..面向对象介绍



## 二、构造函数

### 1.定义

![image-20220811191156881](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%B7%B1%E5%85%A5%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1.assets/image-20220811191156881.png)

### 2.构造函数的问题

![image-20220811191207429](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%B7%B1%E5%85%A5%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1.assets/image-20220811191207429.png)

![image-20220811191219459](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%B7%B1%E5%85%A5%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1.assets/image-20220811191219459.png)

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
        // 构造函数的问题
        // 存在浪费内存的问题
        // 公共方法：   每实例化一个对象，就会在堆内存中开辟一个新的空间储存方法
        
        function Star(name, age) {
            this.name = name 
            this.age = age 
            this.sing = function () {
                console.log('Sing');
            } 
        }

        const ldh = new Star('刘德华', 19)
        const zjl = new Star('周杰伦', 18)
        console.log(ldh.sing === zjl.sing)      /false

        // 我们常说的指向 / 指针
        // 表示内存里存的是地址（指针） （理解为门牌号，房间号），这个地址指向了内存中数据的真实位置
    </script>
</body>
</html>
```

### 3.总结

![image-20220811191343097](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%B7%B1%E5%85%A5%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1.assets/image-20220811191343097.png)

### 4.引入原型解决

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
    // 1.公共的属性，  写在构造函数里面
        function Star(name, age) {
            this.name = name 
            this.age = age 
            // this.sing = function () {
            //     console.log('Sing');
            // } 
        }

    // 2.公共的方法写在原型对象上， 节约了内存
    Star.prototype.sing = function(){
        console.log('Sing');
    }

    const ldh = new Star('刘德华', 19)
    const zjl = new Star('周杰伦', 18)
    console.log(ldh.sing === zjl.sing)      //true
    </script>
</body>
</html>
```



## 三、原型

### 1.原型

#### 1.1定义

![image-20220811191423715](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%B7%B1%E5%85%A5%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1.assets/image-20220811191423715.png)



#### 1.2总结

![image-20220811191439615](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%B7%B1%E5%85%A5%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1.assets/image-20220811191439615.png)



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
        /* 
            原型 ： 字面意思 原始的模型 原始祖先
            JS里 ： 原型就是一个对象，也叫原型对象
            原型对象 ： prototype
        */

        //   1. 所有的函数， 都有一个prototype属性（显示原型）， 这个属性是一个指针， 指向了原型对象
        function Person() {}
        //   dir : 查看一个对象的所有属性和方法
        console.dir(Person)

        //    2. 原型对象默认有一个constructor的属性， 指向了这个构造函数本身
        console.log(Person.prototype.constructor === Person)

        //    Person.prototype 是一个对象

        //    3. 我们可以往这个原型对象上添加属性和方法
        //    所有通过构造函数创建的实例，都共享原型对象上包含的属性和方法

        function Star(name, age) {
            //  公共属性写在构造函数里
            this.name = name 
            this.age = age 
        }

        //  公共方法写在原型上， 节约内存
        Star.prototype.sing = function(){
            console.log('Sing');
        }

        //  原型上也可以添加属性
        Star.prototype.cheer = 'Every step count!'      //  每天进步一点点

        const ldh = new Star('刘德华', 19)
        const zjl = new Star('周杰伦', 18)
        console.log(ldh)

        console.log(ldh.__proto__ === Star.prototype)   //  它们都指向原型对象

       /*  
            Array.prototype.reduce()
            const arr =[1, 2, 3]
            const arr = new Array(1, 2, 3)
            Array   是数组的构造函数，Array.prototype 是数组的原型
            arr.reduce()
            arr.map 
        */
</script>
</body>
</html>
```



#### 1.3原型- this指向

**构造函数和原型对象中的this 都指向 实例化的对象**

![image-20220811191554806](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%B7%B1%E5%85%A5%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1.assets/image-20220811191554806.png)

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
        /* 
            new的执行机制
            1. 在构造函数内创建一个空对象
            2. 让this指向这个空对象
            3. 执行构造函数里面的代码， 给这个对象添加属性和方法
            4. 返回这个对象（return this)
        */

        let that    //     全局变量 
        function Star() {
            this.name = name 
            that = this     // 执行构造函数的时候，把this保存起来， 赋值给that
            console.log(this)
        }

        // const ldh  = new Star('刘德华')
        console.log(that)

        Star.prototype.sing = function(){
            console.log('Sing')
            thst = this
        }
        const ldh  = new Star('刘德华')
        ldh.sing()  // 谁调用， 指向谁
        console.log(that === ldh)   //true

        // 结论
        // 1. 构造函数里面的this， 指向的是实例（对象）
        // 2. 原型对象方法里面的this， 指向的还是实例（对象）

    </script>
</body>
</html>
```

#### 1.4练习

![image-20220811191915144](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%B7%B1%E5%85%A5%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1.assets/image-20220811191915144.png)

```js
// 自己定义 数组扩展方法  求和 和 最大值 
// 1. 我们定义的这个方法，任何一个数组实例对象都可以使用
// 2. 自定义的方法写到  数组.prototype 身上
// 1. 最大值
const arr = [1, 2, 3]
Array.prototype.max = function () {
  // 展开运算符
  return Math.max(...this)
  // 原型函数里面的this 指向谁？ 实例对象 arr
}
// 2. 最小值
Array.prototype.min = function () {
  // 展开运算符
  return Math.min(...this)
  // 原型函数里面的this 指向谁？ 实例对象 arr
}
console.log(arr.max())
console.log([2, 5, 9].max())
console.log(arr.min())
// const arr = new Array(1, 2)
// console.log(arr)
// 3. 求和 方法 
Array.prototype.sum = function () {
  return this.reduce((prev, item) => prev + item, 0)
}
console.log([1, 2, 3].sum())
console.log([11, 21, 31].sum())

```

### 2.constructor 属性

#### 2.1定义

![image-20220811192022281](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%B7%B1%E5%85%A5%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1.assets/image-20220811192022281.png)

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
        // constructor 构造函数

        function Star(name, age) {
            this.name = name
            this.age = age
        }

        const ldh = new Star('刘德华', 18)  // 构造函数
        console.dir(Star)                  // 原型
        
        // 每个原型（对象）都有一个constructor属性， 指向构造函数本身
        // 表示我， 我这个原型， 和那个构造函数向关联， 是那个构造函数的原型

        // constructor 在原型上， 在Star.prototype上
        console.log(Star.prototype.constructor === Star)  //true
        ldh.__proto__ === Star.prototype                  //===>都指向原型
    </script>
</body>
</html>
```



#### 2.2使用场景

![image-20220811192056869](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%B7%B1%E5%85%A5%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1.assets/image-20220811192056869.png)

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
        // ==> 每个原型对象都有一个constructor属性, 指回构造函数本身

        function Star(name, age){
            this.name = name 
            this.age = age
        }

        Star.prototype.sing = function(){
            console.log('唱歌')
        }
        Star.prototype.dance = function(){
            console.log('跳舞')
        }
        console.log(Star.prototype)

        // 直接把对象赋值给Star.prototype
        Star.prototype = {

            /* 
                 这个时候,constructor属性丢失了
                 如果我们直接给原型对象赋值一个对象, 相当于整个替换了原型对象,
                 这个时候,constructor属性丢失, 也就不知道这个原型是哪个构造函数的原型.
                 所以,我们可以手动添加一个constructor属性, 指回原来的构造函数 
            */

            constructor:Star,
            sing: function(){
                console.log('唱歌')
            },
            dance: function(){
                console.log('跳舞')
            }
        }
        console.log(Star.prototype)


        let obj = {a:1, b:2}
        obj.c = 3
        console.log(obj)

        obj = {d: 4}
        console.log(obj)
    </script>
</body>
</html>
```



#### 2.3总结

1. constructor属性的作用是什么？ 
   *  指向该原型对象的构造函数

### 3.对象原型

#### 3.1定义

对象都会有一个属性 __proto__ 指向构造函数的 prototype 原型对象，之所以我们对象可以使用构造函数 prototype  原型对象的属性和方法，就是因为对象有 __proto__ 原型的存在。

![image-20220811192623259](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%B7%B1%E5%85%A5%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1.assets/image-20220811192623259.png)

#### 3.2对象原型注意事项

注意： 

* __proto__ 是JS非标准属性 
* [[prototype]]和__proto__意义相同 
* 用来表明当前实例对象指向哪个原型对象prototype
*  __proto__对象原型里面也有一个 constructor属性，指向创建该实例对象的构造函数

#### 3.3总结

1. prototype是什么？哪里来的？ 

   * 原型（原型对象） 

   * 构造函数都自动有原型

2. constructor属性在哪里？作用干啥的？ 

   * prototype原型和对象原型__proto__里面都有 

   * 都指向创建实例对象/原型的构造函数

3. __proto__属性在哪里？指向谁？

   *  在实例对象里面 

   * 指向原型 prototype

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

         function Star(name, age){
            this.name = name 
            this.age = age
        }

        Star.prototype.sing = function(){
            console.log('Sing');
        }

        const ldh = new Star('刘德华', 19)

        /* 
            方法属性的查找规则
            首先看 ldh 对象本身有没有 sing 这个方法，如果有 ， 就执行这个对象上的sing 方法
            如果没有，就会通过__proto__ 去实例的原型上查找
         */

        // 1. __proto__ 隐式原型
        // 实例通过__proto__ 访问（链接）到它的原型对象
        ldh.__proto__ === Star.prototype

        // 每一个对象都默认有一个__proto__属性， 指向它的构造函数的prototype显示原型
        // __proto__相当于是一个原型， 链接 ，实例通过它的访问原型对象


        function Animal() {
            this.color = 'orange'
        }

        const cat = new Animal()
        console.log(cat.__proto__ === Animal.prototype)     // true
        console.log(cat.__proto__)                          // 得到的是原型
        console.log(Animal.prototype)                       // 得到的也是原型

        console.log(Animal.prototype.constructor === Animal)     
        console.log(cat.__proto__.constructor === Animal)     

        // 实例.__proto__ ==== 构造函数.prototype
    </script>
</body>
</html>
```

### 4.原型继承

#### 4.1定义

![image-20220811193314031](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%B7%B1%E5%85%A5%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1.assets/image-20220811193314031.png)

#### 4.2封装

![image-20220811193341337](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%B7%B1%E5%85%A5%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1.assets/image-20220811193341337.png)

#### 4.3继承

![image-20220811193429748](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%B7%B1%E5%85%A5%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1.assets/image-20220811193429748.png)

#### 4.4问题

![image-20220811193504826](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%B7%B1%E5%85%A5%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1.assets/image-20220811193504826.png)

#### 4.5原因

![image-20220811193528622](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%B7%B1%E5%85%A5%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1.assets/image-20220811193528622.png)

#### 4.6解决

![image-20220811193557589](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%B7%B1%E5%85%A5%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1.assets/image-20220811193557589.png)

#### 4.7 继承写法完善

![image-20220811193625189](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%B7%B1%E5%85%A5%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1.assets/image-20220811193625189.png)

![image-20220811193634200](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%B7%B1%E5%85%A5%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1.assets/image-20220811193634200.png)

```js
   // 继续抽取   公共的部分放到原型上
    // const Person1 = {
    //   eyes: 2,
    //   head: 1
    // }
    // const Person2 = {
    //   eyes: 2,
    //   head: 1
    // }
    // 构造函数  new 出来的对象 结构一样，但是对象不一样
    function Person() {
      this.eyes = 2
      this.head = 1
    }
    // console.log(new Person)
    // 女人  构造函数   继承  想要 继承 Person
    function Woman() {

    }
    // Woman 通过原型来继承 Person
    // 父构造函数（父类）   子构造函数（子类）
    // 子类的原型 =  new 父类  
    Woman.prototype = new Person()   // {eyes: 2, head: 1} 
    // 指回原来的构造函数
    Woman.prototype.constructor = Woman

    // 给女人添加一个方法  生孩子
    Woman.prototype.baby = function () {
      console.log('宝贝')
    }
    const red = new Woman()
    console.log(red)
    // console.log(Woman.prototype)
    // 男人 构造函数  继承  想要 继承 Person
    function Man() {

    }
    // 通过 原型继承 Person
    Man.prototype = new Person()
    Man.prototype.constructor = Man
    const pink = new Man()
    console.log(pink)

```



### 5.构造函数，原型，实例之间的关系

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
        // 构造函数  原型 实例之间的关系
        function Person() {
            this.name = name
        }
        const Person = new Person()
        // 四条线：
        // 1. 构造函数 有一个prototype 属性，指向原型（对象）
        // 2. 原型对象默认有一个constructor属性，指向构造函数
        // （构造函数和原型 是相互指向）

        // 3. 构造函数通过 new 创建一个实例
        // 4. 实例通过__proto__访问     
        // 实例与构造函数原型之间有直接联系（__proto__），但是与构造函数之间没有
    </script>
</body>
</html>
```

### 6.原型链

#### 6.1定义

基于原型对象的继承使得不同构造函数的原型对象关联在一起，并且这种关联的关系是一种链状的结构，我们将原型对 象的链状结构关系称为原型链

![image-20220811194115092](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%B7%B1%E5%85%A5%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1.assets/image-20220811194115092.png)

#### 6.2 原型链-查找规则

① 当访问一个对象的属性（包括方法）时，首先查找这个对象自身有没有该属性。

② 如果没有就查找它的原型（也就是 __proto__指向的 prototype 原型对象） 

③ 如果还没有就查找原型对象的原型（Object的原型对象） 

④ 依此类推一直找到 Object 为止（null） 

⑤ __proto__对象原型的意义就在于为对象成员查找机制提供一个方向，或者说一条路线 

⑥ 可以使用 instanceof 运算符用于检测构造函数的 prototype 属性是否出现在某个实例对象的原型链上

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
        function Person(name){
            this.name = name 
        }
        const person = new Person

        // 原型链
        // 1. Person.prototype也是一个对象, 所以, 它也有__proto__属性. (规则2)
        console.log(Person.prototype) // 原型对象
        // Person.prototype是一个对象, 那么 Person.prototype 这个对象的构造函数是谁呢?
        // Person.prototype这个对象的构造函数 ===> Object()  

        // 所有的对象，都可以理解为时Object()这个构造函数创建的
        // 所以: Person.prototype 的隐式原型 指向 它的构造函数的显示原型
        console.log(Person.prototype.__proto__ === Object.prototype) 

        // 2. Object.prototype 是什么, 是原型 , 是谁的原型 Object()构造函数的原型
        // 2.1 Object.prototype 原型, 默认有一个constructor属性, 指向构造函数Object
        // 2.2 Object构造函数通过 prototype 访问到这个原型 Object.prototype
        console.log(Person.prototype.__proto__ === Object.prototype) 

        // 也就是说 , 以下两个  都指向了 Object()这个构造函数的原型
        console.log(Object.prototype) 
        console.log(Person.prototype.__proto__)

        // 3. Object是构造函数嘛? 是, 所以Object也有prototype属性  (规则3)
        // Object.prototype 它是Object的原型对象. 所以Object.prototype有__proto__属性 (规则2)
        // 但是 Object.prototype.__proto__ 指向空 
        Object.prototype.__proto__  === null

        // 正常的原型链都会终止于 Object的原型对象. 
        // Object原型 的 原型 是 null
        // 我们说的原型, 可以说是构造函数的原型, 也可以说是实例的原型

        // (Object.prototype) ==> Object的原型
        // Object.prototype.__proto__ 能访问到它Object.prototype的原型 
        

        // obj.__proto__  === Object.prototype  obj的原型



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
    <script>
        /* 
            原型链
            每个对象通过__proto__ 属性都能访问到它的原型对象。原型对象也有它的原型对象
            当访问一个对象的属性或方法时，先在自生身中寻找
            如果没有，就会沿着 __proto__ 这条链向上寻找，一直找到最顶层Object.prototype 为止
            Object.prototype.__proto__ === null

            数组的原型链
            arr ---> Array.prototype ---> Object.prototype ---> null
            const arr = [1, 2, 3]
            const arr = new Array(1, 2, 3)

            函数的原型链    fn 相当于是 Function(){} 创建的
            fn --->  Function.prototype --->  Object.prototype ---> null
        */
    </script>
</body>
</html>
```



## 四、原型规则

```js
// 语法糖
// const obj = {}      // const obj = new Object()     
// const arr = []      // const arr = new Array()

//  1.所有的引用类型(对象,数组,函数),   都具有对象的特性,   可以自由扩展属性
const obj = {}         //   obj.a = 1
const arr = []         //   arr.b = 2

//  2.所有的对象,   都有一个__proto__属性(隐式原型),    属性值是一个普通对象
//  __proto__ 也叫做隐式原型  ===>  在浏览器里面 等同于[[prototype]]
console.log(obj.__proto__)
console.log(arr.__proto__)
console.log(fn.__proto__)

//  3.所有的函数,   都有一个__proto__属性,    属性值也是一个普通对象
console.log(fn.prototype)

//  4.所有对象的隐式原型(__proto__),    指向它的构造函数的显示原型(prototype)
obj.__proto__ === Object.prototype   //true
arr.__proto__ === Array.prototype    //true
fn.__proto__ === Function.prototype  //true

//  5.当试图得到对象的某个属性时,   如果这个对象本身没有这个属性,   那么会去它的__proto__中寻找
function Star(name, age) {
    this.name = name 
    this.age = age
    this.sayHi = function () {
        console.log('Hi~');
    }
}
// Star.prototype.sex = '男'
const zjl = new Star('周杰伦', 18)
console.log(zjl)
console.log(zjl.sex)

zjl.__proto__ === Star.prototype
```

## 五、Test

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
        // 01 
        // var a;
        if(false){
            var a=1;
            let b=2;
        }
        console.log(a); // undefined
        console.log(b); // Error

        // 1. if 是语句, 不是函数, var 和 {} 不形成作用域.
        // var 提升到全局
        // 2. let {} 形成块级作用域, 作用域外不能访问到b变量


        // 02 
        fn(123)
        var a = 456;
        function fn(a){
            console.log(a); // 123
        }

        // 03
        var a = 1
        if (true){
            console.log(a)      // Error
            let a = 2
        }
        /* 
            这里 let{} 形成了块级作用域， 必须先声明，后使用
            暂时性死区： let const 声明的变量， 在声明之前如果使用，会报错
        */
    </script>
</body>
</html>
```

## 六、函数声明和变量声明优先级

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
        function a() {}
        var a;
        console.log(a)  // ƒ a() {}
        console.log(typeof a)  // function

        // 1. 函数声明和变量声明, 函数提升的优先级更高, 当二者同时存在的时候, 会优先指向函数声明.
        // 2. 函数提升优先级比变量提升要高,  且不会被同名的变量声明覆盖, 但是, 会被变量的赋值给覆盖掉.

        // 02
        console.log(c) // function c(){}
        var c;
        function c(){
            console.log(c)  // undefined
            var c = 3
        }
        c(2) 

        // 03 
        var c = 1 
        function c(){
            console.log(c)
            var c = 3
        }
        console.log(c)  // 1 
        c(2)  // Error 
        // ==== 转换成下面这样
        function c(){
            console.log(c)
            var c = 3
        }
        var c;
        c = 1 // 赋值了 覆盖掉了
        console.log(c)  // 1 
        c(2)  // Error

        // 04 
        console.log(abc)  // function abc
        var abc;
        console.log(abc)  // 1 
        function abc(){
            console.log(1)
        }


    </script>
</body>
</html>
```

## 七、作用域 this

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
        var name='kaivan';
        (function () {
            if(typeof name==='undefined'){
                var name='chen';
                console.log(name); // chen
            }else {
                console.log(name); //
            }
        })();

        // 02 
        var a=10;
        function test() {
            a=100;
            console.log(a); // 100
            console.log(this.a); // 10
            var a;
            console.log(a); // 100
        }
        test();

        // 03 
        var name='kaivon';
        var object={
            name:'chen',
            getNameFunc:function () {
                return function () {
                    return this.name;
                }
            }
        }
        console.log(object.getNameFunc()())  // kaivon
        // return ==> function () {return this.name;} ==> window.f()  ==> kaivon

        // 04 闭包.
        var name='kaivon';
        var object={
            name:'chen',
            getNameFunc:function () {
                var that = this;
                return function () {
                    return that.name;
                }
            }
        }
        console.log(object.getNameFunc()())
        console.log((function () {return that.name;})())
        // 执行第一次调用的时候,this指向的是object, 用that存了object
        // return ==> function () {return that.name;}
        // 注意这里, 形成了一个闭包, 
        // 第二次调用的时候 , that 取的就是object这个对象. object.name ==> chen

        // 05 
        var a = 666;
        console.log(++a);  // 667  ++a表达式的值, 是a+1之后的.
        console.log(a++);  // 667  a++表达式的值, 是加之前的值
        console.log(a); // 668 

        // 06 
        var a;
        var b='undefined';
        console.log(typeof a);  // undefined
        console.log(typeof b);  // string
        console.log(typeof c); //  undefined

        // 07 作用域的知识点!
        // 函数是加了()才表示调用执行
        var x = 10;
        function fn() {
            console.log(x); // 10
        }
        function show(f) {
            var x=20;
            f();
        }
        show(fn);

        //背下来: 作用域链在定义的时候就确定了, 找定义时候的变量!!!

        // 08  this的指向是执行(调用)的时候确定的.
        var x=10;
        var foo={
            x:90,
            getX:function () {
                return this.x;
            }
        };
        console.log(foo.getX()); // 90
        var xGetter=foo.getX;  // var xGetter = function (){return this.x}
        console.log(xGetter()); // 10 
        // window.xGetter() 
                                                                
        // 09 
        (function (x) {
            // let x = 1
            return (function (y) {
                // let y = 2
                console.log(x);  // 1
            })(2)
        })(1);

        // 10
        var fn = function (){
            console.log(fn); // function(){console.log(fn)}
        }
        fn();
        var obj = {
            // 这里没有作用域
            f2:function(){
                // 函数作用域, 找 f2
                console.log(f2);  // Error f2 is not defined
                // 上层作用域, window里面没有f2 
            }
        }
        obj.f2();
    </script>
</body>
</html>                                                                      
```

## 八、冒泡排序

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
         x// 5 个数, 我们 做了 4 轮排序

        // 第 1 轮(0) , 比较了几次呢 4次
        // 第 2 轮(1) , 比较 3 次 
        // 第 3 轮(2) , 比较 2 次
        // 第 4 轮(3) , 比较 1 次

        // 外层循环 : 控制 比较的轮数(趟数)
        // 内层循环 : 控制每一轮比较的次数(交换), 交换两个变量
        // arr.length - 1  4 ;   i  ==> 0 1 2 3 
        let arr = [5, 1, 4, 2, 8]
        for (let i = 0; i < arr.length - 1; i++) {
            for (let j = 0; j < arr.length - 1 - i; j++){
                // 作比较, 如果前一个数, 比后一个数大; 
                // 交换两个数的位置
                if (arr[j] > arr[j + 1]) {
                    // 交换两个变量
                    let temp = arr[j]
                    arr[j] = arr[j + 1]
                    arr[j + 1] = temp
                }
            }
        }

        console.log(arr)

        // 内层循环 arr.length - 1 - i 
        // 这里的 - i 怎么理解呢? 
        // 每次排一轮之后, 我们确定一个 最大的数.
        // 第 1 轮(0) , 比较了几次呢 4次
        // 第 2 轮(1) , 比较 3 次 
        // 第 3 轮(2) , 比较 2 次
        // 第 4 轮(3) , 比较 1 次

        // 1. 外层循环: 控制比较轮数   : arr.length - 1 数组长度为5, 比较4轮.
        // 2. 内层循环, 控制每一轮比较的次数.(交换)  : arr.length - 1 - i;
        // 3. 外层每走一轮, 就确定一个最大的数.
        // - i 是为了性能更好, 就是每比较一轮之后, 有一个最大的数, 冒泡到最后了

        // 4.注意: 每轮的循环条件, 是小于符号, 不是小于等于.


        for (let i = 0; i < arr.length - 1; i++) {
            for(let j = 0; j < arr.length - 1 - i; j++){
                // 中间交换变量
                if (arr[j] > arr[j+1]){
                    // [a,b] = [b,a]
                    [arr[j], arr[j+1]] = [arr[j+1], arr[j]]
                }
            }
        }

        let arr1 = [ 1, 3, 6, 2, 9, 8]
        // arr.sort() 底层原理, 就是冒泡排序
        arr.sort(cbFn) // 接收一个函数 , 函数里面的两个参数, a,b 就表示相互比较的两个数
        // 如果a > b ==> a - b > 0  ==> 把a冒泡到后面去.
        // arr.sort(function(a,b){
        //     return a - b
        // })
        arr1.sort((a,b) => a - b)  // 从小到大排序
        arr1.sort((a,b) => b - a) // 从大到小排序 
    </script>
</body>
</html>
```



