Node.js 作为目前最热门的开发工具之一，怎样使用它开发命令行程序，是 Web 开发者应该掌握的技能。

# 原始命令行开发及获取参数
首先， 创建一个js文件

命令行创建test.js
```bash
touch test.js

sudo vim test.js

按 i  建开始输入

console.log('hello');
```

手动创建test.js
```js
console.log('hello');
```

执行test.js
```bash
node test.js
```

当我们执行`node test.js `可以直接在脚本文件后面加上参`node test.js LiLi`
在命令行参数可以用系统变量 process.argv 获取。修改test.js
```js
console.log('hello ', process.argv[2]);
//输出 hello LILi
```

# child_process
 child_process 模块新建子进程，从而执行 Unix 系统命令。


