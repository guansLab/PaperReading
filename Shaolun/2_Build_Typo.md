Build_Typo.md(2)
===
>Date:2019/12/1

>Author:Shaolun

>email:haywardryan@foxmail.com

After last release 'Build Typo of PVW', I find some typos once again when i was running the examples on the official [website](https://kitware.github.io/paraviewweb/examples/). Evidence proves that my last suugestion is correct after i ran another demo. But there is another error about a CSS dependency. The error info is as following of **Example_2: ToggleControl**: 
```js
ERROR in ./node_modules/_paraviewweb@3.2.12@paraviewweb/style/ComponentNative/ToggleControl.mcss (./node_modules/_css-loader@3.2.0@css-loader/dist/cjs.js??ref--10-1!./node_modules/_postcss-loader@3.0.0@postcss-loader/src??ref--10-2!./node_modules/_paraviewweb@3.2.12@paraviewweb/style/ComponentNative/ToggleControl.mcss)
Module not found: Error: Can't resolve './font-awesome/css/font-awesome.css' in 'E:\pvw4\node_modules\_paraviewweb@3.2.12@paraviewweb\style\ComponentNative'
 @ ./node_modules/_paraviewweb@3.2.12@paraviewweb/style/ComponentNative/ToggleControl.mcss (./node_modules/_css-loader@3.2.0@css-loader/dist/cjs.js??ref--10-1!./node_modules/_postcss-loader@3.0.0@postcss-loader/src??ref--10-2!./node_modules/_paraviewweb@3.2.12@paraviewweb/style/ComponentNative/ToggleControl.mcss) 3:10-119 11:69-178 11:200-309 11:334-443
 @ ./node_modules/_paraviewweb@3.2.12@paraviewweb/style/ComponentNative/ToggleControl.mcss
 @ ./node_modules/_paraviewweb@3.2.12@paraviewweb/src/Component/Native/ToggleControl/index.js
 @ ./node_modules/_babel-loader@8.0.6@babel-loader/lib??ref--18-0!./src/toggleControls.js
 @ ./src/toggleControls.js-exposed
```
It seems that the webpack cant resolve the mcss file via webpack&webpack-dev-server. This error occurs when i fixed last error of webpack.loader.js. It appears that there is something wrong with the loader. So i turn to webpack.loader.js once again and found that all the style file named XXX.**mcss** will be processed as **css file** and will be processed by **css-loader**. But we fixed the mistake of the question in version of webpack-loader. which means this error is made from other reasons. **Finally, i find something weird when i turn to the `style` file of package `paraviewweb`**. The code in `paraviewweb/style/ComponentNative/ToggleControls.mcss`is written as follows:
```css
.toggleControlButton {
  composes: fa      from 'font-awesome/css/font-awesome.css';
  composes: fa-fw   from 'font-awesome/css/font-awesome.css';
  composes: fa-bars from 'font-awesome/css/font-awesome.css';
  composes: jsControlButton;
  cursor: pointer;
  float: right;
  line-height: 1.5em;
  height: 1.5em;
  padding: 0 5px;
}
```
But the point is **there is no dependency named font-awesome in the dependency library node_modules**. So i turn to package.json and i find the reason:
**the library `font-awesome` is set under devDependencies instead of dependencies**, so as a result this library cannot be installed under file`node_modules`.

So the solution is: installing package `font-awesome` manually and change the file`paraviewweb/style/ComponentNative/ToggleControls.mcss` like this:
```css
.toggleControlButton {
  composes: fa      from '../../node_modules/font-awesome/css/font-awesome.css';
  composes: fa-fw   from '../../node_modules/font-awesome/css/font-awesome.css';
  composes: fa-bars from '../../node_modules/font-awesome/css/font-awesome.css';
  composes: jsControlButton;
  cursor: pointer;
  float: right;
  line-height: 1.5em;
  height: 1.5em;
  padding: 0 5px;
}
```
and then the example will run and the result image can be shown like follows:
![shiyitu](./192101.png)
Shows that our approach worked and it's the same as the demo on the paraviewweb website.

If you find out any mistakes or you have other solutions, please contact me without hesitation. Thanks a lot!