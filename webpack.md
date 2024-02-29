# 如何使用`webpack`

## 下载`webpack`

```shell
npm init -y  初始化文件

npm install webpack webpack-cli --save-dev
```

## 基础配置`webpack` 打包构建

- 打开文件`package.json`

- ```json
  "scripts": {
    "build": "webpack"
   },
  ```

- 新建`webpack.config.js`进行配置

- ```json
  const path = require('path')
  module.exports={
    mode:'development',
    // 入口文件
    entry:"./src/main.js",
    // 打包后文件
    output:{
      filename: 'bundle.js',
      path:path.join(__dirname,'dist')
    }
  }
  ```

  

## `webpack`的工作模式

- `production` 模式
- 启动内置优化插件。自动优化打包结果，打包速度偏慢
- `development` 模式
- 自动优化打包速度，添加一些调试过程的辅助插件
- `none` 模式
- 原始打包，不做任何处理

# 如何通过`loader`实现特殊资源加载

- 下载对应的`xxx-loader`（以`css`为例）

- `npm install css-loader --save-dev`

- ``npm install style-loader --save-dev`

- `webpack.config.js`文件中添加对应的配置属性

- ```js
  module.exports={
    module:{
      rules:[
        {
          test:/\.css$/, // 匹配所有.css
          use:[
            'style-loader',
          	'css-loader'
          ]
        }
      ]
    }
  }
  ```

  

# `webpack`运行机制与核心工作原理

## 流程

- `webpack CLI` 启动打包流程
- 载入`webpack`核心模块，创建`Compiler`对象
- 使用`compiler`对象开始编译整个项目
- 从入口文件开始，解析模块依赖，形成依赖关系树
- 递归依赖树，讲每个模块交给对应的`loader`处理
- 合并`loader`处理完结果，将打包输出`dist`目录

## make阶段

- `singleEntryplugin`中调用了`compilation` 对象的`addEntry`方法，开始解析入口
- `addEntry`方法调用了`_addModuleChain`方法，将入口模块添加到模版依赖列表中
- 紧接着通过`compilation`对象的`buildModule`方法进行模块构建
- `buildModule`方法中执行具体的`Loader`，处理特殊资源的加载
- build完成后，通过`acorn`库生产模块代码的`AST`语法树
- 根据语法树分析这个模块是否有依赖关系，如果有则继续循环`build`每个依赖
- 所有依赖解析完成，`build`阶段结束
- 合并生成需要输出的`bundle.js`，写入`dist`目录



# 模块支持热更新

## 开启`HMR`

```js
// webpack.config.js
const path = require('path')
const webpack = require('webpack')
module.exports={
  
  module:{
    devSever:{
      // 开启hmr特性，如果资源不支持hmr会fallback到 live reloading
      hot:true,
      // 只使用hmr，不会fallback live reloading
      // hotOnly: true
    },
    
    plugins:[
      //hmr 特性需要的插件
      new webpack.HotModuleReplacementPlugin()
    ]
  }
}
```

