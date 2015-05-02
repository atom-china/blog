我们将会在一个月后的今天，**六月一日**，移除 Atom 中所有已经被弃用（Deprecated）的 API. 来为将会在六月末发布的 Atom 1.0 做准备。

为了让这个迁移过程对于插件作者尽可能平滑，Atom 内建了一个查找并报告使用未升级的 API 的情况的工具；Atom 也提供了一个用来预览这些 API 在 1.0 中完全被移除的模式。

如果你对于迁移你的插件到新的 API 有任何疑问，可以在 [atom/atom](http://github.com/atom/atom/issues) 这个库创建 Issue, 我们也非常乐意帮助你的插件为 1.0 做好准备。

## 查找已弃用的 API 调用

我们在一月份 [发布](http://blog.atom.io/2015/01/15/announcing-the-atom-1-api.html) 了 1.0 API 之后，插件如果使用了弃用的 API, 会在状态栏上产生一个警告，你可以点击它打开一个面板（deprecation cop）查看详情。

<img src="http://atom-china.org/uploads/default/84/96b16f5584aefcfc.png" width="690" height="200"> 

这个界面会告诉你哪些插件使用了哪些弃用的 API, 亦提供了一个到 API 调用发生处的链接，以及一些升级的建议。

<img src="http://atom-china.org/uploads/default/85/bec1e5aa3195185d.png" width="690" height="443"> 

你还可以在运行单元测试时，看到类似的警告：

<img src="http://atom-china.org/uploads/default/86/9f73a2b456bb063c.png" width="690" height="406"> 

## 1.0 API 预览模式

Atom 现在拥有了一个 1.0 API 预览模式，它会打开一个新的 Atom 窗口，在新的窗口中，所有弃用的 API 都已经被彻底地移除了。这将会模拟 Atom 1.0 正式发布时的情况，你可以使用这个功能来确认你使用的所有插件是不是都可以在 Atom 1.0 中正常工作。

在命令行中给 `atom` 命令加上 `--one` 参数就可以启动这个模式。

如果你使用的插件还在使用那些将会在 1.0 中移除的 API, 你将会看到一个有关缺少属性或缺少方法的错误提示。

<img src="http://atom-china.org/uploads/default/87/868f249e95676b60.png" width="690" height="289"> 

你可以通过点击错误提示中的按钮来给作者创建一个 Issue, 催促他升级到新版本的 API 然后发布一个新版本。

你需要把 Atom 升级到 0.196 或更高的版本来获得 API 预览模式的功能。
