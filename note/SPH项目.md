## 项目文件结构分析

node_mudles => 项目的依赖库

public

- 放置静态资源，会原封不动的打包出来
-  index.html  favicon.ico reset.css（初始化样式）

src => assets  components  views router store api  utils  App.vue main.js

assets

- 放置全部组件共用的静态资源
- 打包的时候，放在js中了
- 用@符表示路径src，就不用/嵌套了，在js中使用`@`，在css中使用~@`

components => 放置非路由组件，放置通用模块组件(全局组件)，避免重复工作。

views/pages: 放置路由组件，只有一个页面。

router => 路由模块---》 模块化路由：把routes：[]中的路由拆分。

store => 状态管理库---》模块化仓库。

api => axios.js---》请求拦截器 响应拦截器 mock.js

utils => 工具库

App.vue => 根组件

main.js => 入口文件

.eslintignore => eslint忽略文件

.gitignore

babel.config.js => js解析文件

jsconfig.json

package.json => 包管理配置文件

README.md => 项目阅览

vue.config.js

yarn.lock



## Home



### router



**路由组件和非路由组件的区别？**

1.路由组件一般放置在pages|views文件夹中，非路由组件一般放置在components文件夹中，项目中全局组件需要放置在components文件夹中

2.路由组件一般需要在router文件夹中进行注册（使用的即为组件的名字），非路由组件在使用的时候，一般都是以标签的形式使用：导入注册以标签的形式使用

3.注册完路由，不管路由组件还是非路由组件身上都有`$route`和`$router`属性



$route：一般获取路由信息，路径，query, params等等

$router： 一般进行编程式导航进行路由跳转 push|replace|go



**路由的跳转**

编程式导航：router-link

声明式导航：push|replace|go

编程时导航：声明式导航能做的，编程式导航都能做，但是编程式导航除了可以进行路由跳转，还可以做一些其他的业务逻辑



**路由传参**

params参数：属于路径当中的一部分，需要注意，在配置路由的时候，需要占位。

query参数：不属于路径当中的一部分，类似于ajax中的queryString   /home?k=v，不需要占位



第一种：字符串形式

```js
this.$router.push('/search/' + this.keyword + '?k=' + this.keyword.toUpperCase())
```

第二种形式：模板字符串

```js
this.$router.push(`/search/${this.keyword}?k=${this.keyword.toUpperCase()}`)
```

第三种形式：对象:star:

必须在路由规则中添加name属性（命名路由）

```js
{ path: '/search/:keyword', component: Search, meta: { show: true }, name: 'search' },
```

```js
this.$router.push({ name: 'search', params: { keyword: this.keyword }, query: { k:this.keyword.toUpperCase() } })
```



### Proxy

vue.config.js

```js
 devServer: {
    proxy: {
      '/api': {
        target: 'http://gmall-h5-api.atguigu.cn'
      },
    },
  }
```



### nprogress

```js
yarn add nprogress;
```

```js
import nprogress from 'nprogress'
import 'nprogress/nprogress.css'
```

可以在node_modules中改变进度条颜色

在请求拦截器中配置`nprogress.start()`

在响应拦截器中配置`nprogress.done()`

 

### vuex

- 项目中vuex的版本不要过高，请使用3.6.2

- this.$store可以拿到所有小仓库
- vuex仓库存储数据，不是持久化的---》本地存储localStroage
- 切记：仓库当中的state的数据格式，不能瞎写，胡写，乱写，数据格式取决于服务器返回的数据。



context小仓库

- commit提交mutations修改state

- dispatch派发actions
- getter计算属性，简化数据
- state当前仓库数据



### 防抖和节流

节流：在规定的间隔时间范围内不会重复触发回调，只有大于这个时间间隔才会触发回调，把频繁触发变为少量触发

 `_.throttle(func, [wait=0], [options=])`

防抖： 前面的所有的触发都被取消，最后一次执行在规定的时间之后才会触发，也就是说如果连续快速的触发，只会执行一次  

`_.debounce(func, [wait=0], [options=])`



lodash插件：里面封装函数的防抖与节流的业务（闭包+延迟器）



过渡动画：前提组件|元素务必要有v-if|v-show指令才可以进行过渡动画



App.vue组件的mounted只会触发一次，不能放在main.js中，main.js不是一个组件，main.js中的this是undefined。

```js
this.$store.dispatch('categoryList')
```



### mock

1.在src目录下新建mock文件夹

2.准备json数据（mock文件夹中创建相应的JSON文件）--- 格式化一下，别留有空格（要不然跑不起来的）

3.把mock数据需要的图片放置在public文件夹中，（public文件夹在打包的时候，会把相应的资源原封不动打包到dist文件夹中）

4.创建mockServe.js通过mockjs插件实现虚拟数据

5.mockServe.js文件在入口文件中引入（至少需要执行一次，才能模拟数据）



### swiper

```js
yarn add swiper@5.4.5
```

1.引入相应的依赖包 swiper.js| swiper.css（组件中多个地方要用到所有在入口文件main.js中引入）

2.页面中的结构务必要有

3.初始化swiper实例，给轮播图添加动态效果

4.ref拿到dom   `this.refs.定义的ref属性`

:warning:最完美的解决方案，解决轮播图问题 watch + $nextTick

```js
watch: {
    skuImageList() {
      this.$nextTick(() => {
        new Swiper(this.$refs.cur, {
          // 如果需要前进后退按钮
          navigation: {
            nextEl: '.swiper-button-next',
            prevEl: '.swiper-button-prev'
          }
        })
      })
    }
  }
```



### floor组件

getFloorList这个action在哪里触发？

> 不能在floor组件中派发action，因为我们需要v-for遍历floor组件。
>
> 需要在Home路由组件index.vue中派发。



v-for也可以在自定义标签中使用



**组件通信的方式有哪些？面试频率极高**

props：用于父子组件通信

自定义事件：@on @emit 可以实现子给父通信

全局事件总线：$bus 全能

pubsub-js：vue当中几乎不用，全能

插槽：默认插槽，具名插槽，作用域插槽

vuex



第一次书写轮播图的时候，在当前组件的内部发送请求，动态渲染结构，前台至少服务器数据需要回来，而这个的请求实在home组件中发请求，floor组件的数据是父组件home给的，他在内部不需要发请求。请求是父组件发的，父组件通过props传递过来的，而且结构都已经有了的情况下执行mounted



把首页轮播图拆分为一个公用的全局组件。

切记：以后在开发项目的时候，如果看到某一个组件在很多地方都使用，你把它注册成全局组件，注册一次，可以在任意地方使用，共用的组件和非路由组件放到components文件夹中。



## Search

1.写静态页面 + 静态组件拆分出来

2.发请求（API）

3.vuex（三连环）

4.组件获取仓库数据，动态展示数据



getters在项目中，主要作用为了简化仓库中的数据而生。可以把我们将来在组件中需要用的数据简化一下，将来组件在获取数据的时候就会很方便。使用：相当于计算属性，定义成一个方法，要有return。

```js
const getters = {
  // state形参就是当前仓库state
  goodsList(state) {
    // state.searchList.goodsList如果服务器数据回来了，没问题是一个数组
    // 假如网络不给力|没有网state.searchList.goodsList应该返回的是undefined
    return state.searchList.goodsList||[];
  },
  trademarkList(state) {
    return state.searchList.trademarkList||[];
  },
  attrsList(state) {
    return state.searchList.attrsList||[];
  }
}
```



如何在组件上拿到getters的值？

```js
import {mapGetters} from 'vuex'

computed: {
    ...mapGetters(['trademarkList','attrsList'])
}

```





全局事件总线：$bus 全能

main.js

```js
new Vue({
  render: h => h(App),
  // 全局事件总线
  beforeCreate() {
    Vue.prototype.$bus = this
  },
  router,
  store
}).$mount('#app')
```



兄弟组件1

```js
// 通知兄弟组件header清除关键字
      this.$bus.$emit('clear')
```



兄弟组件2

```js
  mounted() {
    // 通过全局事件总线清除关键字
    this.$bus.$on('clear', () => {
      this.keyword = ''
    })
  }
```





阿里图标库的应用

1.找到自己想要的图标

2.加入购物车

3.创建一个项目

4.生成在线链接

5.在public文件夹中index.html引入即可，注意协议为https





### 分页器

1.分页功能实现

为什么很多项目采用分页功能：比如电商平台同时展示的数据有很多（1万+），采用分页功能。

ElementUI是有相应的分页组件，使用起来超级简单，但是咱们前台项目目前不用，掌握自定义分页功能。



2.分页器展示，需要哪些数据（条件）？

需要知道当前是第几页：**pageNo**字段代表当前页数，在连续的页码数中间。

需要知道每一页需要展示多少条数据：**pageSize**字段进行代表

需要知道整个分页器一共有多少条数据：**total**字段进行代表 ---- 》 获取另外一条信息：一共多少页 **totalPage** = total/pageSize

需要知道分页器连续的页码个数：**continues** ----》5|7（奇数，对称好看），暗含的条件分页器至少是5|7页，不正常现象: 总页数没有连续页码多。



总结：对于分页器而言，自定义前提是需要知道四个前提条件。



自定义分页器，在开发的时候先自己传递假的数据进行调试，调试成功以后在用服务器数据。

对于分页器而言，很重要的一个地方即为，算出：连续页面起始数字和结束数字



## detail

1.静态组件（详情页的组件：还没有注册为路由组件）

当点击商品的图片的时候，跳转到详情页面，在路由跳转的时候需要带上产品的ID给详情页面

滚动行为



2.API---->请求接口



3.vuex---->获取产品详情信息

vuex中还需要在新增一个模块detail

需要回到大仓库中进行合并

vuex3连环，派发actions





**全局事件总线`$vus`**

**兄弟组件之间的通信**



入口文件main.js

```js
new Vue({
  render: h => h(App),
  // 全局事件总线
  beforeCreate() {
    Vue.prototype.$bus = this
  },
  router,
  store
}).$mount('#app')
```



发送方

```js
  methods: {
    changeCurrentIndex(index) {
      this.currentIndex = index;
      this.$bus.$emit('getIndex', this.currentIndex)
    }
  }
```



接收方

```js
    mounted() {
      // 全局事件总线：获取兄弟组件传递过来的索引值
      this.$bus.$on('getIndex', (index) => {
        console.log(index);
      })
    }
```



放大镜



加入购物车

**UUID**：点击加入购物车的时候，通过请求头给服务器带临时身份给服务器，存储某一个用户购物车数据

会话存储、去存储产品的信息一级展示功能



**本地存储和会话存储**



## shopcart



### 修改产品的数量

- 节流





### 删除某一个产品的接口





### 产品勾选状态的切换

接口api

- 接口方法大小写都可以
- 模板字符串
- 对象的形式

```js
export const reqUpdareCheckedById = (skuId,isChecked) => requests({url: `/cart/checkCart/${skuId}/${isChecked}`, method: 'get'})
```

```js
export const reqUpdareCheckedById = (skuId,isChecked) => requests({url: `/cart/checkCart/${skuId}/${isChecked}`, method: 'GET'})
```



仓库store

- 在actions接收的参数中，如果是多个应该用对象接收

```js
async updateCheckedById({commit}, {skuId,isChecked}) {
    let result = await reqUpdareCheckedById(skuId, isChecked);
    if(result.code == 200) {
      return 'ok';
    } else {
      return Promise.reject(new Error('faile'));
    }
  }
```



派发actions

> 点击复选框触发此方法，派发actions，修改购物车数据，重新发送请求获取新的数据。

```js
// 修改某一个产品的勾选状态
    async updateChecked(cart,event) {
      try {
        // 带给服务器的参数isChecked，不是布尔值，应该是0|1
        // 如果修改数据成功，再次获取购物车数据
        let isChecked = event.target.checked ? "1" : "0";
        await this.$store.dispatch('updateCheckedById', {skuId: cart.skuId, isChecked});
        this.getData();
      } catch (error) {
        alert(error.message);
      }
    }
```





## Promise

Promise.all([p1,p2,p3])
p1|p2|p3: 每一个都是Promise对象，如果有一个Promise失败，都失败，如果都成功，返回成功。

返回promise对象，要么成功要么失败。



接收异常捕获

```js
try {
    await this.$store.dispath('');
} catch(error) {
    return error.message;
}

Promise.reject(new Error('faile'));
```





## 登录注册



### 注册(register)

1.手机号码和验证码都需要收集，`v-model`双向数据绑定

2.获取验证码的接口：

> 获取验证码的这个接口：把验证码返回，但是正常情况，后台把验证码发到用户手机上，而不是成功的示例上。

- url：/api/user/passport/sendCode/{phone}   

- method: get

- 参数:

  | 参数名称 | 类型   | 是否必选 | 描述       |
  | -------- | ------ | -------- | ---------- |
  | phone    | string | Y        | 注册手机号 |

- api

  ```js
  export const reqGetCode = (phone) => requests({url:`/user/passport/sendCode/${phone}`, method: 'get'});
  ```

  

3.注册用户接口：

- url：/api/user/passport/register

- method: post

- 参数：

  | 参数名称 | 类型   | 是否必选 | 描述       |
  | -------- | ------ | -------- | ---------- |
  | phone    | string | Y        | 注册手机号 |
  | password | string | Y        | 密码       |
  | code     | string | Y        | 验证码     |
  | nickName | string | N        | 别名       |

- api

  ```js
  export const reqUserRegister = (data) => requests({url: '/user/passport/register', data, method: 'post'});
  ```

  

### 登录(login)

- 注册---通过数据库存储用户信息（名字、密码）
- 登录---登录成功的时候，后台为了区分你这个用户是谁-服务器下发tokn【令牌：唯一标识符】
- 登录接口：做的不完美，一般登录成功服务器会下发token,前台持久化存储token,【带着token找服务器要用户信息进行展示】



1.登录接口：

- url：/api/user/passport/login

- method: post

- 参数:

  | 参数名称 | 类型   | 是否必选 | 描述   |
  | -------- | ------ | -------- | ------ |
  | phone    | string | Y        | 用户名 |
  | password | string | Y        | 密码   |

- api

  ```js
  export const reqUserLogin = (data) => requests({url: '/user/passport/login', data, method: 'post'});
  ```

  

**1.登录过后首页用户信息的展示**

1.1当用户注册完成，用户登录【用户名+密码】向服务器发请求（组件派发action:userLogin)
登录成功获取到token，仓储与仓库当中（非持久化），路由跳转跳转到home首页。

登录成功---》Heaher组件显示用户名与退出登录

1.2因此在首页当中(mounted)派发action(getUserInfo)获取用户信息，一级动态展示header组件内容。

1.3一刷新home首页，获取不到用户信息(token：vuex非持久化存储)

1.4.持久化存储token---》本地存储

1.5存在问题1，多个组件展示用户信息需要在每一个组件的mounted中派发this.$store.dispatch('getUserInfo');  繁琐---》此方案不行

1.6存在问题2，用户已经登陆了，就不能在跳转回登录页和注册页。---》导航守卫



### 退出登录(logout)

退出登录接口：

- /api/user/passport/logout 
- mthod: get

```js
export const reqLogout = () => requests({url: '/user/passport/logout', method: 'get'});
```



2.1需要发请求，通知服务器退出登录，清除一些数据：token

2.2清除项目中的数据：userInfo，token

2.3退出登录成功，跳转回到home首页



### 导航守卫

- 全局守卫
- 路由独享守卫
- 组件内守卫



全局守卫

> 执行的时间不同

- 全局前置守卫:star:
- 全局解析守卫
- 全局后置钩子



## trade



**获取用户地址信息接口**

> 用户登录了才可以获取用户地址信息

```js
// 获取用户地址信息
export const reqAddressInfo = () => requests({url: '/user/userAddress/auth/findUserAddressList', method: 'get'});
```



**从仓库中获取数据给组件**

```js
import { mapState } from 'vuex';
```

```js
computed: {
    ...mapState({
        addressInfo: state => state.trade.address
    })
}
```



**获取商品清单接口**

```js
// 获取商品清单
export const reqOrderInfo = () => requests({url: '/order/auth/trade', method: 'get'});
```



修改默认地址，**排他思想**

```js
<div class="address clearFix" v-for="item in addressInfo" :key="item.id">
    <span class="username" :class="{'selected':item.isDefault == 1}">{{item.consignee}}</span>
	<p @click="changeDefault(item, addressInfo)">
        <span class="s1">{{item.fullAddress}}</span>
		<span class="s2">{{item.phoneNum}}</span>
		<span class="s3" v-show="item.isDefault == 1">默认地址</span>
	</p>
</div>
```

```js
methods: {
  // 修改默认地址
  changeDefault(item, addressInfo) {
   addressInfo.forEach(item => item.isDefault = 0);
   item.isDefault = 1;
  }
 }
```





## pay



2)提交订单

2.1先把支付静态组件先搞定

2.2点击提交订单的按钮的时候，还需要向服务器发起一次请求【把支付一些信息传递给服务器】

2.3不使用vuex，数据存储在组件中data

```js
export default {
  name: 'MyPay',
  data() {
    return {
      payInfo: {}
    }
  },
  computed: {
    orderId() {
      return this.$route.query.orderId;
    }
  },
  // 尽量别再生命周期中写async|await
  mounted() {
    this.getPayInfo();
  },
  methods: {
    async getPayInfo() {
      let result = await this.$API.reqPayInfo(this.orderId);
      // 如果成功：组件中存储支付信息
      if(result.code == 200) {
        this.payInfo = result.data;
      }
    }
  }
}
```



/api/order/auth/submitOrder?tradeNo={tradeNo}











## 后台管理系统

> 不用vuex





























