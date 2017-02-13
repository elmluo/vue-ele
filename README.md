<!-- 安装vue官方脚手架 -->
## vue-cli 脚手架安装

``` shell
npm install vue-cli
// options
vue
vue-list
vue init webpack#1.0 vue-ele

cd vue-app
npm install 
// webstom 开启项目会检索文件node_modules文件很多，需要屏蔽 file->setting->directories->选择node_modules
 或者 删除node_modules，在项目当中创建一个空的node_modules文件夹—>右击->Mark Directory as->excluded-npm install,这样也可以忽略node_modules文件
```
## 项目目录文件介绍

- build和config是webpack的相关配置文件
- src 项目代码文件
- static 项目依赖的第三方文件
- babelrc babel编译es6到es5的配置
  - presets 预设 表示babel需要提前安装的插件
    - stage-2
  - plugins 除了预设插件以外的其他插件
    - transform-runtime 把一些es6的插件做转换
    - comments 表示代码转换后不生成注释
- .editorconfig
  - charset = utf-8
  - indent_style = space 以空格方式做缩进
  - indent_size = 2 缩进大小vue风格两个
  - end_of_line = lf linux和mac换行符风格
  - insert_final_newline = true 自动换行文件 在末尾插入一个新行
  - trim_trailing_whitespace = true
- .eslintrc.js
  - eslint语法对于符号，空格规范到变态，建议webstom写完ES6代码后，ctrl+alt+l 格式化一下代码
- .eslintignore 表示对里面的配置文件不会做语法检查
  - build/*.js 忽略对build文件下的所有文件做语法检查
  - config/*.js 忽略对config文件下面的所有文件做语法检查
  - .eslintrc.js eslint配置项
    - extends:'standard' 在项目初始化的时候让它继承标准的规则
    - 'rule' 具体定义的es6规则 不想要的规则配置成0即可
- .gitignore git push时候忽略掉的文件
- package.json 项目生产和开发环境需要的一些配置文件和命令配置
  - "script" 表示执行的命令，例如运行npm run XXX 对应执行的代码
  - "dependencies" 生产环境下需要的依赖
  - "devDependencies" 编译环境下需要的依赖

## 准备项目

### 目录（脚手架生成）
### 需求分析 
### 项目resource 
### 图标fonts
### mockData和配置api`require(../data.json)/express.Router()` 

  ```javascript
  // bulid/dev-server.js
  var apiRoutes = express.Router();
  app.use('/api',apiRoutes);
  apiRoutes.get('/seller',function (req,res) {
    res.json({
      errno: 0,
      data: seller
    });
  });
  ```
## 页面布局框架搭建

### 组件拆分 `header/tab/content/ footer`

  ```javascript
  // 指令标签和HTML标签重命报错，所以注册组件的时候，需要自定义命名
  export default {
    components: {
      'v-header': header
    }
  }
  ```
  - header: retina 1px像素border实现
  - tab：flex自适应布局 
    - 切换Vue-router（npm install vue-router@0.7.13）`v-link="{path:'/goods'}"`
  - content: router-view外联`<router-view></router-view>`
  

# ele-app
> sell


## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# run unit tests
npm run unit

# run e2e tests
npm run e2e

# run all tests
npm test
```

For detailed explanation on how things work, checkout the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).
