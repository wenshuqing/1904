##### node

- 使用工具包的三种方式：
1. cdn 引入网上文件
2. 下载到本地在引入使用
3. 将项目变成 node 项目，在使用 npm 下载 包 引入

- Node.js 是一个基于 Chrome V8 引擎的 JavaScript 运行时。有 Node.js 的地方就能运行 js,并不一定必须要再在浏览器上运行。
- 安装
直接百度 node 进入中文网直接下载安装包，直接进行安装不需要做任何的选择，一直下一步即可。
任意位置打开命令行工具，输入 `node -v` 和 `npm -v` 查看 node 和 npm 的版本号，如果有就安装好了,如果命令出错尝试重启电脑再次执行。

npm 是什么
安装好 node 之后 npm 就附带安装好了。他是 node package manager,node 包管理工具。node 包借助 npm 下载

node 模块(后台，前端)

前端模块包括前端所有的 js 相关的包。

模块概念：把一些 js文件通过语法弄成模块，供其他 js 导入使用

node 模块使用

- 新建文件夹，将该文件夹初始化为 node(npm) 的项目执行 `npm init -y`
- 新建 index.html 页面
- 安装 jquery 插件。执行 `npm install jquery`
  - 安装完毕之后，项目内多了点东西
    - node_modules 文件夹，该文件夹是存储下载的包的地方
    - package-lock.json 文件，该文件是记录安装的包的详细信息的，不需要理会
- 在 html 中使用 jquery 可以按照之前的路径导入(不推荐)。但是现在是使用 npm 下载模块。可以使用 node 模块的方式导入安装好的包。 使用 `require(包名)`
- 但是当做模块导入之后浏览器报错。因为模块语法浏览器不支持需要编译。

npm 的使用
npm 就是下载 node 包的工具。

下载方式有三种

- `npm i 包名 --save`，这种方式一般下载的是项目的必须依赖,记录到 package.json 内的 dependencies 字段内。
  ```
    npm install jquery@2.3.4 --save
    npm i jquery -S
    npm i jquery
  ```
- `npm i 包名 包名 --save-dev`,这种方式安装的是项目的非必须依赖(工具类),记录到 package.json 内的 devDependencies 字段内
  ```
    npm install webpack webpack-cli --save-dev
    npm i webpack -D
  ```
- `npm i -g 包名`,这种方式是全局安装，当你想要在你的电脑上任何地方都使用包的时候进行全局安装。
  ```
    npm i -g server
  ```

卸载包使用 `npm uninstall 包`通过哪种方式安装的就通过哪种方式卸载。

npm 下载包的好处

- 可以使用模块导入
- 下载的包的信息全部记录在 package.json 内
- 同事之间相互传递项目的时候不需要传递 node_modules(此文件夹放的都是下载的所有的包，不管是必须的还是非必须的) 文件夹。使用的时候只需要执行 `npm i` 命令会重新将所有的包下载一遍。

npm 的技巧，直接在任意位置的命令行执行即可

- 切换 npm 包的来源，默认的来源是外网服务器有点慢,为了下快点，可以切换一下 taobao 镜像
  ```
    npm config set registry https://registry.npm.taobao.org
  ```
- 加上 http 显示配置，不让等待过程先得无聊。

  ```
    npm config set loglevel=http
  ```
