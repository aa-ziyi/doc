# js模块化是什么
一个功能点或者某个业务的集合，模块应该有定义、依赖和输出

# js模块解决了什么问题
网页越来越像桌面程序，需要一个团队分工协作、进度管理、单元测试等等......开发者不得不使用软件工程的方法，管理网页的业务逻辑。
Javascript模块化编程，已经成为一个迫切的需求。理想情况下，开发者只需要实现核心的业务逻辑，其他都可以加载别人已经写好的模块。

# js模块实现机制
## script标签
```js
<script src="module1.js"></script>
<script src="module2.js"></script>
<script src="libraryA.js"></script>
<script src="module3.js"></script>
```
这是最原始的 JavaScript 文件加载方式，如果把每一个文件看做是一个模块，那么他们的接
口通常是暴露在全局作用域下，也就是定义在 window 对象中，不同模块的接口调用都是一
个作用域中，一些复杂的框架，会使用命名空间的概念来组织这些模块的接口，典型的例子
如 YUI 库。
这种原始的加载方式暴露了一些显而易见的弊端：

1. 全局作用域下容易造成变量冲突
2. 文件只能按照 <script> 的书写顺序进行加载
3. 开发人员必须主观解决模块和代码库的依赖关系
4. 在大型项目中各种资源难以管理，长期积累的问题导致代码库混乱不堪


## CommonJS
服务器端的 Node.js 遵循 CommonJS规范，该规范的核心思想是允许模块通过 require 方
法来同步加载所要依赖的其他模块，然后通过 exports 或 module.exports 来导出需要暴露
的接口。
```js
require(“module”);
require(“../file.js”);
exports.doStuff = function() {};
module.exports = someValue;
```

优点：
1. 服务器端模块便于重用
2. NPM 中已经有将近20万个可以使用模块包
3. 简单并容易使用
缺点：
1. 同步的模块加载方式不适合在浏览器环境中，同步意味着阻塞加载，浏览器资源是异步加载的
2. 不能非阻塞的并行加载多个模块

实现：
1. 服务器端的 Node.js
2. Browserify，浏览器端的 CommonJS 实现，可以使用 NPM 的模块，但是编译打包后的文件体积可能很大
3. modules-webmake，类似Browserify，还不如 Browserify 灵活。wreq，Browserify 的前身

## AMD
Asynchronous Module Definition 规范其实只有一个主要接口 define(id?, dependencies?,
factory) ，它要在声明模块的时候指定所有的依赖 dependencies ，并且还要当做形参传到
factory 中，对于依赖的模块提前执行，依赖前置。

```
define(“module”, [“dep1”, “dep2”], function(d1, d2) {
return someExportedValue;
});
require([“module”, “../file”], function(module, file) { / … / });
```

优点：
1. 适合在浏览器环境中异步加载模块
2. 可以并行加载多个模块

缺点：
1. 提高了开发成本，代码的阅读和书写比较困难，模块定义方式的语义不顺畅
2. 不符合通用的模块化思维方式，是一种妥协的实现
实现：
RequireJS
curl

## CMD
Common Module Definition 规范和 AMD 很相似，尽量保持简单，并与 CommonJS 和
Node.js 的 Modules 规范保持了很大的兼容性。

```
define(function(require, exports, module) {
  var $ = require('jquery');
  var Spinning = require('./spinning');
  exports.doSomething = ...
  module.exports = ...
})
```

优点：
1. 依赖就近，延迟执行
2. 可以很容易在 Node.js 中运行

缺点：
1. 依赖 SPM 打包，模块的加载逻辑偏重

实现：
1. Sea.js

## ES6 模块
EcmaScript6 标准增加了 JavaScript 语言层面的模块体系定义。ES6 模块的设计思想，是尽
量的静态化，使得编译时就能确定模块的依赖关系，以及输入和输出的变量。CommonJS 和
AMD 模块，都只能在运行时确定这些东西。

```js 
import “jquery”;
export function doStuff() {}
module “localModule” {}
```

优点：

容易进行静态分析
面向未来的 EcmaScript 标准
缺点：

原生浏览器端还没有实现该标准
全新的命令字，新版的 Node.js才支持
实现：

Babel
期望的模块系统
可以兼容多种模块风格，尽量可以利用已有的代码，不仅仅只是 JavaScript 模块化，还有
CSS、图片、字体等资源也需要模块化。

# 现有的实现js模块化的一些解决方案