**Webpack**

## 安装 Webpack

命令行内输入

```
npm install webpack webpack-cli --global
```

表示全局安装`webpack`与`webpack-cli`两个包

### 局部安装 Webpack

1. 首先,命令行内输入 `npm init -y` 创建一个 npm 包管理文件
2. 命令行内输入 `npm install webpack webpack-cli --save-dev` 来局部安装

## 查看当前打包信息

查看打包信息命令:

```
webpack --stats detailed
```

该命令使用的是全局的 webpack,那如果想使用目录下的 webpack 呢
卸载全局 webpack

```
npm uninstall -g webpack

npm uninstall webpack webpack-cli --save-dev
```

使用局部`webpack`

```
npx webpack
```

## webpack 打包文件

直接打包:
文件目录下直接输入 webpack

为打包指定入口文件以及生产环境

```
npx webpack --entry ./src/index.js --mode production
```

## webpack 配置文件

在`package.json`同级目录下,创建文件`webpack.config.js`

```
const path = require("path");
module.exports = {
  // 配置入口文件
  entry: "./02-setup-app/src/index.js",
  // 配置打包文件名字以及打包路径
  output: {
    filename: "dabao.js",
    path: path.resolve(__dirname, "./dist"),
    // 是否每次打包都清理dist文件夹
    clear:true

  },
  // 改为生产环境
  mode: "development",
  // 方便定位错误所在位置
  devtool:'inline-source-map',
};

```

## webpack 插件

首先命令行内安装插件`html-webpack-plugin`,作用是在 html 文件内自动引入打包后的文件

```
npm install html-webpack-plugin
```

在`webpack.config.js`配置文件内,添加插件配置

添加插件配置有两步 1.引入插件常量 2.实体化插件&配置插件内容

```
const path = require("path");

// 引入插件常量
const HtmlWebpackPlugin = require("html-webpack-plugin");

module.exports = {
  // 配置入口文件
  entry: "./src/index.js",
  // 配置打包文件名字以及打包路径
  output: {
    filename: "dabao.js",
    path: path.resolve(__dirname, "./dist"),
  },
  mode: "none",
  // 插件配置
  plugins: [
    // 实体化插件
    new HtmlWebpackPlugin({
      // 指定模板文件
      template: "./index.html",
      // 指定打包后的文件名
      filename: "ok.html",
      // 指定生成后的引用在哪个标签内
      inject: "body",
    }),
  ],
};

```

## webpack 的自动编译

在每次更改 js 代码后,都需要手动的进行`npx webpack`来进行编译 js 文件
使用`watch`参数,可以使每次代码更改保存后,自动进行编译

```
npx webpack --watch
```

## webpack 的浏览器自动刷新

插件:`webpack-dev-server`

安装插件

```
npm install webpack-dev-server -D
```

打开`webpack.config.js`,添加配置项 `devServer`,与`plugins`配置项同级

```
const path = require("path");

// 引入插件常量
const HtmlWebpackPlugin = require("html-webpack-plugin");

module.exports = {
  // 配置入口文件
  entry: "./src/index.js",
  // 配置打包文件名字以及打包路径
  output: {
    filename: "dabao.js",
    path: path.resolve(__dirname, "./dist"),
  },
  mode: "none",
  // 插件配置
  plugins: [
    // 实体化插件
    new HtmlWebpackPlugin({
      // 指定模板文件
      template: "./index.html",
      // 指定打包后的文件名
      filename: "ok.html",
      // 指定生成后的引用在哪个标签内
      inject: "body",
    }),
  ],
    devServer: {
      // 设定服务器根目录
    static: "./dist",
  },
};
```

### 启动插件服务

```
npx webpack-dev-server --open
```

## webpack 引入外部资源 图片 视频 音频 字体库等

### 第一个资源类型 `asset/resource`

在`webpack.config.js`文件内,添加配置项`module`,与`devServer`等同级

引入外部的`png`文件,设置其资源类型为`asset/resource`

```
  module: {
    rules: [
      {
        test: /\.png$/,
        type: "asset/resource",
      },
    ],
  },
```

然后在 js 文件内引入

```
import hello from "../src/hello.js";
import imgsrc from "../access/img/123.png";

hello();

const img = document.createElement("img");
img.src = imgsrc;
document.body.appendChild(img);
```

使用 DOM 结构将其插入到页面当中,即可使用

import 将其引入进来之后,实际上是一个链接,资源的链接地址

### 资源类型 `type:asset`

Webpack 的资源类型
`asset/inline`: 将资源处理成内联的 data URL。可以用于减少对网络请求的依赖，但会增加 HTML 文件的大小。
`asset/eval`: 将资源以 BASE64 编码的形式处理成内联的 data URL，并用 eval 包裹代码。可用于 SVG 文件
`asset/source`: 将资源导出为一个字符串，可以在代码中使用,可用于 txt 文件,将其内容传唤为字符串
`asset/asset`: 将文件与 output 相同的输出位置导出到磁盘，并返回一个 URL。默认使用该导出方式。
`asset/resource`:作为处理图片、字体、音频等文件,会生成一个单独的文件,并导出为 url 使用

如果直接将其设置为`type:asset`,则如果其超过 8KB,则会使用`asset/inline`形式进行引用
如果没有超出,则使用`asset/resource`,

如果需要更改 8KB 这个上限,则可以在`module`配置项中

### 打包外部资源文件时,如何自定义名字以及其路径

有两种办法

在配置项`output`内,新增一个配置`assetModuleFilename`,可以定义其打包的路径与文件名
`assetModuleFilename: "images/[contenthash][ext]"`代表其在 images 文件夹下,使用了哈希值作为文件名,文件名原扩展作为扩展名

```
  // 配置打包文件名字以及打包路径
  output: {
    filename: "dabao.js",
    path: path.resolve(__dirname, "./dist/"),
    assetModuleFilename: "images/[contenthash][ext]",
  },
```

在配置项`module`内,也就是引入外部资源的配置项内,添加`generator`属性,其配置内容与`output`相同,但是区别在于,如果两者配置项同事存在,则`module`的配置优先级较高

```
  module: {
    rules: [
      {
        test: /\.png$/,
        type: "asset/resource",
        generator: {
          filename: "img666/[contenthash][ext]",
        },
      },
    ],
  },
```

## webpack 引入 Css sass less stylus 文件

### 引入 CSS

首先引入 CSS 需要两个依赖包:`style-loader`与`css-loader`
安装指令

```
npm install style-loader
npm install css-loader
```

`webpack.config.js`文件配置引入 css 规则
`use`规则内的`['style-loader','css-loader']`,两者顺序不能更改

```
  module: {
    rules: [
      {
        test: /\.css$/,
        use:['style-loader','css-loader']
      }
    ],
  },
```

`import "../access/css/red.css";`

最后在 js 文件内将 css 文件导入即可使用

### 引入 less

引入 less 文件的步骤与 css 大体相同,也是需要安装两个依赖包`less-loader`与`less`

安装指令, -D 参数表示将其安装至开发环境中

```
npm install less-loader less -D
```

然后在`webpack.config.js`文件中,引入依赖包

```
  module: {
    rules: [
      {
        test: /\.css|less$/,
        use:['style-loader','css-loader','less-loader']
      }
    ],
  },
```

`use`的顺序也是不可更改,其顺序为倒序使用,先 less 编译文件,再由 class 加载,最后由 style 加载至页面

最后将其引入即可

```
import "../access/css/blue.less";
```

## webpack 将 css 独立至一个单独的文件内,并可以使用 link 标签进行引入

插件: `mini-css-extract-plugin`
`mini-css-extract-plugin`是一个可以将 CSS 文件独立打包的 Webpack 插件。该插件的主要作用是将 Webpack 打包后的 CSS 样式文件抽取出来,但是只支持 Webpack5 环境

安装插件

```
npm install mini-css-extract-plugin -D
```

引入 mini-css-extract-plugin 插件

```
const miniCss = require("mini-css-extract-plugin");
```

实例化插件

```
  plugins: [
    // 实例化 mini-css-extract-plugin
    new miniCss(),
  ],
```

使用插件

```
      {
        test: /\.css|less$/,
        // use: ["style-loader", "css-loader", "less-loader"],
        use: [miniCss.loader, "css-loader", "less-loader"],
      },
```

重新使用`npx webpack`编译后,发现 dist 文件夹下多了一个`main.css`文件,其中包含了所使用到的 css 文件
并且打包后的 html 文件内,也变成了 link 引入的 css 文件

如果需要自定义打包后的 css 文件名以及路径,则在实例化插件时添加配置:`filename`即可

实例化插件并自定义

```
  plugins: [
    // 实例化 mini-css-extract-plugin
    new miniCss({
      filename: "./dist/mainCss.css",
    }),
  ],
```

## webpack 压缩打包后的 CSS 代码

插件:`css-minimizer-webpack-plugin`

安装插件

```
npm install css-minimizer-webpack-plugin -D
```

引入插件

```
const CssMinimizerPlugin = require("css-minimizer-webpack-plugin");
```

实例化插件

`webpack.config.js`中添加插件配置项,与`rules`同级,也就是在`module`的下一级

```
  optimization: {
    minimizer: [
      new CssMinimizerPlugin(),
    ],
  },
```

再次`npx webpack`后,可以看到 打包后的 CSS 文件被压缩了

## webpack 加载字体文件

在`webpack.config.js`中,`rules`配置项下,添加字体文件配置

```
      {
        test: /\.(woff|woff2|eot|ttf|otf)$/i,
        type: 'asset/resource',
      },
```

然后在 CSS 中,引入字体文件即可

```
@font-face {
    font-family: "Regular";
    font-weight: 400;
    src: url("../font/KlzqZIs2907R.woff") format("woff2");
    font-display: swap;
}

.fonta {
    font-family: "Regular";
    font-size: 200px;
}
```

## webpack 引入 toml yaml json5 文件资源

安装依赖包

```
npm install toml yaml json5 -D
```

在`webpack.config.js`当中,引入安装好的三个包

```
const toml = require("toml");
const yaml = require("yaml");
const json5 = require("json5");
```

然后在`module`的`rules`配置项中,添加配置

```
      // 引入toml
      {
        test: /\.toml$/,
        type: "json",
        parser: {
          parse: toml.parse,
        },
      },
      // 引入yaml
      {
        test: /\.yaml$/,
        type: "json",
        parser: {
          parse: yaml.parse,
        },
      },

      // 引入json5
      {
        test: /\.json5$/,
        type: "json",
        parser: {
          parse: json5.parse,
        },
      },
```

在 JS 中引入并使用

```
import toml from "../access/to.toml";
import yaml from "../access/ya.yaml";
import json5 from "../access/json5.json5";

.....

// 输出yaml,toml,json5
console.log(yaml);
console.log(toml);
console.log(json5);
```

## webpack 加载多个入口文件

有时候,一个单一的入口文件不足够需求,这时候需要多个入口文件

```
module.exports = {
  // 配置入口文件
  entry: {

  }
  }
```
