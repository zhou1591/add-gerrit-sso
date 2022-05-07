## 版本

稳定版本：[![](https://img.shields.io/npm/v/@authing/native-js-ui-components.svg?style=flat-square)](https://www.npmjs.com/package/@authing/native-js-ui-components)

## 安装

### 使用 npm 或者 yarn 安装

我们这里推荐使用 npm 或 yarn，它们能更好的和 [webpack](https://webpack.js.org/) 打包工具进行配合，也可放心地在生产环境打包部署使用，享受整个生态圈和工具链带来的诸多好处。

```bash
$ npm install @authing/native-js-ui-components --save
```

```bash
$ yarn add @authing/native-js-ui-components
```

如果你的网络环境不佳，我们推荐你使用 [cnpm](https://github.com/cnpm/cnpm)。

### 浏览器引入

在浏览器中使用 `script` 和 `link` 标签直接引入文件，并使用全局变量 `AuthingNativeJsUIComponents`。

我们在 npm 发布包内的 `@authing/native-js-ui-components/lib` 目录下提供了 `index.min.css` 以及 `index.min.js`。

你也可以通过 [![](https://data.jsdelivr.com/v1/package/npm/@authing/native-js-ui-components/badge)](https://www.jsdelivr.com/package/npm/@authing/native-js-ui-components) 或者 [unpkg.com](https://unpkg.com/@authing/native-js-ui-components) 进行下载 `index.min.css` 以及 `index.min.js`。


> 强烈不推荐使用已构建文件，这样无法按需加载，而且难以获得底层依赖模块的 bug 快速修复支持。

## 示例

首先你要在 [Authing Console](https://console.authing.cn) 中获取你的 `应用 ID`。如果你不知道如何获取 `应用 ID`，可以[参考文档](../../guides/faqs/get-app-id-and-secret.md)

### 直接用 `<script>` 引入

```html
<!DOCTYPE html>
<html>

<head>
  <meta charset="UTF-8">
  <!-- JavaScript 代码 -->
  <script src="https://cdn.jsdelivr.net/npm/@authing/native-js-ui-components"></script>

  <!-- CSS 文件 -->
  <link href="https://cdn.jsdelivr.net/npm/@authing/native-js-ui-components/lib/index.min.css" rel="stylesheet">
  </link>

</head>

<body>

  <script>
    var guard = new AuthingNativeJsUIComponents.Guard("AUTHING_APP_ID");
    // 事件监听
    guard.on("load", (authClient) => console.log(authClient));
  </script>
</body>

</html>
```


### 在 JavaScript 项目中引入

```javascript
import { Guard } from "@authing/native-js-ui-components";

// 引入 css 文件
import "@authing/native-js-ui-components/lib/index.min.css";

// 你的 APP ID
const guard = new Guard("AUTHING_APP_ID");

```

### 完整体验

这是一个最简单的 Guard 组件的在线 [codepen](https://codepen.io/) 演示。可以将 `AppId` 修改为你自己的 ID 直接在这里展示。

<iframe height="842" style="width: 100%;" scrolling="no" title="Guard Demo" src="https://codepen.io/xuancaosu/embed/qBpbwmz?default-tab=html%2Cresult&editable=true&theme-id=light" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href="https://codepen.io/xuancaosu/pen/qBpbwmz">
  Guard Demo</a> by Lucsun (<a href="https://codepen.io/xuancaosu">@xuancaosu</a>)
  on <a href="https://codepen.io">CodePen</a>.
</iframe>

### 监听登录事件

你可以通过 `guard.on("login", callback)` 监听登录事件：

```javascript
guard.on("login", (user) => {
  console.log(user);
});
```

在此我们只是简单地把获取到的用户信息 `console.log` 了出来：

用户信息中的 token 字段为该用户的身份凭证，后续访问你后端资源的时候应该带上，然后在后端验证此 token 的身份。

## 实例方法

Guard 实例提供了三个方法：
| 方法名 | 方法参数 | 功能 |
| :----- | :------------------------------------------------------------------------------------ | :------------------- |
| on | <p>evtName: 事件名，详细请查看[事件列表](./parameters.md)</p><p>Handler: 对应事件的处理函数</p> | 监听某个事件 |
| show | - | modal 模式中显示表单 |
| hide | - | modal 模式中隐藏表单 |

