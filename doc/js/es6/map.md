# map是什么
JavaScript 的对象（Object），本质上是键值对的集合（Hash 结构），但是传统上只能用字符串当作键。这给它的使用带来了很大的限制。ES6 提供了 Map 数据结构。它类似于对象，也是键值对的集合，但是“键”的范围不限于字符串，各种类型的值（包括对象）都可以当作键。也就是说，Object 结构提供了“字符串—值”的对应，Map 结构提供了“值—值”的对应，是一种更完善的 Hash 结构实现。如果你需要“键值对”的数据结构，Map 比 Object 更合适。

# map用法
## 基础操作方法
```js
let map = Map();

map.set(key,value);
map.get(key);
map.has(key);
map.delete(key);

map.size  属性返回 Map 结构的成员总数。

map.clear 清楚所有成员的变量
```


## 遍历方法
```js
const map = new Map([
  ['F', 'no'],
  ['T',  'yes'],
]);


> keys()：返回键名的遍历器。
for (let key of map.keys()) {
  console.log(key);
}
// "F"
// "T"


> values()：返回键值的遍历器。
for (let value of map.values()) {
  console.log(value); // "no"  "yes"

}

> entries()：返回所有成员的遍历器。

for (let item of map.entries()) {
  console.log(item[0], item[1]); // "F" "no" , "T" "yes"
}
// 或者
for (let [key, value] of map.entries()) {
  console.log(key, value); // "F" "no" ,"T" "yes"
}
// 等同于使用map.entries()
for (let [key, value] of map) {
  console.log(key, value); // "F" "no", "T" "yes"
}


> forEach()：遍历 Map 的所有成员。

map.forEach(function(value, key, map) {
  console.log("Key: %s, Value: %s", key, value);
});
forEach方法还可以接受第二个参数，用来绑定this。当然这里使用箭头函数是更直接简单
const reporter = {
  report: function(key, value) {
    console.log("Key: %s, Value: %s", key, value);
  }
};
map.forEach(function(value, key, map) {
  this.report(key, value);
}, reporter);

```
## 传参构造
作为构造函数，Map 也可以接受一个数组作为参数。但该数组的成员必须是一个个表示键值对的数组。
```js
const map = new Map([
  ['name', '张三'],
  ['title', 'Author']
]);

map.size // 2
map.has('name') // true
map.get('name') // "张三"
map.has('title') // true
map.get('title') // "Author"
```
## 与其他类型互转
### Map 结构转为数组结构
比较快速的方法是使用扩展运算符（...）
```js
const map = new Map([
  [1, 'one'],
  [2, 'two'],
  [3, 'three'],
]);

[...map.keys()]
// [1, 2, 3]

[...map.values()]
// ['one', 'two', 'three']

[...map.entries()]
// [[1,'one'], [2, 'two'], [3, 'three']]

[...map]
// [[1,'one'], [2, 'two'], [3, 'three']]
``` 
结合数组的map方法、filter方法，可以实现 Map 的遍历和过滤（Map 本身没有map和filter方法）。

### 数组转为Map
将数组传入 Map 构造函数，就可以转为 Map。
```js
new Map([
  [true, 7],
  [{foo: 3}, ['abc']]
])
// Map {
//   true => 7,
//   Object {foo: 3} => ['abc']
// }
```
### Map 转为对象
如果所有 Map 的键都是字符串，它可以无损地转为对象。
```js
function strMapToObj(strMap) {
  let obj = Object.create(null);
  for (let [k,v] of strMap) {
    obj[k] = v;
  }
  return obj;
}

const myMap = new Map()
  .set('yes', true)
  .set('no', false);
strMapToObj(myMap)
// { yes: true, no: false }
```
如果有非字符串的键名，那么这个键名会被转成字符串，再作为对象的键名。

### 对象转为 Map
```js 
function objToStrMap(obj) {
  let strMap = new Map();
  for (let k of Object.keys(obj)) {
    strMap.set(k, obj[k]);
  }
  return strMap;
}

objToStrMap({yes: true, no: false})
// Map {"yes" => true, "no" => false}
```
### Map 转为 JSON
Map 转为 JSON 要区分两种情况。一种情况是，Map 的键名都是字符串，这时可以选择转为对象 JSON。

```js
function strMapToJson(strMap) {
  return JSON.stringify(strMapToObj(strMap));
}

let myMap = new Map().set('yes', true).set('no', false);
strMapToJson(myMap)
// '{"yes":true,"no":false}'
```
另一种情况是，Map 的键名有非字符串，这时可以选择转为数组 JSON。

```js
function mapToArrayJson(map) {
  return JSON.stringify([...map]);
}

let myMap = new Map().set(true, 7).set({foo: 3}, ['abc']);
mapToArrayJson(myMap)
// '[[true,7],[{"foo":3},["abc"]]]'
JSON 转为 Map
JSON 转为 Map，正常情况下，所有键名都是字符串。

function jsonToStrMap(jsonStr) {
  return objToStrMap(JSON.parse(jsonStr));
}

jsonToStrMap('{"yes": true, "no": false}')
// Map {'yes' => true, 'no' => false}
但是，有一种特殊情况，整个 JSON 就是一个数组，且每个数组成员本身，又是一个有两个成员的数组。这时，它可以一一对应地转为 Map。这往往是 Map 转为数组 JSON 的逆操作。

function jsonToMap(jsonStr) {
  return new Map(JSON.parse(jsonStr));
}

jsonToMap('[[true,7],[{"foo":3},["abc"]]]')
// Map {true => 7, Object {foo: 3} => ['abc']}
```

