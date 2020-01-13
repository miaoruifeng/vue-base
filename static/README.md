# Vue

## 基础

### 安装

- **不支持** IE8 及以下版本

- 更新日志

  https://github.com/vuejs/vue/releases

- 安装方式有多种：

  + `<script>` 标签引入

  + 通过 `npm` 安装

    ```shell
    # 默认安装最新稳定版
    $ npm install vue
    ```

  + 其它方式详见官网：

    https://cn.vuejs.org/v2/guide/installation.html

### 介绍

#### 是什么

- 可以轻松构建 SPA（Single Page Application） 应用程序
- 通过 **指令** 扩展了 HTML，通过 **表达式** 绑定数据到 HTML
- **最大程度上解放了 DOM 操作**

#### Vue 特点

- MVVM

  + Model

  + View

  + ViewModel

    ! [MVVM 图示](./images/MVVM.png)

- 数据驱动视图（data driven view）

- 面向数据

- 组件化

  + 组件由 HTML、CSS、JavaScript 构成

#### Vue 的优缺点

- 上手简单
- 简洁的 API
- 轻量高效
- 灵活的组件系统
- 强大的生态系统
  + Vue Router
  + Vuex
- 开源

#### 可以做什么

- 一切和 Web 用户界面相关的都可以使用 Vue 来做
- 对 SEO 没要求的应用
- 更加侧重于 SPA 应用的程序
- 单产品型的应用程序
- 桌面应用程序
- 管理系统
- 混合 APP
- 移动 APP

#### 发展历史

​	https://github.com/vuejs/vue/releases

- Vue.js 由尤雨溪个人正式发布于 2014 年 2 月，并开源于 Github
- 2015 年 10 月 27 日，正式发布 1.0
- 2016 年 8 月 1 日，正式发布 2.0
- 目前 Vue 2.0 最新版本为 2.6.11

#### 对比其他框架

​	https://cn.vuejs.org/v2/guide/comparison.html

### Vue 实例

- 创建实例

- 实例选项
  + el 挂载元素
  + data 数据
  + methods 方法
  + 生命周期钩子（详见后面生命周期钩子）
  + ...
  
- 实例数据 data
  + 响应式数据
  + **注意事项**：
    * 只有 data 里被代理的属性是响应的，也就是说，值的任何改变都会触发视图的重新渲染
    * 如果实例创建之后添加新的属性到实例上，它不会触发视图更新
    * 也就是说，视图需要的数据必须在初始化实例时就定义，否则 vue 会发出警告
  
- 实例方法 methods
  + methods 中的方法**不能使用箭头函数**，否则绑定的是 window
  
  + 不能与属性同名
  
  + 事件绑定不需要调用，传参需要调用
  
  + ES6 为对象成员提供了一种简写的方法：
  
    > handleClick () {}  <=>  handleClick: function() {}  （前者是后者的简写）
  
- **注意**
  
  > 不要在选项属性或回调上使用**箭头函数**，比如 `created: () => console.log(this.a)` 或 `vm.$watch('a', newValue => this.myMethod())`。因为箭头函数并没有 `this`，`this` 会作为变量一直向上级词法作用域查找，直至找到为止，经常导致 `Uncaught TypeError: Cannot read property of undefined` 或 `Uncaught TypeError: this.myMethod is not a function` 之类的错误。
  
  
  
  ```html
  <!DOCTYPE html>
  <html lang="en">
    <head>
      <meta charset="UTF-8">
      <title>Document</title>
    </head>
    <body>
      <div id="app">
        <h1>{{ message }}</h1>
        <button @click="handleClick">Click</button>
      </div>
      <script src="https://cdn.jsdelivr.net/npm/vue@2.6.11"></script>
      <script>
        const app = new Vue({
        data: {
          message: 'Hello World!'
        },
        methods: {
          // handleClick () {}  <=>  handleClick: function() {}  （前者是后者的简写）
          handleClick () {
            console.log('hello vue.js!')
          }
        },
        // 生命周期钩子
        beforeCreate () {
          console.log('beforeCreate')
        },
        created () {
          console.log('created')
        },
        beforeMount () {
          console.log('beforeMount')
        },
        mounted () {
          console.log('mounted')
        },
        beforeUpdate () {
          console.log('beforeUpdate')
        },
        updated () {
          console.log('updated')
        },
        activated () {
          console.log('activated')
        },
        deactivated () {
          console.log('deactivated')
        },
        beforeDestroy () {
          console.log('beforeDestroy')
        },
        destroyed () {
          console.log('destroyed')
        },
        errorCaptured () {
          console.log('errorCaptured')
        },
        }).$mount('#app')
      </script>
    </body>
  </html>
  ```

### 模板语法（数据绑定）

- 双向数据绑定

- “Mustache”语法，即插值语法 -- `{{ }}`

- `v-once` 指令

  一次性插值，当数据改变时，插值处的值不会更新

  ```html
  <h2 v-once>{{ msg }}</h2>
  ```

- `v-html` 指令

  双大括号会将数据解释为普通文本，而非 HTML 代码，为了输出真正的 HTML，需要用 `v-html`

  ```html
  <p>{{ rawHtml }}</p>
  <p v-html="rawHtml"></p>
  ...
  data: {
    rawHtml: '<span>hello vue.js</span>'
  },
  ...
  ```

- `v-bind` 指令

  + 只能用于属性绑定
  + 它的值是一个 JavaScript 表达式，和 {{ }} 语法一模一样
  + 唯一的区别是：{{ }} 用于标签文本绑定，v-bind 用于属性绑定

- 使用 JavaScript 表达式

  对于所有的属性绑定，都支持 JavaScript 表达式

  ```html
  <h1>{{ '这是一个JavaScript表达式绑定数据：' + message }}</h1>
  <h1 v-bind:title="'这是'+ message">{{ message }}</h1>
  ```

- 指令参数

  有些指令可以接收 “参数”

  ```html
  <a v-bind:href="url">...</a>
  <a v-on:click="doSomething">...</a>
  // 这里 href 和 click 是“参数”
  ```

- 指令动态参数

  语法：

  ```html
  <a v-bind:[attibutehref]="'http://baidu.com'">这是一个 a 链接</a>
  <button @[eventname]="handleClick">Button</button>
  ```

  **注意**：避免使用空格、引号、大写字母命名

- 指令修饰符

  以半角句号 `.` 指明的特殊后缀，用于指出一个指令应该以特殊方式绑定

  例如，`.prevent` 修饰符告诉 `v-on` 指令对于触发的事件调用 `event.preventDefault()`：

  ```html
  <form v-on:submit.prevent="onSubmit">...</form>
  ```

- 指令简写

  最常用的两个指令简写：

  `v-bind:href`  =>  `:href`

  `v-on:click="handleClick"`  =>  `@click="handleClick"`

- `v-model`

  + 双向数据绑定
  + 当数据发生改变时，Dom 会自动更新
  + 当表单控件的值改变时，数据也会自动更新

- `v-text` 指令

  指定解决 {{ }} 表达式闪烁问题

- `v-clock` 指令

  + 由于 {{ }} 使用的比较多，如果都使用 `v-text` 又比较麻烦，所有 vue 提供了一个指令 `v-cloak`

  + 这个指令保持在元素上直到关联实例结束编译。和 CSS 规则如 `[v-cloak] { display: none }` 一起用

    时，这个指令可以隐藏未编译的 Mustache 标签直到实例准备完毕。

    ```css
    [v-cloak] {
      display: none;
    }
    ```

    ```html
    <!-- 
      浏览器在解析过程中，发现具有 v-cloak 的属性，则隐藏不显示，所以看不到 {{ }} 闪烁问题
      当 Vue 解析替换完成之后，Vue 自动把 v-cloak 属性移除
    -->
    <h1 v-cloak>{{ message }}</h1>
    ```

- `v-pre`

  + 跳过这个元素和它的子元素的编译过程。

  + 告诉 Vue 不要解析该节点及内部的内容，浪费时间

### 指令

#### 概念及语法

- 指令参数
- 指令修饰符
- 指令缩写

#### 内置指令

- v-html
- v-text
- v-bind
- v-model
- v-show
- v-if
- v-else-if
- v-else
- v-for
- v-on
- v-once
- v-cloak
- v-pre

**总结**

- v-text

  + 和 `{{}}` 一样，唯一的区别是
  + `{{}}` 会有闪烁问题
  + `v-text` 不会有闪烁问题
  + 如果还想用 `{{}}` 又不想有闪烁问题，可以用 `v-cloak`

- v-show

  + 条件显示与隐藏
  + 无论真假都会渲染在 DOM 结构中
  + 本质是 `display` 控制显示隐藏
  + 如果要频繁切换显示隐藏，则使用 v-show

- v-if

  + 真正的条件渲染
  + 条件为真，则渲染 DOM
  + 条件为假，则不渲染 DOM
  + 如果只是一次显示隐藏，则用 v-if

- `v-if` vs `v-show`

  `v-if` 有更高的切换开销，而 `v-show` 有更高的初始渲染开销

#### 自定义指令

- 语法：注册及使用
- 钩子函数

### 表单输入绑定（v-model）

- `v-model` 在内部为不同的输入元素使用不同的属性并抛出不同的事件：
  + text 和 textarea 元素使用 `value` 属性和 `input` 事件；
  + checkbox 和 radio 使用 `checked` 属性和 `change` 事件；
  + select 字段将 `value` 作为 prop 并将 `change` 作为事件。

- 基础用法

  `v-model` 指令在表单 `<input>`、`<textares>` 及 `<select>` 元素上创建双向数据绑定。它会根据控件类型自动选取正确的方法来更新元素。

  > `v-model` 会忽略所有表单元素的 `value`、`checked`、`selected` 特性的初始值，将 Vue 实例的数据作为数据来源。所以必须通过组件的 `data` 选项中声明初始值。

  + 文本（input - text）

    ```html
    <input type="text" v-model="message">
    <p>Message is: {{ message }}</p>
    ```

  + 多行文本（textarea）

    ```html
    <textarea v-model="textareaInfo"></textarea>
    <p>TextareaInfo is: {{ textareaInfo }}</p>
    ```

  + 单个复选框（input-checkbox）-- 绑定到布尔值

    ```html
    <input type="checkbox" id="checkbox" v-model="checked">
    <label for="checkbox">{{ checked }}</label>
    ```

  + 多个复选框（input-checkbox）-- 绑定到同一个数组

    ```html
    <div>
        <input type="checkbox" id="vue" value="Vue" v-model="checkedNames">
        <label for="vue">Vue</label>
        <input type="checkbox" id="react" value="React" v-model="checkedNames">
        <label for="react">React</label>
        <input type="checkbox" id="angular" value="Angular" v-model="checkedNames">
        <label for="angular">Angular</label>
        <p>Checked Names: {{ checkedNames }}</p>
    </div>
    ```

    ```js
    const app = new Vue({
      data: {
        checkedNames: []
      }
    }).$mount('#app')
    ```

  + 单选按钮（input-radio）

    ```html
    <div>
        <input type="radio" id="vue" value="Vue" v-model="picked">
        <label for="vue">Vue</label>
        <input type="radio" id="react" value="React" v-model="picked">
        <label for="react">React</label>
        <input type="radio" id="angular" value="Angular" v-model="picked">
        <label for="angular">Angular</label>
        <p>Picked: {{ picked }}</p>
    </div>
    ```

    ```js
    const app = new Vue({
      data: {
        picked: ''
      }
    }).$mount('#app')
    ```

  + 选择框（select）

    ```html
    <div>
        <select v-model="selected">
            <option value="" disabled>请选择</option>
            <option>Vue</option>
            <option>React</option>
            <option>Angular</option>
        </select>
        <span>Selected: {{ selected }}</span>
    </div>
    ```

    ```js
    const app = new Vue({
      data: {
        selected: ''
      }
    }).$mount('#app')
    ```

- 值绑定

  + 单选按钮 值绑定

    ```html
    <!-- 当选中时，'pickedValue' 为字符串 'abc' -->
    <input type="radio" v-model="pickedValue" value="abc">
    ```

  + 复选框 值绑定

    ```html
    <!-- 'toggle' 为 true 或 false -->
    <input type="checkbox" v-model="toggle">
    ```

  + 选择框 value绑定 

    ```html
    <!-- 默认选中 react 项 -->
    <div>
        <select v-model="selectedValue">
            <option value="" disabled>请选择</option>
            <option value="vue">Vue</option>
            <option value="react">React</option value="vue">
            <option value="angular">Angular</option value="vue">
        </select>
        <span>SelectedValue: {{ selectedValue }}</span>
    </div>
    ```

    ```js
    const app = new Vue({
      data: {
        selectedValue: 'react'
      }
    }).$mount('#app')
    ```

- 修饰符

  + `.lazy`

    * 默认情况下，`v-model` 在每次 `input` 事件触发后将输入框的值与数据进行同步
    * 添加 `lazy` 修饰符，从而转变为使用 `change` 事件进行同步：

    ```html
    <!-- 在“change”时而非“input”时更新 -->
    <input type="text" v-model.lazy="message">
    ```

  + `.number`

    如果不使用 `.number`修饰符，即便是 `type="number"`，`input` 输入总是返回字符串（实际上，

    HTML 输入元素的值总是返回字符串），则计算就会出错

    ```html
    <!-- 如果不使用 .number 输入15  计算记过是151 -->
    <h3>{{ age + 1 }}</h3>
    <input type="number" v-model.number="age">
    ```

  + `.trim`

    用来自动过滤输入的收尾空白字符串

    ```html
    <input type="text" v-model.trim="msgtrim">
    ```

### 条件渲染

- 指令

  + `v-if`
  + `v-else-if`
  + `v-else`

- **注意：** `v-else` 元素必须紧跟在带 `v-if` 或者 `v-else-if` 的元素的后面，否则它将不会被识别

- 在 `<template>` 元素上使用 `v-if` 条件渲染分组

  + v-if 只能作用于一个标签
  + 要想控制多个标签的渲染，则用 `<template>` 元素包裹起来
  + 最终的渲染结果不包含 `<template>` 

- 用 `key` 元素管理可复用的元素

  Vue 为了更高效地渲染元素，通常会复用已有元素而不是从头开始渲染，但有时候会带来一定的麻烦

  再不需要的复用的时候，只要加上 `key` 属性即可

  ```html
  <!-- 
    不加 key 属性，切换时会复用元素，导致输入的内容也保留
    加上 key 属性，切换时，input不再复用，但此时 label 依然复用
  -->
  <div id="app">
      <tempalte v-if="toggle">
          <label for="">账号</label>
          <input type="text" placeholder="请输入用账号" key="username">
      </tempalte>
      <tempalte v-else>
          <label for="">邮箱</label>
          <input type="text" placeholder="请输入用邮箱" key="email">
      </tempalte>
      <button @click="app.toggle = !app.toggle">点击切换</button>
  </div>
  ```

  ```js
  const app = new Vue({
      data: {
          message: 'Hello World!',
          toggle: true,
          type: 'username'
      },
      methods: {}
  }).$mount('#app')
  ```

- `v-show`

  + 注意，`v-show` 不支持 ` <template>` 元素，也不支持 `v-else`

- `v-if` vs `v-show`

  > 详见指令总结内容

### 列表渲染

- 渲染数组

  ```html
  <ul>
      <li v-for="item in list">
          {{ item.id }} - {{ item.name }} - {{ item.age }} - {{ item.gender }}
      </li>
  </ul>
  <!-- 可以有第二个参数 -->
  <ul>
      <li v-for="(item, index) in list">
          {{ index }} - {{ item.name }} - {{ item.age }} - {{ item.gender }}
      </li>
  </ul>
  ```

  ```js
  const app = new Vue({
      data: {
          message: 'Hello World!',
          list: [
              { id: 1, name: 'Jack', age: 18, gender: '男'},
              { id: 2, name: 'Rose', age: 17, gender: '女'},
              { id: 3, name: 'Lile', age: 19, gender: '男'},
          ],
          obj: {
              name: 'Jack Ma',
              age: 18,
          }
      },
      methods: {}
  }).$mount('#app')
  ```

- 渲染对象

  ```html
  <ul>
      <li v-for="(value, key) in obj">
          {{ key }} - {{ value }}
      </li>
  </ul>
  ```

- 用 `key` 属性维护状态

  + 当 Vue 正在更新使用 `v-for` 渲染的元素列表时，它默认使用“就地更新”的策略。如果数据项的顺序被改

    变，Vue 将不会移动 DOM 元素来匹配数据项的顺序，而是就地更新每个元素，并且确保它们在每个索引

    位置正确渲染。

  + 这个默认的模式是高效的，但是**只适用于不依赖子组件状态或临时 DOM 状态 (例如：表单输入值) 的列表**

    **渲染输出**。

  + 为了给 Vue 一个提示，以便它能跟踪每个节点的身份，从而重用和重新排序现有元素，需要为每项提供

    一个唯一 `key` 属性：

    ```html
    <div v-for="item in items" v-bind:key="item.id">
      <!-- 内容 -->
    </div>
    ```

  + 建议尽可能在使用 `v-for` 时提供 `key` attribute，除非遍历输出的 DOM 内容非常简单，或者是刻意依赖

    默认行为以获取性能上的提升。

  + 不要使用对象或数组之类的非基本类型值作为 `v-for` 的 `key`。请用字符串或数值类型的值，一般用 ID 

    作为 key 值

### 事件处理

### Class 与 Style 绑定

### 计算属性和侦听器

## 组件

