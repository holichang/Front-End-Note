[TOC]

## JS 高级程序设计

### 1.JavaScript简介

#### 1.1 ECMA-262：

ECMAScript脚本语言标准，与Web浏览器没有依赖关系，常见的Web浏览器只是JavaScript可能实现的宿主环境之一，宿主环境不仅提供基本的ECMAScript实现，同时也会提供该语言的扩展，以便语言与宿主环境之间交互。而这些扩展——如DOM，则利用ECMAScript的核心类型和语法提供更多更具体的功能，以便实现针对环境的操作。其他宿主环境包括Node和Adobe Flash.

#### 1.2 一个完整的JavaScript实现应该由下列三个不同的部分组成：

（1）核心（ECMAScript）：由ECMA-262定义，提供核心语言功能

（2）文档对象模型(DOM)：提供访问和操作网页内容的方法和接口，DOM1---DOM2---DOM3

DOM不只是针对JavaScript的，很多别的语言也都实现了DOM（如SVG,MathML,SMIL都基于XML）

（3）浏览器对象模型（BOM）：提供与浏览器交互的方法和接口，HTML5将很多BOM功能写入了正式规范

大多数浏览器在提及对JavaScript的支持情况时，一般都以ECMAScript兼容性和对DOM的支持情况为准。

### 2 .在HTML中使用JavaScript

#### 2.1 < script >元素

**2.1.1 标签的位置**

**2.1.2 延迟脚本：**表明脚本在执行时不会影响页面的构造，也就是说，脚本会被延迟到整个页面都解析完毕后再执行。在< script >元素中设置defer 属性，相当于告诉浏览器立即下载，但延迟执行。

**2.1.3 异步脚本：**与defer 类似，async 只适用于外部脚本文件，并告诉浏览器立即下载文件。但与defer不同的是，标记为async 的脚本并不保证按照指定它们的先后顺序执行，第二个脚本文件可能会在第一个脚本文件之前执行，因此设置async属性的两个脚本之间互不依赖非常重要。指定async 属性的目的是不让页面等待两个脚本下载和执行，从而异步加载页面其他内容。为此，建议异步脚本不要在加载期间修改DOM。

**2.1.4 在XHTML中的用法**

XHTML的规则比HTML严格的多，为避免在XHTML中出现类似语法错误，有两个方法：

（1）用相应的HTML实体，如用&lt代替<,但该方法不利于理解

（2）用一个CData片段来包含JS代码：有的浏览器不兼容XHTML，因此不支持CData片段，因此可以注释掉：

```javascript
<script type="text/javascript">
//<![CDATA[
//]]>
</script>
```

**2.1.5 不推荐使用的语法**（已过时）

#### 2.2 嵌入代码与外部文件

外部文件（更推荐）：可维护性、可缓存、适应未来（通过外部文件来包含JavaScript 无须使用前面提到XHTML 或注释hack。HTML 和XHTML 包含外部文件的语法是相同的。）

#### 2.3 文档模式：

通过使用文档类型（doctype）切换实现：最初的两种文档模式：混杂模式和标准模式

**如果在文档开始处没有发现文档类型声明，则所有浏览器都会默认开启混杂模式**

后期：对于准标准模式，可以通过使用过渡型或框架集型文档类型来触发

### 3.基本概念

#### 3.4 数据类型

**3.4.1 typeof操作符**

5种基本数据类型：Undefined,Null,Boolean,String,Number

一种复杂数据类型：Object

`typeof 函数`   //  "function"

`typeof  对象或null`   //  ''object''

**3.4.2 Undefined类型**

```js
var message;//这个变量声明后默认取得了undefined值
// var age;
alert (message);//"undefined"
alert (age);//报错
alert (typeof message);//"undefined"
alert (typeof age);//"undefined"
```

**3.4.3 Null类型**

```js
null==undefined//true
null===undefined//false
```

**3.4.4 Number类型**

将非数值转为数值类型的函数：

Number():与一元+操作符的操作相同，对于Object类型：先调用.valueOf()方法 ,再调用toString()方法

`Number('')\\0`

parseInt()：把字符串转为整数  `parseInt('')//NaN`

parseFloat()：只解析十进制

**3.4.5 String类型**

将值转为字符串类型的方法：

（1）数值、布尔值、对象和字符串值都有toString()方法，但null和undefined值没有这个方法

（2）String():能够将任何类型的值转换为字符串：

`String(null)//'null'   `

`String(undefined)//'undefined'`

（3）''+要转为字符串类型的值

**3.4.5 Object类型**

Object的每个实例都具有下列属性和方法：

constructor:保存用于创建当前对象的函数

hasOwnProperty:用于检查给定的属性在当前对象实例中是否存在

isPrototypeOf(object)：用于检查对象是否是传入对象的原型

propertyIsEnumerable(propertyName)：用于检查给定属性是否能够使用for-in语句来枚举

toLocaleString()：该字符串与执行环境的地区对应

toString()：返回对象的字符串表示

valueOf()：返回对象的字符串、数值或布尔值表示

#### 3.5 操作符

**3.5.1 一元操作符**

（1）递增或递减操作符：**不仅适用于整数，还可以用于字符串、布尔值、浮点数值、对象**

前置：先求值再执行语句

后置：先执行语句再求值

（2）一元加和减操作符：应用于非数值时，类似于Number()转换函数

**3.5.2 位操作符 **

（1）按位非（NOT）：用~表示：**相当于对操作数的负值-1**

（2）按位与（AND）：用&表示

（3）按位或（OR）：用|表示

（4）异或（XOR）：用^表示：不同才为1

（5）左移（<<）:左移不会影响操作数的符号位

（6）右移：有符号右移：>>用符号位的值来填充右移产生的所有空位，与左移类似

​                     无符号右移：>>>用0来填充右移产生的所有空位(对于负数而言，由于将负数看作整数的表示方法，右移后的结果会非常大)

**3.5.3 布尔操作符**

（1）逻辑非：！

（2）逻辑与：&&：可以应用于任何类型的操作数，而不仅仅是布尔值，在有一个操作数不是布尔值的情况下，逻辑与操作就不一定返回布尔值，它遵循以下规则：

> 如果第一个操作数是对象，则返回第二个操作数；
> 如果第二个操作数是对象，则只有在第一个操作数的求值结果为true 的情况下才会返回该
> 对象；
> 如果两个操作数都是对象，则返回第二个操作数；
> 如果有一个操作数是null，则返回null；
> 如果有一个操作数是NaN，则返回NaN；
> 如果有一个操作数是undefined，则返回undefined。

​          短路操作符：**如果第一个操作数能够决定结果，那么就不会再对第二个操作数求值**

（3）逻辑或：||

>如果第一个操作数是对象，则返回第一个操作数；
> 如果第一个操作数的求值结果为false，则返回第二个操作数；
> 如果两个操作数都是对象，则返回第一个操作数；
> 如果两个操作数都是null，则返回null；
> 如果两个操作数都是NaN，则返回NaN；
> 如果两个操作数都是undefined，则返回undefined。

**3.5.4 乘性操作符**

（1）乘法（Infinity*0==NaN）;

（2）除法（Infinity/Infinity==NaN;0/0==NaN）；

（3）求模 ：取余：

**如果被除数是无穷大值而除数是有限大的数值,则取余结果是NaN;**

**如果被除数是有限大的数值，而除数是0，则取余结果是NaN;**

**如果是Infinity被Infinity除，则取余结果是NaN；**

**3.5.5 加性操作符**

如果是+Infinity与-Infinity相加,结果是NaN；

如果是Infinity减Infinity，结果是NaN;

如果是-Infinity减-Infinity，结果是NaN;

**3.5.6关系操作符**

任何操作数与NaN进行关系比较，结果都是false

**3.5.7  相等操作符**

`null==undefined  //true`

`null===undefined//false`

**3.5.8 条件操作符**

**3.5.9 赋值操作符**

**3.5.10 逗号操作符**

#### 3.6语句

**3.6.1 for-in语句**：是一种精准的迭代语句，可以用来枚举对象的属性，如：

```JS
for(var propName in window){
    document.write(propName);
}
```

每次循环，都会将window对象中存在的一个属性名赋值给变量propName。ECMAScript对象的属性没有顺序，因此for-in循环输出的属性名的顺序事不可预测的。

**3.6.2 label语句**：相当于给for循环一个变量名，然后用break或continue来引用

**3.6.3 with语句：**将代码的作用域设置到一个特定的对象中，用于简化多次编写同一个对象的工作（严格模式下不允许使用）

**3.6.4 switch语句：**switch语句在比较值时使用的是全等操作符

#### 3.7 函数

**参数：**ECMAScript中的参数在内部是用一个数组表示，可以用arguments对象访问该参数数组，arguments与数组类似。

**ECMAScript中的所有参数传递的都是值，不可能通过引用传递参数**

### 4 变量、作用域和内存问题

### 4.1 基本类型和引用类型的值

基本类型：null,undefined,number,string,boolean,symbol

引用类型：object

值类型与引用类型的区别:

（1）存储方式的不同：值类型存储的是实际的值，存在栈中；而引用类型的值是保存在堆内存中的对象，JS不允许直接操作对象的内存空间，因此实际操作的是对象的引用而不是实际的对象。

（2）引用类型可以动态添加属性：引用类型可以动态添加对象的属性，值类型不可以

（3）复制变量值的方式不同：从一个变量向另一个变量复制基本类型值，会在变量对象上创建一个新值，然后把该值复制到为新变量分配的位置上，这两个变量可以参与任何操作互不影响；而引用类型复制的是对象的地址引用，指向的是同一个对象，对副本的操作会影响对象本身。

（4）传递参数的方式不同，JS中所有函数的参数都是按值传递的，与复制变量值的过程是一样的，因此在向参数传递引用类型的值时，这个局部变量的变化会反映在函数的外部。（可以把ES函数的参数想象成局部变量）

（5）检测类型时的不同：检测基本数据类型时可以使用typeof操作符；检测引用类型值：instanceof操作符

### 4.2 执行环境及作用域

每个执行环境都有一个与之关联的变量对象，环境中定义的所有变量和函数都保存在这个对象中。

在**Web浏览器**中，全局执行环境被认为是window对象

当代码在一个环境中执行时，会创建变量对象的一个**作用域链**。作用域链的用途，是保证对执行环境有权访问的所有变量和函数的有序访问。作用域的前端，始终都是当前执行的代码所在环境的变量对象。如果这个环境是函数，则将其活动对象作为变量对象。活动对象在最开始时只包含一个变量，即arguments对象（这个对象在全局环境中是不存在的）。作用域链中的下一个变量对象来自包含（外部）环境，而再下一个变量对象则来自下一个包含环境。这样一直延续到全局执行环境；全局执行环境始终是作用域链中的最后一个对象。

标识符解析是沿着作用域链一级一级地搜索标识符的过程。搜索过程始终从作用域链的前端开始，然后逐级地向后回溯，直至找到标识符为止。

**延长作用域链**：try-catch语句的catch块；with语句

**with语句**：用于设置代码在特定对象中的作用域，有了 With 语句，在存取对象属性和方法时就不用重复指定参考对象，在 With 语句块中，凡是 JavaScript 不识别的属性和方法都和该语句块指定的对象有关。（with 语句是运行缓慢的代码块，尤其是在已设置了属性值时。大多数情况下，如果可能，最好避免使用它。）

变量的执行环境有助于确定应该何时释放内存

### 4.3垃圾收集：JS有自动垃圾收集机制

离开作用域的值被自动标记为可以回收，因此将在垃圾收集期间被删除

垃圾收集机制的原理：找出那些不再继续使用的变量，然后释放其占用的内存，垃圾收集器会按照固定的时间间隔（或代码执行中预定的收集时间）周期性地执行这一操作。

**如何标识无用变量**：垃圾收集方式

（1）标记清除：思想是给当前不使用的值加上标记，然后再回收其内存。（**JS中最常用的**）

垃圾收集器在运行的时候会给存储在内存中的所有变量都加上标记，然后去掉环境中的变量以及被环境中变量引用的变量的标记，在此之后再被加上标记的变量将被视为准备删除的变量，原因是环境中的变量已经无法访问到这些变量了。最后垃圾收集机器完成**内存清除**工作，销毁那些带标记的值并回收他们所使用的内存空间。

（2）引用计数：（不太常见）跟踪记录每个值被引用的次数，当引用次数变为0时，将其占用的内存空间回收回来。但有一个严重问题：**循环引用**，因此被放弃了。

（3）性能问题：如何确定垃圾收集的时间间隔：IE7：静态临界值调整为动态修正（<15%：临界值加倍；>85%：重置回默认临界值）

（4）管理内存：**解除引用**：一旦数据不再有用，通过将其值设为null来释放其引用，目的是让值脱离执行环境，以便垃圾收集器下次运行时将其回收，同时也有助于消除循环引用现象。。

### 5.引用类型

对象是某个特定引用类型的实例

### 5.1 Object类型

创建Object实例的方法：  

使用new操作符后跟Object构造函数：var person= new Object()  

使用对象字面量表示法  

访问属性的方法：点表示法和方括号表示法

点表示法只能接受字面量的成员的名字，不接受变量作为名字

```js
var myDataName = 'height'
var myDataValue = '1.75m'
person[myDataName] = myDataValue
```

### 5.2 Array类型

使用Array构造函数时可以省略new操作符，如下面两个例子结果是相同的

```
var colors = new Array(3);
var colors = Array(3);
```

与对象一样，在使用数组字面量表示法时，也不会调用Array构造函数。

检测数组：if(value instanceof Array):但instanceof操作符假定只有一个全局执行环境，当网页包含多个框架，那实际上就存在两个以上不同的全局执行环境，从而**存在两个以上不同版本的Array构造函数**，为解决这个问题，ES5引入了**Array.isArray(value)**。

#### 5.2.1数组转化为字符串：

toString(),toLocaleString():实际调用的是数组中每一项的toString()方法

join():参数为用作分隔符的字符串，若不传入任何值，或传入undefined，则使用逗号作为分隔符。

#### 5.2.2 栈方法：后进先出

push()：可以接受任意数量的参数，把它们逐个添加到数组末尾，并**返回修改后数组的长度**

pop()：从数组末尾移除最后一项，减少数组的length值，然后**返回移除的项**。

#### 5.2.3 队列方法：先进先出：

push()：可以接受任意数量的参数，把它们逐个添加到数组末尾，并**返回修改后数组的长度**

shift()：从数组前端移除一项，减少数组的length值，然后**返回移除的项**。

unshift():能在数组前端添加任意个项，并**返回新数组的长度**

#### 5.2.4重排序方法

reverse()

sort():默认情况下，比较的是每个数组项的字符串，由小到大；因此可以接收函数作为参数，如果第一个参数应该在第二个参数前面，则返回负数，如果第一个参数应该在第二个参数后面则返回整数，**返回对数组的引用**。数组在原数组上进行排序，不生成副本。

#### 5.2.5操作方法

concat()：连接：操作的是副本

slice()：截取：操作的是副本，返回被截取的数组

splice():可以删除、插入以及替换：直接对原数组进行操作,返回一个数组，数组中包含从原始数组中删除的项。

#### 5.2.6 位置方法：

indexOf();lastIndexOf()  要求查找的项必须严格相等（===）

#### 5.2.7 迭代方法：

传入这些方法中的函数会接收三个参数：数组项的值，该项在数组中的位置和数组对象本身

every()：对数组中的每一项运行给定函数，如果该函数对**每**一项都返回true，则返回true

some():对数组中的每一项运行给定函数，如果该函数对**任**一项都返回true，则返回true

filter()：对数组中的每一项运行给定函数，返回该函数会返回true的项组成的数组

forEach()：对数组中的每一项运行给定函数，该方法没有返回值（本质与for循环迭代数组一样）

map()：对数组中的每一项运行给定函数，返回每次函数调用的结果组成的数组

（Array.prototype.map.call("str",function(){})）:可以将map方法用在字符串上

#### 5.2.8 归并方法：

reduce(),reduceRight():传进来的函数包括4个参数：前一个值，当前值，项的索引和数组对象

>**ES6中数组的扩展：**
>
>
>
>

### 5.3 RegExp类型

#### 5.3.1 模式：

g:全局模式   i:不区分大小写模式    m:多行模式

#### 5.3.2 创建：注意双重转义

使用字面量模式： var pattern1 = / [bc]at/i;

使用构造函数创建：var pattern1 = new RegExp("[bc]at","i")

ES3中，正则表达式字面量始终会共享同一个RegExp实例，而使用构造函数创建的没一个新的RegExp实例都是一个新实例。

#### 5.3.3 符号：<https://www.w3school.com.cn/jsref/jsref_obj_regexp.asp>

#### 5.3.4实例方法：

（1）RegExpObject.compile(RegExp):用于在脚本执行过程中编译正则表达式,也可用于改变和重新编译正则表达式。

（2）RegExpObject.exec(string):如果 exec() 找到了匹配的文本，返回一个数组，其中存放匹配的结果。如果未找到匹配，则返回值为null。此数组的第 0 个元素是与正则表达式相匹配的文本，第 1 个元素是与 RegExpObject 的第 1 个子表达式相匹配的文本（如果有的话），第 2 个元素是与 RegExpObject 的第 2 个子表达式相匹配的文本（如果有的话），以此类推。

返回的数组包含两个额外属性：

index:表示匹配项在字符串中的位置  ；   input:表示应用正则表达式的字符串

对于exec()方法而言，即使在模式中设置了全局标志（g），它每次也只返回一个匹配项。

在不设置全局标志的情况下，在同一个字符串上多次调用exec()将始终返回第一个匹配项的信息，而RegExpObject的lastIndex属性依旧为0；

而在设置全局标志的情况下，每次调用exec()则都会在字符串中继续查找新匹配项，RegExpObject的lastIndex属性依旧为为匹配文本的最后一个字符的下一个位置，当 exec() 再也找不到匹配的文本时，它将返回 null，并把 lastIndex 属性重置为 0。

（3）RegExpObject.test(string):用于检测一个字符串是否匹配某个模式.(只想知道是否匹配的情况)

#### 5.3.5 RegExp实例继承的方法：

（1）toLocaleString()和toString()方法都会返回正则表达式的字面量，与创建正则表达式的方式无关

```js
var pattern = new RegExp("\\[bc\\]at","gi");
alert(pattern.toLocaleString());/\[bc\]at/gi
alert(pattern.toString());/\[bc\]at/gi
```

（2）valueof()方法返回正则表达式本身

#### 5.3.6 支持正则表达式的String对象的方法

>**ES6中正则的扩展：**
>
>

### 5.4 Date类型

Date.parse():接受一个表示日期的字符串,然后根据这个字符串返回相应日期的毫秒数

Date.UTC()：参数分别是年份，基于0的月份（0-11），月中的哪一天（1-31），小时数（0-23），分钟，秒数以及毫秒数。同样返回相应的毫秒数（返回的是GMT时间）

Date.now():返回调用这个方法的日期和时间的毫秒数

Date.getTime():返回系统时间的毫秒数

### 5.5 Function类型

#### 5.5.1 函数提升：

解析器在向执行环境中加载数据时，对函数声明和函数表达式并非一视同仁，解析器会率先读取函数声明，并使其在执行任何代码之前可用，至于函数表达式，则必须等到解析器执行它所在的代码行，才会真正被解释执行。

valueOf()和toString()方法返回函数的源代码

#### 5.5.2 函数内部属性：arguments 和this

arguments:类数组对象，有一个名叫callee的属性，该属性是一个指针，指向拥有这个arguments对象的函数

arguments.callee:方便用于递归

另一个函数对象的属性：caller：保存着调用当前函数的函数的引用(arguments.callee.caller:可实现松散的耦合)

#### 5.5.3 函数属性和方法：

属性：length(表示函数希望接收的命名参数的格式) 和 prototype（ES5中不可枚举）

方法：apply()（第二个参数是数组或arguments）和call():用于在特定的作用域中调用函数，**可以扩充函数赖以运行的作用域**

bind():该方法会创建一个函数实例，其this值会被绑定到传给bind()函数的值

>**ES6中函数的扩展**
>
>

### 5.6基本包装类型

ECMAScript提供了3个特殊的引用类型：Boolean,Number和String,每当读取一个基本类型值的时候，后台就会创建一个对应的基本包装类型的对象，从而让我们能够调用一些方法来操作这些数据。

**引用类型与基本包装类型的主要区别就是对象的生存期。使用new操作符创建的引用类型的实例，在执行流离开当前作用域之前都一直保存在内存中。而自动创建的基本包装类型的对象，则只存在于一行代码的执行瞬间，然后立即被销毁。所以我们不能在运行时为基本类型值添加属性和方法。**

对基本包装类型的实例调用typeof会返回“object"，而且所有基本包装类型的对象在转换为布尔值时都是true

在使用typeof 和instanceof操作符测试基本类型数值与引用类型数值时，得到的结果完全不同。

基本包装类型重写了valueOf(),toLocaleString(),toString()方法，重写后的valueOf()方法返回对象表示的基本类型的值，另外两个方法则返回字符串形式的值。

#### 5.6.1 Boolean类型

基本类型的布尔值与Boolean对象之间的区别：

```js
var falseObject=new Object(false);
var result = falseObject && true;
alert (result);//true
alert (typeof falseObject)；//Object
alert (falseObject instanceof Boolean);//true
```

```js
var falseValue=false;
var result = falseValue && true;
alert (result);//false
alert (typeof falseValue)；//boolean
alert (falseValue instanceof Boolean);//false
```

#### 5.6.2 Number类型

将数值格式化为**字符串**的方法：都会进行舍入操作

toFixed(num) ：0<=num<=20：按照指定的小数位数返回数值的字符串表示

toExponential(num): 0<=num<=20,用指数记数法表示，小数点前只有一位

toPrecision(num) :1<=num<=21：返回 NumberObject 的字符串表示，包含 num 个有效数字。如果 num 足够大，能够包括 NumberObject 整数部分的所有数字，那么返回的字符串将采用定点计数法。否则，采用指数计数法，即小数点前有一位数字，小数点后有 num-1 位数字。必要时，该数字会被舍入或用 0 补足。

>**ES6中数值的扩展**：
>
>

#### 5.6.3 String类型

即时字符串中包含双字节字符（不是占一个字节的ASCII字符），每个字符也仍然算一个字符

（1）字符方法：charAt();charCodeAt();方括号表示法：string[index]

（2）字符串操作方法：对原始字符串没有影响

拼接：concat()  或者 +运算符

截取：slice() ; substring() ; substr()（substr第二个参数是返回的字符个数)

slice（）方法会将参数与字符串总长度相加  ;

substring（）方法会将负值变为0，较小值放在第一个参数位置，较大值放在后面  ;

substr（）：第一个参数为负值时，将参数与字符串总长度相加；第二个参数为负值时，将参数变为0 ;

（3）字符串位置方法：indexOf(”str“,index):从字符串开头向后搜索和lastIndexOf(”str“,index)：从末尾向前

（若找不到返回-1,第二个参数可省，表示开始查找的位置）

（4）trim方法：该方法会创建一个字符串的副本，删除前置及后缀的所有空格，然后返回结果。

（部分浏览器还支持trimLeft()和trimRight()）

（5）字符串大小写转换方法：

toLowerCase(),toUpperCase();**toLocaleLowerCase();toLocaleUpperCase()**：更稳妥

（6）**字符串的模式匹配方法：**

match()：与RegExp的exec()方法基本相同（全局模式下有差别）

search():返回字符串中第一个匹配项的索引，若没有查找到则返回-1

**replace(argu1,argu2)**:argu1可以是字符串或者RegExp对象;argu2可以是字符串或者函数(字符串本身不变)

要想替换所有子字符串，要用RegExp的全局模式

若第二个参数为函数，则在只有一个匹配项（即与模式匹配的字符串）的情况下，会向这个函数传递3个参数：模式的匹配项、匹配项在字符串中的位置和原始字符串。在正则表达式定义多个捕获组的情况下，传递给函数的参数依次是模式的匹配项、第一个捕获组的匹配项、第二个捕获组的匹配项......，但最后两个参数依然分别是模式匹配项在字符串中的位置和原始字符串。这个函数返回一个字符串，表示应该被替换的匹配项。

split()：基于指定的分隔符将一个字符串分割成多个子字符串，并将结果放在一个数组中，分隔符可以是字符串也可以是一个RegExp对象，可选的第二个参数用于指定数组的大小。

（7）str1.LocaleCompare(str2)方法：比较两个字符串，返回的数组取决于实现:

str1 在 str2前面：return -1; str1 在 str2后面：return 1;str1 等于 str2：return 0

（8）fromCharCode():接收一或多个字符编码，然后将它们转换成一个字符串

（9）一些HTML方法：如anchor(),big()等，但应尽少使用，因为它们创建的标记通常无法表达语义。

>**ES6中字符串的扩展和新增方法**
>
>
>
>

### 5.7 单体内置对象

### 6.理解对象

【图解】

![对象](D:\Front-End-Note\image\对象.png)

### 6.1 理解对象

#### 6.1.1 属性类型

ES5中有两种属性：数据属性和访问器属性

**数据属性**：数据属性包含一个数据值的位置。在这个位置可以读取和写入值。数据属性有4个描述其行为的特性：

[[Configurable]]:表示能否通过delete删除属性从而重新定义属性，能否修改属性的特性，或者能否把属性修改为访问器属性。

[[Enumerable]]：表示能否通过for-in循环返回属性。

[[Writable]]：表示能否修改属性的值。

[[Value]]：包含这个属性的值。

**要修改属性默认的特性：**ES5的**Object.defineProperty()**方法（三个参数：属性所在的对象、属性的名字、描述符对象）使用如下：

```JS
var person={};
Object.defineProperty(person,"name",{
    writable:false;
    value:"Nicholas";
})
alert(person.name);//"Nicholas"
person.name="Greg";
alert(person.name);//"Nicholas"
```

可以多次调用Object.defineProperty()方法修改同一个属性，但在把configurable特性设置为false之后就会有限制了。同时，**在调用Object.defineProperty()方法创建一个新属性时，如果不指定，configurable，enumerable和writable特性的默认值都是false**,如果调用Object.defineProperty()方法是修改已定义属性的特性，则无此限制。

**访问器属性**（常用方法：设置一个属性的值会导致其他属性发生变化）

访问器属性不包含数据值，它包含一对getter函数和setter函数（不过这两个函数都不是必需的）。在读取访问器属性时，会调用getter函数，这个函数负责返回有效的值，在写入访问器属性时，会调用setter函数并传入新值，这个函数负责决定如何处理数据。访问器属性有如下4个特性：

[[Configurable]]:表示能否通过delete删除属性从而重新定义属性，能否修改属性的特性，或者能否把属性修改为数据属性。

[[Enumerable]]：表示能否通过for-in循环返回属性。

[[Get]]：在读取属性时调用的函数。默认值为undefined。

[[Set]]：在写入属性时调用的函数。默认值为undefined。

**访问器属性不能直接定义，必须使用**Object.defineProperty()来定义。

```JS
var book={
    _year:2004,
    edition:1
};
Object.defineProperty(book,"year",{
    get:function(){
        return book._year;
    },
    set:function(newValue){
        if(newValue>2004){
            this._year=newValue;
            this.edition=newValue-2004;
        }
    }
});
book.year=2005;
alert(book.edition);//2
```

#### 6.1.2 定义多个属性

Object.defineProperties()方法:可以一次性定义多个属性

```JS
Object.defineProperties(book,{
    _year:{
        writable:true,
        value:2004
    },
    edition:{
        writable:true;
        value:1
    },
    year:{
        get:function(){
            return book._year;
        },
        set:function(newValue){
            if(newValue>2004){
                this._year=newValue;
                this.edition=newValue-2004;
            }
        }
    }
});
```

#### 6.1.3 读取属性的特性

**Object.getOwnPropertyDescriptor()**方法：取得给定属性的描述符。接收两个参数：属性所在的对象和要读取其描述符的属性名称，如：(接上段代码)

```js
var descriptor=Object.getOwnPropertyDescriptor(book,"_year");
alert(descriptor.value);//2004
alert(descriptor.configurable);//false
```

**ES5的Object.getOwnPropertyDescriptor（）方法只能用于实例属性，要取得原型属性的描述符，必须直接在原型对象上调用该方法。**

在JavaScript 中，可以针对任何对象——包括 DOM 和BOM 对象，使用Object.getOwnProperty-Descriptor()方法。支持这个方法的浏览器有IE9+、Firefox 4+、Safari 5+、Opera 12+和Chrome。

### 6.2创建对象

#### 6.2.1 工厂模式：

```js
function createPerson(name,age,job){
   var person=new Object();
   person.name=name;
   person.age=age;
   person.job=job;
   person.sayName=function(){
       console.log('my name is'+this.name)
   }
   return person;
}
var person1=createPerson("Nicholas",29,"Software Engineer");
var person2=createPerson("Greg",27,"Doctor");
```

用函数来封装以特定接口创建对象的细节（虽然解决了创建多个相似对象的问题，但没有解决对象识别的问题,即怎么知道一个对象的类型）

#### 6.2.2 构造函数模式

```js
function Person(name,age,job){
    this.name=name;
    this.age=age;
    this.job=job;
    this.sayName=function(){
        return this.name;
    };
}
var person1=new Person("Nicholas",29,"Software Engineer");
var person2=new Person("Greg",23,"Doctor");
alert(person1.constructor==Person);//true
alert(person1 instanceof Person);//true
```

**构造函数模式和工厂模式的区别：**

（1）没有显式地创建一个新对象

（2）直接将属性和方法赋给了新对象

（3）没有return语句

**使用new操作符调用构造函数实际会经历以下步骤：**

（1）创建一个新对象

（2）这个新对象会被执行[[Prototype]]连接；

（3）将构造函数的作用域赋给新对象（因此this就指向了这个对象）

（4）执行构造函数中的代码（为这个新对象添加属性）

（5）返回新对象

**创建自定义的构造函数意味着将来可以将它的实例标识为一种特定的类型；而这正是构造函数模式胜过工厂模式的地方。**在这个例子中，person1 和person2 之所以同时是Object 的实例，是因为所有对象均继承自Object

**构造函数模式存在的问题**：每个方法都要在每个实例重新创建一遍

#### 6.2.3 原型模式

>在所有实现中都无法访问[[prototype]]或_proto_

**构造函数，原型和实例的关系：**

每个构造函数都有一个原型对象，原型对象都包含一个指向构造函数的指针，而实例都包含一个指向原型对象的内部指针。

**（1）理解原型对象**：prototype是通过调用构造函数而创建的那个对象实例的原型对象

```JS
function Person(){
}
Person.prototype.name="Nicholas";
Person.prototype.age=29;
Person.prototype.job="Software Engineer";
Person.prototype.sayName=function(){
    alert(this.name);
};
var person1 = new Person();
person1.sayName();//"Nicholas"
//person1._proto_为Person.prototype
```

在默认情况下，所有原型对象都会自动获得一个constructor(构造函数)属性，这个属性是一个指向prototype属性所在函数的指针。Person.prototype.constructor指向Person

![原型](D:\Front-End-Note\image\原型.png)

明确一点：**这个连接存在于实例与构造函数的原型对象之间**，而不是存在于实例与构造函数之间（即person1与Person.prototype之间的联系）person1内部有一个指向Person.prototype的指针（`[[prototype]]`或`_proto_`：虽然在所有实现中都无法访问到，但可以通过`isprototypeOf()`来确定是否是某实例的原型对象）

```js
alert(Person.prototype.isPrototypeOf(person1));//true
```

**Object.getPrototypeOf():**可以方便地获取一个对象的原型

```js
alert(Object.getPrototypeOf(person1)==Person.prototype);//true
alert(Object.getPrototypeOf(person1).name);//"Nicholas"
```

当代码要取得某个对象的某个属性时，会先从对象实例本身开始搜索，如果没有找到属性名，则继续搜索指针指向的原型对象。

当为对象实例添加一个属性时，这个属性就会屏蔽原型对象中保存的同名属性，也就是说，添加这个属性值会阻止我们访问原型中的那个属性，但不会修改那个属性;不过**使用delete操作符可以完全删除实例属性**。

```JS
person1.name="Greg";
alert(person1.name);//Greg
alert(person1.hasOwnProperty("name"));//true
delete person1.name;
alert(person1.hasOwnProperty("name"));//false
alert(person1.name);//Nicholas
```

**hasOwnProperty()**方法：检测一个属性是存在于实例中还是原型中

*Object.getOwnPropertyDescriptor()方法只能用于实例属性，要取得原型属性的描述符，必须直接在原型对象上调用Object.getOwnPropertyDescriptor()方法*

**（2）原型与in操作符**

**单独使用**：in操作符只要通过对象能访问到属性就返回true,hasOwnProperty()只在属性存在于实例中时才返回true,因此当in操作符返回true，而hasOwnProperty()返回false时,就说明该属性存在于原型中

**for-in循环**时：返回的是所有能够通过对象访问的，可枚举的属性，其中既包括存在于实例中的属性，也包括在原型中的属性。（**屏蔽了原型中不可枚举属性（即将[[Enumerable]]标记为false属性）的实例属性也会在for-in循环中返回，因为根据规定，所有开发人员定义的属性都是可枚举的——只有在IE8及更早版本中例外**）

**Object.keys()**方法：接收一个对象作为参数，返回一个包含所有**可枚举**属性的**字符串**数组

**Object.getOwnPropertyNames():**接收一个对象作为参数，返回一个包含**所有实例属性**的**字符串**数组

**（3）更简单的原型语法**：用字面量法重写原型对象

```js
function Person(){
}
Person.prototype={
    constructor:Person,
    name:"Nicholas",
    age:29,
    job:"Software Engineer",
    sayName:function(){
        alert(this.name);
    }
}
Object.defineProperty(Person.prototype,"constructor",{
    enumerable:false,
    value:Person
});
var person1 = new Person();
person1.sayName();//"Nicholas"
```

但此时，constructor属性不再指向Person函数，而是**指向Object**,但由于此时constructor属性为自定义的，**可枚举**，因此可以通过Object.defineProperty()将其[[Enumerable]]属性特性改为false。

**（4）原型的动态性**

重写原型对象切断了现有原型与任何之前已经存在的对象实例之间的联系，他们引用的仍然是最初的原型。

**所以只能修改**

**（5）原生对象的原型**

可以修改如Array,Object,String等原生引用类型的原型，如:

```JS
String.prototype.startsWith=function(text){
    return this.indexof(text)==0;
}
```

**（6）原型对象的问题**

**原型对象中的引用类型值会被共享**

#### 6.2.4 组合使用构造函数模式和原型模式（最广泛、认同度最高）

构造函数用于定义实例属性，而原型模式用于定义方法和共享的属性。

#### 6.2.5 动态原型模式（可以把所有信息都封装在构造函数中）

通过检查某个应该存在的方法是否有效，来决定是否需要初始化原型，如：

```JS
function Person(name,age,job){
    this.name=name;
    this.age=age;
    this.job=job;
    if(typeof this.sayName!="function")
        //此时sayName若是不存在或者不是函数类型，都会对原型初始化，而且检查一个属性或方法就可以
    {
        Person.prototype.sayName=function(){
            return this.name;
        }
    }
}
```

#### 6.2.6 寄生（parasitic）构造函数模式（不建议使用）

假如我们想创建一个具有额外方法的特殊数组，由于不能直接修改Array函数，因此可以使用这个模式

```JS
values.push.apply(values,arguments);//arguments是个类数组对象，不能直接push到数组中
```

构造函数在没有返回值的情况下，默认返回新对象实例，而该模式下的构造函数形式类似于工厂模式，在末尾有return语句，可以重写调用构造函数时返回的值，因此，**返回的对象与构造函数以及构造函数的原型属性之间没有关系**，也就是说，构造函数返回的对象与在构造函数外部创建的对象没有什么不同。使用instanceof 没有意义。

#### 6.2.7 稳妥构造函数模式

指的是没有公共属性，最适合在一些安全环境中使用，也与工厂模式很像

与寄生构造函数模式的区别：（1）不引用this对象（寄生模式在声明方法时使用）；（2）不使用new操作符

这种模式下创建的对象除了使用方法，没有其他办法访问属性值。

### 6.3 继承

ES只支持实现继承，而且主要依靠原型链

方法签名：

#### 6.3.1 原型链继承

基本思想：利用原型让一个引用类型继承另一个引用类型的属性和方法

实现本质是重写原型对象，代之以另一个新类型的实例

**（1）别忘记默认的原型**

所有函数的默认原型都是Object的实例

![原型链](D:\Front-End-Note\image\原型链.png)

**（2）确定原型和实例的关系**

instanceof操作符：+构造函数：只要用这个操作符测试实例与原型链中出现过的构造函数，就会返回true

isPrototypeOf()方法:只要是原型链中出现过的原型对象，都可以说是该原型链所派生的实例的原型

**（3）谨慎的定义方法**

给原型添加方法的代码一定要放在替换原型的语句之后，且不能使用字面量方法创建原型方法

**（4）原型链的问题**

第一个问题：包含引用类型值的原型属性会被所有实例共享

第二个问题：在创建子类型的实例时，不能向超类型的构造函数中传递参数

#### 6.3.2 借用构造函数（伪造对象或经典继承）

基本思想：在子类型构造函数的内部调用超类型构造函数（使用call()方法或apply()方法）**屏蔽掉超类型中的引用类型值**

好处：可以传递参数

问题：无法避免构造函数模式存在的问题——方法都在构造函数中定义，无法复用

#### 6.3.3 组合继承（JS中最常用的继承模式，也称伪经典继承）

指的是将原型链和借用构造函数的技术组合到一起，使用原型链实现对原型属性和方法的继承，而使用借用构造函数来实现对实例属性的继承。

而且instanceof()和isPrototypeOf()也能够用于识别基于组合继承创建的对象

```js
function SuperType(name){
    this.name=name;
    this.colors=["red","green","blue"];
}
function SubType(name,age){
    //继承属性
    SuperType.call(this,name);//第二次调用构造函数，SubType实例中传入了第二组name和colors
    this.age=age;
}
SuperType.prototype.sayName=function(){
    alert(this.name);
}
//继承方法
SubType.prototype=new SuperType();//第一次调用构造函数，SubType原型中传入了name和colors
/*
使用寄生式组合继承方法：
function inheriPrototype(subType,superType){
    var prototype=object(superType.prototype);//创建对象：构建超类型原型的一个副本
    prototype.constructer=subType;//增强对象
    subType.prototype=prototype;//指定对象：将新创建的对象（即副本）赋值给子类型的原型
}
inheriPrototype(SubType,SuperType);
*/
SubType.prototype.constructor=SubType;
SubType.prototype.sayAge=function(){
    alert(this.age);
}
var instance1 =new SubType("Nicholas",29);
instance1.colors.push("yellow");
alert(instance1.colors);//"red","green","blue","yellow"
instance1.sayName();//"Nicholas"
instance1.sayAge();//29

var instance2 =new SubType("Greg",27);
alert(instance2.colors);//"red","green","blue"
instance2.sayName();//"Greg"
instance2.sayAge();//27
```

<u>问题：会调用两次超类型构造函数</u>

#### 6.3.4 原型式继承:ES5通过Object.create()方法规范化了原型式继承

```JS
function object(o){
    function F(){}
    F.prototype=o;
    return new F();
}//相当于利用一个构造函数做桥接，
```

思想是基于对象o，创建一个实例，该实例的原型对象o,在包含引用类型属性值方面该方法与原型模式是一样的

ES5新增了Object.create()方法：接受两个参数：一个是用作新对象原型的对象和（可选的）一个新对象定义额外的对象，该对象中每个属性都是通过自己的描述符定义的.

```js
var person={
     name:'Nicholas',
     friends:['Shelby','Court',;Van]
}
var person1=Object.create(person,{
    name:{
        value:'Greg'
    }
})
console.log(person1.name);//'Greg'
```

支持Object.create()方法的浏览器有IE9+、Firefox 4+、Safari 5+、Opera 12+ 和Chrome。**在没有必要兴师动众地创建构造函数**，而只想让一个对象与另一个对象保持类似的情况下，原型式继承是完全可以胜任的。不过别忘了，包含引用类型值的属性始终都会共享相应的值，就像使用原型模式一样。

#### 6.3.5 寄生式继承

思路与寄生构造函数和工厂模式类似，即创建一个仅用于封装继承过程的函数，该函数在内部以某种方式来增强对象（即在内部通过构造函数创建一个实例，再为该对象增加方法，最后返回该对象）

```js
function createAnother(o){
    var clone=Object.create(o);
    clone.sayHi=function(){
        alert("Hi!");
    }
    return clone;
}
var person={
    name:'Nichlas',
    friends:['Tom','Bob','Greg']
};
var another=createAnother(person);
another.sayHi();//'Hi!'
```

在主要考虑对象而不是自定义类型和构造函数的情况下，寄生式继承也是一种有用的模式。前面示范继承模式时使用的Object.create()函数不是必需的；任何能够返回新对象的函数都适用于此模式。

#### 6.3.6 寄生组合式继承（最理想）

用于解决组合继承两次调用构造函数的问题，方法见上方代码，该方法只调用一次SuperType构造函数,且原型链保持不变。

**基本思路：不必为了指定子类型的原型而调用超类型的构造函数，我们所需要的不过是超类型原型的一个副本而已，方法同原型式继承**

### 7.函数表达式



## TypeScript





## ES2015+

### 1. 变量的解构赋值

#### 1.1 数组的解构赋值

ES6允许按照一定模式，从数组和对象中提取值，对变量进行赋值，这被称为解构。如：

```js
let [a,b,c]=[1,2,3];
let [foo,[[bar],baz]]=[1.[[2],3]];
let [,,third]=["foo","bar","baz"];
let [x,y,...z]=['a'];
x//'a'
y//undefined
z//[]
```

本质上，这种写法属于模式匹配，只要等号两边模式相同，左边的变量就会被赋予对应的值。

**（1）如果解构不成功，变量的值就等于undefined**

**（2）如果是不完全解构，即等号左边的模式只匹配一部分等号右边的数组，解构依然可以成功。**

**（3）如果等号右边不是数组（或者严格地说，不是可遍历的结构Iterator），那么将会报错；对于Set结构也可以使用数组的解构赋值**

>**1. Iterator:**
>
>
>
>**2. Set**

**（4）解构赋值允许指定默认值**

注意，ES6 内部使用严格相等运算符（`===`），判断一个位置是否有值。所以，只有当一个数组成员严格等于`undefined`，默认值才会生效。

### 2. Symbol

#### 2.1 概述：

ES6 引入了一种新的原始数据类型`Symbol`，表示独一无二的值。它是 JavaScript 语言的第七种数据类型，前六种是：`undefined`、`null`、布尔值（Boolean）、字符串（String）、数值（Number）、对象（Object）。

**（1）Symbol函数的参数只是对当前Symbol值的描述，因此相同参数的Symbol函数的返回值是不相等的**

**（2）Symbol值不能与其他类型的值进行运算，但可以通过String()显式转换为字符串，也可以通过Boolean()显式转换为布尔值，但不能转换为数值**

#### 2.2 Symbol.prototype.description

获取Symbol值的描述，即传进去的描述参数（ES2019）

#### 2.3 作为属性名的Symbol

（1）可以通过方括号结构和Object.defineProperty将对象的属性名设置为Symbol值；**Symbol值作为对象属性名时，不能用点运算符，点运算符的属性名是个字符串；**

（2）Symbol值作为属性名时，该属性是公开属性，不是私有属性；

#### 2.4 实例：消除魔术字符串

魔术字符串：指在代码之中多次出现、与代码形成强耦合的某一个具体的字符串或者数值。风格良好的代码，应该尽量消除魔术字符串，改由含义清晰的变量代替，**对于值为什么并不重要，只需要不与其他属性名冲突的属性名可以使用Symbol值**

#### 2.5 属性名的遍历

Symbol 作为属性名，遍历对象的时候，该属性不会出现在`for...in`、`for...of`循环中，也不会被`Object.keys()`、`Object.getOwnPropertyNames()`、`JSON.stringify()`返回。

（1）但是，它也不是私有属性，有一个**`Object.getOwnPropertySymbols()`**方法，可以获取指定对象的所有 Symbol 属性名。该方法返回一个数组，成员是当前对象的所有用作属性名的 Symbol 值。

（2）**`Reflect.ownkeys()`**:可以返回所有类型的键名，包括常规键名和Symbol键名

（3）由于以 Symbol 值作为键名，不会被常规方法遍历得到。我们可以利用这个特性，为对象定义一些非私有的、但又希望只用于内部的方法。

#### 2.6 Symbol.for(),Symbol.keyFor()

（1）`Symbol.for()`

有时，我们希望重新使用同一个 Symbol 值，**`Symbol.for()`**方法可以做到这一点。它接受一个字符串作为参数，然后搜索有没有以该参数作为描述的 Symbol 值。如果有，就返回这个 Symbol 值，否则就新建一个以该字符串为描述的 Symbol 值，并将其注册到全局，即**已登记，`Symbol.for()`这个登记特性，可以用在不同的iframe或service worker中取到同一个值**。

**而由于`Symbol()`方法没有登记机制，每次调用都会返回一个不同的值。**

（2）`Symbol.keyFor()`:返回一个已登记的Symbol类型值得key

```js
let s1=Symbol.for('foo');
Symbol.keyFor(s1);//'foo'
let s2=Symbol('foo');
Symbol.keyFor(s2);//undefined
```

#### 2.7 实例：模块的Singleton模式

Singleton 模式指的是调用一个类，任何时候返回的都是同一个实例。

#### 2.8 内置的Symbol值

除了定义自己使用的 Symbol 值以外，ES6 还提供了 11 个内置的 Symbol 值，指向语言内部使用的方法。

**2.8.1 Symbol.hasInstance:判断是否是某对象的实例**

对象的Symbol.hasInstance属性指向一个内部方法，当其他对象使用instanceof运算符，判断是否为该对象的实例时，会调用这个方法。比如`foo instanceof Foo`在语言内部，实际调用的是`Foo[Symbol.hasInstance](foo)`

**2.8.2 Symbol.isConcatSpreadable**

对象的`Symbol.isConcatSpreadable`属性等于一个布尔值，表示该对象用于`Array.prototype.concat()`时，是否可以展开：

（1）数组的默认行为是可以展开，`Symbol.isConcatSpreadable`默认等于`undefined`,该属性等于true时，也有展开的效果，等于false时不能展开；

（2）类似数组的对象正好相反，默认不展开，只有当 `Symbol.isConcatSpreadable` 属性设为true才能展开。

**2.8.3 Symbol.species**

**2.8.4 Symbol.match**

**2.8.5 Symbol.replace**

**2.8.6 Symbol.search**

**2.8.7 Symbol.split**

**2.8.8 Symbol.iterator**

**2.8.9 Symbol.toPrimitive**

**2.8.10 Symbol.toStringTag**

**2.8.11 Symbol.unscopables**



### 3. Set和Map数据结构

#### 3.1 Set

set类似于数组，但是成员的值都是唯一的，没有重复的值

**注意：**

（1）向 Set 加入值的时候，不会发生类型转换，所以`5`和`"5"`是两个不同的值。Set 内部判断两个值是否不同，使用的算法叫做“Same-value-zero equality”，它类似于精确相等运算符（`===`），主要的区别是向 Set 加入值时认为`NaN`等于自身，而精确相等运算符认为`NaN`不等于自身。

（2）两个对象总是不相等的

（3）new Set()可用与去除数组中重复的元素和字符串中重复的字符

**Set实例的属性和方法：**

- `Set.prototype.constructor`：构造函数，默认就是`Set`函数。
- `Set.prototype.size`：返回`Set`实例的成员总数。

Set 实例的方法分为两大类：操作方法（用于操作数据）和遍历方法（用于遍历成员）。下面先介绍四个操作方法。

- `Set.prototype.add(value)`：添加某个值，返回 Set 结构本身。
- `Set.prototype.delete(value)`：删除某个值，返回一个布尔值，表示删除是否成功。
- `Set.prototype.has(value)`：返回一个布尔值，表示该值是否为`Set`的成员。
- `Set.prototype.clear()`：清除所有成员，没有返回值。
- `Array.from()：将Set结构转为数组`

Set 结构的实例有四个遍历方法，可以用于遍历成员。

- `Set.prototype.keys()`：返回键名的遍历器
- `Set.prototype.values()`：返回键值的遍历器
- `Set.prototype.entries()`：返回键值对的遍历器，输出一个数组，它的两个成员完全相等
- `Set.prototype.forEach()`：使用回调函数遍历每个成员

**Set结构没有键名，只有键值（或者说键名和键值是同一个值），所以keys方法和values方法的行为完全一致**

#### 3.2 WeakSet

WeakSet结构与Set类似，也是不重复的值的集合。但是它与Set有两个区别：**WeakSet的成员只能是对象，而不能是其他类型的值**。

**WeakSet 中的对象都是弱引用**，即垃圾回收机制不考虑 WeakSet 对该对象的引用，也就是说，如果其他对象都不再引用该对象，那么垃圾回收机制会自动回收该对象所占用的内存，不考虑该对象还存在于 WeakSet 之中。

这是因为垃圾回收机制依赖引用计数，如果一个值的引用次数不为`0`，垃圾回收机制就不会释放这块内存。结束使用该值之后，有时会忘记取消引用，导致内存无法释放，进而可能会引发内存泄漏。WeakSet 里面的引用，都不计入垃圾回收机制，所以就不存在这个问题。因此，WeakSet 适合临时存放一组对象，以及存放跟对象绑定的信息。只要这些对象在外部消失，它在 WeakSet 里面的引用就会自动消失。

由于上面这个特点，WeakSet 的成员是不适合引用的，因为它会随时消失。另外，由于 WeakSet 内部有多少个成员，取决于垃圾回收机制有没有运行，运行前后很可能成员个数是不一样的，而垃圾回收机制何时运行是不可预测的，因此 **ES6 规定 WeakSet 不可遍历**。

WeakSet 结构有以下三个方法。

- **WeakSet.prototype.add(value)**：向 WeakSet 实例添加一个新成员。
- **WeakSet.prototype.delete(value)**：清除 WeakSet 实例的指定成员。
- **WeakSet.prototype.has(value)**：返回一个布尔值，表示某个值是否在 WeakSet 实例之中。

#### 3.3 Map

ES6 提供了 Map 数据结构。它类似于对象，也是键值对的集合，但是“键”的范围不限于字符串，各种类型的值（包括对象）都可以当作键。也就是说，Object 结构提供了“字符串—值”的对应，Map 结构提供了“值—值”的对应，是一种更完善的 Hash 结构实现。如果你需要“键值对”的数据结构，Map 比 Object 更合适。

**实例的属性和操作方法：**

- **size属性：返回Map结构的成员总数**
- **`Map.prototype.set(key,value)`：**返回整个Map结构，因此可以采用链式写法
- **`Map.prototype.get(key)`**
- **`Map.prototype.has(key)`**：返回一个布尔值，表示某个键是否在当前Map对象之中。
- **`Map.prototype.delete(key)`**：删除成功返回true，删除失败返回false
- **`Map.prototype.clear()`**：清除所有成员，没有返回值

Map 结构原生提供三个遍历器生成函数和一个遍历方法。

- `Map.prototype.keys()`：返回键名的遍历器。
- `Map.prototype.values()`：返回键值的遍历器。
- `Map.prototype.entries()`：返回所有成员的遍历器。：Map结构的默认遍历器接口
- `Map.prototype.forEach()`：遍历 Map 的所有成员。

需要特别注意的是，Map 的遍历顺序就是插入顺序。

#### 3.4 WeakMap

**（1）WeakMap只接受对象作为键名（null除外），不接受其他类型的值作为键名；**

**（2）WeakMap的键名所指向的对象，不计入垃圾回收机制**

**（3）只有四个方法可用：`get(),set(),has(),delete()`**

### 4. Iterator 和 for..of循环

#### 4.1 Iterator（遍历器）的概念

**4.1.1 JS原有的表示“集合”的数据结构：**

Array,Object,Map,Set

**4.1.2 Iterator的作用：**

（1）为各种数据结构提供一个统一的、简便的访问接口；

（2）使数据结构的成员能够按某种次序排列

（3）ES6创造了一种新的`for..of`循环，Iterator接口主要供`for..of`消费

#### 4.2 默认Iterator接口

一种数据结构只要部署了Iterator接口，我们就称这种数据结构是“可遍历的”（Iterable）

**凡是部署了Symbol.iterator属性的数据结构，就称为部署了遍历器接口，调用这个接口就会返回一个遍历器对象**

原生具备Iterator接口的数据结构如下：

- Array
- Map
- Set
- String
- TypedArray
- 函数的arguments对象
- NodeList对象



### 5 Class

#### 5.1 简介

基本上，ES6的class可以看做只是一个语法糖，它的绝大部分功能，ES5 都可以做到，新的`class`写法只是让对象原型的写法更加清晰、更像面向对象编程的语法而已。

**（1）类的数据类型就是函数，类本身就指向构造函数，而类中定义的方法实际上是定义在构造函数的prototype对象上的；**

**（2）`Object.assign`方法可以很方便地一次向类添加多个方法（向类的原型中添加）;**

**（3）类的内部定义的所有方法都是不可枚举的(non-enumerable);**

>**获取对象属性的方法：**
>
>**in操作符单独使用**：in操作符只要通过对象能访问到属性就返回true, hasOwnProperty()只在属性存在于实例中时才返回true,因此当in操作符返回true，而hasOwnProperty()返回false时,就说明该属性存在于原型中
>
>**for-in循环**时：返回的是所有能够通过对象访问的，可枚举的属性，其中既包括存在于实例中的属性，也包括在原型中的属性。（**屏蔽了原型中不可枚举属性（即将[[Enumerable]]标记为false属性）的实例属性也会在for-in循环中返回，因为根据规定，所有开发人员定义的属性都是可枚举的——只有在IE8及更早版本中例外**）
>
>**Object.keys()**方法：接收一个对象作为参数，返回一个包含所有**可枚举**属性的**字符串**数组
>
>**Object.getOwnPropertyNames():**接收一个对象作为参数，返回一个包含**所有实例属性**的**字符串**数组
>
>**在调用Object.defineProperty()方法创建一个新属性时，如果不指定，configurable，enumerable和writable特性的默认值都是false**,如果调用Object.defineProperty()方法是修改已定义属性的特性，则无此限制。

**5.1.1 constructor方法**

`constructor`方法是类的默认方法，通过`new`命令生成对象实例时，自动调用该方法。一个类必须有`constructor`方法，如果没有显式定义，一个空的`constructor`方法会被默认添加。

constructor方法也可以返回其他对象，与普通构造函数相似，若没有return返回值则返回实例对象即this

**类与普通构造函数的区别：类必须使用new调用，否则会报错，而普通构造函数可以不用new执行。**

**5.1.2 类的实例**

使用new生成类实例

**5.1.3 取值函数（getter）和存值函数（setter）**

与 ES5 一样，在“类”的内部可以使用`get`和`set`关键字，对某个属性设置存值函数和取值函数，拦截该属性的存取行为。

**5.1.4 注意点：**

**（1）严格模式**：类和模块的内部，默认就是严格模式，所以不需要使用`use strict`指定运行模式。只要你的代码写在类或模块之中，就只有严格模式可用。考虑到未来所有的代码，其实都是运行在模块之中，所以 ES6 实际上把整个语言升级到了严格模式。

**（2）不存在提升**

**（3）name属性：**name属性总是返回紧跟在class关键字后面的类名

**（4）Generator方法：**如果某个方法之前加上星号（`*`），就表示该方法是一个 Generator 函数。

**（5）this的指向：**

类的方法内部如果含有`this`，它默认指向类的实例。但是，必须非常小心，一旦单独使用该方法，很可能报错。

**解决方法：**

- 在构造方法中绑定this
- 使用箭头函数：箭头函数内部的this总是指向定义时所在的对象。
- 使用Proxy,获取方法的时候，自动绑定this

#### 5.2 静态方法：

类相当于实例的原型，所有在类中定义的方法，都会被实例继承。如果在一个方法前，加上`static`关键字，就表示该方法不会被实例继承，而是直接通过类来调用，这就称为“静态方法”。（**js中无需实例化就可以调用的方法叫做静态方法。**）

**（1）如果静态方法包含`this`关键字，这个`this`指的是类，而不是实例。**

**（2）静态方法可以与非静态方法重名**

**（3）父类的静态方法，可以被子类继承**

**（4）静态方法也可以从super对象上调用**

#### 5.3 实例属性的新写法

（1）定义在constructor()方法里面的this上面

（2）直接写在类的最顶层

#### 5.4 静态属性

静态属性指的是 Class 本身的属性，即`Class.propName`，而不是定义在实例对象（`this`）上的属性。

#### 5.5 私有方法和私有属性

**5.5.1 私有方法：**

**现有的解决方案：**

（1）在命名上加以区别：如公有：`foo(baz)`，私有：`_bar(baz)`；**不保险：外部可以调用**

（2）将私有函数移到类的外面，类内部的公有函数用apply,call调用私有函数；

（3）利用Symbol值得唯一性，将私有方法的名字命名为一个Symbol值（**但是Symbol值得属性可以通过Reflect.ownKeys()获取到**）

**5.5.2 私有属性**

目前，有一个[提案](https://github.com/tc39/proposal-private-methods)，为`class`加了私有属性。方法是在属性名之前，使用`#`表示。私有方法也可以用这个符号标识。

>私有属性，私有方法：
>
>只有类内部可以访问，外部无法调用，实例内部也可以访问调用
>
>静态属性，静态方法：
>
>只能使用类本身调用，实例无法获取调用，也可以在类的外部调用

#### 5.6 new.target属性

`new`是从构造函数生成实例对象的命令。ES6 为`new`命令引入了一个`new.target`属性，该属性一般用在构造函数之中，返回`new`命令作用于的那个构造函数。如果构造函数不是通过`new`命令或`Reflect.construct()`调用的，`new.target`会返回`undefined`，因此这个属性可以用来确定构造函数是怎么调用的。

### 6. Class的继承



### 7. 对象的扩展

>如何单独使用某类的方法？
>
>

#### 7.1 属性的简洁表示法

ES6 允许在大括号里面，直接写入变量和函数，作为对象的属性和方法。

**注意：简写的对象方法不能用作构造函数，会报错**

#### 7.2 属性名表达式

ES6允许字面量定义对象时，用表达式（置于方括号中）作为对象的属性名或方法名。

**注意：属性名表达式与简洁表示法不能同时使用，会报错；**

**注意：属性名表达式如果是一个对象，默认情况下会自动将对象转为字符串[object Object]**

#### 7.3 方法的name属性

函数的`name`属性，返回函数名，对象方法也是函数，因此也有name属性

**特殊情况：**

（1）如果对象的方法使用了取值函数（`getter`）和存值函数（`setter`），则`name`属性不是在该方法上面，而是该方法的属性的描述对象的`get`和`set`属性上面，返回值是方法名前加上`get`和`set`。

```js
const obj={
    get foo() {},
    set foo(x) {}
};
obj.foo.name;
//TypeError:Cannot read Property 'name' of undefined
const descriptor=Object.getOwnPropertyDescriptor(obj,'foo');
descriptor.get.name;//'get foo'
descriptor.set.name;//'set foo'
```

（2）`bind`方法创造的函数，`name`属性返回`bound`加上原函数的名字；

（3）`Function`构造函数创造的函数，`name`属性返回`anonymous`（匿名）

（4）如果对象的方法是一个Symbol值，那么name属性返回的是这个Symbol值得描述。

#### 7.4 属性的可枚举性和遍历

目前，有四个操作会忽略`enumerable`为`false`的属性。

- `for...in`循环：只遍历对象自身的和继承的可枚举的属性。
- `Object.keys()`：返回对象自身的所有可枚举的属性的键名。
- `JSON.stringify()`：只串行化对象自身的可枚举的属性。
- `Object.assign()`： 忽略`enumerable`为`false`的属性，只拷贝对象自身的可枚举的属性。
- ES6规定，所有Class的原型的方法都是不可枚举的（即类中定义的方法）

**属性的遍历:ES6中一共有5种方法可以遍历对象的属性**

**（1）for...in**

`for...in`循环遍历对象自身的和继承的可枚举属性（不含 Symbol 属性）。

**（2）Object.keys(obj)**

`Object.keys`返回一个数组，包括对象自身的（不含继承的）所有可枚举属性（不含 Symbol 属性）的键名。

**（3）Object.getOwnPropertyNames(obj)**

`Object.getOwnPropertyNames`返回一个数组，包含对象自身的所有属性（不含 Symbol 属性，但是包括不可枚举属性）的键名。

**（4）Object.getOwnPropertySymbols(obj)**

`Object.getOwnPropertySymbols`返回一个数组，包含对象自身的所有 Symbol 属性的键名。

**（5）Reflect.ownKeys(obj)**

`Reflect.ownKeys`返回一个数组，包含对象自身的所有键名，不管键名是 Symbol 或字符串，也不管是否可枚举。

以上的 5 种方法遍历对象的键名，都遵守同样的属性遍历的次序规则。

- 首先遍历所有数值键，按照数值升序排列。
- 其次遍历所有字符串键，按照加入时间升序排列。
- 最后遍历所有 Symbol 键，按照加入时间升序排列。

#### 7.5 super关键字

`this`关键字总是指向函数所在的当前对象，ES6新增了另一个类似的关键字`super`，指向当前对象的原型对象

**注意：`super`关键字表示原型对象时，只能用在对象的方法之中，用在其他地方都会报错（目前，只能用在对象方法的简写方法中才能让JavaScript引擎确认，定义的是对象的方法）**

`super.foo`等同于`Object.getPrototypeOf(this).foo`（属性）或`Object.getPrototypeOf(this).foo.call(this)`（方法）

#### 7.6 对象的扩展运算符

**7.6.1 解构赋值：**对象的解构赋值用于从一个对象取值，相当于将目标对象自身的所有可遍历的（enumerable）、但尚未被读取的属性，分配到指定的对象上面。所有的键和它们的值，都会拷贝到新对象上面。

扩展运算符：`...`：用于取出参数对象的所有可遍历属性，拷贝到当前对象之中（相当于使用`Object.assign()`方法）

**注意：**

**（1）解构赋值要求等号右边是一个对象，所以如果等号右边是undefined或null，就会报错，因为它们无法转为对象**

**（2）解构赋值必须是最后一个参数，否则会报错**

**（3）解构赋值的拷贝是浅拷贝，即如果一个键的值是复合类型的值（数组、对象、函数），那么解构赋值拷贝的是这个值得引用，而不是这个值得副本**

**（4）扩展运算符的解构赋值，不能复制继承自原型对象的属性**(与`Object.assign(target,source1,source2...)`类似)

>**1.`Object.assign(target,source1,source2...)`：**
>
>- 浅拷贝（即只是复制了引用类型值得指针，拷贝副本的改变会引起原值的改变）
>- 不拷贝继承来的属性，也不拷贝不可枚举的属性（`enumerable:false`）,但可以拷贝Symbol值的属性
>- 后面参数会覆盖前面参数相同属性名的属性值
>
>**2. `Object.create()和 new Object()`：**
>
>`Object.create(proto,[propertiesObject])`
>
>- proto : 必须。表示新建对象的原型对象，即该参数会被赋值到目标对象(即新对象，或说是最后返回的对象)的原型上。该参数可以是`null`， `对象`， 函数的`prototype属性` （创建空的对象时需传null , 否则会抛出`TypeError`异常）。
>- propertiesObject : 可选。 添加到新创建对象的可枚举属性（**即其自身的属性，而不是原型链上的枚举属性**）对象的属性描述符以及相应的属性名称。这些属性对应[`Object.defineProperties()`](https://links.jianshu.com/go?to=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh-CN%2Fdocs%2FWeb%2FJavaScript%2FReference%2FGlobal_Objects%2FObject%2FdefineProperties)的第二个参数。
>- 返回值：
>  在指定原型对象上添加新属性后的对象。
>
>（1）new Object()是通过构造函数创建对象，添加的属性是在自身实例下，Object.create()是以传进来的参数为原型创建了一个实例，添加的对象是在原型下；
>
>（2）通过Object.create()的第二个参数传进来的属性[[Configurable]],[[Enumerable]],[[Writable]]均为false,而通过new Object()或字面量传进来的属性[[Configurable]],[[Enumerable]],[[Writable]]均为true;
>
>（3）通过构造函数或字面量方法创建的对象原型为Object.prototype,而通过Object.create()创建的对象原型为null
>
>

**（5）扩展运算符的参数对象之中，如果有取值函数get，这个函数会执行的**

#### 7.7 链判断运算符

#### 7.8 Null判断运算符

### 8. 对象的新增方法

### 9.Module：

完全可以取代CommonJS和AMD规范，成为服务器和浏览器通用的模块解决方案

**ES6模块的设计思想是尽量的静态化，使得编译时就能确定模块的依赖关系，以及输入输出的变量。CommonJS 和 AMD 模块，都只能在运行时确定这些东西。比如，CommonJS 模块就是对象，输入时必须查找对象属性。**

>AMD在加载完成定义（`define`）好的模块就会立即执行，所有执行完成后，遇到`require`才会执行主逻辑。（提前加载）
> CMD在加载完成定义（`define`）好的模块，仅仅是下载不执行，在遇到`require`才会执行对应的模块。（按需加载）
> AMD用户体验好，因为没有延迟，CMD性能好，因为只有用户需要的时候才执行。
>
>

ES6模块不是对象，而是通过`export`命令显示指定输出的代码，再通过`import`命令输入。这种加载称为"编译时加载"

#### 9.1 Module的语法

模块功能主要由两个命令构成：

**`export`：用于规定模块的对外接口**

**`import`：用于输入其他模块提供的功能**

##### 9.1.1 严格模式

ES6的模块自动采用严格模式，不管你有没有在模块头部加上‘use strict’

严格模式主要有以下限制。

- 变量必须声明后再使用
- 函数的参数不能有同名属性，否则报错
- 不能使用`with`语句
- 不能对只读属性赋值，否则报错
- 不能使用前缀 0 表示八进制数，否则报错
- 不能删除不可删除的属性，否则报错
- 不能删除变量`delete prop`，会报错，只能删除属性`delete global[prop]`
- `eval`不会在它的外层作用域引入变量
- `eval`和`arguments`不能被重新赋值
- `arguments`不会自动反映函数参数的变化
- 不能使用`arguments.callee`
- 不能使用`arguments.caller`
- 禁止`this`指向全局对象
- 不能使用`fn.caller`和`fn.arguments`获取函数调用的堆栈
- 增加了保留字（比如`protected`、`static`和`interface`）

##### 9.1.2 export命令



#### 9.2 Module加载使用

### 10. 数组的扩展

#### 10.1 扩展运算符`...`：

可以将一个数组转为用逗号分隔的参数数列，主要用于函数调用

#### 10.2 Array.from()

`Array.from`方法用于将两类对象转为真正的数组：类似数组的对象（array-like object）和可遍历（iterable）的对象（包括 ES6 新增的数据结构 Set 和 Map）。

**常用的类似数组的对象：DOM操作返回的NodeList集合；函数内部的arguments对象**

扩展运算符[...arguments]也可以将某些数据结构转为数组：**扩展运算符背后调用的是遍历器接口（Symbol.iterator），如果一个对象没有部署这个接口就无法转换**

只要是部署了 Iterator 接口的数据结构，`Array.from`都能将其转为数组。`Array.from`方法还支持类似数组的对象。所谓类似数组的对象，本质特征只有一点，即必须有`length`属性。因此，任何有`length`属性的对象，都可以通过`Array.from`方法转为数组，而此时扩展运算符就无法转换。

**对于还没有部署该方法的浏览器，可以用`Array.prototype.slice`方法替代。**

```js
const toArray(obj){
    (()=>Array.from?Array.from:obj=>[].slice.call(obj))(obj);
}
```

**`Array.from`还可以接受第二个参数，作用类似于数组的`map`方法，用来对每个元素进行处理，将处理后的值放入返回的数组。**

如果`map`函数里面用到了`this`关键字，还可以传入`Array.from`的第三个参数，用来绑定`this`。

#### 10.3 Array.of():用于将一组值转换为数组

主要是弥补了构造函数Array()的不足，**`Array.of`总是返回参数值组成的数组。如果没有参数，就返回一个空数组。**

#### 10.4 Array.copyWithin()

数组实例的`copyWithin()`方法，在当前数组内部，将指定位置的成员复制到其他位置（会覆盖原有成员），然后返回当前数组。也就是说，使用这个方法，会修改当前数组。

```javascript
Array.prototype.copyWithin(target, start = 0, end = this.length)
```

它接受三个参数。

- target（必需）：从该位置开始替换数据。如果为负值，表示倒数。
- start（可选）：从该位置开始读取数据，默认为 0。如果为负值，表示从末尾开始计算。
- end（可选）：到该位置前停止读取数据，默认等于数组长度。如果为负值，表示从末尾开始计算。

这三个参数都应该是数值，如果不是，会自动转为数值。

#### 10.5 数组实例的find()和findIndex()

数组实例的`find`方法，用于找出第一个符合条件的数组成员。它的参数是一个回调函数，所有数组成员依次执行该回调函数，直到找出第一个返回值为`true`的成员，然后返回该成员。如果没有符合条件的成员，则返回`undefined`。

`find`方法的回调函数可以接受三个参数，依次为当前的值、当前的位置和原数组。

数组实例的`findIndex`方法的用法与`find`方法非常类似，返回第一个符合条件的数组成员的位置，如果所有成员都不符合条件，则返回`-1`。

**这两个方法都可以接受第二个参数，用来绑定回调函数的`this`对象。;**

**另外，这两个方法都可以发现`NaN`，弥补了数组的`indexOf`方法的不足。`indexOf`方法无法识别数组的`NaN`成员，但是`findIndex`方法可以借助`Object.is`方法做到。**

>**`Object.is(value1,value2)`**
>
>`Object.is()` 判断两个值是否相同。如果下列任何一项成立，则两个值相同：
>
>- 两个值都是 `undefined`
>- 两个值都是 `null`
>- 两个值都是 `true` 或者都是 `false`
>- 两个值是由相同个数的字符按照相同的顺序组成的字符串
>- 两个值指向同一个对象
>- 两个值都是数字并且
>  - 都是正零 `+0`
>  - 都是负零 `-0`
>  - 都是 `NaN`
>  - 都是除零和`NaN`外的其它同一个数字
>
>这种相等性判断逻辑和传统的 `==` 运算不同，`==`运算符会对它两边的操作数做隐式类型转换（如果它们类型不同），然后才进行相等性比较，（所以才会有类似 `"" == false` 等于 `true` 的现象），但 `Object.is` 不会做这种类型转换。
>
>这与 `===`运算符的判定方式也不一样。`===` 运算符（和`==` 运算符）将数字值 `-0` 和 `+0` 视为相等，并认为 `Number.NaN` 不等于`NaN`。

#### 10.6 数组实例的fill()：使用给定值填充一个数组

`fill`方法还可以接受第二个和第三个参数，用于指定填充的起始位置和结束位置。

**注意，如果填充的类型为对象，那么被赋值的是同一个内存地址的对象，而不是深拷贝对象。**

#### 10.7 数组实例的`entries()`,`keys()`和`values()`

ES6 提供三个新的方法——`entries()`，`keys()`和`values()`——用于遍历数组。它们都返回一个遍历器对象（详见《Iterator》一章），可以用`for...of`循环进行遍历，唯一的区别是`keys()`是对键名的遍历、`values()`是对键值的遍历，`entries()`是对键值对的遍历。

#### 10.8 数组实例的includes()

`Array.prototype.includes`方法返回一个布尔值，表示某个数组是否包含给定的值，与字符串的`includes`方法类似。ES2016 引入了该方法。

该方法的第二个参数表示搜索的起始位置，默认为`0`。如果第二个参数为负数，则表示倒数的位置，如果这时它大于数组长度（比如第二个参数为`-4`，但数组长度为`3`），则会重置为从`0`开始。

**`Array.includes()`与`Array.indexOf()`**

`indexOf`方法有两个缺点:

- 不够语义化，它的含义是找到参数值的第一个出现位置，所以要去比较是否不等于`-1`，表达起来不够直观。
- 它内部使用严格相等运算符（`===`）进行判断，这会导致对`NaN`的误判。

#### 10.9 数组实例的flat(),flatMap()

数组的成员有时还是数组，`Array.prototype.flat()`用于将嵌套的数组“拉平”，变成一维的数组。该方法返回一个新数组，对原数据没有影响。

- 参数为想要拉平的层数，如果不管有多少层嵌套，都要转成一维数组，可以用`Infinity`关键字作为参数。
- 如果原数组有空位，`flat()`方法会跳过空位。

**`flatMap()`方法对原数组的每个成员执行一个函数（相当于执行`Array.prototype.map()`），然后对返回值组成的数组执行`flat()`方法。该方法返回一个新数组，不改变原数组。**

- `flatMap()`只能展开一层数组
- `flatMap()`方法的参数是一个遍历函数，该函数可以接受三个参数，分别是当前数组成员、当前数组成员的位置（从零开始）、原数组
- `flatMap()`方法还可以有第二个参数，用来绑定遍历函数里面的`this`。

#### 10.10 数组的空位

ES5和ES6对数组空位的处理不同

ES5 对空位的处理，已经很不一致了，大多数情况下会忽略空位。

- `forEach()`, `filter()`, `reduce()`, `every()` 和`some()`都会跳过空位。
- `map()`会跳过空位，但会保留这个值
- `join()`和`toString()`会将空位视为`undefined`，而`undefined`和`null`会被处理成空字符串。

**ES6则是明确将空位转为undefined**

- `Array.from`和扩展运算符`...`会将数组的空位转为`undefined`
- `copyWithin()`会连空位一起拷贝
- `fill()`会将空位视为正常的数组位置
- `for...of`循环也会遍历空位
- `entries()`、`keys()`、`values()`、`find()`和`findIndex()`会将空位处理成`undefined`。

**由于空位的处理规则非常不统一，所以应该避免出现空位**

#### 10.11 Array.prototype.sort()的排序稳定性

排序稳定性（stable sorting）是排序算法的重要属性，指的是排序关键字相同的项目，排序前后的顺序不变。

常见的排序算法之中，插入排序、合并排序、冒泡排序等都是稳定的，堆排序、快速排序等是不稳定的。不稳定排序的主要缺点是，多重排序时可能会产生问题。



## 《学习JavaScript数据结构与算法》

### 2. ECMAScript和TypeScript概述



