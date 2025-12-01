# React-QuickStart

## 条件渲染

无特殊语法；使用编写JavaScript代码时相同的技术

## 渲染列表

依赖JavaScript功能呈现组件列表

```javascript
const products = [

  { title: 'Cabbage', id: 1 },

  { title: 'Garlic', id: 2 },

  { title: 'Apple', id: 3 },

];

//map函数将产品数组转换为<li>项

const listItems = products.map(product =>

  <li key={product.id}>

    {product.title}

  </li>

);



return (

  <ul>{listItems}</ul>

);
```

<li>具有key属性，对于每一项都应该传递一个字符串或者数字，以在同级项目中唯一标识该项目



## 相应事件

在组件内声明事件处理函数来响应事件

```react
//组件
function MyButton() {

  function handleClick() {

    alert('You clicked me!');

  }



  return (
  
    <button onClick={handleClick}>

      Click me

    </button>

  );

}
```

`onClick={handleClick}` 末尾没有括号！不要调用事件处理函数：您只需将其传递下去即可。当用户单击按钮时，React 将调用您的事件处理程序。

| 你要做什么                 | 写法                                      |
| -------------------------- | ----------------------------------------- |
| **让函数在点击时执行**     | `onClick={函数名}` （无括号）             |
| **让函数在页面加载时执行** | `函数名()` （有括号，但通常不是你想要的） |

## 更新屏幕

组件记住一些信息并显示它的功能

```react
//第一步：导入useState

import { useState } from 'react';

//声明状态变量
function MyButton() {

  const [count, setCount] = useState(0);
  // ...
```

 `useState` 内有两个变量：当前状态 (`count` )，以及允许您更新它的函数 (`setCount` )。可以起任何名称，但约定是写 `[something, setSomething]` ..



第一次显示按钮时，count是0，因为我将0传给useState()。当我想更改状态时我需要调用setCount()，并把新值传给它。单击此按钮将增加计数器：。

```react
function MyButton() {

  const [count, setCount] = useState(0);



  function handleClick() {

    setCount(count + 1);

  }



  return (

    <button onClick={handleClick}>

      Clicked {count} times

    </button>

  );

}
```



多次渲染同一个组件，每个组件都会获得自己的状态==>

**同一个组件被多次使用时，每个实例都有独立的状态。**

**🎯 为什么这个特性很重要？**

1. **可复用性**：你可以放心地多次使用同一个组件（比如 ``、``），不用担心状态互相干扰。
2. **隔离性**：每个组件管理自己的数据，符合“单一职责”原则。
3. **可预测性**：点击某个按钮只影响它所在的组件，不会意外改变其他地方。

## 使用钩子Hooks

以 `use` 开头的函数称为 Hooks 。 

`useState`是React提供的内置Hook。

您可以在 API 参考中找到其他内置 Hook，或者组合Hook编写自己的Hook。

只能在组件顶部调用Hooks，如果您想在条件或循环中使用 `useState`，请提取一个新组件并将其放在那里。

## 组件之间共享数据

有时需要组件来共享数据并始终一起更新

例如：要使两个 `MyButton` 组件显示相同的 `count` 并一起更新，您需要将状态从各个按钮**“向上”移动**到包含所有按钮的最接近的组件。

