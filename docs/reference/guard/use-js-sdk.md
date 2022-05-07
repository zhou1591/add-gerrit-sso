
# Guard 中使用 AuthenticationClient

`AuthenticationClient` 是 `authing-js-sdk` 提供的以终端用户（End User）的身份进行请求，提供了登录、注册、登出、管理用户资料、获取授权资源等所有管理用户身份的方法。

如果使用的是 `npm` 或者 `yarn` 安装的方式，因为 Guard 依赖 `authing-js-sdk`，可以在项目中直接引用 `authing-js-sdk`[![](https://img.shields.io/npm/v/authing-js-sdk.svg?style=flat-square)](https://www.npmjs.com/package/authing-js-sdk)，并使用相应的方法。具体的方法可以参考文档 [Authing JavaScript/Node SDK](/reference/sdk-for-node/AuthenticationClient.md)。

```JS
import { AuthenticationClient } from "authing-js-sdk"

const authClient = new AuthenticationClient({
    appId: "AUTHING_APP_ID"
})

console.log(authClient)
```

你还可以在 `Guard` 组件中的 `onLogin`、`onLoad` 中得到 `AuthenticationClient`，并且在回调中得到的 Client 是已经初始化完成的，可以直接使用。

可以使用回调事件中返回的 `AuthenticationClient` 完成一个退出登录的操作。以 React 的使用方式为例。

> 复杂一些的场景可以将获取到 `AuthenticationClient` 进行手动单例保存，可以在需要调用退出登录的时候使用。

```JS
import { Guard, SocialConnections } from "@authing/react-ui-components";

function App() {
  let guardAuthClient

  const [guardAuthClient, setGuardAuthClient] = useState()

  return (
    <div className="App">
      <Guard
        appId="AUTHING_APP_ID"
        onLogin={(userInfo, authClient) => {
          console.log(authClient)
          setGuardAuthClient(authClient)
        }}

        onLoad={(authClient) => {
          console.log(authClient)
        }}
      />

      {guardAuthClient && <button onClick={() => guardAuthClient.logout()}>退出</button>}
    </div>
  );
}
```

> 会返回 `AuthenticationClient` 的回调事件还有很多，可以参考[完整参数列表](/reference/guard/parameters.md)。
