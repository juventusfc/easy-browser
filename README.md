# easy-browser

浏览器的主要功能是把 URL 变成屏幕上能显示的网页。

这个过程主要包括：

1. 向 Server 发送请求，Server 返回 HTML
2. 浏览器根据 HTML，构建 DOM
3. 浏览器计算 DOM 上的 CSS
4. 根据 CSS 对元素进行渲染/合成，最后绘制到屏幕上。

注意，上面的过程并非想象的一步做完才能接着下一步，而是一条流水线，即不需要前一步完全完成，下一步就开始处理上一步的输出，这也是我们浏览页面时页面逐步出现的原因。

## 知识体系

- 实现原理
  - [HTTP](/Browser/实现原理-HTTP.md)
  - [解析和构建 DOM](/Browser/实现原理-解析和构建DOM.md)
  - [DOM 添加 CSS](/Browser/实现原理-DOM添加CSS.md)
  - [布局/渲染/合成/绘制](实现原理-布局-渲染-合成-绘制.md)
- 主要的 API
  - [BOM](/Browser/API-BOM.md)
  - [DOM](/Browser/API-DOM.md)
  - [CSSOM](/Browser/API-CSSOM.md)
  - [Event](/Browser/API-Event.md)
- 常见场景
  - [客户端检测](/Browser/客户端检测.md)

## 常用工具

- [抽象语法树生成工具](https://astexplorer.net/)
