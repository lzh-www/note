## 一.vue指令



- Vue的基本使用步骤
- Vue中常用的指令
- vue-devtools调试工具



### 1.什么是 vue

1. 构建用户界面
   + 用 vue 往 html 页面中填充数据，非常的方便
2. 框架
   + 框架是一套现成的解决方案，程序员只能遵守框架的规范，去编写自己的业务功能！
   + 要学习 vue，就是在学习 vue 框架中规定的用法！
   + vue 的指令、组件（是对 UI 结构的复用）、路由、Vuex、vue 组件库



### 2.vue 的两个特性

1. 数据驱动视图：

   + 数据的变化**会驱动视图**自动更新
   + 好处：程序员只管把数据维护好，那么页面结构会被 vue 自动渲染出来！

2. 双向数据绑定：

   > 在网页中，form 表单负责**采集数据**，Ajax 负责**提交数据**。

   + js 数据的变化，会被自动渲染到页面上
   + 页面上表单采集的数据发生变化的时候，会被 vue 自动获取到，并更新到 js 数据中

> 注意：数据驱动视图和双向数据绑定的底层原理是 MVVM（Mode 数据源、View 视图、ViewModel 就是 vue 的实例）



### 3.vue 指令

> 指令是vue为开发者提供的模板语法，用于辅助开发者渲染页面的基本结构。



#### 1. 内容渲染指令

1. `v-text` 指令的缺点：会覆盖元素内部原有的内容！
2. `{{ }}` 插值表达式（Mustache语法）：在实际开发中用的最多，只是内容的占位符，不会覆盖原有的内容！
3. `v-html` 指令的作用：可以把带有标签的字符串，渲染成真正的 HTML 内容！



#### 2. 属性绑定指令

>  注意：插值表达式只能用在元素的**内容节点**中，不能用在元素的**属性节点**中！

+ 在 vue 中，可以使用 `v-bind:` 指令，为元素的属性动态绑定值；

+ `v-bind` 简写是  `:`

+ 在使用 v-bind 属性绑定期间，如果绑定内容需要进行动态拼接，则字符串的外面应该包裹单引号，例如：

  ```xml
  <div :title="'box' + index">这是一个 div</div>
  ```



#### 3. 事件绑定指令

1. `v-on:` 简写是 `@`

2. 语法格式为：

   ```xml
   <button @click="add"></button>
   
   methods: {
      add() {
   			// 如果在方法中要修改 data 中的数据，可以通过 this 访问到
   			this.count += 1
      }
   }
   ```

3. `$event` 的应用场景：如果默认的事件对象 e 被覆盖了，则可以手动传递一个  $event。例如：

   ```xml
   <button @click="add(3, $event)"></button>
   
   methods: {
      add(n, e) {
   			// 如果在方法中要修改 data 中的数据，可以通过 this 访问到
   			this.count += 1
      }
   }
   ```

4. 事件修饰符：

   + `.prevent` 阻止默认行为，from表单有submit事件，阻止表单默认提交，@submit.prevent。

     ```xml
     <a @click.prevent="xxx">链接</a>
     ```

   + `.stop` 阻止冒泡

     ```xml
     <button @click.stop="xxx">按钮</button>
     ```

5. 按键修饰符

   + `.exc`

   + `.enter`

#### 4. 双向数据绑定指令

只能用在表单元素上

1. input 输入框
   + type="radio"
   + type="checkbox"
   + type="xxxx"
2. textarea
3. select
4. v-model指令的修饰符

​	`v-model.number` 自动将用户的输入值转为数值类型

​	`v-model.trim` 自动过滤用户输入的首尾空白字符

​	`v-model.lazy` 在 “change” 时而非 “input” 时更新，input的值变化不会实时变化，在失去光标的时候才会更新。



#### 5. 条件渲染指令

1. `v-show` 的原理是：动态为元素添加或移除 `display: none` 样式，来实现元素的显示和隐藏
   + 如果要频繁的切换元素的显示状态，用 v-show 性能会更好
2. `v-if` 的原理是：每次动态创建或移除元素，实现元素的显示和隐藏
   + 如果刚进入页面的时候，某些元素默认不需要被展示，而且后期这个元素很可能也不需要被展示出来，此时 v-if 性能更好

>  在实际开发中，绝大多数情况，不用考虑性能问题，直接使用 v-if 就好了！！！



v-if 指令在使用的时候，有两种方式：

1. 直接给定一个布尔值 true 或 false

   ```xml
   <p v-if="true">被 v-if 控制的元素</p>
   ```

2. 给 v-if 提供一个判断条件，根据判断的结果是 true 或 false，来控制元素的显示和隐藏

   ```xml
   <p v-if="type === 'A'">良好</p>
   ```

3. `v-else`




#### 6.循环渲染指令

vue提供了`v-for`列表渲染指令，用来辅助开发者基于一个数组来循环渲染一个列表结构。v-for指令需要使用 item in items 形式的特殊语法：

- items是待循环的数组
- item是被循环的每一项

```xml
data: {
    list: [
        {id: 1, name: 'zs'},
        {id: 2, name: 'ls'}
    ]
}

<tr v-for="(item, index) in list" :key="item.id"> //用到v-for一定要绑定:key属性值为字符串或者数字类型，不能重复。
    <td>{{ index }}</td> //索引
    <td>{{ item.id }}</td>
    <td>{{ item.name }}</td>
</tr>
```



## 二.过滤器/侦听器/计算属性

- 过滤器和侦听器
- 计算属性的用法
- axios的基本用法
- vue-cli的安装和使用



### 1.过滤器

> 过滤器在vue3中已经被抛弃了，vue2还能正常使用



#### 1.1私有过滤器

```js
<p>{{ message | capi }}</p>

//过滤器本质上是一个函数
filters: {
    //过滤器函数形参中val，永远都是管道符前面的那个值
    capi(val) {
        return
    }
}
```



#### 1.2全局过滤器

```js
Vue.filter('capi', function (val) {
    return xxx
})
```



:warning:过滤器的注意点

1. 要定义到 filters 节点下，本质是一个函数
2. 在过滤器函数中，一定要有 return 值
3. 在过滤器的形参中，可以获取到“管道符”前面待处理的那个值
4. 如果全局过滤器和私有过滤器名字一致，此时按照“就近原则”，调用的是”私有过滤器“



### 2.侦听器

> watch侦听器允许开发者监视数据的变化，从而针对数据的变化做特定的操作。



```js
//定义成方法
watch: {
    username(newVal, oldVal) {
        console.log(newVal, oldVal)
    }
}
```



>  默认情况下，组件在初次加载完毕后不会调用watch侦听器。如果想让watch侦听器立即被调用，则需要使用==immediate选项==。
>
> 当watch侦听的是一个对象，如果对象中的属性值发生了变化，则无法被监听到。此时需要使用==deep选项==。

```js
//定义成对象
watch: {
    info: {
         handler(newVal, oldVal) {
              console.log(newVal, oldVal)
         },
         immediate: true; // 控制侦听器自动触发一次
         deep:true; // 只要对象中任何一个属性变化了，都会触发对象的侦听器
    }
}
```



> 侦听对象单个属性的变化

```js
data() {
    return {
        info: { username: 'admin', password: '' }
    }
},
watch: {
    'info.username': {
        async handler(nweVal, oldVal) {
            const { data: res } = await axios.get(`https://www.escook.cn/api/finduser/${newVal}`)
            console.log(res)
        }
    }
}
```



侦听器的格式

1. ==方法格式==的侦听器
   + 缺点1：无法在刚进入页面的时候，自动触发
   + 缺点2：如果侦听的是一个对象，如果对象中的属性发生了变化，不会触发侦听器
2. ==对象格式==的侦听器
   + 好处1：可以通过 **immediate** 选项，让侦听器自动触发
   + 好处2：可以通过 **deep** 选项，让侦听器深度监听对象中每个属性的变化
   



侦听器:vs:计算属性

> 计算属性侧重于多个值的变化，最终计算并返回一个新值。
>
> 侦听器侧重于单个数据的变化，最终执行特定的业务处理，不需要有任何返回值。



### 3.计算属性

> 计算属性本质上就是一个==function函数==，它可以实时监听data中数据的变化，并return一个计算后的新值，供租价渲染DOM时使用



```js
computed: {
    rgb() {
        return `rgb($(this.r),$(this.g),$(this.b))`
    }
}
```



特点：

1. 定义在computed节点中
2. 定义的时候，要被定义为“方法”
3. 使用计算属性，把他当做普通属性使用即可
4. 计算属性必须有返回值



好处：

1. 实现了代码的复用
2. 只要计算属性中依赖的数据源变化了，则计算属性会自动重新求值！



计算属性:vs:方法

> 相对于方法来说，计算属性会缓存计算的结果，只有计算属性的依赖项发生变化时，才会重新进行运算。因此计算属性的性能更好。



### 4.axios

> axios 是一个专注于网络请求的库！



```js
import axios from 'axios'

methods: {
    // 封装请求列表数据的方法
    async initCartList() {
        const { data: res } = await axios.get('httpe://www.escook.cn/api/cart')
	}
}
created() {
    // 调用请求数据的方法
    this.initCartList()
}

```



#### 4.1全局配置axios

在实际项目开发中，几乎每个组件中都会用到axios发起数据请求。此时会遇到如下两个问题：

- 每个组件中都需要导入axios（代码臃肿）
- 每次发起请求都需要填写完整的请求路径（不利于后期的维护）

![](E:\Typora笔记\images\Snipaste_2022-09-20_10-20-05.png)



**vue2**

> 需要在main.js入口文件中，通过Vue构造函数的prototype原型对象全局配置axios

```js
import Vue from 'vue'
import axios from 'axios'

axios.defaults.baseURL = 'https://www.escook.cn'
Vue.prototype.$http = axios

```



**vue3**

> 在main.js入口文件中，通过app.config.globalProperties全局挂载axios

![](E:\Typora笔记\images\Snipaste_2022-09-20_10-24-49.png)



### 5.vue-cli



1. 在终端下运行如下的命令，创建指定名称的项目：

   ```bash
   vue cerate 项目的名称; vue ui;
   ```

   

2. vue 项目中 src 目录的构成：

   ```xml
   assets 文件夹：存放项目中用到的静态资源文件，例如：css 样式表、图片资源
   components 文件夹：程序员封装的、可复用的组件，都要放到 components 目录下
   main.js 是项目的入口文件。整个项目的运行，要先执行 main.js
   App.vue 是项目的根组件。
   ```




3. vue项目的运行流程：

   在工程化的项目中，vue要做的事情很单纯：通过main.js把App.veu渲染到index.html的指定区域中。

   ```js
   App.vue用来编写待渲染的模板结构
   index.html中需要预留一个el区域
   main.js把App.vue渲染到了index.html所预留的区域中
   ```



### 6.vite

```js
npm create vite@latest
```

```js
npm init vite-app XXx
```



## 三.组件与生命周期

- 组件的注册与使用
- 组件的props自定义属性
- 解决组件样式冲突
- 组件的生命周期
- 组件之间的通讯（数据共享）

***



### 1.组件

> 组件就是对UI结构的复用



**三个组成部分**

- template -> 组件的模板结构（模板）

- script -> 组件的 JavaScript 行为（脚本）
- style -> 组件的样式（样式）

```js
<script>
// 默认导出
export default {
	name: '',
	//数据源，必须是一个函数
	data() {
        return{}
	},
    //处理函数
    methods: {
        
    },
    //侦听器
    watch: {
        
    },
    //计算属性
    computed: {
        
    },
    //过滤器
    filters: {
        
    },
    //组件
    components: {
        
    }
}
</script>
<style lang="less/css" scoped></style>//使用less语法
```



使用组件的==三个步骤==

1. 导入
2. 注册
3. 以标签形式使用



组件的注册

- 通过components注册的是私有子组件

- 注册全局组件

- 在vue项目的main.js入口文件中，通过Vue.component()方法，可以注册全局组件。

```js
//导入需要全局注册的组件
import Count from '@/components/Count.vue'

//参数1: 字符串格式，表示组件的注册名称
//参数2: 需要被全局注册的那个组件
Vue.component('MyCount', Count) // Count.name


import MySearch from '@/components/Search.vue'
//私有
components: {
    'Mysearch': MySearch // 简写MySearch
}


//使用
<MyCount></MyCount>
<Mysearch></Mysearch>
```



全局注册和局部注册的区别

- 被全局注册的组件，可以在全局任何一个组件内使用
- 被局部注册的组件，只能在当前注册的范围内使用



组件注册时名称的大小写

- 使用kabab-case命名法（==短横线命名法==，列入my-swiper和my-search）
- :star: 使用PascalCase命名法（==帕斯卡命名法==或大驼峰命名法， 列如MySwiper和MySearch）

短横线命名法的特点：

- 必须严格按照短横线名称进行使用

帕斯卡命名法的特点：

- 既可以严格按照帕斯卡名称进行使用，又可以==转化为短横线名称进行使用==



### 2.组件的props

>  props是组件的自定义属性，组件的使用者可以通过props把数据传递到子组件内部，供子组件内部进行使用。
>
> props的作用：父组件通过props向子组件传递要展示的数据，提高了组件的复用性。



```js
export default {
    
    //外界可以传递指定的数据，到当前的组件中
    
    //数组格式props
    props: ['init', '自定义属性...']
    
    //对象格式props 
    props: {
    	init: {
    		default: 0, //设置默认值
    		type: Number, //设置类型
    		required: true //必填项校验
		}
	}
}

// props只读, 不能被修改，需要把props的值，'转存'到data中，就可以进行读写操作。
// 在组件中设置属性的值
<MyCount init="6"></MyCount>
```



> 动态绑定props的值，v-bind。
>
> 在使用组件的时候，如果某个属性名是驼峰命名法的形式声明了props属性的名称，则绑定属性的时候，可以使用短横线命名法。

```js
props: {
    cmtCount: {
      type: [Number, String],
      default: 0
    }
}
```

```js
<ArticleInfo v-for="item in artlist" :key="item.id" :cmt-count="item.comm_count" ></ArticleInfo>
```



### 3.样式冲突

> 单页面应用程序中，所有组件的DOM结构，都是基于==唯一的index.html页面==进行呈现的。每个组件中的样式，都会==影响整个index.heml页面中的DOM元素==。



```js
<style lang="less" scoped></style>

//h5[data-v-xxx] 属性选择器原理

/deep/ h5 {} //当使用第三方组件库的时候，如果有修改组件默认样式的需求，就需要用/deep/深度选择器 vue2
:deep(h5) {} // vue3

```



### 4.样式绑定



#### 4.1动态绑定HTML的class

> 可以通过三元表达式，动态的为元素绑定class的类名。

```js
<h3 class="thin" :class="isItalic ? 'italic' : ''">组件</h3>
<button @click="isItalic = !isItalic">Toggle Italic</button>

data() {
    return {
        isItalic: true
    }
}

.thin {
    font-weight: 200;// 字体变细
}
.italic {
    font-style: italic; // 倾斜字体
}
```



#### 4.2以数组语法绑定HTML的class

> 如果元素需要动态绑定多个clss的类名，此时可以使用数组的语法格式

 ```js
 <h3 class="thin" :class="[isItalic ? 'italic' : '', isDelete  ? 'delete' : '']">组件</h3>
 ```



#### 4.3以对象语法绑定HTML的class

> 使用数组语法动态绑定clss会导致模板结构臃肿的问题。此时可以使用对象语法进行简化

```js
<h3 class="thin" :class="classObj">组件</h3>
<button @click="classObj.italic = !classObj.italic">Toggle Italic</button>
<button @click="classObj.delete = !classObj.delete">Toggle Delete</button>

data() {
    return {
        classObj: {
            italic: true,
            delete: false
        }
    }
}

.thin {
    font-weight: 200;// 字体变细
}
.italic {
    font-style: italic; // 倾斜字体
}
.delete {
    text-decoration: line-through; // 删除线
}
```



#### 4.4以对象语法绑定内联的style

> :style的对象语法十分直观一看着非常像CSS,但其实是一个JavaScript对象。CSS property名可以用驼峰式(camelCase)或短横线分隔(kebab-case,记得用引号括起来)来命名

```js
<div :style="{color: active, fontSize: fsize + 'px', 'background-color': bgcolor}">组件</div>
<button @click="fsize +=1">+</button>
<button @click="fsize -=1">-</button>

data() {
    return {
        active: 'red',
        fize: 30,
        bgcolor: 'pink'
    }
}
```



### 5.组件的生命周期



>  概念：每个组件从==创建 -> 运行 -> 销毁==的一个过程，强调的是一个==时间段==

<img src="E:\Typora笔记\images\屏幕截图 2022-09-19 225848.png" style="zoom: 80%;" />



> 生命周期函数：在生命周期的不同阶段，会按次序，自动依次执行的函数。

<img src="E:\Typora笔记\images\屏幕截图 2022-09-19 232945.png" style="zoom:80%;" />



> :white_check_mark:组件在内存中被创建。经常在它里面发ajax请求初始数据。

```js
created() {}
```



> 组件第一次被渲染页面上，最早可以操作dom元素的函数。

```js
mounted() {}
```



> 当数据变化之后，为了操作最新的dom结构，需要把代码写到update生命周期函数里。

```js
update() {}
```



> 组件被销毁完毕。

```js
unmounted() {}
```



### 6.组件之间的数据共享



> 父组件向子组件共享数据需要使用==自定义属性==。

```js
//父组件
<Son :msg="message" :user="userinfo"></Son>
data() {
    return {
        message: 'hello vue.js',
        userinfo: {name: 'zs', age: 20}
	}
}
```

```js
//子组件
<template>
    <div>
    	<p> msg的值是: {{ msg }}</p>
		<p> user的值是: {{ user }}</p>
    </div>
</template>

props: ['msg', 'user']
```



>  子组件向父组件共享数据使用==自定义事件==。

```js
//子组件
emits: ['num'] //声明自定义事件
methods: {
    add() {
        this.$emit('num', 10); //参数1: 字符串，表示自定义事件的名称 参数2: 值，发送给父组件的数据
	}
}
```

```js
//父组件
<Son @num="getnum"></Son>  //监听组件的自定义事件num

methods: {
    // 通过形参，接收子组件传递过来的数据
    getnum(value) {
        console.log(value); // 10
    } 
}
```



> 父子组件之间数据的双向同步，==组件上的v-model==。

<img src="E:\Typora笔记\images\Snipaste_2022-09-20_09-34-40.png" style="zoom:80%;" />



> 兄弟组件之间数据共享的方案是 ==EventBus==。可以借助于第三方的包mitt来创建eventBus对象。

<img src="E:\Typora笔记\images\Snipaste_2022-09-20_09-41-24.png" style="zoom:80%;" />



> 后代关系组件之间的数据共享，指的是父节点的组件向其子孙组件共享数据。此时组件之间的嵌套关系比较复杂，可以使用provide和inject实现后代关系组件之间的数据共享。

```js
//父级组件发送的数据
provide() {
    return {
        color: this.color
    }
}
```

```js
inject: ['color'] //子级组件接收的数据
```



> 父节点使用provide向下共享数据时，可以结合computed函数向下共享响应式的数据。

```js
import { computed } from 'vue'

export default {
    data() {
        return { color: 'red' }
    },
    provide() {
        return {
            color: computed(() => this.color) //使用computed函数，可以把要共享的数据包装为响应式的数据
        }
    }
}
```

```js
{{ color.value }} //使用 

inject: ['color'] //子级组件接收的数据
```



## 四.ref和$nextTick

- 使用ref引用DOM元素和组件实例
- $nextTick的基本使用

***



### 1.ref引用

> ref用来辅助开发者在不依赖于`jQuery`的情况下，获取DOM元素或组件的引用。
>
> 每个vue的组件实例上，都包含一个$refs对象，里面存储着对应的DOM元素或组件的引用。默认情况下，组件的`$ref`指向一个空对象。



标签使用

```js
ref="自定义属性" // this.$refs.属性 => 拿到dom
```

组件使用

```js
ref="自定义属性" //在组件上使用可以拿到组件实例
```



### 2.$nextTick

> 在下次 DOM 更新循环结束之后执行延迟回调。在修改数据之后立即使用这个方法，获取更新后的 DOM。



```js
this.$nextTick(() => {})
```



## 五.Vue组件的高级用法

- 动态组件的使用
- 插槽的使用（默认插槽，具名插槽，作用域插槽）
- 自定义指令

***



### 1.动态组件

> 动态组件指的是动态切换组件的显示与隐藏。vue提供了一个内置的`<component>`组件，专门用来实现组件的动态渲染。



1. `<component>`是组件的占位符
2. 通过is属性动态指定要渲染的组件名称
3. `<component :is="要渲染组件的名称"></component>`



```js
<component :is=""></component>
```



### 2.keep-alive

> 默认情况下，切换动态组件时无法保持组件的状态。此时可以使用vue内置的<keep-alive>组件保持动态组件的状态。



keep-alive对应的生命周期函数

- 当组件==被缓存==时，会自动触发组件的`deactivated`生命周期函数
- 当组件==被激活==时，会自动触发组件的`activated`生命周期函数



keep-alive的include属性

```js
<keep-alive include="指定缓存组件的名称，用逗号隔开">
    <component :is=""></component>
</keep-alive>
```



keep-alive的exclude属性

```js
<keep-alive exclude="指定不缓存组件的名称，用逗号隔开">
    <component :is=""></component>
</keep-alive>
```



了解组件注册名称和组件声明时name的区别

>如果在“声明组件”的时候，没有为组件指定name名称，则组件的名称默认就是“注册时候的名称”

对比：

1. 组件的“注册名称”的主要应用场景是：以标签的形式，把注册好的组件，渲染和使用到页面结构之中
2. 组件声明时候的`name`名称的主要应用场景：结合 <keep-alive>标签实现组件缓存功能, 以及在调试工具中看到组件的name名称:



### 3.插槽

> vue为组件的封装者提供的能力。允许开发者在封装组件时，把不确定的，希望由用户指定的部分定义为插槽。



**基础用法**

```js
// App组件
<MySlot>
    <p>这个内容将会被渲染到slot插槽中</p>
</MySlot>
```

```js
// MySlot组件
<template>
    <slot></slot> //没有预留插槽的内容会被丢弃
</template>
```



**后备内容**

> 封装租价时，可以为预留的<slot>插槽提供后备内容（默认内容）。如果组件的使用者没有为插槽提供任何内容，则后备内容会生效。



```js
<template>
    <slot>这是后备内容</slot>
</template>
```



**具名插槽**

> 如果在封装组件时需要==预留多个插槽节点==，则需要为每个<slot>插槽指定具体的name名称。这种带有具体名称的插槽叫做"具名插槽"。:warning:没有指定name名称的插槽，会有隐藏的名称叫做"default"。



```js
<template>
    <slot name="header">这是后备内容1</slot>
	<slot>这是后备内容2</slot>
	<slot name="footer">这是后备内容3</slot>
</template>
```



**为具名插槽提供内容**

> 在向具名插槽提供内容的时候，我们可以在一个<template>元素上使用v-slot指令，并以v-slot的参数的形式提供给其名称。`v-slot:` 指令的简写是`#`

```js
// App组件
<MySlot>
    <template v-slot:header>
        <p>这是头部</p>
    </template>
	<template v-slot:default>
        <p>这是内容区域</p>
    </template>
	<template v-slot:footer>
        <p>这是底部</p>
    </template>
</MySlot>
```



**作用域插槽**

> 在封装组件时，为预留的<slot>插槽绑定props数据，这种带有props数据的<slot>叫做作用域插槽。



```js
// App组件
<MySlot>
    <template v-slot:header="{msg, info}"> //解构赋值
        <p>{{ msg }}</p>
		<p>{{ info }}</p>
    </template>
</MySlot>
```



```js
<template>
    <slot name="header" :msg="message" :info="infomation">这是后备内容1</slot>
</template>

export default {
	data() {
        return {
            message: '信息',
            infomation: {
                name: '张三',
                age: 15
            }
        }
    }
}

```



### 4.自定义指令



vue中的自定义指令分为两类：

- 私有自定义指令
- 全局自定义指令



在每个vue组件中，可以在directives节点下声明私有自定义指令。

```js
<div v-color="color">自定义指令</div>
<div v-color="'red'">自定义指令</div>
```

```js
data() {
    return {
        color: 'blue'
    }
}
```

```js
directives: {
    color: {
        // 当指令第一次被绑定到元素时被调用
        mounted(el, binding) {
            el.style.color = binding.value
        },
        // 每次DOM更新时被调用
        update(el, binding) {
        	el.style.color = binding.value
    	}
    }
}
```



自定义指令自动获取焦点

```js
  directives: {
    focus(el) {
      el.focus()
    }
//使用v-focus
```



函数简写

如果bind和update函数中的逻辑完全相同，则对象格式的自定义指令可以简写成函数格式

```js
directives: {
    color(el, binding) {
        el.style.color = binding.value
    }
}
```



在main.js中，用app.directives()声明全局自定义指令。

```js
app.directive('color', {
    bind(el, binding) {
        el.style.color = binding.value
    },
    update(el, binding) {
        el.style.color = binding.value
    }
})
```

简写

```js
app.directive('color', function(el, binding) {
    el.style.color = binding.value
})
```



## 六.路由(vue-router)

- 路由的基本配置与使用
- 路由重定向
- 嵌套路由，动态路由
- 编程式导航，路由导航守卫

***



### 1.前端路由的概念与原理

> 路由就是对应关系。路由分为两大类：后端路由和前端路由



==前端路由==（Hash地址与组件之间的对应关系）

==后端路由==（请求方式，请求地址与function处理函数之间的对应关系）



#### 1.SPA与前端路由

> SPA指的是一个web网站只有唯一的一个HTML页面，所有组件的展示与切换都在这唯一的一个页面内完成。此时，不同组件之间的切换需要通过前端路由来实现。



#### 2.前端路由的工作方式

> 1. 用户点击了页面上的路由链接
> 2. 导致了URL地址栏中的Hash值发生了变化
> 3. 前端路由监听到了Hash地址的变化
> 4. 前端路由把当前Hash地址对应的组件渲染到浏览器中

<img src="E:\Typora笔记\images\Snipaste_2022-09-22_23-26-20.png" style="zoom:80%;" />



### 2.vue-router 的基本使用

> vue-router 是vue.js官方给出的路由解决方案。它只能结合vue项目进行使用，能够轻松的管理SPA项目中组件的切换。



#### 2.1 vue-router 的版本

> :warning:版本3和版本4的路由最主要的区别：创建路由模块的方式不同！

- [vue-router 3.x](https://router.vuejs.org/zh/) 结合vue2使用
- [vue-router 4.x](https://next.router.vuejs.org/zh/) 结合vue3使用



#### 2.2 vue-router 3.x 的基本使用步骤



在vue2的项目中，安装并使用vue-router 3.x版本的路由：

```js
npm install vue-router@3.4.9 -S
```



```js
// 使用router-link代替普通的a链接
<router-link to="/home">首页</router-link>
<router-link to="/movie">电影</router-link>
<router-link to="/about">关于</router-link> 
```



```js
<router-view></router-view> // 占位符
```



在src目录下创建==路由模块==router --> index.js

```js
import Vue from 'vue'
import VueRouter from 'vue-router' //导入路由构造函数

//导入组件
import Home from '@/components/Home.vue'
import Movie from '@/components/Movie.vue'

//调用Vue.use()函数，把VueRouter安装为Vue的插件
Vue.use(VueRouter)

//创建路由的实例对象
const router = new VueRouter({
    //路由规则
    routes: [
        { path: '/home', component: Home },
        { path: '/movie', component: Movie }
    ]
})

//向外共享路由的实例对象
export default router
```



main.js入口文件

```js
import router from './router/index.js' //引入路由

new Vue({
  render: h => h(App),
  router // 注册路由
}).$mount('#app')
```



#### 3.vue-router 4.x 的基本使用步骤

1. 在项目中安装vue-router
2. 定义路由组件
3. 声明路由链接和占位符
4. 创建路由模块
5. 导入并挂载路由模块



在vue3的项目中，安装并使用vue-router 4.x版本的路由：

```js
npm install vue-router@next -S
```



路由模块

```js
import { createRouter, createWebHashHistory } from 'vue-router'

const router = createRouter({
    history: createWebHashHistory(),
    routes: [
        { path:'' , component: }
    ]
})

export default router
```



main.js


```js

import { createApp } from 'vue'
import App from './App.vue'


createApp(App).use(router).mount('#app')
```





### 3.路由重定向



> 用户在访问地址A的时候，强制用户跳转到地址C，从而展示特定的组件页面。通过路由规则的==redirect属性==，指定一个新的路由地址，可以很方便地设置路由的重定向



```js
routes: [
    { path: '/', redirect: '/home' },
    { path: '/home', component: Home }
]
```



### 4.嵌套路由

> 通过路由实现组件的嵌套展示，叫做嵌套路由。

<img src="E:\Typora笔记\images\Snipaste_2022-09-23_10-48-11.png" style="zoom:80%;" />



1.声明子路由链接和子路由占位符

```js
//在关于页面中，声明两个路由链接
<router-link to="/about/tab1"></router-link>
<router-link to="/about/tab2"></router-link>

//在关于页面中，声明tab1和tab2的路由占位符
<router-view></router-view>
```



2.在父路由规则中，通过children属性嵌套声明子路由规则

```js
routes: [
    { path: '/', redirect: '/home' },
    { path: '/home', component: Home, children: [
        {path: 'tab1', component: Tab1}, // 不加'/'号
        {path: 'tab2, component: Tab2},
    ] }
]
```



3.在嵌套路由中使用路由重定向

```js
routes: [
    { path: '/', redirect: '/home' },
    { path: '/home', component: Home, redirect: '/home/tab1', children: [
        {path: 'tab1', component: Tab1}, // 不加'/'号
        {path: 'tab2, component: Tab2},
    ] }
]
```



默认子路由

> 如果在children数组中，某个路由规则的path值为空字符串，则这条路由规则，叫做“默认子路由”



### 5.动态路由匹配

> 把Hash地址中可变的部分定义为参数项，从而提高路由规则的复用性。在vue-router中使用`:`号来定义路由的参数项



```js
{path: '/movie/1', component: Movie}
{path: '/movie/2', component: Movie}
{path: '/movie/3', component: Movie}
```

```js
{path: '/movie/:id', component: Movie} //动态的参数项id可以任意取名合法既可
```



获取动态路由参数值的两种方案



1.$route.params 参数对象

> 通过动态路由匹配的方式渲染出来的组件中，可以使用$route.params对象访问到动态匹配的参数值。



```js
$route.params.参数
```



2.使用props接收路由参数

> 为了简化路由参数的获取形式，vue-router允许在路由规则中开启props传参。



```js
{path: '/movie/:id', component: Movie, props: true} //动态的参数项id可以任意取名合法既可
```

```js
export default {
    props: ['id'] //使用props接收路由规则中匹配到的参数项
}
```





### 6.导航

> 在浏览器中，点击链接实现导航的方式，叫做声明式导航。:普通网页中点击<a>链接，vue项目中点击<router-link>
>
> 在浏览器中，调用API方法实现导航的方式，叫做编程式导航。:普通网页中调用location.href跳转到新页面的方式



vue-router中的编程式导航API

:one: this.$router.push( 'hash地址' )

- 增加一条历史记录

:two:this.$router.replace( 'hash地址' )

- 替换掉当前的历史记录

:three:this.$router.go( n )

- 可以在浏览历史前进后退，如果上限则原地不动

- $router.back( -n ) 后退一层
- $router.forwaid( n ) 前进一层



### 7.命名路由

> 通过name属性为路由规则定义名称的方式，叫做命名路由。:warning:name值不能重复，必须保证唯一性。

```js
{path: '/movie/:id', component: Movie, name: 'mov'}
```



使用命名路由实现声明式导航

> 为<router-link>标签动态绑定to属性的值，并通过name属性指定要跳转到的路由规则。期间还可以用params属性指定跳转期间要携带的路由参数。

```js
<router-link to="{ name: 'mov', params: { id: 3 } }"></router-link>
```



使用命名路由实现编程式导航

> 调用push函数期间指定一个配置对象，name是要跳转到的路由规则，params是携带的路由参数。

```js
<button @click="gotoMovie(3)">go to Movie</button>

methods: {
    gotoMovie(id) {
        this.$router.push({ name: 'mov', params: { id: 3 } })
    }
}

```



### 8.导航守卫

> 导航守卫可以控制路由的访问权限。

<img src="E:\Typora笔记\images\Snipaste_2022-09-23_11-51-57.png" style="zoom: 80%;" />



在路由模块下声明全局前置导航守卫

```js
router.beforeEach((to, from, next) => {
    // to表示将要访问的路由信息对象
    // from表示将要离开的路由信息对象
    // next()函数表示放行的意思
})
```

```js
router.beforeEach((to, from, next) => {
    if(to.path === '/main') {
        next('/login')
    } else {
        next()
	}
})
```



注意:warning:

- 在守卫方法中如果不声明next形参，则默认允许用户访问每一个路由!

- 在守卫方法中如果声明next形参，则必须调用 next() 函数，否则不允许用户访问任何一个路由!



next函数的3中调用方式

:one:当前用户拥有后台主页的访问限制，直接放行：next()

:two:当前用户没有后台主页的访问限制，强制其跳转到登录页面：next('/login')

:three:当前用户没有后台主页的访问限制，不允许跳转到后台主页，强制停留在当前页面：next(false)



关于token

```js
localStorage.setItem('token', 'Bearer xxxx') //设置token
```

```js
localStorage.removeItem('token') //清除token
```

```js
localStorage.getItem('token') //获取token
```



### 9.路由元信息

> 配置路由的时候，可以给路由添加路由元信息，`meta` 路由需要配置对象，它的key不能瞎写，胡写，乱写。



```js
meta: { show: true }

$route.meta.show //组件实例下$route挂载
```



### 10.路由传参

> params参数：属于路径中的一部分，需要注意，在配置路由的时候，需要占位，`path: '/search/:keyword'`。
>
> query参数：不属于路径当中的一部分，类似于ajax中的queryString  /home?k=v&k1=v1 ，不需要占位



:one: 字符串形式 

```js
this.$router.push('/search/' + this.keyword + '?k=' + this.keyword.toUpperCase())
```



:two: 模板字符串

```js
this.$router.push(`/search/${this.keyword}?k=${this.keyword.toUpperCase()}`)
```



:three: 对象形式:star:

> 需要在配置路由的时候定义name，命名路由

```js
this.$router.push({ name: 'search' , params: { keyword: this.keyword }, query: { k: this.keyword.toUapperCase() }})
```



路由组件传递props

1.布尔值形式： `props：true` 只能传递params参数

2.对象形式：`props: {}` 额外给路由组件传递一些props

3.函数形式:star: ：`props: ($route) => ({keyword: $route.params.keyword, k:$route.query.k})`





## 七.Vuex

- Vux概述
- Vue的基本使用
- Vue的核心概念

---



### 1.Vuex的概述

> vuex是官方提供一个插件，用来实现组件全局状态管理的一种机制，状态管理库，集中式管理项目中组件共用的数据。
>
> :warning:切记，并不是全部项目都需要Vuex，如果项目很小，完全不需要Vue。如果项目很大，组件很多，数据很多，数据维护很费劲，使用Vuex。



### 2.Vuex的基本配置



1.安装vuex依赖包

```js
npm install vuex --save;
```

```js
yarn add vuex
```



2.在src/store/index.js中导入vuex包

```js
import Vuex from 'vuex';
import Vue from 'vue';

Vue.use(Vuex)
```



3.创建store对象

```js
// 对外暴露Store类的一个实例
export default new Vuex.Store({
  state: {},
  mutations: {},
  actions: {},
  getters: {}
})
```



4.在main.js中将store对象挂载到vue实例中

> 将创建的共享数据对象，挂载到Vue实例中，所有的组件，就可以直接从store中获取全局的数据。



注册仓库：组件实例的身上会多出一个属性`$store`属性



```js
import store from '@/store'

new Vue({
    el: '#app',
    render: h => h(app),
    router,
    store
})
```



### 3.Vuex的核心概念

> state: 仓库存储数据的地方

> mutations: 修改state的唯一手段

> actions: 处理action，可以书写自己的业务逻辑，也可以处理异步，不能修改state

> getters: 理解为计算属性，用于简化仓库数据，让组件获取 仓库的数据更加方便



### 4.Vuex的基本使用















## 八.Vue3

- props验证
- 计算属性
- 自定义事件
- 组件上的v-model
- 任务列表案例

***



### 1.props验证



> 在封装组件时对外界传递过来的props数据进行合法性的校验，从而防止数据不合法的问题。
>
> 使用数组类型的props节点的缺点：无法为每个props指定具体的数据类型。



对象类型的props节点

使用对象类型的props节点，可以对每个prop进行数据类型的校验。

![image-20220918184737583](C:\Users\lanzh\AppData\Roaming\Typora\typora-user-images\image-20220918184737583.png)



对象类型的props节点提供了多种数据验证方案

- 基础的类型检查
- 多个可能的类型
- 必填项校验
- 属性默认值
- 自定义验证函数



自定义验证函数

```js
props: {
    pro: {
        validator(value) { //函数返回值为true表示验证通过，false表示验证失败
            return ['success', 'warning', 'danger'].indexOf(value) !== -1
        }
    }
}
```



### 3.自定义事件



在封装组件时：

- 声明自定义事件
- 触发自定义事件

```js
//1.声明自定义事件
emits: ['countChange']

//2.this.$emit触发自定义事件
this.$emit('countChange', this.count)
```



在使用组件时：

- 监听自定义事件

```js
<MyCounter @countChange="getCount"></my-counter>

methods: {
    getCount(val) {
        console.log('出发了 countChange 自定义事件', val)
    }
}

```



### 4.组件上的v-model

> v-model是双向数据绑定指令，当需要维护组件内外数据的同步时，可以在组件上使用v-model指令。
>
> 通过自定义事件更新属性对应的值emit: ['update: 属性']



![image-20220919095035060](C:\Users\lanzh\AppData\Roaming\Typora\typora-user-images\image-20220919095035060.png)



### 5.路由高亮



路由高亮

可以通过如下的两种方式，将==激活的路由链接==进行高亮显示：

1. 使用默认的高亮class类
2. 自定义路由高亮的class类



1.默认的高亮class类

>被激活的路由链接，默认会应用一个叫做router-link-active的类名。开发者可以使用此类名选择器，为激活的路由链接设置高亮的样式。



2.自定义路由高亮的class类

> 在创建路由的实例对象时，开发者可以基于linkActiveClass属性，自定义路由链接被激活时所应用的类名



```js
import { createRouter, createWebHashHistory } from 'vue-router'

const router = createRouter({
    history: createWebHashHistory(),
    linkActiveClass: 'active-router', //自定义路由高亮的class类
    routes: [
        { test:'' , component: }
    ]
})

export default router
```



### 6.vue-cli

> [vue-cli](https://cli.vuejs.org/zh/)（俗称：vue脚手架）是vue官方提供的，快速生成vue工程化项目的工具。



特点:rocket:

- 开箱即用
- 基于webpack

- 功能丰富且易于扩展

- 支持创建vue2和vue3



可视化面板

```js
vue ui
```

命令行

```js
vue create xxx
```



### 7.组件库

> 在实际开发中，前端开发者可以把自己封装的.vue组件整理，打包，并发布为npm的包，从而供其他人下载和使用。这种可以直接下载并在项目中使用的现成组件，就叫做vue组件库。



最常用的vue组件库:book:

:one:Pc端

- [Element UI](https://element.eleme.cn/#/zh-CN)

- [View UI](http://v1.iviewui.com/)

:two:移动端

- [Mint UI](http://mint-ui.github.io/#!/zh-cn)
- [Vant](https://vant-contrib.gitee.io/vant/#/zh-CN/)



### 8.axios拦截器

> 拦截器会在每次发起ajax请求和得到响应的时候自动被触发。



#### 1.配置请求拦截器

> 通过axios.interceptors.request.use(成功的回调，失败的回调) 可以配置请求拦截器。失败的回调函数可以被省略!



```js
axios.interceptors.request.use(function(config) { retutn config; }, function(error) { return Promise.reject(error)})
```



请求拦截器Token验证

```js
import axios from 'axios'

axios.defaults.baseURL = 'https://www.escook.cn'

//配置请求的拦截器
axios.interceptors.request.use(config => {
    //为当前请求配置 Token 认证字段
    config.headers.Authorization = 'Bearer xxx'
    return config
})

Vue.prototype.$http = axios
```



请求拦截器 Loading效果

```js
import { Loading } from 'element-ui'

let loadingInstance = null

//配置请求的拦截器
axios.interceptors.request.use(config => {
    loadingInstance = Loading.service({ fullscreen: true })
    return config
})
```



#### 2.配置响应拦截器

> 通过axios.interceptors.response.use(成功的回调，失败的回调) 可以配置响应拦截器。失败的回调函数可以被省略!

```js
axios.interceptors.response.use(function(response) { retutn response; }, function(error) { return Promise.reject(error)})
```



响应拦截器关闭Loading效果

> 调用Loading实例提供的close()方法即可关闭Loading效果

```js
axios.interceptors.response.use((response) => {
    loadingInstance.close()
	retutn response; 
})
```



### 9.proxy跨域代理

> JSONP CROS  代理 [Proxy](https://webpack.docschina.org/configuration/dev-server/#devserverproxy)



![](E:\Typora笔记\images\Snipaste_2022-09-23_23-47-53.png)



### 10.Element Plus



按需导入在vue.config.js配置

```js
const AutoImport = require('unplugin-auto-import/webpack')
const Components = require('unplugin-vue-components/webpack')
const { ElementPlusResolver } = require('unplugin-vue-components/resolvers')

module.exports = defineConfig({
  configureWebpack: {
      plugins: [
        AutoImport({
          resolvers: [ElementPlusResolver()],
        }),
        Components({
          resolvers: [ElementPlusResolver()],
        }),
  	  ],
  }
)}
```







## 总结

```js
<template></template>
<script>
// 默认导出
export default {
	name: '',
	//数据源，必须是一个函数
	data() {
        return{}
	},
    //处理函数
    methods: {
        
    },
    //侦听器
    watch: {
        
    },
    //计算属性
    computed: {
        
    },
    //过滤器
    filters: {
        
    },
    //组件
    components: {
        
    },
    //自定义属性
    props: {

	},
    //自定义指令
    directives: {
        
    }
</script>
<style lang="less/css" scoped></style>//使用less语法
```



























































































