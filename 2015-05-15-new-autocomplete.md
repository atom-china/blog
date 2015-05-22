在 Atom 的 0.199.0 版本中，我们首次将一个社区开发的插件 —— [autocomplete-plus](https://github.com/atom/autocomplete-plus) 捆绑到了 Atom 中，作为官方发行版的一部分。

[@joefitzgerald](https://github.com/joefitzgerald), [@saschagehlich](https://github.com/saschagehlich) 以及 [@park9140](https://github.com/park9140) 改进了默认的 autocomplete 插件，提高了补全建议的准确性，随着输入实时地提供建议，并且实现了高拓展性。autocomplete-plus 像野火一样蔓延，被下载了 33 万次，是整个 Atom 生态系统中最受欢迎的插件。所以现在 autocomplete-plus 替换了原来的 autocomplete 插件。

## 新功能

当你更新之后，你会看到两个最显著的改进：在你输入字符时补全建议就会自走的那个出现，而且每个补全建议都有一个彩色的图标。

<img src="http://atom-china.org/uploads/default/107/d3a8461933056a8e.png" width="690" height="445"> 

补全建议中会包括所有已打开的文档中的符号（Symbol），包括函数、变量、字符串中的单词。左面的图标会告诉你这个符号的类型，箭头表示代码片段（Snippet），`v` 代表变量，`c` 代表类（Class），`f` 代表函数。

Atom 0.199.0 版本开始，补全建议中除了符号还会包括更高智能的，对 HTML, CSS, Atom API 和代码片段的补全。

## HTML

在 HTML 和众多基于 HTML 的模板语言（例如 PHP 和 ERB）中，现在会对标签、属性、属性值提供补全建议，同时还会显示它们的描述，以及一个指向 MDN 的链接。

![](https://cloud.githubusercontent.com/assets/69169/7637208/15859d98-fa21-11e4-87db-cae05b14d367.gif)

## CSS

在 Atom 0.199.0 中借助属性和值的自动提示来写 CSS 将会变得容易得多。CSS 补全在基于 CSS 的语言（例如 LESS 和 SCSS）中同样可用，而且也会有针对 LESS 和 SCSS 内建函数（例如 `darken` 和 `fadeout`）的补全。

![](https://cloud.githubusercontent.com/assets/69169/7637610/14a8521e-fa24-11e4-8905-a587773eb7bd.gif)

## Atom API

Atom 现在会为 `atom` 这个全局变量提供补全，就像 HTML 和 CSS 的补全一样，补全列表的下方会显示这个 API 的描述，和指向 atom.io 的文档的链接。只需在你的插件中的 JavaScript 或 CoffeeScript 文件里输入 `atom.` 就可以显示这个补全列表了。

<img src="http://atom-china.org/uploads/default/108/1eb9fe6a86e6ab29.png" width="690" height="134"> 

## 代码片段

[Snippets](https://atom.io/docs/latest/using-atom-snippets) 可以帮助你非常方便地输入常用的代码片段，例如引入模块（require）、函数（function）、循环（loop）等等。补全建议中箭头图标表示这是一个代码片段，它们对于很多种文件类型都是可用的。

<img src="http://atom-china.org/uploads/default/109/4e485b1558615200.png" width="690" height="136"> 

## 拓展性

最令 Atom 核心团队激动的是 autocomplete-plus 的拓展性。autocomplete-plus 可以使用（Consume ）来自其他插件提供的对于特定语言的补全驱动，例如 [haskell](https://atom.io/packages/autocomplete-haskell)，或者对于特定情况的补全，例如当你引入一个模块时 [补全文件路径](https://atom.io/packages/autocomplete-paths).

所有的智能补全功能，例如对 HTML, CSS, Atom API 和代码片段的补全，都是被内置在官方发行版中的插件驱动的：[autocomplete-html](https://atom.io/packages/autocomplete-html), [autocomplete-css](https://atom.io/packages/autocomplete-css), [autocomplete-atom-api](https://atom.io/packages/autocomplete-atom-api), [autocomplete-snippets](https://atom.io/packages/autocomplete-snippets).

除了内置的补全驱动，还有很多社区开发的驱动插件，可以为你常用的语言提供更智能的补全：[JavaScript](https://atom.io/packages/atom-ternjs), [TypeScript](https://atom.io/packages/atom-typescript), [Python](https://atom.io/packages/autocomplete-plus-python-jedi), [Golang](https://atom.io/packages/go-plus), [C#](https://atom.io/packages/omnisharp-atom). 更多的驱动列表可以在 [Autocomplete Plus 的 WIKI 页面](https://github.com/atom/autocomplete-plus/wiki/Autocomplete-Providers) 上找到。

`atom-ternjs` 驱动：

<img src="http://atom-china.org/uploads/default/112/c4e013bc38c35661.png" width="690" height="203"> 

`autocomplete-plus-python-jedi` 驱动：

<img src="http://atom-china.org/uploads/default/113/66da74725e42ac86.png" width="690" height="94"> 

### 自己编写驱动

你可以参考 [Autocomplete 驱动 API 文档](https://github.com/atom/autocomplete-plus/wiki/Provider-API) 和上面列出的驱动插件来了解如何编写驱动。

很多语言的静态分析工具和补全系统都可以被集成到一个 autocomplete-plus 驱动插件中：[ternjs](http://ternjs.net) 提供了 JavaScript 的支持，[jedi](https://github.com/davidhalter/jedi) 提供了 Python 的支持，[rsense](https://github.com/rsense/rsense) 提供了 Ruby 的支持，[clang](https://github.com/benogle/autocomplete-clang#clang-notes) 提供了 C/C++ 以及 Objective-C 的支持。借助这些工具，autocomplete-plus 的驱动相当于是 Atom 和这些深度分析工具之间的一些胶水代码。

### 更好的语言支持

如果你安装了多个补全驱动，那么这些驱动提供的建议会被整合到一起，详细信息可以在 [SymbolProvider API 文档](https://github.com/atom/autocomplete-plus/wiki/SymbolProvider-Config-API) 和 [语言示例插件](https://github.com/atom/language-less/blob/43ccc24025dbcefa1268d85576d3398845c46926/settings/language-less.cson#L4-L11) 中找到。

## 展望

我们对于 autocomplete-plus 感到非常激动，不仅仅是以为它本身提供的功能，更多的是它的开发过程。Atom 的哲学就是持续地改进，我们觉得这是 Atom 的一次巨大的进步：autocomplete-plus 从一个简单的插件的社区分支逐渐演变成了一个功能强大且可拓展的插件。我们相信可拓展和模块化的架构并非可有可无，而是构建像 Atom 这样复杂架构的软件所必须的要素。Atom 的力量建立在社区的力量之上，我们觉得 autocomplete-plus 是 Atom 拥有充满活力和创造力的社区的一个最好的例子。

最后，非常感谢 [@joefitzgerald](https://github.com/joefitzgerald), [@saschagehlich](https://github.com/saschagehlich) 和 [@park9140](https://github.com/park9140) 创造了 autocomplete-plus. 也感谢所有驱动的作者，尤其是 [@basarat](https://github.com/basarat), [@tststs](https://github.com/tststs), [@tinloaf](https://github.com/tinloaf), [@eqot](https://github.com/eqot), [@ctolkien](https://github.com/ctolkien), 他们在此期间一直保证他们的插件使用了最新的 API.
