# Guard SSO 单点登录

Guard 为开发者提供了简单易用的函数来实现 Web 端的单点登录效果，你可以通过改变传入的参数来进行使用，为你的多个业务软件实现浏览器内的单点登录效果。

## 如何使用
使用 Guard 进行单点登录只需要初始化的时候将 `config` 中的 `isSSO` 为 `true` 即可，下方以 `React` 代码为例：

```JS
const App = () => {
  return (
    <>
      <Guard
        appId="AUTHING_APP_ID"
        onLogin={(user) => {
          console.log(user)
        }}
        config={{
          isSSO: true,
        }}
      />
    </>
  )
}

ReactDOM.render(<App />, document.getElementById('root'))
```

如果 `Guard` 检测可以进行单点登录时，会调用 `onLogin` 方法，返回的值与正常登录相同。

## Authing SSO

使用 `Guard` 完成单点登录只是我们提供的方法之一，我们也提供了其他的方式比如 `Authing SSO`，它可以在项目中更加灵活的使用，具体可以参考文档 [Authing SSO](/reference/sdk-for-sso.md)

::: hint-danger
从 13.1 版本开始，Safari 默认会**阻止第三方 Cookie**，会影响 Authing 的某些**单点登录功能**。其他类似的更新，从 Chrome 83 版本开始，**隐身模式**下默认禁用第三方 Cookie。其他浏览器也在慢慢进行此类更新以保护用户隐私，很多浏览器将禁用第三方 Cookie 作为了一个安全配置功能。

这可能会对此方法产生影响，详情请见 [禁用第三方 Cookie 对 Authing 的影响](/guides/faqs/block-third-party-cookie-impact.md#tracksession)，你可以在此[查看解决方案](/guides/faqs/block-third-party-cookie-impact.md#如何解决)。
:::

