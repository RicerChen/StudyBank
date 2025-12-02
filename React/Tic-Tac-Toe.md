# Tic-Tac-Toe

## 逐行理解

### App.js

```js
export default function Square() {
  return <button className="square">X</button>;
}
```

第一行定义了一个名为 `Square` 的函数。 

`export` JavaScript 关键字使该函数可以在此文件外部访问。

 `default` 关键字告诉使用您代码的其他文件，它是您文件中的 main 函数。

第二行返回一个按钮。

 `return` JavaScript 关键字意味着后面的任何内容都会作为值返回给函数的调用者。

<button>是一个 JSX 元素。 JSX 元素是 JavaScript 代码(行为逻辑)和 HTML 标记的组合，用于描述您想要显示的内容。 

className="square"是一个按钮属性或道具，告诉 CSS 如何设置按钮的样式。

</button>关闭 JSX 元素以指示任何后续内容不应放置在按钮内部。

### styles.css

```css
* {
  box-sizing: border-box;
}

body {
  font-family: sans-serif;
  margin: 20px;
  padding: 0;
}

h1 {
  margin-top: 0;
  font-size: 22px;
}

h2 {
  margin-top: 0;
  font-size: 20px;
}

h3 {
  margin-top: 0;
  font-size: 18px;
}

h4 {
  margin-top: 0;
  font-size: 16px;
}

h5 {
  margin-top: 0;
  font-size: 14px;
}

h6 {
  margin-top: 0;
  font-size: 12px;
}

code {
  font-size: 1.2em;
}

ul {
  padding-inline-start: 20px;
}

* {
  box-sizing: border-box;
}

body {
  font-family: sans-serif;
  margin: 20px;
  padding: 0;
}

.square {
  background: #fff;
  border: 1px solid #999;
  float: left;
  font-size: 24px;
  font-weight: bold;
  line-height: 34px;
  height: 34px;
  margin-right: -1px;
  margin-top: -1px;
  padding: 0;
  text-align: center;
  width: 34px;
}

.board-row:after {
  clear: both;
  content: '';
  display: table;
}

.status {
  margin-bottom: 10px;
}
.game {
  display: flex;
  flex-direction: row;
}

.game-info {
  margin-left: 20px;
}

```

该文件定义了 React 应用程序的样式。

前两个 CSS 选择器（ `*` 和 `body` ）定义应用程序大部分的样式，而 `.square` 选择器定义 `className` 属性设置为 `square` 的任何组件的样式。

在您的代码中，这将与 `App.js` 文件中的 Square 组件中的按钮匹配。

### index.js

```js
import { StrictMode } from 'react';
import { createRoot } from 'react-dom/client';
import './styles.css';

import App from './App';
```

第 1-5 行将所有必要的部分组合在一起：

- React 
- React 与 Web 浏览器对话的库 (React DOM)
- 组件的样式
- 您在 `App.js` 中创建的组件..

文件的其余部分将所有部分组合在一起，并将最终产品注入 `public` 文件夹中的 `index.html` 中。



### 如何从一个方块生成九宫格

#### 并列

```js
export default function Square() {
  return (
    <>
      <button className="square">X</button>
      <button className="square">X</button>
    </>
  );
}
```

##### pitfall陷阱！

相邻的 JSX 元素必须包含在封闭标签中

React 组件需要返回**单个** JSX 元素，而不是像两个按钮那样返回多个相邻的 JSX 元素。要解决此问题，您可以使用片段（`<>` 和 </> ）来包装多个相邻的 JSX 元素，

#### 分行

用

```js
<div>
</div>
```

标签把三个方块封装成一个对象

```js
export default function Square() {
  return (
    <>
      <div className = "board-row">
        <button className="square">X</button>
        <button className="square">X</button>
        <button className="square">X</button>
      </div>

      <div className = "board-row">
        <button className="square">X</button>
        <button className="square">X</button>
        <button className="square">X</button>
      </div>

      <div className = "board-row">
        <button className="square">X</button>
        <button className="square">X</button>
        <button className="square">X</button>
      </div>
    </>
  );
}
```

### 通过 props 传递数据 



```js
function Square() {
  return <button className="square">1</button>;
}

export default function Board() {
  return (
    <>
      <div className="board-row">
        <Square />
        <Square />
        <Square />
      </div>

      <div className="board-row">
        <Square />
        <Square />
        <Square />
      </div>

      <div className="board-row">
        <Square />
        <Square />
        <Square />
      </div>
    </>
  );
}

```

使用 props 将每个方块应具有的值从父组件 (`Board` ) 传递到其子组件 (`Square` )。

```js
function Square({ value }) {
  return <button className="square">1</button>;
}
```

表示 Square 组件可以传递一个名为 `value` 的 prop ..

#### 辨析

```js

function Square({ value }) {
  return <button className="square">value</button>;
}


function Square({ value }) {
  return <button className="square">{value}</button>;
}
```

<img src="C:\Users\鳌\AppData\Roaming\Typora\typora-user-images\image-20251203012900229.png" alt="image-20251203012900229" style="zoom: 33%;" />

<img src="C:\Users\鳌\AppData\Roaming\Typora\typora-user-images\image-20251203012913840.png" alt="image-20251203012913840" style="zoom: 33%;" />

您想要从组件中呈现名为 `value` 的 JavaScript 变量，而不是“值”一词。要从 JSX“转义到 JavaScript”，您需要大括号。

更新后如下

```js
function Square({ value }) {
  return <button className="square">{value}</button>;
}

export default function Board() {
  return (
    <>
      <div className="board-row">
        <Square value="1" />
        <Square value="2" />
        <Square value="3" />
      </div>

      <div className="board-row">
        <Square value="4" />
        <Square value="5" />
        <Square value="6" />
      </div>

      <div className="board-row">
        <Square value="7" />
        <Square value="8" />
        <Square value="9" />
      </div>
    </>
  );
}

```

### 制作交互内容

