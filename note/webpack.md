### 1. 为什么需要打包工具？

> 开发时，我们会使用框架（React, Vue），Es6 模块化语法，Less/Sass 等Css预处理器等语法进行开发。这样的代码要想在浏览运行必须经过编译成浏览器能识别的 JS, Css 等语法，才能运行。所以我们需要打包工具帮我们做完这些事，除此之外，打包工具还能==压缩代码，做兼容性处理，提升代码性能==等。



### 2.前端工程化的相关概念



前端开发4个现代化：

- 模块化（js的模块化，css的模块化，资源的模块化）
- 组件化（复用现有的UI结构，样式，行为） 
- 规范化（目录结构的划分，编码规范化，接口规范化，文档规范化，Git分支管理）
- 自动化（自动化构建，自动部署，自动化测试）



前端工程化的好处: 

- 前端工程化让前端开发能够==自成体系==，覆盖了前端项目从创建到部署的方方面面
- 最大程度地提高了前端的开发效率，降低了技术选型，前后端联调等带来的协调沟通成本



早期的前端工程化解决方案：

- [grunt](https://www.gruntjs.net/) :recycle:
- [gulp](https://www.gulpjs.com.cn/) :recycle:



目前主流的前端工程化解决方案：

- [webpack](https://www.webpackjs.com/) :star2:
- [parcel ](https://zh.parceljs.org/) :star:



### 3.webpack基本概念

> webpack是一种前端资源构建工具，一个静态模块打包器(module bundler)。



### 4.webpack的基本使用



#### 2.1安装与配置

webpack的安装

```js
npm install webpack webpack-cli -D/--save-dev;
```



配置webpack



:one:在项目根目录中，创建名为==webpack.config.js==的webpack配置文件

mode节点的可选值有两个，分别是：

1. **development**

- ==开发环境==
- 不会对打包的文件进行代码压缩和性能优化
- 打包速度快，适合在开发阶段使用



2. **production**

- ==生产环境==
- 会对打包生成的文件进行代码压缩和性能优化
- 打包速度很慢，仅适合在项目发布阶段使用



```js
module.exports = {
    mode: 'development' //production
}
```



:two:在package.json的scripts节点下，新增dev脚本

```js
"scripts": {
    "serve": "webpack --mode=development --watch", //--watch监听代码变化重新编译
    "build": "webpack --mode=production"
}
```



:three:在终端中运行，启动webpack进行项目的打包构建

```js
npm run dev
```



#### 2.2自定义打包入口与出口



在webpack中有如下的默认约定：

> 默认的打包入口文件为 src -> index.js
>
> 默认的输出文件路径为 dist -> main.js



在webpack.config.js配置文件中，通过==entry节点==指定打包的入口。通过==output节点==指定打包的出口。

```js
const path = require('path')

module.exports = {
    entry: '', //打包入口文件的路径，绝对路径和相对路径都可以
    output: {
    	path: path.resolve(__dirname, 'dist'), //打包后输出文件的存放路径，必须是绝对路径
        filename: 'static/js/bundle.js' //输出文件的名称
	}
}
```



### 5.plugins插件



1.webpack-dev-server

- 类似于Node.js阶段用到的nodemon工具
- 每当修改了源代码,webpack会自动进行项目的打包和构建



2.html-webpack-plugin

- webpack中的HTML插件（类似于一个模板引擎插件）
- 可以通过此插件自定制index.html页面的内容



#### 3.1html-webpack-plugin

> 自动引入打包输出的资源



html-webpack-plugin的安装

```js
npm install html-webpack-plugin -D
```



```js
const HtmlPlugin = require('html-webpack-plugin')

module.exports = {
    plugins: [
       new HtmlPlugin({
       		template: path.resolve(__dirname, '../src/assets/index.html')
	   })
    ], //挂载插件实例对象
}
```



#### 3.2 webpack-dev-server

> 为了解决每次写完代码需要手动输入指令才能编译代码，所有我们希望一切自动化。
>
> 开发服务器：不会输出资源，在内存中编译打包。



1.webpack-dev-server的安装

```js
npm install webpack-dev-server -D
```



2.修改package.json的scripts节点中的dev命令

```js
"scripts": {
    "dev": "webpack serve"
}
```



3.在devServer节点中配置

```js
devServer: {
    host: '127.0.0.1', //实时打包所使用的主机地址localhost
    port: 80, //实时打包所使用的端口号
    open: true, //初次打包完成后，自动打开浏览器
}
```



### 6.loader加载器



> webpack 只能理解 JavaScript 和 JSON 文件，这是 webpack 开箱可用的自带能力。**loader** 让 webpack 能够去处理其他类型的文件，并将它们转换为有效 [模块](https://webpack.docschina.org/concepts/modules)，以供应用程序使用，以及被添加到依赖图中。



<img src="E:\Typora笔记\images\屏幕截图 2022-09-17 155515.png" style="zoom: 80%;" />



#### 4.1 处理css资源



安装处理css文件的loader模块

```js
npm i style-loader css-loader -D;
```



在webpack.config.js的module ,rules数组中，添加loader规则

> :warning: use数组中指定的loader顺序是固定的，多个loader的调用顺序是从右到左解析原则

```js
module: {
    // 所有第三方文件模块的匹配规则
    rules: [
        {test: /\.css$/, use: ['style-loader', 'css-loader']} //文件后缀名的匹配规则，定义不同模块对应的loader
    ]
}
```



#### 4.2处理less资源

```js
npm i less-loader less -D; //less@4.1.1属于内置依赖
```

```js
{test: /\.less$/, use: ['style-loader', 'css-loader', 'less-loader']}
```



#### 4.3处理Sass资源

```js
npm i sass-loader sass -D;
```

```js
{ test: /\.s[ac]ss$/, use: ['style-loader', 'css-loader', 'sass-loader'] }
```



#### 4.4处理Stylus资源

```js
npm install stylus stylus-loader -D;
```

```js
{ test: /\.styl$/, use: ['style-loader', 'css-loader', 'stylus-loader'] }
```



#### 4.5 处理图片资源

> 过去在Webpack4，我们处理图片资源通过`file-loader`和`url-loader`进行处理，现在在Webpack5已经将两个Loader功能内置到了Webpack里了，我们只需要简单配置即可处理图片资源。



**Webpack4的方法**

打包处理样式表中与URL路径相关的文件的loader模块

```js
npm i url-loader file-loader -D; 
```



在webpack.config.js的module ,rules数组中，添加loader规则

```js
module: {
    // 所有第三方文件模块的匹配规则
    rules: [
        {test: /\.jpg|png|gif$/, use: 'url-loader?limit=22229'} // 单个loader数组可以省略
    ]
}
// limi用来指定图片大小，单位是字节（byte）
// 只有<=limit大小的图片，才会被转为base64格式的图片
use: {
    loader: 'url-loader',
    options: {
        limit: 22229
    }
}
```



**Webpack5的方法**

> hash图片名字哈希；ext后缀名；query查询字符串参数

```js
{ 
    test: /\.(png|jpe?g|gif|svg|webp)$/, 
    type: 'asset', //会转换为base64
    parser: {
         dataUrlCondition: {
           maxSize: 10 * 1024 // 小于10kb的图片转base64，减少请求数量，体积会更大
         }
    },
  	generator: {
         filename: 'static/images/[hash:10][ext][query]' //输出图片的名字
    }
}
```



#### 4.6处理字体图标资源

```js
{ 
    test: /\.(ttf|woff2)$/, 
    type: 'asset/resource', //原封不动的输出
  	generator: {
         filename: 'static/media/[hash:10][ext][query]' //输出图片的名字
    }
}
```



#### 4.7处理其他资源

> 处理音频视频等其他资源

```js
{ 
    test: /\.(ttf|woff2|map|map4|avi)$/, //往后加即可
    type: 'asset/resource', //原封不动的输出
  	generator: {
         filename: 'static/media/[hash:10][ext][query]' //输出图片的名字
    }
}
```



#### 4.8Eslint

安装依赖

```js
npm install eslint-webpack-plugin eslint --save-dev
```



webpack.config.json配置

```js
const ESLintPlugin = require('eslint-webpack-plugin');

module.exports = {
  // ...
  plugins: [new ESLintPlugin({
      context: path.resolve(__dirname, 'src')
  })],
  // ...
};
```



在项目根目录下新建`.eslintrc.js`

```js
module.exports = {
    extends: ['eslint: recommended'], //继承 Eslint 规则
    env: {
        node: true, // 启用node中全局变量
        browser: true //启用浏览器中全局变量
    },
    parserOptions: {
        ecmaVersion: 6, // es6
        sourceType: 'module' // es module
    },
    rules: {
        'no-var': 2, //不能使用var定义变量
    }
}
```



#### 4.9 处理js资源

> Webpack对js处理是有限的，只能编译js中ES模块化语法，不能编译他其语法，导致js不能在IE等浏览器运行，所有我们希望做一些兼容性处理。



> 其次在开发中，团队对代码格式是有严格要求的，我们不能由肉眼去检测代码格式，需要使用专业的工具来检测。我们先完成ESlint，检测代码格式无误后，再由babel做代码兼容性处理。



:one:针对js兼容性处理，我们使用babel来完成

:two:针对代码格式，我们使用Eslint来完成



```js
npm i babel-loader @babel/core @babel/preset-env -D
```



在webpack.config.js的module ,rules数组中，添加loader规则

```js
// 注意：必须使用exclude指定排除项，因为node_modules 目录下的第三方包不需要被打包
{ test: /\.js$/, 
  exclude: /node_modules/, 
  use: {
      loader: 'babel-loader', 
      options: {
          plugins: ['@babel/plugin-proposal-class-properties']
      }
  }
}
```



#### 4.10处理html资源

> 自动引入打包后输出的资源



```js
npm install --save-dev html-webpack-plugin
```



```js
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
  // ...
  plugins: [new HtmlWebpackPlugin({
    template: './src/index.html', //指定要复制哪个文件
    filename: './index.html', //指定生成的文件的存放路径
  })],
  // ...
};
```



### 7.Eslint

> 可组装的JavaScript和JSX检查工具



#### 7.1配置文件

>  .eslinttrc.js



#### 7.2具体配置

```js
module.exports = {
  root: true,
  env: {
    node: true,
    browser: true
  },
  extends: [
    'eslint:recommended'
  ],
  parserOptions: {
    ecmaVersion: 6,
    sourceType: 'module'
  },
  rules: {
    'space-before-function-paren': 0,
    'no-var': 2
  }
}
```



#### 7.3在webpack中使用



```js
npm install eslint-webpack-plugin eslint -D
```



```js
const ESLintPlugin = require('eslint-webpack-plugin');

module.exports = {
  // ...
  plugins: [new ESLintPlugin({
      context: path.resolve(__dirname, 'src')
  })],
  // ...
};
```



#### 7.3eslintignore忽略文件

>  .eslintignore

```js
dist
```



#### 7.4在vue项目中关闭eslint

在vue.config.js文件中

```js
module.exports = {
    lintOnSave: false
}
```



### 8.生产与开发模式的配置



>  在根目录中创建config文件夹，添加2个环境的配置文件，webpack.dev.js webpack.prod.js



#### 8.1配置命令

在package.json文件scripts节点中，配置buil命令

```js
"scripts": {
    "dev": "webpack server --config ./config/webpack.dev.js", //开发环境 npm run dev
    "build": "webpack --config ./config/webpack.prod.js" //项目发布打包 npm run build
}
```



#### 8.2开发环境

webpack.dev.js

```js
const path = require('path')
const { VueLoaderPlugin } = require('vue-loader')
const HtmlWebpackPlugin = require('html-webpack-plugin')

module.exports = {
    mode: 'development',
	entry: './src/main.js',
    output: {
    	path: undefined, // 开发环境不需要输出
    	filename: 'static/js/bundle.js'
	},
	module: {
        rules: [
            { test: /\.vue$/, use: 'vue-loader' },
            { test: /\.css$/, use: ['style-loader', 'css-loader'] },
            { test: /\.s[ac]ss$/, use: ['style-loader', 'css-loader', 'sass-loader'] },
            { 
              test: /\.(png|jpe?g|gif|svg|webp)$/,
              type: 'asset',
              parser: {
                  dataUrlCondition: {
                      maxSize: 10 * 1024 // 小于10kb的图片转base64，减少请求数量，体积会更大
                  }
              },
              generator: {
                  filename: 'static/images/[hash:10][ext][query]'
              }
            },
            {
              test: /.\(ttf|woff2)$/,
              type: 'asset/resource',
              generator: {
                  filename: 'static/media/[hash:10][ext][query]'
			  }
            }
            { 
              test: /\.js$/, 
              exclude: /node_modules/, //排除node_modules中的js文件
  	          use: {
      	        loader: 'babel-loader', 
                //配置babel-loader
      	        options: {
                     presets: ['@babel/preset-env'] //智能预设
      			}
  	  		   }
		     }
         ]
    },
    plugins: [
        new VueLoaderPlugin(), 
        new HtmlWebpackPlugin({
    		template: path.resolve(__dirname, '../pulic/index.html')
  		})
    ],
	devServer: {
        host: 'localhost',
        port: '3000',
        open: true
    },
    devtool: 'eval-source-map'
}
```



#### 8.3生成环境



:link:[提取Css成单独文件](https://webpack.docschina.org/plugins/mini-css-extract-plugin/)

> 提取Css成单独文件，解决网速慢，页面先解析Js，导致内容展示闪屏的问题。



```js
npm install --save-dev mini-css-extract-plugin
```



样式兼容性处理

```js
npm i postcss-loader postcss postcss-preset-env -D
```



在package.json加入节点

```js
"browserslist": [
    "ie >= 8"
]
```



实际开发中配置一般如下：

```js
"browserslist": [
    "last 2 version", //所有浏览器只用最近的2个版本
    "> 1%", //覆盖百分之99的浏览器
    "not dead" //有些浏览器开发过程中有些版本已经死了
]
```



:link:[css压缩](https://webpack.docschina.org/plugins/css-minimizer-webpack-plugin/)

```js
npm install css-minimizer-webpack-plugin --save-dev
```



```js
const path = require('path')
const { VueLoaderPlugin } = require('vue-loader')
const HtmlWebpackPlugin = require('html-webpack-plugin')
const MiniCssExtractPlugin = require("mini-css-extract-plugin");
const CssMinimizerPlugin = require("css-minimizer-webpack-plugin");

// 用来获取处理样式的Loader,在css之后less/sass之前添加兼容性处理
function getStyleLoader(pre) {
    return [
       MiniCssExtractPlugin.loader,//需要把所有style-loader修改
       'css-loader',
       {
         loader: 'postcss-loader',
         options: {
             postcssOptions: {
               plugins: [
                     'postcss-preset-env'
               ]
            }
         }
       },
       pre
    ].filter(Boolean)
}

module.exports = {
    mode: 'production', 
	entry: './src/main.js',
    output: {
    	path: path.resolve(__dirname, '../dist'), //绝对路径，__dirname是一个node变量
    	filename: 'static/js/bundle.js',
        clean: true //自动清空上次打包的内容
	},
	module: {
        rules: [
            { test: /\.vue$/, use: 'vue-loader' },
            { 
              test: /\.css$/,
              use: getStyleLoader()
            }, 
            { 
              test: /\.s[ac]ss$/,
              use: getStyleLoader('sass-loader')
            },
            { 
              test: /\.(png|jpe?g|gif|svg|webp)$/,
              type: 'asset',
              parser: {
                  dataUrlCondition: {
                      maxSize: 10 * 1024 // 小于10kb的图片转base64，减少请求数量，体积会更大
                  }
              },
              generator: {
                  filename: 'static/images/[hash:10][ext][query]'
              }
            },
            {
              test: /.\(ttf|woff2)$/,
              type: 'asset/resource',
              generator: {
                  filename: 'static/media/[hash:10][ext][query]'
			  }
            }
            { 
              test: /\.js$/, 
              exclude: /node_modules/, //排除node_modules中的js文件
      	      loader: 'babel-loader', 
      	      options: {
                   presets: ['@babel/preset-env'] //智能预设
      		  }
		    }
         ]
    },    
    plugins: [
        new VueLoaderPlugin(), 
        new HtmlWebpackPlugin({
    		template: path.resolve(__dirname, '../pulic/index.html')
  		}),
        new MiniCssExtractPlugin({
            filename: 'static/css/index.css'
        }),
        new CssMinimizerPlugin()
    ], //每一个插件的构造函数的实例
    devtool: 'nosources-source-map'
}
```



### 9.Webpack高级

> 所谓高级配置其实就是进行Webpack优化，让我们代码在编译/运行时性能更好

- 提升开发体验
- 提升打包构建速度
- 减少代码体积
- 优化代码运行性能



#### 9.1Source Map

> Source Map就是一个信息文件，里面存储着位置信息。也就是说，Source Map 文件中存储着压缩混淆后的代码，所对应的转换前的位置。有了它，出错的时候，除错工具将直接显示原始代码，而不是转换后的代码，能够极大的方便后期的调试。
>



##### 9.1.1开发环境

> 开发环境下默认生成的Source Map，记录的是生成后的代码的位置。会导致运行时报错的行数与源代码的行数不一致的问题。



开发环境下,推荐在webpack.config.js中添加如下的配置，即可保证运行时报错的行数与源代码的行数保持一致：

```js
module.exports = {
    mode: 'development',
    devtool: 'eval-source-map'
}
```



##### 9..1.2生产环境

在生产环境下，如果省略了devtool选项，则最终生成的文件中不包含Source Map。这能够防止原始代码通过Source Map 的形式暴露给别有所图之人。



**只定位行数不暴露源码**

在生产环境下，如果只想定位报错的具体行数，且不想暴漏源码。此时可以将devtool的值设置为nosources-source-map。

```js
module.exports = {
    mode: 'production',
    devtool: 'nosources-source-map'
}
```



##### Source Map 的最佳实践

1.开发环境下：

- 建议把devtool的值设置为eval-source-map
- 好处：可以精准定位到具体的错误行

2.生产环境下：

- 建议关闭 Source Map 或将devtool的值设置为nosources-source-map
- 好处：防止源码泄露，提高网站的安全性



#### 9.2HMR



为什么？

> 开发时问我们修改了其中一个模块代码，Webpack默认会将所有模块全部重新打包编译，速度很慢。所以我们需要做到修改某个模块代码，就只有这个模块代码需要重新打包编译，其他模块不变，这样打包速度就会变快。



是什么？

> HotModuleReplacement ( 热模块替换 )：在程序运行中，替换，添加或删除模块，而无需重新加载整个页面。



怎么用？

```js
devServer: {
    host: '127.0.0.1', //实时打包所使用的主机地址localhost
    port: 80, //实时打包所使用的端口号
    open: true, //初次打包完成后，自动打开浏览器
    hot: true //开启HMR,默认开启,只能在开发环境下用
}
```



#### 9.3OneOf



为什么？

> 打包是每个文件都会经过所有loader处理，虽然因为test正则原因实际没有处理上，但是都要过一遍，比较慢。



是什么？

> 顾名思义就是只能匹配上一个loader，剩下的就不匹配了。



怎么用？

```js
module: {
    rules: [
        {
          oneof: [
              {},
              {},
              {}
          ]
        }
    ]
}
```



#### 9.4Include-Exclude

> 只针对js文件处理



为什么？

> 开发时我们我们需要使用第三方的库或插件，所有文件都下载到node_modules中了。而这些文件是不需要编译可以直接使用。所以我们在对js文件处理时，要排除node_modules下面的文件



是什么？

- include

包含，只处理xxx文件

- exclude

排除，除了xxx文件以外其他文件都处理



#### 9.5Cache-缓存



为什么？

> 每次打包，时js文件都要经过Eslint检查和Babel编译，速度比较慢。
> 我们可以缓存之前的Eslint检查和Babel编译结果，这样==第二次打包时速度就会更快了==。



是什么？

> 对Eslint检查和Babel编译结果进行缓存。



怎么做？

```js
{ 
    test: /\.js$/, 
    exclude: /node_modules/, //排除node_modules中的js文件
    loader: 'babel-loader', 
    options: {
        presets: ['@babel/preset-env'] //智能预设,
        cacheDirectory: true, // 开启babel缓存
        cacheCompression: false, // 关闭缓存文件压缩
    }
}
```



plugin的配置

```js
new ESLintPlugin({
    context: path.resolve(__dirname, "../src"), // 检测哪些文件
    exclude: "node_modules", // 默认值
    cache: true, // 开启缓存
    cacheLocation: path.resolbe(__dirname, '../node_modules/.cache/eslintcache')
})
```



#### 9.6Thead-多线程打包





#### 9.7Tree Shaking-减少代码体积



为什么？

> 开发时我们定义了一些工具函数库，或者引用第三方工具函数库或组件库。
> 如果没有特殊处理的话我们打包时会引入整个库，但是实际上可能我们可能只用上极小部分的功能。
> 这样将整个库都打包进来，体积就太大了。



是什么？

> Tree Shaking是一个术语，通常用于描述移除JavaScript中的没有使用上的代码。



怎么做？

> Webpack已经默认开启了这个功能，无需其他配置。



#### 9.8减少Babel生成文件的体积





#### 9.9压缩图片



为什么？

> 开发如果项目中引用了较多图片，那么图片体积会比较大，将来请求速度比较慢。
> 我们可以对图片进行压缩，减少图片体积。
>
> 注意：如果项目中图片都是在线链接，那么就不需要了。本地项目静态图片才需要进行压缩。



是什么？

> image-minigizer-webpack-.plugin:用来压缩图片的插件



怎么做？

> 



#### 10.0CodeSplit-多入口





#### 10.1CodeSplit-多入口提取公共模块





#### 10.2CodeSplit-多入口按需加载





#### 10.3CodeSplit-单入口





#### 10.4CodeSplit-给模块命名





#### 10.5CodeSplit-统一命名





#### 10.6Preload和Prefetch





#### 10.7Network Cache





#### 10.8解决js兼容性问题CoreJS





#### 10.9PWA



























### 10.用@表示路径

@表示src源代码目录，从外往里查找，不要使用 ../ 从里往外找

```js
resolve: {
    alias: {
        '@': path.join(__dirname, './src/'); //告诉webpack，@符号代表src这一层目录
    }
}
```



@路径提示

```js
"path-autocomplete.extensionOnImport": true,
"path-autocomplete.pathMappings": {"@": "${folder}/src"}
```



### 11.依赖

> 项目依赖：vue



> 开发依赖：webpack webpack-cli vue-loader vue-template-compiler sass-loader sass css-loader style-loader babel-loader @babel/core @babel/preset-env mini-css-extract-plugin postcss-loader postcss postcss-preset-env css-minimizer-webpack-plugin





































