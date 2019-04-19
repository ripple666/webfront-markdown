### 安装
	npm install --save-dev webpack

如果你使用 webpack 4+ 版本，你还需要安装 CLI。

	npm install --save-dev webpack-cli

### 模块(module)
这些选项决定了如何处理项目中的不同类型的模块。

### rules定义规则

webpack 根据正则表达式，来确定应该查找哪些文件，并将其提供给指定的 loader。在这种情况下，以 .css 结尾的全部文件，都将被提供给 style-loader 和 css-loader。这使你可以在依赖于此样式的文件中 import './style.css'。现在，当该模块运行时，含有 CSS 字符串的 style 标签，将被插入到 html 文件的 <head> 中。

##### style-loader、css-loader 处理css

```js

{
	test:/\.css$/,
	use:['style-loader','css-loader']
}
	
```

##### file-loader处理图片、字体


当你 import MyImage from './my-image.png'，该图像将被处理并添加到 output 目录，_并且_ MyImage 变量将包含该图像在处理后的最终 url。当使用 css-loader 时，如上所示，你的 CSS 中的 url('./my-image.png') 会使用类似的过程去处理。

```js

{
	test:/\.(png|svg|jpg|gif)$/,
	use:['file-loader']
}

```

通过配置好 loader 并将字体文件放在合适的地方，你可以通过一个 @font-face 声明引入。本地的 url(...)

```js

{
	test:/\.(woff|woff2|eot|ttf|otf)$/,
	use:['file-loader']
}

```

##### csv-loader xml-loader处理数据，JSON 是内置的，不需要额外引入


### 使用 source map

### 配置plugin

##### CleanWebpackPlugin
##### HtmlWebpackPlugin
