# Web APIs 第六天 正则

## 一、正则表达式

### 1.介绍

* 正则表达式（Regular Expression）是用于匹配字符串中字符组合的模式。在 JavaScript中，正则表达式也是对象 
* 通常用来查找、替换那些符合正则表达式的文本，许多语言都支持正则表达式。

![image-20220801192439842](C:/Users/fortu/AppData/Roaming/Typora/typora-user-images/image-20220801192439842.png)

* 请在上图中找出【戴帽子和眼镜的男人】
* 戴帽子、戴眼镜、男人都是描述信息，通过这些信息能够在人群中查找到确定的某个人，那么这些用于查找的描述信 息编写一个模式，对应到计算机中就是所谓的正则表达式。

* 正则表达式在 JavaScript中的使用场景：  
  * 例如验证表单：用户名表单只能输入英文字母、数字或者下划线， 昵称输入框中可以输入中文(匹配) 
  * 比如用户名: /^[a-z0-9_-]{3,16}$/ 
  * 过滤掉页面内容中的一些敏感词(替换)，或从字符串中获取我们想要的特定部分(提取)等 。

1.正则表达式是什么？ 

* 是用于匹配字符串中字符组合的模式 

2.正则表达式有什么作用？

* 表单验证（匹配） 
* 过滤敏感词（替换）
* 字符串中提取我们想要的部分（提取）

### 2.语法

![image-20220801192718386](Web%20APIs%20%E7%AC%AC%E5%85%AD%E5%A4%A9%20%E6%AD%A3%E5%88%99&%E9%98%B6%E6%AE%B5%E6%A1%88%E4%BE%8B.assets/image-20220801192718386.png)

####  2.1 定义正则表达式语法：

![image-20220801192726278](Web%20APIs%20%E7%AC%AC%E5%85%AD%E5%A4%A9%20%E6%AD%A3%E5%88%99&%E9%98%B6%E6%AE%B5%E6%A1%88%E4%BE%8B.assets/image-20220801192726278.png)

#### 2.2 判断是否有符合规则的字符串：

![image-20220801192737437](Web%20APIs%20%E7%AC%AC%E5%85%AD%E5%A4%A9%20%E6%AD%A3%E5%88%99&%E9%98%B6%E6%AE%B5%E6%A1%88%E4%BE%8B.assets/image-20220801192737437.png)

##### 2.2.1总结

![image-20220801192845276](Web%20APIs%20%E7%AC%AC%E5%85%AD%E5%A4%A9%20%E6%AD%A3%E5%88%99&%E9%98%B6%E6%AE%B5%E6%A1%88%E4%BE%8B.assets/image-20220801192845276.png)

#### 2.3 检索（查找）符合规则的字符串：

![image-20220801192928465](Web%20APIs%20%E7%AC%AC%E5%85%AD%E5%A4%A9%20%E6%AD%A3%E5%88%99&%E9%98%B6%E6%AE%B5%E6%A1%88%E4%BE%8B.assets/image-20220801192928465.png)

#### 2.4总结

![image-20220801193016659](Web%20APIs%20%E7%AC%AC%E5%85%AD%E5%A4%A9%20%E6%AD%A3%E5%88%99&%E9%98%B6%E6%AE%B5%E6%A1%88%E4%BE%8B.assets/image-20220801193016659.png)

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
      // 正则表达式 ： Regular Expression    Regular ： 有规律的
      // 定义： 是一种字符串匹配模式 （pattern） （规则） ； 匹配模式， 匹配模式。
      // 同时， 正则表达式 是一个对象。

      // 作用：
      //    1. 表单验证 ： 匹配 （看是否满足条件）
      //    2. 过滤敏感词 ： 替换  **
      //    3. 字符串种提取想要的部分： 提取
      const str = '我们在学前端'
      // 1. reg.test()
      // 定义规则
      const reg = /前端/
      console.log(typeof reg) // object
      // 看是否匹配
      // console.log(reg.test(str))  // true

      // 2. reg.exec()
      // exec() 查找符合规则的字符串,找到返回结果数组, 否则为null
      console.log(reg.exec(str)) // 返回数组

      // 区别：
      // reg.test()   返回的是boolean， true或者false    常用这个！
      // reg.exec()   返回的是结果数组， 如果不匹配， 返回null   了解
    </script>
  </body>
</html>

```



### 3.元字符

#### 1.定义

* 目标：能说出什么是元字符以及它的好处

*  普通字符: 

  大多数的字符仅能够描述它们本身，这些字符称作普通字符，例如所有的字母和数字。 也就是说普通字符只能够匹配字符串中与它们相同的字符。

* 元字符(特殊字符） 

  是一些具有特殊含义的字符，可以极大提高了灵活性和强大的匹配功能。

  *  比如，规定用户只能输入英文26个英文字母，普通字符的话 abcdefghijklm….. 
  * 但是换成元字符写法： [a-z]  

*  参考文档： 

  * MDN：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions 
  * 正则测试工具: http://tool.oschina.net/regex

##### 1.1总结

![image-20220801193240736](Web%20APIs%20%E7%AC%AC%E5%85%AD%E5%A4%A9%20%E6%AD%A3%E5%88%99&%E9%98%B6%E6%AE%B5%E6%A1%88%E4%BE%8B.assets/image-20220801193240736.png)



#### 2.边界符

为了方便记忆和学习，我们对众多的元字符进行了分类： 

*  边界符（表示位置，开头和结尾，必须用什么开头，用什么结尾） 
* 量词 （表示重复次数）
* 字符类 （比如 \d 表示 0~9）

![image-20220801193923670](Web%20APIs%20%E7%AC%AC%E5%85%AD%E5%A4%A9%20%E6%AD%A3%E5%88%99&%E9%98%B6%E6%AE%B5%E6%A1%88%E4%BE%8B.assets/image-20220801193923670.png)

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
      // 元字符

      console.log(/哈/.test('哈')) //true
      console.log(/哈/.test('哈哈')) //true
      console.log(/哈/.test('二哈')) //true
      console.log('------------------')
      // 1. 边界符
      // ^ 开头
      console.log(/^哈/.test('哈')) //true
      console.log(/^哈/.test('哈哈')) //true
      console.log(/^哈/.test('二哈')) //false
      // $ 结尾  精确匹配 只能以/^哈$/开头结尾，一个哈，个数也不能多
      console.log(/^哈$/.test('哈')) //true
      console.log(/^哈$/.test('哈哈')) //false
      console.log(/^哈$/.test('二哈')) //false
      console.log('------------------')
      // 如果两个同时使用，必须精确匹配
    </script>
  </body>
</html>

```

#### 3.量词

![image-20220801193959156](Web%20APIs%20%E7%AC%AC%E5%85%AD%E5%A4%A9%20%E6%AD%A3%E5%88%99&%E9%98%B6%E6%AE%B5%E6%A1%88%E4%BE%8B.assets/image-20220801193959156.png)

* ​		+ 表示重复至少 1 次 
* ​        ? 表示重复 0 次或1次 
* ​        *表示重复 0 次或多次 
* ​        {m, n} 表示复 m 到 n 次

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
      // 量词 ： 表示重复的次数， 设定某个模式（规则）出现的次数

      // 1. *  表示 >= 0  0次或者更多次  记忆： 想象天上的星星， 可能一颗也没有， 也可能很多颗， 可能数也数不过来
      console.log(/^哈$/.test('哈')) // true
      console.log(/^哈*$/.test('')) // true
      console.log(/^哈*$/.test('哈哈')) // true
      console.log(/^哈*$/.test('哈哈哈')) // true
      console.log(/^哈*$/.test('二哈很傻')) // false
      console.log(/^哈*$/.test('哈很傻')) // false
      console.log(/^哈*$/.test('哈很哈')) // false

      // /^哈*$/  表示 哈字 0次或者多次 '', 哈, 哈哈， 哈哈哈 ， 哈哈哈哈哈

      // 2. + 表示 >=1   1次或者多次    记忆： 加号追加的意思， 得先有一个，然后才考虑追加
      console.log(/^哈$/.test('哈')) // true
      console.log(/^哈+$/.test('')) // false  注意这个！
      console.log(/^哈+$/.test('哈哈')) // true
      console.log(/^哈+$/.test('哈哈哈')) // true
      console.log(/^哈+$/.test('二哈很傻')) // false
      console.log(/^哈+$/.test('哈很傻')) // false
      console.log(/^哈+$/.test('哈很哈')) // false

      // /^哈+$/  表示 哈字 1次或者多次  哈, 哈哈， 哈哈哈， 哈哈哈哈哈

      console.log('----------------------------------')
      // 3. ?  0 || 1, 0次或者1次  怎么记忆呢： 问号 ： 有吗？
      console.log(/^哈?$/.test('')) // true
      console.log(/^哈?$/.test('哈')) // true
      console.log(/^哈?$/.test('哈哈')) // false
      console.log(/^哈?$/.test('哈哈哈')) // false
      console.log(/^哈?$/.test('二哈很傻')) // false
      console.log(/^哈?$/.test('哈很傻')) // false
      console.log(/^哈?$/.test('哈很哈')) // false

      console.log('----------------------------------')
      // 4. {n}  写几, 就必须出现几次   哈哈哈
      console.log(/^哈{3}$/.test('')) // false
      console.log(/^哈{3}$/.test('哈')) // false
      console.log(/^哈{3}$/.test('哈哈')) // false
      console.log(/^哈{3}$/.test('哈哈哈')) // true
      console.log(/^哈{3}$/.test('哈哈哈哈')) // false
      console.log(/^哈{3}$/.test('哈哈哈哈哈')) // false

      console.log('----------------------------------')
      // 5. {n,}  >=n
      console.log(/^哈{3,}$/.test('')) // false
      console.log(/^哈{3,}$/.test('哈')) // false
      console.log(/^哈{3,}$/.test('哈哈')) // false
      console.log(/^哈{3,}$/.test('哈哈哈')) // true
      console.log(/^哈{3,}$/.test('哈哈哈哈')) // true
      console.log(/^哈{3,}$/.test('哈哈哈哈哈')) // true

      // 6. {n,m}  逗号两边一定不要有空格！！！ >= n && <= m

      console.log('-------------------')
      console.log(/^哈{3,6}$/.test('')) // false
      console.log(/^哈{3,6}$/.test('哈')) // false
      console.log(/^哈{3,6}$/.test('哈哈')) // false
      console.log(/^哈{3,6}$/.test('哈哈哈')) // true
      console.log(/^哈{3,6}$/.test('哈哈哈哈')) // true
      console.log(/^哈{3,6}$/.test('哈哈哈哈哈')) // true
      console.log(/^哈{3,6}$/.test('哈哈哈哈哈哈')) // true
      console.log(/^哈{3,6}$/.test('哈哈哈哈哈哈哈')) // false

      // 横向模糊匹配 ： 一个正则可匹配的字符串长度不是固定的，可以是多种情况
      // 实现方式： 使用量词。

      const reg = /ab{2,5}c/
      //  表示：==>  第一个字符'a', 接下来是 2到5个 'b', 最后是字符'c'

      // abbc  abbbc abbbbc abbbbbc
      console.log(reg.test('bbbc')) // false
      console.log(reg.test('dbabbc')) // true

      console.log('----------------')
      const reg2 = /^ab{2,5}c$/
      console.log(reg2.test('dbabbc')) // false
    </script>
  </body>
</html>

```

#### 4.字符类

![image-20220801194352557](Web%20APIs%20%E7%AC%AC%E5%85%AD%E5%A4%A9%20%E6%AD%A3%E5%88%99&%E9%98%B6%E6%AE%B5%E6%A1%88%E4%BE%8B.assets/image-20220801194352557.png)



![image-20220801194400497](Web%20APIs%20%E7%AC%AC%E5%85%AD%E5%A4%A9%20%E6%AD%A3%E5%88%99&%E9%98%B6%E6%AE%B5%E6%A1%88%E4%BE%8B.assets/image-20220801194400497.png)

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
      // 一些系统自带的字符组简写形式

      // \d   [0-9] 数字字符   记忆: 英文 digit(数字)  小写!
      // \w   [0-9a-zA-Z_] 单词字符: 表示数字,大小写字母和下划线. 记忆: w, word 单词字符.
      // \s   [ \t\v\n\r\f] 空白字符  记忆 : space 空格的意思. (注意这里, 前面第一个是空格)

      // 排除性字符组简写 (大写)
      // \D  [^0-9]  表示除了数字外的任意单个字符. 非数字字符.
      // \W  [^0-9a-zA-Z_]  非单词字符
      // \S  [^ \t\v\n\r\f] 非空白符

      console.log(/\d/.test('n')) // false
      console.log(/\d/.test('999')) // true

      console.log(/\w/.test('%')) // false
      console.log(/\w/.test('aa')) // true

      console.log(/^\w$/.test('aa')) // false

      // 如果要匹配任意字符
      // [\d\D]  任意单个字符
      // [\s\S]
      // [\w\W]
    </script>
  </body>
</html>

```



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
      // 字符组：同一个位置上可能出现的各种字符， 也叫纵向模糊匹配
      // 写法： [] 方括号之间列出所有可能出现的字符

      // 联想： 抽奖， 三个框框一直转动， 每一个框框就选出一个字符，只能选一个！
      // /[abc]/  ==> 检测的字符， 只要包含a, b， c中任意一个， 就返回true； reg.test()

      // [...] 多选一， 括号中任意单个元素！ 只能一个！
      console.log(/^[abc]$/.test('a')) //true
      console.log(/^[abc]$/.test('b')) //true
      console.log(/^[abc]$/.test('c')) //true
      console.log('===============================')
      console.log(/^[abc]$/.test('ab')) //false
      console.log(/^[abc]$/.test('bc')) //false
      console.log('===============================')
      console.log(/^[abc]{2}$/.test('bc')) //true
      console.log(/^[abc]{2}$/.test('ab')) //true
      console.log(/^[abc]{2}$/.test('ca')) //true

      console.log('===============================')
      // 2. 范围表示法
      // 用-表示区间范围
      // [0123456789]  ==>  [0-9]
      // 注意， 不能写[9-0], [Z-A], 范围表示是从  码值小的-码值大的

      // [a-z]  a-z 匹配所有的英文小写字母，  只能选一个！
      // [A-Z]  A-Z 只能选一个
      // [0-9]  0-9 只能选一个
      // [a-zA-Z0-9]  大小写字母加数字， 只能选一个
      // [a-zA-Z0-9_]  大小写字母加数字加下划线， 只能选一个; 平时校验密码

      console.log(/^[A-Z]$/.test('d')) // false
      console.log(/^[A-Z]$/.test('D')) // true
      console.log(/^[0-9]$/.test('8')) // true
      console.log(/^[a-zA-Z0-9]$/.test('2')) // true
      console.log(/^[a-zA-Z0-9]$/.test('A')) // true
      console.log(/^[a-zA-Z0-9]$/.test('a')) // true

      console.log(/^[a-zA-Z0-9_]{6,10}$/.test('11')) //false
      console.log(/^[a-zA-Z0-9_]{6,10}$/.test('123456')) // true

      // 注意：
      // 1. {} 重复的是离它最近的前面那一个规则！ 横向模拟匹配， 拉长
      // 2. [] 是多个中选一个， 选一个， 选一个！ 纵向模糊匹配
    </script>
  </body>
</html>

```



![image-20220801194411498](Web%20APIs%20%E7%AC%AC%E5%85%AD%E5%A4%A9%20%E6%AD%A3%E5%88%99&%E9%98%B6%E6%AE%B5%E6%A1%88%E4%BE%8B.assets/image-20220801194411498.png)



![image-20220801194419033](Web%20APIs%20%E7%AC%AC%E5%85%AD%E5%A4%A9%20%E6%AD%A3%E5%88%99&%E9%98%B6%E6%AE%B5%E6%A1%88%E4%BE%8B.assets/image-20220801194419033.png)

![image-20220801200155332](Web%20APIs%20%E7%AC%AC%E5%85%AD%E5%A4%A9%20%E6%AD%A3%E5%88%99&%E9%98%B6%E6%AE%B5%E6%A1%88%E4%BE%8B.assets/image-20220801200155332.png)

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
      // 取反  ^
      //  在方括号[]里面最前面写上^ (脱字符), 表示取反.
      // [^0-9] 表示当前位置上, 匹配除了0-9以外的所有字符.(非数字)

      // [^abc]  除了'a', 'b', 'c' 以外的其他任何单个字符
      console.log(/[^abc]/.test('c')) // false
      console.log(/[^abc]/.test('-')) // true
      console.log(/[^abc]/.test('=')) // true

      // [^a-z]  匹配除了小写字母以外的其他任何单个字符
      // [^a-zA-Z0-9] 除了英文字母加数字外的 任何 单个字符

      console.log(/[^a-zA-Z0-9]/.test('+')) // true

      // 特殊单字符
      // . 匹配除了换行之外的任何单个字符

      console.log(/./.test('22')) // true
    </script>
  </body>
</html>

```

#### 5.总结 

1.字符类 . (点)代表什么意思？ 

* 匹配除换行符之外的任何单个字符

2.字符类 [] 有若干代表什么意思？

* [abc] 匹配abc其中的任何单个字符 
*  [a-z] 匹配26个小写英文字母其中的任何单个字符 
* [^a-z] 匹配除了26个小写英文字母之外的其他任何 单个字符

#### 6.案例（用户名验证案）

![image-20220801194834447](Web%20APIs%20%E7%AC%AC%E5%85%AD%E5%A4%A9%20%E6%AD%A3%E5%88%99&%E9%98%B6%E6%AE%B5%E6%A1%88%E4%BE%8B.assets/image-20220801194834447.png)

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
      span {
        display: inline-block;
        width: 250px;
        height: 30px;
        vertical-align: middle;
        line-height: 30px;
        padding-left: 15px;
      }

      .error {
        color: red;
        background: url(./images/error1.png) no-repeat left center;
      }

      .right {
        color: green;
        background: url(./images/right.png) no-repeat left center;
      }
    </style>
  </head>

  <body>
    <input type="text" />
    <span></span>
    <script>
      const input = document.querySelector('input')
      const span = input.nextElementSibling
      const reg = /^[a-zA-Z0-9-_]{6,16}$/
      input.addEventListener('blur', function () {
        if (reg.test(input.value)) {
          span.innerHTML = '输入正确'
          span.className = 'right'
        } else {
          span.innerHTML = '请输入6-16位英文数字下划线短横线'
          span.className = 'error'
        }
      })
    </script>
  </body>
</html>

```



### 4.修饰符

![image-20220801200210494](Web%20APIs%20%E7%AC%AC%E5%85%AD%E5%A4%A9%20%E6%AD%A3%E5%88%99&%E9%98%B6%E6%AE%B5%E6%A1%88%E4%BE%8B.assets/image-20220801200210494.png)

![image-20220801200218909](Web%20APIs%20%E7%AC%AC%E5%85%AD%E5%A4%A9%20%E6%AD%A3%E5%88%99&%E9%98%B6%E6%AE%B5%E6%A1%88%E4%BE%8B.assets/image-20220801200218909.png)

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
      //  修饰符
      //  约束正则执行的某些细节行为，比如是否区分大小写。
      // /表达式/修饰符
      // 常用的修饰符
      //  1. i  忽略字母大小写   单词 ignoreCase
      //  2. g  全局匹配， 找到所有匹配的   单词 global

      console.log(/^java$/.test('java'))
      console.log(/^java$/i.test('JAVA'))
      console.log(/^java$/i.test('Java'))

      // 字符串替换
      // str.replace   (/正则/，要替换的文本)
      const str = 'Java是一门编程语言，学完JAVA薪资很高'
      const res = str.replace(/java/gi, '前端')
      console.log(res)
      // 如果不写g.只会替换第一个匹配的字符
    </script>
  </body>
</html>

```

![image-20220801200307619](Web%20APIs%20%E7%AC%AC%E5%85%AD%E5%A4%A9%20%E6%AD%A3%E5%88%99&%E9%98%B6%E6%AE%B5%E6%A1%88%E4%BE%8B.assets/image-20220801200307619.png)

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
    <textarea name="" id="" cols="30" rows="10"></textarea>
    <button>发布</button>
    <div></div>
    <script>
      const tx = document.querySelector('textarea')
      const btn = document.querySelector('button')
      const div = document.querySelector('div')
      btn.addEventListener('click', function () {
        // str.replace(/正则/g, '要替换的文本')
        // 激情 基情 正则里面，或则|
        div.innerHTML = tx.value.replace(/激情|基情/g, '**')
        tx.value = ''
      })
    </script>
  </body>
</html>

```

## 二、作业

PC端地址： https://ks.wjx.top/vj/OCUF8u5.aspx

![image-20220801200500285](Web%20APIs%20%E7%AC%AC%E5%85%AD%E5%A4%A9%20%E6%AD%A3%E5%88%99&%E9%98%B6%E6%AE%B5%E6%A1%88%E4%BE%8B.assets/image-20220801200500285.png)