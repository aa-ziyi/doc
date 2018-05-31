# set是什么
ES6 提供了新的数据结构 Set。Set 本身是一个构造函数，用来生成 Set 数据结构。

# set 特性
它类似于数组，但是成员的值都是唯一的，没有重复的值。

# set 使用
Set 函数可以接受一个数组、类数组对象（或者具有 iterable 接口的其他数据结构）作为参数，用来初始化。

```js
let set = new Set([1,2,3]);
// 1,2,3

let set2 = new Set([1,2,2]);
// 1,2   成员都是唯一没有重复值，可用于数组的去重

let set2 = new Set(document.getElementsByTagName(div))；
```
向 Set 加入值的时候，不会发生类型转换，所以5和"5"是两个不同的值。Set 内部判断两个值是否不同，使用的算法叫做“Same-value-zero equality”，它类似于精确相等运算符（===），主要的区别是NaN等于自身，而精确相等运算符认为NaN不等于自身，但在 Set 内部，两个NaN是相等。

# set实例方法
Set 结构的实例有以下属性。

* Set.prototype.constructor：构造函数，默认就是Set函数。
* Set.prototype.size：返回Set实例的成员总数。
Set 实例的方法分为两大类：操作方法（用于操作数据）和遍历方法（用于遍历成员）。下面先介绍四个操作方法。

## 操作方法（用于操作数据）
> add(value)：添加某个值，返回 Set 结构本身。
> delete(value)：删除某个值，返回一个布尔值，表示删除是否成功。
> has(value)：返回一个布尔值，表示该值是否为Set的成员。
> clear()：清除所有成员，没有返回值。

## 四个遍历方法，可以用于遍历成员。
> keys()：返回键名的遍历器
> values()：返回键值的遍历器
> entries()：返回键值对的遍历器
> forEach()：使用回调函数遍历每个成员

keys方法、values方法、entries方法返回的都是遍历器对象。由于 Set 结构没有键名，只有键值（或者说键名和键值是同一个值），所以keys方法和values方法的行为完全一致。

# Set 结构转为数组
Array.from方法可以将set结构转为数组：提供数组去重的方法
```js
const items = new Set([1, 2, 3, 4, 5]);
const array = Array.from(items);
 扩展运算符（...）内部使用for...of循环，所以也可以用于 Set 结构

let set = new Set(['red', 'green', 'blue']);
let arr = [...set];
// ['red', 'green', 'blue']
```

# set 实现并集（Union）、交集（Intersect）和差集（Difference）。
```js 
let a = new Set([1, 2, 3]);
let b = new Set([4, 3, 2]);

// 并集
let union = new Set([...a, ...b]);
// Set {1, 2, 3, 4}

// 交集
let intersect = new Set([...a].filter(x => b.has(x)));
// set {2, 3}

// 差集
let difference = new Set([...a].filter(x => !b.has(x)));
// Set {1}

```

# 改变set结构
如果想在遍历操作中，同步改变原来的 Set 结构，目前没有直接的方法，但有两种变通方法。一种是利用原 Set 结构映射出一个新的结构，然后赋值给原来的 Set 结构；另一种是利用Array.from方法。

```js
// 方法一
let set = new Set([1, 2, 3]);
set = new Set([...set].map(val => val * 2));
// set的值是2, 4, 6

// 方法二
let set = new Set([1, 2, 3]);
set = new Set(Array.from(set, val => val * 2));
// set的值是2, 4, 6
上面代码提供了两种方法，直接在遍历操作中改变原来的 Set 结构。

```