# react-less
react-less 中配置less


1.初始化并安装项目

```

npx create-react-app my-app

cd my-app/

npm run eject

npm install less less-loader --save

```

2.配置webpack.config.js

```
const cssRegex = /\.css$/;
const cssModuleRegex = /\.module\.css$/;
const sassRegex = /\.(scss|sass)$/;
const sassModuleRegex = /\.module\.(scss|sass)$/;
const lessRegex = /\.less$/;  // 新增less配置
const lessModuleRegex = /\.module\.less$/; // 新增less配置，这个其实不配置也行

```

增加module下面rule规则，可以copy cssRegex或者sassRegex的配置。

```
{
    test: sassModuleRegex,
    use: getStyleLoaders({
            importLoaders: 2,
            sourceMap: isEnvProduction && shouldUseSourceMap,
            modules: true,
            getLocalIdent: getCSSModuleLocalIdent
        },
        "sass-loader"
    )
}, 
// 新增部分
            {
              test: lessRegex,
              exclude: lessModuleRegex,
              use: getStyleLoaders(
                  {
                    importLoaders: 2,
                    sourceMap: isEnvProduction
                        ? shouldUseSourceMap
                        : isEnvDevelopment,
                  },
                  'less-loader'
              ),
              sideEffects: true,
            },

            {
              test: lessModuleRegex,
              use: getStyleLoaders(
                  {
                    importLoaders: 2,
                    sourceMap: isEnvProduction
                        ? shouldUseSourceMap
                        : isEnvDevelopment,
                    modules: true,
                    getLocalIdent: getCSSModuleLocalIdent,
                  },
                  'less-loader'
              ),
            },
```
