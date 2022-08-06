# JavaScript 基础第一天 基础语法

## **1.1 JavaScript的含义**

JavaScript是一种运行在客户端（浏览器）的编程语言，实现人机交互效果。

## **1.2 JavaScript的作用**

网页特效（监听用户的一些行为让网页做出对应的反馈）

表单验证（针对表单数据的合法性进行判断）

数据交互（获取后台的数据，渲染到前端）

服务器编程（node.js）

## **1.3.JavaScript的组成**

### **1.3.1 ECMAScript:**

规定了JS基础语法核心知识。

例如:变量、分支语句、循环语句、对象等等

### **1.3.2 Web APIs:**

DOM ：操作文档

ex:页面元素进行移动、大小、添加删除等操作

BOM ：操作浏览器

例如:页面弹窗，检测窗口宽度、存储数据到浏览器等等

JavaScript权威网站： https://developer.mozilla.org/zh-CN/docs/Web/JavaScript

## **2.1 JavaScript书写位置**

### **2.1.1 内部JavaScript：**

通过 script 标签包裹 JavaScript 代码

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>JavaScript 基础 - 引入方式</title>
</head>
<body>
  <!-- 内联形式：通过 script 标签包裹 JavaScript 代码 -->
  <script>
    alert('嗨，欢迎来传智播学习前端技术！')
  </script>
</body>
</html>
```

### **2.1.2 外部JavaScript：**

一般将 JavaScript 代码写在独立的以 .js 结尾的文件中，然后通过 script 标签的 src 属性引入

独立的.js结尾文件

```js
// demo.js
document.write('嗨，欢迎来传智播学习前端技术！')
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>JavaScript 基础 - 引入方式</title>
</head>
<body>
  <!-- 外部形式：通过 script 的 src 属性引入独立的 .js 文件 -->
  <script src="demo.js"></script>
</body>
</html>
```

### **2.1.3 内联JavaScript：**

代码写在标签内部

注意： 此处作为了解即可，但是后面vue框架会用这种模式

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>JavaScript 基础 - 引入方式</title>
</head>
<body>
    <button onclick="alert('你好啊')">点击</button>
</body>
</html>
```

## 2.2 练习

![image-20220720220407328](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%80%E5%A4%A9%20%E5%9F%BA%E7%A1%80%E8%AF%AD%E6%B3%95.assets/image-20220720220407328.png)

### 2.2.1 外部JavaScript

```js
// demo.js
alert('奋斗，努力')
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>JavaScript 基础 - 引入方式</title>
</head>
<body>
     <script src="demo.js"></script>
</body>
</html>
```

### 2.1.2 内部JavaScript

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>JavaScript 基础 - 引入方式</title>
</head>
<body>
     <script>
         alert('奋斗，努力')
     </script>
</body>
</html>
```

## 3. 注释和结束符

### 3.1通过注释可以屏蔽代码被执行或添加备注信息

#### 3.1.1单行注释

符号：`/`

作用：//右边这一行的代码会被忽略

快捷键：`ctrl + /`

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>JavaScript 基础 - 注释</title>
</head>
<body>
  
  <script>
    // 这种是单行注释的语法
    // 一次只能注释一行
    // 可以重复注释
    document.write('嗨，欢迎来传智播学习前端技术！');
  </script>
</body>
</html>
```

### 3.1.2 块注释

符号：`/*   */`

作用：在/* 和 */之间的所有内容都会被忽略

快捷键：`shift + alt + A`

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>JavaScript 基础 - 注释</title>
</head>
<body>
  
  <script>
    /* 这种的是多行注释的语法 */
    /*
    	更常见的多行注释是这种写法
    	在些可以任意换行
    	多少行都可以
      */
    document.write('嗨，欢迎来传智播学习前端技术！')
  </script>
</body>
</html>
```

## 4.结束符

在JavaScript中`;`代表一段代码的结束，多数情况下可以省略`;`使用回车（enter）替代

浏览器（JavaScript引擎）可以自动推断语句的结束位置

实际开发中有许多人主张书写 JavaScript 代码时省略结束符 `;`

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>JavaScript 基础 - 结束符</title>
</head>
<body>
  
  <script> 
    alert(1);
    alert(2);
    alert(1)
    alert(2)
  </script>
</body>
</html>
```

## 5. JavaScript输入输出语法

### 5.1 JavaScript输入输出语法定义

输出和输入也可理解为人和计算机的交互，用户通过键盘、鼠标等向计算机输入信息，计算机处理后再展示结果给用户，这便是一次输入和输出的过程。

举例说明：如按键盘上的方向键，向上/下键可以滚动页面，按向上/下键这个动作叫作输入，页面发生了滚动了这便叫输出。

### 5.2 输出语法

  JavaScript可以接收用户的输入，然后再将输入的结果输出：

`alert()、document.write()`

以数字为例，向 `alert()` 或 `document.write()`输入任意数字，他都会以弹窗形式展示（输出）给用户。

```javascript
document.write('页面输出内容')
```

作用：向body内输出内容

注意：如果输出的内容写的是尾标签，也会被解析成网页元素

```javascript
alert('页面输出内容')
```

作用：页面弹出警告对话框

```javascript
console.log('控制台打印')
```

作用：控制台输出语法，程序员调试使用

### 5.3 输入语法

向`prompt()`输入任意内容会以弹窗形式出现在浏览器中，一般会提示用户输入一些内容

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>JavaScript 基础 - 输入输出</title>
</head>
<body>
  
  <script> 
    // 1. 输入的任意数字，都会以弹窗形式展示
    document.write('要输出的内容')
    alert('要输出的内容');

    // 2. 以弹窗形式提示用户输入姓名，注意这里的文字使用英文的引号
    prompt('请输入您的姓名:')
  </script>
</body>
</html>
```

### 5.4 练习

![image-20220713113540391](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%80%E5%A4%A9%20%E5%9F%BA%E7%A1%80%E8%AF%AD%E6%B3%95.assets/image-20220713113540391.png)



```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>JavaScript 基础 - 输入输出</title>
</head>
<body>
  
  <script> 
   alert('你好 JS~')
   document.write('JavaScript')
   console.log('它~会魔法把')
  </script>
</body>
```

## 6.字面量

字面量（literal）是在计算机中描述 事/物

 比如： 我们工资是： 1000 此时 1000 就是 数字字面量 

​			'黑马程序员' 字符串字面量 

​			还有接下来我们学的 [] 数组字面量 {} 对象字面量 等

---



# 二、变量

## 1. 变量定义

变量是计算机中用来存储数据的“容器”，它可以让计算机变得有记忆，通俗的理解变量就是使用【某个符号】来代表【某个具体的数值】（数据）

注意：变量不是数据本身，它们仅仅是一个用于储存数据的容器

```html
<script>
  // x 符号代表了 5 这个数值
  x = 5
  // y 符号代表了 6 这个数值
  y = 6
    
  //举例： 在 JavaScript 中使用变量可以将某个数据（数值）记录下来！

  // 将用户输入的内容保存在 num 这个变量（容器）中
  num = prompt('请输入一数字!')

  // 通过 num 变量（容器）将用户输入的内容输出出来
  alert(num)
  document.write(num)
</script>
```

## 2.变量的基本使用

### 2.1声明

声明(定义)变量有两部分构成：声明关键字、变量名（标识）

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>JavaScript 基础 - 声明和赋值</title>
</head>
<body>
  
  <script> 
    // let 变量名
    // 声明(定义)变量有两部分构成：声明关键字、变量名（标识）
    // let 即关键字，所谓关键字是系统提供的专门用来声明（定义）变量的词语
    // age 即变量的名称，也叫标识符
    let age
  </script>
</body>
</html>
```

关键字是 JavaScript 中内置的一些英文词汇（单词或缩写），它们代表某些特定的含义，如 `let` 的含义是声明变量的，看到 `let` 后就可想到这行代码的意思是在声明变量，如 `let age;`

`let` 和 `var` 都是 JavaScript 中的声明变量的关键字，推荐使用 `let` 声明变量

### 2.2 赋值

声明（定义）变量相当于创造了一个空的“容器”，通过赋值向这个容器中添加数据。

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>JavaScript 基础 - 声明和赋值</title>
</head>
<body>
  
  <script> 
    // 声明(定义)变量有两部分构成：声明关键字、变量名（标识）
    // let 即关键字，所谓关键字是系统提供的专门用来声明（定义）变量的词语
    // age 即变量的名称，也叫标识符
    let age
    // 赋值，将 18 这个数据存入了 age 这个“容器”中
    age = 18
    // 这样 age 的值就成了 18
    document.write(age)
    
    // 也可以声明和赋值同时进行
    let str = 'hello world!'
    alert(str);
  </script>
</body>
</html>
```

### 2.3 关键字

JavaScript 使用专门的关键字 `let` 和 `var` 来声明（定义）变量，在使用时需要注意一些细节：

以下是使用 `let` 时的注意事项：

1. 允许声明和赋值同时进行
2. 不允许重复声明
3. 允许同时声明多个变量并赋值
4. JavaScript 中内置的一些关键字不能被当做变量名

以下是使用 `var` 时的注意事项：

1. 允许声明和赋值同时进行
2. 允许重复声明
3. 允许同时声明多个变量并赋值

大部分情况使用 `let` 和 `var` 区别不大，但是 `let` 相较 `var` 更严谨，因此推荐使用 `let`，后期会更进一步介绍二者间的区别。

### 2.4 变量名命名规则

关于变量的名称（标识符）有一系列的规则需要遵守：

1. 只能是字母、数字、下划线、$，且不能能数字开头
2. 字母区分大小写，如 Age 和 age 是不同的变量
3. JavaScript 内部已占用于单词（关键字或保留字）不允许使用
4. 尽量保证变量具有一定的语义，见字知义

注：所谓关键字是指 JavaScript 内部使用的词语，如 `let` 和`var`，保留字是指 JavaScript 内部目前没有使用的词语，但是将来可能会使用词语。

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>JavaScript 基础 - 变量名命名规则</title>
</head>
<body>
  
  <script> 
    let age = 18 // 正确
    let age1 = 18 // 正确
    let _age = 18 // 正确

    // let 1age = 18; // 错误，不可以数字开头
    let $age = 18 // 正确
    let Age = 24 // 正确，它与小写的 age 是不同的变量
    // let let = 18; // 错误，let 是关键字
    let int = 123 // 不推荐，int 是保留字
  </script>
</body>
</html>
```

### 2.5 变量拓展

#### 2.5.1 let和var的区别

let 和 var 区别：

​	 	在较旧的JavaScript，使用关键字 var 来声明变量 ，而不是 let。

var 现在开发中一般不再使用它，只是我们可能再老版程序中看到它。 

let 为了解决 var 的一些问题。 

var 声明: 

-  		可以先使用 在声明 (不合理) 
-  		​		 var 声明过的变量可以重复声明(不合理) 
-  		​		 比如变量提升、全局变量、没有块级作用域等等

#### 2.5.2 数组

目标：能够声明数组并且能够获取里面的数据

- 数组是按顺序保存，所以每个数据都有自己的编号 
- 计算机中的编号从0开始，所以小明的编号为0，小刚编号为1，以此类推
- 在数组中，数据的编号也叫索引或下标 
- 数组可以存储任意类型的数据

---

![image-20220713132240009](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%80%E5%A4%A9%20%E5%9F%BA%E7%A1%80%E8%AF%AD%E6%B3%95.assets/image-20220713132240009-16583259067831.png)

# 三、常量

1. 概念：使用 const 声明的变量称为“常量”。
2. 使用场景：当某个变量永远不会改变的时候，就可以使用 const 来声明，而不是let。
3. 命名规范：和变量一致

```javascript
const PI = 3.14
console.log(PI)
```

> 注意： 常量不允许重新赋值,声明的时候必须赋值（初始化）
>
> ​			不需要重新赋值的数据使用const

# 四、数据类型

> 计算机世界中的万事成物都是数据。

计算机程序可以处理大量的数据，为了方便数据的管理，将数据分成了不同的类型：

![image-20220713132852008](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%80%E5%A4%A9%20%E5%9F%BA%E7%A1%80%E8%AF%AD%E6%B3%95.assets/image-20220713132852008.png)

注：通过 typeof 关键字检测数据类型

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>JavaScript 基础 - 数据类型</title>
</head>
<body>
  
  <script> 
    // 检测 1 是什么类型数据，结果为 number
    document.write(typeof 1)
  </script>
</body>
</html>
```

![image-20220713134104941](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%80%E5%A4%A9%20%E5%9F%BA%E7%A1%80%E8%AF%AD%E6%B3%95.assets/image-20220713134104941-16583260992693.png)

## 1. 数值类型(Number)

即我们数学中学习到的数字，可以是整数、小数、正数、负数

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>JavaScript 基础 - 数据类型</title>
</head>
<body>
  
  <script> 
    let score = 100 // 正整数
    let price = 12.345 // 小数
    let temperature = -40 // 负数

    document.write(typeof score) // 结果为 number
    document.write(typeof price) // 结果为 number
    document.write(typeof temperature) // 结果为 number
  </script>
</body>
</html>
```

JavaScript 中的数值类型与数学中的数字是一样的，分为正数、负数、小数等。

![image-20220713133057604](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%80%E5%A4%A9%20%E5%9F%BA%E7%A1%80%E8%AF%AD%E6%B3%95.assets/image-20220713133057604.png)

![image-20220713133332460](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%80%E5%A4%A9%20%E5%9F%BA%E7%A1%80%E8%AF%AD%E6%B3%95.assets/image-20220713133332460.png)

## 2. 字符串类型(String)

通过单引号（ `''`） 、双引号（ `""`）或反引号包裹的数据都叫字符串，单引号和双引号没有本质上的区别，推荐使用单引号。

注意事项：

1. 无论单引号或是双引号必须成对使用
2. 单引号/双引号可以互相嵌套，但是不以自已嵌套自已
3. 必要时可以使用转义符 `\`，输出单引号或双引号

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>JavaScript 基础 - 数据类型</title>
</head>
<body>
  
  <script> 
    let user_name = '小明' // 使用单引号
    let gender = "男" // 使用双引号
    let str = '123' // 看上去是数字，但是用引号包裹了就成了字符串了
    let str1 = '' // 这种情况叫空字符串
		
    documeent.write(typeof user_name) // 结果为 string
    documeent.write(typeof gender) // 结果为 string
    documeent.write(typeof str) // 结果为 string
  </script>
</body>
</html>
```

![image-20220713133547753](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%80%E5%A4%A9%20%E5%9F%BA%E7%A1%80%E8%AF%AD%E6%B3%95.assets/image-20220713133547753.png)

![image-20220713133602949](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%80%E5%A4%A9%20%E5%9F%BA%E7%A1%80%E8%AF%AD%E6%B3%95.assets/image-20220713133602949.png)

## 3. 布尔类型(Boolean)

表示肯定或否定时在计算机中对应的是布尔类型数据，它有两个固定的值 `true` 和 `false`，表示肯定的数据用 `true`，表示否定的数据用 `false`。

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>JavaScript 基础 - 数据类型</title>
</head>
<body>
  
  <script> 
    //  pink老师帅不帅？回答 是 或 否
    let isCool = true // 是的，摔死了！
    isCool = false // 不，套马杆的汉子！

    document.write(typeof isCool) // 结果为 boolean
  </script>
</body>
</html>
```

## 4. 未定义类型(Undefined)

未定义是比较特殊的类型，只有一个值 undefined，只声明变量，不赋值的情况下，变量的默认值为 undefined，一般很少【直接】为某个变量赋值为 undefined。

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>JavaScript 基础 - 数据类型</title>
</head>
<body>
  
  <script> 
    // 只声明了变量，并末赋值
    let tmp;
    document.write(typeof tmp) // 结果为 undefined
  </script>
</body>
</html>
```

**注：JavaScript 中变量的值决定了变量的数据类型。**

![image-20220713133655708](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%80%E5%A4%A9%20%E5%9F%BA%E7%A1%80%E8%AF%AD%E6%B3%95.assets/image-20220713133655708.png)

## 5.空类型（null)

![image-20220713133723182](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%80%E5%A4%A9%20%E5%9F%BA%E7%A1%80%E8%AF%AD%E6%B3%95.assets/image-20220713133723182.png)

# 五、类型转换

在 JavaScript 中数据被分成了不同的类型，如数值、字符串、布尔值、undefined，在实际编程的过程中，不同数据类型之间存在着转换的关系。

## 1.隐式转换

某些运算符被执行时，系统内部自动将数据类型进行转换，这种转换称为隐式转换。

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>JavaScript 基础 - 隐式转换</title>
</head>
<body>
  <script> 
    let num = 13 // 数值
    let num2 = '2' // 字符串

    // 结果为 132
    // 原因是将数值 num 转换成了字符串，相当于 '13'
    // 然后 + 将两个字符串拼接到了一起
    console.log(num + num2)

    // 结果为 11
    // 原因是将字符串 num2 转换成了数值，相当于 2
    // 然后数值 13 减去 数值 2
    console.log(num - num2)

    let a = prompt('请输入一个数字')
    let b = prompt('请再输入一个数字')

    alert(a + b);
  </script>
</body>
</html>
```

注：数据类型的隐式转换是 JavaScript 的特征，后续学习中还会遇到，目前先需要理解什么是隐式转换。

补充介绍模板字符串的拼接的使用

## 2.显式转换

编写程序时过度依靠系统内部的隐式转换是不严禁的，因为隐式转换规律并不清晰，大多是靠经验总结的规律。为了避免因隐式转换带来的问题，通常根逻辑需要对数据进行显示转换。

![image-20220713134332553](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%80%E5%A4%A9%20%E5%9F%BA%E7%A1%80%E8%AF%AD%E6%B3%95.assets/image-20220713134332553-16583262088844.png)

![image-20220713134409627](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%80%E5%A4%A9%20%E5%9F%BA%E7%A1%80%E8%AF%AD%E6%B3%95.assets/image-20220713134409627.png)

**Number**

通过 `Number` 显示转换成数值类型，当转换失败时结果为 `NaN`（Not a Number）即不是一个数字。

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>JavaScript 基础 - 隐式转换</title>
</head>
<body>
  <script>
    let t = '12'
    let f = 8

    // 显式将字符串 12 转换成数值 12
    t = Number(t)

    // 检测转换后的类型
    // console.log(typeof t);
    console.log(t + f) // 结果为 20

    // 并不是所有的值都可以被转成数值类型
    let str = 'hello'
    // 将 hello 转成数值是不现实的，当无法转换成
    // 数值时，得到的结果为 NaN （Not a Number）
    console.log(Number(str))
  </script>
</body>
</html>
```

 电脑端： https://ks.wjx.top/vj/h8kAn6p.aspx

![image-20220715202143014](JavaScript%20%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%80%E5%A4%A9%20%E5%9F%BA%E7%A1%80%E8%AF%AD%E6%B3%95.assets/image-20220715202143014.png)