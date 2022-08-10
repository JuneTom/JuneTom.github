# JavaScript 进阶第二天 构造函数&数据常用函数

## 一、深入对象

### 1.创建对象三种方式

#### 1.1利用对象字面量创建对象

![image-20220809175727175](D:\Program Files (x86)\blog\docs\Work\JavaScript高级\JavaScript 进阶第二天 构造函数&数据常用函数.assets/image-20220809175727175.png)

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
        // 对象：是属性和方法的集合。（集合本身就是无序的）
        // 属性: 描述事物的特性，常用名词
        // 方法：描述事物的行为，常用动词

        // 创建对象的三种方式
        // 1. 利用对象字面量的方式创建对象 {} 
        const obj = {}  // 创建了一个空对象

        const p1 = {
            name:'张三丰',
            age:128,
            sayHi:function(){
                console.log('Hello World')
            }
        }
        // 1. 获取对象的属性
        // 1.1 对象名.属性名
        console.log(p1.name)
        // 1.2 对象名['属性名']
        console.log(p1['name'])

        // 2. 调用对象的方法 加小括号
        // 2.1 对象名.方法()
        p1.sayHi()
        // 2.2 忘掉 
        // p1['sayHi']()
        
    </script>
</body>
</html>
```

#### 1.2利用 new Object 创建对象

![image-20220809175802436](D:\Program Files (x86)\blog\docs\Work\JavaScript高级\JavaScript 进阶第二天 构造函数&数据常用函数.assets/image-20220809175802436.png)

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
        // 利用 new Object() 创建对象
        const obj = new Object() // 创建了一个空对象
        obj.name = '张三丰'
        obj.age = '128'
        obj.sex = 'female'
        obj.sayHi = function(){
            console.log('Hi~')
        }

        // 可以直接传入要添加的属性
        const p1 = new Object({uname:'周杰伦'})
        console.log(p1)

        // 语法糖  甜甜的 用了就不会再用其他方式了
        const obj = {}  // ===>  const obj = new Object()
        const arr = []  // ===>  const arr = new Array()
    </script>
</body>
</html>
```

#### 1.3利用构造函数创建对象

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
      // 思考： 为什么要用构造函数 ？

      // 构造函数相当于一个模板
      // function 构造函数名(形参1,形参2,形参3) { // 构造函数的形参与对象的普通属性是一般一致的
      //     this.属性名1 = 形参1;
      //     this.属性名2 = 形参2; // 属性的值，一般是通过同名的形参来赋值的
      //     this.属性名3 = 形参3;
      //     this.方法名 = function(){
      //     };
      // }
      // 调用
      const obj = new 构造函数名(实参1, 实参2, 实参3)

      // 简记
      function 构造函数名() {
        this.属性 = 值 // 当前的这个对象的
        this.方法 = function () {}
      }
      new 构造函数名()

      // 注意:
      // 1. 构造函数名字首字母要大写
      // 2. 构造函数里 属性和方法前面必须添加 this
      // 2. 构造函数不需要 return 就可以返回结果
      // 3. 我们调用构造函数 必须使用 new
    </script>
  </body>
</html>

```



### 2.构造函数

#### 2.1定义

* 构造函数 ：是一种特殊的函数，主要用来初始化对象
*  使用场景：常规的 {...} 语法允许创建一个对象。比如我们创建了佩奇的对象，继续创建乔治的对象还需要重新写一 遍，此时可以通过构造函数来快速创建多个类似的对象。

![image-20220809180000294](D:\Program Files (x86)\blog\docs\Work\JavaScript高级\JavaScript 进阶第二天 构造函数&数据常用函数.assets/image-20220809180000294.png)

#### 2.2构造函数的两个约定

构造函数在技术上是常规函数。 

不过有两个约定： 

1. 它们的命名以大写字母开头。 
2.  它们只能由 "new" 操作符来执行。

![image-20220809180247665](D:\Program Files (x86)\blog\docs\Work\JavaScript高级\JavaScript 进阶第二天 构造函数&数据常用函数.assets/image-20220809180247665.png)



![image-20220809180443724](D:\Program Files (x86)\blog\docs\Work\JavaScript高级\JavaScript 进阶第二天 构造函数&数据常用函数.assets/image-20220809180443724.png)

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
    // Person
    // 需求：定义一个人类构造函数，通过它创建的人类对象包含
    // 属性：姓名，年龄，性别 name, age, sex
    // 方法：打招呼。sayHi

    // 简记
    // function 构造函数名() {
    //     this.属性 = 值;  // 当前的这个对象的
    //     this.方法 = function() {}
    // }
    // new 构造函数名();

    function Person(name, age, sex) {
        this.name = name 
        this.age = age 
        this.sex = sex
        this.sayHi = function(msg){  // 构造函数的方法如果想要传参，形参写在这里
            console.log(msg)
        }
    }

    const p1 = new Person('周街路', 18, '男')
    // console.log(p1)
    const p2 = new Person('周杰伦', 19, 'male')
    // console.log(p2)

    // 获取属性
    // console.log(p1.name)
    // 调用对象的方法
    p1.sayHi('Nice to meet U :)')

    // 注意：
    // 1. 构造函数的首字母大写
    // 2. 构造函数里面，属性和方法前面必须加this
    // 3. 构造函数不需要return 就可以返回结果
    // 4. 我们调用构造函数 ，必须使用new 

    // 构造函数，相当于一个模板， 通过它，我们可以创建一系列具有相同属性和方法的对象。
    // 实例化： 通过构造函数创建对象的过程， 就叫作实例化。


    </script>
</body>
</html>
```

#### 2.3总结

* 构造函数的作用是什么？怎么写呢？

  * 构造函数是来快速创建多个类似的对象 

  * 大写字母开头的函数 

* new 关键字调用函数的行为被称为？ 
  * 实例化

* 构造函数内部需要写return吗，返回值是什么？

  *  不需要 

  * 构造函数自动返回创建的新的对象

#### 2.4练习(利用构造函数创建多个对象)

![image-20220809180722900](D:\Program Files (x86)\blog\docs\Work\JavaScript高级\JavaScript 进阶第二天 构造函数&数据常用函数.assets/image-20220809180722900.png)

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
        // Goods
        function Goods(name, price, count){
            this.name = name 
            this.price = price
            this.count = count
        }

        const mi = new Goods('小米', 1999, 20)
        const hw = new Goods('华为', 3999, 59)
        console.log(mi, hw)
    </script>
</body>
</html>
```

#### 2.5实例化执行过程

说明：

1. 创建新对象
2.  构造函数this指向新对象 
3. 执行构造函数代码，修改this，添加新的属性
4. 返回新对象

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
    function Person(name, age, sex) {
        // const this = {}
        this.name = name 
        this.age = age 
        this.sex = sex
        this.sayHi = function(msg){  // 构造函数的方法如果想要传参，形参写在这里
            console.log(msg)
        }
        // return this
    }
    const p1 = new Person('杰伦', 18, '男')
    console.log(p1)

    // new的执行过程 背下来！必须背下来！理解
    // 1. 在函数内部创建了一个空对象
    // 2. 让this指向这个空对象
    // 3. 执行构造函数里面的代码，给这个空对象添加属性和方法
    // 4. 返回这个对象（return this）
    </script>
</body>
</html>
```



### 3.实例成员&静态成员

#### 3.1实例成员

![image-20220809181047394](D:\Program Files (x86)\blog\docs\Work\JavaScript高级\JavaScript 进阶第二天 构造函数&数据常用函数.assets/image-20220809181047394.png)

#### 3.2静态成员

![image-20220809182510489](D:\Program Files (x86)\blog\docs\Work\JavaScript高级\JavaScript 进阶第二天 构造函数&数据常用函数.assets/image-20220809182510489.png)

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
      function Person(name, age, sex) {
        this.name = name
        this.age = age
        this.sex = sex
        this.sayHi = function (msg) {
          // 构造函数的方法如果想要传参，形参写在这里
          console.log(msg)
        }
      }

      const p1 = new Person('周街路', 18, '男')
      const p2 = new Person('周杰伦', 19, 'male')
      //   实例：通过构造函数创造的对象
      //   实例成员：实例对象的属性和方法
      //   也就是构造函数内部通过this添加属性和方法

      console.log(p1.name)
      console.log(p1.sayHi('吃饭了嘛？'))

      // 静态成员：在构造函数本身添加的属性和方法
      // 函数也是一个对象，可以添加属性和方法
      // 静态成员，通过构造函数来访问

      // 静态属性
      Person.demo = 'test'
      // 静态方法
      Person.max = function () {
        console.log(max)
      }
      console.dir(Person)
    </script>
  </body>
</html>

```

#### 3.3总结

1. 什么是实例成员？

   实例对象的属性和方法即为实例成员 

2. 什么是静态成员？ 

    构造函数的属性和方法被称为静态成员

## 二、内置构造函数

### 1.数据类型

![image-20220809182920202](D:\Program Files (x86)\blog\docs\Work\JavaScript高级\JavaScript 进阶第二天 构造函数&数据常用函数.assets/image-20220809182920202.png)

![image-20220809182930155](D:\Program Files (x86)\blog\docs\Work\JavaScript高级\JavaScript 进阶第二天 构造函数&数据常用函数.assets/image-20220809182930155.png)

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
      // 字符串
      // String Number Boolean undefinded null Symbol BigInt
      const str = 'skyblue'
      //   按理说，基本数据类型没有属性和方法
      // 检测字符串长度
      console.log(str.length)
      const num = 10

      //   numtoFixed()  //保留两位小数
      console.log(num.toFixed(2))

      // 基本包装类型:Js底层，把简单数据类型，包装成复杂数据类型（对象）
      const str1 = '1212121'
      //   const str1 = new String('12121')
    </script>
  </body>
</html>

```



### 2.Object

![image-20220810150015991](D:\Program Files (x86)\blog\docs\Work\JavaScript高级\JavaScript 进阶第二天 构造函数&数据常用函数.assets/image-20220810150015991.png)

#### 2.1Object.keys 静态方法获取对象中所有属性（键）

![image-20220810150629993](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%9E%84%E9%80%A0%E5%87%BD%E6%95%B0&%E6%95%B0%E6%8D%AE%E5%B8%B8%E7%94%A8%E5%87%BD%E6%95%B0.assets/image-20220810150629993.png)

#### 2.2Object.values 静态方法获取对象中所有属性值

![image-20220810150711996](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%9E%84%E9%80%A0%E5%87%BD%E6%95%B0&%E6%95%B0%E6%8D%AE%E5%B8%B8%E7%94%A8%E5%87%BD%E6%95%B0.assets/image-20220810150711996.png)



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
      // 回忆for in 遍历对象的属性
      const obj = { name: 'zz', age: 18 }

      for (let key in obj) {
        // console.log(key)
        console.log(obj[key])
        // obj[key] 方括号的形式
        // key作为一个字符串的变量。
        // console.log(obj.key) // undefined
      }

      console.log(obj.key)
      // obj.key 点的形式
      // 这个时候，key表示属性名，只有对象拥有这个属性的时候，才能打印

      //      Object静态方法
      // Object.keys()
      // 返回由传入对象的所有属性名组成的字符串数组
      console.log(Object.keys(obj))

      Object.values()
      // 返回由传入对象的所有属性值组成的数组
      console.log(Object.values(obj))

      const obj2 = {
        name: '周杰伦',
        age: 18,
        sex: '男',
        sayHi: function () {
          console.log('1')
        },
      }
      // 获取所有的属性名:
      console.log(Object.keys(obj2))

      // 获取所有的属性值:
      console.log(Object.values(obj2))
      const res = Object.values(obj2)
      res[3]()
    </script>
  </body>
</html>

```



#### 2.3Object. assign 静态方法常用于对象拷贝

![image-20220810150733854](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%9E%84%E9%80%A0%E5%87%BD%E6%95%B0&%E6%95%B0%E6%8D%AE%E5%B8%B8%E7%94%A8%E5%87%BD%E6%95%B0.assets/image-20220810150733854.png)

![image-20220810150812496](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%9E%84%E9%80%A0%E5%87%BD%E6%95%B0&%E6%95%B0%E6%8D%AE%E5%B8%B8%E7%94%A8%E5%87%BD%E6%95%B0.assets/image-20220810150812496.png)

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
      /* 
            Object.assign() 对象的拷贝，浅拷贝
            Object.assign(target,...sources)
            参数：
            target 目标对象
            sources 源对象，一个或者多个，把他的属性复制给对象

        */
      //   const obj = {}
      //   const o = { name: 'xx' }
      //   Object.assign(obh, o) //有返回值
      //   const res = Object.assign(obj, o)
      //   console.log(res)

      //   作用：合并对象
      const o1 = { a: 1 }
      const o2 = { b: 1 }
      const o3 = { c: 1 }

      const obj = Object.assign(o1, o2, o3)
      console.log(o1) //o1被修改
      console.log(obj) //返回值就是目标对象
      console.log(o1 === obj) //true
    </script>
  </body>
</html>

```



#### 2.4总结

1. 什么是静态方法？

   只能给构造函数使用的方法 比如 Object.keys()

2.  Object.keys()方法的作用是什么 ？

   获取对象中所有属性（键）

3.  Object.values()方法的作用是什么 ？

   获取对象中所有属性值（值）

### 3.Array

![image-20220810151109811](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%9E%84%E9%80%A0%E5%87%BD%E6%95%B0&%E6%95%B0%E6%8D%AE%E5%B8%B8%E7%94%A8%E5%87%BD%E6%95%B0.assets/image-20220810151109811.png)

#### 3.1数组常见实例方法-核心方法

![image-20220810151142230](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%9E%84%E9%80%A0%E5%87%BD%E6%95%B0&%E6%95%B0%E6%8D%AE%E5%B8%B8%E7%94%A8%E5%87%BD%E6%95%B0.assets/image-20220810151142230.png)

![image-20220810151150613](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%9E%84%E9%80%A0%E5%87%BD%E6%95%B0&%E6%95%B0%E6%8D%AE%E5%B8%B8%E7%94%A8%E5%87%BD%E6%95%B0.assets/image-20220810151150613.png)

#### 3.2 数组的reduce

![image-20220810151258522](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%9E%84%E9%80%A0%E5%87%BD%E6%95%B0&%E6%95%B0%E6%8D%AE%E5%B8%B8%E7%94%A8%E5%87%BD%E6%95%B0.assets/image-20220810151258522.png)

![image-20220810151430797](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%9E%84%E9%80%A0%E5%87%BD%E6%95%B0&%E6%95%B0%E6%8D%AE%E5%B8%B8%E7%94%A8%E5%87%BD%E6%95%B0.assets/image-20220810151430797.png)

![image-20220810151440712](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%9E%84%E9%80%A0%E5%87%BD%E6%95%B0&%E6%95%B0%E6%8D%AE%E5%B8%B8%E7%94%A8%E5%87%BD%E6%95%B0.assets/image-20220810151440712.png)

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
      // 实例方法：通过构造函数生成的实例，调用的方法
      // mdn 中间带有prototype(原型)的这种方法，就叫实例方法

      //   const arr = new Array(3, 5)
      //   const arr = [3, 5]

      /*
                    语法: arr.reduce(function(){}, initValue)
              作用: 对数组的每个元素,都执行一个自定义的reducer函数, 将其结果汇总为单个返回值
              参数:
                  callbackFn  回调函数 (必选)
                  initValue   初始值   (非必选)
              callbackFn的参数
                   previousValue : 上一次调用callbackFn时的返回值. (必选)
                   currentValue  : 当前元素 (必选)
                   currentIndex  : 当前元素的索引 (非必选)
                   array         : 源数组  (非必选)

                   注意 :第一次调用的时候,如果有初始值,则prev 为初始值
                   否则,prev为数组的第一个元素arr[0]
            */

      const arr = [1, 2, 3]
      const res1 = arr.reduce(function (pre, cur) {
        return pre + cur
      }, 2)
      console.log(res1)
      /* 
        2+1=3
        3+2=5
        5+3=8
      */

      //   箭头函数   常用于求和
      const res2 = arr.reduce((pre, cur) => pre + cur)
      console.log(res2)
    </script>
  </body>
</html>

````

#### 3.3练习(员工涨薪计算成本)

![image-20220810151512602](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%9E%84%E9%80%A0%E5%87%BD%E6%95%B0&%E6%95%B0%E6%8D%AE%E5%B8%B8%E7%94%A8%E5%87%BD%E6%95%B0.assets/image-20220810151512602.png)

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
      // 需求:计算涨薪后的成本
      const arr = [
        {
          name: '张三',
          salary: 10000,
        },
        {
          name: '李四',
          salary: 10000,
        },
        {
          name: '王五',
          salary: 20000,
        },
        {
          name: '庞钰鹏',
          salary: 50000,
        },
      ]

      //   const money = arr.reduce(function (pre, cur) {
      //     console.log(cur)
      //     return pre + cur.salary * 0.3
      //   }, 0)
      //   console.log(money)

      const money = arr.reduce((pre, cur) => pre + cur.salary * 0.3, 0)
      console.log(money)
    </script>
  </body>
</html>

```

#### 3.4 Array的常用语法



![image-20220810151819510](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%9E%84%E9%80%A0%E5%87%BD%E6%95%B0&%E6%95%B0%E6%8D%AE%E5%B8%B8%E7%94%A8%E5%87%BD%E6%95%B0.assets/image-20220810151819510.png)

##### 3.5 arr.find(cbFn)  arr.findIndex(cbFn)

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
      /*
            语法 arr.find(cbFn)
            作用:返回数组中满足条件的第一个数组元素,否则返回 undefinded
            参数:
                cbFn 回调函数

            cbFn 回调函数参数:
                参数一:item  当前的元素
                参数二:index 当前元素的索引号(非必须)
            返回值:数组中第一个满足条件的元素
         */

      //   const arr = ['red', 'green', 'blue']
      //   const res = arr.find(function (item) {
      //     return (item === 'green')
      //   })

      //   const res = arr.find((item) => item === 'green')
      //   console.log(res)

      const arr = [
        { name: '小米', price: 1999 },
        { name: '华为', price: 3999 },
        { name: 'iphone', price: 5999 },
      ]

      const res = arr.find(function (item) {
        return item.name === '小米'
      })
      console.log(res)

      
    </script>
  </body>
</html>

````

#### 3.6 arr.findIndex(cbFn)

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
      const arr = [
        { name: '小米', price: 1999 },
        { name: '华为', price: 3999 },
        { name: 'iphone', price: 5999 },
      ]
      /*
       语法 arr.findIndex(cbFn)
            作用:查询数组中满足条件的第一个元素的索引,否则返回-1
            参数:
                cbFn 回调函数
            cbFn 回调函数参数:
                参数一:item  当前的元素
                参数二:index 当前元素的索引号(非必须)
      */

      const index = arr.findIndex((item) => item.name === 'iphone')
      console.log(index)
    </script>
  </body>
</html>

```



#### 3.7 arr.every(cbFn)

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
      /* 
            语法 arr.every(cbFn)                    cbFn : callbackFn : 回调函数
            作用:检测数组中的所有元素是否都符合指定的条件,如果符合返回True,否则false
            
            语法 arr.some(cbFn)                    cbFn : callbackFn : 回调函数
            作用:检测数组中的部分元素是否符合指定的条件,如果符合返回True,否则false
            参数:
                cbFn 回调函数
            cbFn 回调函数参数:
                参数一:item  当前的元素
                参数二:index 当前元素的索引号(非必须)
            返回值:
                Boolean 所有元素都通过才返回TRUE
            注意:
                因为这个方法有返回值,所以回调函数中需要有return
        */

      const arr = [10, 20, 30]
      const res1 = arr.every((item) => item >= 10)
      const res2 = arr.some((item) => item >= 30)
      console.log(res1)
      console.log(res2)
    </script>
  </body>
</html>

```

#### 3.8 arr.includes() Array.from()

![image-20220810153406412](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%9E%84%E9%80%A0%E5%87%BD%E6%95%B0&%E6%95%B0%E6%8D%AE%E5%B8%B8%E7%94%A8%E5%87%BD%E6%95%B0.assets/image-20220810153406412.png)

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
      <li></li>
      <li></li>
      <li></li>
    </ul>
    <script>
      /* 
            arr.includes()
            作用: 判断一个数组是否包含某个元素,如果有返回true 否则返回false

            Array.from()    静态fangfa
            作用:把伪数组转换为真数组
            伪数组:有length,有索引号,没有数组的 pop()等一些方法
        */
      const arr = [10, 20, 30]
      const res1 = arr.includes(10)
      const res2 = arr.includes(40)
      console.log(res1)
      console.log(res2)

      const lis = document.querySelector('ul li')
      console.log(lis)
      const lis_R = Array.from(lis)
      lis_R.pop()
      console.log(lis_R)
    </script>
  </body>
</html>

```

#### 3.9 练习

![image-20220810153217877](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%9E%84%E9%80%A0%E5%87%BD%E6%95%B0&%E6%95%B0%E6%8D%AE%E5%B8%B8%E7%94%A8%E5%87%BD%E6%95%B0.assets/image-20220810153217877.png)

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
    <div></div>
    <script>
      const spec = { size: '40cm*40cm', color: '黑色' }
      const div = document.querySelector('div')

      //   1.获取对象的所有属性值
      //  arr.join('')将数组转换为字符串,参数可以传入分隔符
      const res = Object.values(spec).join('/')
      console.log(res)
      //   放入div
      div.innerHTML = res
    </script>
  </body>
</html>

```

### 4.String

![image-20220810153453101](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%9E%84%E9%80%A0%E5%87%BD%E6%95%B0&%E6%95%B0%E6%8D%AE%E5%B8%B8%E7%94%A8%E5%87%BD%E6%95%B0.assets/image-20220810153453101.png)

#### 4.1. 常见实例方法

![image-20220810153515040](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%9E%84%E9%80%A0%E5%87%BD%E6%95%B0&%E6%95%B0%E6%8D%AE%E5%B8%B8%E7%94%A8%E5%87%BD%E6%95%B0.assets/image-20220810153515040.png)

#### 4.2str.split()

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
        // 1.  str.split()
        // 使用指定分隔符，将字符串分割，得到一个字符串数组。
        const str = 'The quick brown fox jumps over the lazy dog.'
        const words = str.split(' ')
        console.log(words)

        const str1 = '2022-08-09'
        const arr = str1.split('-')
        console.log(arr)
        console.log(arr[0]) // 得到年


    </script>
</body>
</html>
```

#### 4.3 str.substring

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
      /* 
            str.substring(开始的索引号[,结束的索引号])
            作用:字符串截取
            注意:
                1.如果省略indexEnd,取到最后
                2.前闭后开区间[start,end),结束索引号不包含在截取的字符串
        */
      const str = '你喜欢吃冰淇淋嘛?'
      console.log(str.substring(1))
      console.log(str.substring(1, 3))
    </script>
  </body>
</html>

```

#### 4.4str.startsWith()

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
      /* 
            str.startsWith()
            语法:str.startsWith(searchString[, position])
            作用:判断是否以某个字母开头
            参数:
                参数一:要搜索的字符串
                参数二:在str中搜索的开始位置,默认为0(非必选)
            返回值:true/false
        */

      const str = 'To be, or not to be, that is the question.'

      console.log(str.startsWith('To be')) // true
      console.log(str.startsWith('not to be')) // false
      console.log(str.startsWith('not to be', 10)) // true

    </script>
  </body>
</html>

```



#### 4.5str.includes()

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
     

      /* 
        str.includes()
        作用:判断一个字符串是否包含在另外一个字符串中
        注意:区分大小写
        返回值:true/false
      */

      const str1 = 'To be, or not to be, that is the question.'

      console.log(str1.includes('To be')) // true
      console.log(str1.includes('Question')) // false

      const str2 = '今天你吃了嘛?'
      console.log(str1.includes('你', 2)) // true
      console.log(str1.includes('你', 1)) // false
    </script>
  </body>
</html>

```

#### 4.6练习（显示赠品练习）

![image-20220810154435483](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%9E%84%E9%80%A0%E5%87%BD%E6%95%B0&%E6%95%B0%E6%8D%AE%E5%B8%B8%E7%94%A8%E5%87%BD%E6%95%B0.assets/image-20220810154435483.png)

![image-20220810154454004](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%9E%84%E9%80%A0%E5%87%BD%E6%95%B0&%E6%95%B0%E6%8D%AE%E5%B8%B8%E7%94%A8%E5%87%BD%E6%95%B0.assets/image-20220810154454004.png)



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
    <div></div>
    <script>
      const gift = '50g茶叶,清洗球'
      // 把字符串以 , 分割,转为数组
      const arr = gift.split(',')
      console.log(arr)
      //   map遍历数组
      const res = arr.map(function (item) {
        return `<span>【赠品】${item}</span></br>`
      })
      console.log(res)
      document.querySelector('div').innerHTML = res.join('')
    </script>
  </body>
</html>

```

### 5.Number

![image-20220810161953688](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%9E%84%E9%80%A0%E5%87%BD%E6%95%B0&%E6%95%B0%E6%8D%AE%E5%B8%B8%E7%94%A8%E5%87%BD%E6%95%B0.assets/image-20220810161953688.png)

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
      // num.toFixed()
      // 设置保留两位小数
      const num = 10.45
      // 如果不传入参数,四舍五入转为整数形式的字符串
      console.log(num.toFixed())
      console.log(typeof num.toFixed())
      console.log(num.toFixed(1))

      const num1 = 10
      console.log(num1.toFixed(2))
    </script>
  </body>
</html>

```



## 三、综合案例(购物车展示)



![image-20220810162144870](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%9E%84%E9%80%A0%E5%87%BD%E6%95%B0&%E6%95%B0%E6%8D%AE%E5%B8%B8%E7%94%A8%E5%87%BD%E6%95%B0.assets/image-20220810162144870.png)

![image-20220810162156663](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%9E%84%E9%80%A0%E5%87%BD%E6%95%B0&%E6%95%B0%E6%8D%AE%E5%B8%B8%E7%94%A8%E5%87%BD%E6%95%B0.assets/image-20220810162156663.png)

![image-20220810162229126](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%9E%84%E9%80%A0%E5%87%BD%E6%95%B0&%E6%95%B0%E6%8D%AE%E5%B8%B8%E7%94%A8%E5%87%BD%E6%95%B0.assets/image-20220810162229126.png)

![image-20220810162245154](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%9E%84%E9%80%A0%E5%87%BD%E6%95%B0&%E6%95%B0%E6%8D%AE%E5%B8%B8%E7%94%A8%E5%87%BD%E6%95%B0.assets/image-20220810162245154.png)

![image-20220810162311379](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%9E%84%E9%80%A0%E5%87%BD%E6%95%B0&%E6%95%B0%E6%8D%AE%E5%B8%B8%E7%94%A8%E5%87%BD%E6%95%B0.assets/image-20220810162311379.png)

![image-20220810162325338](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%9E%84%E9%80%A0%E5%87%BD%E6%95%B0&%E6%95%B0%E6%8D%AE%E5%B8%B8%E7%94%A8%E5%87%BD%E6%95%B0.assets/image-20220810162325338.png)

![image-20220810162342710](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%9E%84%E9%80%A0%E5%87%BD%E6%95%B0&%E6%95%B0%E6%8D%AE%E5%B8%B8%E7%94%A8%E5%87%BD%E6%95%B0.assets/image-20220810162342710.png)

![image-20220810162440525](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%9E%84%E9%80%A0%E5%87%BD%E6%95%B0&%E6%95%B0%E6%8D%AE%E5%B8%B8%E7%94%A8%E5%87%BD%E6%95%B0.assets/image-20220810162440525.png)

![image-20220810162515065](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%9E%84%E9%80%A0%E5%87%BD%E6%95%B0&%E6%95%B0%E6%8D%AE%E5%B8%B8%E7%94%A8%E5%87%BD%E6%95%B0.assets/image-20220810162515065.png)

```html
<body>
    <div class="list">
      <!-- <div class="item">
      <img src="https://yanxuan-item.nosdn.127.net/84a59ff9c58a77032564e61f716846d6.jpg" alt="">
      <p class="name">称心如意手摇咖啡磨豆机咖啡豆研磨机 <span class="tag">【赠品】10优惠券</span></p>
      <p class="spec">白色/10寸</p>
      <p class="price">289.90</p>
      <p class="count">x2</p>
      <p class="sub-total">579.80</p>
    </div> -->
    </div>
    <div class="total">
      <div>合计：<span class="amount">1000.00</span></div>
    </div>
    <script>
      const goodsList = [
        {
          id: '4001172',
          name: '称心如意手摇咖啡磨豆机咖啡豆研磨机',
          price: 289.9,
          picture:
            'https://yanxuan-item.nosdn.127.net/84a59ff9c58a77032564e61f716846d6.jpg',
          count: 2,
          spec: { color: '白色' },
        },
        {
          id: '4001009',
          name: '竹制干泡茶盘正方形沥水茶台品茶盘',
          price: 109.8,
          picture:
            'https://yanxuan-item.nosdn.127.net/2d942d6bc94f1e230763e1a5a3b379e1.png',
          count: 3,
          spec: { size: '40cm*40cm', color: '黑色' },
        },
        {
          id: '4001874',
          name: '古法温酒汝瓷酒具套装白酒杯莲花温酒器',
          price: 488,
          picture:
            'https://yanxuan-item.nosdn.127.net/44e51622800e4fceb6bee8e616da85fd.png',
          count: 1,
          spec: { color: '青色', sum: '一大四小' },
        },
        {
          id: '4001649',
          name: '大师监制龙泉青瓷茶叶罐',
          price: 139,
          picture:
            'https://yanxuan-item.nosdn.127.net/4356c9fc150753775fe56b465314f1eb.png',
          count: 1,
          spec: { size: '小号', color: '紫色' },
          gift: '50g茶叶,清洗球',
        },
      ]

      // 根据数据渲染页面
      const listEL = document.querySelector('.list')
      const res = goodsList.map(function (item) {
        // 解构
        const { picture, price, name, count, spec, gift } = item
        // 处理spec的数据
        const text = Object.values(spec).join('/')
        // 处理gift模块
        // 注意 :gift有些元素没有gift字段,所以需要三元表达式,进行判断
        const gifts = gift ? gift.split(',').map((item) => `<span class="tag">【赠品】${item}</span>`).join('') : ''
        // 小计模块
        // *100 是因为小数的精度问题,先转为整数
        const subTotal = ((price * 100 * count) / 100).toFixed(2)
        return `
                      <div class="item">
                    <img src="${picture}" alt="">
                    <p class="name">${name} ${gifts}</p>
                    <p class="spec">${text}</p>
                    <p class="price">${price}</p>
                    <p class="count">x${count}</p>
                    <p class="sub-total">${subTotal}</p>
                  </div>
              `
      })
      listEL.innerHTML = res.join('')
      const total = goodsList.reduce(function (pre,cur) {
        return pre + (cur.count * 100 * cur.price ) / 100
      }, 0)
      document.querySelector('.amount').innerHTML = total.toFixed(2)
    </script>
  </body>
```

## 四、作业

PC端地址： https://ks.wjx.top/vj/QG54lSj.aspx

![image-20220810162645912](JavaScript%20%E8%BF%9B%E9%98%B6%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%9E%84%E9%80%A0%E5%87%BD%E6%95%B0&%E6%95%B0%E6%8D%AE%E5%B8%B8%E7%94%A8%E5%87%BD%E6%95%B0.assets/image-20220810162645912.png)
