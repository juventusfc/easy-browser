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

当使用状态机创建 token 后，使用栈将 token 转化为 DOM 树。构建 DOM 树的过程就是使用算法将 token 构造成新的数据结构的过程。
