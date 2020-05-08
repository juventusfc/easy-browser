# CSSOM

CSSOM 是 CSS 的对象模型，允许用户通过操作 CSSOM 的 API 进行开发。

[参考手册](https://css-tricks.com/an-introduction-and-guide-to-the-css-object-model-cssom/)

## 模型部分

- `document.styleSheets` 获取文档中所有的样式表
- `document.styleSheets[0].insertRule("p { color:pink; }", 0) document.styleSheets[0].removeRule(0)` 修改样式表
- `window.getComputedStyle(elt, pseudoElt);` 获取某个 Element 的属性

## View 部分

CSSOM View 这一部分的 API，可以视为 DOM API 的扩展，它在原本的 Element 接口上，添加了显示相关的功能，这些功能，又可以分成三个部分：

- 窗口部分: 窗口 API 用于操作浏览器窗口的位置、尺寸等
- 滚动部分: 包括视口滚动和元素滚动
- 布局部分: 包括全局尺寸信息和元素的布局信息
