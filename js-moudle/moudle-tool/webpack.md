# webpack原理

# webpack核心概念

## entry 
: 一般来讲单页只有一个入口文件，多页有多个入口文件；
entry 一个可执行模块或库的入口文件。

## chunk
chunk 多个文件组成的一个代码块，例如把一个可执行模块和它所有依赖的模块组合和一个 chunk 这体现了webpack的打包机制。

## loader 
loader 文件转换器，例如把es6转换为es5，scss转换为css。

## plugin
plugin 插件，用于扩展webpack的功能，在webpack构建生命周期的节点上加入扩展hook为webpack加入功能。


## webpack构建流程
从启动webpack构建到输出结果经历了一系列过程：
1. 解析webpack配置参数，合并从shell传入和webpack.config.js文件里配置的参数，生产最后的配置结果。
2. 注册所有配置的插件，好让插件监听webpack构建生命周期的事件节点，以做出对应的反应。
3. 从配置的entry入口文件开始解析文件构建AST语法树，找出每个文件所依赖的文件，递归下去。
4. 在解析文件递归的过程中根据文件类型和loader配置找出合适的loader用来对文件进行转换。
5. 递归完后得到每个文件的最终结果，根据entry配置生成代码块chunk。输出所有chunk到文件系统。
6. 需要注意的是，在构建生命周期中有一系列插件在合适的时机做了合适的事情，比如UglifyJsPlugin会在loader转换递归完后对结果再使用UglifyJs压缩覆盖之前的结果。


webpack其实很简单，可以用一句话涵盖它的本质：
```
webpack是一个打包模块化js的工具，可以通过loader转换文件，通过plugin扩展功能。
```
如果webpack让你感到复杂，一定是各种loader和plugin的原因。


# 什么是webpack 

# webpack的诞生解决了什么问题


# 如何使用webpack