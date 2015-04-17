我们最近为 Atom 添加了在同一个窗口中打开多个目录的功能，如果你经常需要跨越多个目录来编辑文件的话，相信你会觉得这个功能很有用。

<img src="http://atom-china.org/uploads/default/48/071193e115443960.png" width="544" height="500"> 

## 使用

你可以在命令行运行 Atom 的时候传递多个路径作为参数：

```
atom ./first/folder ./second/folder
```

你也可以在命令面板中用 `Application: Add Project Folder` 来向已有的 Atom 窗口中添加目录，对应的快捷键在 Mac 上是 `cmd-shift-o`, 在 Linux 和 Windows 上是 `ctrl-alt-o`.

如果想要从项目中移除一个目录，你可以在目录树上点击右键，然后选择 `Remove Project Folder`, 你也可以使用右键选单中的 `Add Project Folder` 来添加目录。

目录 Atom 的所有内建插件都已经支持包含多个目录的项目了，例如：

* 如果你使用 ctags, 你可以用 `Symbols View: Go To Declaration` 命令从一个目录中的符号跳转到这个符号在另一个目录中的定义。
* 查找和替换默认会搜索所有的目录。如果想要只搜索某个目录，你可以在 `File/Directory pattern` 字段中指定。
* 模糊查找框会查找来自所有目录中的文件。你可以在通过输入某个目录的名字（的前几个字符）来限制只在某个目录中查找。

## 升级你的插件

如果你维护的插件使用了 [atom.project](https://atom.io/docs/api/latest/Project), 我们希望你确保它支持了包含多个目录的项目，我们对 `Project` API 做了一些修改：

* 如果你想找到一个绝对路径所对应的项目，你可以使用 [atom.project.relativizePath(filePath)](https://atom.io/docs/api/latest/Project#instance-relativizePath), 它会返回这个绝对路径对应的项目，和它在项目中的相对路径。[fuzzy-finder](https://github.com/atom/fuzzy-finder) 插件就 [用了这个 API](https://github.com/atom/fuzzy-finder/blob/5a9c0a4f26691f723571bc3b68f15e4938aa8cf0/lib/fuzzy-finder-view.coffee#L153) 来缩写文件路径。
* 你可以用 [atom.project.repositoryForDirectory(directory)](https://atom.io/docs/api/latest/Project#instance-repositoryForDirectory) 获取一个目录对应的 Git 仓库。Atom 的 [TextEditor](https://atom.io/docs/api/latest/TextEditor) 就 [用到了这个 API](https://github.com/atom/atom/blob/74a627d41b41ce39e0a5ad43a08dbd4ce2a46fcc/src/text-editor.coffee#L593) 来实现 `Editor: Checkout Head Revision` 命令。

## 展望

我们正在采取更多措施来改进 Atom 对同时编辑多个目录的支持，我们创建了 [一个 Issue](https://github.com/atom/atom/issues/5728) 来接收反馈，如果你有更好的主意请告诉我们。
