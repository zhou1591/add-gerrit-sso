# 用户登出

使用 `Guard` 组件，组件加载完成后回触发的 onLoad 事件与登陆成功触发的 `onLogin` 事件都会返回 `AuthenticationClient`。获取到 `AuthenticationClient` 进行手动单例保存，可以在需要调用退出登录的时候使用。下方代码以 `React` 为例

```JS
import { Guard, SocialConnections } from "@authing/react-ui-components";

function App() {
  let guardAuthClient

  return (
    <div className="App">
      <Guard
        appId="AUTHING_APP_ID"
        onLogin={(userinfo, authClient) => {
          console.log(authClient)
        }}

        onLoad={(authClient) => {
          console.log(authClient)
          guardAuthClient = authClient
        }}
      />

      {guardAuthClient && <button onClick={() => guardAuthClient.logout()}>登出</button>}
    </div>
  );
}
```

## 使用 Token 完成登出操作

用户登录成功后，在二次会话时，我们需要在用户登录成功时将 `token` 进行缓存，具体的方法可以参考文档 [校验以及获取用户信息](/reference/guard/save-token.md#token-缓存)。我们使用 `authing-js-sdk` 中的 `logout` 方法，logout [方法的相关文档]((/reference/sdk-for-node/authentication/AuthenticationClient.md#退出登录)。这样使用的话需要使用 `token` 初始化 `AuthenticationClient`。

```JS
const authClient = new AuthenticationClient({
    appId: 'AUTHING_APP_ID',
    token: 'USER_TOKEN',
})

authClient.logout()
```
