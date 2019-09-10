## 1.JavaScript简介

##### 1.1 ECMA-262：

ECMAScript脚本语言标准，与Web浏览器没有依赖关系，常见的Web浏览器只是JavaScript可能实现的宿主环境之一，宿主环境不仅提供基本的ECMAScript实现，同时也会提供该语言的扩展，以便语言与宿主环境之间交互。而这些扩展——如DOM，则利用ECMAScript的核心类型和语法提供更多更具体的功能，以便实现针对环境的操作。其他宿主环境包括Node和Adobe Flash.

##### 1.2 一个完整的JavaScript实现应该由下列三个不同的部分组成：

（1）核心（ECMAScript）：由ECMA-262定义，提供核心语言功能

（2）文档对象模型(DOM)：提供访问和操作网页内容的方法和接口，DOM1---DOM2---DOM3

DOM不只是针对JavaScript的，很多别的语言也都实现了DOM（如SVG,MathML,SMIL都基于XML）

（3）浏览器对象模型（BOM）：提供与浏览器交互的方法和接口，HTML5将很多BOM功能写入了正式规范

大多数浏览器在提及对JavaScript的支持情况时，一般都以ECMAScript兼容性和对DOM的支持情况为准。

## 2 .在HTML中使用JavaScript



## 3.基本概念

## 4 变量、作用域和内存问题

## 5.引用类型

对象是某个特定引用类型的实例

#### 5.1 Object类型

创建Object实例的方法：  

使用new操作符后跟Object构造函数：var person= new Object()  

使用对象字面量表示法  

访问属性的方法：点表示法和方括号表示法

#### 5.2 Array类型

##### 5.2.1 

#### 5.3 RegExp类型

##### 5.3.1 模式：

g:全局模式   i:不区分大小写模式    m:多行模式

##### 5.3.2 创建：注意双重转义

使用字面量模式： var pattern1 = / [bc]at/i;

使用构造函数创建：var pattern1 = new RegExp("[bc]at","i")

ES3中，正则表达式字面量始终会共享同一个RegExp实例，而使用构造函数创建的没一个新的RegExp实例都是一个新实例。

##### 5.3.3 符号：<https://www.w3school.com.cn/jsref/jsref_obj_regexp.asp>

\d:数字    \s：空格或者Tab等空白符    \w：字母   . :任意字符

*：>=0    +：>=1      ?:1或者0    {n}:n个字符   {n,m}:n到m个字符

[]:表示范围：可以进行更精确地匹配  

A|B：A或者B

^:表示行的开头      $:表示行的结束

##### 5.3.4实例方法：

（1）RegExpObject.compile(RegExp):用于在脚本执行过程中编译正则表达式,也可用于改变和重新编译正则表达式。

（2）RegExpObject.exec(string):如果 exec() 找到了匹配的文本，返回一个数组，其中存放匹配的结果。如果未找到匹配，则返回值为null。此数组的第 0 个元素是与正则表达式相匹配的文本，第 1 个元素是与 RegExpObject 的第 1 个子表达式相匹配的文本（如果有的话），第 2 个元素是与 RegExpObject 的第 2 个子表达式相匹配的文本（如果有的话），以此类推。

返回的数组包含两个额外属性：

index:表示匹配项在字符串中的位置  ；   input:表示应用正则表达式的字符串

对于exec()方法而言，即使在模式中设置了全局标志（g），它每次也只返回一个匹配项。

在不设置全局标志的情况下，在同一个字符串上多次调用exec()将始终返回第一个匹配项的信息，而RegExpObject的lastIndex属性依旧为0；

而在设置全局标志的情况下，每次调用exec()则都会在字符串中继续查找新匹配项，RegExpObject的lastIndex属性依旧为为匹配文本的最后一个字符的下一个位置，当 exec() 再也找不到匹配的文本时，它将返回 null，并把 lastIndex 属性重置为 0。

（3）RegExpObject.test(string):用于检测一个字符串是否匹配某个模式.(只想知道是否匹配的情况)

##### 5.3.5 RegExp实例继承的方法：

（1）toLocaleString()和toString()方法都会返回正则表达式的字面量，与创建正则表达式的方式无关

```js
var pattern = new RegExp("\\[bc\\]at","gi");
alert(pattern.toLocaleString());/\[bc\]at/gi
alert(pattern.toString());/\[bc\]at/gi
```

（2）valueof()方法返回正则表达式本身

##### 5.3.6 支持正则表达式的String对象的方法

#### 5.4 Date类型



#### 5.5 Function类型

#### 5.6基本包装类型

ECMAScript提供了3个特殊的引用类型：Boolean,Number和String,每当读取一个基本类型值的时候，后台就会创建一个对应的基本包装类型的对象，从而让我们能够调用一些方法来操作这些数据。

引用类型与基本包装类型的主要区别就是对象的生存期。使用new操作符创建的引用类型的实例，在执行流离开当前作用域之前都一直保存在内存中。而自动创建的基本包装类型的对象，则只存在于一行代码的执行瞬间，然后立即被销毁。所以我们不能在运行时为基本类型值添加属性和方法。

对基本包装类型的实例调用typeof会返回“object"，而且所有基本包装类型的对象在转换为布尔值时都是true

在使用typeof 和instanceof操作符测试基本类型数值与引用类型数值时，得到的结果完全不同。

基本包装类型重写了valueOf(),toLocaleString(),toString()方法，重写后的valueOf()方法返回对象表示的基本类型的值，另外两个方法则返回字符串形式的值。

##### 5.6.1 Boolean类型

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

##### 5.6.2 Number类型

将数值格式化为**字符串**的方法：都会进行舍入操作

toFixed(num) ：0<=num<=20：按照指定的小数位数返回数值的字符串表示

toExponential(num): 0<=num<=20,用指数记数法表示，小数点前只有一位

toPrecision(num) :1<=num<=21：返回 NumberObject 的字符串表示，包含 num 个有效数字。如果 num 足够大，能够包括 NumberObject 整数部分的所有数字，那么返回的字符串将采用定点计数法。否则，采用指数计数法，即小数点前有一位数字，小数点后有 num-1 位数字。必要时，该数字会被舍入或用 0 补足。

##### 5.6.3 String类型

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

**replace(argu1,argu2)**:argu1可以是字符串或者RegExp对象;argu2可以是字符串或者函数

要想替换所有子字符串，要用RegExp的全局模式

若第二个参数为函数，则在只有一个匹配项（即与模式匹配的字符串）的情况下，会向这个函数传递3个参数：模式的匹配项、匹配项在字符串中的位置和原始字符串。在正则表达式定义多个捕获组的情况下，传递给函数的参数依次是模式的匹配项、第一个捕获组的匹配项、第二个捕获组的匹配项......，但最后两个参数依然分别是模式匹配项在字符串中的位置和原始字符串。这个函数返回一个字符串，表示应该被替换的匹配项。

split()：基于指定的分隔符将一个字符串分割成多个子字符串，并将结果放在一个数组中，分隔符可以是字符串也可以是一个RegExp对象，可选的第二个参数用于指定数组的大小。

（7）str1.LocaleCompare(str2)方法：比较两个字符串，返回的数组取决于实现:

str1 在 str2前面：return -1; str1 在 str2后面：return 1;str1 等于 str2：return 0

（8）fromCharCode():接收一或多个字符编码，然后将它们转换成一个字符串

（9）一些HTML方法：如anchor(),big()等，但应尽少使用，因为它们创建的标记通常无法表达语义。

#### 5.7 单体内置对象



## 6.理解对象

#### 6.1 理解对象





