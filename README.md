# --------------------------Sass---------------------------- #

<p id="tit"></p>
                       
## :mortar_board:导航 ##

:arrow_down:<a href="#a1">1.l安装及准备工作</a>

:arrow_down:<a href="#a2">2.Sass脚本</a>

:arrow_down:<a href="#a3">3.Sass变量</a>

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
<p id="a2"></p>
       
### :fish: 使用变量  ###

:arrow_double_up:<a href ="#tit">返回目录</a>

sass让人们受益的一个重要特性就是它为css引入了变量。你可以把反复使用的css属性值 定义成变量，然后通过变量名来引用它们，而无需重复书写这一属性值。或者，对于仅使用过一 次的属性值，你可以赋予其一个易懂的变量名，让人一眼就知道这个属性值的用途。

sass使用$符号来标识变量(老版本的sass使用!来标识变量。改成$是多半因为!highlight-color看起来太丑了。)，比如$highlight-color和$sidebar-width。为什么选择$ 符号呢？因为它好认、更具美感，且在CSS中并无他用，不会导致与现存或未来的css语法冲突。

#### 	:globe_with_meridians:变量声明 ####

sass变量的声明和css属性的声明很像：

```
$highlight-color: #F90;
```

这意味着变量$highlight-color现在的值是#F90。任何可以用作css属性值的赋值都 可以用作sass的变量值，甚至是以空格分割的多个属性值，如$basic-border: 1px solid black;，或以逗号分割的多个属性值，如$plain-font: "Myriad Pro"、Myriad、"Helvetica Neue"、Helvetica、"Liberation Sans"、Arial和sans-serif; sans-serif;。这时变 量还没有生效，除非你引用这个变量——我们很快就会了解如何引用。

与CSS属性不同，变量可以在css规则块定义之外存在。当变量定义在css规则块内，那么该变量只能在此规则块内使用。如果它们出现在任何形式的{...}块中（如@media或者@font-face块），情况也是如此：

```
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

```
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

```
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

```
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

```
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


















