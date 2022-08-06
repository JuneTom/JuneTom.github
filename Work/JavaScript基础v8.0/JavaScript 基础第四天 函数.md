# JavaScript 基础第四天 函数

## 一、函数

### 1.为什么需要函数

![image-20220717180424259](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E5%87%BD%E6%95%B0.assets/image-20220717180424259.png)



### 2.函数使用

#### 2.1函数的声明语法

函数可以把具有相同或相似逻辑的代码“包裹”起来，通过函数调用执行这些被“包裹”的代码逻辑，这么做的优势是有利于精简代码方便复用。

#### 声明（定义）

声明（定义）一个完整函数包括关键字、函数名、形式参数、函数体、返回值5个部分

![image-20220720214208969](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E5%87%BD%E6%95%B0.assets/image-20220720214208969.png)



#### 2.2函数名命名规范

![image-20220720191632314](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E5%87%BD%E6%95%B0.assets/image-20220720191632314.png)

![image-20220720191647963](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E5%87%BD%E6%95%B0.assets/image-20220720191647963.png)

#### 2.3函数的调用语法

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>JavaScript 基础 - 声明和调用</title>
</head>
<body>
  <script>
    // 声明（定义）了最简单的函数，既没有形式参数，也没有返回值
    function sayHi() {
      console.log('嗨~')
    }
    // 函数调用，这些函数体内的代码逻辑会被执行
    // 函数名()
        
    sayHi()
    // 可以重复被调用，多少次都可以
    sayHi()
  </script>
</body>
</html>
```

**注：函数名的命名规则与变量是一致的，并且尽量保证函数名的语义。**

![image-20220720191755446](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E5%87%BD%E6%95%B0.assets/image-20220720191755446.png)

#### 2.4函数体

![image-20220720191836128](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E5%87%BD%E6%95%B0.assets/image-20220720191836128.png)

#### 2.3.总结

![image-20220720191913249](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E5%87%BD%E6%95%B0.assets/image-20220720191913249.png)

#### 2.4.课堂练习

![image-20220720191946458](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E5%87%BD%E6%95%B0.assets/image-20220720191946458.png)

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
    // let num = 10
    // console.log(num)
    // 1. 函数的声明   
    function sayHi() {
      console.log('hi~~~')
    }
    // 2. 函数调用   函数不调用，自己不执行
    sayHi()
    sayHi()
    sayHi()
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
  <style>
    span {
      display: inline-block;
      width: 100px;
      padding: 5px 10px;
      border: 1px solid pink;
      margin: 2px;
      border-radius: 5px;
      box-shadow: 2px 2px 2px rgba(255, 192, 203, .4);
      background-color: rgba(255, 192, 203, .1);
      text-align: center;
      color: hotpink;
    }
  </style>
</head>

<body>

  <script>
    // // 1. 外层循环控制行数
    // for (let i = 1; i <= 9; i++) {
    //   // 2. 里层循环控制列数
    //   for (let j = 1; j <= i; j++) {
    //     document.write(`<span>${j} X ${i} = ${i * j}</span>`)
    //   }
    //   // 换行
    //   document.write('<br>')
    // }
    // // 1. 外层循环控制行数
    // for (let i = 1; i <= 9; i++) {
    //   // 2. 里层循环控制列数
    //   for (let j = 1; j <= i; j++) {
    //     document.write(`<span>${j} X ${i} = ${i * j}</span>`)
    //   }
    //   // 换行
    //   document.write('<br>')
    // }
    // // 1. 外层循环控制行数
    // for (let i = 1; i <= 9; i++) {
    //   // 2. 里层循环控制列数
    //   for (let j = 1; j <= i; j++) {
    //     document.write(`<span>${j} X ${i} = ${i * j}</span>`)
    //   }
    //   // 换行
    //   document.write('<br>')
    // }
    // 声明
    function sheet99() {
      for (let i = 1; i <= 9; i++) {
        // 2. 里层循环控制列数
        for (let j = 1; j <= i; j++) {
          document.write(`<span>${j} X ${i} = ${i * j}</span>`)
        }
        // 换行
        document.write('<br>')
      }
    }
    // 调用
    sheet99()
    sheet99()
    sheet99()
    sheet99()
  </script>
</body>

</html>
```

![image-20220720192143614](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E5%87%BD%E6%95%B0.assets/image-20220720192143614.png)

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
    // 1. 求2个数的和
    // function getSum() {
    //   let num1 = +prompt('请输入第一个数')
    //   let num2 = +prompt('请输入第二个数')
    //   console.log(num1 + num2)
    // }
    // getSum()
    // 2. 求 1~100 累加和
    function getSum() {
      let sum = 0
      for (let i = 1; i <= 100; i++) {
        sum += i
      }
      console.log(sum)
    }
    getSum()
  </script>
</body>

</html>
```

### 3.函数的传参

#### 3.1函数传参定义

### 参数

通过向函数传递参数，可以让函数更加灵活多变，参数可以理解成是一个变量。

声明（定义）一个功能为打招呼的函数

- 传入数据列表

- 声明这个函数需要传入几个数据

- 多个数据用逗号隔开

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>JavaScript 基础 - 函数参数</title>
  </head>
  <body>
  
    <script>
      // 声明（定义）一个功能为打招呼的函数
      // function sayHi() {
      //   console.log('嗨~')
      // }
      // 调用函数
      // sayHi()
  	
  
      // 这个函数似乎没有什么价值，除非能够向不同的人打招呼
      // 这就需要借助参数来实现了
      function sayHi(name) {
        // 参数 name 可以被理解成是一个变量
        console.log(name)
        console.log('嗨~' + name)
      }
  
      // 调用 sayHi 函数，括号中多了 '小明'
      // 这时相当于为参数 name 赋值了
      sayHi('小明')// 结果为 小明
  
      // 再次调用 sayHi 函数，括号中多了 '小红'
      // 这时相当于为参数 name 赋值了
      sayHi('小红') // 结果为 小红
    </script>
  </body>
  </html>
  ```

  

![image-20220720192343074](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E5%87%BD%E6%95%B0.assets/image-20220720192343074.png)

#### 3.2声明语法

![image-20220720192531193](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E5%87%BD%E6%95%B0.assets/image-20220720192531193.png)

#### 3.3调用语法

![image-20220720192558685](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E5%87%BD%E6%95%B0.assets/image-20220720192558685.png)

#### 3.4总结

总结：

1. 声明（定义）函数时的形参没有数量限制，当有多个形参时使用 `,` 分隔
2. 调用函数传递的实参要与形参的顺序一致

#### 形参和实参

形参：声明函数时写在函数名右边小括号里的叫形参（形式上的参数）

实参：调用函数时写在函数名右边小括号里的叫实参（实际上的参数）

形参可以理解为是在这个函数内声明的变量（比如 num1 = 10）实参可以理解为是给这个变量赋值

开发中尽量保持形参和实参个数一致

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>JavaScript 基础 - 函数参数</title>
</head>
<body>
  <script>
    // 声明（定义）一个计算任意两数字和的函数
    // 形参 x 和 y 分别表示任意两个数字，它们是两个变量
    function count(x, y) {
      console.log(x + y);
    }
    // 调用函数，传入两个具体的数字做为实参
    // 此时 10 赋值给了形参 x
    // 此时 5  赋值给了形参 y
    count(10, 5); // 结果为 15
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
    // 求 n ~ m 的累加和
    function getSum(n = 0, m = 0) {
      let sum = 0
      for (let i = n; i <= m; i++) {
        sum += i
      }
      console.log(sum)
    }
    // getSum()
    // getSum(1, 2)
    let num1 = +prompt('请输入起始值:')
    let num2 = +prompt('请输入结束值:')
    // 调用函数
    getSum(num1, num2)  // 实参可以是变量
  </script>
</body>

</html>
```



![image-20220720192706952](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E5%87%BD%E6%95%B0.assets/image-20220720192706952.png)

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

    // 2. 求 1~100 累加和
    // function getSum(end) {   // end = 50
    //   // console.log(end)
    //   let sum = 0
    //   for (let i = 1; i <= end; i++) {
    //     sum += i
    //   }
    //   console.log(sum)
    // }
    // getSum(50)  // 1~50
    // getSum(100)  // 1~100

    function getSum(start, end) {   // end = 50
      // 形参  形式上的参数  
      // console.log(end)
      let sum = 0
      for (let i = start; i <= end; i++) {
        sum += i
      }
      console.log(sum)
    }
    getSum(1, 50)  // 调用的小括号里面 实参 - 实际的参数
    getSum(100, 200)  // 实参 - 实际的参数
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
    // 函数求和
    // function getSum(x = 0, y = 0) {
    //   // x = 1
    //   // num1 默认的值 undefined
    //   document.write(x + y)
    // }
    // getSum(1, 2)
    // getSum()  // 0
    function getSum(start = 0, end = 0) {   // end = 50
      // 形参  形式上的参数
      // console.log(end)
      let sum = 0
      for (let i = start; i <= end; i++) {
        sum += i
      }
      console.log(sum)
    }
    getSum(1, 50)  // 调用的小括号里面 实参 - 实际的参数
    getSum(100, 200)  // 实参 - 实际的参数
    getSum()
  </script>
</body>

</html>
```



#### 3.5练习

![image-20220720192734954](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E5%87%BD%E6%95%B0.assets/image-20220720192734954.png)

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
    // 1. 封装函数
    // 给一个参数的默认值
    function getArrSum(arr = []) {
      // console.log(arr)
      let sum = 0
      for (let i = 0; i < arr.length; i++) {
        sum += arr[i]
      }
      console.log(sum)
    }
    getArrSum([1, 2, 3, 4, 5])
    getArrSum([11, 22, 33])
    getArrSum()  // 0
  </script>
</body>

</html>
```

#### 3.6函数传参-参数默认值

![image-20220720193223292](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E5%87%BD%E6%95%B0.assets/image-20220720193223292.png)

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
    // 求 n ~ m 的累加和
    function getSum(n = 0, m = 0) {
      let sum = 0
      for (let i = n; i <= m; i++) {
        sum += i
      }
      console.log(sum)
    }
    // getSum()
    // getSum(1, 2)
    let num1 = +prompt('请输入起始值:')
    let num2 = +prompt('请输入结束值:')
    // 调用函数
    getSum(num1, num2)  // 实参可以是变量
  </script>
</body>

</html>
```



### 4.函数返回值

#### 1.什么是函数？

![image-20220720211850234](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E5%87%BD%E6%95%B0.assets/image-20220720211850234.png)

#### 2.函数返回值定义

### 返回值

函数的本质是封装（包裹），函数体内的逻辑执行完毕后，函数外部如何获得函数内部的执行结果呢？要想获得函数内部逻辑的执行结果，需要通过 `return` 这个关键字，将内部执行结果传递到函数外部，这个被传递到外部的结果就是返回值。

![image-20220720211948305](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E5%87%BD%E6%95%B0.assets/image-20220720211948305.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>JavaScript 基础 - 函数返回值</title>
</head>
<body>

  <script>
    // 定义求和函数
    function count(a, b) {
      let s = a + b
      // s 即为 a + b 的结果
      // 通过 return 将 s 传递到外部
      return s
    }

    // 调用函数，如果一个函数有返回值
    // 那么可将这个返回值赋值给外部的任意变量
    let total = count(5, 12)
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
    // // 函数的返回值
    // function fn() {
    //   return 20
    // }
    // // fn() 调用者 相当于执行了    fn()   = 20
    // // return 的值返回给调用者
    // // console.log(fn())
    // // let num = prompt('请输入数字')
    // let re = fn()
    // console.log(re)

    // 求和函数的写法
    function getTotalPrice(x, y) {
      return x + y
      // return 后面的代码不会被执行
    }
    // console.log(getTotalPrice(1, 2))
    // console.log(getTotalPrice(1, 2))
    let sum = getTotalPrice(1, 2)
    console.log(sum)
    console.log(sum)

    function fn() {

    }
    let re = fn()
    console.log(re)  // undefined
  </script>
</body>

</html>
```

#### 3.函数返回值的使用

![image-20220720212108361](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E5%87%BD%E6%95%B0.assets/image-20220720212108361.png)

#### 4.有返回值的函数

![image-20220720212258605](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E5%87%BD%E6%95%B0.assets/image-20220720212258605.png)

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
    // // 函数的返回值
    // function fn() {
    //   return 20
    // }
    // // fn() 调用者 相当于执行了    fn()   = 20
    // // return 的值返回给调用者
    // // console.log(fn())
    // // let num = prompt('请输入数字')
    // let re = fn()
    // console.log(re)

    // 求和函数的写法
    function getTotalPrice(x, y) {
      return x + y
      // return 后面的代码不会被执行
    }
    // console.log(getTotalPrice(1, 2))
    // console.log(getTotalPrice(1, 2))
    let sum = getTotalPrice(1, 2)
    console.log(sum)
    console.log(sum)

    function fn() {

    }
    let re = fn()
    console.log(re)  // undefined
  </script>
</body>

</html>
```



#### 5.总结

1. 在函数体中使用return 关键字能将内部的执行结果交给函数外部使用
2. 函数内部只能出现1 次 return，并且 return 下一行代码不会再被执行，所以return 后面的数据不要换行写
3. return会立即结束当前函数
4. 函数可以没有return，这种情况默认返回值为 undefined

![image-20220720212337503](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E5%87%BD%E6%95%B0.assets/image-20220720212337503.png)

#### 6.练习

![image-20220720212359355](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E5%87%BD%E6%95%B0.assets/image-20220720212359355.png)

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
  <div></div>
  <script>
    // 1. 求最大值函数
    // function getMax(x, y) {
    //   return x > y ? x : y
    // }
    // let max = getMax(11, 234)
    // console.log(max)

    // //  2. 求任意数组的最大值，并且返回
    // function getArrValue(arr = []) {
    //   // (1)先准备一个max变量存放数组的第一个值
    //   let max = arr[0]
    //   // (2) 遍历比较
    //   for (let i = 1; i < arr.length; i++) {
    //     if (max < arr[i]) {
    //       max = arr[i]
    //     }
    //   }
    //   // (3) 返回值
    //   return max
    // }

    // // let max = getArrValue([1, 3, 5, 7, 9])
    // // let num = prompt('请输入')
    // let max = getArrValue([11, 3, 55, 7, 29])
    // console.log(max)
    //  3. 求任意数组的最大值和最小值，并且返回
    function getArrValue(arr = []) {
      // (1)先准备一个max变量存放数组的第一个值
      let max = arr[0]
      let min = arr[0]  // 最小值
      // (2) 遍历比较
      for (let i = 1; i < arr.length; i++) {
        // 最大值
        if (max < arr[i]) {
          max = arr[i]
        }
        // 最小值
        if (min > arr[i]) {
          min = arr[i]
        }
      }
      // (3) 返回值  返回的是数组
      return [max, min]
      // return min
    }
    let newArr = getArrValue([11, 3, 55, 7, 29])
    console.log(`数组的最大值是: ${newArr[0]}`)
    console.log(`数组的最小值是: ${newArr[1]}`)
  </script>
</body>

</html>
```

#### 7.函数细节补充

![image-20220720212509212](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E5%87%BD%E6%95%B0.assets/image-20220720212509212.png)

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
    // function getSum(x, y) {
    //   return x + y
    //   // 返回值返回给了谁？ 函数的调用者  getSum(1, 2)
    //   // getSum(1, 2) = 3
    // }
    // // let result = getSum(1, 2) = 3
    // // let num = parseInt('12px')
    // let result = getSum(1, 2)
    // console.log(result)
    // 1. 函数名相同， 后面覆盖前面

    // function fn() {
    //   console.log(1)
    // }
    // function fn() {
    //   console.log(2)
    // }
    // fn()
    // 2. 参数不匹配

    function fn(a, b) {
      console.log(a + b)
    }
    // (1). 实参多余形参   剩余的实参不参与运算
    // fn(1, 2, 3)
    // (2). 实参少于形参   剩余的实参不参与运算
    fn(1)   // 1 + undefined  = NaN 
  </script>
</body>

</html>
```



### 5.作用域

#### 1.作用域定义

### 作用域

通常来说，一段程序代码中所用到的名字并不总是有效和可用的，而限定这个名字的可用性的代码范围就是这个名字的作用域。

作用域的使用提高了程序逻辑的局部性，增强了程序的可靠性，减少了名字冲突。

#### 全局作用域

作用于所有代码执行的环境(整个 script 标签内部)或者一个独立的 js 文件

处于全局作用域内的变量，称为全局变量

#### 局部作用域

作用于函数内的代码环境，就是局部作用域。 因为跟函数有关系，所以也称为函数作用域。

处于局部作用域内的变量称为局部变量

**如果函数内部，变量没有声明，直接赋值，也当全局变量看，但是强烈不推荐**

**但是有一种情况，函数内部的形参可以看做是局部变量。**

```htm
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
    let num = 10  // 1. 全局变量
    console.log(num)
    function fn() {
      console.log(num)
    }
    fn()

    // 2. 局部变量
    function fun() {
      let str = 'pink'
    }
    console.log(str)  // 错误
  </script>
</body>

</html>
```



#### 2.根据作用域的不同，变量可以分为

![image-20220720212704351](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E5%87%BD%E6%95%B0.assets/image-20220720212704351.png)

![image-20220720212743966](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E5%87%BD%E6%95%B0.assets/image-20220720212743966.png)

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
    // let num = 20
    // function fn() {
    //   num = 10  // 全局变量来看  强烈不允许
    // }
    // fn()
    // console.log(num)

    // function fun(x, y) {
    //   // 形参可以看做是函数的局部变量
    //   console.log(x)
    // }
    // fun(1, 2)
    // console.log(x)  // 错误的

    // let num = 10
    function fn() {
      // let num = 20
      function fun() {
        // let num = 30
        console.log(num)
      }
      fun()
    }
    fn()
  </script>
</body>

</html>
```



#### 3.总结

![image-20220720212801190](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E5%87%BD%E6%95%B0.assets/image-20220720212801190.png)



4.变量访问原则

![image-20220720212829418](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E5%87%BD%E6%95%B0.assets/image-20220720212829418.png)

![image-20220720213031616](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E5%87%BD%E6%95%B0.assets/image-20220720213031616.png)

### 6.函数

#### 1.函数划分

函数可以分为具名函数和匿名函数

匿名函数：没有名字的函数,无法直接使用。

```js
// 声明
let fn = function() { 
   console.log('函数表达式')
}
// 调用
fn()
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
    // console.log(num)
    // let num = 10

    // 3 + 4
    // num = 10
    // 1. 函数表达式
    fn(1, 2)  //错误
    let fn = function (x, y) {
      // console.log('我是函数表达式')
      console.log(x + y)
    }

    // 函数表达式和 具名函数的不同   function fn() {}
    // 1. 具名函数的调用可以写到任何位置
    // 2. 函数表达式，必须先声明函数表达式，后调用
    // function fun() {
    //   console.log(1)
    // }
    // fun()
  </script>
</body>

</html>
```



#### 2.匿名函数

##### 2.1匿名函数定义

![image-20220720213202275](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E5%87%BD%E6%95%B0.assets/image-20220720213202275.png)



##### 2.2匿名函数表达式

![image-20220720213246543](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E5%87%BD%E6%95%B0.assets/image-20220720213246543.png)

#### 2.立即执行函数

**无需调用，立即执行，其实本质已经调用了**

**多个立即执行函数之间用分号隔开**

```js
(function(){ xxx  })();
(function(){xxxx}());
```



##### 2.1立即执行函数作用

![image-20220720213346778](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E5%87%BD%E6%95%B0.assets/image-20220720213346778.png)

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
    // let num = 10
    // let num = 20
    // (function () {
    //   console.log(11)
    // })()

    // (function () {
    //   let num = 10
    // })();
    // (function () {
    //   let num = 20
    // })();
    // 1. 第一种写法
    (function (x, y) {
      console.log(x + y)
      let num = 10
      let arr = []
    })(1, 2);
    // (function(){})();
    // 2.第二种写法
    // (function () { }());
    (function (x, y) {
      let arr = []
      console.log(x + y)
    }(1, 3));


    // (function(){})()
    // (function(){}())
  </script>
</body>

</html>
```



##### 2.2总结

![image-20220720213420910](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E5%87%BD%E6%95%B0.assets/image-20220720213420910.png)

## 二、综合案例

### 1.转换时间案例

![image-20220720213504639](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E5%87%BD%E6%95%B0.assets/image-20220720213504639.png)

![image-20220720213540449](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E5%87%BD%E6%95%B0.assets/image-20220720213540449.png)

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
    // age = age + 1
    // 1. 用户输入
    let second = +prompt('请输入秒数:')
    // 2.封装函数
    function getTime(t) {
      // console.log(t)  // 总的秒数
      // 3. 转换
      // 小时：  h = parseInt(总秒数 / 60 / 60 % 24)
      // 分钟：  m = parseInt(总秒数 / 60 % 60)
      // 秒数: s = parseInt(总秒数 % 60) 
      let h = parseInt(t / 60 / 60 % 24)
      let m = parseInt(t / 60 % 60)
      let s = parseInt(t % 60)
      h = h < 10 ? '0' + h : h
      m = m < 10 ? '0' + m : m
      s = s < 10 ? '0' + s : s
      // console.log(h, m, s)
      return `转换完毕之后是${h}小时${m}分${s}秒`
    }
    let str = getTime(second)
    document.write(str)
    console.log(h)
  </script>
</body>

</html>
```

### 2.逻辑中断

![image-20220720213721163](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E5%87%BD%E6%95%B0.assets/image-20220720213721163.png)

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
    function fn(x, y) {
      x = x || 0
      y = y || 0
      console.log(x + y)
    }
    fn(1, 2)
    // fn()

    // console.log(false && 22)
    // console.log(false && 3 + 5)
    // let age = 18
    // console.log(false && age++) // age++ 不执行  一假则假
    // console.log(age)

    // console.log(true || age++)
    // console.log(age)


    // console.log(11 && 22)  // 都是真，这返回最后一个真值
    // console.log(11 || 22)  //  输出第一个真值
  </script>
</body>

</html>
```

### 3.逻辑运算符里的短路

![image-20220720213813184](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E5%87%BD%E6%95%B0.assets/image-20220720213813184.png)

### 4.转换为Boolean型

##### 4.1显示转换

![image-20220720213842902](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E5%87%BD%E6%95%B0.assets/image-20220720213842902.png)

4.2隐式转换

![image-20220720213951859](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E5%87%BD%E6%95%B0.assets/image-20220720213951859.png)

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
    console.log(Boolean('pink'))
    console.log(Boolean(''))
    console.log(Boolean(0))
    console.log(Boolean(90))
    console.log(Boolean(-1))
    console.log(Boolean(undefined))
    console.log(Boolean(null))
    console.log(Boolean(NaN))

    console.log('--------------------------')
    let age
    if (age) {
      console.log(11)
    }
  </script>
</body>

</html>
```

## 三、复习

PC端： https://ks.wjx.top/vj/wV1PSkl.aspx

![image-20220720214059916](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E5%87%BD%E6%95%B0.assets/image-20220720214059916.png)