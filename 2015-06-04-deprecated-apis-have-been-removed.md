在刚发布的 [v0.206.0](https://github.com/atom/atom/releases/tag/v0.206.0) 版本中，被弃用的 API 默认将会是不可用的，使用了这些 API 的包则不会被加载。

## 历程
因为我们仅使用公开的 API 来开发内建的包（Internal Package），所以在发布 Atom 之后，我们以实际需求为导向，到处添加 API. 结果导致了 API 并不完整又显得不够一致，不过这是衍化出今天的 API 所必经的步骤。这是一个探索的过程，比如 API 需要实现什么功能？又应该如何暴露这些 API 呢？这些早期的 API 则是探索的过程中产生的草稿。

在将 Atom 开源之后，有上百个包使用这些 API, 我们必须更加深入地思考这些 API. 我们发现了大家在关注 [服务机制的实现](https://github.com/atom/atom/pull/5277)，[更好的命令管理机制](https://github.com/atom/atom/pull/3469)，以及 [用于减少重复工作的装饰器](http://blog.atom.io/2014/07/24/decorations.html)。 基于这些了解，我们对 API 进行了一次主要的重构，在 [大概六个月前](http://blog.atom.io/2015/01/15/announcing-the-atom-1-api.html) 发布了 [新的 1.0 API](https://atom.io/docs/api/latest/Atom).

在这之后，出现了 1000 多个新的包，还有 800 个包升级过，新的 API 则没有再经过大的修改。

## 变化

### 更快
Atom `v0.206.0` 的启动速度和使用时性能都得到了提高 —— 因为不必再触发旧版的事件，也不必为了兼容旧版创建一些不必要的对象。移除这些 这些 API 也将我们从保持兼容性的繁杂工作中解放了出来。

### 一些包将不会被加载

这里有一份包含了 [172 个未升级到新版 API 的包](https://gist.github.com/benogle/afad37e6c8de58272128) 的列表，Atom 从 v0.206.0 之后将不会加载这些包，你会收到一个通知：

<img src="http://atom-china.org/uploads/default/original/1X/cd1fa28fbe7adbeb31a558ee07b3cf909858dd65.png" width="690" height="284"> 

点击按钮则会在设置界面中告诉你为什么这些包无法被加载。

<img src="http://atom-china.org/uploads/default/original/1X/095413df429c52102524696a7e222967a81eef6f.png" width="623" height="500"> 

当然这些包也并非永远无法使用，一旦作者将某个包升级到了最新的 API, 你就可以使用它了。如果你在 [这个列表](https://gist.github.com/benogle/afad37e6c8de58272128) 上看到了你在使用的插件，你也不必太担心，你可以为这个包的仓库创建一个 Issue 来反应情况，或者直接帮助作者来维护这个包。

## 短期解决方案
在接下来的一小段时间，你依然可以用 `--include-deprecated-apis` 这个启动参数来让 Atom 继续保留被弃用的 API, 这样你就可以继续使用暂未升级的包了。但我们将会在六月末移除这个功能，因此这只是一个短期的解决方案。

## 结尾
尽管对于一些包将无法使用我们表示很通信，但移除弃用的 API 将会为我们带来一个更加严格、更加一致、性能更好的 Atom. 精简 API 是我们发布 Atom 1.0 的步骤之一，可以解决代码中的一些历史遗留问题，让核心团队专注于用户所关心的功能。

非常感谢在 [最后两个星期](https://github.com/atom/atom/issues/6867) 中升级了他们的包的作者，他们让这次 API 精简带来的影响减少了许多。
