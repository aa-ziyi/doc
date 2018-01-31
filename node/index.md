# node版本控制

Node.js发展迅猛，版本发布频繁，比如我们在日常开发中使用的稳定版本是v0.10.26，同时又需要体验具有harmony特性的v0.11.12，那么如何安装和管理多版本Node，就需要使用下面介绍的两个Node版本管理工具——n和nvm。


# n

## 安装n
1、通过npm安装
```
$ npm install -g n
 ```

2、或者，通过源代码安装
```
$ git clone https://github.com/visionmedia/n.git
$ cd n
$ make install
```

3、如果需要安装到指定目录，需要在安装前增加PREFIX前缀
```
$ PREFIX=$HOME make install #将n安装到~/bin/n
```

## 安装指定版本的node
```
$ n 0.8.17
$ n 0.10.26
$ n 0.11.12
```

## 在命令行中输入n来选择已经安装的node版本，或者通过^C取消选择
```
$ n
  0.8.17
ο 0.10.26
  0.11.12
```

## 使用或安装稳定的官方版本
```
$ n latest
```

## 使用或安装稳定的官方版本
```
$ n stable
```

## 切换到之前的版本
```
$ n prev
``
## 删除某版本node
```
$ n rm 0.10.26 v0.11.12

//或者

$ n - 0.11.12
```

## 查看某版本node的安装路径
```
$ n bin 0.11.12
/usr/local/n/versions/0.11.12/bin/node
```

## 用指定版本的node运行some.js

```
$ n use 0.11.12 some.js
$ n use 0.11.12 --harmony some.js #带参数
```

## 查看可使用和安装的node版本
```
n ls

命令别名

which   bin
use     as
list    ls
-       rm
```
通过n安装的node存放在/usr/local/n/versions目录中。

# nvm

## 安装
1、通过脚本文件自动安装
```
$ curl https://raw.github.com/creationix/nvm/v0.4.0/install.sh | sh
或者
$ wget -qO- https://raw.github.com/creationix/nvm/v0.4.0/install.sh | sh
以上命令会将nvm仓库克隆到~/.nvm目录，并将启动脚本添加到shell配置文件中（~/.bash_profile、 ~/.zshrc 或~/.profile）
```
你还可以通过参数 NVM_SOURCE NVM_DIR NVM_PROFILE 进行自定义安装，比如curl ... | NVM_DIR=/usr/local/nvm sh

2、通过源码手动安装
```
$ git clone https://github.com/creationix/nvm.git ~/.nvm
$ cd ~/.nvm
$ source ~/.nvm/nvm.sh # 将这一行加入到shell配置文件中，根据环境不同，可能是~/.bashrc, ~/.profile, 或 ~/.zshrc
```
## 使用安装某版本的node
```
$ nvm install 0.10.26 #安装nodejs v0.10.26
$ nvm install 0.11 #安装nodejs v0.11.x最新版本
```

##删除某版本的node

$ nvm uninstall 0.10.26
$ nvm uninstall default
在shell中切换使用已经安装的指定版本

$ nvm use 0.11
你还可以在你的项目根目录中新建.nvmrc文件来存放node版本，然后在该目录运行

$ nvm use
用指定版本运行some.js

$ nvm run 0.11.12 some.js
查看已经安装的版本

$ nvm ls
查看可以安装哪些版本

$ nvm ls-remote
恢复使用系统安装的版本，撤销nvm使用的版本

$ nvm deactivate
使用别名设置默认的版本

$ nvm alias default 0.10
$ nvm use default
指定安装源

$ export NVM_NODEJS_ORG_MIRROR=http://nodejs.org/dist
$ nvm install 0.10
# 或者
$ NVM_NODEJS_ORG_MIRROR=http://nodejs.org/dist nvm install 0.10
后记
不要在使用nvm的同时，再去使用n，这将会导致node版本混乱，反之亦是如此。
根据自己的喜好和习惯，选择其一。
其他语言也都有类似的版本管理器，比如Ruby的RVM