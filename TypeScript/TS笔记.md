# TypeScript

## 什么是TS
TS是微软公司开发的一款JavaScript超集语言

JavaScript超集：当前任何合法的javascript都是合法的TS代码

TS主要为JS提供类型系统和ES6语法支持

## Ts和 flow的区别

Flow是JS代码静态类型检查工具， 而TS是一门语言！

并且TS有自己的编译工具，我们写好的TS代码最终会通过编译器编译成JS代码进行运行

## TS安装

安装TS命令行工具, 同时它也是TS编译器
```
npm i -g typescript
```

安装好之后，全局会提供一个`tsc` 命令给我们使用!


### 编写TS代码

在变量写法上和flow类似, 变量后`:类型` 能够声明变量的类型

在函数的参数后`:类型` 能够声明函数参数的类型

在函数定义形参的括号之后 `:类型`能够声明return 值的类型

```ts
let a:string = '哈哈'
function say(a: number, b: number):Object {
  return {
    a,
    b
  }
}
let p = say(1, 2)
console.log(p)
```

## TS配置文件生成及说明

创建配置文件
```
tsc --init  //会在当前文件生成配置文件
```
`target: ES5` 将TS代码转换哪个版本的JS代码, ES5/ES3 

`module: commonjs`: 是将TS代码转换JS使用的模块标准

`outFile: ./`: 指定输出名字

`outDir: ./dist` : 指定TS代码转换为JS代码的输出路径

`rootDir: ./src`: 将哪个文件夹下的TS文件转换为JS代码

注意当我们指定输出路径和源文件路径时, 直接执行下面命令就会在`dist/index.js` 对应路径下生成对应的文件
```
tsc -p ./tsconfig.json
```

`strict: true` : 指定生成的js是否为严格模式

`esModuleInterop: true` : 当我们在引入第三方包时, 文件中没有导出项, 它默认会找一些导出项, 不常用

## TS的数据类型

### number 类型
```ts
// number 类型
let num1: number = 1
let num2: number = 2
let num3!: number = 3  // num3 是数字类型并且非空 
```

### string类型
```ts
// 字符串类型
let str: string = '哈哈'
let str2: string = `支持es6中的模板字符串${1}`
```

### 布尔类型
```ts
// 布尔类型
let flag1: boolean = true
let flag2: boolean = false
```

### 数组类型
```ts
// 只能存放数字类型的数组
let arr1: Array<number> = [1, 2]
let arr2: number[] = [4, 4]
// 任意类型
let arr4: any[] = [1, 'a', {a: 'a'}]
```

### 元组
```ts
let arr3: [number, string, string] = [1, '1', 'h']
// arr3[1] = 1 报错
arr3[1] = '哈哈'
arr3[2] = '嘻嘻'
```

### 空值 void
在某种程度上, `void` 和 `any` 类型相反, 它表示没有任何类型

当一个函数没有返回值时, 通常会见到其返回值类型是 `void`
```ts
function warnUser(): void {
    alert('这是一个没有返回值的函数')
}
```
声明一个`void` 的变量没有什么用处, 因为赋予它的是`null` 和 `undefined`
```ts
// 现在void的变量不能是 null 只能是 undefined 和 flow一样
let unable: void = undefined
```
### null和undefined
在TS中`null` 和 `undefined` 是两种类型,和 `void`相似, 他们本身的类型用处意义不大
```ts
// null 和 undefined
let res1: null = null
let res2: undefined = undefined
```

### 任意值 any
`any` 表示可以是任意类型
```ts
// 任意类型
let some: any = []
let some1: any = 10
let some2: any = {} 
```

### Never 类型
`never` 类型表示那些永不存在的值的类型. 例如, `never` 类型时那些总是会抛出异常或根本就不会有返回值的函数表达式或箭头函数表达式的返回值类型. 

变量也可能是`never` 类型, 当他们被永不为真的类型保护所约束时.

`never` 类型时任何类型的子类型, 也可以赋值给任何类型. 然而, 没有类型是 `never` 的子类型或可以赋值给 `never` 类型 (除了 `never` 本身之外). 即使 `any` 也不可以赋值给 `never`

下面是一些返回 `never` 类型的函数
```ts
// 可见, never 类型可以给任何类型赋值
let neverFnc: Object = (): never => {
  throw new Error('出错误了')
} 

// 推断的返回值为never类型
function fail() {
  return Error('some error')
}

// 返回 never 的函数必须存在无法达到的终点
function infiniteLoop(): never {
  while(true) {}
}
```

**一般来说, never 用在没有返回值的函数 或者 永远不可能有返回值的函数做类型确定的时候, 用never类型**

**没有返回值和返回值为null和undefined是两个概念**


### object类型
```ts
// object 类型
let o1: object = {}
let o2: {name: string, age: number} = {name: 'zs', age: 14}
```

### 枚举类型 enum

`enum` 类型时对javascript 标准数据类型的一个补充. 像C# 等其他语言一样, 使用枚举类型可以为一组数值赋予友好的名字

```ts
// 枚举类型 enum
enum Color {
  red,
  green,
  lime
}
let c: Color = Color.red
```

默认情况下, 从 `0` 开始为元素编号, 第一个是 0 第二个是 1 依次编号. 我们可以手动的指定成员的数值. 例如, 我们将上面的例子改成从 `1` 开始编号
```ts
enum Color {
  red = 1, // 编号从 1 开始
  green,
  lime
}
let c: Color = Color.red
```

或者全部手动编号

`Gender` 可以理解为我们定义的数据类型, 并且可以使用它提供的值代指一些值
```ts
enum Gender {
  male = 1,
  female = 0,
  unKnow = -1
}
let c: Gender = Gender.male // 等同于下面
let d: Gender = 1 

// 在object中也可以使用枚举类型
let obj: object = {
  gender: Gender.male
}
```


### 类型断言

有时候我们会遇到这样的情况, 我们比TypeScript更了解某个值的详细情况, 比如, 它的类型

通过类型断言这种方式可以告诉编译器, "相信我, 我知道我在干什么". 

它只在编译时器作用, 对运行时没有影响

类型断言有两种方式. 其中一种是"尖括号" 语法:

```ts
let str5: any = 'hello'
// 可以加类型断言
let leng: number = (<string>str5).length 
```

另一种 `as` 语法:
```ts
// as 语法
let str6: any = 'world'
let leng2: number = (str6 as string).length 
```

**两种写法时等价的, 但是, 在TS中使用 JSX时, 只有 `as` 语法是被允许的**



## TS中类

与ES6 中不同的是属性必须声明, 需要指定类型, 声明好属性之后, 属性必须赋值一个默认值或者在构造函数(constructor)中进行初始化

```ts
// ts中的类
class TsClass {
  // 必须声明类的属性
  name: string
  age: number
  gender: number = 1  //如果没在构造函数中初始化, 就必须给默认值
  // ----------------------------
  constructor (name: string, age:number) {
    this.name = name
    this.age = age
  }
  
    sayHi (message: string): void {
    console.log(message);
  }
}
```

ES6 中的 类
```js
class Es6Class {
  constructor (name, age) {
    this.name = name
    this.age = age
  }
}
```


### TS中的类继承

TS中类的继承和ES6中的继承基本一致, 唯一注意的地方是, TS中属性需要声明

继承的子类需要调用`super()` 之后, 才能使用this 初始化属性
```ts
class Animal {
  name: string
  age: number

  constructor (name: string, age: number) {
    this.name = name
    this.age = age
  }

  eat () {
    console.log('喜欢吃大骨头')
  }
}

class Dog extends Animal {
  color: string
  gender: number = 1
  constructor (name: string, age: number, color: string,) {
    super(name, age)
    this.color = color
  }
}

const dog1 = new Dog('哈士奇', 2, '灰色')
dog1.eat()
```


### TS中类成员的访问修饰符

访问修饰符: 指的是可以在类的成员前可以添加关键字设置成员的访问权限

- `public` : 公开的, 默认  所有人都可以访问
- `private` : 私有的, 只能在当前类中访问
- `protected` : 受保护的, 只能在当前类或者子类中访问
 
```ts
enum Color {
  red,
  green
}
class Car {
  // 公共的成员
  public color: Color
  constructor () {
    this.color = Color.red
    this.run()
  }

  // 当前成员只能在当前类中访问, new 的实例对象不能访问 
  private run () {
    console.log('这个车可以跑')
  }

  // 只能在当前类和子类中访问, 实例对象不能
  protected loadPerson () {
    console.log('这个车可以载人')
  }

  // 子类, 当前类, 子类都能访问, 默认是 public
  biaoChe () {
    console.log('我能飙车')
  }
}

class BaoMa extends Car {
  liaoMei () {
    // protected 在子类中可以访问
    this.loadPerson()
  }
}
const baoma520 = new BaoMa()
baoma520.biaoChe() // 没有修饰符, 默认是public 都能访问
```

### readonly 修饰符

**只读属性和参数属性**

只读属性 : 对于类中的一个属性, 我们可以在前加上 `readonly` 修饰符, 那么我们就必须在在声明的时候就赋值 或者在 构造函数(constructor) 中赋值

参数属性 : 在构造函数的参数前面加上修饰符, 就相当于声明属性了

```ts
class Cat {
  // readonly name: string = '皮皮猫'
  readonly name:string
  constructor (public color: string) {
    // 在构造函数中也可以赋值
    this.name = '皮皮猫' 

    // 构造函数参数前加修饰符, 就相当于声明属性了
    this.color = color 
  }
}
```


### 类成员存取器

类成员存取器和Object.defineProperty() 劫持属性类似

```ts
class Person {
  // 不使用类成员存取器
  name: string = ''

  // 使用类成员存取器
  private _age: number = 0
  // get 是在读取的时候调用
  get age() {
    return this._age
  }
  // 在设置属性时调用
  set age(val: number) {
    // 在这个就可以进行类型校验, 判断, 书写逻辑等
    if (val < 0 || val > 100) {
      throw new Error('年龄不合法')
    }
    this._age = val
  }
}

const p1 = new Person()
p1.name = '张三'
p1.age = 18
```


## TS中的接口

### 接口初探
TypeScript 的核心原则之一是对值所具有的结构进行类型检查. 它又是被称作 "鸭式变形法" 或 "结构性子类型化". 在TypeScript中, 接口的作用就是为这些类型命名和为你的代码或第三方代码定义契约

简单来说, 接口可以理解为规范, 一个约定

接口使用 `interface` 声明

接口的作用: 限制用户传的参数类型和必须传的参数项

接口的基本使用:
```ts
// 定义个函数参数的接口: 约定参数的类型和必传参数
interface ajaxOptions {
  url: string,
  type: string,
  data: object,
  success(response: object): void
}

function ajax(options: ajaxOptions) {}

ajax({
  type: 'get',
  url: 'http://www.baicu.com',
  data: {},
  success (res) {
    console.log(res)
  }
})
```

### 可选属性

接口中的属性不全都是必须的. 有的可传可不传, 不传有默认值

在写法上, 只需在接口属性后加上 `?` 即可

```ts
interface axiosOptions {
  url: string,
  // 属性后加问号即可
  type?: string,
  data?: object,
  success(res: object): void
}

function axios(options: axiosOptions) {}
```

### 只读属性

一些对象属性只允许在对象刚刚创建是指定其值, 不允许后期修改, 可以用 `readonly` 指定只读属性

```ts
interface Point {
  readonly left: number,
  readonly top: number
}

let point1: Point = { left: 10, top : 20 }
// point1.left = 20 // error 不允许修改
```


### 额外属性

有时候我们接口规定传的属性, 在实际声明对象时, 会多传参数, 即使我们不使用这个参数, 那么我们就可以在接口定义中, 规定额外属性类型

```ts
interface Point {
  readonly left: number,
  readonly top: number,

  // propName 不是固定, 可以随便起名字,代表可以使用额外属性
  [propName: string]: any 
}

let point1: Point = { 
            left: 10, 
            top : 20, 
            // 下面两个则为额外属性
            right: 50, 
            bottom: 22
            }
```


### 函数类型的接口

```ts
// 定义函数类型的接口
interface sumInterface {
  (x: number, y: number): any
}

let getSum: sumInterface = function (x: number, y: number) {
  return x + y
}
```

### 类(class)类型的接口

与 C# 和 java中的接口一样, TS也能够用它来明确的强制一个类去符合某种契约

简单来说, 就是约定某个类必须有某些属性和方法

```ts
interface PersonInterface {
  name: string,
  age: number,
  eat(): void 
}

// 我们强制要求, 这个类有 name age eat 属性和方法, 对类进行一些约束
class XiaoMin implements PersonInterface {
  name: string = '小明'
  age: number = 19
  eat () {}
  
  // 可以有其他属性或方法
  gender: string = '男'
}

// 意义在于我们可以放心使用某些属性和方法
const XM = new XiaoMin()
XM.name
XM.age
XM.eat()
```


### 接口的继承


