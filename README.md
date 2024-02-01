# Vue 3 + TypeScript + Vite

This template should help get you started developing with Vue 3 and TypeScript in Vite. The template uses Vue 3 `<script setup>` SFCs, check out the [script setup docs](https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup) to learn more.

## Recommended IDE Setup

- [VS Code](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (and disable Vetur) + [TypeScript Vue Plugin (Volar)](https://marketplace.visualstudio.com/items?itemName=Vue.vscode-typescript-vue-plugin).

## Type Support For `.vue` Imports in TS

TypeScript cannot handle type information for `.vue` imports by default, so we replace the `tsc` CLI with `vue-tsc` for type checking. In editors, we need [TypeScript Vue Plugin (Volar)](https://marketplace.visualstudio.com/items?itemName=Vue.vscode-typescript-vue-plugin) to make the TypeScript language service aware of `.vue` types.

If the standalone TypeScript plugin doesn't feel fast enough to you, Volar has also implemented a [Take Over Mode](https://github.com/johnsoncodehk/volar/discussions/471#discussioncomment-1361669) that is more performant. You can enable it by the following steps:

1. Disable the built-in TypeScript Extension
   1. Run `Extensions: Show Built-in Extensions` from VSCode's command palette
   2. Find `TypeScript and JavaScript Language Features`, right click and select `Disable (Workspace)`
2. Reload the VSCode window by running `Developer: Reload Window` from the command palette.

## mswjs 安装

### 安装依赖

npm install msw --save-dev

设置 woker 目录
public 和 package.json

```shell
npx msw init ./public --save
```

这行命令会在 public 目录下生成一个 mockServiceWorker.js 文件来提供 worker 服务来进行接口 mock。
`--save`会在 package.json 中添加一个配置

```json
{
  "name": "vite-vue3-ts-template",
  "msw": {
    "workerDirectory": "public"
  }
}
```

## 拷贝 example 中的 mocks 文件夹到工程`src`目录中

`https://github.com/mswjs/examples/tree/main/examples/with-vue/src/mocks`

改造 main.ts

```js
async function prepareApp() {
  if (process.env.NODE_ENV === 'development' || process.env.NODE_ENV === 'test') {
    const { worker } = await import('./mocks/browser');
    return worker.start();
  }

  return Promise.resolve();
}

const app = createApp(App);

prepareApp().then(() => {
  app.mount('#app');
});
```

此时启用项目，浏览器控制台已经可以看到 mswjs 启动完成，并给出了警告信息，所有没有被成功拦截都会使用 warn 输出，所有成功拦截的都使用黑体文字输出。

### 常用场景

解析 RESTFul 规范的请求

<https://mswjs.io/docs/network-behavior/rest>

解析 graphql 规范的请求

<hhttps://mswjs.io/docs/network-behavior/graphql>

高阶解释器

<https://mswjs.io/docs/recipes/higher-order-resolver>

延迟返回

<hhttps://mswjs.io/docs/api/delay>

处理 cookies

<hhttps://mswjs.io/docs/recipes/cookies>

从 url 中获取参数

<hhttps://mswjs.io/docs/recipes/query-parameters>

对请求进行代理，修改响应参数

<hhttps://mswjs.io/docs/recipes/response-patching>

透传

<https://mswjs.io/docs/api/passthrough>

模拟流数据

<hhttps://mswjs.io/docs/recipes/streaming>

模拟请求异常情况

<hhttps://mswjs.io/docs/recipes/network-errors>

模拟文件上传

<hhttps://mswjs.io/docs/recipes/file-uploads>

模拟二进制

<hhttps://mswjs.io/docs/recipes/responding-with-binary>

启用 HTTPS

<hhttps://mswjs.io/docs/recipes/using-local-https>
