# React-SlowStart

## 描述用户界面UI

React 是一个用于渲染用户界面 (UI) 的 JavaScript 库。 

UI 由按钮、文本和图像等小单元构建。

 React 允许您将它们组合成可重用、可嵌套的组件。  从网站到手机应用程序，屏幕上的所有内容都可以分解为组件。



### 编写第一个组件

React 组件是一个 JavaScript 函数，您可以在其中添加标记。

这是一个 `Gallery` 组件渲染了三个 `Profile` 组件：

```react
function Profile() {
  return (  
    <img  
      src="https://i.imgur.com/MK3eW3As.jpg"
      alt="Katherine Johnson"  
    />
  );  
}

export default function Gallery() {
  return (  
    <section>  
      <h1>Amazing scientists</h1>
      <Profile />  
      <Profile />  
      <Profile />  
    </section>  
  );  
}
```



### 什么是组件

组件是UI构建块

在 Web 上，HTML 允许我们使用其内置标签集（如 <h1><li> :）创建丰富的结构化文档。

```react
<article>
  <h1>My First Component</h1>
  <ol>
    <li>Components: UI Building Blocks</li>
    <li>Defining a Component</li>
    <li>Using a Component</li>
  </ol>
</article>
```

React 允许您将标记、CSS 和 JavaScript 组合到自定义“组件”中，即应用程序的可重用 UI 元素。 

就是联合三者构建成一个组件？

对，组件就是一个函数/类，把上面三者封装到一起

#### 例子

```react
//组件文件
// LikeButton.jsx
import React, { useState } from 'react';
import './LikeButton.css'; // 引入专属 CSS

export default function LikeButton() {
  // 🔹 JavaScript 逻辑：管理状态
  const [liked, setLiked] = useState(false);
  const [count, setCount] = useState(0);

  // 处理点击
  const handleClick = () => {
    if (liked) {
      setCount(count - 1);
    } else {
      setCount(count + 1);
    }
    setLiked(!liked);
  };

  // 🔹 标记（JSX）+ 动态类名（结合 JS 和 CSS）
  return (
      // className动态设置 CSS 类名 的写法，用到了 模板字符串（template literal） 和 三元表达式。
    <button 
      className={`like-button ${liked ? 'liked' : ''}`} 
      onClick={handleClick}
    >
      👍 {count}
    </button>
  );
}
```



```react
单行理解
"like-button " + (liked ? "liked" : "")
```

- 如果 `liked` 是 `true` → `"like-button " + "liked"` → `"like-button liked"`
- 如果 `liked` 是 `false` → `"like-button " + ""` → `"like-button "`

（模板字符串 ``...`` 只是更现代的拼接方式）



### 💡 组件优势

#### 1. **高内聚**

- 所有和“点赞按钮”相关的东西（结构、样式、行为）都在一个地方。
- 修改时不用到处找文件。

#### 2. **可复用**

- 写一次，整个应用随便用。
- 比如电商网站的商品卡片、用户头像、导航菜单……都可以做成组件。

#### 3. **隔离性**

- 每个 `LikeButton` 实例有自己的状态（你点第一个，第二个不会变）。
- CSS 类名如果用 CSS Modules 还能避免冲突。

### 定义组件

React 组件是一个 JavaScript 函数

#### **第 1 步：导出组件**

`export default` 前缀是标准 JavaScript 语法（并非特定于 React）。它允许您在文件中标记主要函数，以便稍后可以从其他文件导入它。

#### 第 2 步：定义函数

##### Pitfall陷阱

React 组件是常规的 JavaScript 函数，但它们的名称必须以大写字母开头，否则它们将无法工作！

### 第 3 步：添加标记 

<img /> 的编写方式类似于 HTML，但它实际上是 JavaScript！这种语法称为 JSX ，它允许您将标记嵌入到 JavaScript 中。

```react
export default function Profile() {
return(                                                  
    <img        
      src="https://i.imgur.com/MK3eW3Am.jpg"
      alt="Katherine Johnson"      
    />
  )
}
```

Return 语句可以全部写在一行上，如本组件所示：

```react
return <img src="https://i.imgur.com/MK3eW3As.jpg" alt="Katherine Johnson" />;
```

但是，如果您的标记并非全部与 `return` 关键字在同一行，则必须将其括在一对括号中：

```react
return (
  <div>
    <img src="https://i.imgur.com/MK3eW3As.jpg" alt="Katherine Johnson" />
  </div>
);
```

如果return语句在一行上，return末尾要加分号；如果不在同一行，不用加分号且在括号内

##### pitfall

如果没有括号，`return` 之后的行上的任何代码都将被忽略！

### 使用组件

使用多个 `Profile` 组件的 `Gallery` 组件：

```react
function Profile() {
  return (  
    <img  
      src="https://i.imgur.com/MK3eW3As.jpg"
      alt="Katherine Johnson"  
    />
  );  
}

export default function Gallery() {
  return (        
    <section>        
      <h1>Amazing scientists</h1>										<Profile/>                                               <Profile/>                                               <Profile/>                                              </section>                                        );                                                     
}

```

#### 浏览器看到什么

注意大小写的区别：

- <section> 是小写的，所以 React 知道我们引用的是 HTML 标签。

- <Profile> 以大写 `P` 开头，因此 React 知道我们想要使用名为 `Profile` 的组件..

实际上浏览器看到的是这样的

```react
<section>

  <h1>Amazing scientists</h1>

  <img src="https://i.imgur.com/MK3eW3As.jpg" alt="Katherine Johnson" />

  <img src="https://i.imgur.com/MK3eW3As.jpg" alt="Katherine Johnson" />

  <img src="https://i.imgur.com/MK3eW3As.jpg" alt="Katherine Johnson" />

</section>
```

### 嵌套和组织组件

因为 `Profile` 组件在 `Gallery` 内部渲染（甚至多次！），我们可以说 `Gallery` 是父组件，将每个 `Profile` 渲染为“子组件”。这是 React 魔力的一部分：你可以定义一个组件一次，然后在任意多的地方、任意多次使用它。

#### pitfall

组件可以渲染其他组件，但绝对不能嵌套它们的定义：

```react
export default function Gallery() {
  // 🔴 Never define a component inside another component!
  function Profile() {
    // ...
  }
  // ...
}
```

当子组件需要来自父组件的一些数据时，通过 props 传递它而不是嵌套定义。

```react
export default function Gallery() {
  // ...
}

// ✅ Declare components at the top level
function Profile() {
  // ...
}
```



### 根组件

**每个 React 应用都有一个“起点”组件，叫“根组件”**。

#### 🌱 什么是“根组件”？

- 它是**整个应用的最顶层组件**，所有其他组件都嵌套在它里面。
- 就像一棵树的“树根”，其他枝叶（子组件）都从它长出来。

#### 📁 不同工具中根组件的位置：

| 工具 / 框架                    | 根组件文件位置                    | 说明                                   |
| ------------------------------ | --------------------------------- | -------------------------------------- |
| **Create React App**（最常见） | `src/App.js`                      | 你写的 `export default App` 就是根组件 |
| **CodeSandbox**（在线编辑器）  | 通常是 `src/App.js` 或 `index.js` | 自动创建                               |
| **Next.js**（React 框架）      | `pages/index.js`                  | 访问 `/` 时显示这个组件                |
| **Vite + React**               | `src/App.jsx`                     | 类似 Create React App                  |







纯自己手写的第一个组件来着

AI能不能不要这么好用了！！！！！

```react
// Write your component below!
export default function Congratulations() {
  return(
    <h1>Good job!</h1>
  )
} 
```

### 移动组件

您可以通过三个步骤移动组件：

1. 创建一个新的 JS 文件来放入组件。
2. 从该文件导出函数组件（使用默认导出或命名导出）。
3. 将其导入到您将使用该组件的文件中（使用导入默认或命名导出的相应技术）。