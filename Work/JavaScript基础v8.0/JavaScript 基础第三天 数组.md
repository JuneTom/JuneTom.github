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