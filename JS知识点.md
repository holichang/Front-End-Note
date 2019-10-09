#### 1.全角和半角：

全角：是一种电脑字符，是指一个全角字符占用两个标准字符(或两个半角字符)的位置。全角占两个字节。

半角：是指一个字符占用一个标准的字符位置。半角占一个字节。

全角和半角主要是针对标点符号来说的，全角标点占两个字节，半角占一个字节。不管是半角还是全角，汉字都要占两个字节。

##### JS判断输入的文字是全角还是半角

```js
str="中文；;a";
alert(str.match(/[\u0000-\u00ff]/g));   //半角 
alert(str.match(/[\u4e00-\u9fa5]/g));   //中文 
alert(str.match(/[\uff00-\uffff]/g));   //全角
```

##### JS找到全角空格和半角空格

str.charCodeAt()==32 ||str.charCodeAt()==12288

##### JS对全角与半角的相互转化：charCodeAt()  fromCharCode()

全角空格为12288，半角空格为32

其他字符半角(33-126)与全角(65281-65374)的对应关系是：均相差65248

全角空格：/\u3000/g    

半角空格：/\u0020/g

#### 2.JSON：

##### 2.1 JSON.stringfy()

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

##### 12.1XMLHttpRequest对象的三个属性：

onreadystatechange:存储函数（或函数名），每当 readyState 属性改变时，就会调用该函数。

readyState:存有 XMLHttpRequest 的状态。从 0 到 4 发生变化。

0: 请求未初始化

1: 服务器连接已建立

2: 请求已接收

3: 请求处理中

4: 请求已完成，且响应已就绪

status:200: "OK";404: 未找到页面

