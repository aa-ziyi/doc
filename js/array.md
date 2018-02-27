# 数组去重的集中解法

# 1、利用ES6中的Set,
   
  ```js
  let arry = [1,2,4,4,6]
  let set = new Set(arry);
  [...set]  //[1,2,4,6]
  ```
# 2、排序后比较前后两个是否相等；


# 3、利用object的键值对，这种方法是利用一个空的 Object 对象，我们把数组的值存成 Object 的 key 值，比如 Object[value1] = true，在判断另一个值的时候，如果 Object[value2]存在的话，就说明该值是重复的。示例代码如下
```js
let arry = [1,2,4,4,6]

let obj = {}
let new arry = arry.filter((item,index)=>{
  return obj.hasoWnProperty(item) ? false : (obj[item] = true)
})
```