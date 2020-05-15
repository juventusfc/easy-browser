# CSSOM

CSSOM 是 CSS 的对象模型，允许用户通过操作 CSSOM 的 API 进行开发。在 W3C 标准中，它包含两个部分：描述样式表和规则等 CSS 的模型部分（CSSOM），和跟元素视图相关的 View 部分（CSSOM View）。

## 模型部分

- `document.styleSheets` 获取文档中所有的样式表
- `document.styleSheets[0].cssRules` 获取某个样式表中的所有规则
- `document.styleSheets[0].insertRule("p { color:pink; }", 0)`
- `document.styleSheets[0].removeRule(0)`
- `window.getComputedStyle(elt, pseudoElt);` 获取某个 Element 的属性

## View 部分

CSSOM View 这一部分的 API，可以视为 DOM API 的扩展，它在原本的 Element 接口上，添加了显示相关的功能：

- 窗口部分: 窗口 API 用于操作浏览器窗口的位置、尺寸等

  窗口部分由 window 对象上的一组 API 控制

  - `moveTo(x, y)` 窗口移动到屏幕的特定坐标
  - `moveBy(x, y)` 窗口移动特定距离
  - `resizeTo(x, y)` 改变窗口大小到特定尺寸
  - `resizeBy(x, y)` 改变窗口大小特定尺寸

- 滚动部分: 包括视口滚动和元素滚动

  - 视口滚动

    可视区域（视口）滚动行为由 window 对象上的一组 API 控制。

    - `scrollX` 是视口的属性，表示 X 方向上的当前滚动距离，有别名 pageXOffset
    - `scrollY` 是视口的属性，表示 Y 方向上的当前滚动距离，有别名 pageYOffset
    - `scroll(x, y)` 使得页面滚动到特定的位置，有别名 scrollTo，支持传入配置型参数 {top, left}
    - `scrollBy(x, y)` 使得页面滚动特定的距离，支持传入配置型参数 {top, left}。

  - 元素滚动

    在 Element 类（参见 DOM 部分），为了支持滚动，加入了以下 API。

    - `scrollTop` 元素的属性，表示 Y 方向上的当前滚动距离
    - `scrollLeft` 元素的属性，表示 X 方向上的当前滚动距离
    - `scrollWidth` 元素的属性，表示元素内部的滚动内容的宽度，一般来说会大于等于元素宽度
    - `scrollHeight` 元素的属性，表示元素内部的滚动内容的高度，一般来说会大于等于元素高度
    - `scroll(x, y)` 使得元素滚动到特定的位置，有别名 scrollTo，支持传入配置型参数 {top, left}
    - `scrollBy(x, y)` 使得元素滚动到特定的位置，支持传入配置型参数 {top, left}
    - `scrollIntoView(arg)` 滚动元素所在的父元素，使得元素滚动到可见区域，可以通过 arg 来指定滚到中间、开始或者就近。

- 布局部分: 包括全局尺寸信息和元素的布局信息

## 参考文档

[参考手册](https://css-tricks.com/an-introduction-and-guide-to-the-css-object-model-cssom/)
