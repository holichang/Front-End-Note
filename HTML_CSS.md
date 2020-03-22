[TOC]

#### 1.CSS Sprites:

**简介**

CSS Sprites在国内很多人叫css精灵，是一种网页图片应用处理方式。它允许将一个页面涉及到的所有零星图片都包含到一张大图中， 利用CSS的“background-image”，“background- repeat”，“background-position”的组合进行背景定位， 访问页面时避免图片载入缓慢的现象。

**优点**

（1）CSS Sprites能很好地减少网页的http请求，从而大大的提高页面的性能，这是CSS Sprites最大的优点，也是其被广泛传播和应用的主要原因；

（2）CSS Sprites能减少图片的字节；

（3）CSS Sprites解决了网页设计师在图片命名上的困扰，只需对一张集合的图片命名，不需要对每一个小图片进行命名，从而提高了网页制作效率。

（4）CSS Sprites只需要修改一张或少张图片的颜色或样式来改变整个网页的风格。

**缺点**

（1）图片合并麻烦：图片合并时，需要把多张图片有序的合理的合并成一张图片，并留好足够的空间防止版块出现不必要的背景。

（2）图片适应性差：在高分辨的屏幕下自适应页面，若图片不够宽会出现背景断裂。

（3）图片定位繁琐：开发时需要通过工具测量计算每个背景单元的精确位置。

（4）可维护性差：页面背景需要少许改动，可能要修改部分或整张已合并的图片，进而要改动css。在避免改动图片的前提下，又只能（最好）往下追加图片，但这样增加了图片字节。

#### 2.怎么实现水平居中布局，分情况解释：

2.1 子元素为行内元素：设置父元素的`text-align:center;line-height:父元素的高度;`

2.2 子元素为给定高宽的块状元素：

（1）设置子元素的左右margin值均为auto；计算父元素和子元素的高度差，设置margin-top或margin-botton;

（2）设置子元素的左右margin值均为auto；设置父元素`display:table-cell;vertical-align:middle`   table单元格的vertical-align属性可以设置垂直对齐；

（3）将子元素设为`display:inline-block`，然后设置父元素`text-align:center;display:table-cell;vertical-align:middle`;

（4）通过flex布局：设置`justify-content:space-around;align-items:center`设置主轴和交叉轴的对齐方式

（5）通过设置`position:absolute`控制子元素与父元素的距离，或者通过设置`position:relative`设置子元素与其正常文本流下的距离

2.3 子元素为未给定高宽的块状元素：

未设置子元素的height和width，块状元素的宽度为父元素的宽度，高度被内部撑开，相当于只需要设置垂直居中：设置父元素`display:table-cell;vertical-align:middle`   

#### 3.试想一下一个盒子设置了overflow:hidden，里面的一个子元素设置了position为fixed超出了盒子的边界，这个子元素会显示在页面中吗？

答：会，父元素的overflow:hidden会失效

#### 4.关于布局

#### 5.BFC

#### 6.Less

Less 是一门 CSS 预处理语言，它扩充了 CSS 语言，增加了诸如变量、混合（mixin）、函数等功能，让 CSS 更易维护、方便制作主题、扩充。

Less 可以运行在 Node、浏览器和 Rhino 平台上。网上有很多第三方工具帮助你编译 Less 源码。



