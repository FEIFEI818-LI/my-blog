---
title: 准备工作
data: 2021-03-23
sidebar: auto
---
## 在编写express准备工作
写过node代码都知道，我们每次更改代码时都要重新启动，这会非常麻烦，所以这里推荐使用一个插件。
:::tip
npm install supervisor -g
:::
这里注意一点的就是，supervisor必须安装到全局，如果你不安装到全局，错误命令会提示你安装到全局。

启动时输入supervisor 文件入口文件的地址，需要注意的是输入的文件入口文件在当前则修改的代码如果也在当前文件，运行时会起作用，如果不在当前则不起作用。

supervisor app

即可启动应用。