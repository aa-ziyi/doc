
# react
## props
父组件传给子组件的属性，对应vue的props。
只读，对其进行修改会报错。
需要在constructor中通过super(props)继承。
注意：在子组件中引用了props内引用类型的值，再修改该引用，等于间接修改了父元素内的值，尽可能避免（vue里也有类似情况：vue内可以直接修改props内的值，虽然官方不推荐，但在表单等场景下可以作为简单的双向绑定使用以减少代码量，不知道react内有没有这种场景）

## state
组件的状态，对应vue的data。
可修改。
在constructor内声明this.state = {xxx: xxx, yyy: yyy}。
不要直接修改，而是用setState()去修改。因为直接修改不会触发视图的渲染。

## setState
修改组件的state并触发render重渲染视图。对应vue的话，应该是vue的劫持变量的set和get来自动渲染视图。但react是手动挡，vue是自动挡。对应小程序的setData()。
注意：setState是异步操作。如果需要立即基于修改后的state进行操作，应该传入一个回调：setState({}, () => {console.log(this.state)})。另外，在componentDidUpdate钩子下是可以确保拿到最新的state。
同上，如果state的新值需要基于state当前的值计算，最好是传入一个函数来保证不会出错：setState((preState) => {a: preState.a + 1})

## render
返回一个JSX对象，对应vue的templete
每次setState()会触发该组件的render函数
注意：事实上，只有setState()才能触发render。子组件props改变触发的子组件render，实质上是父组件setState触发父组件render后导致的子组件render，并非props修改自动触发的。
生命周期
```
getDefaultProps
getInitialState
componentWillMount
render
componentDidMount
componentWillReceiveProps
shouldComponentUpdate
componentWillUpdate
componentDidUpdate
componentWillUnmount
```
详细说明：http://react-china.org/t/react/1740

和​vue相比，大部分钩子相似，区别在于vue没有把render过程暴露出来

## 事件监听
和vue类似。<div onClick={this.handle}></div>
要注意，直接作为回调函数将方法传入会导致该方法丢失当前的this，需要在传入前绑定this。三种方式：constructor内bind绑定、JSX内bind绑定、传入箭头函数
传参的两种方式：

```js
1、bind：<div onClick={this.handle.bind(this, a)}></div> 
2、箭头函数：<div onClick={(a) => this.handle(a)}></div>
```
todo：研究一下lodash-decorators/bind的@bind用法

## 反向数据流
不同于vue的双向绑定概念，react提倡单项数据流，导致反向数据流的实现较vue略繁琐，但逻辑上更为清晰
反向数据流主要出现在两个场景：
1、受控组件，如input、radio等（对应vue的v-model）
将state绑定在受控组件的value上，此时用户的输入是无效的，因为视图层的value只受到state控制。然后再在组件的onChange事件中用setState更新state来渲染视图。
2、子组件修改父组件状态
父组件给子组件的props里传一个handle（注意这里要先绑定this），然后子组件通过该handle来操作父组件的state。

# redux
##流程

组件通过store.dispatch触发action，store接收到action执行reducer，reducer返回的值用于更新state。
组件内部可以通过store.getState获取state，可以通过store.subscribe监听state的修改并执行setState更新视图

## state
一个不能直接修改，只能通过触发action来修改的状态变量
初始值可以在reducer的state参数上定默认值，也可以在createStore时传入。后者会覆盖前者。
## action
一个用于描述如何修改state的对象
一般会把异步操作也放在action层来做，但需要中间件支持：redux-thunk
## reducer
一个根据传入的action来判断该对state做什么的函数，返回值会作为新的state
接收两个参数：reducer(state, aciton)
纯函数
## store
连接state、action、reducer的桥梁
通过createStore(reducer)创建
提供三个方法：getState用于获取state，dispatch用于触发action来执行reducer，subscribe用于监听state变化来更新视图

## 其他​
js函数传参是按值传递还是按引用传递？https://www.cnblogs.com/zareb/p/5699571.html


## react-redux
主要提供的功能有Provider和connect
简单来说，react-redux的作用就是将store作为组件的props传入
## Provider
Provider是react-redux提供的一个组件，通常我们将其包裹在我们应用的最外层，并将store作为provider的props，此时store会通过context传到每一个子组件，子组件可以通过this.context访问到store。
但我们一般不会直接通过context访问store，而是通过connect方法将store绑在组件的props上
## connect
一个柯里化的函数，通常我们会这样调用：connect(mapStateToProps, mapDispatchToProps)(component)
调用第一次时，返回接收一个react组件作为参数的函数；调用第二次时，返回一个react组件
同时connect还会把store.dispatch通过props传入组件，组件可以直接调用this.props.dispatch来触发action
mapStateToProps
mapStateToProps(state, ownProps)可以将store中的数据绑定在组件的props上，每次store更新，都会调用该函数来更新组件的props，从而触发组件的componentWillReceiveProps（目前不确定是否会自动触发render，待验证）
一般绑定的方式如下：(state) => { return state.myComponentData }
在绑定props时，最好做到最小够用原则，即只绑定组件需要的数据，否则无关数据的更新也会触发组件的render，影响效率
mapDispatchToProps
mapDispatchToProps(dispatch, ownProps)可以将触发action的方法绑定在组件的props上。