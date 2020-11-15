# less与sass的区别

一、less与sass分别是什么

1、less

Less 是一门 CSS 预处理语言，它扩展了 CSS 语言，增加了变量、Mixin、函数等特性，使 CSS 更易维护和扩展，它可以运行在 Node 或浏览器端。

2、sass

Sass 是一款强化 CSS 的辅助工具，它在 CSS 语法的基础上增加了变量 、嵌套 、混合  、导入  等高级功能，这些拓展令 CSS 更加强大与优雅。使用 Sass 以及 Sass  的样式库（如Compass）有助于更好地组织管理样式文件，以及更高效地开发项目。

二、less和sass的相同之处

Less和Sass在语法上有些共性，比如下面这些：

1、混入(Mixins)——class中的class；

2、参数混入——可以传递参数的class，就像函数一样；

3、嵌套规则——Class中嵌套class，从而减少重复的代码；

4、运算——CSS中用上数学；

5、颜色功能——可以编辑颜色；

6、名字空间(namespace)——分组样式，从而可以被调用；

7、作用域——局部修改样式；

8、JavaScript 赋值——在CSS中使用JavaScript表达式赋值。

三、less和sass的区别

Less是基于JavaScript，是在客户端处理的。

Sass是基于Ruby的，是在服务器端处理的。

关于变量在Less和Sass中的唯一区别就是Less用@，Sass用$。

输出设置，Less没有输出设置，Sass提供4中输出选项：nested, compact, compressed 和 expanded。

Sass支持条件语句，可以使用if{}else{},for{}循环等等，而Less不支持。



详细对比列举如下：



1、Less：



(1)、声明变量:@变量名:变量值;

使用变量: @变量名

>less中变量的类型：

①数字类  1 10px  

②字符串：无引号字符串 red ;有引号字符串  "haha"  

③颜色类：red #000000 rgb()    

④值列表类型：用逗号和空格分隔    10px solid red



变量使用原则：

多次频繁出现的值、需要修改的值，设为变量

(2)、混合(MiXins)

①无参混合

声明：.name{}  选择器中调用：.name;

②代参混合

无默认值声明：.name(@param){} 调用：.name(parValue);

有默认值声明：.name(@param:value){}

        调用：.name(parValue);  parValue可省

如果声明时，参数没有默认值，则调用时必须赋值，否则报错！

无参混合，会在css中编译除同名的class选择器，有参的不会

(3)、less的匹配模式：使用混合进行匹配，类似于if结构

声明：

.name(条件一，参数){}

.name(条件二，参数){}

.name(@_,参数){}

调用：.name(条件值，参数值);

匹配规则：根据调用时提供的条件值去寻找与之匹配的"MiXins"执行，其中@_表示永远需要执行的部分

(4)、less中的运算

+ - * /  可带、可不带单位

颜色运算时，红绿蓝分三组计算，组内可进位，组间互不干涉

(5)、包含了传进来的所有参数：border:@arguments;

(6)、less中的嵌套：保留HTML中的代码结构

①嵌套默认是后代选择器，如果需要子代选择器，则在子代前加>

②.&表示上一层       &:表示上一层的hover事件

编译为:

1section{ 2p{ 3color: red; 4background-color: yellowgreen; 5text-align: center; 6} 7ul{ 8padding: 0px; 9list-style: none;10li{11float:  left;12margin: 10px;13width: 100px;14text-align: center;15border:  @border;16&:hover{17background-color: yellow;18}19}

2、Sass：

(1)、Sass中的变量

使用   $变量名：变量值，声明变量；

如果变量需要在字符串中嵌套，则需使用#加大括号包裹；

border-#{$left}:10px solid blue;

(2)、Sass中的运算，会将单位也进行运算，使用时需注意最终单位

例：10px*10px=100px

(3)、sass中的嵌套：选择器嵌套，属性嵌套，伪类嵌套

选择器嵌套 ul{ li{} } 后代

ul{ >li{} }  子代

&:表示上一层div{ ul{ li{ &=="div ul li" } } }

属性嵌套：属性名与大括号之间必须有:  

例如:border:{color:red;}

伪类嵌套：ul{li{ &:hover{ "ul li:hover" } } }

(4)、混合宏、继承、占位符

①混合宏：声明：@mixin name($param:value){}

调用：@include name(value);

>声明时，可以有参，可以无参；可带默认值，也可不带；但是，调用时，必须符合声明规范。同less

>优点；可以传参，不会生成同名class；

>缺点：会将混合宏中的代码，copy到对应的选择器中，产生冗余代码！

②继承：声明：.class{} 调用：@extend .class;

>优点：继承的相同代码，会提取到并集选择器中，减少冗余代码

>缺点：无法进行传参，会在css中，生成一个同名class

③占位符：声明：&class{}  调用：@extend  %class;

>优点：继承相同代码，会提前到并集选择器；不会生成同名的class选择器

>缺点：无法进行传参

综上所述：当需要传递参数时，用混合宏；当有现成的class时用继承；当不需要参数，也不需要class时，用占位符

（5） 混合指令 (Mixin Directives)

混合指令（Mixin）用于定义可重复使用的样式，避免了使用无语意的 class，比如 .float-left。混合指令可以包含所有的 CSS 规则，绝大部分 Sass 规则，甚至通过参数功能引入变量，输出多样化的样式。

 ①定义混合指令 @mixin (Defining a Mixin: @mixin)

混合指令的用法是在 @mixin 后添加名称与样式，比如名为 large-text 的混合通过下面的代码定义：

@mixin large-text { font: { family: Arial; size: 20px; weight: bold; } color: #ff0000; }

（6）. 函数指令 (Function Directives)

Sass 支持自定义函数，并能在任何属性值或 Sass script 中使用：

$grid-width: 40px; $gutter-width: 10px; @function grid-width($n) { @return $n * $grid-width + ($n - 1) * $gutter-width; } #sidebar { width: grid-width(5); }

编译为

#sidebar { width: 240px; }

与 mixin 相同，也可以传递若干个全局变量给函数作为参数。一个函数可以含有多条语句，需要调用 @return 输出结果。

自定义的函数也可以使用关键词参数，上面的例子还可以这样写：

#sidebar { width: grid-width($n: 5); }

建议在自定义函数前添加前缀避免命名冲突，其他人阅读代码时也会知道这不是 Sass 或者 CSS 的自带功能。

自定义函数与 mixin 相同，都支持 variable arguments


参考文献：[less与sass的区别](https://www.jianshu.com/p/b062155f3739)