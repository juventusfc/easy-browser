# BOM

BOM 表示 Browser Object Model，为 JavaScript 提供了控制浏览器中与显示内容无关的功能，比如窗口控制功能、历史记录控制功能等。

## window 对象

window 对象表示浏览器窗口的一个实例，在网页中用 JavaScript 定义的任何对象、变量、函数，都是以 window 作为其 Global 对象的。也就是说，浏览器提供了一个宿主对象 window 给 JavaScript。

```javascript
var age = 29;

age; // 29
window.age; // 29
```

以上代码，在浏览器中执行时，相当于在 window 对象上创建了 age 属性，值为 29。

在以前的代码中，经常会看到使用 frame，使一个浏览器窗口加载多个 HTML。

```html
<!DOCTYPE html>
<html>
  <head>
    <title>HTML Frames</title>
  </head>

  <frameset rows="10%,80%,10%">
    <frame name="top" src="/html/top_frame.htm" />
    <frame name="main" src="/html/main_frame.htm" />
    <frame name="bottom" src="/html/bottom_frame.htm" />

    <noframes>
      <body>
        Your browser does not support frames.
      </body>
    </noframes>
  </frameset>
</html>
```

在这个例子中，最外层的 HTML 引入了其他 3 个 HTML，这 3 个 HTML 也会生成独立的 window 对象，附属在最外层的 window 对象上。可以使用 `top.frame[1]` 来获得里层的第二个 window 对象。**HTML5 后，建议不要有这种操作**。

网页中引入了框架、库后，会将框架中定义的全局对象变为 window 对象的属性。比如我们经常使用的 jQuery，只要我们在 HTML 引入了这个框架，就可以在 JavaScript 中使用`$`了。`window.$ == $`的结果是 true。

window 主要用于操作窗口，常见的操作有：

- 移动窗口

  移动窗口常用的方法有 `moveTo()` 和 `moveBy()`。由于浏览器的限制，只能移动自己创建的窗口。

  ```html
  <!DOCTYPE html>
  <html>
    <body>
      <p>
        Open "myWindow" and move the new window to the top left corner of the
        screen:
      </p>

      <button onclick="openWin()">Open "myWindow"</button>
      <button onclick="moveWin()">Move "myWindow"</button>

      <script>
        var myWindow;

        function openWin() {
          myWindow = window.open("", "myWindow", "width=200, height=100");
          myWindow.document.write("<p>This is 'myWindow'</p>");
        }

        function moveWin() {
          myWindow.moveTo(500, 100);
          myWindow.focus();
        }
      </script>
    </body>
  </html>
  ```

- 调整窗口大小

  - `resizeTo(x,y)`: 调整到大小 x,y
  - `resizeBy(x,y)`: 在原来的基础上，调整 x,y

- 导航和打开窗口

  - `open(URL, name, specs, replace)`

- 关闭窗口

  - `close()`: 该方法仅适用于自己创建的窗口

- 调出系统对话框

  显示对话框时，代码停止执行。

  - `alert()`
  - `confirm()`
  - `prompt()`

## location 对象

location 对象提供了当前窗口中加载的文档的相关内容以及导航功能。开发中，主要用它控制和获取浏览器地址栏。在浏览器中，`location`、 `window.location`、 `document.location`完全相等。

location 的属性主要有：

```json
{
  "href": "https://www.google.com/search?q=JavaScript+bad+things&rlz=1C1GCEU_enNL819SG819&biw=1536&bih=722&source=lnt&tbs=cdr%3A1%2Ccd_min%3A11%2F1%2F2016%2Ccd_max%3A&tbm=", // 完整 URL
  "ancestorOrigins": {},
  "origin": "https://www.google.com",
  "protocol": "https:", // 协议
  "host": "www.google.com", // 服务器名称和端口号
  "hostname": "www.google.com", // 服务器名称
  "port": "", // 端口号
  "pathname": "/search", // 路径
  "search": "?q=JavaScript+bad+things&rlz=1C1GCEU_enNL819SG819&biw=1536&bih=722&source=lnt&tbs=cdr%3A1%2Ccd_min%3A11%2F1%2F2016%2Ccd_max%3A&tbm=", // 查询字符串
  "hash": "" // Hash值
}
```

常用 API:

- 在浏览器 history 中留下记录

  - 直接修改 location 的属性(hash 除外)以更改 URL，浏览器会以新的 URL 重新加载
  - `location.assign("http://www.baidu.com")`: 更改 URL 并重新加载

- 不在浏览器 history 中留下记录

  - `location.replace("http://www.huawei.com")`:

比如在`http://www.qq.com`中，使用`location.assign("http://www.baidu.com")`，会在 history 中留下 qq 和 baidu 记录。接着，在 baidu 这个页面执行`location.replace("http://www.huawei.com")`,在 history 中，huawei 会覆盖 baidu，也就是说，在 history 中，只留下了 qq 和 huawei。

## navigator 对象

navigator 对象用以识别客户端浏览器。

## screen 对象

screen 对象用以表明客户端的能力，如显示器的像素宽度和高度等。

## history 对象

history 对象保存了上网的历史记录。出于安全考虑，不能直接得知用户浏览过的 URL。

常用属性和方法：

- length: 历史纪录的数量
- `go(-1)`: 后退一页
- `back()`: 后退一页
- `go(1)`: 前进一页
- `forward()`: 前进一页
