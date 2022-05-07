---
tags:
  - 组件
  - Guard
  - Guard组件
  - React
  - Vue
  - React
  - Angular
  - 快速开始
  - 安装
---

# Guard 快速开始

<LastUpdated/>

Guard 被认为是灵活性和集成之间的最佳平衡。如果集成需要更深入的自定义级别或一些前后端分离的场景中无法使用[托管模式](/guides/basics/authenticate-first-user/use-embeded-login-component/)，则建议使用组此模式。内嵌登录组件由 Authing 构建和更新，使用行业最佳实践安全性设计，仅需要几行 JavaScript 代码就可以集成到你开发的项目中。它可以直接从 CDN 或 NPM 加载，也可以从源代码构建。Authing 登录组件同时提供 Javascript 原生、React、Vue 和 Angular 的多种集成模式，在你的任何项目中都可以无缝集成并享有高度自定义灵活性。

> 你可以[点此](/concepts/embeded-vs-hosted.md)了解 {{$localeConfig.brandName}} 托管的登录页（Hosted）和内嵌登录组件（Embedded）的区别。

![Guard Demo](../images/Guard_demo.png)

Authing Web 端 Guard 3.0 版本已于 2021.12.31 正式上线，关于本次更新主要涉及嵌入式 Guard 组件的 MFA、登录安全策略、自定义 CSS 以及登录注册协议相关功能的实现，同时对嵌入式和托管式 Guard 登录框的 UI 进行了全面翻新。 关于本次更新的详细内容以及迁移方案请查看：[从 AuthingGuard 迁移](/reference/guard/migration.md)

## 不同的前端框架使用

<StackSelector snippet="example" selectLabel="选择前端框架" :order="['react', 'vue', 'angular', 'native-javascript']"/>

## 了解获取用户信息之后该怎么做？

获取到用户信息之后，你可以得到用户的身份凭证（用户信息的 token 字段），token 字段为标准的 OIDC IdToken，你可以在后端使用应用的 ID 和 Secret 验证此 token。

token 缓存以及获取用户信息的相关操作，可以参考另外一篇文档
