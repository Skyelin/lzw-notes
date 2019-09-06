#### 一.变量let和const

引入了块级作用域。

- let

  用法：声明一个变量

  特点：

  ​		只在声明的代码块中生效

  ​		暂时性死区

  ​		没有变量提升

  ​		同一作用域内无法重复声明

- const

  用法：声明只读的变量 (可理解为常量 ) 

  特点:同let命令
  注意事项:
         声明的同时必须立即赋值
         如声明的是简单类型的数据，变量值不可变

  实质:保证变量指向的内存地址所保存的数据不允许改动。

```javascript
// ES5变量声明（全局作用域，局部作用域）

var i = 2;
// for(var i = 0; i<10; i++) {
// }
// console.log(i)  输出10
// 使用let定义
function() {
  // ES5
  console.log(b)//输出undefined
  var b =10;// 存在变量提升，变量在后边声明，在前面也可以得到
  // ES6中在定义变量前使用的上述写法会报错
  // let b =20	// 重复声明也会报错
  // let b = 10;
}

```

#### 二.Symbol

ES5数据类型：

- Number(数字)
- String(字符 )
- Boolean(布尔值)
- Object(对象)
- Null(空对象指针)
- Undefined(声明的变量未被初始化时)

ES6新类型：Symbol

- 引入原因：

对象的属性名容易产生命名冲突，为保证键名的唯一性，故es6引入Symbol这种新的数据类型，确保创建的每个变量都是独一无二的 

- 特点：

Symbol类型的数据是类似字符串的数据类型，由于Symbol函数返回的值是原始类型的数据， 不是对象，因此Symbol函数前不能使用new命令，否则会报错。

可选参数。由于控制台输出不同的Symbol变量时都是Symbol()，故为了区分，可在创建Symbol变量时传一参数进行区分。

- 用法：

  - 用于定义对象的独一无二的属性名

  ```js
  let name = Symbol()
  // 方法一：
  let a = {}
  a[name] = 'Nick',
  // 方法二：
  let a = {
  	[name]: 'Nick'
  }
  // 方法三：
  let a = {}
  Object.defineProperty(a,name,{value:'Nick'})
  ```

  - 定义字符串常量

  ```js
  const name = Symbol("Nick")
  ```

  

```js
let a1 = Symbol('kk') //'kk'为对于symbol的描述
// 使用Symbol()是一个函数，不需要加new关键字
let a2 = Symbol('kk')
console.log(a1 === a2)   //false 独一无二的值

let a1 = Symbol.for('kk');  // 'kk'相当于key值
let a2 = Symbol.for('kk');
// console.log(a1 === a2)   //true
```

#### 三.解构赋值

ES6中只要数据可循环迭代（有Iterator接口)，都可以进行数组的解构赋值

- 使用场景：

  - 数组

    ```js
    let a,b,c
    [a,b,c] = [1,2] 
    
    let a,other
    [a,...other] = [1,2,3]
    
    let a,b
    [a,,b] = [1,2,3]
    ```

  - 对象

    ```js
    let a,b
    {a,b} = {a:2,b:3}
    
    let num,total
    {a:num,b:total} = {a:2,b:3}
    
    let b = {
    	name: 'Nick',
    	nameList:[{
    		name: 'KK'
    	}]
    }
    let {name:person,nameList:[{name:other}]} = b
    ```

  - 字符串

  - 布尔值

  - 函数参数

  - 数值

#### 四.字符串

```js
// ES5 JavaScript允许采用\uxxxx形式表示一个字符，这种表示法只限于码点在\u0000~\uFFFF之间的字符。
// 超出这个范围的字符，必须用两个双字节的形式表示，ES5却无法正确的识别这个有两个字节组成的字符。
const str1 = 'a'
const str2 = '\u20bb7'
console.log(str2)  // unicode超过ffff的会出现乱码
// ES6
const str3 = '\u{20bb7}'
console.log('str3', str3)   // ES6引入了花括号处理超过范围的码点
```

|             方法             |                           描述                           |
| :--------------------------: | :------------------------------------------------------: |
|  includes(string, position)  |       判断字符中是否包含指定字符 ，返回值是布尔值        |
| startsWith(string, position) |    判断字符串的开头是否包含指定字符 ，返回值是布尔值     |
|  endsWith(string, position)  |    判断字符串的尾部是否包含指定字符 ，返回值是布尔值     |
|          repeat(n)           |    repeat()  法返回一个新字符 ，表示将院字符 重复n 次    |
|                              |                                                          |
|          字符串补全          | 第一个参数是补全后的字符长度，第二个参数是用于补全的字符 |
|    padStart(length, str)     |                        于头部补全                        |
|     padEnd(length, str）     |                        于尾部补全                        |

引入了模板字符串：

```js
const name = "nick"
const age = 18
const str = '我叫'+name+',我今年'+age+'岁。'  // ES5写法
const str = `我叫${name}我今年${age}岁`      // ES6写法
const str2 = `我叫${name}，

 我今年${age}岁。`    // 可以输出相应的空格，回车
```

#### 五.数组

数组的拷贝

```js
// arr1与arr2指向同一地址
var arr1 = [1, 2, 3];
var arr2 = arr1;

// 拷贝
var arr1 = [1,2,3];
var arr2 = [...arr1];

// 分割数组
const totalList = [1, 'a', 'b', 'c']
let [, ...strList] = totalList
console.log(strList)

// 给函数传参
function add(x, y) {
    return x + y
}

let addList = [1, 2]
console.log(add(...addList))

```

深拷贝

```js
// ES6实现的数组的深拷贝方法1
var arr1 = [1,2,3];
var arr2 = Array.from(arr1);
```

新增的常用方法 

- fill

  ```js
  // fill
  const list = [1, 2, 3, 4, 5]
  let list2 = [...list].fill(3)
  let list3 = [...list].fill(3, 1, 4)  // [1,4)
  console.log(list2, list3) // [3,3,3,3,3]   [1,3,3,3,5]
  ```

- find  findIndex

  ```js
  // find返回第一个找到的结果
  // findIndex
  const list = [{ title: 'es6' }, { title: 'webpack', id: 2 }, { title: 'vue' }, { title: 'webpack', id: 3 }]
  let result = list.find(function (item) {
      return item.title === 'webpack'
  })
  let resultIndex = list.findIndex(function (item) {
      return item.title === 'webpack'
  })
  console.log(result, resultIndex)
  ```

- Includes  indexOf

  ```js
  // 判断简单类型数据
  const list = [1, 2, 3, 4, 5, 6]
  let result = list.includes(2)
  console.log('includes', result)
  ```

- flat

  ```js
  // 利用concat与扩展运算符，进行数组展开
  const list = [1, 2, 3, ['2nd', 4, 5, 6, ['3rd', 7, 8]]]
  let flatList = [].concat(...list)
  console.log(flatList)
  
  // 默认只展开第一层数组，可传参
  let flatList2 = list.flat(2)
  console.log('flat', flatList2)
  ```

- filter 

- 数组中的map和reduce

  - map 数据映射

    ```js
    // map 数据映射
    const json = [{ title: 'es6', status: 1 }, { title: 'react', status: 0 }, { title: 'webpack', status: 1 }, { title: 'vue', status: 1 }]
    let video = json.map(function (item) {
    		// 方法一：
        // return {
        //     name: item.title,
        //     statusTxt: item.status ? '已上线' : '未上线'
        // }
        // 方法二：
        let obj = {}
        Object.assign(obj, item)
        obj.status = item.status ? '已上线' : '未上线'
        return obj
    })
    console.log('json', json)
    console.log('video', video)
    ```

  - reduce

  - ```js
    /**
     * reduce 对数组中的每个元素进行一次回调，升序执行然后将回调值汇总一个返回值
     * @params cb(acc, currentValue, currentIndex, Array), initalValue
     * initalValue定义acc的返回值，未定义的话默认返回数组第一个值
     */
    const letterList = 'abcadefrd'
    const result = letterList.split('').reduce(function (acc, cur) {
        acc[cur] ? acc[cur]++ : acc[cur] = 1
        return acc
    }, {})
    console.log(result)		// 统计了字符串中字符出现的个数
    
    //展开多层数组
    const list = [1, ['2nd', 2, 3, ['3rd', 4, 5]], ['2nd', 6, 7]]
    const deepFlat = function(list) {
        return list.reduce(function(acc, cur) {
            return acc.concat(Array.isArray(cur) ? deepFlat(cur) : cur)
        }, [])
    }
    let flatList = deepFlat(list)
    console.log('reduce-flat', flatList)
    ```

- Array.from

  ```js
  // Array.from 类数组对象 有length,可遍历
  const str = 'hello'
  const strList = Array.from(str)
  console.log(strList)
  ```

#### 六.对象

- 扩展运算符的使用：

- 坑点：简单类型的时候，使用扩展运算符是没问题的，但是如果扩展运算符展开对象以后，还是一个对象的话，我们复制的只是一个指针

- 复制对象

  ```js
  const obj = { name: 'Nick', video: 'es6' }
  const initObj = { color: 'red' }
  let videoObj = { ...obj }
  console.log(videoObj)
  ```

  给对象设置默认值

  ```js
  let obj2 = { ...obj, name: 'Jack' }
  console.log(obj2)
  ```

  合并对象

  ```js
  let obj3 = { ...obj, ...initObj }
  console.log(obj3)
  ```

- 属性初始化的简写

  ```js
  // ES5
  let name = '小明'
  let age = 18
  let es5Obj = {
      name: name,
      age: age,
      sayHello: function () {
          console.log('this is es5Obj')
      }
  }
  // ES6
  let es6Obj = {
      name,
      age,
      sayHello() {
          console.log('this is es6Obj')
      }
  }
  ```

- 对象方法的简写

- 可计算的属性名

- ```js
  // ES5
  let key = 'name'
  let es5Obj = {}
  es5Obj[key] = '小明'
  // ES6
  let es6Obj = {
      [key]: '小红'
  }
  ```

- 新增方法

  - Object.is

    ```js
    // Object.is()和'==='
    let result = Object.is(NaN, NaN)
    console.log(result, NaN === NaN)	// true,false
    ```

  - Object.assign(目标对象，复制对象)     //浅拷贝

  - ```js
    const person = { name: '小米', age: 18, info: { height: 180 } }
    let person2 = {}
    Object.assign(person2, person)
    person.info.height = 160
    console.log(person2) // 改变了，浅拷贝
    ```

  - Object.keys

  - Object.values

  - Object.entries

    ```js
    // Object.keys() Object.values(), Object.entries()
    const json = { name: 'Nick', video: 'es6', date: 2019 }
    let obj = {}
    for (const key of Object.keys(json)) {
        obj[key] = json[key]	// 浅拷贝
    }
    console.log(obj)
    ```

#### 七.Map与WeakMap

提出背景：JavaScript中的对象，实质就是键值对的集合(Hash结构)，但是在对象中却只能用字符串作为键名。在一些特殊的场景中满足不了我们的需求，因此Map这一数据提出，它是JavaScript中的一种更完善Hash结构。

- Map对象

  用于保存键值对，任何值都可以作为一个键或者值（与对象最大的不同）

  ```js
  // set()添加元素
  let map = new Map();
  map.set([1,2,3], 'number')
  let map2 = new Map([['name', 'Nick'], ['sex', 'male']])
  // 链式写法
  map2.set('name', 'Jack').set('hobbies', ['swimming', 'running'])
  
  map2.get('age')
  map2.has('age')
  map2.delete('hobbies')
  map2.clear()
  ```

- 内置API

  - 遍历器生成函数

    keys

    values

    entries

  - 遍历器方法

    forEach

    ```js
    // keys() values() entries() 遍历器生成函数， forEach
    const map = new Map([
        ['name', '小明'],
        ['age', 20]
    ])
    // for of 循环 默认遍历entries
    for(let key of map) {
        console.log(key)
    }
    ```

  |      方法      |                      方法                      |
  | :------------: | :--------------------------------------------: |
  |      size      |                返回键值对的数量                |
  |    clear()     |                 清除所有键值对                 |
  |    has(key)    | 判断键值对中是否有指定的键名，返回值为布尔类型 |
  |   repeat(n)    |   获取指定键名的键值对，不存在返回undefined    |
  | set(key,value) |      添加键值对，如果键名已经存在，更新值      |
  |  delete(key)   |              删除指定键名的键值对              |

- WeakMap

  1. 只接受对象作为一个键名，不接受其他类型的数据作为键名

  2. WeakMap可以当键名引用销毁时，可以自动销毁。其他情况键名所指的对象不触发垃圾回收机制

  3. 没有clear， 没有size， 无法遍历

  ```js
  let weakmap = new WeakMap([
   [{name: 'hah'}, 'jack']
  ])
  console.log(weakmap)
  // 操作dom，可以将dom当做键，当dom销毁时，对象也会被销毁
  const ulObj = document.getElementById('test')
  // 其他类型数据，需要手动进行清空
  let obj ={name: 'jack'}
  let array = [obj, 'person']
  array[0] = null
  ```

#### 八.Set与WeakSet

- Set

  ES6给开发者提供的 种类似数组的数据结构，可以理解为值的集合。它和数组的最大的区别就在于: 它的值不会有重复项。

  特点：成员值唯一

  属性及方法

|            方法            |                    描述                    |
| :------------------------: | :----------------------------------------: |
|            size            |                返回成员个数                |
|          clear()           |                清楚所有成员                |
| endsWith(string, position) | 判断键值对中是否有指定值，返回值为布尔类型 |
|       delete(value)        |                 删除指定值                 |
|         add(value)         |                  添加元素                  |

遍历器生成函数

​	keys

​	values

​	entries

​	foreach

```js
// keys(), values(), entries(), set里面key和value的值相等, for of 默认遍历values
const set = new Set([1, 2, 3, 4, 5])
for (const value of set.entries()) {
    console.log(value)
}
```

使用场景：数组去重

```js
const array = [1, 2, 4, 5, 1, 2, 5, 7, 9, 7]
let unique = new Set(array)
let uniqueArray = Array.from(unique)
console.log(uniqueArray)
```

- WeakSet

  1. 元素只能是对象， 对象也是弱引用

  2. 无法遍历， 没有size， 也没有clear

#### 九.数组，对象，Map，Set

```js
// 增加
array.push(gooditem)
obj['fruit'] = 'apple'
map.set('fruit', 'apple')
set.add(gooditem)
// 查询
const resultArray = array.includes(gooditem)
const resultObj = 'fruit' in obj
const resultMap = map.has('fruit')
const resultSet = set.has(gooditem)
// 修改
array.forEach(function (item) {
    item.fruit = item.fruit ? 'orange' : ''
})
obj['fruit'] = 'orange'
map.set('fruit', 'orange')
set.forEach(function (item) {
    item.fruit = item.fruit ? 'orange' : ''
})
// 删除
const index = array.findIndex(function (item) {
    return item.fruit
})
array.splice(index, 1)
delete obj.fruit
map.delete('fruit')
set.delete(gooditem)
// 类型转换 map和对象间的转换
let obj = {
    name: 'Nick',
    hobbies: 'swimming'
}
console.log(Object.entries(obj))
let map = new Map(Object.entries(obj))
console.log('map', map)

let obj2 = Object.fromEntries(map)
console.log('obj', obj2)

// 数组和set
let array = [1, 2, 3, 4, 5]
let set = new Set(array)
console.log('set', set)
let array2 = Array.from(set)
console.log('array', array2)
```

#### 十.proxy与reflect

Proxy：代理，代理对象的一些操作

```js
/* @params
** target:  Proxy包装的目标对象
** handler:  个对象，对代理对象进行拦截操作的函数，如set、get */
let p = new Proxy(target, handler)
```

示例：

```js
// Proxy, 代理的就是对象的一些操作

let account = {
    id: 9923,
    name: 'admin',
    _private: 'test',
    phone: '13812345678',
    create_time: '2019'
}

let accountProxy = new Proxy(account, {
    // 拦截读取和设置的操作
    get: function (target, key) {
        switch (key) {
            case 'phone':
                return target[key].substring(0, 3) + '****' + target[key].substring(7)
            case 'create_time':
                return target[key].replace('2019', 2020)
            default:
                return target[key]
        }
    },

    set: function (target, key, value) {
        if (key === 'id') {
            return target[key]
        } else {
            return target[key] = value
        }
    },

    // 拦截 key in object 
    has: function(target, key) {
        if(key in target) {
            console.log(`${key}：`, target[key])
            return true
        } else {
            console.log('并无此属性')
            return false
        }
    },

    // 拦截delete
    deleteProperty: function(target, key) {
        if(key.indexOf('_') === 0) {
            console.warn('私有属性不能被删除')
            return false
        } else {
            delete target[key]
            return true
        }
    },

    // 拦截Object.keys()
    ownKeys(target) {
        return Object.keys(target).filter(function(item) {
            return item !== 'id' && item.indexOf('_') !== 0
        })
    }
})
```

Reflect：ES6推荐的操作对象的方法，所有对于对象的操作都可以用reflect实现

```js
let obj = {
    name: 'Nick',
    age: '32',
    sex: 'male',
    hobbies: 'swimming'
}

console.log(Reflect.get(obj, 'name'))
Reflect.set(obj,'name', 'Jack')
console.log(obj.name)
// 'name' in obj
Reflect.has(obj, 'name')
```

利用Proxy和Reflect实现数据双向绑定

```js
// 获取dom元素
const inputObj = document.getElementById('input')
const txtObj = document.getElementById('txt')

// 初始化代理对象
const obj = {}

// 代理选项
const handler = {
    get: function(target, key) {
        return Reflect.get(target, key)
    },

    set: function(target, key, value) {
        if(key === 'text') {
            inputObj.value = inputObj.value === value ? inputObj.value : value
            txtObj.innerHTML = value
        }
        return Reflect.set(target, key, value)
    }
}

let objProxy = new Proxy(obj, handler)

// 给input添加键盘键入事件
inputObj.addEventListener('keyup', function(e) {
    objProxy.text = e.target.value
    console.log(objProxy)
})

objProxy.text = '124'
```

#### 十一.函数

- 函数默认参数

```js
// ES5默认参数
function es5Print(x, y) {
    y = y || 'world'
    console.log('es5', x + y)
}
es5Print('hello', '')
// ES6
function es6Print(x, y = 'world') {
    console.log('es6', x + y)
}
es6Print('hello', '')
```

- rest参数（不定参数）

```js
// rest
function add(...rest) {
    let sum = 0
    console.log(rest)
    for (let value of rest) {
        sum += value
    }
    console.log(sum)
    // Array.prototype.method.apply(argument) // ES5中的使用方法
}
add(1, 2, 3, 4, 5)
```

- 扩展运算符
- 尾调用

```js
// 尾调用
function step2(x) {
    console.log('尾调用', x)
}
function step1(x) {
    return step2(x)
}
```

- 箭头函数

  特点：

  - 更短的函数
  - 不绑定this，arguments，super或 new.target，指向声明的对象

  声明函数

  ```js
  // 声明函数
  const arrow = (x) => {
      console.log('箭头函数')
  }
  ```

  注意事项：

  - 什么情况使用

    Object.method()调用的话就用普通函数进行申明，其他情况下都用箭头函数，例如setTimeout(()=>{})

  - 箭头函数没有argument

箭头函数有几个使用注意点。

（1）函数体内的`this`对象，就是定义时所在的对象，而不是使用时所在的对象。

（2）不可以当作构造函数，也就是说，不可以使用`new`命令，否则会抛出一个错误。

（3）不可以使用`arguments`对象，该对象在函数体内不存在。如果要用，可以用 rest 参数代替。

（4）不可以使用`yield`命令，因此箭头函数不能用作 Generator 函数。

可以让setTimeout中的this绑定定义时所在的作用域

对于函数的`this`指向问题：

1. 箭头函数的`this`永远指向其上下文的 `this`，任何方法都改变不了其指向，如`call(), bind(), apply()`
2. 普通函数的`this`指向调用它的那个对象

#### 十二.类和继承

ES5之前JS没有类的概念，是基于原型的面向对象语言，原型对象特点就是将自身的属性共享给新对象

- new操作，做了以下的事情

  - 产生一个新的对象

  - 将这个空对象的\_proto\_指向了构造函数内部的prototype

  - 将构造函数的this绑定到这个对象上(即new创建的对象，其函数体内的this指向的是这个对象)

  - 返回到这个新对象上

    ```js
    const obj = {}
    obj._proto_ = 构造函数.prototype
    构造函数.call(obj)
    ```

传统写法，通过原型

```js
// ES5的时候是通过构造函数来实现类的功能的
function Person(name, age) {
    this.name = name
    this.age = age
}
Person.prototype.sayHello = function () {
    console.log(`大家好， 我叫${this.name}，我今年${this.age}岁了`)
}

const p = new Person('小明', 17)
console.log(p)
```

ES6写法

```js
// ES6改造ES5实现类的方法
class Person {
    constructor(name, age) {
        this.name = name
        this.age = age
    }
    sayHello() {
        console.log(`大家好， 我叫${this.name}，我今年${this.age}岁了`)
    }
}
const p = new Person('小红', 17)
console.log('class', p)
console.log(typeof Person) // function
```

类的继承

```js
//ES5传统写法原型继承
function Person(name,age){ // 类、构造函数
    this.name = name;
    this.age = age;
}
Person.prototype.showName = function(){
    return this.name;
};
Person.prototype.showAge = function(){
    return this.age;
};
// 工人类
function Worker(name,age){
    // 属性继承过来
    Person.apply(this,arguments);
}
// 原型继承
Worker.prototype = new Person();
```

ES6继承

```js
class Person{
    // 构造器
    constructor(name,age){
        this.name = name;
        this.age = age;
    }
    showName(){
        return this.name;
    }
    showAge(){
        return this.age;
    }
}
class Worker extends Person{
    constructor(name,age,job='啦啦啦'){
        // super放在构造函数最前边，继承超父类的属性
        super(name,age);
        this.job = job;
    }
    showJob(){
        return this.job;
    }
}
```

类的get，set方法

```js
class Person {
    constructor(name = 'Nick') {
        this.name = name
    }
    get fullName() {
        return this.name + '\xa0' + 'Liu'
    }
    set fullName(value) {
        this.name = value
    }
}
const p = new Person()
console.log('get', p.fullName)
p.fullName = 'Jack'
console.log('set', p.name)
```

定义静态方法（通过类名调用，不能被继承）

```js
// 定义静态方法
class Person {
    constructor(name = 'Nick') {
        this.name = name
    }
    static sayHello(obj) {
        console.log('my name is ' + obj.name)
    }
}

const p = new Person('小花')
Person.sayHello(p)
```

定义静态属性

```js
// 定义静态属性
class Person {
    static prop = 'test' // ES7
    constructor(name = 'Nick') {
        this.name = name
    }
    static sayHello(obj) {
        console.log('my name is ' + obj.name)
    }
}
// Person.prop = 'test'   //ES6
console.log(Person.prop)
```

#### 十三.import与export

ES6之前没有模块的说法

模块化开发方案：

- CommonJS：CommonJS是Node中的模块化规范以及原生模块

- AMD和RequireJS：AMD是"Asynchronous Module Definition"的缩写，采用异步方式加载模块，模块的加载不影响它后面语句的运行 。所有依赖这个模块的语句，都定义在一个回调函数中，等到所有依赖加载完成之后(前置依赖)，这个回调函数才会运行

- Import和Export（ES6）

#### 十四.异步

- 同步：当一个"调用"发出时，在没有得到结果之前，这个"调用"就会阻塞后面代码的执行，得到结果的时候才会返回。"调用者"要主动等待代码的执行结果，得到返回结果后，程序才会继续运行 。 

- 异步："调用"发出的时候，就直接返回，对应的结果会通过状态、通知来告诉"调用者"或通过回调函数处理这个调用。异步调用发出后，不会阻塞后面的代码。
- JS为什么引入异步
  - JS是单线程的
  - 同步代码会阻塞后面的代码
  - 异步不会阻塞程序的运行
- 异步的实现
  - 回调函数
  - setInterval和setTimeout
  - Promise
  - Generator
  - async

#### 十五.Promise

应用场景，axios中ajax请求返回一个Promise对象

结合async函数，异步编程同步化

为了解决回调地狱，提出了Promise对象

```js
// 回调地狱，回调函数写法臃肿，可读性差
function ajax(cb) {
    setTimeout(() => {
        cb && cb(() => {
            console.log('任务2')
        })
    }, 1000)
}
ajax((cb2) => {
    console.log('任务1')
    setTimeout(() => {
        cb2 && cb2()
    },1000)
})
```

Promise是一个对象，应用场景：当XXX执行完毕的时候，then执行XXX动作，Promise里不仅可以存放着异步的代码，也可以存放同步代码。

```js
// Promise改造回调函数，通过.then链式编写了上面的功能
function ajax() {
    return new Promise((resolve, reject) => {
        setTimeout(() => resolve(), 1000)
    })
} 
ajax()
    .then(() => {
        console.log('任务1')
        return new Promise(resolve => {
            setTimeout(() => resolve(), 1000)
        })
    })
    .then(() => {
        console.log('任务2')
    })
```

Promise的使用：

- 封装一个Promise

- 捕获异常

  ```js
  // 使用catch方法捕捉错误
  function judgeNumber(num) {
      return new Promise((resolve, reject) => {
          if (typeof (num) === 'number') {
              resolve(num)
          } else {
              const err = new Error('请输入数字')
              reject(err)
          }
      })
  }
  judgeNumber('2')
      .then(num => console.log(num))
      .catch(err => console.log(err))
  ```

- Promise.all，当传入的所有Promise函数状态改变之后，才会执行下一步

- Promise.race，多个Promise中，只要有一个执行成功就可以

```js
// Promise.all示例：当所有图片全部加载完成后，统一渲染
const imgUrl1 = 'http://xd-video-pc-img.oss-cn-beijing.aliyuncs.com/xdclass_pro/video/1901/vue/vue.png'
const imgUrl2 = 'http://xd-video-pc-img.oss-cn-beijing.aliyuncs.com/xdclass_pro/video/1901/webpack/webpack.png'
const imgUrl3 = 'https://xd-video-pc-img.oss-cn-beijing.aliyuncs.com/xdclass_pro/video/2019_frontend/html_css/html.png'

function getImage(url) {
    return new Promise((resolve, reject) => {
        const img = document.createElement('img')
        img.src = url
        img.onload = () => resolve(img)
        img.onerror = (err) => reject(err)
    })
}

function showImage(imgs) {
    imgs.forEach(item => {
        document.body.appendChild(item)
    })
}

Promise.all([getImage(imgUrl1), getImage(imgUrl2),getImage(imgUrl3)]).then(showImage)

function showFirstImage(img) {
    document.body.appendChild(img)
}
Promise.race([getImage(imgUrl2),getImage(imgUrl1),getImage(imgUrl3)]).then(showFirstImage)

```

#### 十六.Iterator接口

- Iterator接口，给不同的数据结构提供统一的循环方式

- 作用：
  - 为不同的数据结构提供统一的访问接口
  - 将数据成员按照一定的顺序输出
  - 提供给ES6中的for of循环语句进行使用

- 具备原生的iterator接口的数据结构

  - Array
  - String
  - Set
  - Map
  - 函数的argument对象

- 默认的Iterator接口

  - Symbol.iterator
    - 本质，一个函数，是当前的数据集合默认的遍历器生成函数，执行函数，会返回一个遍历器
    - 返回值，返回一个遍历器对象，这个对象里的特点就是有一个next()方法，每次调用next()方法可以返回描述当前成员的信息对象，具有value和done两个属性

  ```js
  const arr = [1, 2, 3]
  const fn = arr[Symbol.iterator]()
  console.log(fn.next())
  console.log(fn.next())
  console.log(fn.next())
  console.log(fn.next())
  ```

  ```js
  // 应用场景 实现对象的for of
  const obj = {
      color: 'red',
      price: 18,
      size: 'small',
      [Symbol.iterator]() {
          let index = 0
          const values = Object.values(this)
          return {
              next() {
                  if(index < values.length) {
                      return {
                          value: values[index ++],
                          done: false
                      }
                  } else {
                      return {
                          done: true
                      }
                  }
              }
          }
      }
  }
  
  for (const value of obj) {
      console.log(value)
  }
  ```

  

#### 十七.Generator

- Generator用于生成一个迭代器Iterator

- next()

- yield：相当于可以写多次的return语句

- 应用场景

- ```js
  const say = function* () {
    yield 'a'
    yield 'b'
    yield 'c'
  }
  const fn = say();
  console.log(fn.next())
  ```

  ```js
  // 通过Generator函数可以直接定义对象的Symbol.iterator
  let obj = {
      a: 1,
      b: 2,
      c: 3
  }
  
  obj[Symbol.iterator] = function* () {
      for (const key of Object.keys(obj)) {
          yield obj[key]
      }
  }
  
  for (const value of obj) {
      console.log(value)
  }
  ```

  ```js
  // 定义状态基
  const state = function* () {
      while(1) {
          yield 'success'
          yield 'fail'
          yield 'pending'
      }
  }
  const stateData = state()
  console.log(stateData.next())
  console.log(stateData.next())
  console.log(stateData.next())
  console.log(stateData.next())
  ```

  ```js
  // 长轮询，例如判断用户是否完成支付
  function fn1() {
      return new Promise(resolve => {
          setTimeout( () => {
              console.log('查询中')
              resolve({code: 0})
          },1000)
      })
  }
  
  const getStatus = function* () {
      yield fn1()
  }
  
  function autoGetStatus() {
      const gen = getStatus()
      const status = gen.next()
      status.value.then(res => {
          if(res.code === 0) {
              console.log('用户付款成功')
          } else {
              console.log('暂未付款')
              setTimeout( () => autoGetStatus(), 500)
          }
      })
  }
  autoGetStatus()
  ```

  ```js
  // Generator实现异步
  const ajax = function* () {
      console.log('start')
      yield function (cb) {
          setTimeout(() => {
              console.log('异步任务结束')
              cb && cb()
          }, 1000)
      }
      console.log('end')
  }
  
  const runAjax = ajax()
  const first = runAjax.next()
  first.value(() => runAjax.next())
  ```

#### 十八.async

- async是异步的简写，用于声明一个函数是异步函数

- await等的是什么？await是一个等待的表达式，这个表达式的计算结果是Promise对象或者其他值，通常等待Promise的resolve和reject

  async函数时Generator的语法糖，async中定义的await相当于，generator中定义的yeild，不过调用async函数会自动调用了Generator的next方法。 

  ```js
  function fn1() {
      return new Promise(resolve => {
          setTimeout(() => {
              console.log('任务1')
              resolve()
          },1000)
      })
  } 
  
  function fn2() {
      return new Promise(resolve => {
          setTimeout(() => {
              console.log('任务2')
              resolve()
          },1000)
      })
  }   
  
  function fn3() {
      return new Promise(resolve => {
          setTimeout(() => {
              console.log('任务3')
              resolve()
          },1000)
      })
  }  
  
  async function init(fn1,fn2,fn3) {
      await fn1()
      await fn2()
      await fn3()
  }
  init(fn1, fn2, fn3)
  ```

  



