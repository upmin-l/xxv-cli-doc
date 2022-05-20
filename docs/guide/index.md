## 介绍

> xxv-cli 是一个基于 [Vue3.0](https://v3.cn.vuejs.org/) 生态进行快速开发的完整系统，提供一套基于 Vue3、[thingJs](http://www.thingjs.com/guide/) 的完整 Web 项目解决方案，让开发者更加专注于业务逻辑的开发

使用 xxv-cli 主要有两种方式：

1. 去 gitlab 上面克隆 [xxv-cli](https://git.uino.com/lanshikeng/xxv-cli) 并本地 `npm link`。
2. 使用 [npm](#npm) 安装它。

### 版本核心包

最新版本：![npm](https://img.shields.io/badge/xxv--cli-1.0.0--Alpha.1-brightgreen)

<p align="left">
  <a href="https://www.npmjs.com/package/commander/v/6.2.0"><img src="https://img.shields.io/badge/commander-6.2.0-brightgreen" alt="Version"></a>
  <a href="https://nodejs.org/en/about/releases/"><img src="https://img.shields.io/badge/node-%3E%3D12.0.0-green" alt="Node Compatibility"></a>
  <a href="https://nodejs.org/en/about/releases/"><img src="https://img.shields.io/badge/npm-%3E%3D6.0.0-red" alt="Node Compatibility"></a>
  <a href="https://www.npmjs.com"><img src="https://img.shields.io/badge/license-MIT-blue" alt="License"></a>
 </p>


### npm 

::: warning 提示
目前暂时没有发包到 npm
:::

```javascript
npm install -g xxv-cli
# OR
yarn global add xxv-cli
```

## 基础

### 创建一个项目


```bash
xxv create hello-world
```

你会被提示选取一个 preset。你可以选默认的包含了基本的 [园区项目](#介绍) 和 [uearth项目](#介绍) 设置的 preset，

![CLI 预览](/cli-new-project.png)

也可以选“手动选择特性”来选取需要的特性。

![CLI 手动预览](/cli-manual-project.png)

如果你决定手动选择特性，在操作提示的最后你可以选择将已选项保存为一个将来可复用的 preset。

::: tip ~/.xxvrc
被保存的 preset 将会存在用户的 home 目录下一个名为 .xxvrc 的 JSON 文件里。如果你想要修改被保存的 preset / 选项，可以编辑这个文件。
:::

## 开发

### 目录结构

```markdown
├── bin                         # node 执行文件
│   ├── index.js                # xxv 命令执行文件
├── package
│   ├── cli-cli                 # create 命令执行
│        ├── index.js
│   ├── cli-pinia               # pinia 模块
│        ├── src                # 存放非TypeScript支持下的pinia模板文件
│        ├── src-ts             # 存放TypeScript支持下的pinia模板文件
│        ├── index.js
│   ├── cli-spray               # spray 模块
│        ├── src                # 存放非TypeScript支持下的spray模板文件
│        ├── src-ts             # 存放TypeScript支持下的spray模板文件
│        ├── index.js
│   ├── cli-vue-router          # router 模块
│        ├── src                # 存放非TypeScript支持下的router模板文件
│        ├── src-ts             # 存放TypeScript支持下的router模板文件
│        ├── index.js
│   ├── cli-vuex                # vuex 模块
│        ├── src                # 存放非TypeScript支持下的vuex模板文件
│        ├── src-ts             # 存放TypeScript支持下的vuex模板文件
│        ├── index.js
│   ├── cli-jest                # jest 模块
│        ├── common             # 存放jest通用的模板文件（不管是否支持TypeScript）
│        ├── src                # 存放非TypeScript支持下的jest模板文件
│        ├── src-ts             # 存放TypeScript支持下的jest模板文件
│        ├── index.js
│   ├── cli-typescript          # typescript 模块
│        ├── src                # 存放TypeScript支持下的模板文件
│        ├── index.js
│   ├── pluginModules           # 手动预选依赖模块 apply
│   ├── plugMode                # 静态文件 template
│        ├── common             # 存放需要ejs转换的通用模板文件（不管是否选择了TypeScript支持）
│        ├── public             # 输出为项目根目录下的public文件夹内容，里面的文件内容是不需要ejs转换的模板文件
│        ├── mapThemes          # 地图主题包
│        ├── vendor             # thingJs 等静态资源，输出到项目的目录为：/public/vendor
│        ├── template           # 存放非TypeScript支持下的默认模板文件
│        ├── template-ts        # 存放TypeScript支持下的默认模板文件
│   ├── util                    # 工具方法模块
│        ├── executeCommand     # 子进程执行下载依赖
│        ├── generateReadme     # create 项目 README.md 文件内容生成逻辑
│        ├── getRelyVersions    # 依赖包 版本获取
│        ├── injectImports      # 出来依赖导入语句逻辑
│        ├── PackageManager     # 包管理逻辑
│        ├── packageModules     # 手动预选依赖注入
│        ├── rcPath             # 负责处理路径模块
│        ├── sortObject         # 包顺序
│        ├── writeFileTree      # 负责文件写入
│   ├── create                  # xxv 项目创建create 命令入口
│   ├── Creator                 # 命令交互逻辑，依赖入口收集逻辑
│   ├── GeneratorAPI            # 各种模板生成 核心逻辑
│   ├── options                 # 本地存储预设逻辑及默认渲染初始定义
│   ├── ResolveMultistage       # 处理问答工厂函数
│   ├── SetupTemplate           # 执行依赖各个插件内部逻辑，语句的导入及最终模板的生成
│   ├── utils                   # 公共方法
```

### 扩展方法

::: tip  提示
xxv-cli 手动依赖采用观察者设计模式，无需理解整个cli 逻辑也能扩展内置依赖

在 `src/package` 文件夹下 创建以 `cli-` 开头的文件夹 
:::

![CLI](/extend.png)