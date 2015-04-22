Atom [0.193.0](https://github.com/atom/atom/releases/tag/v0.193.0) 发布了，这个版本带来了一些显著的改进。

## 调整窗格宽度

调整窗格的宽度或高度是 [很多人期待的功能](https://github.com/atom/atom/issues/274) 之一，社区成员 [@liuxiong332](https://github.com/liuxiong332) 推动了 [这项工作](https://github.com/atom/atom/pull/5902) 的完成，感谢 @liuxiong332.

<img src="http://atom-china.org/uploads/default/64/fcb9592b94cc9505.png" width="657" height="500"> 

## 恢复程序关闭时的状态

让我们打开 Atom, 创建一些窗口，然后重启 Atom, 然后 ... [我的窗口哪去了](https://github.com/atom/atom/issues/1603)！[@maxbrunsfeld](https://github.com/maxbrunsfeld) 解决了这个问题，现在当你从应用菜单（而不是在命令行用参数）打开 Atom 时，Atom 会恢复到你上次退出时的状态。

<img src="https://cloud.githubusercontent.com/assets/69169/7261869/ee95d346-e829-11e4-87bf-0f595586ed78.gif" width="639" height="500">

## 减少启动耗时

[@kevinsawicki](https://github.com/kevinsawicki) 在提高启动速度上花了很大的功夫，在过去的每个版本中，启动速度都在逐步提高。

`0.193.0` 版本中，我们用 [Asar](https://github.com/atom/asar) 将 [Atom 的源码打包在一起](https://github.com/atom/atom/pull/6313)，在启动时只读取一个文件而不是数千个小文件，进而提高了启动速度。在我 2 年前的 15" Macbook Pro 上，从 0.192.0 更新到 0.193.0 使启动耗时减少了至少 100ms, 大约相当于 15% 的速度提升

0.192.0:

<img src="http://atom-china.org/uploads/default/68/e403134d5b4ef290.png" width="690" height="287"> 

0.193.0:

<img src="http://atom-china.org/uploads/default/69/c9df648e6e84de2e.png" width="690" height="308"> 

用 `atom --one` 以 1.0 预览模式运行 Atom 会更快——在我的电脑上不到 500ms.

<img src="http://atom-china.org/uploads/default/70/929deadb387c5d9d.png" width="690" height="308">

## 提高安装和更新速度

因为使用了 Asar 并 [优化了打包流程](https://github.com/atom/atom/pull/6447)，我们最后减少了 85% 的文件数量，减少了 10% 的文件体积，安装和更新速度提高了至少 50%.

## 接下来的功能

更多的改进正在进行中，例如 [支持编辑 2M 以上的文件](https://github.com/atom/text-document)、[更好的自动补全](https://github.com/atom-community/autocomplete-plus/issues/351) 以及进一步优化启动速度。

我们接下来会在这个博客上介绍我们是如何使用 Asar 优化 Atom 启动速度的。
