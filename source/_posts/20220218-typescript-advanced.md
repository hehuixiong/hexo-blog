---
title: TypeScript进阶之路
date: 2022-02-18 14:00:00
cover: https://s-gz-2804-blog-image.oss.dogecdn.com/20220223175131.png
top_img: https://s-gz-2804-blog-image.oss.dogecdn.com/20220223175131.png
categories:
  - TypeScript
tags:
  - typeScript
---

# 前言

随着项目越来越大,市面上所使用的五花八门插件库也越来越多,随便一个项目都少说会1w+行代码以上,导致项目维护越来越差。尤其上在开发原生**JavaScript**的时候从中找**Bug**更是难如登天。**TypeScript**犹如**the Saviour**让更多开发者得心应手,也是现在开发大型工程化项目必不可缺少的一部分语言了...

# 一、TypeScript 是什么?

**TypeScript** 是一种由微软开发的自由和开源的编程语言。它是 JavaScript 的一个超集，而且本质上向这个语言添加了可选的静态类型和基于类的面向对象编程。
TypeScript 提供最新的和不断发展的 JavaScript 特性，包括那些来自 2015 年的 ECMAScript 和未来的提案中的特性，比如异步功能和 Decorators，以帮助建立健壮的组件。下图显示了 TypeScript 与 ES5、ES2015 和 ES2016 之间的关系：
<img src="https://s-gz-2804-blog-image.oss.dogecdn.com/20220223170549.png" style="width: 400px;margin-top: 40px;" />

#### 1.1 TypeScript 与 JavaScript 的区别

|-|TypeScript|JavaScript|
| :----- | :----- | :----- |
|1|JavaScript 的超集用于解决大型项目的代码复杂性|一种脚本语言，用于创建动态网页|
|2|可以在编译期间发现并纠正错误|作为一种解释型语言，只能在运行时发现错误|
|3|强类型，支持静态和动态类型|弱类型，没有静态类型选项|
|4|最终被编译成 JavaScript 代码，使浏览器可以理解|可以直接在浏览器中使用|
|5|支持模块、泛型和接口|不支持模块，泛型或接口|
|6|社区的支持仍在增长，而且还不是很大|大量的社区支持以及大量文档和解决问题的支持|

#### 1.2 获取 TypeScript

> 命令行的 TypeScript 编译器可以使用 npm 包管理器来安装。

#### #1.安装 TypeScript
```shell
$ npm install -g typescript
```

#### #2.验证 TypeScript

```shell
$ tsc -v 
# Version 4.0.2
```

#### #3.编译 TypeScript 文件

```shell
$ tsc helloworld.ts
# helloworld.ts => helloworld.js
```

当然，对刚入门 **TypeScript** 的小伙伴来说，也可以不用安装 **typescript**，而是直接使用线上的 **TypeScript Playground**来学习新的语法或新特性。通过配置 **TS Config** 的 **Target**，可以设置不同的编译目标，从而编译生成不同的目标代码。
下图示例中所设置的编译目标是**ES5**：

![](https://s-gz-2804-blog-image.oss.dogecdn.com/20220223171955.png)

#### 1.3 典型 TypeScript 工作流程
![](https://s-gz-2804-blog-image.oss.dogecdn.com/20220223174847.png)

如你所见，在上图中包含 3 个 **ts** 文件：**a.ts、b.ts** 和 **c.ts**。这些文件将被TypeScript编译器，根据配置的编译选项编译成 3 个 **js** 文件，即 **a.js、b.js 和 c.js**。对于大多数使用 **TypeScript** 开发的 **Web** 项目，我们还会对编译生成的 **js** 文件进行打包处理，然后在进行部署。

#### 1.4 TypeScript 初体验
新建一个 **hello.ts** 文件，并输入以下内容：

```typescript
function greet(person: string) {
  return 'Hello, ' + person;
}
 
console.log(greet("TypeScript"));
```
观察以上编译后的输出结果，我们发现 **person** 参数的类型信息在编译后被擦除了。**TypeScript** 只会在编译阶段对类型进行静态检查，如果发现有错误，编译时就会报错。而在运行时，编译生成的 **JS** 与普通的 **JavaScript** 文件一样，并不会进行类型检查。

# 二、TypeScript 基础类型

#### #2.1 Boolean 类型

```typescript
let isDone: boolean = false;
// ES5：var isDone = false;
```

#### #2.2 Number 类型
```typescript
let count: number = 10;
// ES5：var count = 10;
```
#### #2.3 String 类型
```typescript
let name: string = "semliker";
// ES5：var name = 'semlinker';
```
#### #2.4 Symbol 类型
```typescript
const sym = Symbol();
let obj = {
  [sym]: "semlinker",
};
console.log(obj[sym]); // semlinker 
```
#### #2.5 Array 类型
```typescript
let list: number[] = [1, 2, 3];
// ES5：var list = [1,2,3];
 
let list: Array<number> = [1, 2, 3]; // Array<number>泛型语法
// ES5：var list = [1,2,3];
```
#### #2.6 Enum 类型
使用枚举我们可以定义一些带名字的常量。 使用枚举可以清晰地表达意图或创建一组有区别的用例。 **TypeScript** 支持数字的和基于字符串的枚举。

> 1.数字枚举

```rust
enum Direction {
  NORTH,
  SOUTH,
  EAST,
  WEST,
}
 
let dir: Direction = Direction.NORTH;
```

> 2.字符串枚举
> 在 **TypeScript 2.4** 版本，允许我们使用字符串枚举。在一个字符串枚举里，每个成员都必须用字符串字面量，或另外一个字符串枚举成员进行初始化。

```nginx
enum Direction {
  NORTH = "NORTH",
  SOUTH = "SOUTH",
  EAST = "EAST",
  WEST = "WEST",
}
```
以上代码对应的**ES5**代码如下：

```javascript
"use strict";
var Direction;
(function (Direction) {
    Direction["NORTH"] = "NORTH";
    Direction["SOUTH"] = "SOUTH";
    Direction["EAST"] = "EAST";
    Direction["WEST"] = "WEST";
})(Direction || (Direction = {}));
```

通过观察数字枚举和字符串枚举的编译结果，我们可以知道数字枚举除了支持 从成员名称到成员值 的普通映射之外，它还支持 从成员值到成员名称 的反向映射：

```rust
enum Direction {
  NORTH,
  SOUTH,
  EAST,
  WEST,
}
 
let dirName = Direction[0]; // NORTH
let dirVal = Direction["NORTH"]; // 0

```

另外，对于纯字符串枚举，我们不能省略任何初始化程序。而数字枚举如果没有显式设置值时，则会使用默认规则进行初始化。

> 3.常量枚举
> 除了数字枚举和字符串枚举之外，还有一种特殊的枚举 —— 常量枚举。它是使用 const 关键字修饰的枚举，常量枚
举会使用内联语法，不会为枚举类型编译生成任何JavaScript。为了更好地理解这句话，我们来看一个具体的例子：

```rust
const enum Direction {
  NORTH,
  SOUTH,
  EAST,
  WEST,
}
 
let dir: Direction = Direction.NORTH;
```

以上代码对应的**ES5**代码如下：

```javascript
"use strict";
var dir = 0 /* NORTH */;
```

> 4.异构枚举
> 异构枚举的成员值是数字和字符串的混合：

```rust
enum Enum {
  A,
  B,
  C = "C",
  D = "D",
  E = 8,
  F,
}
```

以上代码对于的 ES5 代码如下：

```javascript
"use strict";
var Enum;
(function (Enum) {
    Enum[Enum["A"] = 0] = "A";
    Enum[Enum["B"] = 1] = "B";
    Enum["C"] = "C";
    Enum["D"] = "D";
    Enum[Enum["E"] = 8] = "E";
    Enum[Enum["F"] = 9] = "F";
})(Enum || (Enum = {}));
```

通过观察上述生成的 ES5 代码，我们可以发现数字枚举相对字符串枚举多了 “反向映射”：

```less
console.log(Enum.A) //输出：0
console.log(Enum[0]) // 输出：A
```

#### #2.7 Any 类型
在**TypeScript**中，任何类型都可以被归为**any**类型。这让**any**类型成为了类型系统的顶级类型（也被称作全局超级类型）。

```nginx
let notSure: any = 666;
notSure = "semlinker";
notSure = false;
```

**any**类型本质上是类型系统的一个逃逸舱。作为开发者，这给了我们很大的自由：**TypeScript** 允许我们对**any**类型的值执行任何操作，而无需事先执行任何形式的检查。比如：

```csharp
let value: any;
 
value.foo.bar; // OK
value.trim(); // OK
value(); // OK
new value(); // OK
value[0][1]; // OK
```
在许多场景下，这太宽松了。使用 any 类型，可以很容易地编写类型正确但在运行时有问题的代码。如果我们使用 any 类型，就无法使用 TypeScript 提供的大量的保护机制。为了解决 any 带来的问题，TypeScript 3.0 引入了 unknown`类型。

#### #2.8 Unknown 类型
就像所有类型都可以赋值给 **any**，所有类型也都可以赋值给 unknown。这使得 unknown 成为 TypeScript 类型系统的另一种顶级类型（另一种是 any）。下面我们来看一下 unknown 类型的使用示例：

```csharp
let value: unknown;
 
value = true; // OK
value = 42; // OK
value = "Hello World"; // OK
value = []; // OK
value = {}; // OK
value = Math.random; // OK
value = null; // OK
value = undefined; // OK
value = new TypeError(); // OK
value = Symbol("type"); // OK

```

对 **value** 变量的所有赋值都被认为是类型正确的。但是，当我们尝试将类型为 **unknown** 的值赋值给其他类型的变量时会发生什么？

```csharp
let value: unknown;
 
let value1: unknown = value; // OK
let value2: any = value; // OK
let value3: boolean = value; // Error
let value4: number = value; // Error
let value5: string = value; // Error
let value6: object = value; // Error
let value7: any[] = value; // Error
let value8: Function = value; // Error
```

**unknown**类型只能被赋值给 any 类型和 unknown 类型本身。直观地说，这是有道理的：只有能够保存任意类型值的容器才能保存 unknown 类型的值。毕竟我们不知道变量 value 中存储了什么类型的值。
现在让我们看看当我们尝试对类型为**unknown**的值执行操作时会发生什么。以下是我们在之前**any**章节看过的相同操作：

```csharp
let value: unknown;
 
value.foo.bar; // Error
value.trim(); // Error
value(); // Error
new value(); // Error
value[0][1]; // Error
```
将 value变量类型设置为unknown后，这些操作都不再被认为是类型正确的。通过将 any 类型改变为unknown类型，我们已将允许所有更改的默认设置，更改为禁止任何更改。

#### #2.9 Tuple 类型
众所周知，数组一般由同种类型的值组成，但有时我们需要在单个变量中存储不同类型的值，这时候我们就可以使用元组。在 JavaScript 中是没有元组的，元组是 TypeScript 中特有的类型，其工作方式类似于数组。
元组可用于定义具有有限数量的未命名属性的类型。每个属性都有一个关联的类型。使用元组时，必须提供每个属性的值。为了更直观地理解元组的概念，我们来看一个具体的例子：

```typescript
let tupleType: [string, boolean];
tupleType = ["semlinker", true];
```
在上面代码中，我们定义了一个名为tupleType的变量，它的类型是一个类型数组 [string, boolean]，然后我们按照正确的类型依次初始化tupleType变量。与数组一样，我们可以通过下标来访问元组中的元素：

```scss
console.log(tupleType[0]); // semlinker
console.log(tupleType[1]); // true
```
在元组初始化的时候，如果出现类型不匹配的话，比如：

```ini
tupleType = [true, "semlinker"];
```

此时，TypeScript 编译器会提示以下错误信息：

```csharp
[0]: Type 'true' is not assignable to type 'string'.
[1]: Type 'string' is not assignable to type 'boolean'.
```

很明显是因为类型不匹配导致的。在元组初始化的时候，我们还必须提供每个属性的值，不然也会出现错误，比如：

```ini
tupleType = ["semlinker"];
```

此时，TypeScript编译器会提示以下错误信息：

```go
Property '1' is missing in type '[string]' but required in type '[string, boolean]'.
```

#### #2.10 Void 类型
某种程度上来说，**void** 类型像是与 any 类型相反，它表示没有任何类型。当一个函数没有返回值时，你通常会见到其返回值类型是 **void**：

```javascript
// 声明函数返回值为void
function warnUser(): void {
  console.log("This is my warning message");
}
```

以上代码编译生成的 ES5 代码如下：
```javascript
"use strict";
function warnUser() {
  console.log("This is my warning message");
}
```

需要注意的是，声明一个void类型的变量没有什么作用，因为在严格模式下，它的值只能为**undefined**：
```typescript
let unusable: void = undefined;
```
#### #2.11 Null 和 Undefined 类型
ypeScript 里，undefined 和 null 两者有各自的类型分别为 undefined 和 null。

```yaml
let u: undefined = undefined;
let n: null = null;
```

#### #2.12 object, Object 和 {} 类型

> 1.object 类型
> object类型是：TypeScript2.2 引入的新类型，它用于表示非原始类型。

```typescript
// node_modules/typescript/lib/lib.es5.d.ts
interface ObjectConstructor {
  create(o: object | null): any;
  // ...
}
 
const proto = {};
 
Object.create(proto);     // OK
Object.create(null);      // OK
Object.create(undefined); // Error
Object.create(1337);      // Error
Object.create(true);      // Error
Object.create("oops");    // Error
```

> 2.Object 类型
> Object 类型：它是所有 Object 类的实例的类型，它由以下两个接口来定义：

**Object** 接口定义了 Object.prototype 原型对象上的属性；
```php
// node_modules/typescript/lib/lib.es5.d.ts
interface Object {
  constructor: Function;
  toString(): string;
  toLocaleString(): string;
  valueOf(): Object;
  hasOwnProperty(v: PropertyKey): boolean;
  isPrototypeOf(v: Object): boolean;
  propertyIsEnumerable(v: PropertyKey): boolean;
}
```

ObjectConstructor 接口定义了 Object 类的属性。

```typescript
// node_modules/typescript/lib/lib.es5.d.ts
interface ObjectConstructor {
  /** Invocation via `new` */
  new(value?: any): Object;
  /** Invocation via function calls */
  (value?: any): any;
  readonly prototype: Object;
  getPrototypeOf(o: any): any;
  // ···
}
 
declare var Object: ObjectConstructor;
```

Object 类的所有实例都继承了 Object 接口中的所有属性。

> 3.{} 类型
> {} 类型描述了一个没有成员的对象。当你试图访问这样一个对象的任意属性时，TypeScript 会产生一个编译时错误。

```go
// Type {}
const obj = {};
 
// Error: Property 'prop' does not exist on type '{}'.
obj.prop = "semlinker";
```
但是，你仍然可以使用在 Object 类型上定义的所有属性和方法，这些属性和方法可通过 JavaScript 的原型链隐式地使用：

```go
// Type {}
const obj = {};
 
// "[object Object]"
obj.toString();
```

#### #2.13 Never 类型
never 类型表示的是那些永不存在的值的类型。 例如，never 类型是那些总是会抛出异常或根本就不会有返回值的函数表达式或箭头函数表达式的返回值类型。

```php
// 返回never的函数必须存在无法达到的终点
function error(message: string): never {
  throw new Error(message);
}
 
function infiniteLoop(): never {
  while (true) {}
}
```
在 TypeScript 中，可以利用 never 类型的特性来实现全面性检查，具体示例如下：

```typescript
type Foo = string | number;
 
function controlFlowAnalysisWithNever(foo: Foo) {
  if (typeof foo === "string") {
    // 这里 foo 被收窄为 string 类型
  } else if (typeof foo === "number") {
    // 这里 foo 被收窄为 number 类型
  } else {
    // foo 在这里是 never
    const check: never = foo;
  }
}
```
注意在 else 分支里面，我们把收窄为 never 的 foo 赋值给一个显示声明的 never 变量。如果一切逻辑正确，那么这里应该能够编译通过。但是假如后来有一天你的同事修改了 Foo 的类型：

```typescript
type Foo = string | number | boolean;
```

然而他忘记同时修改**controlFlowAnalysisWithNever**方法中的控制流程，这时候**else**分支的**foo**类型会被收窄为**boolean**类型，导致无法赋值给 **never**类型，这时就会产生一个编译错误。通过这个方式，我们可以确保**controlFlowAnalysisWithNever** 方法总是穷尽了 **Foo** 的所有可能类型。 通过这个示例，我们可以得出一个结论：使用never避免出现新增了联合类型没有对应的实现，目的就是写出类型绝对安全的代码。