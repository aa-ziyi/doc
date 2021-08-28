# vue 响应式原理

Vue.js的响应式原理依赖于Object.defineProperty，尤大大在Vue.js文档中就已经提到过，这也是Vue.js不支持IE8 以及更低版本浏览器的原因。Vue通过设定对象属性的 setter/getter 方法来监听数据的变化，通过getter进行依赖收集，而每个setter方法就是一个观察者，在数据变更的时候通知订阅者更新视图

# 那么Vue是如何将所有data下面的所有属性变成可观察的（observable）呢？

```js
function observer(value, cb) {
    Object.keys(value).forEach((key) => defineReactive(value, key, value[key] , cb))
}

function defineReactive (obj, key, val, cb) {
    Object.defineProperty(obj, key, {
        enumerable: true,
        configurable: true,
        get: ()=>{
            /*....依赖收集等....*/
            /*Github:https://github.com/answershuto*/
        },
        set:newVal=> {
            cb();/*订阅者收到消息的回调*/
        }
    })
}

class Vue {
    constructor(options) {
        this._data = options.data;
        observer(this._data, options.render)
    }
}

let app = new Vue({
    el: '#app',
    data: {
        text: 'text',
        text2: 'text2'
    },
    render(){
        console.log("render");
    }
})
```