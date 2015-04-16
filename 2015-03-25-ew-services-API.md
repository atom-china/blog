很多插件并不是完全独立地工作的，而是需要依赖于其他插件。例如 [vim-mode](https://atom.io/packages/vim-mode) 依赖于状态栏插件 [status-bar](https://atom.io/packages/status-bar) 来显示当前的 VIM 模式。

<img src="http://atom-china.org/uploads/default/33/fcad508b234c2ee5.png" width="690" height="55"> 

之前像 vim-mode 这样的包需要订阅每个插件被加载的事件，然后去 DOM 查找相应的 UI 元素来实现交互。这样的方式不仅很麻烦，而且很容易在 status-bar 的 API 出现变化后发生错误。

NPM（Node.js 的包管理器）让每个包用 [语义化版本](http://semver.org) 声明依赖的版本，并通过为每个包提供所有依赖的独立副本的方式解决了类似的问题。但 Atom 却不能给每个插件一个单独的 status-bar 副本，因为 Atom 的窗口上只有一个 status-bar.

## 提供服务与消费服务

Atom 提供了一个 [新的服务 API](https://atom.io/docs/latest/behind-atom-interacting-with-packages-via-services) 来解决这个问题，它允许一个插件提供由语义化版本声明的服务 API, 供其他的插件消费（使用）。在前面的例子中，status-bar 可以提供多个版本的 API, 这样当 API 改编的时候，就可以为依赖它的其他插件提供平滑地升级的可能。

服务 API 也从另一个角度为插件开发提供了一种新的可能性，即通过开发具有同样的 API 的插件来替换掉原来的插件。例如如果有人希望实现一个叫 status-bar-plus 的插件来提供更好的状态栏，那么他可以让这个新插件继续实现原来的名为 status-bar 的服务，这样就可以兼容像 vim-mode 这样的，使用了 status-bar 服务的其他插件。这使得新插件的作者与原有的已经被大量依赖的插件，站在了同一个起跑线上。

插件通过 `package.json` 来声明要提供或要消费的服务，例如 status-bar [通过新的服务 API 提供](https://github.com/atom/status-bar/blob/d4da6a42b7e5a8ec8b09807fd0e92cdb6919b0ec/package.json#L16-L23) 了两个版本的服务：

```
"providedServices": {
  "status-bar": {
    "description": "A container for indicators at the bottom of the workspace",
    "versions": {
      "1.0.0": "provideStatusBar",
      "0.58.0": "legacyProvideStatusBar"
    }
  }
}
```

上面的代码允许其他插件通过消费 status-bar 服务的方式去使用 [status-bar 插件的 provideStatusBar 方法](https://github.com/atom/status-bar/blob/076d51ef89f2875ba32219343787d079b4bfbf64/lib/main.coffee#L92-L96) 的返回值，例如 vim-mode 插件在 `package.json` 中声明了：

```
"consumedServices": {
  "status-bar": {
    "versions": {
      "^1.0.0": "consumeStatusBar"
    }
  }
}
```

这样 vim-mode 就可以在 [consumeStatusBar 方法](https://github.com/atom/vim-mode/blob/762a480c93cc444746c1a8150b5a24db90836144/lib/vim-mode.coffee#L42-L46) 中去获取 status-bar 的 provideStatusBar 方法的返回值对象，通过这个对象可以在状态栏上显示当前所在的 VIM 模式：

```
consumeStatusBar: (statusBar) ->
    @statusBarManager.initialize(statusBar)
    @statusBarManager.attach()
    @disposables.add new Disposable =>
      @statusBarManager.detach()
```

有关服务 API 的更多信息可以阅读文档的 [Interacting with Other Packages via Services](https://atom.io/docs/latest/behind-atom-interacting-with-packages-via-services)（通过服务 API 与其他插件交互）一节。
