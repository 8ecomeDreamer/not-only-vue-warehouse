## 总结

### URL从输入到打开网站经历了哪些过程？

1. 本地DNS对URL进行解析，转化为ip地址。
2. ip地址对目标ip地址建立TCP连接后发起http请求，期间经历三次握手过程。
3. 服务端获取到请求后拿到响应的数据，对页面进行渲染。

**整个过程一共经历了五个阶段：解析ip地址、建立tcp连接、发起http请求、获取服务器响应、渲染界面。因此，性能优化也是从这几个方面进行优化。**

### 网络优化

> 网络优化两个大方向： 减少请求http次数、缩短单次http请求的时间。（即资源的压缩与优化）

### [webpack-bundle-analyzer](https://www.npmjs.com/package/webpack-bundle-analyzer)

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
