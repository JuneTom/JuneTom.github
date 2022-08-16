# JavaScript 高级第四天 高阶技巧

## 1. 深浅拷贝

### 1. 基本数据类型

> 也叫（原始类型 / 值类型 / 原始值）7种

```js
Number String Boolean  /  undefined null / Symbol BigIntCopy to clipboardErrorCopied
```

- 基本数据类型不可以添加属性和方法

```js
let str = '123'
str.a = '222'
str.max = function(){}
console.log(str) // '123'
console.log(str.a) // undefined
console.log(str.max) // undefinedCopy to clipboardErrorCopied
```

### 2. 引用数据类型

> 也叫复杂数据类型，对象Object

```js
Object / Function / Array / RegExp / Date / Math / Error等Copy to clipboardErrorCopied
```

### 3. 内存存储

> 基本类型的数据和引用类型的数据在内存中怎么存储的呢?

栈 （Stack）： 基本数据类型的值， 存在栈内存面。

堆 （Heap）：引用类型的数据，栈里存放的是地址，这个地址指向堆里面的数据。

### 4. 检测数据类型

#### 4.1 typeof

```js
// 1. typeof 可以用来判断一个变量是否为除了null的基本类型(原始类型)
// 基本类型
console.log(typeof 1); 
console.log(typeof ""); 
console.log(typeof true); 
console.log(typeof undefined); 
console.log(typeof null); // object---有点儿特殊 Bug
console.log(typeof Symbol('id'))
console.log(typeof 9007199254740999n) 
console.log(typeof BigInt(9007199254740999)) 

// 2. typeof 总是返回一个字符串
console.log(typeof (typeof 1)) // string  

// 3. typeof 检测对象(引用类型), 除了function, 其他都是'object'
// 引用类型
console.log(typeof [1,2,3]); // 'object'
console.log(typeof function(){}); // 'function'
console.log(typeof {});  // 'object'
let date = new Date();
let error = new Error();
console.log(typeof date); // 'object'
console.log(typeof error); // 'object'Copy to clipboardErrorCopied
```

#### 4.2 instanceof

```js
// instanceof可以用于引用类型的检测, 但对基本数据类型无效.

// 用于检测构造函数的 prototype 属性是否出现在某个实例对象的原型链上。
// ==> 检测实例对象是不是构造函数创建的,或者是否属于某个祖先构造函数.
// 基本类型 无效
console.log('1' instanceof String) // false 
console.log(1 instanceof Number) 
console.log(true instanceof Boolean) 
console.log(typeof Symbol('id') instanceof Symbol) 
console.log(typeof 9007199254740999n instanceof BigInt) 
console.log(typeof BigInt(9007199254740999) instanceof BigInt) 

// 引用类型
console.log([] instanceof Array)  // true
console.log(function () {} instanceof Function) // true 
console.log({} instanceof Object)  // trueCopy to clipboardErrorCopied
```

#### 4.3 Object.prototype.toString.call()

> 终极方法 Object.prototype.toString.call()

```js
let num = 123
let str = '123'
let bool = true
let und = undefined
let nul = null 
let symb = Symbol('id')
let big = 9007199254740999n

let arr = [1,2,3]
let obj = {}
let fn = function(){}
let date = new Date()   // [object Date]
let reg = /a/g          // [object RegExp]
let error = new Error() // [object Error]
// 前面的object小写, 后面的类型, 大写开头; 字符串
console.log(Object.prototype.toString.call(num)) // [object Number]
console.log(Object.prototype.toString.call(str))  // [object String]
console.log(Object.prototype.toString.call(bool)) // [object Boolean]
console.log(Object.prototype.toString.call(und)) // [object Undefined]
console.log(Object.prototype.toString.call(nul)) // [object Null]
console.log(Object.prototype.toString.call(symb)) // [object Symbol]
console.log(Object.prototype.toString.call(big)) // [object BigInt]

console.log(Object.prototype.toString.call(arr))  // [object Array]
console.log(Object.prototype.toString.call(obj))  // [object Object]
console.log(Object.prototype.toString.call(fn))   // [object Function]
console.log(Object.prototype.toString.call(date))   // [object Date]
console.log(Object.prototype.toString.call(reg))   // [object RegExp]
console.log(Object.prototype.toString.call(error))   // [object Error]Copy to clipboardErrorCopied
// 封装一个CheckType  ?  ==> 扩展运算符  剩余参数  箭头函数 forEach 
const tempArr = [num, str, bool, und, nul, symb, big, arr, obj, fn, date, reg, error]
Copy to clipboardErrorCopied
```

#### 4.4 判断数组

> 1. instanceof
> 2. Object.prototype.toString.call()
> 3. Array.isArray() 判断一个对象是否为数组

```js
const arr = [1, 23];
const obj = {};
console.log(Array.isArray(arr));   // true
console.log(Array.isArray(obj));   // falseCopy to clipboardErrorCopied
```

### 5. 深浅拷贝

#### 5.1 赋值 Copy

> 赋值是将某一数值或对象赋给某个变量的过程

- 基本数据类型：值传递, 赋值之后两个变量互不影响
- 引用数据类型：赋**址**(地址)，两个变量具有相同的引用，指向同一个对象，相互之间有影响

```js
// 值类型
let a = '莫听穿林打叶声，何妨吟啸且徐行'
let b = a
console.log(b)
a = '贵有恒，何必三更起五更眠'

// 引用类型
let obj1 = {
  name: "JS",
  book: {
    title: "You Don't Know JS",
    price: "169"
  }
}
let obj2 = obj1

obj2.name = 'Hello World'
console.log(obj2, obj1)Copy to clipboardErrorCopied
```

##### 小结

当我们把一个对象赋值给一个新的变量时，**赋的其实是该对象的在栈中的地址，而不是堆中的数据**。也就是两个对象指向的是同一个存储空间，无论哪个对象发生改变，其实都是改变的存储空间的内容，因此，两个对象是联动的。

#### 5.2 浅拷贝 Shallow Copy

> *狭义上的深浅拷贝只是针对引用数据类型而言的，基本数据类型只有赋值操作。*

- 浅拷贝是创建一个新对象，这个对象有着原始对象属性值的一份精确拷贝。如果属性是基本类型，拷贝的就是基本类型的值，如果属性是引用类型，拷贝的就是内存地址 ，所以**如果其中一个对象改变了这个地址，就会影响到另一个对象**。

![image-20220816150740882](JavaScript%20%E9%AB%98%E7%BA%A7%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E9%AB%98%E9%98%B6%E6%8A%80%E5%B7%A7/image-20220816150740882.png)

简单来说可以理解为浅拷贝只解决了第一层的问题，拷贝第一层的**基本类型值**，以及第一层的**引用类型地址**。

浅拷贝: 重新在堆中创建内存空间，拷贝前后对象的基本数据类型互不影响，但拷贝前后对象的引用类型因共享同一块内存，会相互影响。

##### 1. Object.assign()

##### 2. 扩展运算符...

##### 3. 数组方法：concat() / slice()

```js
let a = {
  name: "JS",
  book: {
    title: "You Don't Know JS",
    price: "169"
  }
}
let b = Object.assign({}, a)Copy to clipboardErrorCopied
```

##### 小结

> 浅拷贝: 只拷贝一层, 简单类型拷贝值, 引用类型拷贝地址

![image-20220814020929172](JavaScript%20%E9%AB%98%E7%BA%A7%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E9%AB%98%E9%98%B6%E6%8A%80%E5%B7%A7/image-20220814020929172.png)

#### 5.3 深拷贝 Deep Copy

- 深拷贝: 在堆内存中开辟一个新的区域存放新对象, 拷贝原对象的所有属性( 对对象中的子对象进行递归拷贝 ). 拷贝前后两个对象互不影响。
- 深拷贝相比于浅拷贝速度较慢并且花销较大。

![image-20220814012722077](JavaScript%20%E9%AB%98%E7%BA%A7%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E9%AB%98%E9%98%B6%E6%8A%80%E5%B7%A7/image-20220814012722077.png)

##### 递归函数

> 递归: 一句话来讲就是自己调用自己

![image-20220814021051556](JavaScript%20%E9%AB%98%E7%BA%A7%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E9%AB%98%E9%98%B6%E6%8A%80%E5%B7%A7/image-20220814021051556.png)

```js
function fn(n) {
    if (n === 1) {
        return 1
    }
    return n + fn(n - 1)
}

// 调用
let res = fn(1000000)
console.log(res)Copy to clipboardErrorCopied
```

![image-20220816171109658](JavaScript%20%E9%AB%98%E7%BA%A7%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E9%AB%98%E9%98%B6%E6%8A%80%E5%B7%A7/image-20220816171109658.png)

##### 模拟 setInterval

![image-20220814023036187](JavaScript%20%E9%AB%98%E7%BA%A7%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E9%AB%98%E9%98%B6%E6%8A%80%E5%B7%A7/image-20220814023036187.png)

```js
function getTime() {
  document.querySelector('div').innerHTML = new Date().toLocaleString()
  setTimeout(getTime, 1000)
}
getTime()Copy to clipboardErrorCopied
```

##### 1. JSON.parse(JSON.stringify())

> 有缺陷！

```js
 const newObj = JSON.parse( JSON.stringify( obj ) )Copy to clipboardErrorCopied
const obj = {
    name: 'zjl',
    age: 18,
    hobyy:['dance','music'],
    book:{
        book_name:'Golang',
        price:66
    }
}
//==========
test0:function(){},
test1:undefined,
test2:Symbol('id'),
test3:new RegExp(/abc/, 'i'),
test4:NaN,
test5:Infinity,
test6:new Date()    
//============
const newObj = JSON.parse( JSON.stringify( obj ) )Copy to clipboardErrorCopied
```

> 主要记住，拷贝对象中的值如果是function， undefined等会丢失键值对。

##### 2. 手写递归

```js
const obj = {
  name: 'zjl',
  age: 18,
  hobyy:['dance','music'],
  book:{
     book_name:'Golang',
     price:66
  }
}

const deepClone = (newObj, oldObj) => {
    for (let k in oldObj) {
        // k 属性名  oldObj[k] 属性值
        if (oldObj[k] instanceof Array) {
            newObj[k] = []  // obj.hobby = [], 创建了一个新对象

            deepClone(newObj[k], oldObj[k])
        } else if (oldObj[k] instanceof Object){
            newObj[k] = {}
            deepCopy(newObj[k], oldObj[k])
        } else{
            // 不是数组， 执行 else
            newObj[k] = oldObj[k]
        }
    }
}Copy to clipboardErrorCopied
```

- 考虑 Date、RegExp类型， 直接生成一个新的实例返回
- 考虑数组 `let target = Array.isArray(obj)? [] : {}`
- 考虑循环引用 利用WeakMap作为hash表， 检测到对象已存在于哈希表中，取出该值返回即可
- 针对不可枚举属性以及 Symbol 类型，使用 Reflect.ownKeys()
- 函数部分太复杂，函数的原型，多层柯里化等
- 针对Map, Set, Error等，Object.getOwnPropertyDescriptors(obj) 也不考虑
- 递归爆栈问题，改用循环解决，广度优先
- [深拷贝的终极探索（99%的人都不知道）](https://segmentfault.com/a/1190000016672263)
- [如何写出一个惊艳面试官的深拷贝?](https://juejin.cn/post/6844903929705136141#heading-4)

```js
// 这一版， 大家以后 想跳槽大厂... 阿里腾讯随便进
// 检测对象 
const isObject = (obj) => {
    return typeof obj === 'object' && obj != null  // !!obj
}

const deepClone = (obj, hash = new WeakMap()) => {
  // 值类型 直接返回
  if (!isObject(obj)) return obj
  // Date, RegExp  constructor容易被修改丢失，被认为不安全，不推荐作为判断
  // instanceof好一些
//  if (obj.constructor === Date) return new Date(obj)
//  if (obj.constructor === RegExp) return new RegExp(obj)
    if (obj instanceof Date) return new Date(obj)
    if (obj instanceof RegExp) return new RegExp(obj)
  // 解决循环引用，查哈希表
  if (hash.has(obj)) return hash.get(obj)
//     let allDesc = Object.getOwnPropertyDescriptors(obj)
//     let target = Object.create(Object.getPrototypeOf(obj),allDesc)
  let target = Array.isArray(obj) ? [] : {} // 考虑数组
  hash.set(obj, target)
  
  Reflect.ownKeys(obj).forEach(key => {
    if (isObject(obj[key])) {
      target[key] = deepClone(obj[key], hash)
    } else {
      target[key] = obj[key]
    }
  })
  return target
}Copy to clipboardErrorCopied
```

##### 3. lodash库

> Lodash 是一个一致性、模块化、高性能的 JavaScript 实用工具库。

- [中文网](https://www.lodashjs.com/)
- [Github-lodash](https://github.com/lodash/lodash)

##### _.cloneDeep(value)

```js
const obj = {
    name: 'zjl',
    age: 18,
    hobyy:['dance','music'],
    book:{
        book_name:'Golang',
        price:66
    }
}
const o = _.cloneDeep(obj)
console.log(o)
o.book.price = 99
console.log(obj)Copy to clipboardErrorCopied
```

##### 小结

![image-20220814032850738](JavaScript%20%E9%AB%98%E7%BA%A7%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E9%AB%98%E9%98%B6%E6%8A%80%E5%B7%A7/image-20220814032850738.png)

#### 5.4 总结

| Type   | 和原数据是否指向同一对象 | 第一层数据为基本数据类型 | 原数据中包含子对象     |
| ------ | ------------------------ | ------------------------ | ---------------------- |
| 赋值   | 是                       | 改变会使原数据一同改变   | 改变会使原数据一同改变 |
| 浅拷贝 | 否                       | 改变**不会**影响原数据   | 改变会使原数据一同改变 |
| 深拷贝 | 否                       | 改变**不会**影响原数据   | 改变**不会**影响原数据 |

## 2. 异常处理

### 2.1 throw

![image-20220814034114613](JavaScript%20%E9%AB%98%E7%BA%A7%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E9%AB%98%E9%98%B6%E6%8A%80%E5%B7%A7/image-20220814034114613.png)

![image-20220814034206755](JavaScript%20%E9%AB%98%E7%BA%A7%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E9%AB%98%E9%98%B6%E6%8A%80%E5%B7%A7/image-20220814034206755.png)

![image-20220814034236460](JavaScript%20%E9%AB%98%E7%BA%A7%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E9%AB%98%E9%98%B6%E6%8A%80%E5%B7%A7/image-20220814034236460.png)

### 2.2 try / catch

![image-20220814034332157](JavaScript%20%E9%AB%98%E7%BA%A7%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E9%AB%98%E9%98%B6%E6%8A%80%E5%B7%A7/image-20220814034332157.png)

#### 小结

![image-20220814034359151](JavaScript%20%E9%AB%98%E7%BA%A7%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E9%AB%98%E9%98%B6%E6%8A%80%E5%B7%A7/image-20220814034359151.png)

### 2.3 debugger

![image-20220814034411172](JavaScript%20%E9%AB%98%E7%BA%A7%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E9%AB%98%E9%98%B6%E6%8A%80%E5%B7%A7/image-20220814034411172.png)

## 3. this指向

### 3.1 普通函数

![image-20220814034450447](JavaScript%20%E9%AB%98%E7%BA%A7%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E9%AB%98%E9%98%B6%E6%8A%80%E5%B7%A7/image-20220814034450447.png)

```js
// this 指向  ===>  指向 可以理解为 等于 代表谁
// this在定义的时候不能确定, 只有执行调用的时候才能确定.!!! 重要
// 背下来! 

// 1. 全局作用域中 / 普通函数中 / 定时器里面  this 指向 window
// 1.1 全局作用域
console.log(this)  // window

// 1.2 普通函数调用
function fn() {
  console.log('大家吃早饭了嘛?')
  console.log(this) // window
}
fn()

// 1.3 定时器里面
setTimeout(function(){
  console.log(this)  // window
}, 1000)

// 2.1 方法调用中, 谁调用这个方法, this指向谁
const obj = {
  name: '小平',
  age: 18,
  sayHi: function(){
    console.log(this)
  }
}
obj.sayHi()

// 2.2 事件注册的时候, this指向被绑定的元素
const btn = document.querySelector('button')
btn.addEventListener('click', function(e){
  console.log(this) // 绑定事件的元素
  console.log(e.target) // 触发事件的元素
  console.log(e.currentTarget) // 同this, 绑定事件的元素
})

console.log('-------------------------')

// 3. 构造函数中, this 指向的是 构造函数的实例
function Foo(name, age) {
  this.name = name 
  this.age = age 
  console.log(this)
}
const person1 = new Foo('小红', 19)
const person2 = new Foo('小白', 18)Copy to clipboardErrorCopied
```

### 3.2 箭头函数

![image-20220814034536430](JavaScript%20%E9%AB%98%E7%BA%A7%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E9%AB%98%E9%98%B6%E6%8A%80%E5%B7%A7/image-20220814034536430.png)

![image-20220814034559698](JavaScript%20%E9%AB%98%E7%BA%A7%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E9%AB%98%E9%98%B6%E6%8A%80%E5%B7%A7/image-20220814034559698.png)

![image-20220814034625108](JavaScript%20%E9%AB%98%E7%BA%A7%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E9%AB%98%E9%98%B6%E6%8A%80%E5%B7%A7/image-20220814034625108.png)

#### 小结

![image-20220814034717018](JavaScript%20%E9%AB%98%E7%BA%A7%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E9%AB%98%E9%98%B6%E6%8A%80%E5%B7%A7/image-20220814034717018.png)

### 3.3 改变this指向

#### 3.3.1 call()

![image-20220814035243759](JavaScript%20%E9%AB%98%E7%BA%A7%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E9%AB%98%E9%98%B6%E6%8A%80%E5%B7%A7/image-20220814035243759.png)

![image-20220814035257909](JavaScript%20%E9%AB%98%E7%BA%A7%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E9%AB%98%E9%98%B6%E6%8A%80%E5%B7%A7/image-20220814035257909.png)

#### 3.3.2 apply()

![image-20220814035314194](JavaScript%20%E9%AB%98%E7%BA%A7%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E9%AB%98%E9%98%B6%E6%8A%80%E5%B7%A7/image-20220814035314194.png)

![image-20220814035346601](JavaScript%20%E9%AB%98%E7%BA%A7%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E9%AB%98%E9%98%B6%E6%8A%80%E5%B7%A7/image-20220814035346601.png)

> call() 和 apply() 的区别？

- 都是调用函数， 都能改变this指向
- call接收参数列表， apply参数是数组

#### 3.3.3 bind()

![image-20220814035509968](JavaScript%20%E9%AB%98%E7%BA%A7%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E9%AB%98%E9%98%B6%E6%8A%80%E5%B7%A7/image-20220814035509968.png)

#### 小结

![image-20220814035523443](JavaScript%20%E9%AB%98%E7%BA%A7%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E9%AB%98%E9%98%B6%E6%8A%80%E5%B7%A7/image-20220814035523443.png)

## 4. 防抖节流

### 4.1 防抖 debounce

> 回调函数在一段时间后才执行, 如果这段时间内再次调用, 则重新计时.

> 在一定时间的间隔内, 将多次触发变成一次触发.

![image-20220815035033289](JavaScript%20%E9%AB%98%E7%BA%A7%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E9%AB%98%E9%98%B6%E6%8A%80%E5%B7%A7/image-20220815035033289.png)

- https://www.mi.com/shop 小米商城, 每次输入, 一直输入不会触发搜索请求.. 当键盘输入停止了, 等待100ms后请求.

#### 应用场景

1. 搜索框输入查询
2. 限制鼠标连续点击按钮提交()

![image-20220815035128412](JavaScript%20%E9%AB%98%E7%BA%A7%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E9%AB%98%E9%98%B6%E6%8A%80%E5%B7%A7/image-20220815035128412.png)

#### Code

```html
<style>
    .box {
        width: 500px;
        height: 500px;
        background-color: #ccc;
        color: #fff;
        text-align: center;
        font-size: 100px;
    }
</style>
<div class="box">0</div>Copy to clipboardErrorCopied
```

![image-20220815035137047](JavaScript%20%E9%AB%98%E7%BA%A7%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E9%AB%98%E9%98%B6%E6%8A%80%E5%B7%A7/image-20220815035137047.png)

```js
const box = document.querySelector('.box')
let i = 1 
const move = () => {
    box.innerHTML = i++
}

box.addEventListener('mousemove', move)Copy to clipboardErrorCopied
```

![image-20220815035147904](JavaScript%20%E9%AB%98%E7%BA%A7%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E9%AB%98%E9%98%B6%E6%8A%80%E5%B7%A7/image-20220815035147904.png)

![image-20220815035157997](JavaScript%20%E9%AB%98%E7%BA%A7%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E9%AB%98%E9%98%B6%E6%8A%80%E5%B7%A7/image-20220815035157997.png)

### Code

```js
// https://www.30secondsofcode.org/js/s/debounce 目前看见最简写法，best！
const debounce = (fn, ms = 0) => {
  let timeoutId
  return function(...args) { 
    // function(...args) rest参数 ，将args转为数组
    // 对比数组的扩展运算 fn.call(obj,...args) 含义不一样, 将args转为参数列表
    clearTimeout(timerId) // 每次点击的时候清除上一个定时器，重新计时
    timeoutId = setTimeout(() => fn.apply(this,args), ms)
  }
}Copy to clipboardErrorCopied
```

### 4.2 节流 throttle

> 持续的触发事件, 在一段时间内只允许函数执行一次.
>
> 每隔一段时间, 只执行一次, 减少一段时间内, 事件的触发频率.

#### 应用场景

1. 浏览器窗口缩放, resize事件
2. scroll滚动事件 / mousemove事件等

![image-20220815034840930](JavaScript%20%E9%AB%98%E7%BA%A7%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E9%AB%98%E9%98%B6%E6%8A%80%E5%B7%A7/image-20220815034840930.png)

![image-20220815034851228](JavaScript%20%E9%AB%98%E7%BA%A7%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E9%AB%98%E9%98%B6%E6%8A%80%E5%B7%A7/image-20220815034851228.png)

![image-20220815034904376](JavaScript%20%E9%AB%98%E7%BA%A7%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E9%AB%98%E9%98%B6%E6%8A%80%E5%B7%A7/image-20220815034904376.png)

![image-20220815034914097](JavaScript%20%E9%AB%98%E7%BA%A7%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E9%AB%98%E9%98%B6%E6%8A%80%E5%B7%A7/image-20220815034914097.png)

![image-20220815034937319](JavaScript%20%E9%AB%98%E7%BA%A7%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E9%AB%98%E9%98%B6%E6%8A%80%E5%B7%A7/image-20220815034937319.png)

#### 小结

![image-20220815035228204](JavaScript%20%E9%AB%98%E7%BA%A7%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E9%AB%98%E9%98%B6%E6%8A%80%E5%B7%A7/image-20220815035228204.png)

### 4.3 lodash

![image-20220815035402017](JavaScript%20%E9%AB%98%E7%BA%A7%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E9%AB%98%E9%98%B6%E6%8A%80%E5%B7%A7/image-20220815035402017.png)

### 4.3 节流案例

![image-20220815040011422](JavaScript%20%E9%AB%98%E7%BA%A7%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E9%AB%98%E9%98%B6%E6%8A%80%E5%B7%A7/image-20220815040011422.png)

![image-20220815040019483](JavaScript%20%E9%AB%98%E7%BA%A7%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E9%AB%98%E9%98%B6%E6%8A%80%E5%B7%A7/image-20220815040019483.png)

![image-20220815040026660](JavaScript%20%E9%AB%98%E7%BA%A7%E7%AC%AC%E5%9B%9B%E5%A4%A9%20%E9%AB%98%E9%98%B6%E6%8A%80%E5%B7%A7/image-20220815040026660.png)