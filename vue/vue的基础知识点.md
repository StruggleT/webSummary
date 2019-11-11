# Vue.js

## 什么是vue?

Vue.js 是一套构建用户界面的框架，``只关注视图层``，它不仅易于上手，还便于与第三方库或既有项目整合。（Vue有配套的第三方类库，可以整合起来做大型项目的开发）

## 框架和库的区别？

- 框架：是一套完整的解决方案；对项目的侵入性较大，项目如果需要更换框架，则需要重新架构整个项目。

  - node中的express

- 库：提供某一个小功能，对项目的侵入性较小，如果某个库无法完成某些需求，可以很容易切换到其它库实现需求。

  - 从Jquery 切换到 Zepto

  - 从 EJS 切换到 art-template

## MVVM是什么？

MVVM 是 Model-View-ViewModel 的缩写。mvvm 是一种设计思想。Model 层代表数据模型，也可以在 Model 中定义数据修改和操作的业务逻辑；View 代表 UI 组件，它负责将数据模型转化成 UI 展现出来，ViewModel 是一个同步 View 和 Model 的对象。

在 MVVM 架构下，View 和 Model 之间并没有直接的联系，而是通过 ViewModel 进行交互，Model 和 ViewModel 之间的交互是双向的， 因此 View 数据的变化会同步到 Model 中，而 Model 数据的变化也会立即反应到 View 上。

ViewModel 通过双向数据绑定把 View 层和 Model 层连接了起来，而 View 和 Model 之间的同步工作完全是自动的，无需人为干涉，因此开发者只需关注业务逻辑，不需要手动操作 DOM, 不需要关注数据状态的同步问题，复杂的数据状态维护完全由 MVVM 来统一管理。

## MVC和MVVM之间的区别？

mvc 和 mvvm 其实区别并不大。都是一种设计思想。主要就是 mvc 中 Controller 演变成 mvvm 中的 viewModel。mvvm 主要解决了 mvc 中大量的 DOM 操作使页面渲染性能降低，加载速度变慢，影响用户体验。和当 Model 频繁发生变化，开发者需要主动更新到 View 。

参考：[MVC和MVVM的区别]{https://www.kancloud.cn/lixianshengdezhanghao/interview/904696}

## Vue中常见的指令

- v-cloak：使用 v-cloak 能够解决 插值表达式闪烁的问题 

- v-text： v-text会覆盖元素中原本的内容，但是插值表达式只会替换自己的这个占位符，不会把 整个元素的内容清空 

- v-html：里面的内容可以是html代码，并且会解析执行 

- v-bind（缩写是:）：用于绑定属性的指令，只能实现数据的单向绑定，从 M 自动绑定到 V， 无法实现数据的双向绑定 

- v-on（缩写是@）：事件绑定机制   

- v-model： 可以实现 表单元素和 Model 中数据的双向数据绑定  
- v-for： vue中提供的循环

- v-if ：每次都会重新删除或创建元素 

- v-show：每次不会重新进行DOM的删除和创建操作，只是切换了元素的 display:none 样式

## v-if和v-show的区别？

- v-if每次都会重新删除或创建元素，所以有较高的切换性能消耗，如果元素涉及到频繁的切换，最好不要使用 v-if, 而是推荐使用 v-show。

- 每次不会重新进行DOM的删除和创建操作，只是切换了元素的 display:none 样式，但是它有有较高的初始渲染消耗，如果元素可能永远也不会被显示出来被用户看到，则推荐使用 v-if。

## [vue中的过滤器](https://cn.vuejs.org/v2/guide/filters.html)



