#### 通过 sass-resources-loader 全局注册变量

```
npm install sass-resources-loader
```

##### 在 build/utils.js 如下配置

```
exports.cssLoaders = function (options) {

    function generateSassResourceLoader () {
        var loaders = [
            cssLoader,
            'sass-loader',
            {
                loader: 'sass-resources-loader',
                options: {
                    resources: [
                        path.resolve(__dirname, '../src/assets/var.scss'), //需要注册到全局的文件
                        path.resolve(__dirname, '../src/assets/mixins.scss')
                    ]
                }
            }
        ]
        if (options.extract) {
            return ExtractTextPlugin.extract({
                use: loaders,
                fallback: 'vue-style-loader'
            })
        } else {
            return ['vue-style-loader'].concat(loaders)
        }
    }

    return {
        sass: generateSassResourceLoader(),
        scss: generateSassResourceLoader(),
    }
}

```
