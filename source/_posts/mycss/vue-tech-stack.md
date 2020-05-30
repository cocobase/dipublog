---
title: vue前端技术栈
date: 2020-03-20 17:39:36
tags: vue
keywords: vue
---

## Vue.js技术栈
* npm：node.js的包管理工具，用于同一管理我们前端项目中需要用到的包、插件、工具、命令等，便于开发和维护。
* ES6：Javascript的新版本，ECMAScript6的简称。利用ES6我们可以简化我们的JS代码，同时利用其提供的强大功能来快速实现JS逻辑。
* Babel：一款将ES6代码转化为浏览器兼容的ES5代码的插件
* vue-cli：Vue的脚手架工具，用于自动生成Vue项目的目录及文件。
* vue-router： Vue提供的前端路由工具，利用其我们实现页面的路由控制，局部刷新及按需加载，构建单页应用，实现前后端分离。
* vuex：Vue提供的状态管理工具，用于同一管理我们项目中各种数据的交互和重用，存储我们需要用到数据对象。
* webpack：一款强大的文件打包工具，可以将我们的前端项目文件同一打包压缩至js中，并且可以通过vue-loader等加载器实现语法转化与加载。

<!--more-->

## Node.js
node.js是对Chrome V8引擎进行了封装，是一个能让JavaScript运行在服务端的开发平台，它让JavaScript成为与PHP、Python、Perl、Ruby等服务端语言平起平坐的脚本语言。作为异步驱动的 JavaScript 运行时，Node.js 被设计成可升级的网络应用。Node 中几乎没有函数直接执行 I/O 操作，因此进程从不阻塞。由于没有任何阻塞，可伸缩系统在 Node 中开发是非常合理的。  

HTTP 是 Node.js 中的一等公民。它设计的是流式和低延迟。这使得 Node.js 非常适合于 web 库或框架的基础。

## Npm
在传统的前端开发中我们会经常引入jquery、bootstrap、echarts等js插件，我们首先去插件的每个官网去下载下来，然后放到自己前端工程中static/js目录下，我们每引用一个插件都要去官网下载，然后将下载的插件拖到工程中来，美国的一个程序员Isaac Z. Schlueter就做够了这种机械运动，想简化这个流程，于是做了这样一件事：

* 买了台服务器作为代码仓库(registry), 用于存放被共享的代码
* 发邮件分别通知各大JS插件作者(如jQuery的作者、bootstrap的作者、Vue的作者、element-ui的作者等等)让他们使用npm publish 命令将自己的JS插件提交到registry中
* 用户如果想使用某个JS插件可以先在package.json中配置一些需要安装的插件名称和对应的版本号(依赖dependency)，然后通过npm install命令来下载它们，下载下来的插件自动放在node_modules目录下面

这套思想和maven是完全一样的，熟悉maven或者gradle的也就自然理解npm了，只不过npm用于js,maven用于java，都是作者先将共享的代码放到某个公共的代码仓库，用户先在配置文件中配置好要使用的依赖，然后通过一个命令就能下载下来。

## Webpack:前端项目的构建工具
传统的前端一般会html、javascript、css这三样东西就够了。现代的前端发展迅猛，引入了TypeScript、SCSS、LESS、stylus(CSS预处理器)等技术，提供了更丰富的特性，提高了开发效率，但是引入的这些技术不能直接被浏览器解析，需要一个东西将浏览器不能解析的代码翻译成浏览器可以直接解析代码，这就是webpack的作用。

* TypeScript是JavaScript类型的超集(简单的说就是对JavaScript的封装)，提供更加丰富的特性(在JavaScript上添加了可选的静态类型和基于类的面向对象编程)，而且可以编译成纯JavaScript
* ECMAScript：ECMAScript是标准，JavaScript是ECMAScript的实现，ECMAScript也在快速发展，引入了更多的语法新特性等。其中ECMAScript6使用较多，现在ECMAScript8已经发布了。
* SCSS: SCSS即是SASS的新语法，是Sassy CSS的简写，是CSS3语法的超集，也就是说所有有效的CSS3样式也同样适合于SASS。SASS是CSS3的一个扩展，增加了规则嵌套、变量、混合、选择器继承等等。通过使用命令行工具或WEB框架插件把它转换成标准的、格式良好的CSS代码。
* less: Less 是一门 CSS 预处理语言，它扩展了 CSS 语言，增加了变量、Mixin、函数等特性，使 CSS 更易维护和扩展。Less 可以运行在 Node 或浏览器端。
* stylus：文件后缀是. styl 的这个哥们儿学名叫 stylus，是 CSS 的预处理框架。stylus 给 CSS 添加了可编程的特性，也就是说，在 stylus 中可以使用变量、函数、判断、循环一系列 CSS 没有的东西来编写样式文件，执行这一套骚操作之后，这个文件可编译成 CSS 文件。

webpack可以看做是模块打包机：它做的事情是，分析你的项目结构，找到JavaScript模块以及其它的一些浏览器不能直接运行的拓展语言（TypeScript、SCSS等），并将其打包为合适的格式以供浏览器直接使用。随着webpack的发展，webpack支持ECMAScript6、ECMAScript7、ECMAScript8等。随着webpack的发展，webpack不仅仅用来编译(翻译)代码，也集成了更多的功能，比如：
1. 热加载：修改了代码然后保存，浏览器会自动刷新
2. 压缩文件：压缩图片，字体, 脚本文件等
3. 插件(plugin)：webpack打包时可以执行某个插件，控制webpack打包时的某个过程，这种插件机制和maven中的插件原理完全一样

模块(module)化就是把复杂的应用程序细分为较小的文件，在webpack中一切都是模块，js、css、图片、字体等待都可称为模块。

### webpack中的重要功能
1. devtool:
   devtool: "eval-source-map" webpack打包后的文件可读性非常低，不利于调试，使用devtool可以生成对应的源码便于调试。使用eval打包源文件模块，在同一个文件中生成干净的完整的source map。这个选项可以在不影响构建速度的前提下生成完整的sourcemap，但是对打包后输出的JS文件的执行具有性能和安全的隐患。在开发阶段这是一个非常好的选项，在生产阶段则一定不要启用这个选项；
2. webpack-dev-server:
   webpack-dev-server 是一个本地开发服务器，居于node.js实现的，使用npm run dev 后就可以使用默认的8080端口在浏览器上访问了，类似于apache的功能
3. loaders:
   loader可以让webpack有能力调用外部的脚本或工具，实现对不同格式的文件的处理，比如说分析转换scss为css，或者把下一代的JS文件（ES6，ES7)转换为现代浏览器兼容的JS文件。css-loader 和 style-loader 就是用来处理样式的。
4. Babel(很重要):
   Babel其实是一个编译JavaScript的平台，它可以编译代码帮你达到以下目的：
   * 让你能使用最新的JavaScript代码（ES6，ES7等待），而不用管新标准是否被当前使用的浏览器完全支持；
   * 让你能使用基于JavaScript进行了拓展的语言，比如React的JSX；
5. plugins:
   插件（Plugins）是用来拓展Webpack功能的，它们会在整个构建过程中生效，执行相关的任务。
   Loaders和Plugins常常被弄混，但是他们其实是完全不同的东西，可以这么来说，loaders是在打包构建过程中用来处理源文件的（JSX，Scss，Less..），一次处理一个，插件并不直接操作单个文件，它直接对整个构建过程其作用。
   Webpack有很多内置插件，同时也有很多第三方插件，可以让我们完成更加丰富的功能  

   常用的插件：
   * HtmlWebpackPlugin
   * Hot Module Replacement（HMR） 热加载：允许你在修改组件代码后，自动刷新实时预览修改后的效果
   * clean-webpack-plugin 去除build文件中的残余文件
   * OccurenceOrderPlugin :为组件分配ID，通过这个插件webpack可以分析和优先考虑使用最多的模块，并为它们分配最小的ID
   * UglifyJsPlugin： 压缩JS代码
   * ExtractTextPlugin：分离CSS和JS文件

## Vue
* 它是一个轻量级的MVVM框架。
* 使用 数据驱动+组件化 来开。
* 数据双向绑定(当修改视图时数据也会赋值给model，当更改model的时候也会反应到视图上)。
* 页面上每个独立的可视或者可交互的区域均视为一个组件，每个组件对应一个工程目录(文件夹)，组件所需要的各种资源尽可能的都放在这个目录下就近维护(即将模板、样式、js等都写在一个.vue文件中)，组件可以嵌套自由组合，形成完整的页面。

## 集成Element
1. 安装element-ui
   ```js
   # 切换到项目根目录
   $ cd <project root dir>
   # 安装element-ui, 安装后package.json中dependencies就会增加element-ui依赖
   $ cnpm i element-ui -S 
2. 在main.js中配置element-ui
   在main.js中增加导入和让Vue使用ElementUI
   ```js
   import Vue from 'vue'
   import App from './App'
   import router from './router'
   // 导入element-ui
   import ElementUI from 'element-ui'
   Vue.config.productionTip = false
   // Vue使用ElementUI
   Vue.use(ElementUI)
   /* eslint-disable no-new */
   new Vue({
       el: '#app',
       router,
       components: { App },
       template: '<App/>'
       })

3. 安装依赖
   cnpm install


