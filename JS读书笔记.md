## 1.JavaScript简介

### 1.1 ECMA-262：

ECMAScript脚本语言标准，与Web浏览器没有依赖关系，常见的Web浏览器只是JavaScript可能实现的宿主环境之一，宿主环境不仅提供基本的ECMAScript实现，同时也会提供该语言的扩展，以便语言与宿主环境之间交互。而这些扩展——如DOM，则利用ECMAScript的核心类型和语法提供更多更具体的功能，以便实现针对环境的操作。其他宿主环境包括Node和Adobe Flash.

### 1.2 一个完整的JavaScript实现应该由下列三个不同的部分组成：

（1）核心（ECMAScript）：由ECMA-262定义，提供核心语言功能

（2）文档对象模型(DOM)：提供访问和操作网页内容的方法和接口，DOM1---DOM2---DOM3

DOM不只是针对JavaScript的，很多别的语言也都实现了DOM（如SVG,MathML,SMIL都基于XML）

（3）浏览器对象模型（BOM）：提供与浏览器交互的方法和接口，HTML5将很多BOM功能写入了正式规范

大多数浏览器在提及对JavaScript的支持情况时，一般都以ECMAScript兼容性和对DOM的支持情况为准。

## 2 .在HTML中使用JavaScript



## 3.基本概念

### 3.6语句

for-in语句：是一种精准的迭代语句，可以用来枚举对象的属性，如：

```JS
for(var propName in window){
    document.write(propName);
}
```

每次循环，都会将window对象中存在的一个属性名赋值给变量propName。ECMAScript对象的属性没有顺序，因此for-in循环输出的属性名的顺序事不可预测的。



## 4 变量、作用域和内存问题

### 4.1 基本类型和引用类型的值

值类型与引用类型的区别:

存储方式的不同：值类型存储的是实际的值，存在栈中；而引用类型的值是保存在堆内存中的对象，JS不允许直接操作对象的内存空间，因此实际操作的是对象的引用而不是实际的对象。

引用类型可以动态添加属性：引用类型可以动态添加对象的属性，值类型不可以

复制变量值的方式不同：从一个变量向另一个变量复制基本类型值，会在变量对象上创建一个新值，然后把该值复制到为新变量分配的位置上，这两个变量可以参与任何操作互不影响；而引用类型复制的是对象的地址引用，指向的是同一个对象，对副本的操作会影响对象本身。

传递参数的方式不同，JS中所有函数的参数都是按值传递的，与复制变量值的过程是一样的，因此在向参数传递引用类型的值时，这个局部变量的变化会反映在函数的外部。（可以把ES函数的参数想象成局部变量）

检测类型时的不同：检测基本数据类型时可以使用typeof操作符；检测引用类型值：instanceof操作符

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

## 5.引用类型

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

检测数组：if(value instanceof Array):但instanceof操作符假定只有一个全局执行环境，当网页包含多个框架，那实际上就存在两个以上不同的全局执行环境，从而存在两个以上不同版本的Array构造函数，为解决这个问题，ES5引入了Array.isArray(value)。

#### 5.2.1数组转化为字符串：

toString(),toLocaleString():实际调用的是数组中每一项的toString()方法

join():参数为用作分隔符的字符串，若不传入任何值，或传入undefined，则使用逗号作为分隔符。

#### 5.2.2 栈方法：后进先出

push()：可以接受任意数量的参数，把它们逐个添加到数组末尾，并返回修改后数组的长度

pop()：从数组末尾移除最后一项，减少数组的length值，然后返回移除的项。

#### 5.2.3 队列方法：先进先出：

push()：可以接受任意数量的参数，把它们逐个添加到数组末尾，并返回修改后数组的长度

shift()：从数组前端移除一项，减少数组的length值，然后返回移除的项。

unshift():能在数组前端添加任意个项，并返回新数组的长度

#### 5.2.4重排序方法

reverse()

sort():默认情况下，比较的是每个数组项的字符串，由小到大；因此可以接收函数作为参数，返回对数组的引用。数组在原数组上进行排序，不生成副本。

#### 5.2.5操作方法

concat()

slice()

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

### 5.6基本包装类型

ECMAScript提供了3个特殊的引用类型：Boolean,Number和String,每当读取一个基本类型值的时候，后台就会创建一个对应的基本包装类型的对象，从而让我们能够调用一些方法来操作这些数据。

引用类型与基本包装类型的主要区别就是对象的生存期。使用new操作符创建的引用类型的实例，在执行流离开当前作用域之前都一直保存在内存中。而自动创建的基本包装类型的对象，则只存在于一行代码的执行瞬间，然后立即被销毁。所以我们不能在运行时为基本类型值添加属性和方法。

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

### 5.7 单体内置对象

## 6.理解对象

### 6.1 理解对象

#### 6.1.1 属性类型

ES5中有两种属性：数据属性和访问器属性

**数据属性**：数据属性包含一个数据值的位置。在这个位置可以读取和写入值。数据属性有4个描述其行为的特性：

[[Configurable]]:表示能否通过delete删除属性从而重新定义属性，能否修改属性的特性，或者能否把属性修改为访问器属性。

[[Enumerable]]：表示能否通过for-in循环返回属性。

[[Writable]]：表示能否修改属性的值。

[[Value]]：包含这个属性的值。

**要修改属性默认的特性：**ES5的Object.defineProperty()方法（三个参数：属性所在的对象、属性的名字、描述符对象）使用如下：

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

可以多次调用Object.defineProperty()方法修改同一个属性，但在把configurable特性设置为false之后就会有限制了。同时，在调用Object.defineProperty()方法创建一个新属性时，如果不指定，configurable，enumerable和writable特性的默认值都是false,如果调用Object.defineProperty()方法是修改已定义属性的特性，则无此限制。

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

Object.getOwnPropertyDescriptor()方法：取得给定属性的描述符。接收两个参数：属性所在的对象和要读取其描述符的属性名称，如：(接上段代码)

```js
var descriptor=Object.getOwnPropertyDescriptor(book,"_year");
alert(descriptor.value);//2004
alert(descriptor.configurable);//false
```

**ES5的Object.getOwnPropertyDescriptor（）方法只能用于实例属性，要取得原型属性的描述符，必须直接在原型对象上调用该方法。**

### 6.2创建对象

#### 6.2.1 工厂模式：

用函数来封装以特定接口创建对象的细节（虽然解决了创建多个相似对象的问题，但没有解决对象识别的问题）

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

调用构造函数实际会经历以下4个步骤：

（1）创建一个新对象

（2）将构造函数的作用域赋给新对象（因此this就指向了这个对象）

（3）执行构造函数中的代码（为这个新对象添加属性）

（4）返回新对象

**构造函数模式存在的问题**：每个方法都要在每个实例重新创建一遍

#### 6.2.3 原型模式

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
```

在默认情况下，所有原型对象都会自动获得一个constructor(构造函数)属性，这个属性是一个指向prototype属性所在函数的指针。Person.prototype.constructor指向Person

明确一点：**这个连接存在于实例与构造函数的原型对象之间**，而不是存在于实例与构造函数之间（即person1与Person.prototype之间的联系）person1内部有一个指向Person.prototype的指针

```js
alert(Person.prototype.isPrototypeOf(person1));//true
```

**Object.getPrototypeOf():**可以方便地获取一个对象的原型

```js
alert(Object.getPrototypeOf(person1)==Person.prototype);//true
alert(Object.getPrototypeOf(person1).name);//"Nicholas"
```

当代码要取得某个对象的某个属性时，会先从对象实例本身开始搜索，如果没有找到属性名，则继续搜索指针指向的原型对象。

当为对象实例添加一个属性时，这个属性就会屏蔽原型对象中保存的同名属性，也就是说，添加这个属性值会阻止我们访问原型中的那个属性，但不会修改那个属性;不过使用delete操作符可以完全删除实例属性。

```JS
person1.name="Greg";
alert(person1.name);//Greg
alert(person1.hasOwnProperty("name"));//true
delete person1.name;
alert(person1.hasOwnProperty("name"));//false
alert(person1.name);//Nicholas
```

**hasOwnProperty()**方法：检测一个属性是存在于实例中还是原型中

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

原型对象中的引用类型值会被共享

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

```JS
values.push.apply(values,arguments);//arguments是个类数组对象，不能直接push到数组中
```

构造函数在没有返回值的情况下，默认返回新对象实例，而该模式下的构造函数形式类似于工厂模式，在末尾有return语句，可以重写调用构造函数时返回的值，因此，**返回的对象与构造函数以及构造函数的原型属性之间没有关系**，也就是说，构造函数返回的对象与在构造函数外部创建的对象没有什么不同。使用instanceof 没有意义。

#### 6.2.7 稳妥构造函数模式

指的是没有公共属性，最适合在一些安全环境中使用，也与工厂模式很像

与寄生构造函数模式的区别：（1）不引用this对象；（2）不使用new操作符

这种模式下创建的对象除了使用方法，没有其他办法访问属性值。

### 6.3 继承

ES只支持实现继承，而且主要依靠原型链

方法签名：

#### 6.3.1 原型链



