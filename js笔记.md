#### 一.数据类型：

- 6种基本数据类型：undefined，null，boolean，number，string，object
- typeof操作符，可能的返回值：undefined，boolean，number，string，object（对象或null），function
- Boolean类型与其他类型的转换关系

| 数据类型  | true                   | false     |
| --------- | ---------------------- | --------- |
| String    | 非空字符串             | “”        |
| Number    | 非零数值               | 0和NaN    |
| Object    | 任何对象，包括空对象{} | null      |
| Undefined | n/a                    | undefined |

- Number，对于浮点数会产生舍入误差，特例：判断 if(0.1+0.2==0.3)会返回false。

能够表示的最大，最小数值为Number.MAX_VALUE，Number.MIN_VALUE。

超出范围的值会被转换为 Infinity，-Infinity。

访问Number.POSITIVE_INFINITY,Number.NEGATIVE_INFINITY会返回相应值

NaN两个特殊的点：任何涉及NaN的操作都会返回NaN，NaN与任何值都不相等包括自己本身

数值转换函数：Number（），parseInt（），parseFloat（）

- Object的每个实例都具有如下属性和方法：

  constructor：构造函数

  hasOwnProperty(PropertyName)：用于稽查给定属性在当前对象中是否存在

  isPrototypeOf(object)：检查传入对象是否为当前对象的原型

  propertyIsEnumerable（propertyName）：检查属性是否可以用于for in语句来枚举

  toLocalString()：返回字符串，与执行环境有关

  toString（）

  valueOf（）：通常与toString（）返回相同值

  为了区分Object对象具体是什么类型的对象，引入了instanceof操作符，可以用来验证引用类型数据是Array，RegExp等

- 基本数据类型和引用数据类型：
  - 基本类型值在内存中占据固定大小空间，因此保存在栈内存中。
  - 从一个变量向另一个变量复制基本类型的值，会创建这个值的副本
  - 引用类型的值是对象，保存在堆内存中。
  - 包含引用类型值得变量实际上包含的并不是对象本身，而是一个指向该对象的指针
  - 从一个变量向另一个变量复制引用类型的值，复制的其实是指针，因此两个变量指向同一对象
  - 使用typeof操作符来确定一个值属于哪种基本类型
  - 使用instanceof操作符来确定一个值属于哪种引用类型

#### 二.操作符

- 一元操作符：++，--
- 位操作符：~，&，|，^，<<，>>，>>>
- 布尔操作符：！，&&，||
- 乘性操作符：*，/，%
- 加性操作符：+，-
- 关系操作符：<，>，<=，>=

- 相等操作符

  == 与 !=：先进行强制类型转换，在比较是否相等

  特殊情况：

  - null == undefined  true

  - NaN == NaN false
  - NaN != NaN true
  - false == 0
  - true == 1	
  - undefined == 0 false
  - null == 0 false

  === 与 !==：比较前不进行类型转换

  - null === undefined false

- 条件操作符：?XXX :YYY

- 赋值操作符：=，(*/%+-)=

- 逗号操作符：可以在一条语句中执行多个操作，常用于声明变量

#### 三.语句

- if语句
- do-while
- while
- for
- for-in，可以用来枚举对象的属性
- label可以在代码中添加标签，由break和continue引用
- break，continue
- with，可将代码作用于设置到一个特定对象，性能下降，不建议使用
- switch，可以使用任何数据类型

#### 四.函数

- function（）来定义
- 无需指定函数的返回值，可以在任何地方返回任何类型的值
- 没有函数签名的概念，因为函数参数以一个包含零或多个值得数组形式的arguments传递的
- 可以向函数传递任意数量的参数，并且可以通过arguments对象来访问这些参数
- 由于不存在函数签名的特性，无法实现函数的重载
- 函数参数按值传递

#### 五.执行环境和作用域

```js
var color = "blue"
function changeColor() {
	var anotherColor = "red"
	function swapColors() {
		var tempColor = anotherColor
		anotherColor = color
		color = tempColor
	}
	swapColors()
}
changeColor
```

- 所有变量都存在于一个执行环境（作用域）中，这个执行环节决定了变量的生命周期，以及那一部分代码可以访问其中的变量
- 执行环境：分为全局执行环境（全局环境windows）和函数执行环境
- 每次进入一个新的执行环境，都会创建一个用于搜索变量和函数的作用域链
- 函数的局部环境不仅可以访问函数作用域中的变量，还有权访问其父环境，乃至全局环境。
- 全局环境只能访问全局环境中的变量和函数
- 作用域链：内部环境可以通过作用域链访问所有外部环境，二外部环境不可访问内部环境中任何变量和函数。

- 作用域链的用途：保证对执行环境有权访问的所有变量和函数的有序访问
- 作用域链的前端，始终是当前执行的代码所在环境的变量对象
- 任何环境可以向上搜索作用域链，任何环境都不可以向下搜索作用域链而进入另一个执行环节。

windows

​	|__color

​	|__changeColor（）

​				|__anotherColor

​				|__swapColors（）

​								|__tempColor		

- 延长作用域链：当执行流进入下面语句时，作用域链会得到延长
  - try-catch中的catch块：会创建一个新的变量对象，其中包含被抛出的错误对象的声明
  - with语句：会将指定的对象添加到作用域链中
- ES6之前无块级作用域的概念
- 查询标识符，在某环境中为引入一个标识符时，会从作用域链的前端开始，向上逐级查询与给定名字匹配的标识符，一直追溯到全局环境。过程中，存在一个局部的变量的定义，搜索会自动停止。
- 变量的执行环境有助于确定何时释放内存
- 垃圾回收
  - 标记清除，为变量标记“进入环境”，“离开环境”，IE，Firefox，chrome，safari都用这种
  - 引用计数，跟踪记录每个值被引用的次数。循环引用时，会存在大量内存得不到回收。Netscape Navigator3.0使用，4.0转为标记清除方式。但IE浏览器非原生JS对象（如DOM元素）等还是采用引用计数，因此可能会存在循环引用的问题

#### 六.引用数据类型

##### 6.1Object类型

- 创建方式：

  ```js
  // 方法一
  var obj = new Object()
  obj.name = "LZW"
  obj.age = 18
  // 方法二 字面量表示法，创建Object不会调用Object构造函数
  var obj = {
  	name: "LZW",
  	age: 18
  }
  ```

- 访问对象属性

  ```js
  // .点表示法
  obj.name
  // []方括号语法，用于通过变量访问属性
  obj[name]
  ```

##### 6.2 Array类型

- 与其他语言不同，JS中的数组的每一项可以保存任何类型的数据。

- 且数组长度可变

- 创建方式

  ```js
  // 方法一
  var arr = new Array()
  // 方法二 字面量表示法，不调用Array构造函数
  var arr = ["cat","dog"]
  ```

- length属性，不是只读的，可以通过设置，从数组末尾删除数组中的项，或在末尾添加新增项。

  - arr[arr.length] = "pig"

- 检测数组：除了instanceof Array，还可以用Array.isArray()

- 转换方法：toString, toLocaleString, valueOf，join()方法

  ```js
  var colors = ["red","green","blue"]
  console.log(colors.toString())  // red,green,blue
  // toString,依次调用了数组元素的toString，toLocaleString与其类似会依次调用toLocaleString
  console.log(colors.valueOf()) // red,green,blue 
  // valueOf返回数组本身，在输出时调用了toString方法
  console.log(colors) // red,green,blue
  // join()方法，可使用不同的分割符号来构建最终的输出字符串。
  console.log(colors.join("|")) // red|green|blue
  ```

- 栈方法
  - push()，可接收任意数量的参数，并逐个添加到数组末尾，并返回修改后长度
  - pop()，从数组末尾移除一项，减少length，返回移除项

- 队列方法（使用push和shift可实现队列，使用unshift和pop可以实现反方向队列）
  - shift()，从数组前端移除一项，减少length，返回移除项
  - unshift()，在数组前端添加任意个项，并返回数组修改后长度

- 重排序方法
  - reverse()，翻转数组
  - sort()，按照升序排列数组向（最小项在前面），默认通过调用toString，比较字符串会出现乱序，因此sort函数可接收比较函数

- 操作方法

  - concat()，用于连接数组，或创建副本，调用该函数的原数组值不变
  - slice(a,b)，用于创建包含原数组中[a,b)的新数组，原数组值不变
  - splice()：以数组形式返回从原始数组中删除的项，会改变调用的数组
    - 删除：可删除任意数量的项，splice(要删除的第一项index，删除个数)
    - 插入：可向指定位置插入任意数量的项splice（起始位置，0删除数，要插入的任意个项）
    - 替换：同理

- 位置方法

  - indexOf()，从位置0开始查找

  - lastIndexOf()，从末尾开始查找

    都可接收两个参数，要查找的项和查找起点位置索引（可选），返回所找项第一次出现的索引，未找到返回-1。

    比较是采用===

- 迭代方法

  - every()，对每一项执行函数，若每一项返回true，则返回true

  - filter()，对每一项执行函数，返回该函数会返回true的项组成的数组

  - forEach()，对每一项执行函数，返回undefined

  - map()，对每一项执行函数，返回每次调用结果组成的数组

  - some()，对每一项执行函数，若其中任意一项返回true，则返回true

    且都不会修改原数组

- 归并方法

  - reduce()，迭代数组所有项，从数组第一项开始，逐个遍历到最后

  - reduceRight()，迭代数组所有项，从数组最后一项开始，遍历到第一项

    两个函数可接收两个参数：每一项上调用的函数，作为递归基础的初始值

    传给reduce()和reduceRight()的函数可接收4个参数：前一个值，当前值，项的索引值和数组对象。该函数返回的任意值都会作为第一个参数自动传给下一项。

    ```js
    // 数组求和的递归实现
    var value = [1,2,3,4,5]
    var sum = value.reduce(function(prev,cur,index,array){
    	return prev + cur
    })
    ```

##### 6.3 Date类型

- toDateString()
- toTimeString()
- toLocaleDateString()
- toLocaleTimeString()
- toUTCString()

##### 6.4 RegExp类型

- 模式：
  - g全局模式
  - i不区分大小写
  - m多行模式
- 方法：
  - exec()
  - test()，最常用

##### 6.5 function类型

- JS中函数实际上是对象。函数名相当于指针。

- Function构造函数可以接收任意数量的参数，但最后一个始终被看做函数体。

- 因此JS中函数可以定义为

- ```js
  // 函数表达式
  var sum = function(num1,num2){
  	return num1+num2
  }
  // 还可以这样将一个函数的引用付给另一个函数
  var anothersum = sum	// 调用anothersum可以得到与sum同样的效果
  ```

- 没有重载，当生命了两个同名函数时，相当于给一个对象赋值，最后一次的赋值将前面的覆盖了。

- 函数声明与函数表达式：

  - 解析器会率先读取函数声明，使其在执行任何代码之前可用
  - 而对于函数表达式，则必须等到解析器执行到所在的代码行，才会被解释执行。

- 作为值的函数：JS中，可用将函数作为值来使用

  - 可像传递参数一样把一个函数传给另一个函数
  - 也可用把一个函数作为另一个函数的结果返回。

- 函数内部属性

  - arguments：类数组对象，包含传入函数的所有参数，其中具有一个名为callee的属性，该属性是一个指针，指向拥有这个arguments对象的函数。
  - this：引用的是函数执行的环节对象

  