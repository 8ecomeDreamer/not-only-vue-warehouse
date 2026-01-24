| col1 | col2 | col3 |
| ---- | ---- | ---- |
|      |      |      |
|      |      |      |

## 总结

### URL从输入到打开网站经历了哪些过程？

1. 本地DNS对URL进行解析，转化为ip地址。
2. ip地址对目标ip地址建立TCP连接后发起http请求，期间经历三次握手过程。
3. 服务端获取到请求后拿到响应的数据，对页面进行渲染。

**整个过程一共经历了五个阶段：解析ip地址、建立tcp连接、发起http请求、获取服务器响应、渲染界面。因此，性能优化也是从这几个方面进行优化。**

### 网络优化

> 网络优化两个大方向： 减少请求http次数、缩短单次http请求的时间。（即资源的压缩与优化）

#### [webpack-bundle-analyzer](https://www.npmjs.com/package/webpack-bundle-analyzer)

我们要学会使用一个非常好用的包组成可视化工具——[webpack-bundle-analyzer](https://www.npmjs.com/package/webpack-bundle-analyzer)，配置方法和普通的 plugin 无异，它会以矩形树图的形式将包内各个模块的大小和依赖关系呈现出来。

vue3版本使用vite，则推荐vite-bundler-analyzer，格局如官方所提供这张图所示。

![image](../images/vite-bundle-analyzer.gif)

```javascript
import { analyzer } from 'vite-bundle-analyzer'

export default defineConfig({
  ...
  plugins: [
  ...
    analyzer({
      analyzerPort: 8889, // 修改为其他端口，比如 8889
      openAnalyzer: true
    })
  ],

```

> 插件默认8888端口，可以使用 npx vite-bundle-analyzer --port 8889 命令或者在配置项中添加具体端口来启动可视化工具。

config中引入插件后，启动项目后类似下图。

![image](../images/vite-bundle-analyzer-project.png)

#### 图片优化

> 学会JPG认各种图片格式

JPEG、JPG、PNG（PNG-8、PNG-24）、Webp、SVG、Base64

|          | JPG                            | JPEG   | PNG-8                          | PNG-24                                                                              | Webp                         | SVG                                | Base64                    |
| -------- | ------------------------------ | ------ | ------------------------------ | ----------------------------------------------------------------------------------- | ---------------------------- | ---------------------------------- | ------------------------- |
| 常见用途 | 轮播图                         | 轮播图 | 小logo或对颜色要求比较高的图片 | 小logo或对颜色要求比较高的图片                                                      |                              | 小图标                             | 小图标、雪碧图            |
| 优点     | 体积小，加载速度快，不支持透明 |        | 无损压缩，支持透明             | 优缺点与png-8相同，<br />但相比前者支持传输更多颜色，<br />约1000多种， 前者256种。 | 全能型选手（jpg+png+gif）    | 图片放大不失真，<br />可用代码修改 | 以编码形式存储            |
| 缺点     | 有损压缩                       |        | 体积大，加载速度慢             |                                                                                     | 兼容性会较差，资源占用率较高 | 渲染成本、学习成本高               | 体积约正常图片体积的4/3倍 |

#### 存储优化
