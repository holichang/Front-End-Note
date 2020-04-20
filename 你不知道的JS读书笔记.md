[TOC]



## 第一部分  作用域和闭包

#### 第一章 作用域是什么

##### 1.编译原理：

JavaScript（即时编译）:一门编译语言，但与传统编译语言不同，它不是提前编译的，编译结果也不能在分布式系统中进行移植。尽管如此，JS引擎进行编译的步骤和传统编译语言非常相似，在某些环节可能比预想的要复杂。

传统编译语言的流程中：分为三部分：

分词/词法分析（分解成词法单元）——解析/语法分析（词法单元流转化为抽象语法树AST）——代码生成（AST转换为可执行代码）

##### 2.理解作用域：（编译器，引擎，作用域）

``` js
var a=2;//在编译时声明，在执行时赋值
```

赋值操作会执行两个动作，首先编译器会在当前作用域中声明一个变量（如果之前没有声明过），然后在运行时引擎会在作用域中查找该变量，如果能够找到就会对它赋值。

引擎查找类型：（赋值操作的左右，不一定是=的左右）

LHS：当变量出现在赋值操作的左侧时进行LHS查询，即试图找到变量的容器本身，从而可以对其赋值

RHS：变量出现在右侧时，RHS查询即简单的查找某个变量的值。（“非左侧”）可以理解为取到它的源值

编译器可以在代码生成的同时处理声明和值的定义（编译时声明函数，不需要在执行时进行LHS引用）

##### 3.作用域嵌套

作用域：是根据名称查找变量的一套规则，规定了当前代码对某个变量的使用权限

##### 4.异常

如果RHS查询在所有嵌套的作用域中都遍寻不到所需的变量，引擎就会抛出ReferenceError异常。

如果RHS查询到了一个变量，但你对该值进行了不合理的操作，引擎会抛出TyprError操作。

而LHS查询时，如果在顶层（全局作用域）中也无法找到目标变量，全局作用域中就会创建一个具有该名称的变量，并将其返还给引擎，前提是程序运行在“非严格模式”下。

（严格模式（ES5引入）下，LHS查询失败不会创建全局变量，会抛出ReferenceError异常）

#### 第二章，词法作用域

作用域主要有两种工作模型：**词法作用域**（JS及大部分编程语言所采用）和动态作用域

##### 1.词法阶段

词法作用域就是定义在词法阶段的作用域，换句话说，词法作用域是由你在写代码时将变量和块作用域写在哪里来决定的，因此当词法分析器处理代码时会保持作用域不变（大部分情况下是这样的）

无论函数在哪里被调用，也无论它如何被调用，它的词法作用域都只由被声明时所处的位置决定

##### 2.欺骗词法：动态修改词法作用域或动态创建新的词法作用域

**2.1 eval()**

接受一个字符串为参数，并将其中的内容视为好像书写时就存在于程序中这个位置的代码，可以在运行期修改书写期的词法作用域

**2.2 with(obj)**

with可以将一个没有或有多个属性的对象处理为一个完全隔离的词法作用域，因此这个对象的属性也会被处理为定义在这个作用域中的词法标识符

**eval()函数如果接受了含有一个或多个声明的代码，就会修改其所处的词法作用域，而with()声明实际上是根据你传给它的对象凭空创建了一个新的词法作用域**

**为什么不推荐使用eval()和with()?**

(1)欺骗词法会导致性能下降

(2)会被严格模式所限制，with被完全禁止，而在保留核心功能的前提下，间接或非安全地使用eval()也被禁止了

**2.3 性能**

为什么会导致性能下降？

JS引擎会在编译阶段进行数项的性能优化，其中有些优化依赖于能够根据代码的词法进行静态分析，并预先确定所有变量和函数的定义位置，才能在执行过程中快速找到标识符。但如果引擎在代码中发现了eval()和with()，在悲观情况下可能会做不到任何优化。

**引擎无法在编译时对作用域查找进行优化，因为引擎只能谨慎地认为这样的优化是无效的**

#### 第三章 函数作用域和块作用域

##### 1.函数中的作用域

##### 2.隐藏内部实现

规避冲突：

全局命名空间（比如引入第三方库）；

*模块管理*

##### 3.函数作用域

函数表达式可以是匿名的，而函数声明则不可以省略函数名——在JS的语法里面是非法的

**匿名函数的缺点：**

（1）匿名函数在栈追踪中不会显示出有意义的函数名，使得调试很困难；

（2）如果没有函数名，当函数需要引用自身时只能使用已经过期的arguments.callee引用，比如在递归中。另一个函数需要引用自身的例子，是在事件触发后事件监听器需要解绑自身；

（3）匿名函数省略了对于代码可读性/可理解性很重要的函数名，一个描述性的名称可以让代码不言自明。

##### 4.块作用域

（1）with

（2）try……catch

（3）let

（4）const

#### 第四章 提升

##### 1.先有鸡还是先有蛋

先声明（编译阶段）再赋值（执行阶段）

函数声明会被提升，但函数表达式不会被提升（如：`var foo=function(){}`）

##### 2.编译器再度来袭

##### 3.函数优先

函数声明优先于变量声明;

**一个普通块内部的函数声明通常会被提升到所在作用域的顶部**

#### 第五章 作用域闭包

**无论通过何种手段将内部函数传递到所在的词法作用域以外，它持有对原始定义作用域的引用，无论在何处执行这个函数都会使用闭包**

> 思考：通过使用闭包，在作用域之外也可以调用函数，同时该函数还可以访问本身词法作用域中的变量

在定时器、事件监听器、AJAX请求、跨窗口通信、Web Workers或者任何其他的异步（或同步）任务中，只要使用了**回调函数**，实际上就是在使用闭包

##### 1.1 循环和闭包

IIFE：立即执行函数表达式，相当于将块转为了一个可以被关闭的作用域（var）

先看下面这个例子：

```js
for(var i=1;i<=5;i++){
    setTimeout(function timer(){
        console.log(i);
    },1000*i)
}
//预期：分别输出数字1-5，每秒一次，每次一个
//该段代码会以每秒一次的频率输出五次6
```

缺陷是我们试图假设循环中的每个迭代在运行时都会给自己捕获一个i的副本，但是根据作用域的工作原理，实际情况是尽管循环中的五个函数是在各个迭代中分别定义的，但是它们都被**封闭在一个共享的全局作用域中，**因此事实上只有一个i。

如何修改？

**方法一：使用IIFE**

```js
for(var i=1;i<=5;i++){
    function(j){
        setTimeout(function timer(){
            console.log(j)
        },1000*j)
    }(i)
}
```

**方法二：使用setTimeout第三个参数**

```js
for(var i=0;i<=5;i++){
    setTimeout(function timer(j){
        console.log(j)
    },i*1000,i)
}
//setTimeout的第三个参数为传给执行函数的其他参数（IE9 及其更早版本不支持该参数）。
```

**方法三：使用let：块级作用域**

```js 
for(var i=0;i<=5;i++){
    let j=i;
    setTimeout(function timer(j){
        console.log(j)
    },j*1000)
}
或：
for(let i=0;i<=5;i++)
    setTimeout(function timer(i){
        console.log(i)
    },i*1000)
}
//每次迭代都会创建一个i的副本
```

##### 1.2 模块

模块模式需要具备两个必要条件：

（1）必须有外部的封闭函数，该函数必须至少被调用一次，（**每次调用都会创建一个新的模块实例？**）

（2）封闭函数必须返回至少一个内部函数，这样内部函数才能在私有作用域中形成闭包，并且可以访问或者修改私有的状态

**现代的模块机制：**

大多数模块依赖加载器/管理器本质上都是将这种模块定义封装进一个友好的API。这里并不会研究某个具体的库，为了宏观了解会简单介绍一些核心概念：

```js
var MyModules=(function(){
    var module={};
    function define(name,deps,impl){
        for (var i=0;i<deps.length;i++){
            deps[i]=module[deps[i]];
        }
        modules[name]=impl.apply(impl,deps)
        //引入需要的依赖
    }//该函数用于向管理中添加模块
    function get(name){
        return module[name];
    }//通过名称获取模块
    return{
        define:define,
        get:get
    }
})();
//下面为使用方法：[]为新定义的模块需要引入的依赖模块列表
MyModules.define("bar",[],function(){
    function hello(who){
        return 'let me introduce:'+who;
    }
    return {
        hello:hello
    }
});
MyModules.define("foo",["bar"],function(bar){
    var hungry="hippo";
    function awesome(){
        console.log(bar.hello(hungry).toUpperCase());
	}
	return{
        awesome:awesome
    }
});
var bar=MyModules.get("bar");
var foo=MyModules.get("foo");
console.log(
	bar.hello("hippo")
);//let me introduce: hippo
foo.awesome();//LET ME INTRODUCE:HIPPO
```



## 第二部分 this和对象原型

this既不指向函数自身也不指向函数的词法作用域，this实际上是在函数被调用时发生的绑定，它指向什么完全取决于函数在哪里被调用。

#### 第一章.this全面解析

##### 1 调用位置：函数在代码中被调用的位置（而不是被声明的位置）

调用栈：为了到达当前执行位置所调用的所有函数

##### 2 绑定规则：

**2.1 默认绑定**：独立函数调用。可以把这条规则看作是无法应用其他规则时的默认规则；

回调函数相当于隐式的传参

非严格模式下，将全局对象用于默认绑定，而严格模式下，this会绑定到undefined

*对于默认绑定来说，决定this绑定对象的并不是调用位置是否是严格模式，而是函数体是否处于严格模式*

**2.2 隐式绑定**：在一个对象内部包含一个指向函数的属性，并通过这个属性间接引用函数，从而把this间接（隐式）绑定到这个对象上

考虑调用位置是否有上下文对象（对象属性引用链中只有上一层或者说是最后一层在调用位置中起作用），参数传递其实就是一种隐式赋值；可能会发生隐式丢失

**2.3 显式绑定**：使用call()和apply()

**硬绑定：**典型应用场景就是创建一个包裹函数，负责接收参数并返回值

ES5提供了内置方法：Function.prototype.bind:会返回一个硬编码的新函数，它会把你指定的参数设置为this的上下文并调用原始函数。

>怎么原生JS实现bind?
>
>```js
>if(!Function.prototype.myBind){
>Function.prototype.myBind=function(oThis){
>   if(typeof this!=='function'){
>       throw new TypeError('Function.prototype.myBind-what is trying '+'to be found is not callable');
>   }
>   var aArgs=Array.prototype.slice.call(arguments,1);
>   var fToBind=this;//要绑定的函数
>   var fNOP=function () {};
>   //
>   var fBound=function(){
>       return fToBind.apply((this instanceof fNOP && oThis? this:oThis),aArgs.concat.apply(aArgs,arguments));
>       //不是被new调用的时候this绑定到全局对象或者undefined,被new调用的时候this绑定到fBound
>   };   
>   fNOP.prototype=this.prototype;
>   fBound.prototype=new fNOP();
>   //
>   //这段代码会判断硬绑定是否是被new调用，如果是的话就会用新创建的this替换硬绑定的this
>   return fBound;
>}
>}
>```
>
>>如何判断一个函数是否是被new调用？new 的实现原理：
>>
>>

**API调用的“上下文”：**如arr.forEach(function,可选参数，指定this)

**2.4 new绑定**:实际上并不存在所谓的“构造函数”，只有对于函数的构造调用

使用new来调用函数，会自动执行下面的操作：

a.创建（或者说是构造）一个全新的对象；

b.这个新对象会被执行[[Prototype]]连接；

c.这个新对象会绑定到函数调用的this；

d.如果函数没有其他返回对象，那么new表达式中的函数调用会自动返回这个新对象

##### 3 优先级：new绑定>显式绑定>隐式绑定>默认绑定

> **判断this：**
>
> 1.函数是否在new中调用（new绑定）？如果是的话this绑定的是新创建的对象
>
> 2.函数是否通过apply,call(显式绑定)？如果是的话，this绑定的是指定的对象
>
> 3.函数是否在某个上下文对象中调用（隐式绑定）？如果是的话，this绑定的就是这个上下文对象
>
> 4.如果上述都不是的话就是默认绑定，严格模式下this 绑定到undefined，非严格模式下绑定到全局对象

##### 4 绑定例外

（1）被忽略的this

如`foo.apply(null,arguments)`或`foo.bind(null,可预设参数)`，当函数并不关心this时，可以用null占位，默认规则下会把this绑定到全局对象，这种方式可能会导致许多问题（比如修改了全局对象），可以通过`Object.Create(null)`创建一个空对象，该对象与{}很像，**但并不会创建Object.prototype这个委托，所以它比{}更空**.

（2）间接引用

容易在赋值的时候发生，传递的是原函数的引用

（3）软绑定:在绑定之后还保留隐式绑定和显式绑定对this值得修改（重点：考虑this不绑定全局对象和undefined时，可修改为其他对象）

> 原生JS实现软绑定：

```js
if (!Function.prototype.softBind){
    Function.prototype.softBind=function(obj){
        var fn=this;
        //捕获所有curried参数
        var curried=[].slice.call(arguments,1);
        var bound=function(){
            return fn.apply(
                (!this||this===global)?obj:this,curried.concat.apply(curried,arguments))
        };
        bound.prototype=Object.create(fn.prototype);//使fn成为bound的原型
        return bound;
    }
}
function foo(){
    console.log("name:"+this.name);
}
var obj={name:"obj"},obj1={name:"obj1"},obj2={name:"obj2"};
var fooOBJ=foo.softBind(obj);
fooOBJ();//"obj"
//此处调用采用默认绑定，this绑定到undefined 或全局对象
//在强绑定中这之后this绑定不会再更换，而在软绑定中可通过隐式绑定或显示绑定修改内部this绑定
obj2.foo=fooOBJ;
obj2.foo();//"obj2"
fooOBJ.apply(obj1,arguments);//"obj3"
```

##### 5. this词法

ES6中的箭头函数并不会使用四条标准的绑定规则，而是根据当前的词法作用域来决定this,具体来说，箭头函数会继承外层函数调用的this绑定（无论this绑定到什么），这其实和ES6之前的self=this机制一样





 