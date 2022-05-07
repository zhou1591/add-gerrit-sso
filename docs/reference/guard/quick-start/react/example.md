## 版本

稳定版本：[![](https://img.shields.io/npm/v/@authing/react-ui-components.svg?style=flat-square)](https://www.npmjs.com/package/@authing/react-ui-components)

### 使用 npm 或者 yarn 安装

我们这里推荐使用 npm 或 yarn，它们能更好的和 [webpack](https://webpack.js.org/) 打包工具进行配合，也可放心地在生产环境打包部署使用，享受整个生态圈和工具链带来的诸多好处。

```bash
$ yarn add @authing/react-ui-components

# OR

$ npm install @authing/react-ui-components --save
```

如果你的网络环境不佳，我们推荐你使用 [cnpm](https://github.com/cnpm/cnpm)。

### 浏览器引入

在浏览器中使用 `script` 和 `link` 标签直接引入文件，并使用全局变量 `AuthingReactUIComponents`。

我们在 npm 发布包内的 `@authing/react-ui-components/lib` 目录下提供了 `index.min.css` 以及 `index.min.js`。

你也可以通过 [![](https://data.jsdelivr.com/v1/package/npm/@authing/react-ui-components/badge)](https://www.jsdelivr.com/package/npm/@authing/react-ui-components) 或者 [unpkg.com](https://unpkg.com/@authing/react-ui-components) 进行下载 `index.min.css` 以及 `index.min.js`。

> 注意：react-ui-components 依赖 React，请确保提前引入 React 文件。

## 示例

首先你要在 [Authing Console](https://console.authing.cn) 中获取你的 `应用 ID`。如果你不知道如何获取 `应用 ID`，可以[参考文档](../../guides/faqs/get-app-id-and-secret.md)

### 在 React 项目中引入

#### 初始化

```javascript
import React from "react";
import ReactDOM from "react-dom";
import { Guard } from "@authing/react-ui-components";
// 引入 css 文件
import "@authing/react-ui-components/lib/index.min.css";

const App = () => {
  const appId = "AUTHING_APP_ID";
  const onLogin = userInfo => {
    console.log(userInfo);
  };
  return <Guard appId={appId} onLogin={onLogin} />;
};

ReactDOM.render(<App />, document.getElementById("root"));
```

### 直接用 `<script>` 引入

#### CDN 引入

```html
<html lang="en">

<head>
  <meta charset="utf-8" />
  <!-- 引入 babel，支持 jsx -->
  <script src="https://cdn.jsdelivr.net/npm/babel-standalone@6.26.0/babel.min.js"></script>

  <!-- 引入 React -->
  <script src="https://cdn.jsdelivr.net/npm/react@16.14.0/umd/react.production.min.js" crossorigin></script>
  <script src="https://cdn.jsdelivr.net/npm/react-dom@16.14.0/umd/react-dom.production.min.js" crossorigin></script>

  <!-- JavaScript 代码 -->
  <script>
    window.react = React
    window['react-dom'] = ReactDOM
  </script>
  <script src="https://cdn.jsdelivr.net/npm/@authing/react-ui-components"></script>

  <!-- CSS 文件 -->
  <link href="https://cdn.jsdelivr.net/npm/@authing/react-ui-components/lib/index.min.css" rel="stylesheet">
  </link>
</head>

<body>
  <div id="root"></div>
  <script>
    var App = () => {
      const appId = "AUTHING_APP_ID";
      const onLogin = userInfo => {
        console.log(userInfo);
      };
      return React.createElement(
        AuthingReactUIComponents.Guard, {
          appId: appId,
          onLogin: onLogin,
        },
      )
    };
    ReactDOM.render(React.createElement(App), document.getElementById("root"));
  </script>
</body>

</html>
```

### 完整体验

这是一个最简单的 Guard 组件的在线 [codepen](https://codepen.io/) 演示。可以将 `AppId` 修改为你自己的 ID 直接在这里展示。

<iframe height="760" style="width: 100%;" scrolling="no" title="Untitled" src="https://codepen.io/xuancaosu/embed/rNJOvBO?default-tab=html%2Cresult&editable=true&theme-id=light" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href="https://codepen.io/xuancaosu/pen/rNJOvBO">
  Untitled</a> by Lucsun (<a href="https://codepen.io/xuancaosu">@xuancaosu</a>)
  on <a href="https://codepen.io">CodePen</a>.
</iframe>

### 监听登录事件

`Guard` 组件传入 `onLogin` 事件回调函数，当用户成功登录时回调用此函数，你可以在此获取当前用户的用户信息。[查看完整事件列表](#完整参数)。

```javascript
import { Guard } from "@authing/react-ui-components";
import "@authing/react-ui-components/lib/index.min.css";

function App() {
  return (
    <div className="App">
      <Guard
        appId="AUTHING_APP_ID"
        onLogin={userinfo => {
          console.log(userinfo);
        }}
      />
    </div>
  );
}
```

在此我们只是简单地把获取到的用户信息 `console.log` 了出来：

用户信息中的 token 字段为该用户的身份凭证，后续访问你后端资源的时候应该带上，然后在后端验证此 token 的身份。