# JavaScript 基础第五天 对象

## 一、对象

### 1.什么是对象

对象是 JavaScript 数据类型的一种，之前已经学习了数值类型、字符串类型、布尔类型、undefined。对象数据类型可以被理解成是一种数据集合。它由属性和方法两部分构成。

![image-20220720221423826](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%94%E5%A4%A9%20%E5%AF%B9%E8%B1%A1.assets/image-20220720221423826.png)

### 2.对象使用

#### 2.1对象声明语法

声明对象，并添加了若干属性后，可以使用 `.` 或 `[]` 获得对象中属性对应的值，我称之为属性访问。

声明一个对象类型的变量与之前声明一个数值或字符串类型的变量没有本质上的区别。

![image-20220720221621456](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%94%E5%A4%A9%20%E5%AF%B9%E8%B1%A1.assets/image-20220720221621456.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>JavaScript 基础 - 对象语法</title>
</head>
<body>

  <script>
    // 声明字符串类型变量
    let str = 'hello world!'
    
    // 声明数值类型变量
    let num = 199

    // 声明对象类型变量，使用一对花括号
    // user 便是一个对象了，目前它是一个空对象
    let user = {}
  </script>
</body>
</html>
```



#### 2.2对象有属性和方法组成

数据描述性的信息称为属性，如人的姓名、身高、年龄、性别等，一般是名词性的。

1. 属性都是成 对出现的，包括属性名和值，它们之间使用英文 `:` 分隔

2. 多个属性之间使用英文 `,` 分隔

3. 属性就是依附在对象上的变量

4. 属性名可以使用 `""` 或 `''`，一般情况下省略，除非名称遇到特殊符号如空格、中横线等

   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
     <meta charset="UTF-8">
     <title>JavaScript 基础 - 对象语法</title>
   </head>
   <body>
   
     <script>
       // 通过对象描述一个人的数据信息
       // person 是一个对象，它包含了一个属性 name
       // 属性都是成对出现的，属性名 和 值，它们之间使用英文 : 分隔
       let person = {
         name: '小明', // 描述人的姓名
         age: 18, // 描述人的年龄
         stature: 185, // 描述人的身高
         gender: '男', // 描述人的性别
       }
     </script>
   </body>
   </html>
   ```

   

![image-20220720221649188](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%94%E5%A4%A9%20%E5%AF%B9%E8%B1%A1.assets/image-20220720221649188.png)

#### 2.3对象的使用增删改查

![image-20220720222135456](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%94%E5%A4%A9%20%E5%AF%B9%E8%B1%A1.assets/image-20220720222135456.png)

![image-20220720222216403](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%94%E5%A4%A9%20%E5%AF%B9%E8%B1%A1.assets/image-20220720222216403.png)

![image-20220720222226290](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%94%E5%A4%A9%20%E5%AF%B9%E8%B1%A1.assets/image-20220720222226290.png)

![image-20220720222206522](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%94%E5%A4%A9%20%E5%AF%B9%E8%B1%A1.assets/image-20220720222206522.png)

![image-20220720222156512](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%94%E5%A4%A9%20%E5%AF%B9%E8%B1%A1.assets/image-20220720222156512.png)

![image-20220720222445321](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%94%E5%A4%A9%20%E5%AF%B9%E8%B1%A1.assets/image-20220720222445321.png)

![image-20220720222459801](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%94%E5%A4%A9%20%E5%AF%B9%E8%B1%A1.assets/image-20220720222459801.png)

#### 2.4总结

![image-20220720222339744](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%94%E5%A4%A9%20%E5%AF%B9%E8%B1%A1.assets/image-20220720222339744.png)

![image-20220720222521413](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%94%E5%A4%A9%20%E5%AF%B9%E8%B1%A1.assets/image-20220720222521413.png)



#### 2.5对象中的方法

![image-20220720222557848](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%94%E5%A4%A9%20%E5%AF%B9%E8%B1%A1.assets/image-20220720222557848.png)

![image-20220720222627110](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%94%E5%A4%A9%20%E5%AF%B9%E8%B1%A1.assets/image-20220720222627110.png)

##### 2.5.1对象中的方法的总结

![image-20220720222656461](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%94%E5%A4%A9%20%E5%AF%B9%E8%B1%A1.assets/image-20220720222656461.png)

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
    // 1.声明对象
    // let pink = {
    //   uname: 'pink老师',
    //   age: 18,
    //   gender: '女'
    // }
    // // console.log(pink)
    // // console.log(typeof pink)
    // // 改 把性别的女改为男
    // pink.gender = '男'
    // console.log(pink)
    // // 增
    // pink.hobby = '足球'
    // console.log(pink)
    // // 删 (了解)
    // delete pink.age
    // console.log(pink)
    // // let num = 10
    // num = 20
    // console.log(num)
    // 1. 声明
    // console.log(window.name)
    let obj = {
      'goods-name': '小米10青春版',
      num: '100012816024',
      weight: '0.55kg',
      address: '中国大陆'
    }
    obj.name = '小米10 PLUS'
    obj.color = '粉色'
    // console.log(obj.name)
    console.log(obj.num)
    console.log(obj.weight)
    console.log(obj.address)
    console.log(obj.color)
    // console.log(obj.goods - name)
    // 查的另外一种属性：
    // 对象名['属性名']
    console.log(obj['goods-name'])


    // 查总结：
    // (1) 对象名.属性名  obj.age
    console.log(obj.num)
    // (2) 对象名['属性名']  obj['age']
    console.log(obj['num'])





    // // console.log(address)
    // // 2. 使用属性 查  对象名.属性名
    // console.log(obj.address)
    // console.log(obj.name)


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
    let obj = {
      uname: '刘德华',
      // 方法
      song: function (x, y) {
        // console.log('冰雨')
        console.log(x + y)
      },
      dance: function () { }
    }
    // 方法调用 对象名.方法名
    // console.log(obj.song(1, 2))
    obj.song(1, 2)

    // document.write('123')
  </script>
</body>

</html>
```

### 3.遍历对象

#### 1.定义

![image-20220720222843833](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%94%E5%A4%A9%20%E5%AF%B9%E8%B1%A1.assets/image-20220720222843833.png)



![image-20220720223124737](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%94%E5%A4%A9%20%E5%AF%B9%E8%B1%A1.assets/image-20220720223124737.png)

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
    let students = [
      { name: '小明', age: 18, gender: '男', hometown: '河北省' },
      { name: '小红', age: 19, gender: '女', hometown: '河南省' },
      { name: '小刚', age: 17, gender: '男', hometown: '山西省' },
      { name: '小丽', age: 18, gender: '女', hometown: '山东省' }
    ]
    for (let i = 0; i < students.length; i++) {
      // console.log(i)  // 下标索引号
      // console.log(students[i]) // 每个对象
      console.log(students[i].name)
      console.log(students[i].hometown)
    }
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
    // for in 我们不推荐遍历数组
    // let arr = ['pink', 'red', 'blue']
    // for (let k in arr) {
    //   console.log(k)  // 数组的下标 索引号  但是是字符串 '0'
    //   console.log(arr[k])  // arr[k]
    // }
    // 1. 遍历对象 for in   
    let obj = {
      uname: 'pink老师',
      age: 18,
      gender: '男'
    }
    // 2. 遍历对象
    for (let k in obj) {
      console.log(k) // 属性名  'uname'   'age'
      // console.log(obj.uname)
      // console.log(obj.k)
      // console.log(obj.'uname')
      // console.log(obj['uname'])   'uname'  === k
      console.log(obj[k])  // 输出属性值  obj[k]
    }
  </script>
</body>

</html>
```

#### 2.总结

![image-20220720223133442](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%94%E5%A4%A9%20%E5%AF%B9%E8%B1%A1.assets/image-20220720223133442.png)

#### 3.练习

![image-20220720223412579](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%94%E5%A4%A9%20%E5%AF%B9%E8%B1%A1.assets/image-20220720223412579.png)

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        table {
            width: 600px;
            text-align: center;
        }

        table,
        th,
        td {
            border: 1px solid #ccc;
            border-collapse: collapse;
        }

        caption {
            font-size: 18px;
            margin-bottom: 10px;
            font-weight: 700;
        }

        tr {
            height: 40px;
            cursor: pointer;
        }

        table tr:nth-child(1) {
            background-color: #ddd;
        }

        table tr:not(:first-child):hover {
            background-color: #eee;
        }
    </style>
</head>

<body>
    <h2>学生信息</h2>
    <p>将数据渲染到页面中...</p>

    <table>
        <caption>学生列表</caption>
        <tr>
            <th>序号</th>
            <th>姓名</th>
            <th>年龄</th>
            <th>性别</th>
            <th>家乡</th>
        </tr>
        <!-- script写到这里 -->
        <script>
            // 1. 数据准备
            let students = [
                { name: '小明', age: 18, gender: '男', hometown: '河北省' },
                { name: '小红', age: 19, gender: '女', hometown: '河南省' },
                { name: '小刚', age: 17, gender: '男', hometown: '山西省' },
                { name: '小丽', age: 18, gender: '女', hometown: '山东省' },
                { name: '晓强', age: 16, gender: '女', hometown: '蓝翔技校' }
            ]
            // 2. 渲染页面
            for (let i = 0; i < students.length; i++) {
                document.write(`
                <tr>
                    <td>${i + 1}</td>
                    <td>${students[i].name}</td>
                    <td>${students[i].age}</td>
                    <td>${students[i].gender}</td>
                    <td>${students[i].hometown}</td>
                </tr>
                `)
            }
        </script>
    </table>

</body>


</html>
```

### 4.内置对象

#### 1.内置对象是什么

回想一下我们曾经使用过的 `console.log`，`console`其实就是 JavaScript 中内置的对象，该对象中存在一个方法叫 `log`，然后调用 `log` 这个方法，即 `console.log()`。

除了 `console` 对象外，JavaScritp 还有其它的内置的对象

![image-20220720223559030](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%94%E5%A4%A9%20%E5%AF%B9%E8%B1%A1.assets/image-20220720223559030.png)

#### 2.内置对象-Math

`Math` 是 JavaScript 中内置的对象，称为数学对象，这个对象下即包含了属性，也包含了许多的方法。

![image-20220720223627021](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%94%E5%A4%A9%20%E5%AF%B9%E8%B1%A1.assets/image-20220720223627021.png)

#### 属性

- Math.PI，获取圆周率

```javascript
// 圆周率
console.log(Math.PI);
```

#### 方法

- Math.random，生成 0 到 1 间的随机数

```javascript
// 0 ~ 1 之间的随机数, 包含 0 不包含 1
Math.random()
```

- Math.ceil，数字向上取整

```javascript
// 舍弃小数部分，整数部分加1
Math.ceil(3.4)
```

- Math.floor，数字向下取整

```javascript
// 舍弃小数部分，整数部分不变
Math.floor(4.68)
```

- Math.round，四舍五入取整

```javascript
// 取整，四舍五入原则
Math.round(5.46539)
Math.round(4.849)
```

- Math.max，在一组数中找出最大的

```javascript
// 找出最大值
Math.max(10, 21, 7, 24, 13)
```

- Math.min，在一组数中找出最小的

```javascript
// 找出最小值
Math.min(24, 18, 6, 19, 21)
```

- Math.pow，幂方法

```javascript
// 求某个数的多少次方
Math.pow(4, 2) // 求 4 的 2 次方
Math.pow(2, 3) // 求 2 的 3 次方
```

- Math.sqrt，平方根

```javascript
// 求某数的平方根
Math.sqrt(16)
```

数学对象提供了比较多的方法，这里不要求强记，通过演示数学对象的使用，加深对对象的理解。

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
    // 属性
    console.log(Math.PI)
    // 方法
    // ceil 天花板  向上取整
    console.log(Math.ceil(1.1)) // 2 
    console.log(Math.ceil(1.5)) // 2 
    console.log(Math.ceil(1.9)) // 2 
    // floor 地板  向下取整
    console.log(Math.floor(1.1))  // 1
    console.log(Math.floor(1.5))  // 1
    console.log(Math.floor(1.9))  // 1
    console.log(Math.floor('12px'))  // 1
    console.log('----------------')
    // 四舍五入 round
    console.log(Math.round(1.1))  // 1
    console.log(Math.round(1.49))  // 1
    console.log(Math.round(1.5))  // 2
    console.log(Math.round(1.9))  // 2
    console.log(Math.round(-1.1))  // -1 
    console.log(Math.round(-1.5))  // -1
    console.log(Math.round(-1.51))  // -2

    // 取整函数 parseInt(1.2)   // 1
    // 取整函数 parseInt('12px')   // 12

    console.log(Math.max(1, 2, 3, 4, 5))
    console.log(Math.min(1, 2, 3, 4, 5))
    console.log(Math.abs(-1));

    // null  类似 let obj = {}
    let obj = null 
  </script>
</body>

</html>
```

#### 3.内置对象-生成任意范围随机数

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
    // 左闭右开 能取到 0 但是取不到 1 中间的一个随机小数
    // console.log(Math.random())

    // 0~ 10 之间的整数
    // console.log(Math.floor(Math.random() * 11))
    // let arr = ['red', 'green', 'blue']
    // let random = Math.floor(Math.random() * arr.length)
    // // console.log(random)
    // console.log(arr[random])
    // 取到 N ~ M 的随机整数
    function getRandom(N, M) {
      return Math.floor(Math.random() * (M - N + 1)) + N
    }
    console.log(getRandom(4, 8))
  </script>
</body>

</html>
```

#### 4.案例

##### 4.1随机点名案例

![image-20220720223829700](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%94%E5%A4%A9%20%E5%AF%B9%E8%B1%A1.assets/image-20220720223829700.png)

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
    let arr = ['赵云', '黄忠', '关羽', '张飞', '马超', '刘备', '曹操']
    // 1. 得到一个随机数， 作为数组的索引号， 这个随机数 0~6
    let random = Math.floor(Math.random() * arr.length)
    // 2. 页面输出数组里面的元素 
    document.write(arr[random])

    // 3. splice(起始位置(下标), 删除几个元素)
    arr.splice(random, 1)
    console.log(arr)
  </script>
</body>

</html>
```

##### 4.2猜数字游戏

![image-20220720223843823](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%94%E5%A4%A9%20%E5%AF%B9%E8%B1%A1.assets/image-20220720223843823.png)

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
    // 1. 随机生成一个数字 1~10
    // 取到 N ~ M 的随机整数
    function getRandom(N, M) {
      return Math.floor(Math.random() * (M - N + 1)) + N
    }
    let random = getRandom(1, 10)
    console.log(random)
    // 需要不断的循环
    while (true) {
      // 2. 用户输入一个值
      let num = +prompt('请输入你猜的数字:')
      // 3. 判断输出
      if (num > random) {
        alert('您猜大了')
      } else if (num < random) {
        alert('您猜小了')
      } else {
        alert('猜对啦，真厉害')
        break  // 退出循环
      }
    }
  </script>
</body>

</html>
```

![image-20220720223921358](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%94%E5%A4%A9%20%E5%AF%B9%E8%B1%A1.assets/image-20220720223921358.png)

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
    // 1. 随机生成一个数字 1~10
    // 取到 N ~ M 的随机整数
    function getRandom(N, M) {
      return Math.floor(Math.random() * (M - N + 1)) + N
    }
    let random = getRandom(1, 10)
    // 2. 设定三次  三次没猜对就直接退出
    let flag = true  // 开关变量 
    for (let i = 1; i <= 3; i++) {
      let num = +prompt('请输入1~10之间的一个数字:')
      if (num > random) {
        alert('您猜大了，继续')
      } else if (num < random) {
        alert('您猜小了，继续')
      } else {
        flag = false
        alert('猜对了，真厉害')
        break
      }
    }
    // 写到for的外面来
    if (flag) {
      alert('次数已经用完')
    }
  </script>
</body>

</html>
```

##### 4.3生成随机颜色

![image-20220720224024935](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%94%E5%A4%A9%20%E5%AF%B9%E8%B1%A1.assets/image-20220720224024935.png)

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
      width: 300px;
      height: 300px;

    }
  </style>
</head>

<body>

  <script>
    // 1. 自定义一个随机颜色函数
    function getRandomColor(flag = true) {
      if (flag) {
        // 3. 如果是true 则返回 #ffffff
        let str = '#'
        let arr = ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9', 'a', 'b', 'c', 'd', 'e', 'f']
        // 利用for循环随机抽6次 累加到 str里面
        for (let i = 1; i <= 6; i++) {
          // 每次要随机从数组里面抽取一个  
          // random 是数组的索引号 是随机的
          let random = Math.floor(Math.random() * arr.length)
          // str = str + arr[random]
          str += arr[random]
        }
        return str

      } else {
        // 4. 否则是 false 则返回 rgb(255,255,255)
        let r = Math.floor(Math.random() * 256)  // 55
        let g = Math.floor(Math.random() * 256)  // 89
        let b = Math.floor(Math.random() * 256)  // 255
        return `rgb(${r},${g},${b})`
      }

    }
    // 2. 调用函数 getRandomColor(布尔值)
    console.log(getRandomColor(false))
    console.log(getRandomColor(true))
    console.log(getRandomColor())



    // let str = '#'
    // str = str + 'f'


  </script>
</body>

</html>
```



## 二、综合案例

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
    let num1 = 10
    let num2 = num1
    num2 = 20
    console.log(num1) // 结果是？


    let obj1 = {
      age: 18
    }
    let obj2 = obj1
    // 修改属性
    obj2.age = 20
    console.log(obj1.age)
  </script>
</body>

</html>
```

### 1.术语解释

![image-20220720224120645](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%94%E5%A4%A9%20%E5%AF%B9%E8%B1%A1.assets/image-20220720224120645.png)

### 2.基本数据类型和引用数据类型

![image-20220720224128325](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%94%E5%A4%A9%20%E5%AF%B9%E8%B1%A1.assets/image-20220720224128325.png)

### 3.堆栈空间分配区别

![image-20220720224138904](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%94%E5%A4%A9%20%E5%AF%B9%E8%B1%A1.assets/image-20220720224138904.png)

### 4.简单类型的内存分配

![image-20220720224146677](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%94%E5%A4%A9%20%E5%AF%B9%E8%B1%A1.assets/image-20220720224146677.png)

### 5.复杂类型的内存分配

![image-20220720224153481](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%94%E5%A4%A9%20%E5%AF%B9%E8%B1%A1.assets/image-20220720224153481.png)

## 三、复习

PC端地址: https://ks.wjx.top/vj/tHu7X7y.aspx

![image-20220720224210894](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%BA%94%E5%A4%A9%20%E5%AF%B9%E8%B1%A1.assets/image-20220720224210894.png)