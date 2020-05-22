# 解析和构建 DOM

当浏览器拿到服务端返回的 HTML 文件流后，开始对 HTML 文件流进行解析和构建 DOM。

![parse](./images/parse.png)

粗略地来说，就是 Response Body 返回回来的 HTML 字符流，经过状态机处理生成 token，然后使用栈构建 DOM。

## 生成 token

HTML 的 token 主要有：

- “标签开始”的开始  
  `<abc`
- 属性  
  `a="xxx"`
- “标签开始”的结束  
  `/>`
- 文本  
  `hello world`
- 结束标签  
  `</abc>`
- 注释  
  `<!-- comment -->`
- CDATA 节点  
  `<![CDATA[hello world!]]>`

由于字符流是逐步进入的，下一个进来的字符会决定前面字符的 token 类型，所以用**状态机来生成 token**。

![state-machine](./images/state-machine.png)

上图中，红色的 data 表示当前 HTML 字符流，即当前状态机的初始状态。

状态机的初始状态，我们仅仅区分 `<` 和 `非 <`：

- 如果获得的是一个 `非 <` 字符，那么可以认为进入了一个文本节点
- 如果获得的是一个 `<` 字符，那么进入一个标签状态。

## 使用栈构建 DOM 树

当使用状态机创建 token 后，需要将 token emit 出，使用栈将 token 转化为 DOM 树。构建 DOM 树的过程就是使用算法将 token 构造成新的数据结构的过程。

```html
<html maaa="a">
  <head>
    <title>cool</title>
  </head>
  <body>
    <img src="a" />
  </body>
</html>
```

通过这个栈，我们可以构建 DOM 树：

- 栈顶元素就是当前节点；
- 遇到属性，就添加到当前节点；
- 遇到文本节点，如果当前节点是文本节点，则跟文本节点合并，否则入栈成为当前节点的子节点；
- 遇到注释节点，作为当前节点的子节点；
- 遇到 tag start 就入栈一个节点，当前节点就是这个节点的父节点；
- 遇到 tag end 就出栈一个节点（还可以检查是否匹配）。

## 总结

[HTML 标准](https://html.spec.whatwg.org/multipage/parsing.html#tokenization)

生成 DOM 树：

1. 使用状态机生成各个 token
2. 将 token 赋给 element
3. 将 element 放入 stack 中
