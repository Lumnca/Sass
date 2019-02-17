# --------------------------Sass---------------------------- #

<p id="tit"></p>
                       
## :mortar_board:导航 ##

:arrow_down:<a href="#a1">1.l安装及准备工作</a>

:arrow_down:<a href="#a2">2.Sass脚本</a>

:arrow_down:<a href="#a3">3.Sass变量</a>

:arrow_down:<a href="#a4">4.嵌套CSS 规则</a>

:arrow_down:<a href="#a5">5.混合器</a>

:arrow_down:<a href="#a6">6.使用选择器继承来精简CSS</a>

<p id="a1"></p>
       
### :fish:安装及准备工作 ###

:arrow_double_up:<a href ="#tit">返回目录</a>

[官方安装文档](https://www.sass.hk/install/) 这是官方安装文档，按照上面步骤来即可，我使用的编译器为VS code，下面操作以VC作为示例。

在VC的扩展商店中搜索Sass并安装，Sass如下所示：

![](https://github.com/Lumnca/Sass/blob/master/Img/a1.png)

ass 可以通过以下三种方式使用：作为命令行工具；作为独立的 Ruby 模块 (Ruby module)；或者作为 Rack-enabled 框架的插件（例如 Ruby on Rails 与 Merb）。无论哪种方式都需要先安装 Sass gem （Windows 系统需要先安装 Ruby）Ruby和Sass安装完毕后，在VC的终端输入以下命令：

```
gem install sass
```

现在就可以创建sass文件，在文件夹中创建一个叫input的sass文件，只需要命名为input.scss即可。写完代码后保存编译，在VC终端命令行中运行 Sass：

```
sass input.scss output.css
```

上面input为sass文件， output为编译后转换成的css文件，前者必须要有，后者可以没有，编译后会自动创建一个编译后css的文件，`所以sass编译后转换就为css文件`。像上面这样比较麻烦，代码改一次，就需要保存并在命令行中编译一次。可以在命令行中输入以下命令：

```
sass --watch input.scss:output.css
```

以上就是监视单个 Sass 文件，每次修改并保存时自动编译。还可以监视整个文件夹：

```
sass --watch app/sass:public/stylesheets
```

app即为文件夹。

<p id="a2"></p>
       
### :fish: Sass脚本 ###

:arrow_double_up:<a href ="#tit">返回目录</a>

在 CSS 属性的基础上 Sass 提供了一些名为 SassScript 的新功能。 SassScript 可作用于任何属性，允许属性使用变量、算数运算等额外功能。

通过 interpolation，SassScript 甚至可以生成选择器或属性名，这一点对编写 mixin 有很大帮助。


Interactive Shell 可以在命令行中测试 SassScript 的功能。在命令行中输入 sass -i，然后输入想要测试的 SassScript 查看输出结果：

```
$ sass -i
>> "Hello, Sassy World!"
"Hello, Sassy World!"
>> 1px + 1px + 1px
3px
>> #777 + #777
#eeeeee
>> #777 + #888
white
```
<p id="a3"></p>
       
### :fish: 使用变量  ###

:arrow_double_up:<a href ="#tit">返回目录</a>

sass让人们受益的一个重要特性就是它为css引入了变量。你可以把反复使用的css属性值 定义成变量，然后通过变量名来引用它们，而无需重复书写这一属性值。或者，对于仅使用过一 次的属性值，你可以赋予其一个易懂的变量名，让人一眼就知道这个属性值的用途。

sass使用$符号来标识变量(老版本的sass使用!来标识变量。改成$是多半因为!highlight-color看起来太丑了。)，比如$highlight-color和$sidebar-width。为什么选择$ 符号呢？因为它好认、更具美感，且在CSS中并无他用，不会导致与现存或未来的css语法冲突。

#### 	:globe_with_meridians:变量声明 ####

sass变量的声明和css属性的声明很像：

```sass
$highlight-color: #F90;
```

这意味着变量$highlight-color现在的值是#F90。任何可以用作css属性值的赋值都 可以用作sass的变量值，甚至是以空格分割的多个属性值，如$basic-border: 1px solid black;，或以逗号分割的多个属性值，如$plain-font: "Myriad Pro"、Myriad、"Helvetica Neue"、Helvetica、"Liberation Sans"、Arial和sans-serif; sans-serif;。这时变 量还没有生效，除非你引用这个变量——我们很快就会了解如何引用。

与CSS属性不同，变量可以在css规则块定义之外存在。当变量定义在css规则块内，那么该变量只能在此规则块内使用。如果它们出现在任何形式的{...}块中（如@media或者@font-face块），情况也是如此：

```sass
$nav-color: #F90;
nav {
  $width: 100px;
  width: $width;
  color: $nav-color;
}

//编译后

nav {
  width: 100px;
  color: #F90;
}
```

在这段代码中，$nav-color这个变量定义在了规则块外边，所以在这个样式表中都可以像 nav规则块那样引用它。$width这个变量定义在了nav的{ }规则块内，所以它只能在nav规则块 内使用。这意味着是你可以在样式表的其他地方定义和使用$width变量，不会对这里造成影响。

只声明变量其实没啥用处，我们最终的目的还是使用它们。上例已介绍了如何使用 $nav-color和$width这两个变量，接下来我们将进一步探讨变量的使用方法。

#### 	:globe_with_meridians:变量引用 ####

凡是css属性的标准值（比如说1px或者bold）可存在的地方，变量就可以使用。css生成时，变量会被它们的值所替代。之后，如果你需要一个不同的值，只需要改变这个变量的值，则所有引用此变量的地方生成的值都会随之改变。

```sass
$highlight-color: #F90;
.selected {
  border: 1px solid $highlight-color;
}

//编译后

.selected {
  border: 1px solid #F90;
}
```

看上边示例中的$highlight-color变量，它被直接赋值给border属性，当这段代码被编译输出css时，$highlight-color会被#F90这一颜色值所替代。产生的效果就是给selected这个类一条1像素宽、实心且颜色值为#F90的边框。

在声明变量时，变量值也可以引用其他变量。当你通过粒度区分，为不同的值取不同名字时，这相当有用。下例在独立的颜色值粒度上定义了一个变量，且在另一个更复杂的边框值粒度上也定义了一个变量：

```sass
$highlight-color: #F90;
$highlight-border: 1px solid $highlight-color;
.selected {
  border: $highlight-border;
}

//编译后

.selected {
  border: 1px solid #F90;
}
```

这里，$highlight-border变量的声明中使用了$highlight-color这个变量。产生的效 果就跟你直接为border属性设置了一个1px $highlight-color solid的值是一样的。 最后，我们来了解一下变量命名的实用技巧，以结束关于变量的介绍。

1-3. 变量名用中划线还是下划线分隔;
sass的变量名可以与css中的属性名和选择器名称相同，包括中划线和下划线。这完全取决于个人的喜好，有些人喜欢使用中划线来分隔变量中的多个词（如$highlight-color），而有些人喜欢使用下划线（如$highlight_color）。使用中划线的方式更为普遍，这也是compass和本文都用的方式。

不过，sass并不想强迫任何人一定使用中划线或下划线，所以这两种用法相互兼容。用中划线声明的变量可以使用下划线的方式引用，反之亦然。这意味着即使compass选择用中划线的命名方式，这并不影响你在使用compass的样式中用下划线的命名方式进行引用：

```sass
$link-color: blue;
a {
  color: $link_color;
}

//编译后

a {
  color: blue;
}
```

在上例中，$link-color和$link_color其实指向的是同一个变量。实际上，在sass的大 多数地方，中划线命名的内容和下划线命名的内容是互通的，除了变量，也包括对混合器和Sass函数的命名。但是在sass中纯css部分不互通，比如类名、ID或属性名。

sass变量也有局部与全局变量之分，变量支持块级作用域，嵌套规则内定义的变量只能在嵌套规则内使用（局部变量），不在嵌套规则内定义的变量则可在任何地方使用（全局变量）。将局部变量转换为全局变量可以添加 !global 声明：

```sass
#main {
  $width: 5em !global;
  width: $width;
}

#sidebar {
  width: $width;
}
编译为

#main {
  width: 5em;
}

#sidebar {
  width: 5em;
}
```

尽管变量自身提供了很多有用的地方，但是sass基于变量提供的更为强大的工具才是我们关注的焦点。只有当变量与sass的其他特性一起使用时，才能发挥其全部的潜能。接下来，我们将探讨其中一个非常重要的特性，即规则嵌套。

<p id="a4"></p>
       
### :fish:嵌套CSS 规则   ###

:arrow_double_up:<a href ="#tit">返回目录</a>

css中重复写选择器是非常恼人的。如果要写一大串指向页面中同一块的样式时，往往需要 一遍又一遍地写同一个ID：

```css
#content article h1 { color: #333 }
#content article p { margin-bottom: 1.4em }
#content aside { background-color: #EEE }
```

像这种情况，sass可以让你只写一遍，且使样式可读性更高。在Sass中，你可以像俄罗斯套娃那样在规则块中嵌套规则块。sass在输出css时会帮你把这些嵌套规则处理好，避免你的重复书写。

```sass
#content {
  article {
    h1 { color: #333 }
    p { margin-bottom: 1.4em }
  }
  aside { background-color: #EEE }
}
 /* 编译后 */
#content article h1 { color: #333 }
#content article p { margin-bottom: 1.4em }
#content aside { background-color: #EEE }
```

上边的例子，会在输出css时把它转换成跟你之前看到的一样的效果。这个过程中，sass用了两步，每一步都是像打开俄罗斯套娃那样把里边的嵌套规则块一个个打开。首先，把#content（父级）这个id放到article选择器（子级）和aside选择器（子级）的前边：

```sass
#content {
  article {
    h1 { color: #333 }
    p { margin-bottom: 1.4em }
  }
  #content aside { background-color: #EEE }
}
 /* 编译后 */
#content article h1 { color: #333 }
#content article p { margin-bottom: 1.4em }
#content aside { background-color: #EEE }
```
然后，#content article里边还有嵌套的规则，sass重复一遍上边的步骤，把新的选择器添加到内嵌的选择器前边。



一个给定的规则块，既可以像普通的CSS那样包含属性，又可以嵌套其他规则块。当你同时要为一个容器元素及其子元素编写特定样式时，这种能力就非常有用了。

```sass
#content {
  background-color: #f5f5f5;
  aside { background-color: #eee }
}
```
容器元素的样式规则会被单独抽离出来，而嵌套元素的样式规则会像容器元素没有包含任何属性时那样被抽离出来。

```css
#content { background-color: #f5f5f5 }
#content aside { background-color: #eee }
```
大多数情况下这种简单的嵌套都没问题，但是有些场景下不行，比如你想要在嵌套的选择器 里边立刻应用一个类似于：hover的伪类。为了解决这种以及其他情况，sass提供了一个特殊结 构&。

#### 	:globe_with_meridians:父选择器的标识符& ####

一般情况下，sass在解开一个嵌套规则时就会把父选择器（#content）通过一个空格连接到子选择器的前边（article和aside）形成（#content article和#content aside）。这种在CSS里边被称为后代选择器，因为它选择ID为content的元素内所有命中选择器article和aside的元素。但在有些情况下你却不会希望sass使用这种后代选择器的方式生成这种连接。

最常见的一种情况是当你为链接之类的元素写：hover这种伪类时，你并不希望以后代选择器的方式连接。比如说，下面这种情况sass就无法正常工作：

```sass
article a {
  color: blue;
  :hover { color: red }
}
```

这意味着color: red这条规则将会被应用到选择器article a :hover，article元素内链接的所有子元素在被hover时都会变成红色。这是不正确的！你想把这条规则应用到超链接自身，而后代选择器的方式无法帮你实现。

解决之道为使用一个特殊的sass选择器，即父选择器。在使用嵌套规则时，父选择器能对于嵌套规则如何解开提供更好的控制。它就是一个简单的&符号，且可以放在任何一个选择器可出现的地方，比如h1放在哪，它就可以放在哪。

```sass
article a {
  color: blue;
  &:hover { color: red }
}
```

当包含父选择器标识符的嵌套规则被打开时，它不会像后代选择器那样进行拼接，而是&被父选择器直接替换：

```sass
article a { color: blue }
article a:hover { color: red }
```

在为父级选择器添加：hover等伪类时，这种方式非常有用。同时父选择器标识符还有另外一种用法，你可以在父选择器之前添加选择器。举例来说，当用户在使用IE浏览器时，你会通过JavaScript在<body>标签上添加一个ie的类名，为这种情况编写特殊的样式如下：

```sass
#content aside {
  color: red;
  body.ie & { color: green }
}

/*编译后*/
#content aside {color: red};
body.ie #content aside { color: green }
```

sass在选择器嵌套上是非常智能的，即使是带有父选择器的情况。当sass遇到群组选择器（由多个逗号分隔开的选择器形成）也能完美地处理这种嵌套。

#### 	:globe_with_meridians:群组选择器的嵌套 ####

在CSS里边，选择器h1h2和h3会同时命中h1元素、h2元素和h3元素。与此类似，.button button会命中button元素和类名为.button的元素。这种选择器称为群组选择器。群组选择器 的规则会对命中群组中任何一个选择器的元素生效。

```css
.button, button {
  margin: 0;
}
```

当看到上边这段代码时，你可能还没意识到会有重复性的工作。但会很快发现：如果你需要在一个特定的容器元素内对这样一个群组选择器进行修饰，情况就不同了。css的写法会让你在群组选择器中的每一个选择器前都重复一遍容器元素的选择器。

```css
.container h1, .container h2, .container h3 { margin-bottom: .8em }
```

非常幸运，sass的嵌套特性在这种场景下也非常有用。当sass解开一个群组选择器规则内嵌的规则时，它会把每一个内嵌选择器的规则都正确地解出来：

```css
.container {
  h1, h2, h3 {margin-bottom: .8em}
}
```

首先sass将.container和h1.container和h2.container和h3分别组合，然后将三 者重新组合成一个群组选择器，生成你前边看到的普通css样式。对于内嵌在群组选择器内的嵌 套规则，处理方式也一样：

```sass
nav, aside {
  a {color: blue}
}
```

首先sass将nav和aaside和a分别组合，然后将二者重新组合成一个群组选择器：

```css
nav a, aside a {color: blue}
```

处理这种群组选择器规则嵌套上的强大能力，正是sass在减少重复敲写方面的贡献之一。尤其在当嵌套级别达到两层甚至三层以上时，与普通的css编写方式相比，只写一遍群组选择器大大减少了工作量。

有利必有弊，你需要特别注意群组选择器的规则嵌套生成的css。虽然sass让你的样式表看上去很小，但实际生成的css却可能非常大，这会降低网站的速度。

#### 	:globe_with_meridians:嵌套属性 ####

在sass中，除了CSS选择器，属性也可以进行嵌套。尽管编写属性涉及的重复不像编写选择器那么糟糕，但是要反复写`border-styleborder-widthborder-color`以及`border-*`等也是非常烦人的。在sass中，你只需敲写一遍border：

```sass
nav {
  border: {
  style: solid;
  width: 1px;
  color: #ccc;
  }
}
```

嵌套属性的规则是这样的：把属性名从中划线-的地方断开，在根属性后边添加一个冒号:，紧跟一个{ }块，把子属性部分写在这个{ }块中。就像css选择器嵌套一样，sass会把你的子属性一一解开，把根属性和子属性部分通过中划线-连接起来，最后生成的效果与你手动一遍遍写的css样式一样：

```sass
nav {
  border-style: solid;
  border-width: 1px;
  border-color: #ccc;
}
```

对于属性的缩写形式，你甚至可以像下边这样来嵌套，指明例外规则：

```sass
nav {
  border: 1px solid #ccc {
  left: 0px;
  right: 0px;
  }
}
```

这比下边这种同等样式的写法要好：

```sass
nav {
  border: 1px solid #ccc;
  border-left: 0px;
  border-right: 0px;
}
```

属性和选择器嵌套是非常伟大的特性，因为它们不仅大大减少了你的编写量，而且通过视觉上的缩进使你编写的样式结构更加清晰，更易于阅读和开发。

即便如此，随着你的样式表变得越来越大，这种写法也很难保持结构清晰。有时，处理这种大量样式的唯一方法就是把它们分拆到多个文件中。sass通过对css原有@import规则的改进直接支持了这一特性。

<p id="a5"></p>
       
### :fish:混合器 ###

:arrow_double_up:<a href ="#tit">返回目录</a>
  
如果你的整个网站中有几处小小的样式类似（例如一致的颜色和字体），那么使用变量来统一处理这种情况是非常不错的选择。但是当你的样式变得越来越复杂，你需要大段大段的重用样式的代码，独立的变量就没办法应付这种情况了。你可以通过sass的混合器实现大段样式的重用。

混合器使用@mixin标识符定义。看上去很像其他的CSS @标识符，比如说@media或者@font-face。这个标识符给一大段样式赋予一个名字，这样你就可以轻易地通过引用这个名字重用这段样式。下边的这段sass代码，定义了一个非常简单的混合器，目的是添加跨浏览器的圆角边框。

```sass
@mixin rounded-corners {
  -moz-border-radius: 5px;
  -webkit-border-radius: 5px;
  border-radius: 5px;
}
```

然后就可以在你的样式表中通过@include来使用这个混合器，放在你希望的任何地方。@include调用会把混合器中的所有样式提取出来放在@include被调用的地方。与其他编程语言的函数一样，创建并调用，如果像下边这样写：

```sass
notice {
  background-color: green;
  border: 2px solid #00aa00;
  @include rounded-corners;
}

//sass最终生成：

.notice {
  background-color: green;
  border: 2px solid #00aa00;
  -moz-border-radius: 5px;
  -webkit-border-radius: 5px;
  border-radius: 5px;
}
```

在.notice中的属性border-radius-moz-border-radius和-webkit-border-radius全部来自rounded-corners这个混合器。这一节将介绍使用混合器来避免重复。通过使用参数，你可以使用混合器把你样式中的通用样式抽离出来，然后轻松地在其他地方重用。实际上，混合器太好用了，一不小心你可能会过度使用。大量的重用可能会导致生成的样式表过大，导致加载缓慢。所以，首先我们将讨论混合器的使用场景，避免滥用。
  
#### 	:globe_with_meridians:混合器中的CSS规则 ####

混合器中不仅可以包含属性，也可以包含css规则，包含选择器和选择器中的属性，如下代码:

```sass
@mixin no-bullets {
  list-style: none;
  li {
    list-style-image: none;
    list-style-type: none;
    margin-left: 0px;
  }
}
```

当一个包含css规则的混合器通过@include包含在一个父规则中时，在混合器中的规则最终会生成父规则中的嵌套规则。举个例子，看看下边的sass代码，这个例子中使用了no-bullets这个混合器：

```sass
ul.plain {
  color: #444;
  @include no-bullets;
}
```

sass的@include指令会将引入混合器的那行代码替换成混合器里边的内容。最终，上边的例子如下代码:

```sass
ul.plain {
  color: #444;
  list-style: none;
}
ul.plain li {
  list-style-image: none;
  list-style-type: none;
  margin-left: 0px;
}
```

混合器中的规则甚至可以使用sass的父选择器标识符&。使用起来跟不用混合器时一样，sass解开嵌套规则时，用父规则中的选择器替代&。

如果一个混合器只包含css规则，不包含属性，那么这个混合器就可以在文档的顶部调用，写在所有的css规则之外。如果你只是为自己写一些混合器，这并没有什么大的用途，但是当你使用一个类似于Compass的库时，你会发现，这是提供样式的好方法，原因在于你可以选择是否使用这些样式。

接下来你将学习如何通过给混合器传参数来让混合器变得更加灵活和可重用。
  
#### 	:globe_with_meridians: 给混合器传参 #### 
  
混合器并不一定总得生成相同的样式。可以通过在@include混合器时给混合器传参，来定制混合器生成的精确样式。当@include混合器时，参数其实就是可以赋值给css属性值的变量。如果你写过JavaScript，这种方式跟JavaScript的function很像：

```sass
@mixin link-colors($normal, $hover, $visited) {
  color: $normal;
  &:hover { color: $hover; }
  &:visited { color: $visited; }
}
```

当混合器被@include时，你可以把它当作一个css函数来传参。如果你像下边这样写：

```sass
a {
  @include link-colors(blue, red, green);
}
```

//Sass最终生成的是：

```sass
a { color: blue; }
a:hover { color: red; }
a:visited { color: green; }
```

当你@include混合器时，有时候可能会很难区分每个参数是什么意思，参数之间是一个什么样的顺序。为了解决这个问题，sass允许通过语法$name: value的形式指定每个参数的值。这种形式的传参，参数顺序就不必再在乎了，只需要保证没有漏掉参数即可：

```sass
a {
    @include link-colors(
      $normal: blue,
      $visited: green,
      $hover: red
  );
}
```

尽管给混合器加参数来实现定制很好，但是有时有些参数我们没有定制的需要，这时候也需要赋值一个变量就变成很痛苦的事情了。所以sass允许混合器声明时给参数赋默认值。
  
<p id="a6"></p>
       
### :fish:使用选择器继承来精简CSS ###

:arrow_double_up:<a href ="#tit">返回目录</a>  
 
 使用sass的时候，最后一个减少重复的主要特性就是选择器继承。基于Nicole Sullivan面向对象的css的理念，选择器继承是说一个选择器可以继承为另一个选择器定义的所有样式。这个通过@extend语法实现，如下代码:

```sass
//通过选择器继承继承样式
.error {
  border: 1px solid red;
  background-color: #fdd;
}
.seriousError {
  @extend .error;
  border-width: 3px;
}
```

在上边的代码中，.seriousError将会继承样式表中任何位置处为.error定义的所有样式。以class="seriousError" 修饰的html元素最终的展示效果就好像是class="seriousError error"。相关元素不仅会拥有一个3px宽的边框，而且这个边框将变成红色的，这个元素同时还会有一个浅红色的背景，因为这些都是在.error里边定义的样式。

.seriousError不仅会继承.error自身的所有样式，任何跟.error有关的组合选择器样式也会被.seriousError以组合选择器的形式继承，如下代码:

```sass
//.seriousError从.error继承样式
.error a{  //应用到.seriousError a
  color: red;
  font-weight: 100;
}
h1.error { //应用到hl.seriousError
  font-size: 1.2rem;
}
```

如上所示，在class="seriousError"的html元素内的超链接也会变成红色和粗体。

本节将介绍与混合器相比，哪种情况下更适合用继承。接下来在探索继承的工作细节之前，我们先了解一下继承的高级用法。最后，我们将看看使用继承可能会有哪些坑，学习如何避免这些坑。

#### 	:globe_with_meridians:何时使用继承 #### 

前面介绍了混合器主要用于展示性样式的重用，而类名用于语义化样式的重用。因为继承是基于类的（有时是基于其他类型的选择器），所以继承应该是建立在语义化的关系上。当一个元素拥有的类（比如说.seriousError）表明它属于另一个类（比如说.error），这时使用继承再合适不过了。

这有点抽象，所以我们从几个方面来阐释一下。想象一下你正在编写一个页面，给html元素添加类名，你发现你的某个类（比如说.seriousError）另一个类（比如说.error）的细化。你会怎么做？

你可以为这两个类分别写相同的样式，但是如果有大量的重复怎么办？使用sass时，我们提倡的就是不要做重复的工作。
你可以使用一个选择器组（比如说.error.seriousError）给这两个选择器写相同的样式。如果.error的所有样式都在同一个地方，这种做法很好，但是如果是分散在样式表的不同地方呢？再这样做就困难多了。
你可以使用一个混合器为这两个类提供相同的样式，但当.error的样式修饰遍布样式表中各处时，这种做法面临着跟使用选择器组一样的问题。这两个类也不是恰好有相同的 样式。你应该更清晰地表达这种关系。
综上所述你应该使用@extend。让.seriousError从.error继承样式，使两者之间的关系非常清晰。更重要的是无论你在样式表的哪里使用.error.seriousError都会继承其中的样式。
现在你已经更好地掌握了何时使用继承，以及继承有哪些突出的优点，接下来我们看看一些高级用法。

#### 	:globe_with_meridians:继承的高级用法 #### 

任何css规则都可以继承其他规则，几乎任何css规则也都可以被继承。大多数情况你可能只想对类使用继承，但是有些场合你可能想做得更多。最常用的一种高级用法是继承一个html元素的样式。尽管默认的浏览器样式不会被继承，因为它们不属于样式表中的样式，但是你对html元素添加的所有样式都会被继承。

接下来的这段代码定义了一个名为disabled的类，样式修饰使它看上去像一个灰掉的超链接。通过继承a这一超链接元素来实现：

```sass
.disabled {
  color: gray;
  @extend a;
}
```

假如一条样式规则继承了一个复杂的选择器，那么它只会继承这个复杂选择器命中的元素所应用的样式。举例来说， 如果.seriousError@extend.important.error ， 那么.important.error 和h1.important.error 的样式都会被.seriousError继承， 但是.important或者.error下的样式则不会被继承。这种情况下你很可能希望.seriousError能够分别继承.important或者.error下的样式。

如果一个选择器序列（#main .seriousError）@extend另一个选择器（.error），那么只有完全匹配#main .seriousError这个选择器的元素才会继承.error的样式，就像单个类 名继承那样。拥有class="seriousError"的#main元素之外的元素不会受到影响。

像#main .error这种选择器序列是不能被继承的。这是因为从#main .error中继承的样式一般情况下会跟直接从.error中继承的样式基本一致，细微的区别往往使人迷惑。

现在你已经了解了通过继承能够做些什么事情，接下来我们将学习继承的工作细节，在生成对应css的时候，sass具体干了些什么事情。

#### 	:globe_with_meridians:继承的工作细节 #### 

跟变量和混合器不同，继承不是仅仅用css样式替换@extend处的代码那么简单。为了不让你对生成的css感觉奇怪，对这背后的工作原理有一定了解是非常重要的。

@extend背后最基本的想法是，如果.seriousError @extend .error， 那么样式表中的任何一处.error都用.error.seriousError这一选择器组进行替换。这就意味着相关样式会如预期那样应用到.error和.seriousError。当.error出现在复杂的选择器中，比如说h1.error.error a或者`#main .sidebar input.error[type="text"]，`那情况就变得复杂多了，但是不用担心，sass已经为你考虑到了这些。

关于@extend有两个要点你应该知道。

跟混合器相比，继承生成的css代码相对更少。因为继承仅仅是重复选择器，而不会重复属性，所以使用继承往往比混合器生成的css体积更小。如果你非常关心你站点的速度，请牢记这一点。
继承遵从css层叠的规则。当两个不同的css规则应用到同一个html元素上时，并且这两个不同的css规则对同一属性的修饰存在不同的值，css层叠规则会决定应用哪个样式。相当直观：通常权重更高的选择器胜出，如果权重相同，定义在后边的规则胜出。
混合器本身不会引起css层叠的问题，因为混合器把样式直接放到了css规则中，而继承存在样式层叠的问题。被继承的样式会保持原有定义位置和选择器权重不变。通常来说这并不会引起什么问题，但是知道这点总没有坏处。

#### 	:globe_with_meridians:使用继承的最佳实践 #### 

通常使用继承会让你的css美观、整洁。因为继承只会在生成css时复制选择器，而不会复制大段的css属性。但是如果你不小心，可能会让生成的css中包含大量的选择器复制。

避免这种情况出现的最好方法就是不要在css规则中使用后代选择器（比如.foo .bar）去继承css规则。如果你这么做，同时被继承的css规则有通过后代选择器修饰的样式，生成css中的选择器的数量很快就会失控：

```sass
.foo .bar { @extend .baz; }
.bip .baz { a: b; }
```

在上边的例子中，sass必须保证应用到.baz的样式同时也要应用到.foo .bar（位于class="foo"的元素内的class="bar"的元素）。例子中有一条应用到.bip .baz（位于class="bip"的元素内的class="baz"的元素）的css规则。当这条规则应用到.foo .bar时，可能存在三种情况，如下代码:

```html
<div class="foo">
  <div class="bip">
    <div class="bar">...</div>
  </div>
</div>
<div class="bip">
  <div class="foo">
    <div class="bar">...</div>
  </div>
</div>
<div class="foo bip">
  <div class="bar">...</div>
</div>
```

为了应付这些情况，sass必须生成三种选择器组合（仅仅是.bip .foo .bar不能覆盖所有情况）。如果任何一条规则里边的后代选择器再长一点，sass需要考虑的情况就会更多。实际上sass并不总是会生成所有可能的选择器组合，即使是这样，选择器的个数依然可能会变得相当大，所以如果允许，尽可能避免这种用法。

值得一提的是，只要你想，你完全可以放心地继承有后代选择器修饰规则的选择器，不管后代选择器多长，但有一个前提就是，不要用后代选择器去继承。
  
  
  
  
  
  
  
  
  
  
  
