# 渐进式框架

Vue 的设计非常注重灵活性和“**可以被逐步集成**”

- 无需构建步骤，渐进式增强静态的 HTML
- 在任何页面中作为 Web Components 嵌入
- 单页应用 (SPA)
- 全栈 / 服务端渲染 (SSR)
- Jamstack / 静态站点生成 (SSG)
- 开发桌面端、移动端、WebGL，甚至是命令行终端中的界面



# 单文件组件SFC

顾名思义，Vue 的单文件组件会将一个组件的逻辑 (JavaScript)，模板 (HTML) 和样式 (CSS) 封装在同一个文件里

- 使用熟悉的 HTML、CSS 和 JavaScript 语法编写模块化的组件
- [让本来就强相关的关注点自然内聚](https://cn.vuejs.org/guide/scaling-up/sfc.html#what-about-separation-of-concerns)
- 预编译模板，避免运行时的编译开销
- [组件作用域的 CSS](https://cn.vuejs.org/api/sfc-css-features.html)
- [在使用组合式 API 时语法更简单](https://cn.vuejs.org/api/sfc-script-setup.html)
- 通过交叉分析模板和逻辑代码能进行更多编译时优化
- [更好的 IDE 支持](https://cn.vuejs.org/guide/scaling-up/tooling.html#ide-support)，提供自动补全和对模板中表达式的类型检查
- 开箱即用的模块热更新 (HMR) 支持



# API风格

Vue 的组件可以按两种不同的风格书写：**选项式 API** 和**组合式 API**。



# 为什么会有组合式API

- 更好的逻辑复用
- 更灵活的代码组织
- 更好的类型推导
- 更小的生产包体积



# 创建一个应用

### 应用实例

每个 Vue 应用都是通过 [`createApp`](https://cn.vuejs.org/api/application.html#createapp) 函数创建一个新的 **应用实例**：

```javascript
import { createApp } from 'vue'

const app = createApp({
  /* 根组件选项 */
})

```



### 根组件

我们传入 `createApp` 的对象实际上是一个组件，每个应用都需要一个“根组件”，其他组件将作为其子组件。

如果你使用的是单文件组件，我们可以直接从另一个文件中导入根组件。

```javascript
import { createApp } from 'vue'
// 从一个单文件组件中导入根组件
import App from './App.vue'

const app = createApp(App)

```



### 挂载应用

应用实例必须在调用了 `.mount()` 方法后才会渲染出来。该方法接收一个“容器”参数，可以是一个实际的 DOM 元素或是一个 CSS 选择器字符串：

```html
<div id="app"></div>
```

```javascript
app.mount('#app')
```

应用根组件的内容将会被渲染在容器元素里面。容器元素自己将**不会**被视为应用的一部分。

`.mount()` 方法应该始终在整个应用配置和资源注册完成后被调用。同时请注意，不同于其他资源注册方法，它的返回值是根组件实例而非应用实例。



### 应用配置

应用实例会暴露一个 `.config` 对象允许我们配置一些应用级的选项，例如定义一个应用级的错误处理器，用来捕获所有子组件上的错误：

```javascript
app.config.errorHandler = (err) => {
  /* 处理错误 */
}
```

应用实例还提供了一些方法来注册**应用范围内(全局组件)**可用的资源，例如注册一个组件：

```javascript
app.component('TodoDeleteButton', TodoDeleteButton)
```



# 模板语法

- {{}}
- v-html
- v-text
- v-bind(:)

![](E:\截图\Snipaste_2023-02-07_14-28-46.png)



### 类与样式绑定

绑定HTML Class：

- 绑定对象
- 绑定数组
- 在组件上使用

绑定内联样式

- 绑定对象
- 绑定数组
- 自动前缀
- 样式多值



### 条件渲染

- v-if
- v-else-if
- v-else
- v-show

一个 `v-else` 元素必须跟在一个 `v-if` 或者 `v-else-if` 元素后面，否则它将不会被识别。

同时使用 `v-if` 和 `v-for` 是**不推荐的**，因为这样二者的优先级不明显。当 `v-if` 和 `v-for` 同时存在于一个元素上的时候，`v-if` 会首先被执行。



### 列表渲染

- v-for

**v-for与对象**

value：对象的值

key：属性名

index：位置索引

``` vue
<li v-for="(value, key, index) in myObject">
  {{ index }}. {{ key }}: {{ value }}
</li>
```



**在 `v-for` 里使用范围值**

`v-for` 可以直接接受一个整数值。在这种用例中，会将该模板基于 `1...n` 的取值范围重复多次。

```
<span v-for="n in 10">{{ n }}</span>
```

注意此处 `n` 的初值是从 `1` 开始而非 `0`。



key管理状态

```html
<div v-for="item in items" :key="item.id">
  <!-- 内容 -->
</div>
```





### 事件处理

- v-on(@)

内联事件处理器

方法事件处理器



事件修饰符

- `.stop`
- `.prevent`
- `.self`
- `.capture`
- `.once`
- `.passive`

按键修饰符

- `.enter`
- `.tab`
- `.delete` (捕获“Delete”和“Backspace”两个按键)
- `.esc`
- `.space`
- `.up`
- `.down`
- `.left`
- `.right`

- `.ctrl`
- `.alt`
- `.shift`
- `.meta`

鼠标按键修饰符

- `.left`
- `.right`
- `.middle`



### 表单输入绑定

**基础用法**

- 文本
- 多行文本（文本域）
- 复选框
- 单选按钮
- 选择器（下拉框）



注意在 `<textarea>` 中是不支持插值表达式的。请使用 `v-model` 来替代：

```vue
<!-- 错误 -->
<textarea>{{ text }}</textarea>

<!-- 正确 -->
<textarea v-model="text"></textarea>

```



**值绑定**

对于单选按钮，复选框和选择器选项，`v-model` 绑定的值通常是静态的字符串 (或者对复选框是布尔值)



复选框

`true-value` 和 `false-value` 是 Vue 特有的 attributes，仅支持和 `v-model` 配套使用。这里 `toggle` 属性的值会在选中时被设为 `'yes'`，取消选择时设为 `'no'`。

```vue
<input
  type="checkbox"
  v-model="toggle"
  true-value="yes"
  false-value="no" />
```



**修饰符**

- `lazy`

- `number`

- `trim`



# 生命周期钩子

> 每个 Vue 组件实例在创建时都需要经历一系列的初始化步骤，比如设置好数据侦听，编译模板，挂载实例到 DOM，以及在数据改变时更新 DOM。在此过程中，它也会运行被称为生命周期钩子的函数，让开发者有机会在特定阶段运行自己的代码。



![](E:\截图\Snipaste_2023-02-07_14-56-43.png)



# 组件基础

全局注册

局部注册

1. 导入
2. 注册
3. 以标签的形式使用



# 组合式API

```vue
<script lang='ts'>
import { defineComponent } from 'vue';

export defult defineComponent({
    setup() {
        
    }
    return {
    
	}
})
</script>
```



setup语法糖

```vue
<script lang='ts' setup>
import {  } from 'vue';

</script>
```



### reactive 响应式状态

- 用来实现复杂数据类的响应式
- 不用点value



### ref 响应式变量

- 用来实现基本数据类型的响应式

- 基本数据类型：.value

- 对象： .value.属性



- 解包：当 ref 在模板中作为顶层属性被访问时，它们会被自动“解包”，所以不需要使用 `.value`

  插值表达式

  当一个 `ref` 被嵌套在一个响应式对象中，作为属性被访问或更改时，它会自动解包，因此会表现得和一般的属性一样

- 对象和集合类型的ref不会进行解包



### computed 





### onMounted

生命周期钩子：组件挂载完毕，可以通过ref获取标签



### nextTick

在下一次的dom更新执行（只会执行一次）



### readonly





### watch





### watchEffect





### defineProps 不需要显示的引入





### defineEmits 不需要显示的引入





### provide(提供)《====》inject(注入)





### defineAsyncComponent



# 组合式函数



### 鼠标跟踪器示例

```javascript
// mouse.js
import { ref, onMounted, onUnmounted } from 'vue'

// 按照惯例，组合式函数名以“use”开头
export function useMouse() {
  // 被组合式函数封装和管理的状态
  const x = ref(0)
  const y = ref(0)

  // 组合式函数可以随时更改其状态。
  function update(event) {
    x.value = event.pageX
    y.value = event.pageY
  }

  // 一个组合式函数也可以挂靠在所属组件的生命周期上
  // 来启动和卸载副作用
  onMounted(() => window.addEventListener('mousemove', update))
  onUnmounted(() => window.removeEventListener('mousemove', update))

  // 通过返回值暴露所管理的状态
  return { x, y }
}
```

```javascript
<script setup>
import { useMouse } from './mouse.js'

const { x, y } = useMouse()
</script>

<template>Mouse position is at: {{ x }}, {{ y }}</template>

```



# Vue Router

```java
<script src="https://unpkg.com/vue@3"></script>
<script src="https://unpkg.com/vue-router@4"></script>

<div id="app">
  <h1>Hello App!</h1>
  <p>
    <!--使用 router-link 组件进行导航 -->
    <!--通过传递 `to` 来指定链接 -->
    <!--`<router-link>` 将呈现一个带有正确 `href` 属性的 `<a>` 标签-->
    <router-link to="/">Go to Home</router-link>
    <router-link to="/about">Go to About</router-link>
  </p>
  <!-- 路由出口 -->
  <!-- 路由匹配到的组件将渲染在这里 -->
  <router-view></router-view>
</div>
```



# Pinia

数据持久化

```js
npm i pinia-plugin-persist  安装
```



main.ts

```js
import inia-plugin-persist from 'inia-plugin-persist'
import pinia from "@/store";
pinia.use(pinia-plugin-persist);
```



```js
export const useMenusStore = defineStore("menus", {
    persist: {
        enabled: true,
        strategies: [
            {
                key: 'state',
                storage: localStorage,
            }
        ]
    },
    state: () => ({
    }),
    getters: {},
    actions: {}
})
```

























































