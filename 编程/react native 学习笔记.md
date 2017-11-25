---
date: 2017-04-02 13:13
status: public
title: 'React Native 学习笔记'
---

这个假期要看一下 RN，节后可能会用到，了解学习一下。

## 区分 Android/iOS 平台
```JavaScript
var React = require('react-native');
var {Platform} = React;
console.log(Platform);
// 在安卓上运行结果:
{ OS: 'android', Version: 23 }
// 在iOS上运行结果如下：
{ OS: 'ios' }
```

> 一种这样的技术是单一功能原则（single responsibility principle），也就是一个组件在理想情况下只做一件事情。如果它最终增长了，它就应该被分解为更小的组件。

## 压缩、解压文件
使用包：[react-native-zip-archive](https://github.com/mockingbot/react-native-zip-archive)
注意点：使用`zip`方法压缩文件时，sourcePath 对应的应该是目标目录，而不是目标文件名，否则会得到一个空压缩包。
