Paraviewweb(pvw)官方文档setup过程的一些问题
===
缺少启动指令的配置项
---
官方文档关于package.json的配置项如下面代码所示，
```json
{
  [...]
  "scripts": {
    "build": "webpack --mode development",
    "build:debug": "webpack --display-modules",
    "build:release": "webpack --mode production",
    "start": "webpack-dev-server",

    "commit": "git cz",
    "semantic-release": "semantic-release"
  },
}
```
然后在cmd里直接npm start启动项目，但是会报如下错误：
```shell
'webpack-dev-server' is not an internal or external command, nor is it a runnable program
```
原因是在文档中script配置项中启动命令npm start webpack-dev-server中并有说明安装webpack和webpack-dev-server自启动插件，所以找不到script命令

建议在package.json中加入
```json
[...]

 "devDependencies": {
    "webpack": "^4.41.2",
    "webpack-dev-server": "^3.9.0"
  }
```
然后在cmd中直接npm install，系统会自动安装依赖项

pvw的官方包内的配置文件有错
---

完成上述操作后，`npm start`启动项目之后，系统报错信息如下：

```shell
Module build failed (from ./node_modules/_css-loader@3.2.0@css-loader/dist/cjs.js):
ValidationError: Invalid options object. CSS Loader has been initialised using an options object that does not match the API schema.
 - options has an unknown property 'localIdentName'. These properties are valid:
   object { url?, import?, modules?, sourceMap?, importLoaders?, localsConvention?, onlyLocals? }
    at validate (E:\pvw0\node_modules\_schema-utils@2.5.0@schema-utils\dist\validate.js:50:11)
    at Object.loader (E:\pvw0\node_modules\_css-loader@3.2.0@css-loader\dist\index.js:34:28)
 @ ./node_modules/_paraviewweb@3.2.12@paraviewweb/style/ComponentNative/Composite.mcss 1:14-174
 @ ./node_modules/_paraviewweb@3.2.12@paraviewweb/src/Component/Native/Composite/index.js
 @ ./node_modules/_babel-loader@8.0.6@babel-loader/lib??ref--18-0!./src/index.js
 @ ./src/index.js-exposed
```

提示模块构建打包的过程中出错，经过查找原因是因为路径`node_modules\_paraviewweb@3.2.12@paraviewweb\config\webpack.loaders.js` 下的webpackloaderjs文件中的use配置项，
```json
use: [
      { loader: 'style-loader' },
      {
        loader: 'css-loader',
        options: {
          localIdentName: '[name]-[local]_[sha512:hash:base32:5]',
          modules: true,
        },
      },
      {
        loader: 'postcss-loader',
        options: {
          plugins: () => [autoprefixerPlugin],
        },
      },
    ],
```
中的localIdentName在webpackloader新的版本中已经被降级到module配置项下，所以应该将pvw安装包下的config文件夹下的webpack.loader.js改为如下所示的配置：
```json
use: [
      { loader: 'style-loader' },
      {
        loader: 'css-loader',
        options: {
          modules:{
            localIdentName: '[name]-[local]_[sha512:hash:base32:5]',
          },
          modules: true,
        },
      },
      {
        loader: 'postcss-loader',
        options: {
          plugins: () => [autoprefixerPlugin],
        },
      },
    ],
```
这样在打包过程中才不会出错。

html文件挂载DOM为生成
---
在官方例子中，`const container = document.querySelector('.content');`的挂载节点是html的content DOM，而在生成的html中，并没有content节点，所以要在html的body中加入一个新标签来挂载外部js文件
```html
    <div class="content"></div>
```

以上就是对一些问题我的处理方法，如有问题或者其他解决方法可以联系我邮箱：`haywardryan@foxmail.com`