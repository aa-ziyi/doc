# mpvue 的源码分析系列

mpvue -loader 基于 vue-loader 的 13.0.4 版本进行的修改，具体参考 [commit 记录](https://github.com/mpvue/mpvue-loader/commit/11e672234f26e672039c7f6257683e1ae64f6385#diff-b9cfc7f2cdf78a7f4b91a753d10865a2)

style scoped
熟悉 vue 的同学知道在其单文件组件中，支持 style scoped，使用方式如下：

模板内容：

<template>

<div class="mobike-wrap">

  <div class="mobike-wrap-banner">

  </div>

</div>

</template>

样式内容：

<style scoped>

.mobike-wrap {

  color: #f05b48;

}

</style>
