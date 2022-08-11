# JavaScript 基础第三天 数组

## 一、循环--for

### 1. for 循环-基本使用

![image-20220715203425316](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%95%B0%E7%BB%84.assets/image-20220715203425316.png)

![image-20220715203515387](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%95%B0%E7%BB%84.assets/image-20220715203515387.png)

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
    // 1. 输出1~100岁
    // for (let i = 1; i <= 100; i++) {
    //   document.write(`今年我${i}岁了 <br>`)
    // }
    // 2. 求1~100之间的偶数和
    // let sum = 0
    // for (let i = 1; i <= 100; i++) {
    //   if (i % 2 === 0) {
    //     // 把i加到sum里面去
    //     // sum = sum + i
    //     sum += i
    //   }
    // }
    // document.write(`1~100之间的偶数和是: ${sum}`)
    // 3. 页面打印5个小星星
    // for (let i = 1; i <= 5; i++) {
    //   document.write('★')
    // }
    // 4. 打印数组
    let arr = ['刘德华', '刘晓强', '刘晓庆', '刘若英', '刘热巴', 'pink老师']
    // console.log(arr[0])
    // console.log(arr[1])
    // console.log(arr[2])
    // console.log(arr[3])
    // i <= 4    长度 - 1
    // for (let i = 0; i <= arr.length - 1; i++) {
    //   console.log(arr[i])
    // }
    // 必须从0开始，因为数组索引号从0开始  arr.length = 6
    // 遍历数组 ：  从第一个循环到最后一个
    for (let i = 0; i < arr.length; i++) {
      console.log(arr[i])
    }

    let arr1 = []
    console.log(arr1)
    console.log(arr1[0]) // undefined
    console.log(arr1[1]) // undefined
  </script>
</body>

</html>
```

#### 1.1退出循环

![image-20220715203553984](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%95%B0%E7%BB%84.assets/image-20220715203553984.png)



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
    // for (let i = 1; i <= 5; i++) {
    //   if (i === 3) {
    //     continue  // 退出本次循环，本次循环中 continue下面的语句不在执行
    //   }
    //   console.log(i)
    //   document.write(i)
    // }

    // for (let i = 1; i <= 5; i++) {
    //   if (i === 3) {
    //     break  // 退出整个循环 结束循环
    //   }
    //   console.log(i)
    //   document.write(i)
    // }
    // 无限循环
    for (; ;) {
      console.log(11)
    }
  </script>
</body>

</html>
```

#### 1.2for循环和while循环区别

![image-20220715204459215](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%95%B0%E7%BB%84.assets/image-20220715204459215.png)

### 2for 循环嵌套

![image-20220715204950643](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%95%B0%E7%BB%84.assets/image-20220715204950643.png)

#### 2.1假如每天记住5个单词，3天后一共能记住多少单词？

![image-20220715205009757](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%95%B0%E7%BB%84.assets/image-20220715205009757.png)

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
    // 外层循环打印 第 n 天
    for (let i = 1; i <= 3; i++) {
      document.write(`第${i}天<br>`)
      // 里层循环打印 第几个单词
      for (let j = 1; j <= 5; j++) {
        document.write(`记住了第${j}个单词<br>`)
      }
    }
  </script>
</body>

</html>
```

#### 2.2页面中打印出5行5列的星星

![image-20220715205156974](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%95%B0%E7%BB%84.assets/image-20220715205156974.png)

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
    // // 外层循环打印行数
    // for (let i = 1; i <= 5; i++) {
    //   // 里层循环打印几个星星
    //   for (let j = 1; j <= 5; j++) {
    //     document.write('☆')
    //   }
    //   // 进行换行显示
    //   document.write('<br>')
    // }

    let row = +prompt('请输入行数:')
    let col = +prompt('请输入列数:')
    // 外层循环打印行数
    for (let i = 1; i <= row; i++) {
      // 里层循环打印几个星星
      for (let j = 1; j <= col; j++) {
        document.write('☆')
      }
      // 进行换行显示
      document.write('<br>')
    }
  </script>
</body>

</html>
```

#### 2.3打印倒三角形星星

![image-20220715205243471](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%95%B0%E7%BB%84.assets/image-20220715205243471.png)

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
    // 1. 外层循环控制行数
    for (let i = 1; i <= 5; i++) {
      // 2. 里层循环控制列数（几个星星）
      for (let j = 1; j <= i; j++) {
        document.write('◆')
      }
      // 换行
      document.write('<br>')
    }

  </script>
</body>

</html>
```

#### 2.4九九乘法表

![image-20220715205309538](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%95%B0%E7%BB%84.assets/image-20220715205309538.png)

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
    // 1. 外层循环控制行数
    for (let i = 1; i <= 9; i++) {
      // 2. 里层循环控制列数
      for (let j = 1; j <= i; j++) {
        document.write(`<span>${j} X ${i} = ${i * j}</span>`)
      }
      // 换行
      document.write('<br>')
    }

  </script>
</body>

</html>
```

## 二、数组

### 1.数组是什么

![image-20220715205738020](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%95%B0%E7%BB%84.assets/image-20220715205738020.png)

### 2.数组的基本使用

#### 2.1 声明语法

![image-20220811175539283](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%95%B0%E7%BB%84.assets/image-20220811175539283.png)

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
    // 1. 字面量声明数组
    // let arr = [1, 2, 'pink', true]
    // 2. 使用new Array 构造函数声明   了解
    // let arr = new Array(1, 2, 3, 4)
    // console.log(arr)
  </script>
</body>

</html>
```



#### 2.2 取值语法

![image-20220811175616114](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%95%B0%E7%BB%84.assets/image-20220811175616114.png)

#### 2.3 一些术语

![image-20220811175650637](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%95%B0%E7%BB%84.assets/image-20220811175650637.png)

#### 2.4遍历数组(重点)

![image-20220811175731866](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%95%B0%E7%BB%84.assets/image-20220811175731866.png)

#### 2.5练习

##### 2.5.1数组求和

![image-20220811175916909](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%95%B0%E7%BB%84.assets/image-20220811175916909.png)

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
    let arr = [2, 6, 1, 7, 4]
    // 1. 求和的变量 sum
    let sum = 0
    // 2.遍历累加
    for (let i = 0; i < arr.length; i++) {
      // console.log(arr[i])
      // sum = sum + arr[i]
      sum += arr[i]
    }
    console.log(`数组的和的结果是: ${sum}`)
    // 3. 平均值  和 / arr.length  = 4
    console.log(`数组的平均值结果是: ${sum / arr.length}`)


    // sum = sum + arr[0]
    // console.log(sum) 
  </script>
</body>

</html>
```



##### 2.5.2数组求最大值和最小值

![image-20220811175929513](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%95%B0%E7%BB%84.assets/image-20220811175929513.png)

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
    let arr = [2, 6, 1, 7, 400, 55, 88, 100]
    // max里面要存的是最大值
    let max = arr[0]
    // min 要存放的是最小值
    let min = arr[0]
    // 遍历数组
    for (let i = 1; i < arr.length; i++) {
      // 如果max 比 数组元素里面的值小，我们就需要把这元素赋值给 max
      // if (max < arr[i]) max = arr[i]
      max < arr[i] ? max = arr[i] : max
      // 如果min 比 数组元素大， 我们就需要把数组元素给min
      // if (min > arr[i]) {
      //   min = arr[i]
      // }
      min > arr[i] ? min = arr[i] : min
    }
    // 输出 max
    console.log(`最大值是: ${max}`)
    console.log(`最小值是: ${min}`)
  </script>
</body>

</html>
```



### 3.操作数组

![image-20220811180238911](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%95%B0%E7%BB%84.assets/image-20220811180238911.png)

#### 3.1操作数组-新增

##### 3.1.1新增

![image-20220811180307347](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%95%B0%E7%BB%84.assets/image-20220811180307347.png)

![image-20220811180324964](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%95%B0%E7%BB%84.assets/image-20220811180324964.png)

##### 3.1.2总结

![image-20220811180441443](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%95%B0%E7%BB%84.assets/image-20220811180441443.png)

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
    let arr = ['pink', 'hotpink']
    // 新增  push 推末尾
    // console.log(arr.push('deeppink'))  // 3
    // arr.push('deeppinnk', 'linghtpink')
    // console.log(arr)
    // 开头追加
    arr.unshift('red')
    console.log(arr)
  </script>
</body>

</html>
```



##### 3.1.3练习

![image-20220811180520121](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%95%B0%E7%BB%84.assets/image-20220811180520121.png)

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
    // 重点案例
    let arr = [2, 0, 6, 1, 77, 9, 54, 3, 78, 7]
    // 1. 声明新的空的数组
    let newArr = []
    // 2. 遍历旧数组
    for (let i = 0; i < arr.length; i++) {
      if (arr[i] >= 10) {
        // 3. 满足条件 追加给新的数组
        newArr.push(arr[i])
      }
    }
    // 4. 输出新的数组
    console.log(newArr)
  </script>
</body>

</html>
```



![image-20220811180531081](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%95%B0%E7%BB%84.assets/image-20220811180531081.png)

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
    let arr = [2, 0, 6, 1, 77, 0, 52, 0, 25, 7]
    // 1. 声明一个新的数组
    let newArr = []
    // 2. 遍历筛选
    for (let i = 0; i < arr.length; i++) {
      if (arr[i] !== 0) {
        newArr.push(arr[i])
      }
    }
    // 输出新数组
    console.log(newArr)
  </script>
</body>

</html>
```

#### 3.2操作数组-删除

##### 3.2.1删除

![image-20220811180718590](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%95%B0%E7%BB%84.assets/image-20220811180718590.png)

![image-20220811180727062](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%95%B0%E7%BB%84.assets/image-20220811180727062.png)

![image-20220811180738918](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%95%B0%E7%BB%84.assets/image-20220811180738918.png)

##### 3.2.2总结

![image-20220811180847353](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%95%B0%E7%BB%84.assets/image-20220811180847353.png)

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
    let arr = ['red', 'green', 'blue']
    // console.log(arr.pop()) // blue
    // 1.pop() 删除最后一个元素
    // arr.pop()
    // arr.pop()
    // console.log(arr)
    // 2. shift() 删除第一个元素
    // arr.shift()
    // console.log(arr)
    // 3. splice 删除指定元素  splice(起始位置-索引号, 删除几个)
    arr.splice(1, 1)  // 是从索引号1的位置开始删， 只删除1个
    // arr.splice(1) // 从green 删除到最后
    console.log(arr)
  </script>
</body>

</html>
```

#### 3.3操作数组-修改

![image-20220811181625545](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%95%B0%E7%BB%84.assets/image-20220811181625545.png)

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
    // let arr = []
    // console.log(arr)
    // // console.log(arr[0])  // undefined
    // arr[0] = 1
    // arr[1] = 5
    // console.log(arr)
    let arr = ['pink', 'red', 'green']
    // 修改
    // arr[0] = 'hotpink'
    // console.log(arr)
    // 给所有的数组元素后面加个老师  修改
    for (let i = 0; i < arr.length; i++) {
      // console.log(arr[i])
      arr[i] = arr[i] + '老师'
    }
    console.log(arr)

  </script>
</body>

</html>
```



### 4.数组案例(根据数据生成柱形图)

![image-20220811181752310](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%95%B0%E7%BB%84.assets/image-20220811181752310.png)

![image-20220811181825981](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%95%B0%E7%BB%84.assets/image-20220811181825981.png)

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
        }

        .box {
            display: flex;
            width: 700px;
            height: 300px;
            border-left: 1px solid pink;
            border-bottom: 1px solid pink;
            margin: 50px auto;
            justify-content: space-around;
            align-items: flex-end;
            text-align: center;
        }

        .box>div {
            display: flex;
            width: 50px;
            background-color: pink;
            flex-direction: column;
            justify-content: space-between;
        }

        .box div span {

            margin-top: -20px;
        }

        .box div h4 {
            margin-bottom: -35px;
            width: 70px;
            margin-left: -10px;
        }
    </style>
</head>

<body>




    <script>
        // 1. 四次弹框效果
        // 声明一个新的数组
        let arr = []
        for (let i = 1; i <= 4; i++) {
            // let num = prompt(`请输入第${i}季度的数据:`)
            // arr.push(num)
            arr.push(prompt(`请输入第${i}季度的数据:`))
            // push记得加小括号，不是等号赋值的形式
        }
        // console.log(arr)  ['123','135','345','234']
        // 盒子开头
        document.write(` <div class="box">`)

        // 盒子中间 利用循环的形式  跟数组有关系
        for (let i = 0; i < arr.length; i++) {
            document.write(`
              <div style="height: ${arr[i]}px;">
                <span>${arr[i]}</span>
                <h4>第${i + 1}季度</h4>
              </div>          
            `)
        }
        // 盒子结尾
        document.write(` </div>`)
    </script>
</body>

</html>
```

### 5.冒泡排序

![image-20220811181901753](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%95%B0%E7%BB%84.assets/image-20220811181901753.png)

![image-20220811181912045](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%95%B0%E7%BB%84.assets/image-20220811181912045.png)

![image-20220811181921999](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%95%B0%E7%BB%84.assets/image-20220811181921999.png)

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
    // let arr = [5, 4, 3, 2, 1]
    let arr = [2, 4, 3, 5, 1]
    // for (let i = 0; i < arr.length - 1; i++) {
    //   for (let j = 0; j < arr.length - i - 1; j++) {
    //     // 开始交换 但是前提 第一个数大于第二个数才交换
    //     if (arr[j] > arr[j + 1]) {
    //       // 交换2个变量
    //       let temp = arr[j]
    //       arr[j] = arr[j + 1]
    //       arr[j + 1] = temp
    //     }
    //   }
    // }
    // arr.sort()  // 排序
    // sort 升序排列
    // arr.sort(function (a, b) {
    //   return a - b
    // })
    // sort() 降序
    arr.sort(function (a, b) {
      return b - a
    })
    console.log(arr)

    // let num1 = 10
    // let num2 = 20
    // let temp = num1
    // num1 = num2
    // num2 = temp 
  </script>
</body>

</html>
```

## 三、作业

PC端：https://ks.wjx.top/vj/YDMWN1o.aspx

![image-20220811182042404](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%89%E5%A4%A9%20%E6%95%B0%E7%BB%84.assets/image-20220811182042404.png)