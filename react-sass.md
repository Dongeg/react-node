# react-scss
react 中设置 scss

```
// create-react-app中默认启用scss/sass

npm run eject // 暴露配置

npm i sass-resources-loader --save-dev // 装依赖包

```

修改webpack.config.js

```
            // Opt-in support for SASS (using .scss or .sass extensions).
            // By default we support SASS Modules with the
            // extensions .module.scss or .module.sass
            {
              test: sassRegex,
              exclude: sassModuleRegex,
              use: getStyleLoaders(
                {
                  importLoaders: 3,
                  sourceMap: isEnvProduction && shouldUseSourceMap,
                },
                'sass-loader'
              ).concat({      // 新增部分开始
                loader: 'sass-resources-loader',
                options: {
                  resources: [
                    // 这里按照你的文件路径填写
                    path.resolve(__dirname, './../src/assets/css/common.scss')
                  ]
                }           // 新增部分结束
              }),
              // Don't consider CSS imports dead code even if the
              // containing package claims to have no side effects.
              // Remove this when webpack adds a warning or an error for this.
              // See https://github.com/webpack/webpack/issues/6571
              sideEffects: true,
            },
            // Adds support for CSS Modules, but using SASS
            // using the extension .module.scss or .module.sass
            {
              test: sassModuleRegex,
              use: getStyleLoaders(
                {
                  importLoaders: 3,
                  sourceMap: isEnvProduction && shouldUseSourceMap,
                  modules: {
                    getLocalIdent: getCSSModuleLocalIdent,
                  },
                },
                'sass-loader'
              )
            },
```

然后重启项目
