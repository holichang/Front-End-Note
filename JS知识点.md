[TOC]



#### 1.全角和半角：

全角：是一种电脑字符，是指一个全角字符占用两个标准字符(或两个半角字符)的位置。全角占两个字节。

半角：是指一个字符占用一个标准的字符位置。半角占一个字节。

全角和半角主要是针对标点符号来说的，全角标点占两个字节，半角占一个字节。不管是半角还是全角，汉字都要占两个字节。

**JS判断输入的文字是全角还是半角**

```js
str="中文；;a";
alert(str.match(/[\u0000-\u00ff]/g));   //半角 
alert(str.match(/[\u4e00-\u9fa5]/g));   //中文 
alert(str.match(/[\uff00-\uffff]/g));   //全角
```

**JS找到全角空格和半角空格**

str.charCodeAt()==32 ||str.charCodeAt()==12288

**JS对全角与半角的相互转化：charCodeAt()  fromCharCode()**

全角空格为12288，半角空格为32

其他字符半角(33-126)与全角(65281-65374)的对应关系是：均相差65248

全角空格：/\u3000/g    

半角空格：/\u0020/g

#### 2.JSON：

`JSON.stringfy()`:将对象转为JSON字符串

`JSON.parse`：将JSON字符串转为对象

#### 3.回调函数

#### 4.文本框提示：

用keyup, keypress, keydown以及oninput四个事件分别来测试对于用户输入的事件监听，并在事件响应函数中增加console.log('event handle')。并尝试以下输入方式，观察提示框内容变化的情况，以及console的输出情况：

- 一个字母一个字母的输入

- 一个字母一个字母输入，同时加上按回车键，ESC键，上下左右键

- 按住某个字母键不动

  |                      |  keyup   | keypress | keydown  | oninput  |
  | :------------------: | :------: | :------: | :------: | :------: |
  | 一个字母一个字母输入 | 响应一次 | 响应一次 | 响应一次 | 响应一次 |
  |      加上回车键      | 响应一次 | 响应一次 | 响应一次 | 没有响应 |
  |      加上ESC键       | 响应一次 | 没有响应 | 响应一次 | 没有响应 |
  |     加上下左右键     | 响应一次 | 没有响应 | 响应一次 | 没有响应 |
  |  按住某个字母键不动  | 响应一次 | 持续响应 | 持续响应 | 持续响应 |

keypress和keydown显示的文本有延迟，不显示最后一个按键

（1）KeyDown触发后，不一定触发KeyUp，当KeyDown 按下后，拖动鼠标，那么将不会触发KeyUp事件。

（2）KeyPress主要用来捕获数字(**注意：包括Shift+数字的符号**)、字母（**注意：包括大小写**）、小键盘等除了F1-12、SHIFT、Alt、Ctrl、Insert、Home、PgUp、Delete、End、PgDn、ScrollLock、Pause、NumLock、{菜单键}、{开始键}和方向键外的ANSI字符

（3）KeyDown 和KeyUp 通常可以捕获键盘除了PrScrn所有按键(这里不讨论特殊键盘的特殊键）

（4）KeyPress 只能捕获单个字符

（5）KeyDown 和KeyUp 可以捕获组合键。

（6）KeyPress 可以捕获单个字符的大小写

（7）KeyDown和KeyUp 对于单个字符捕获的KeyValue 都是一个值，也就是不能判断单个字符的大小写。

（8）KeyPress 不区分小键盘和主键盘的数字字符。

（9）KeyDown 和KeyUp 区分小键盘和主键盘的数字字符。

（10）其中PrScrn 按键KeyPress、KeyDown和KeyUp 都不能捕获。

（11）在使用键盘的时候，通常会使用到CTRL+SHIFT+ALT 类似的组合键功能。对于此，我们如何来判定？

​     通过KeyUp 事件能够来处理（这里说明一下为什么不用KeyDown，因为在判定KeyDown的时候，CTRL、SHIFT和ALT 属于一直按下状态，然后再加另外一个键是不能准确捕获组合键，所以使用KeyDown 是不能准确判断出的，要通过KeyUp 事件来判定 ）

#### 5.Web安全之XSS攻防

**跨站脚本攻击(Cross Site Scripting)**，缩写为XSS。恶意攻击者往Web页面里插入恶意Script代码，当用户浏览该页之时，嵌入其中Web里面的Script代码会被执行，从而达到恶意攻击用户的目的。

[原文](https://blog.csdn.net/ganyingxie123456/article/details/70230486)

#### 6.innerText和innerHTML之间的转义

innerText:包含子结点的所有文本内容

innerHTML：不只是文本内容，还包含子节点的标签

```js
(temp.textContent != undefined ) ? (temp.textContent = html) : (temp.innerText = html);
```

textContent：谷歌,火狐支持,IE8不支持；innerText：谷歌,火狐,IE8都支持
判断这个属性的类型 是不是undefined,就知道浏览器是否支持

innerHTML在左边时，字符串会被自动编码如：

```JS
innerHTML=&lt;b&gt;//会被转为<b>
str=innerHTML;//innerHTML中的<b>标签被转为&lt;b&gt;
```

#### 7.相关方法

select() 方法用于选取input密码域或文本域中的文本

focus()方法用于使输入框获得焦点

对于<select>标签：

selectedIndex:设置或返回下拉列表中被选项目的索引号。

**方法：**

add():向下拉列表添加一个选项。

blur():从下拉列表移开焦点。

focus():在下拉列表上设置焦点。

remove():从下拉列表中删除一个选项。

#### 8.获取上一个节点和下一个节点

previousSibling 属性返回元素节点之前的兄弟节点（包括文本节点、注释节点）；

previousElementSibling 属性只返回元素节点之前的兄弟元素节点（不包括文本节点、注释节点）；

nextSibling 属性返回元素节点之后的兄弟节点（包括文本节点、注释节点）；

nextElementSibling 属性只返回元素节点之后的兄弟元素节点（不包括文本节点、注释节点）；

#### 9.innerHTML和outerHTML

innerHTML 设置或获取位于对象起始和结束标签内的HTML

outerHTML设置或获取对象及其内容的HTML形式

#### 10.html中的name，id和value

**value 和 name**

1.name是控件的名称（多个控件可以取同一个名称），value是控件的值

2.并不是所有控件的value都会显示出来，比如 checkbox, radio, hidden；

3.定义控件的 name和value 就可以在服务器上获取这个控件和它的值;

4.你没看到 submit 的name，并不表示浏览器忽略了它的 name，在提交之前它也被浏览器定义了 name，在服务器上一样可以得到它的 name 和 value；

5.控件不定义name/value也可以显示，只是为了方便在服务器接收和区别，才定义它的 name/value，当然按钮的 value 不光是存放它的值，也用来显示

[name 和id](https://www.cnblogs.com/jamesf/p/4751722.html)

#### 11.SVG

##### 11.1 XML：是独立于软件和硬件的信息传输工具。

**(1)XML和HTML：**

XML 被设计用来传输和存储数据。HTML 被设计用来显示数据

XML没有任何行为

XML仅仅是纯文本

XML的标签是没有预定义的，可以发明自己的标签

**（2）XML的用途**

XML把数据从HTML分离；XML简化数据共享，简化数据传输，简化平台变更，使数据更有用，用于创建新的Internet语言

**（3）XML验证：DTD**（document type definition）

DTD 的作用是定义 XML 文档的结构。它使用一系列合法的元素来定义文档结构：

**（4）如何通过JS读写XML**





##### 11.2 SVG

SVG 是使用 XML 来描述二维图形和绘图程序的语言。

SVG 文件可通过以下标签嵌入 HTML 文档：<embed>、<object> 或者 <iframe>。

<embed>标签定义嵌入的内容，比如插件，使H5中的新标签

SVG的代码可以直接嵌入到HTML页面中，或您可以直接链接到SVG文件。

##### 11.3 JS动态写入SVG：

**外部SVG：**

（1）通过object、embed或者iframe标签将SVG文件引入到HTML页面:其中的内容会有完全属于自己的document对象，可以用**getSVGDocument()**方法获取SVG文档对象

（2）如果使用object或iframe引入SVG文档，除了`getSVGDocument()`，还可以使用`contentDocument`属性来获取其引入文档对应的document对象。区别在于如果是引入的不是SVG文件，而是XML或者HTML等等，`contentDocuement`依然会返回对象，而`getSVGDocument()`则返回`null`。

（3）SVG元素对象都需要通过调用[`setAttribute()`](https://developer.mozilla.org/en-US/docs/Web/API/element.setAttribute)方法来设定属性值

**要求：满足同源策略（Same-origin-policy）**

同源策略指的是三个相同

- 协议相同
- 域名相同
- 端口相同

如果非同源，那么以下的行为将会受到限制；1，**cookie，localStorage**     2，**ajax** 

#### 12.AJAX

##### XMLHttpRequest对象的三个属性：

onreadystatechange:存储函数（或函数名），每当 readyState 属性改变时，就会调用该函数。

readyState:存有 XMLHttpRequest 的状态。从 0 到 4 发生变化。

0: 请求未初始化

1: 服务器连接已建立

2: 请求已接收

3: 请求处理中

4: 请求已完成，且响应已就绪

status:200: "OK";404: 未找到页面

xmlhttp.responseText:返回的文本文件

xmlhttp.open()

xmlhttp.send()

#### 13 HTML5 本地存储五种方案

##### 13.1 Web Storage API

源：origin，同源策略

**（1）localStorage：**

`localStorage` 中的键值对总是以字符串的形式存储。

`localStorage.setItem()`

`localStorage.getItem()`

`localStorage.removeItem()`

`localStorage.clear()`

**（2）sessionStorage：**

**（3）通过StorageEvent响应存储的变化**

无论何时，[`Storage`](https://developer.mozilla.org/zh-CN/docs/Web/API/Storage) 对象发生变化时（即创建/更新/删除数据项时，重复设置相同的键值不会触发该事件，[`Storage.clear()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Storage/clear) 方法至多触发一次该事件），`StorageEvent` 事件会触发。在同一个页面内发生的改变不会起作用——在**相同域名**下的**其他**页面（如一个新标签或 iframe）发生的改变才会起作用。在其他域名下的页面不能访问相同的 Storage 对象。

当前页面使用的storage被其他页面修改时会触发StorageEvent事件. 

**[事件在同一个域下的不同页面之间触发，即在A页面注册了storge的监听处理，只有在跟A同域名下的B页面操作storage对象，A页面才会被触发storage事件] **

事件属性：

![1570695196(1)](E:\Front-End-Note\image\1570695196(1).png)

##### 13.2 Cookie(曾一度用于客户端存储，逐渐被淘汰)

**（1）HTTP Cookie（也叫Web Cookie或浏览器Cookie）**

Cookie主要用于以下三个方面：

**会话状态管理**（如用户登录状态、购物车、游戏分数或其它需要记录的信息）

**个性化设置**（如用户自定义设置、主题等）

**浏览器行为跟踪**（如跟踪分析用户行为等）

**HttpOnly**:为避免跨域脚本 (XSS) 攻击，通过JavaScript的 Document.cookie API无法访问带有 HttpOnly 标记的Cookie，它们**只应该发送给服务端**。如果包含服务端 Session 信息的 Cookie 不想被客户端 JavaScript 脚本调用，那么就应该为其设置 HttpOnly 标记。

JavaScript可以通过跨站脚本攻击（XSS）的方式来窃取Cookie。

**安全：**

会话劫持和XSS；跨站请求伪造（CSRF）

**（2）document.cookie**

`docCookies.setItem(name, value[, end[, path[, domain[, secure]]]])`

`docCookies.getItem(name)`

`docCookies.removeItem(name[, path],domain)`

`docCookies.hasItem(name)`

`docCookies.keys()`

路径限制并**不能**阻止从其他路径访问cookie. 使用简单的DOM即可轻易地绕过限制(比如创建一个指向限制路径的, 隐藏的[iframe](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/iframe), 然后访问其 `contentDocument.cookie` 属性). 保护cookie不被非法访问的唯一方法是将它放在另一个域名/子域名之下, 利用[同源策略](https://developer.mozilla.org/zh-CN/docs/Web/Security/Same-origin_policy)保护其不被读取.

document.cookie的键和值中不能使用；，=以及空格，要用escape()函数进行编码，取出值后用unescape()解码

##### 13.3 IndexedDB

#### 14.event.preventDefault()

告诉[user agent](https://developer.mozilla.org/en-US/docs/Glossary/user_agent)：如果此事件没有被显式处理，那么它默认的动作也不要做（因为默认是要做的）。

`event.stopPropagation()`:阻止捕获和冒泡阶段中当前事件的进一步传播

#### 15.进程与线程

**进程：**CPU资源分配的最小单位，是能拥有资源和独立运行的最小单位（任一时刻，CPU总是运行一个进程，其他进程处于非运行状态）

**线程：**CPU调度的最小单位，是建立在进程基础上的一次程序运行单位，属于单个的程序执行流，是一个进程中代码的不同执行路线

一个进程中可以拥有多个线程，同一进程下的各个线程之间共享程序的内存空间（包括代码段、数据集、堆等）及一些进程级的资源。虽然不同进程之间也可以通信，不过代价较大。（可以在电脑的任务管理器中查看进程）

**浏览器是多进程的**

**概述：**

（1）浏览器之所以能够运行，是因为系统给它的进程分配了资源（cpu和内存）

（2）每打开一个tab页，就创建了一个独立的浏览器进程，每个进程相互独立

**多进程的好处：**

（1）不会因为一个tab页崩溃，导致其他tab页也被影响

（2）相对于线程，进程之间是不共享资源和地址空间的，所以也不会存在太多的安全问题

**浏览器包含的进程种类：**

（1）Browser进程——浏览器的主进程，负责协调、主控，只有一个

（2）第三方插件进程——每种类型的插件对应一个进程，仅当使用该插件时才创建

（3）GPU进程——最多一个，用于3D绘制等

（4）浏览器渲染进程——也就是浏览器内核

**浏览器内核是多线程的：**

**常驻线程：**

（1）GUI 渲染线程——负责渲染浏览器界面，解析HTML，CSS，当界面需要重排、重绘或由于某种操作引发回流时,该线程就会执行。**但需要注意 GUI渲染线程与JS引擎是互斥的，当JS引擎执行时GUI线程会被挂起，GUI更新会被保存在一个队列中等到JS引擎空闲时立即被执行。**

（2）JavaScript引擎线程——负责处理Javascript脚本程序：是基于事件驱动单线程执行的，JS引擎一直等待着任务队列中任务的到来，然后加以处理，浏览器无论什么时候都只有一个JS线程在运行JS程序。

（3）定时触发器线程——处理setInterval与setTimeout任务

（4）事件触发线程——处理事件消息，控制事件循环：当一个事件被触发时该线程会把事件添加到待处理队列的队尾，等待JS引擎的处理。这些事件可来自JavaScript引擎当前执行的代码块如setTimeOut、也可来自浏览器内核的其他线程如鼠标点击、AJAX异步请求等，但由于JS的单线程关系所有这些事件都得排队等待JS引擎处理。

（5）异步http请求线程——处理XMLHttpRequest异步请求

**js为什么会阻塞页面加载**

（1）由于GUI渲染线程与JavaScript执行线程是互斥的关系，当浏览器在执行JavaScript程序的时候，GUI渲染线程会被保存在一个队列中，直到JS程序执行完成，才会接着执行。

（2）因此如果JS执行的时间过长，这样就会造成页面的渲染不连贯，导致页面渲染加载阻塞的感觉

**JS是单线程的**

引用阮一峰老师的回答 --->  JavaScript的单线程，与它的用途有关。作为浏览器脚本语言，JavaScript的主要用途是与用户互动，以及操作DOM。这决定了它只能是单线程，否则会带来很复杂的同步问题。比如，假定JavaScript同时有两个线程，一个线程在某个DOM节点上添加内容，另一个线程删除了这个节点，这时浏览器应该以哪个线程为准？

所以，为了避免复杂性，从一诞生，JavaScript就是单线程。

**单线程和异步** 

看过很多关于 JavaScript 单线程与异步的介绍，大多数都引用这一类例子来说明：单线程就是排队，前一个任务不完成后一个就不能开始，也就是常说的串行。 饭店点餐，所有人排队，A顾客点完之后，厨房开始做，做完后A领到餐后，B再开始点餐，厨房又开始做…周而复始，这就是同步，点餐的时候厨房是闲着的，做菜的时候前台是闲着的。即单线程。所有人都能够很好的理解，这样做效率太低了！

　　换个思路，A点完餐后，到一旁等着，服务员将菜单递给厨房，厨房开始做，然后继续服务B顾客，当A顾客的餐做好之后，A来队伍里插个队，把餐领走。 听到这里，效率高了很多嘛，整个餐厅没有浪费一点工作力，大家都各司其事。然后作者就下了结论，这就是 JavaScript 的单线程与异步。

**JS中的异步操作：**

（1）定时器都是异步操作

（2）事件绑定都是异步操作

（3）AJAX中一般我们都采用异步操作（也可以同步）

（4）回掉函数可以理解为异步（不是严谨的异步操作）

#### 17.Flash和JS通过什么类如何交互？

Flash提供了**ExternalInterface**接口与JavaScript通信，ExternalInterface有两个方法，**call和addCallback**：

- **ExternalInterface.addCallback**("在js里可调用的flash方法名",flash内方法) //在flash中通过这个方法公开 在js中可调用的flash内的方法;
- **ExternalInterface.call**("js方法",传给js的参数) //在flash里调用js里的方法

#### 18. apply和call：提供参数的方式不同

（1）基本使用方法：可以只写一次这个方法然后在另一个对象中继承它，而不用在新对象中重复写该方法。

`Function.apply(obj,argu)`

obj:这个对象将代替Function类里的this对象，即调用这个函数的对象（非严格模式下如果用null或undefined则会替代为全局环境）

argu:要传入函数的参数数组，也可以是类数组

`Function.call(obj,[param1[,param2[,…[,paramN]]]])`

后面是要传入函数的参数列表

**（2）apply的一些巧妙用法**

>**用apply将数组添加到另一个数组**
>
>不同于concat(另建了一个副本，并没有改变原数组)
>
>```js
>var arr1=[1,2,3];
>var arr2=[4,5,6];
>arr1.push.apply(arr1,arr2);
>```
>
>**使用apply和内置函数**
>
>如：`Math.max()`,`Math.min()`
>
>**使用apply来链接构造器：*

