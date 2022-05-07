# Token 校验以及获取用户信息

## Token 缓存

使用 `Guard` 登陆成功后会返回对应的用户信息，其中的 `token` 字段为标准的 `OIDC IdToken`，你可以在后端使用应用的 ID 和 Secret 验证此 `token`。

你的用户登录成功后，需要将 `token` 信息手动缓存，以方便次用户二次会话时使用。下方代码以 `React` 为例

```JS
const App = () => {
  return (
    <>
      <Guard
        appId="AUTHING_APP_ID"
        onLogin={(user) => {
          console.log(user)
          if (user.token) {
            // 放到 localStorage 中
            localStorage.setItem('user_id_token', user.token)
          }
        }}
      />
    </>
  )
}
```

上方的例子是将 `token` 放到了 `localStorage` 中，在实际使用时，可以更加灵活，可以采用其他的方式进行缓存。

> `Guard` 组件在 `3.0.0` 后，不在主动将 `token` 缓存到 `localStorage`。这样做的原因是可以提供更高的灵活性，不再依赖 `Guard` 进行 `token` 的校验。

## 检测 Token 登录状态

用户登录成功后，在二次会话的时候，我们之前已经将 `token` 进行了缓存。我们首先需要对这个 `token` 进行登录状态校验，校验成功后在进行用户详细信息的获取。下方代码以 `React` 为例。

检测 Token 登录状态，可以使用 `authing-js-sdk`，提供的内置方法，这个是相关的文档 [checkLoginStatus](/reference/sdk-for-node/authentication/AuthenticationClient.md#检测-token-登录状态)。

> what？你不知道如何使用 `authing-js-sdk`，那你可以参一下文档 [Guard 中使用 AuthenticationClient](/reference/guard/use-js-sdk.md)

```JS
const App = () => {
  const [client, setClient] = useState<AuthenticationClient>()
  const [user, setUser] = useState<User>()

  return (
    <>
      <Guard
        appId="AUTHING_APP_ID"
        onLogin={(user, client) => {
          setUser(user)
          setClient(client)
        }}
        config={{
          mode: GuardMode.Modal,
        }}
      />

      <Button
        onClick={() => {
          if (!user || !client) return

          const token = user.token
          client.checkLoginStatus(token as string).then((c) => console.log(c))
        }}
      >
        校验 Token
      </Button>
    </>
  )
}
```

`checkLoginStatus` 成功返回的信息如下：

```JS
{
    "code": 200,
    "message": "已登录",
    "status": true,
    "exp": 1653107498,
    "iat": 1651897898,
    "data": {
        "id": "6275f6233b799c1b072947f3",
        "userPoolId": "6248526da636844b244e5de9",
        "arn": null
    }
}
```

## 获取用户信息

获取用户的信息最优的方案是，通过校验 `token` 返回的 `data` 中的 `id`、`userPoolId` 在后端进行校验，而不是在前端进行用户信息的获取。

如果必须在前端进行用户信息获取的话，可以通过 `token` 进行信息的获取。使用 `authing-js-sdk` 中的 `getCurrentUser` 可以完成，这个是相关的文档 [getCurrentUser](/reference/sdk-for-node/authentication/AuthenticationClient.md#获取当前登录的用户信息)。这样使用的话需要使用 `token` 初始化 `AuthenticationClient`。

> what？你不知道如何使用 `authing-js-sdk`，那你可以参一下文档 [Guard 中使用 AuthenticationClient](/reference/guard/use-js-sdk.md)

```JS
const authClient = new AuthenticationClient({
    appId: 'AUTHING_APP_ID',
    token: 'USER_TOKEN',
})

authClient.getCurrentUser().then((user) => {
    console.log('current user')
    console.log(user)
})
```
