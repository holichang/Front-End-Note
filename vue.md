[TOC]



## 一.相关知识点

#### 1.渐进式框架：

没有强主张，没有多做职责之外的事

#### 2.前端工程化：

[原文](https://www.cnblogs.com/ihardcoder/p/5378290.html)

##### 2.1 前端工程化，面临的问题是如何提高**编码->测试->维护**阶段的生产效率

##### 2.2 要解决前端工程化的问题，可以从两个角度入手：**开发**和**部署**。

从**开发角度**，要解决的问题包括：

（1）提高开发生产效率；

（2）降低维护难度。

这两个问题的解决方案有两点：

（1）制定开发规范，提高团队协作能力；

（2）分治。软件工程中有个很重要的概念叫做**模块化开发**其中心思想就是分治。

从**部署角度**，要解决的问题主要是**资源管理**，包括：

（1）代码审查；

（2）压缩打包；

（3）增量更新；

（4）单元测试；

**模块化开发：**模块白盒，组件黑盒。颗粒度不同

##### 2.3 构建&编译

2016年节点下，一个典型的web前后端协作模式如下图：

![img](https://images2015.cnblogs.com/blog/595796/201604/595796-20160411142716207-1803317219.png)

**大前端模式下：**

![img](https://images2015.cnblogs.com/blog/595796/201604/595796-20160411142733598-1823214206.png)

大前端体系下，前端开发人员掌握着Node.js搭建的web server层。与上文提到的常规前端开发体系下相比，省略了mock server的角色，但是构建在大前端体系下的作用并没有发生改变。也就是说，不论是大前端还是“小”前端，构建阶段在两种模式下的作用完全一致，**构建的作用就是对静态资源以及模板进行处理**，换句话说：**构建的核心是资源管理**。

**什么是资源管理？**

前端的资源可以分为**静态资源**和**模板**。模板对静态资源是引用关系，两者相辅相成，构建过程中需要对两种资源使用不同的构建策略。

静态资源包括js、css、图片等文件，目前随着一些新规范和css预编译器的普及，通常开发阶段的静态资源是：

1. es6/7规范的文件；
2. less/sass等文件（具体看团队技术选型）；
3. [可选]独立的小图标，在构建阶段使用工具处理成spirit图片。

构建可以分为**工具层面**和**平台层面**的功能：

- 工具层面

1. 预编译，包括es6/7语法转译（比如babel）、css预编译器处理（如将less/sass编译成css）、spirit图片生成；
2. 依赖打包。分析文件依赖关系，将同步依赖的的文件打包在一起，减少http请求数量；
3. 资源嵌入。比如小于10KB的图片编译为base64格式嵌入文档，减少一次http请求；
4. 文件压缩。减小文件体积；
5. hash指纹。通过给文件名加入hash指纹，以应对浏览器缓存引起的静态资源更新问题；
6. 代码审查。避免上线文件的低级错误；
7. 模板构建。

- 平台层面

1. 文件监听。配合动态构建、浏览器自动刷新等功能，提高开发效率；（热加载）
2. mock server。并非所有前端团队都是大前端（事实上很少团队是大前端），即使在大前端体系下，mock server的存在也是很有必要的；

##### 2.4 总结;

一个完整的前端工程体系应该包括：

（1）统一的开发规范；

（2）组件化开发；

（3）构建流程。

#### 3.脚手架

简易前端工作流如下：

![1569339963707](C:\Users\凌多\AppData\Roaming\Typora\typora-user-images\1569339963707.png)

脚手架：作用是创建项目的初始文件,**让项目从"搭建-开发-部署"更加快速以及规范**，前端脚手架的实质包含两项，命令式的构建项目（解析命令，拷贝项目到本地），提供项目的配置（构建，编译，代码规范检查）,同时应具备高度可扩展性

#### 4.构建

- Gulp,Grunt（重在规范前端开发流程，并不强调模块化）：集成度不高，要写很多配置后才可以用，无法做到开箱即用。相比于Grunt,Gulp增加了监听文件、读写文件、流式处理的功能。

- fis:百度开发的，配置简单、开箱即用、内置了许多功能，无需做太多配置就能完成大量工作

- webpack（重在模块化开发，文件压缩，预编译等功能只是附带的）：Webpack（https://webpack.js.org） 是一个打包模块化JavaScript的工具，在Webpack里一切文件皆模块，通过Loader转换文件，通过Plugin注入钩子，最后输出由多个模块组合成的文件。Webpack专注于构建模块化项目。

  优点：专注于处理模块化的项目，能做到开箱即用、一步到位；可通过Plugin扩展，完整好用又不失灵活；使用场景不局限于Web开发；社区庞大活跃，经常引入紧跟时代发展的新特性，能为大多数场景找到已有的开源扩展；良好的开发体验。

  缺点：只能用于采用模块化开发的项目。

#### 5.less、sass、scss

less 和 sass 是两种 css 预编译语言，就是说通过 less 或者 scss 写的代码最终都会被编译成 css 再使用。其目的是为了更快、更结构的编写 css 文件，都能使用 变量、运算符、判断、方法等等。

scss 与 sass 的区别：

先有的 sass 后有的 scss
scss 需要大括号{}和分号;
sass 什么都不用直接裸奔，通过缩进来区分代码等级，像 yaml 语言

#### 6.MVC、MVP、MVVM

**6.1 MVC**

MVC模式软件可以分为三个部分:View（用户界面）,Controller（业务逻辑）,Model（数据保存）,但这三个部分没有明显的界限

各部分之间的通信方式如下：所有通信都是单向的

![MVC](D:\Front-End-Note\image\MVC.png)

**6.2 MVP**

MVP模式将Controller改名为Presenter,同时改变了通信方向：

![MVP](D:\Front-End-Note\image\MVP.png)

- 各部分之间的通信，都是双向的。
-  View 与 Model 不发生联系，都通过 Presenter 传递。
-  View 非常薄，不部署任何业务逻辑，称为"被动视图"（Passive View），即没有任何主动性，而 Presenter非常厚，所有逻辑都部署在那里。

**6.3 MVVM：**Model-View-ViewModle：模型-视图-**视图模型（核心：双向桥梁）**

![MVVM](D:\Front-End-Note\image\MVVM.png)

和MVP唯一的区别是MVVM采用双向绑定，View的变化会自动反映在ViewModel，反之亦然。

【模型】转为【视图】：数据绑定

【视图】转为【模型】：DOM事件监听

在MVVM的框架下视图和模型是不能直接通信的。它们通过ViewModel来通信，ViewModel通常要实现一个observer观察者，当数据发生变化，ViewModel能够监听到数据的这种变化，然后通知到对应的视图做自动更新，而当用户操作视图，ViewModel也能监听到视图的变化，然后通知数据做改动，这实际上就实现了数据的双向绑定。

ViewModel存在目的在于抽离Controller中展示的业务逻辑

主流框架实现双向绑定（响应式）：

**（1）脏值检查 **（angular.js）
**（2）观察者-订阅者（数据劫持）**（Vue.js）VueObserver数据监听器

Vue双向绑定原理：

![Vue双向绑定](D:\Front-End-Note\image\Vue双向绑定.jpg)

从图中可以看出，当执行 new Vue() 时，Vue 就进入了初始化阶段，一方面Vue 会遍历 data 选项中的属性，并用 Object.defineProperty 将它们转为 getter/setter，实现数据变化监听功能；另一方面，Vue 的指令编译器Compile 对元素节点的指令进行解析，初始化视图，并订阅Watcher 来更新视图， 此时Watcher 会将自己添加到消息订阅器中(Dep),初始化完毕。当数据发生变化时，Observer 中的 setter 方法被触发，setter 会立即调用Dep.notify()，Dep 开始遍历所有的订阅者，并调用订阅者的 update 方法，订阅者收到通知后对视图进行相应的更新。因为VUE使用Object.defineProperty方法来做数据绑定，而这个方法又无法通过兼容性处理，所以Vue 不支持 IE8 以及更低版本浏览器。另外，查看vue原代码，发现在vue初始化实例时， **有一个proxy代理方法，它的作用就是遍历data中的属性，把它代理到vm的实例上，这也就是我们可以这样调用属性：vm.aaa等于vm.data.aaa。**

**proxy代理：**



****

## 二. Vue知识点：

## 基础：

**Vue的特点：**

- 渐进式框架：没有强主张，没有做职责之外的事

- 自底向上逐层应用

- 只关注视图层，便于与第三方库或既有项目整合

- 当与**现代化的工具链**以及**各种支持类库**结合使用时，能够为复杂的单页应用提供驱动

  >什么是现代化的工具链？
  >
  >

**对比其它框架：**

>
>
>

Vue不仅可以把数据绑定到DOM文本或attribute，还可以绑定到DOM结构，以及强大的过渡效果系统，可以在Vue插入/更新/移除元素时自动应用过渡效果

v-bind:attr绑定属性，v-if，v-for，v-on:click事件监听，v-model:处理用户输入

### 1. Vue实例

（1）当一个 Vue 实例被创建时，它将 `data` 对象中的所有的 property 加入到 Vue 的**响应式系统**中。当这些 property 的值发生改变时，视图将会产生“响应”，即匹配更新为新的值。

（2）只有当实例被创建时就已经存在于data中的property才是响应式的。

（3）Vue通过$将Vue的实例property和方法与用户定义的property区分开来。

#### 1.1 实例生命周期钩子：

钩子函数和回调函数：

钩子函数 和 回调函数 一般都可用来处理事件“回调”。

回调函数是你留个处理方法给事件，事件发生了以后会自动执行你留下调处理方法；

钩子函数是好比找了个代理，监视事件是否发生，如果发生了这个代理就执行你的事件处理方法；在这个过程中，代理就是钩子函数；

在某种意义上，回调函数做的处理过程跟钩子函数中要调用调方法一样

但是有一点需要明确： 钩子函数一般是又事件发生者提供的。直白了说，它留下一个钩子，这个钩子的作用就是钩住你的回调方法。

#### 1.2 生命周期图示：

每个 Vue 实例在被创建时都要经过一系列的初始化过程——例如，需要设置数据监听、编译模板、将实例挂载到 DOM 并在数据变化时更新 DOM 等。

<img src="D:\Front-End-Note\image\vue生命周期.png" alt="vue生命周期" style="zoom:50%;" />

### 2.模板语法

**虚拟DOM：**相比重排/重绘，javaScript运行速度很快，虚拟DOM是放在JS 和 HTML中间的一个层。它可以通过新旧DOM的对比，来获取对比之后的差异对象，然后有针对性的把差异部分真正地渲染到页面上，从而减少实际DOM操作，最终达到性能优化的目的。

![virtualDOM](D:\Front-End-Note\image\virtualDOM.png)

#### 2.1 插值

**文本：**双大括号{{message}}（v-once指令可以限制执行一次性插值），数据可以改变但视图不会变化

**原始HTML：**使用v-html指令，需要一个元素作为容器，该容器的内容会被替换为v-html所指的属性

> **注意：**不能用v-html来复合局部模板，因为Vue不是基于字符串的模板引擎，对于用户界面，组件更适合作为可重用和可组合的基本单位。并且，在站点上动态渲染的任意 HTML 可能会非常危险，因为它很容易导致 [XSS 攻击](https://en.wikipedia.org/wiki/Cross-site_scripting)。请只对可信内容使用 HTML 插值，**绝不要**对用户提供的内容使用插值。

**特性**：v-bind,通过v-bind绑定HTML attribute

**使用JavaScript表达式**：每个绑定都只能包含**单个表达式**

>模板表达式都被放在沙盒中，只能访问全局变量的一个白名单，如Math和Date。你不应该在模板表达式中试图访问用户定义的全局变量。
>
>沙盒（sandbox）：为了让不可信的代码运行在一定的环境中，从而限制这些代码访问隔离区之外的资源

#### 2.2 指令

指令的职责是，当表达式的值改变时，将其产生的连带影响，响应式地作用于 DOM。

**参数**：如：v-bind:href="url"    v-on:click="doSomething"

**动态参数（2.6.0新增）：**用方括号括起来，如：v-bind:[attributaName]="url"

*约束：动态参数的字符串值为null时，可以显性地移除绑定；动态参数表达式有一些语法约束，因为某些字符，如空格和引号，放在 HTML attribute 名里是无效的。*

**修饰符：**以半角句号 `.` 指明的特殊后缀，用于指出一个指令应该以特殊方式绑定。

#### 2.3 缩写

**v-bind:**   :

**v-on:**   @

### 3.计算属性和侦听器

#### 3.1计算属性

Vue实例下的computed属性

提供的函数将用作属性的getter函数

**计算属性与方法**

method:方法；computed:计算属性

不同的是**计算属性是基于它们的响应式依赖进行缓存的**。只在相关**响应式依赖**发生改变时它们才会重新求值。这就意味着只要 `message` 还没有发生改变，多次访问 `reversedMessage` 计算属性会立即返回之前的计算结果，而不必再次执行函数。相比之下，每当触发重新渲染时，调用方法将**总会**再次执行函数。

>计算属性可以通过闭包来实现传参
>
>

**计算属性与侦听属性**

watch:侦听（被侦听的属性发生改变后会执行所对应的函数）

侦听属性易被滥用

**计算属性的setter**：不是直接修改计算属性而是修改它的依赖

#### 3.2 侦听属性watch：

使用watch选项允许我们执行异步操作（访问一个API），限制我们执行某操作的频率（watch中可以执行任何逻辑，如函数防抖，节流，Ajax异步获取数据）

>计算属性和侦听属性：
>
>1. 计算属性：
>   * 数据可以进行逻辑处理，减少模板中计算逻辑
>   * 对计算属性中的数据进行监视
>   * 依赖固定的数据类型
>   * 由get和set两部分组成
>   * 不能执行异步任务，必须同步执行
>2. 侦听属性：
>   * handler:侦听属性发生变化时触发的回调函数
>   * deep:布尔值，设置为true时可监听到被侦听对象属性的变化
>   * immediate:布尔值，设置为true将立即以表达式的当前值触发回调
>3. computed能做的，watch都能做，反之则不行
>4. 能用computed的尽量用computed

### 4.Class与Style绑定：

在将v-bind用于class和style时，Vue.js做了专门的增强，表达式结果的类型除了字符串还可以是对象或数组

#### 4.1绑定HTML Class

**对象语法**

**数组语法**

**用在组件上**

#### 4.2绑定内联样式

**对象语法**

**数组语法**

**自动添加前缀：**当`v-bind:style`使用需要添加浏览器引擎前缀的CSS property时，如transform，Vue.js会自动侦测并添加相应的前缀

**多重值**

### 5.条件渲染

**5.1 v-if**

`v-if` 指令用于条件性地渲染一块内容。这块内容只会在指令的表达式返回 truthy 值的时候被渲染。

也可以用`v-else-if`, `v-else` 添加一个“else 块”

**5.2 在<template>元素上使用v-if条件渲染分组**

可以把一个 `<template>` 元素当做不可见的包裹元素

**5.3 用key管理可复用的元素**

**Vue会尽可能高效地渲染元素，通常会复用已有元素而不是从头开始渲染，为元素添加key可以阻止元素的复用**

key属性表示两种元素是完全独立的，不要复用他们

**5.4**  v-show：该元素一直存在，只是切换CSS属性的display

>**`v-show `和` v-if`:**
>
>- 实现本质方法区别：带有v-show的元素始终会被渲染并保留在DOM中，v-show只是简单地切换元素的CSS属性display；v-if是动态地向DOM树内添加或者删除DOM元素
>- 编译的区别：v-show其实就是在控制CSS；v-if切换有一个局部编译/卸载的过程，切换过程中销毁和重建内部的事件监听和子组件
>- 编译的条件：v-show初始值为false也会进行编译；v-if初始值为false不会编译
>- 性能：v-show只编译一次，后面其实就是控制css:display，而v-if不停地销毁和创建，故v-show性能更好一点
>
>**`display:none`和`visibility:hidden`:**
>
>- `display:none`会被渲染出来，但不占据任何空间，切换display的值会导致重排（盒子大小位置变了），但没有操作DOM；而`visibility:hidden`隐藏后的元素空间依旧保留，切换visibility只会导致重绘
>- visibility具有继承性，给父元素设置visibility:hidden;子元素也会继承这个属性。但是如果重新给子元素设置visibility: visible,则子元素又会显示出来。这个和display: none有着质的区别
>- visibility: hidden不会影响计数器的计数
>- CSS3的transition支持visibility属性，但是并不支持display，由于transition可以延迟执行，因此可以配合visibility使用纯css实现hover延时显示效果。提高用户体验。

`v-if` 是“真正”的条件渲染，因为它会确保在切换过程中条件块内的事件监听器和子组件适当地被销毁和重建。

因此，如果需要非常频繁地切换，则使用 `v-show` 较好；如果在运行时条件很少改变，则使用 `v-if` 较好。

v-if与v-for一起使用：当 `v-if` 与 `v-for` 一起使用时，`v-for` 具有比 `v-if` 更高的优先级。

>**思考：display:none的元素被渲染了吗？**
>
>[参考：Web图片资源的加载与渲染时机](https://segmentfault.com/a/1190000010032501)
>
>浏览器渲染页面的顺序：
>
>* 解析html,构建dom树；
>
>* 加载css，解析css,构建css规则树；
>
>* 加载js，执行js代码
>
>* 把dom树和css规则树匹配构建渲染树
>
>* 计算元素位置进行布局
>
>* 绘制
>
>  当匹配DOM树和css规则树时，若发现一个严肃的对应的样式规则上有`display:none`，浏览器会认为该元素不可见，因此不会把该元素产出到渲染树
>
>  * 把背景图片转为base64格式作为占位符：
>
>  * base64格式有什么用？
>
>    **如果图片足够小且因为用处的特殊性无法被制作成雪碧图（CssSprites），在整个网站的复用性很高且基本不会被更新**。
>

### 6.列表渲染

**6.1 用v-for把一个数组对应为一组元素**

`v-for` 还支持一个可选的第二个参数，即当前项的索引。

**6.2 在v-for里使用对象**（会按照Object.keys()的结果遍历）：可以遍历对象

支持第二个参数键名和第三个参数索引

**6.3 维护状态**

如果数据项的顺序被改变，Vue 将不会移动 DOM 元素来匹配数据项的顺序，而是就地更新每个元素，并且确保它们在每个索引位置正确渲染。

这个默认的模式是高效的，但是**只适用于不依赖子组件状态或临时 DOM 状态 (例如：表单输入值) 的列表渲染输出**。

为了给 Vue 一个提示，**以便它能跟踪每个节点的身份，从而重用和重新排序现有元素**，你需要为每项提供一个唯一 `key` 属性：key属性是Vue识别节点的一个通用机制

>**注意事项：**
>
>由于JavaScript的限制，vue不能检测数组和对象的变化
>
>改变数组数据的方法：1.改变数组的引用；2.使用数组的变异方法；3. 使用`Vue.set()`或`vm.$set()`
>
>改变对象数据的方法：1.改变对象的引用；2.使用`Vue.set()`或`vm.$set()`

**6.4 数组更新检测**

变异方法：（改变了数组本身）：`push()`,`pop()`,`shift()`,`unshift()`,`splice()`,`sort()`,`reverse()`

替换数组：（不会改变数组本身，因此用新数组替换原始数组，Vue的智能启发式方法使得用含有相同元素的数组替换原来的数组非常高效）：`filter()`,`concat()`,`slice()`

注意事项：由于 JavaScript 的限制，Vue **不能**检测以下数组的变动：

1. 当你利用索引直接设置一个数组项时，例如：`vm.items[indexOfItem] = newValue`

2. 当你修改数组的长度时，例如：`vm.items.length = newLength`

   可以改用以下方法:

   ```JS
   Vue.set(vm.items, indexOfItem, newValue)
   vm.items.splice(indexOfItem, 1, newValue)
   ```

**6.5对象变更检测注意事项**

对于已经创建的实例，Vue 不允许动态添加根级别的响应式属性。（向对象中添加新的属性不会响应在视图中）但是，可以使用 `Vue.set(object, propertyName, value)` 方法向嵌套对象添加响应式属性。

有时你可能需要为已有对象赋值多个新属性，比如使用 `Object.assign()` 或 `_.extend()`。

如：

```JS
vm.userProfile = Object.assign({}, vm.userProfile, {
age: 27,
favoriteColor: 'Vue Green'
})
```

`Object.assign()` 方法用于将所有可枚举属性的值从一个或多个源对象复制到目标对象。它将返回目标对象。

**6.6 显示过滤/排序后的结果**

数组不改变，但要显示过滤/排序后的结果：用方法或者计算属性

**6.7 在v-for里使用值范围**

v-for="n in 10"

**6.8 在<template>上使用v-for**

**6.9 v-for 与 v-if一同使用**（v-for的优先级高于v-if）

> 不推荐在同意元素上使用v-if和v-for

>不推荐在同意元素上使用v-if和v-for

当处于同一节点可以只渲染部分节点；

当v-if处于外层元素，可以有条件的跳过循环的执行

**6.10 在组件上使用v-for:**

任何数据都不会被自动传递到组件里，因为组件有自己独立的作用域，为了把迭代数据传递到组件里， 要使用prop:

### 7.事件处理

**有时候需要在内联语句处理器中访问原始的DOM事件，可以用特殊变量`$event`把它传入方法**

**事件修饰符：**

**按键修饰符：**

元素获得焦点之后才会触发按键事件，所以要把keyup绑定在document上，或者先触发*获得焦点事件*

**系统修饰符**：

- `.ctrl`：keycode为17

- `.alt`：keycode为18

- `.shift`：keycode为16

- ``.meta`：（windows键）

  修饰符仅在按下相应按键时才触发鼠标或键盘事件的监听器

请注意修饰键与常规按键不同，在和 `keyup` 事件一起用时，事件触发时修饰键必须处于按下状态。换句话说，只有在按住 `ctrl` 的情况下释放其它按键，才能触发 `keyup.ctrl`。而单单释放 `ctrl` 也不会触发事件。如果你想要这样的行为，请为 `ctrl` 换用 `keyCode`：`keyup.17`。

`.exact`:修饰符允许你控制由精确的系统修饰符组合触发的事件。

<!-- 即使 Alt 或 Shift 被一同按下时也会触发 -->
`<button @click.ctrl="onClick">A</button>`
<!-- 有且只有 Ctrl 被按下的时候才触发 -->
`<button @click.ctrl.exact="onCtrlClick">A</button>`
<!-- 没有任何系统修饰符被按下的时候才触发 -->
`<button @click.exact="onClick">A</button>`

**鼠标按钮修饰符**

`.left`,`.right`,`.middle`这些修饰符会限制处理函数仅响应特定的鼠标按钮。

### 8.表单输入绑定

#### 8.1 基础用法：

`v-model` 在内部为不同的输入元素使用不同的属性并抛出不同的事件：

text 和 textarea 元素使用 `value` 属性和 `input` 事件；

checkbox 和 radio 使用 `checked` 属性和 `change` 事件；

**checkbox：单个复选框，绑定到checked布尔值；多个复选框，绑定到同一个数组,数组元素为被选中元素的value值，按照被选中顺序push进数组**

**radio：单选框：绑定的为被选中元素的value属性值，String类型‘’**

select 字段将 `value` 作为 prop 并将 `change` 作为事件。

#### 8.2 修饰符：

* .lazy：默认情况下，v-model在每次input事件触发后将输入框的值与数据进行同步，.lazy修饰符可以转为在change事件后进行同步
* .number：自动将用户输入值转为数值类型，如果该值无法被parseFloat()解析，则会返回原始的值。***（type为number时，如果无法被parseFloat()解析，直接返回空字符串？type为text时，如果无法被parseFloat()解析返回原始值）***
* .trim：自动过滤用户输入的首尾空白字符

### 9.组件

组件是可复用的实例，它们与`new Vue`接收相同的选项，例如`data`、`computed`、`watch`、`methods`以及生命周期钩子等。仅有的例外是像el这样根实例特有的选项。

**但组件中的data选项必须是一个函数，这样每创建一个组件都会返回一个新的对象，各个组件之间互不影响**

* 通过prop向子组件传递数据：将需要传递的数据赋给prop，component中再通过prop设置要显示的内容

* 监听子组件事件
* 通过插槽分发内容
* 动态组件
* 解析DOM模板时的注意事项

#### 9.1 组件注册

定义组件名的方式有两种：

* kebab-case（短横线分隔命名）：使用该组件时也要用kebab-case;
* PascleCase（首字母大写命名）：使用该组件时可以用短横线分隔命名，也可以用首字母大写命名，但**直接在DOM（非字符串模板）中使用时只有kebab-case是有效的**

全局注册和局部注册：

* 在模块系统中局部注册（通过import或require引入要使用的其他模块，进行局部注册）

* 基础组建的自动化全局注册：**webpack：require.context**

  >**待重看**
  >
  >

#### 9.2 Prop

* HTML中attribute名是大小写不敏感的，浏览器会把所有大写字符解释为小写字符。意味着使用DOM模板时camelCase的prop名需要使用其等价的短横线分隔命名；但在字符串模板中没有这个限制

* 可以以对象的形式列出prop,指定名称和类型

* 单向数据流：

  * 所有的prop都使得其父子prop之间形成了一种**单向下行绑定**：父级prop的更新会向下流动到子组件中，但是反过来不行。这样会防止从子组件意外变更父级组件的状态，从而导致应用的数据流向难以理解。

  * 每次父级组件发生变更时，子组件中所有的prop都将会刷新为最新的值。这意味着不应该在一个子组件内部改变prop，如果这样做了，Vue会在浏览器控制台中发出警告；
  * 两种常见的试图变更一个prop的情形：
    * 这个prop用于传递一个初始值：这个子组件接下来希望将其作为一个本地的prop数据来使用。（这种情况最好在子组件中定义一个data property，并将这个prop用作初始值 ）；
    * 这个prop以一种原始的值传入且需要进行转换。（这种情况下，最好使用这个prop值来定义一个计算属性）

* prop验证：

  **prop会在一个组件实例创建之前进行验证，所以实例的property（如data,computed等）在default或validator函数中是不可用的**

  type可以是下列原生构造函数中的一个：

  * String
  * Number
  * Boolean
  * Array
  * Object
  * Date
  * Function
  * Symbol
  * 额外的，还可以是一个自定义构造函数，是通过instanceof来进行检查的

* 非prop的Attribute：组件可以接受任意的attribute，而这些attribute会被添加到这个组件的根元素上

  * 如果不希望组件的根元素继承attribute,可以在组件的选项中设置`inheritAttrs:false`;
  * 通过`$attr`可以手动决定这些attribute会被赋予给哪个元素：`v-bind=$attrs`

#### 9.3 自定义事件

* 事件名：推荐使用kebab-case的事件名
* 自定义组件的`v-model`,组件中的model选项允许一个自定义组件在使用v-model时定制prop和event(子传父，父传子)
* 将原生事件绑定到组件上
  * 可以在组件的**根元素**上直接监听一个原生事件：使用`v-on`的`.native`修饰符
  * 如果想监听组件内部元素的原生事件：
    * `$listeners`：是一个对象，里面包含了作用在这个组件上的所有监听器
    * 可以配合`v-on='$listeners'`将所有的事件监听器指向这个组件的某个特定的子元素

* 修饰符 `.sync`：实现双向绑定：`v-bind:value.sync='content'`，相当于实现了父传子，子组件触发了`update:value`的语法糖。也可以`v-bind.sync='object'`，对象object内部的属性作为被传值的属性，此时不支持表达式。

#### 9.4 插槽

**父级模板里的所有内容都是在父级作用域中编译的；子模版里的内容都是在子作用域中编译的**

**（1）具名插槽**

子组件模板中：`<slot name='head'></slot>`

为命名的插槽为：`<slot name='default'></slot>`

父组件中：`<template v-slot:head>要传入的内容</template>`

**`v-slot`缩写为#，上述可以简写为：**

`<template #head></template>`

**（2）作用域插槽**：父级渲染时在插槽中使用子组件的数据：利用插槽prop

原来的版本中：`<template slot-scope='slotProps'>{{slotProps.user}}</template>`

2.6以后的版本中：

* 只有默认插槽时：

`<template v-slot:default='slotProps'>{{slotProps.user}}</template>`

或`<template v-slot='slotProps'>{{slotProps.user}}</template>`

**slotProps为包含所有插槽props的对象，可自己命名**

插槽可以提供数据内容，由父组件提供样式

#### 9.5 动态组件&异步组件

**（1）动态组件**

`<component v-bind:is='currentTabComponent'></component>`

创建缓存，保存上一次渲染结果：

```html
<keep-alive>
  <component v-bind:is='currentTabComponent'></component>
</keep-alive>
```

**（2）异步组件** ：待进一步理解

#### 9.6 处理边界情况

**9.6.1 访问元素&组件**

* 访问根实例：`this.$root`

  在每个`new vue`实例的子组件中，可以将该实例作为一个全局store来访问或使用(推荐使用Vuex)

* 访问父级组件实例：`this.$parent`

  针对需要向任意更深层级的组件提供上下文信息时推荐**依赖注入**

* 访问子组件实例或子元素：`this.$refs.input`：从父组件中获取到子组件，只会在组件渲染完成之后生效，不是响应式的。

* 依赖注入：非响应式的。**建议使用vuex管理状态**

  父级组件中：提供provide选项，无需知道哪些子组件使用了它提供的property

  子组件中：提供inject选项，无需知道该注入是哪个父组件提供的

**9.6.2 程序化的事件监听器**

- 通过 `$on(eventName, eventHandler)` 侦听一个事件

- 通过 `$once(eventName, eventHandler)` 一次性侦听一个事件

- 通过 `$off(eventName, eventHandler)` 停止侦听一个事件

  ```vue
  this.$once('hook:beforeDestroy',function(){
  	//事件处理函数
  })
  ```

**9.6.3 循环引用**

解决办法：

* 等到开始组件的生命周期钩子`beforeCreate`时去注册它
* 本地注册时使用webpack的异步import

**9.6.4 模板定义的替代品**(不建议使用)

* 内联模版：inline-template
* X-Template：在`<script type='text/x-template' id=''></script>`

**9.6.5 控制更新**

* 强制更新：`$forceUpdate`
* `v-once`：确保内容只被计算一次就被缓存起来

### 10. 过渡/动画

**10.1 进入/离开&列表过渡**

**10.2 状态过渡**

### 11. 可复用性&组合

#### 11.1 混入：mixins

```js
var component=Vue.extend({
  mixins:[myMixin]
})
//定义一个使用混入对象的组件
```

* 数据对象在内部会进行递归合并，并在发生冲突时以组件数据优先。
* 同名钩子函数将合并为一个数组，都将被调用，混入对象的钩子将在组件自身钩子**之前**调用。
* 值为对象的选项，例如 `methods`、`components` 和 `directives`，将被合并为同一个对象。两个对象键名冲突时，取组件对象的键值对。

#### 11.2 自定义指令：

>思考：什么时候用自定义指令，什么时候用自定义插件，二者区别
>
>使用自定义指令的情况：
>
>* 需要对普通DOM元素进行底层操作
>* 

* 全局指令：`Vue.directive(指令名，如：'focus'，{钩子函数：})`
* 局部指令：`directives:{focus:{option}}`：只能在组件内部使用
* 钩子函数：参数：el,binding,vnode,oldVnode
  * bind:只调用一次，指令第一次绑定到元素时调用，在这里可以进行一次性的初始化设置
  * inserted:被绑定元素插入父节点时调用（仅保证父节点存在，但不一定已被插入文档中）
  * update:所在组件的VNode更新时调用，但可能发生在其子VNode 更新之前
  * componentUpdated:指令所在组件的VNode及其子VNode全部更新后调用
  * unbind:只调用一次，指令与元素解绑时调用

#### 11.3 渲染函数&JSX

* 虚拟DOM：`createElement`返回的是虚拟节点，简写为‘VNode’，虚拟DOM是对由Vue组件树建立起来的整个VNode树的称呼
* 

#### 11.4 插件

插件通常用来为 Vue 添加全局功能。插件的功能范围没有严格的限制——一般有下面几种：

1. 添加全局方法或者 property。如：[vue-custom-element](https://github.com/karol-f/vue-custom-element)
2. 添加全局资源：指令/过滤器/过渡等。如 [vue-touch](https://github.com/vuejs/vue-touch)
3. 通过全局混入来添加一些组件选项。如 [vue-router](https://github.com/vuejs/vue-router)
4. 添加 Vue 实例方法，通过把它们添加到 `Vue.prototype` 上实现。
5. 一个库，提供自己的 API，同时提供上面提到的一个或多个功能。如 [vue-router](https://github.com/vuejs/vue-router)

* 使用插件：在调用`new Vue()`之前通过`Vue.use(myPlugin,{someOption:})`使用插件
* 开发插件：

#### 11.5 过滤器

### 12. 工具

#### 12.1 单文件组件

#### 12.2 单元测试

#### 12.3 TypeScript支持

#### 12.4 生产环境部署





****

## 三.相关构建工具

### 1.webpack打包

WebPack可以看作是一个模块打包机，它用于分析项目结构，找到JS模块以及其他的一些浏览器无法直接运行的拓展语言（scss,typeScript等），将其编译并打包为合适的格式供浏览器使用。

### 2.使用入门

```js
//首先初始化，生成package.json文件，该文件用于记录这个项目的详细信息
npm init
//接下来安装webpack
npm install -g webpack//全局安装
npm install --save-dev webpack //安装到某个项目文件夹
```



## 1. Vue基础学习：

### 1.1 可复用性&组合

#### 1.1.1 混入：mixin:一个混入对象可以包含任意组件选项

* 

#### 1.1.2  自定义指令

#### 1.1.3 渲染函数&JSX

#### 1.1.4 插件

#### 1.1.5 过滤器

### 1.2 生命周期：（待确认，看源码）

* beforeCreate之前初始化事件和生命周期；
* beforeCreate和created之间初始化injection和reactivity:已经可以获取到data

* created和beforeMount间的生命周期：

  综合排名优先级：

  render函数选项 > template选项 > outer HTML

* beforeMount和mounted之间的生命周期：

  在mounted之前，在dom中通过{{message}}占位，以js中的虚拟DOM形式存在，mounted之后给Vue实例添加$el成员，并替换掉挂载的DOM元素（beforeMount阶段是虚拟DOM，到了mounted阶段才有真实的DOM）

* beforeUpdate和updated：

  在beforeUpdate可以监听到data的变化但view层没有被重新渲染，view层的数据没有变化；到Updated的时候view层才被重新渲染，数据更新。

### 1.3 

## 