## 安装`vue3`

- `npm create vite@latest`
- 然后按照提示操作即可！



## `css`路径映射

```ts
// vite.config.ts
import { fileURLToPath, URL } from 'node:url'

import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
import vueJsx from '@vitejs/plugin-vue-jsx'

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [
    vue(),
    vueJsx(),
  ],
  resolve: {
     // 路径映射
    alias: {
      '@': fileURLToPath(new URL('./src', import.meta.url))
    }
  }
})

```

## 环境变量

- `import.meta.env` 内置代码
- `MODE`现在处于什么模式
- `BASE_URL` 当前域名的`url`
- `PROD` 生产环境
- `DEV` 测试环境
- `SSR` 是否服务端渲染
- 通过创建`.env`文件，可以自定义值(自定义值要加上VITE前缀，例如`VITE_TITLE=hello`)





## 预编译

```js
// vite.config.js
import { fileURLToPath, URL } from 'node:url'

// https://vitejs.dev/config/
export default defineConfig({
  optimizeDeps:{
    include:['xxx'],   // 需要预编译的文件
    exclude:['xxxx']  //不需要预编译的文件
  },
})

```

