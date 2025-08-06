## 创建vite项目

创建项目

```bash
npm install vite@latest MyWeb
```

随后可选择项目设置，语言等

## 修改端口号和IP启动

原网址：<https://blog.csdn.net/jiangliuhuan123/article/details/131934185>

在package.json中修改

```js
"scripts": {
    "dev": "vite --port 5555",   // 添加--port {端口号}即可修改，例如 --port 5021
    "build": "vite build",
    "lint": "eslint . --ext js,jsx --report-unused-disable-directives --max-warnings 0",
    "preview": "vite preview"
  },
```

## 服务器代理

官网教程：<https://vitejs.dev/config/server-options.html>

其他教程：<https://zxuqian.cn/vite-proxy-config/>

以vitie为例，在vite.config.js中修改

```js
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

// https://vitejs.dev/config/
export default defineConfig({
  // 添加配置项
  server: {
    // 指定侦听的地址，0.0.0.0 或者 true 都是监听所有地址
    host: '0.0.0.0',
    // 添加proxy配置项
    proxy: {
      // 属性名‘/api'为需要代理的URL路径段，值为相关配置
      '/api': {
        target: 'http://172.16.10.46:3001',
        changeOrigin: true,
        rewrite: (path) => path.replace(/^\/api/, ''),
      },
    }
  },
  plugins: [react()],
})

```

其中在 proxy 配置对象中：

*   `target`，为实际的后端 URL，它会追加到属性名配置的 `/api` 这个片段的前面，例如访问 `/api/some_end_point`会转换为 `http://localhost:3001/api/some_end_point`。
*   `changeOrigin`，是否改写 origin，设置为 true 之后，就会把请求 API header 中的 origin，改成跟 `target` 里边的域名一样了。
*   `rewrite` 可以把请求的 URL 进行重写，这里因为假设后端的 API 路径不带 `/api` 段，所以我们使用 `rewrite`去掉 `/api`。给 `rewrite`传递一个函数，函数的参数 `path`是前端请求的 API 路径，后面直接使用了 replace() 方法，在里面写一个正则表达式，把 `/api`开头的这一段替换为空。

## Vite开启本地https服务

教程网页：<https://blog.csdn.net/qq_40868156/article/details/131801416>

运行`npm i vite-plugin-mkcert -D`安装依赖

## Vite使用环境变量

官网教程：<https://cn.vitejs.dev/guide/env-and-mode>

1.自带的环境变量有：

```js
console.log(import.meta.env)
{
	BASE_URL: "/",			// 基本url
	DEV: false,				// 是否在开发环境
	MODE: "production",		// 当前运行的模式	开发模式：development	生产模式：production
	PROD: true,				// 是否在生产环境
	SSR: false				//是否运行在server上
}
```

根据运行命令可进入不同的模式，如： pnpm dev进入的是开发环境， pnpm build是生产模式

2.自定义环境变量

可通过在根目录新建文件达到，创建.env文件是当处于任意一种环境时都可以获取到，.env.development为开发环境时获取，.env.production为生产环境获取

拓展：<https://juejin.cn/post/7094940781726826526>
