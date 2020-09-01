#### ECMAScript 6 es2015 新 js

##### const 和 let

let const 和 var 的不同

- 不能重复声明
- 没有声明提升
- 存在块级作用域(作用域被定义在 {} 内。{}是局部作用域)

const 是声明常量(不可修改的例如 π)的,常量的名称都是`全大写`的
let 声明的变量是可以被修改的

 - 写在后面
   - 一共有两个类型：值的类型，引用类型。
       - 值的类型包括：null,undefined,数值,字符串,布尔，值的类型保存与复制的是值本身，const 所定义的`值的类型`常量，`值`不可以改变。  
       - 引用类型包括：对象object(function,array,Date)，对象类型保存与复制的是指向对象的一个指针，const 所定义的`对象类型`常量，`地址`不可以改变。

 ```js    
    // 1. 值的类型保存与复制的是值本身，const在这里所定义的是数值型常量，存储的是值本身，常量值类型的 值 是不可以改变的，所以下边这个操作会出错。
    const num = 100
    num = num + 1

    // 2. 对象类型保存与复制的是指向对象的一个指针，const在这里所定义的是对象，存储的是指向该对象的地址，对象类型的 地址不改变就行，所以下边这个操作不会出错。
    //下边这个操作就是把 obj 对象里添加了一个属性，但是 obj 对象的地址没有改变.
    const obj = {
      name: '吕布',
      age: 28,
    }
    obj.level = 15

    // 3. 而下面这个操作将 obj 对象的地址改变了，所以会出错 Assignment to constant variable。
    const obj = {
      name: '吕布',
      age: 28,
    }
     obj = {
      name: '吕布',
      age: 28,
    }
 ```

##### 变量的解构赋值

对象解构赋值

```js
const obj = {
  username: "貂蝉",
  userage: 18,
  level: 10,
};
//1.顺序无所谓，名字必须相同，对上即可。
//2.没有对应的名字，obj对象中的属性(如:level)就没有使用到。
//3.用冒号":"可以改名。
const { username, userage: age } = obj;
console.log(username, age);
```

数组的解构赋值

```js
const arr = [1, 2, 3, 4, 5];
const [a, b, c] = arr;
// abc 的值分别是1，2，3；所以数组的解构赋值是按顺序来的
console.log(a, b, c);
```

函数参数的解构赋值

```js
const obj = {
  username: "貂蝉",
  userage: 18,
  level: 10,
};
function showInfo({ username, level }) {
  // const { username, level } = obj
  console.log(`该英雄的名称是${username}`, `等级${level}`);
}
showInfo(obj);
```

技巧: 实现变量调换
```js
let x = 1;
let y = 2;

[x, y] = [y, x];
```

##### 字符串的扩展

模版字符串

```js
const username = "lucy";
console.log(`my name is ${username}`);
```

新增的字符串方法
indexOf(`任意字符串`，查看位置，母串中的位置从0开始，找不到返回-1)； 
charAt(`数值型`，是几就拿到字符串中第几个)； 
includes(`任意字符串`，是否包含什么，返回true或false)； 
startsWith(`任意字符串`，是否以什么开头，返回true或false)； 
endsWith(`任意字符串`，是否以什么结尾，返回true或false)；
trim(删除字符串`头部和尾部空格`并返回新字符串,不会修改原始字符串)； 
trimStart(删除字符串`头部空格`并返回新字符串,不会修改原始字符串)；
trimEnd(删除字符串`头部空格`并返回新字符串,不会修改原始字符串),以前是 trimRight() ；
某个字符串a.padStart(`数值`，'补齐时用的字符串b')用 b 补齐 a ，将 a 补齐到`第 数值` 位；
某个字符串a.padEnd(`数值`，'补齐时用的字符串b')用 b 补齐 a ，将 a 补齐到`倒数第 数值`位；
match(用正则表达式取字符串：如果正则表达式没写全局，取一个；写了全局，取多个)；用法 `字符串.match(正则表达式)`
matchAll(正则表达式不写全局，也可以取多个)；用法 `字符串.matchAll(正则表达式)`.

##### loadsh 插件 
包含了所有的基础数据的处理方式，使用时用 '-' 表示 (jquery 用 '$' 表示)

##### 函数的扩展

函数参数的默认值

 - 普通方式(函数参数非对象)
 直接`在参数处赋值`即可，参数就有默认值了，当不传值时参数就使用默认值
```js

const fun = function (color = "黑色", bgColor = "红色") {
  console.log("颜色:::", color);
  console.log("背景色:::", bgColor);
};
fun("蓝色");
```

 - 参数为对象
  应用到了`函数参数的解构赋值`,直接`函数参数(对象的属性)处赋值`即可，参数就有默认值了，当不传值时参数就使用默认值
  
```js
const fun = function ({ color = "黑色", bgColor = "蓝色" }) {
  console.log("颜色:::", color);
  console.log("背景色:::", bgColor);
};
fun({ color: "粉色" });
// 不能什么都不传，最起码传递一个空对象；因为不传的话，值是undefined，没法解构赋值。
```

 - 类数组(以后学了在补)
  1. 类数组(arguments) --->  数组([...arguments])，即：类数组 转变成 数组加上 `...` 和 `[]` 即可。
```js 
  function add(){
     [...arguments].forEach(function (ele) {
     // 值是 1-->6
     console.log(ele)
     })
     // 值是 [1，2, 3, 4, 5, 6]
     console.log([...arguments])
  }
  add(1,2,3,4,5,6)
```

 - rest(剩余) 参数
 1. `函数参数名`可以是任意的，但必须加上 `'...'` 才是剩余参数。
 2. `剩余参数`必须是`余下的`，`剩余的`，剩余参数后边不在可以有别的参数。
```js
function add(...rest) {
  // function add(a,...xxx) {} 正确
  // function add(a,...xxx,b) {} 错误
  console.log(rest); 
  // 值是 1-->10； rest 是数组，不是类数组。
}
add(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
```
  
箭头函数
写法：省略了function，所以就没有函数式声明，只能变量式声明。

```js
// function add(num1, num2) {
//   return num1 + num2
// }
const add = (num1, num2) => num1 + num2;
// 箭头函数定义只能变量式定义，因为省略了function，所以就没有函数式声明，只能变量式声明。
// 箭头左边是 函数的参数部分 使用小括号包裹参数逗号拼接,当参数只有一个的时候可以省略小括号
// 箭头右边是 函数主体，使用花括号包裹，返回值设置依然使用 return。当函数不需要操作就设置返回值的话可以省略花括号和 return 直接写返回值即可
const res = add(10, 20);
console.log(res);
```

箭头函数和普通函数的区别

- 函数体内的 this 对象，就是定义时所在的对象，而不是使用时所在的对象。
- 不可以当作构造函数，也就是说，不可以使用 new 命令，否则会抛出一个错误。
- 不可以使用 arguments 对象，该对象在函数体内不存在。如果要用，可以用 rest 参数代替。
- 不可以使用 yield 命令，因此箭头函数不能用作 Generator 函数。

##### 数组的扩展

- 第一个方法
Array.from(): 将类数组(注意：类数组的起始位置从 0 开始依次往后)转化为数组，否则 from 转换不了

```js
const fun1 = function () {
  console.log(arguments);
  console.log(Array.from(arguments));
};
fun1(1, 2, 3, 4, 5, 6);
const obj = {
  //如果想将此类数组（对象(这个对象类似类数组)）转为数组，起始位置需从 0 开始依次往后，否则 from 转换不了
  "0": 12312,
  "1": 98768,
  length: 2,
  // 。。。。。。
};
console.log(Array.from(obj));
```

##### 数组新增方法 flat，flatMap
- flat
- 1. `flat`:将多维数组转化成一维数组可以使用,()中的参数是几就拉平几层，不写是 1，即默认值是 1。
  - [1,2,[3,4]].flat()-->[1,2,3,4]
  - [1,2,[3,4,[5,6]]].flat(2)--[1,2,3,4,5,6]
- 2. 不管有多少层，都要转换为一维数组，可以使用 `Infinity` 关键字。
  - [1,2,[3,4,[5,6]]].flat(Infinity)--[1,2,3,4,5,6]
- flatMap
- 先对数组的返回值进行 map 生成新的数组，然后对得到的数组进行一次(仅一次) flat

##### 扩展运算符 `...`

作用是对象的拷贝，还有类数组转化数组

- 拷贝
- 对象展开(对象浅拷贝)
```js
const obj = {
  name: "庄周",
  age: 18,
};
const obj1 = { ...obj };
obj1.hobby = "浪";
console.log(obj, obj1);
```
- 数组展开(数组浅拷贝)
```js
const arr = [1, 2, 3];
const arr1 = [...arr];
arr1.push(4);
console.log(arr, arr1);
```

##### 对象的扩展

对象的简洁表示法

```js
const username = "哈哈";
const userage = 20;
const obj = {
  username,
  // 当对象的属性名和作为该属性的属性值的变量名相同时(只有名字相同时才可省略属性值)
  userage,
  // 函数方法可以省略 function，随时能简写，但前提是该函数是普通函数，箭头函数不可以再简写了。(箭头函数：say()=>{})
  say() {},
};
console.log(obj);
```
对象的方法(以后补充)
1. Object.keys(对象名) 返回该对象下由属性名组成的数组
2. Object.values(对象名) 返回该对象下由属性值组成的数组

##### Symbol

第七种数据类型，生成独一无二的数据

##### set 数据结构

类似于数组，但是不能存重复的值
可以实现数组去重
```js
const ary = new Set([1, 2, 131, 312, 1, 2, 131]);
console.log(ary);
// 属性
// size 个数，长度
console.log(ary.size);
// 方法
// add()  向set数据内添加一个(只能添加一个)不重复的成员,返回数据本身
ary.add(1000);
console.log(ary);
// delete() 删除某个值，返回一个布尔值，表示删除是否成功
//  has() 查看该值是否为Set的成员，返回一个布尔值
// clear() 清除所有成员，没有返回值
// 如何将 set 数据转化成数组
console.log([...ary]);
```

Set 结构的实例有四个遍历方法，可以用于遍历成员。

- Set.prototype.keys()：返回键名的遍历器
- Set.prototype.values()：返回键值的遍历器
- Set.prototype.entries()：返回键值对的遍历器
- Set.prototype.forEach()：使用回调函数遍历每个成员

还有一个额外的 WeakSet 数据结构,内部成员只能是对象类型

##### class 类

写法

```js
class Hero {
  // 类的花括号内默认一般只写方法，而且方法之间不需要逗号
  // constructor 是 class 自带函数，该函数被称作构造器和以前的构造函数类似
  // constructor 函数当 创建实例化类的时候自动触发
  //   // 如果不需要 constructor 可以省略，如果不写 constructor ,父类中也会有 constructor ,只不过是空的(即：constructor(){})，也就是说，父类会默认添加 constructor 方法。
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
  // 除了 constructor 函数之外定义的函数都相当于原来的 prototype 内的方法
  say = () => {
    console.log("我是王者荣耀的英雄" + this.name);
  };
  // 普通函数的写法
  say(){
  console.log('我是王者荣耀的英雄' + this.name)
}
const a = new Hero("牛", 20);
const b = new Hero("小乔", 18);
console.log(a);
console.log(b);
a.say();
```

继承

```js
class CarryHero extends Hero {
  constructor(name, age) {
    super(name, age);
    // super 调用了才真正实现了继承
  }
}
const c = new CarryHero("赵云", 19);
console.log(c);
```

##### 使用 webpack 打包编译我们的项目

- webpack 功能：打包 和 编译

webpack 的功能是将 es6 这种高级语法转成浏览器认识的

你的 node 项目内使用 node 模块导入各种依赖，wbpack 可以实现将模块的导入导出编译成浏览器认识的语法，也可以将所有的导入模块操作打包。
如何使用 [参考链接](https://www.webpackjs.com/guides/)

- 项目内安装 webpack 使用 npm 下载的
  ```
    npm install webpack webpack-cli --save-dev
  ```
- 将 js 文件夹的名字改成 src，保证项目的根目录有 src ，并且 src 下存在 index.js，还有 index.js 是页面的主要用的 js
- 执行编译打包命令 `npx webpack`，会将 src 下的 index.js 打包编译到项目下的 dist 文件夹下的 main.js
- 页面导入打包好的 js
- 上面是使用了 webpack 的默认配置进行的打包，可以在项目根目录下新建 `webpack.config.js` 文件，当作 webpack 编译的配置文件。参考网址 `https://www.webpackjs.com/guides/getting-started/#%E4%BD%BF%E7%94%A8%E4%B8%80%E4%B8%AA%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6`,复制基础的配置到该文件内。
- 一直敲编译命令很繁琐，可以使用 package.json 中的 scripts 字段配置'快捷键'。使用 npm run +配置文件`webpack.config.js`的快捷名 快捷执行。

##### module

导出两种种方式

- 默认导出，只能有一次
  `export default 变量`
- 命名导出，可以有多次
  `export {变量}`

导入两种种方式

- 默认导入，只能有一次
  `import 名字:可以和导出的变量名不一样 from "路径或包名"`
- 命名导入，可以有多次
  `import {名字:不可以和导出的变量名不一样,但可以使用 as 换名} from "路径或包名"`

- 注：默认导出和默认导入对应，命名导出和命名导入对应。 默认 和 命名 可以同时存在。