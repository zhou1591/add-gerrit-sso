## 版本

稳定版本：[![](https://img.shields.io/npm/v/@authing/vue-ui-components.svg?style=flat-square)](https://www.npmjs.com/package/@authing/vue-ui-components)

## 对于 Vue 的支持

我们对于 Vue2 与 Vue3 同时支持，可以在两种不同版本的 Vue 中直接引入并进行使用。

## 安装

### 使用 npm 或者 yarn 安装

我们这里推荐使用 npm 或 yarn，它们能更好的和 [webpack](https://webpack.js.org/) 打包工具进行配合，也可放心地在生产环境打包部署使用，享受整个生态圈和工具链带来的诸多好处。

```bash
$ npm install @authing/vue-ui-components --save
```

```bash
$ yarn add @authing/vue-ui-components
```

如果你的网络环境不佳，我们推荐你使用 [cnpm](https://github.com/cnpm/cnpm)。

### 浏览器引入

在浏览器中使用 `script` 和 `link` 标签直接引入文件，并使用全局变量 `AuthingVueUIComponents`。

我们在 npm 发布包内的 `@authing/vue-ui-components/lib` 目录下提供了 `index.min.css` 以及 `index.min.js`。

你也可以通过 [![](https://data.jsdelivr.com/v1/package/npm/@authing/vue-ui-components/badge)](https://www.jsdelivr.com/package/npm/@authing/vue-ui-components) 或者 [unpkg.com](https://unpkg.com/@authing/vue-ui-components) 进行下载 `index.min.css` 以及 `index.min.js`。

> 注意：vue-ui-components 依赖 Vue，请确保提前引入 Vue 文件。

## 示例

首先你要在 [Authing Console](https://console.authing.cn) 中获取你的 `应用 ID`。如果你不知道如何获取 `应用 ID`，可以[参考文档](../../guides/faqs/get-app-id-and-secret.md)

### 在 Vue 项目中引入

```html
<template>
  <Guard :appId="appId" />
</template>

<script>
  import { Guard } from "@authing/vue-ui-components";

  // 引入 CSS 文件
  import "@authing/vue-ui-components/lib/index.min.css";

  export default {
    components: {
      Guard,
    },
    data() {
      return {
        // 你的 AppId
        appId: "AUTHING_APP_ID",
      };
    },
  };
</script>
```

#### 初始化

在 Vue.js 项目中引入 `@authing/vue-ui-components` 并初始化。

```html
<template>
  <Guard :appId="appId" />
</template>

<script>
  import { Guard } from "@authing/vue-ui-components";
  import "@authing/vue-ui-components/lib/index.min.css";

  export default {
    components: {
      Guard,
    },
    data() {
      return {
        appId: "AUTHING_APP_ID",
      };
    },
  };
</script>
```

### 直接用 `<script>` 引入

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <script src="https://cdn.jsdelivr.net/npm/vue@2.6.12/dist/vue.js"></script>
    
    <script src="https://cdn.jsdelivr.net/npm/@authing/vue-ui-components/lib/index.min.js"></script>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@authing/vue-ui-components/lib/index.min.css"></link>
  </head>

  <body>
    <div id="app"></div>
    <!-- built files will be auto injected -->

    <script>
      // 这可以替换你的 AppId
      const appId = '5d70d0e991fdd597019df70d'

      const config = {
        logo: 'https://usercontents.authing.cn/client/logo@2.png',
        title: 'Authing',
      }

      const app = new Vue({
        el: '#app',
        render: (h) => h(AuthingVueUIComponents.Guard, {
          props: {
            config,
            appId,
          },
        }),
      })

      window.app = app

    </script>
  </body>
</html>
```

### 完整体验

这是一个最简单的 Guard 组件的在线 [codepen](https://codepen.io/) 演示。可以将 `AppId` 修改为你自己的 ID 直接在这里展示。

<iframe height="760" style="width: 100%;" scrolling="no" title="Vue 2 Guard Demo" src="https://codepen.io/xuancaosu/embed/NWXxZYx?default-tab=html%2Cresult&editable=true&theme-id=light" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href="https://codepen.io/xuancaosu/pen/NWXxZYx">
  Vue 2 Guard Demo</a> by Lucsun (<a href="https://codepen.io/xuancaosu">@xuancaosu</a>)
  on <a href="https://codepen.io">CodePen</a>.
</iframe>

### 监听登录事件

`Guard` 组件可以使用 `@login` 事件回调函数，当用户成功登录时回调用此函数，你可以在此获取当前用户的用户信息。[查看完整事件列表](#完整参数)。

```vue
<template>
  <Guard :appId="appId" @login="onLogin" />
</template>

<script>
import { Guard } from "@authing/vue-ui-components";
import "@authing/vue-ui-components/lib/index.min.css";

export default {
  components: {
    Guard,
  },
  data() {
    return {
      appId: "AUTHING_APP_ID",
    };
  },
  methods: {
    onLogin(userInfo) {
      console.log(userInfo);
    },
  },
};
</script>
```

在此我们只是简单地把获取到的用户信息 `console.log` 了出来：

用户信息中的 token 字段为该用户的身份凭证，后续访问你后端资源的时候应该带上，然后在后端验证此 token 的身份。
