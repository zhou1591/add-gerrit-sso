#### 安装

```bash
$ yarn add @authing/ng-ui-components

# OR

$ npm install @authing/ng-ui-components --save
```

#### 初始化

首先需要在项目的 tsconfig.json 里面的 compilerOptions 添加：

```json
"skipLibCheck": true
```

在 Angular 项目中初始化：

1. `app.module.ts`

```javascript
import { NgModule } from "@angular/core";
import { BrowserModule } from "@angular/platform-browser";

import { AppRoutingModule } from "./app-routing.module";
import { AppComponent } from "./app.component";

import { GuardModule } from "@authing/ng-ui-components";

@NgModule({
  declarations: [AppComponent],
  imports: [BrowserModule, AppRoutingModule, GuardModule],
  providers: [],
  bootstrap: [AppComponent],
})
export class AppModule {}
```

2. `app.component.ts`

```js
import { Component } from "@angular/core";
import { CommonMessage, AuthenticationClient } from "ng-ui-components";
@Component({
  selector: "app-root",
  templateUrl: "./app.component.html",
  styleUrls: ["./app.component.scss"],
})
export class AppComponent {
  appId = "AUTHING_APP_ID";
  onLoad([e]: [AuthenticationClient]) {
    console.log("onLoad", e);
  }
}
```

3. `app.component.html`

```javascript
<guard [appId]="appId" (onLoad)="onLoad($event)"></guard>
```

### 使用 CDN

#### 使用 CDN 引入

```html
<script src="https://cdn.jsdelivr.net/npm/@authing/ng-ui-components"></script>
```

#### 在 Script 代码块中初始化

```html
<div ng-app="">
  <guard [appId]="AUTHING_APP_ID"></guard>
</div>
```

### 监听登录事件

`guard` 组件传入 `onLogin` 事件回调函数，当用户成功登录时回调用此函数，你可以在此获取当前用户的用户信息。[查看完整事件列表](#完整参数)。

```html
<guard [appId]="appId" (onLogin)="onLogin($event)"></guard>
```

```js
import { AuthenticationClient } from "@authing/ng-ui-components";

import { User } from "@authing/native-js-ui-components";

export class AppComponent {
  appId = "AUTHING_APP_ID";
  onLogin([user]: [User, AuthenticationClient]) {
    console.log("userInfo: ", user);
  }
}
```
