# reflect 是什么

Reflect对象与Proxy对象一样，也是 ES6 为了操作对象而提供的新 API


# reflect 解决什么问题

（1） 将Object对象的一些明显属于语言内部的方法（比如Object.defineProperty），放到Reflect对象上。现阶段，某些方法同时在Object和Reflect对象上部署，未来的新方法将只部署在Reflect对象上。也就是说，从Reflect对象上可以拿到语言内部的方法。

（2） 修改某些Object方法的返回结果，让其变得更合理。比如，Object.defineProperty(obj, name, desc)在无法定义属性时，会抛出一个错误，而Reflect.defineProperty(obj, name, desc)则会返回false。
```js
// 老写法
try {
  Object.defineProperty(target, property, attributes);
  // success
} catch (e) {
  // failure
}

// 新写法
if (Reflect.defineProperty(target, property, attributes)) {
  // success
} else {
  // failure
}
```
让Object操作都变成函数行为
```js
// 老写法 命令式操作
'assign' in Object // true

// 新写法  函数式操作
Reflect.has(Object, 'assign') // true
```

# feflect 如何使用