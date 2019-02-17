# --------------------------Sass---------------------------- #

<p id="tit"></p>
                       
## :mortar_board:导航 ##

:arrow_down:<a href="#a1">1.l安装及准备工作</a>

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
