# Redux 学习笔记

*绝大部分摘录自 Redux 中文文档*

Redux 是 JavaScript 状态容器，提供可预测化的状态管理。

应⽤中所有的 state 都以⼀个对象树的形式储存在⼀个单⼀的 store 中。 惟⼀改变 state 的办法是触发 action，⼀个描述发⽣什么的对象。 为了描述 action 如何改变 state 树，你需要编写 reducers。

随着 JavaScript 单⻚应⽤开发⽇趋复杂，JavaScript 需要管理⽐任何时候都 要多的 state （状态）。 这些 state 可能包括服务器响应、缓存数据、本地 ⽣成尚未持久化到服务器的数据，也包括 UI 状态，如激活的路由，被选中的 标签，是否显示加载动效或者分⻚器等等。

这⾥的复杂性很⼤程度上来⾃于：我们总是将两个难以理清的概念混淆在⼀ 起：变化和异步。 我称它们为曼妥思和可乐。如果把⼆者分开，能做的很 好，但混到⼀起，就变得⼀团糟。

Redux 试图让 state 的变化变得可预测。

## 核心思想

* 强制使⽤ action 来描述所有变化
* action 就像是描述 发⽣了什么的⾯包屑
* 为了把 action 和 state 串起来，开发⼀些函 数，这就是 reducer
* reducer 只是⼀个接收 state 和 action，并返回新的 state 的函数

## 三大原则

* 单一数据源
* State 是只读的
* 使⽤纯函数来执⾏修改

## 先前技术

Redux 的灵感来源于 Flux 的⼏个重要特性。和 Flux ⼀样，**Redux 规定，将 模型的更新逻辑全部集中于⼀个特定的层（Flux ⾥的 store，Redux ⾥的 reducer）**。Flux 和 Redux 都不允许程序直接修改数据，⽽是⽤⼀个叫作 “action” 的普通对象来对更改进⾏描述。

Redux 设想你永远不会变动你的数据

Redux 并不在意你如何存储 state，state 可以是普通对象，不可变对象，或 者其它类型。

## 具体编写

在 Redux 应⽤中，所有的 state 都被保存在⼀个单⼀对象中。

store 能维持应⽤的 state，并在当你发起 action 的时候调⽤ reducer。

