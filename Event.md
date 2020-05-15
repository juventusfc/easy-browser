# Event

事件来自输入设备。常见的输入设备有：

- 鼠标
- 触摸屏
- 键盘

## pointer 设备产生的事件

鼠标和触摸屏被称为 pointer 设备，输入最终会被抽象成屏幕上面的一个点。

```javascript
target.addEventListener(type, listener[, options]);
target.addEventListener(type, listener[, useCapture]);
target.addEventListener(type, listener[, useCapture, wantsUntrusted  ]); // Gecko/Mozilla only
```

**捕获过程是从外向内，冒泡过程是从内向外**。

实际上点击事件来自触摸屏或者鼠标，鼠标点击并没有位置信息，但是一般操作系统会根据位移的累积计算出来，跟触摸屏一样，提供一个坐标给浏览器。那么，把这个坐标转换为具体的元素上事件的过程，就是捕获过程了。而冒泡过程，则是符合人类理解逻辑的：当你按电视机开关时，你也按到了电视机

捕获是计算机处理事件的逻辑，而冒泡是人类处理事件的逻辑。

在一个事件发生时，捕获过程跟冒泡过程总是先后发生，跟你是否监听毫无关联。

```html
<body>
  <input id="i" />
</body>
```

```javascript
// true|false indicate useCapture or not
document.body.addEventListener(
  "mousedown",
  () => {
    console.log("key1");
  },
  true
);

document.getElementById("i").addEventListener(
  "mousedown",
  () => {
    console.log("key2");
  },
  true
);

document.body.addEventListener(
  "mousedown",
  () => {
    console.log("key11");
  },
  false
);

document.getElementById("i").addEventListener(
  "mousedown",
  () => {
    console.log("key22");
  },
  false
);
```

输出:

```text
key1
key2
key22
key11
```

## 焦点设备产生的事件

键盘事件是由焦点系统控制的，一般来说，操作系统也会提供一套焦点系统，但是现代浏览器一般都选择在自己的系统内覆盖原本的焦点系统。焦点系统认为整个 UI 系统中，有且仅有一个“聚焦”的元素，所有的键盘事件的目标元素都是这个聚焦元素。

Tab 键被用来切换到下一个可聚焦的元素，焦点系统占用了 Tab 键，但是可以用 JavaScript 来阻止这个行为。

浏览器提供的操作焦点的 API 主要有：

```javascript
document.body.focus();

document.body.blur();
```

## 自定义事件

```javascript
var evt = new Event("look", { bubbles: true, cancelable: false });
document.dispatchEvent(evt);
```
