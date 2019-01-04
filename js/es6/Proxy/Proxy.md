# proxy 定义
Proxy 用于修改某些操作的默认行为，等同于在语言层面做出修改，所以属于一种“元编程”（meta programming），即对编程语言进行编程。

# proxy 能做什么，解决了什么问题
Proxy 可以理解成，在目标对象之前架设一层“拦截”，外界对该对象的访问，都必须先通过这层拦截，因此提供了一种机制，可以对外界的访问进行过滤和改写。Proxy 这个词的原意是代理，用在这里表示由它来“代理”某些操作，可以译为“代理器”。

proxy能用自己的定义覆盖了语言的原始定义。

# proxy 如何使用

ES6 原生提供 Proxy 构造函数，用来生成 Proxy 实例

```js
var proxy = new Proxy(target, handler);
```
Proxy 对象的所有用法，都是上面这种形式，不同的只是handler参数的写法。其中，new Proxy()表示生成一个Proxy实例，target参数表示所要拦截的目标对象，handler参数也是一个对象，用来定制拦截行为。

拦截读取属性行为
```js
var proxy = new Proxy({}, {
  get: function(target, property) {
    return 35;
  }
});

proxy.time // 35
proxy.name // 35
proxy.title // 35
```
如果handler没有设置任何拦截，那就等同于直接通向原对象。
```js
var target = {};
var handler = {};
var proxy = new Proxy(target, handler);
proxy.a = 'b';
target.a // "b"
```
上面代码中，handler是一个空对象，没有任何拦截效果，访问proxy就等同于访问target。


```js
var obj = new Proxy({}, {
  get: function (target, key, receiver) {
    console.log(`getting ${key}!`);
    return Reflect.get(target, key, receiver);
  },
  set: function (target, key, value, receiver) {
    console.log(`setting ${key}!`);
    return Reflect.set(target, key, value, receiver);
  }
});
```
上面代码对一个空对象架设了一层拦截，重定义了obj对象属性的读取（get）和设置（set）行为【proxy能用自己的定义覆盖了语言的原始定义】。这里暂时先不解释具体的语法，只看运行结果。对设置了拦截行为的对象obj，去读写它的属性，就会得到下面的结果。
```js
obj.count = 1
//  setting count!
++obj.count
//  getting count!
//  setting count!
//  2
```

# proxy 应用场景