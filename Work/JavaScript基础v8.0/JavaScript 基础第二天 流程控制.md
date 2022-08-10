# JavaScript 基础第二天 流程控制

## 一、运算符

### 1.1 赋值运算符

![image-20220809193531267](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%B5%81%E7%A8%8B%E6%8E%A7%E5%88%B6.assets/image-20220809193531267.png)



```html

<body>
  <script>

    let num = 1
    // num = num + 1
    // 采取赋值运算符
    // num += 1
    num += 3
    console.log(num)
  </script>
</body>

```

### 1.2一元运算符

![image-20220714210606515](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%B5%81%E7%A8%8B%E6%8E%A7%E5%88%B6.assets/image-20220714210606515.png)

![image-20220714210636788](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%B5%81%E7%A8%8B%E6%8E%A7%E5%88%B6.assets/image-20220714210636788.png)

```html
  <script>
    // let num = 10
    // num = num + 1
    // num += 1
    // // 1. 前置自增
    // let i = 1
    // ++i
    // console.log(i)

    // let i = 1
    // console.log(++i + 1)
    // 2. 后置自增
    // let i = 1
    // i++
    // console.log(i)
    // let i = 1
    // console.log(i++ + 1)

    // 了解 
    let i = 1
    console.log(i++ + ++i + i)
  </script>
```

### 1.3比较运算符

![image-20220714210739690](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%B5%81%E7%A8%8B%E6%8E%A7%E5%88%B6.assets/image-20220714210739690.png)

![image-20220714210755195](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%B5%81%E7%A8%8B%E6%8E%A7%E5%88%B6.assets/image-20220714210755195.png)

![image-20220714210809788](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%B5%81%E7%A8%8B%E6%8E%A7%E5%88%B6.assets/image-20220714210809788.png)

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

    console.log(3 > 5)
    console.log(3 >= 3)
    console.log(2 == 2)
    // 比较运算符有隐式转换 把'2' 转换为 2  双等号 只判断值
    console.log(2 == '2')  // true
    // console.log(undefined === null)
    // === 全等 判断 值 和 数据类型都一样才行
    // 以后判断是否相等 请用 ===  
    console.log(2 === '2')
    console.log(NaN === NaN) // NaN 不等于任何人，包括他自己
    console.log(2 !== '2')  // true  
    console.log(2 != '2') // false 
    console.log('-------------------------')
    console.log('a' < 'b') // true
    console.log('aa' < 'ab') // true
    console.log('aa' < 'aac') // true
    console.log('-------------------------')
  </script>
</body>

</html>
```

### 1.4 逻辑运算符

![image-20220714210922047](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%B5%81%E7%A8%8B%E6%8E%A7%E5%88%B6.assets/image-20220714210922047.png)

![image-20220714210934880](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%B5%81%E7%A8%8B%E6%8E%A7%E5%88%B6.assets/image-20220714210934880.png)





![image-20220714210955152](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%B5%81%E7%A8%8B%E6%8E%A7%E5%88%B6.assets/image-20220714210955152.png)

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
    // 1. 用户输入
    let num = +prompt('请输入一个数字:')
    // 2. 弹出结果
    alert(num % 4 === 0 && num % 100 !== 0)
  </script>
</body>

</html>
```

### 1.5运算符优先级

![image-20220714211130297](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%B5%81%E7%A8%8B%E6%8E%A7%E5%88%B6.assets/image-20220714211130297.png)

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
    // 逻辑与 一假则假
    console.log(true && true)
    console.log(false && true)
    console.log(3 < 5 && 3 > 2)
    console.log(3 < 5 && 3 < 2)
    console.log('-----------------')
    // 逻辑或 一真则真
    console.log(true || true)
    console.log(false || true)
    console.log(false || false)
    console.log('-----------------')
    // 逻辑非  取反
    console.log(!true)
    console.log(!false)

    console.log('-----------------')

    let num = 6
    console.log(num > 5 && num < 10)
    console.log('-----------------')
  </script>
</body>

</html>
```

## 二、语句

### 2.1表达式和语句

![image-20220715194051483](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%B5%81%E7%A8%8B%E6%8E%A7%E5%88%B6.assets/image-20220715194051483.png)

### 2.2分支语句

![image-20220715194135635](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%B5%81%E7%A8%8B%E6%8E%A7%E5%88%B6.assets/image-20220715194135635.png)

![image-20220715194156199](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%B5%81%E7%A8%8B%E6%8E%A7%E5%88%B6.assets/image-20220715194156199.png)

#### 2.2.1 if语句

##### 2.2.1.1if单分支语句

![image-20220715194242588](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%B5%81%E7%A8%8B%E6%8E%A7%E5%88%B6.assets/image-20220715194242588.png)

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
    // 单分支语句
    // if (false) {
    //   console.log('执行语句')
    // }
    // if (3 > 5) {
    //   console.log('执行语句')
    // }
    // if (2 === '2') {
    //   console.log('执行语句')
    // }
    //  1. 除了0 所有的数字都为真
    //   if (0) {
    //     console.log('执行语句')
    //   }
    // 2.除了 '' 所有的字符串都为真 true
    // if ('pink老师') {
    //   console.log('执行语句')
    // }
    // if ('') {
    //   console.log('执行语句')
    // }
    // // if ('') console.log('执行语句')

    // 1. 用户输入
    let score = +prompt('请输入成绩')
    // 2. 进行判断输出
    if (score >= 700) {
      alert('恭喜考入黑马程序员')
    }
    console.log('-----------------')

  </script>
</body>

</html>
```

##### 2.2.1.2if多分支语句

![image-20220715194253591](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%B5%81%E7%A8%8B%E6%8E%A7%E5%88%B6.assets/image-20220715194253591.png)

![image-20220715194506783](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%B5%81%E7%A8%8B%E6%8E%A7%E5%88%B6.assets/image-20220715194506783.png)

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
    // 1. 用户输入
    let uname = prompt('请输入用户名:')
    let pwd = prompt('请输入密码:')
    // 2. 判断输出
    if (uname === 'pink' && pwd === '123456') {
      alert('恭喜登录成功')
    } else {
      alert('用户名或者密码错误')
    }
  </script>
</body>

</html>
```

![image-20220715194656270](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%B5%81%E7%A8%8B%E6%8E%A7%E5%88%B6.assets/image-20220715194656270.png)

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
    // 1. 用户输入
    let year = +prompt('请输入年份')
    // 2. 判断输出
    if (year % 4 === 0 && year % 100 !== 0 || year % 400 === 0) {
      alert(`${year}年是闰年`)
    } else {
      alert(`${year}年是平年`)
    }
  </script>
</body>

</html>
```

##### 2.2.1.3if多分支语句

![image-20220715194821694](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%B5%81%E7%A8%8B%E6%8E%A7%E5%88%B6.assets/image-20220715194821694.png)

![image-20220715194830604](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%B5%81%E7%A8%8B%E6%8E%A7%E5%88%B6.assets/image-20220715194830604.png)

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
    // 1. 用户输入
    let score = +prompt('请输入成绩：')
    // 2. 判断输出
    if (score >= 90) {
      alert('成绩优秀，宝贝，你是我的骄傲')
    } else if (score >= 70) {
      alert('成绩良好，宝贝，你要加油哦~~')
    } else if (score >= 60) {
      alert('成绩及格，宝贝，你很危险~')
    } else {
      alert('成绩不及格，宝贝，我不想和你说话，我只想用鞭子和你说话~')
    }
  </script>
</body>

</html>
```

#### 2.2.2三元运算符

![image-20220715195451986](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%B5%81%E7%A8%8B%E6%8E%A7%E5%88%B6.assets/image-20220715195451986.png)

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
    // 三元运算符
    // 条件 ? 代码1 : 代码2
    // console.log(3 > 5 ? 3 : 5)
    // if (3 < 5) {
    //   alert('真的')
    // } else {
    //   alert('假的')
    // }
    // 3 < 5 ? alert('真的')  : alert('假的')

    let sum = 3 < 5 ? 3 : 5
    console.log(sum)
  </script>
</body>

</html>
```

![image-20220715195501946](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%B5%81%E7%A8%8B%E6%8E%A7%E5%88%B6.assets/image-20220715195501946.png)

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
    // 1. 用户输入
    let num1 = +prompt('请您输入第一个数：')
    let num2 = +prompt('请您输入第二个数：')
    // 2. 判断输出-三元运算符
    // if (num1 > num2) {
    //   alert(num1)
    // } else {
    //   alert(num2)
    // }
    num1 > num2 ? alert(`最大值是: ${num1}`) : alert(`最大值是: ${num2}`)
  </script>
</body>

</html>
```

![image-20220715195603534](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%B5%81%E7%A8%8B%E6%8E%A7%E5%88%B6.assets/image-20220715195603534.png)

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
    // let age = 18 
    // age = age + 1
    //  age++

    // 1. 用户输入 
    let num = prompt('请您输入一个数字:')
    // 2. 判断输出- 小于10才补0
    // num = num < 10 ? 0 + num : num
    num = num >= 10 ? num : 0 + num
    alert(num)

  </script>
</body>

</html>
```

#### 2.2.3Swich语句

![image-20220715195903275](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%B5%81%E7%A8%8B%E6%8E%A7%E5%88%B6.assets/image-20220715195903275.png)

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
    switch (2) {
      case 1:
        console.log('您选择的是1')
        break  // 退出switch
      case 2:
        console.log('您选择的是2')
        break  // 退出switch
      case 3:
        console.log('您选择的是3')
        break  // 退出switch
      default:
        console.log('没有符合条件的')
    }
  </script>
</body>

</html>
```

![image-20220715200630663](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%B5%81%E7%A8%8B%E6%8E%A7%E5%88%B6.assets/image-20220715200630663.png)

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
    // 1.用户输入  2个数字 +  操作符号  + - *  / 
    let num1 = +prompt('请您输入第一个数字:')
    let num2 = +prompt('请您输入第二个数字:')
    let sp = prompt('请您输入 + - * / 其中一个:')
    // 2. 判断输出
    switch (sp) {
      case '+':
        alert(`两个数的加法操作是${num1 + num2}`)
        break
      case '-':
        alert(`两个数的减法操作是${num1 - num2}`)
        break
      case '*':
        alert(`两个数的乘法操作是${num1 * num2}`)
        break
      case '/':
        alert(`两个数的除法操作是${num1 / num2}`)
        break
      default:
        alert(`你干啥咧，请输入+-*/`)

    } 
  </script>
</body>

</html>
```

### 2.3循环结构

#### 2.3.1断点测试

![image-20220715200939843](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%B5%81%E7%A8%8B%E6%8E%A7%E5%88%B6.assets/image-20220715200939843.png)

#### 2.3.2While循环

![image-20220715201016187](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%B5%81%E7%A8%8B%E6%8E%A7%E5%88%B6.assets/image-20220715201016187.png)

![image-20220715201307018](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%B5%81%E7%A8%8B%E6%8E%A7%E5%88%B6.assets/image-20220715201307018.png)

![image-20220715201412234](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%B5%81%E7%A8%8B%E6%8E%A7%E5%88%B6.assets/image-20220715201412234.png)

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
    // let age = 18
    // age = age + 1
    // age += 1
    // 1. 页面输出1~100
    // let i = 1
    // while (i <= 100) {
    //   document.write(`这是第${i}个数<br>`)
    //   i++
    // }
    // 2. 页面输出1~100 累加和
    // let i = 1  // 变量的起始值
    // let sum = 0  // 累加和变量
    // while (i <= 100) {
    //   // 把i 累加到 sum 里面
    //   // sum = sum + i
    //   sum += i
    //   i++
    // }
    // console.log(sum) // 5050
    // 3. 页面输出1~100 偶数和
    let i = 1
    let sum = 0
    while (i <= 100) {
      // 筛选偶数 只有偶数才累加
      if (i % 2 === 0) {
        sum = sum + i
      }
      // 每次循环都要自加
      i++
    }
    console.log(sum)
  </script>
</body>

</html>
```

### 2.4循环退出

![image-20220715201611121](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%B5%81%E7%A8%8B%E6%8E%A7%E5%88%B6.assets/image-20220715201611121.png)

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
    // let i = 1
    // while (i <= 5) {
    //   console.log(i)
    //   if (i === 3) {
    //     break  // 退出循环
    //   }
    //   i++

    // }


    let i = 1
    while (i <= 5) {
      if (i === 3) {
        i++
        continue
      }
      console.log(i)
      i++

    }
  </script>
</body>

</html>
```

![image-20220715201630032](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%B5%81%E7%A8%8B%E6%8E%A7%E5%88%B6.assets/image-20220715201630032.png)

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
    while (true) {
      let str = prompt('你爱我吗')
      // 退出条件 爱
      if (str === '爱') {
        break
      }
    }
  </script>
</body>

</html>
```

![image-20220715201801519](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%B5%81%E7%A8%8B%E6%8E%A7%E5%88%B6.assets/image-20220715201801519.png)

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
    // 1. 开始循环 输入框写到 循环里面
    // 3. 准备一个总的金额
    let money = 100
    while (true) {
      let re = +prompt(`
        请您选择操作：
        1.存钱
        2.取钱
        3.查看余额
        4.退出
        `)
      // 2. 如果用户输入的 4 则退出循环， break  写到if 里面，没有写到switch里面， 因为4需要break退出循环
      if (re === 4) {
        break
      }
      // 4. 根据输入做操作
      switch (re) {
        case 1:
          // 存钱
          let cun = +prompt('请输入存款金额')
          money = money + cun
          break
        case 2:
          // 存钱
          let qu = +prompt('请输入取款金额')
          money = money - qu
          break
        case 3:
          // 存钱
          alert(`您的银行卡余额是${money}`)
          break
      }
    }
  </script>
</body>

</html>
```

 pc端地址：https://ks.wjx.top/vj/h46xYbn.aspx

![image-20220715201917256](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%8C%E5%A4%A9%20%E6%B5%81%E7%A8%8B%E6%8E%A7%E5%88%B6.assets/image-20220715201917256.png)
