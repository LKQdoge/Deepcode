# # Day 1 学习

## HTML学习



> HTML是超文本标记语言的简称，它是一种不严谨的、简单的标识性语言。它用各种标签将页面中的元素组织起来，告诉浏览器该如何显示其中的内容。

+ 分区 div （网页中划分区域）
+ 标题 h1-h6 (共六级)
+ 段落标签<p>
+ 图像 img

​       键盘输入 `img`，按 `tab`键，即可出现图像标签代码:

​       `<img src="" alt="">`

+ 列表 (ul:无序列表/ ol:有序列表 / dl: 定义列表 / dir:目录列表 / menu:菜单列表)

+ 超链接 a

  在 HTML 中创建超链接非常简单，只需用 a 标签环绕需要被链接的对象即可，其基本语法格式如下:

`<a href="链接地址">文本或图片</a>`

+ 表单 form

  `<input  type="text"（input元素类型）name="fname"（input元素名称） 
  value="text"（input元素的值）/>`

+ 表格 table

  > <table>	定义表格，生成的表格在一对<table></table>中；
  > 2	<caption>	定义表格标题，当表格需要标题时，使用<caption>表格标题</caption>
  > 3	<thead>	定义表格的页眉
  > 4	<tbody>	定义表格的主体
  > 5	<tfoot>	定义表格的页脚
  > 6	<th>	定义表格的表头，一般是表头中的内容会被加黑；
  > 7	<tr>	定义表格的行
  > 8	<td>	定义表格单元格
  > 9	<col>	定义用于表格列的属性
  > 10	<colgroup>	定义表格列的组
  > 原文链接：https://blog.csdn.net/weixin_47139649/article/details/109099704

+ 框架 iframe(内嵌框架，用于局部)

+ html5特性 (我还不是很看得懂,先放篇文章)

  [html5的十大特性]([(16条消息) HTML5的十大特性_SummerJX的博客-CSDN博客_html5的特性有哪些](https://blog.csdn.net/SummerJX/article/details/80998055?ops_request_misc=%7B%22request%5Fid%22%3A%22164242273516780274148549%22%2C%22scm%22%3A%2220140713.130102334..%22%7D&request_id=164242273516780274148549&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-1-80998055.first_rank_v2_pc_rank_v29&utm_term=html5特性&spm=1018.2226.3001.4187))



## CSS学习

> CSS 指层叠样式表 (**C**ascading **S**tyle **S**heets)

+ 引入方式：行内/内部/外部

+ 选择器（前四个最常用）

  + 通用选择器(页面所有元素)

    `* { margin: 0; padding: 0;}`

    (呐，页面所有元素都居中了↑)

  + 标签选择器

    > 用HTML标签名称作为选择器，按标签名称分类，为页面中某一类标签指定统一的CSS样式。其基本语法格式如下：
    > 标签名 {属性1:属性值1; 属性2:属性值2; 属性3:属性值3; ......}
    > 标签选择器最大的优点是能快速为页面中同类型的标签统一样式，同时这也是他的缺点，不能设计差异化样式。

    

  + id 选择器(id选择器比较局限，不能重用。)

    `#container { width: 960px; margin: auto;}`

  + class 选择器

    > class 选择器用于描述一组元素的样式，class 选择器有别于id选择器，class可以在多个元素中使用。
    >
    > class 选择器在HTML中以class属性表示, 在 CSS 中，类选择器以一个点"."号显示.
    >
    > 所有拥有 center 类的 HTML 元素均为居中。 
    >
    >  `.center {text-align:center;}`

  + 属性选择器

    > 属性选择器可以为拥有指定属性的 HTML 元素设置样式；属性选择器通过 `[]` 来定义，`[]` 内部为元素的属性，属性选择器的权重要高于标签选择器。

    `el[attr=val]`  选择 attr 为 val 的 el 元素

  + 派生选择器 

    + 后代选择器(比如我们要选择在li元素中包含a标签的链接（不是所有的链接），取消下划线的默认样式，我们可以这样代码实现)

      `li a {text-decoration: none;}`

    + 子元素选择器(缩小范围，只选择某个元素的子元素,非任意选择)

      `h1 > strong {color:red;}`

      (这个规则会把第一个 h1 下面的两个 strong 元素变为红色，但是第二个 h1 中的 strong 不受影响)

    + 相邻兄弟选择器(选择紧接在另一个元素后的元素，而且二者有相同的父元素)

        例如增加紧接在 h1 元素后出现的段落的上边距，可以这样写：

        `h1 + p {margin-top:50px;}`

  + 组合选择器

  + 伪选择器(:link 伪类来定义所有还没有点击链接的样式，:visited 伪类定义我们曾经点击过或者访问过的链接样式，示例代码如下:)

    `a:link { color: red; }a:visted { color: purple; }`

  + 选择器优先级

    > 每个规则对应一个初始"四位数"：0、0、0、0
    > 若是 行内选择符，则加1、0、0、0
    > 若是 ID选择符，则加0、1、0、0
    > 若是 类选择符/伪类选择符，则分别加0、0、1、0
    > 若是 元素选择符，则分别加0、0、0、1
    > 算法：将每条规则中，选择符对应的数相加后得到的”四位数“，从左到右进行比较，大的优先级越高。

     所以优先级由高到低顺序为：

    1.id选择器（#myid）

    2.类选择器（.myclassname）

    3.标签选择器（div,h1,p）

    4.子选择器（ul < li）

    5.后代选择器（li a）

    6.伪类选择（a:hover,li:nth-child）

    

+ 文档流 (布局从上至上，从左至右。 符合html中标签本身含义的布局。)

+ 内联元素 / 块状元素

  > 行内元素最常使用的就是span，其他的只在特定功能下使用，修饰字体<b>和<i>标签，还有<sub>和<sup>这两个标签可以直接做出平方的效果，而不需要类似移动属性的帮助，很实用。
  >
  > 　行内元素特征：
  >
  > (1)设置宽高无效
  >
  > (2)对margin仅设置左右方向有效，上下无效；padding设置上下左右都有效，即会撑大空间
  >
  > (3)不会自动进行换行

  > 块状元素代表性的就是div，其他如p、nav、aside、header、footer、section、article、ul-li、address等等，都可以用div来实现。不过为了可以方便程序员解读代码，一般都会使用特定的语义化标签，使得代码可读性强，且便于查错。
  >
  > 　块状元素特征：
  >
  > (1)能够识别宽高
  >
  > (2)margin和padding的上下左右均对其有效
  >
  > (3)可以自动换行
  >
  > (4)多个块状元素标签写在一起，默认排列方式为从上至下

+ 盒子模型

  - ##### W3C标准盒子模型

    **标准模式下，一个块的宽度 = width+padding(内边距)+border(边框)+margin(外边距)**

    > CSS中的宽（width）=内容（content）的宽
    >
    > CSS中的高（height）=内容（content）的高

  - ##### IE盒子模型

    **怪异模式下，一个块的宽度 = width+margin(外边距**)

    > CSS中的宽（width）=内容（content）的宽+（border+padding）*2
    > CSS中的高（height）=内容（content）的高+（border+padding）*2

+ 浮动(左右浮动)

  > 如果你把几个浮动的元素放到一起，如果有空间的话，它们将彼此相邻。

  ```css
  .thumbnail 
  {
      float:left;
      width:110px;
      height:90px;
      margin:5px;
  }
  ```

  

+ 定位

  + static

    ```css
    div.static {
        position: static;
        border: 3px solid #73AD21;
    }
    ```

  + fixed

    ```css
    p.pos_fixed
    {
        position:fixed;
        top:30px;
        right:5px;
    }
    ```

  + relative

    ```css
    h2.pos_left
    {
        position:relative;
        left:-20px;
    }
    h2.pos_right
    {
        position:relative;
        left:20px;
    }
    ```

    

  + absolute

    ```css
    h2
    {
        position:absolute;
        left:100px;
        top:150px;
    }
    ```

    

  + sticky

    ```css
    div.sticky {
        position: -webkit-sticky; /* Safari */
        position: sticky;
        top: 0;
        background-color: green;
        border: 2px solid #4CAF50;
    }
    ```

    

+ 层叠规则

  > 概念：CSS中的层叠就是让多个来源的样式叠加在一起，然后结合样式的特殊性（后面详细介绍）、继承性，确定最终应用的样式。

+ CSS3