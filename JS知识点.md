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

