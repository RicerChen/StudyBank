# 🧊 Glassmorphism 学习笔记

**Author:** RicerChen\
**Date:** 2025.11.13\
**Project:** React + Vite Personal Blog UI Design

## 💡 一、什么是 Glassmorphism？

> "Glassmorphism" 是一种界面设计风格，让元素看起来像**磨砂玻璃**。\
> 常见于 macOS、Windows 11、Notion、Fluent UI 等现代界面中。\
> 这种设计带来一种"半透明、柔光、悬浮"的质感，非常适合简洁科技风网站。

## 🧠 二、核心特征

  特征         描述
  ------------ ---------------------------------------------------
  半透明背景   使用 `rgba()` 颜色实现部分透明度
  背景模糊     使用 `backdrop-filter: blur()` 模糊元素背后的内容
  柔和边框     白色或浅色半透明边框增强"玻璃边缘感"
  阴影浮层     `box-shadow` 营造悬浮视觉
  渐变背景     背景通常使用渐变色或柔光图片，让玻璃效果更立体

## ⚙️ 三、基础实现代码（纯 CSS）

``` css
.glass {
  background: rgba(255, 255, 255, 0.15);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
  border-radius: 16px;
  border: 1px solid rgba(255, 255, 255, 0.3);
  box-shadow: 0 4px 30px rgba(0, 0, 0, 0.1);
}
```

然后在 HTML 中这样用：

``` html
<div class="glass">
  <h2>Hello Glassmorphism ✨</h2>
  <p>This is a frosted glass effect.</p>
</div>
```

## 🪞 四、在 React + Tailwind CSS 中实现

推荐直接使用 Tailwind 来实现毛玻璃风格，语义清晰而且可组合性强：

``` jsx
export default function GlassCard() {
  return (
    <div className="backdrop-blur-lg bg-white/20 border border-white/30 shadow-lg rounded-2xl p-6 text-white">
      <h2 className="text-xl font-bold">Glassmorphism Card</h2>
      <p className="text-white/80">Smooth, transparent, elegant.</p>
    </div>
  );
}
```

### Tailwind 属性解释：

  属性                 含义
  -------------------- ----------------
  `backdrop-blur-lg`   模糊背景
  `bg-white/20`        半透明白色背景
  `border-white/30`    半透明边框
  `shadow-lg`          柔和阴影
  `rounded-2xl`        圆角玻璃效果

## 🌌 五、设计主题：暮光渐变（Twilight Gradient）

在 Glassmorphism 风格下，背景渐变是关键，它决定了玻璃层的立体感。\
推荐配色如下（与你博客风格一致）：

``` css
body {
  background: linear-gradient(135deg, #6A5ACD, #FF69B4);
}
```

这种从 **Slate Blue → Hot Pink** 的渐变，会呈现出温柔的暮光氛围。

## 🧱 六、两种常见布局风格

  -----------------------------------------------------------------------------------------------------------
  类型                简介                                                   适用场景
  ------------------- ------------------------------------------------------ --------------------------------
  **B. 居中卡片式**   内容集中在页面中央，一到两块玻璃卡片展示文章预览       博客主页、文章区

  **C. 全屏封面式**   整个页面为封面背景，居中显示标题与按钮，点击进入主页   博客首页或介绍页
  -----------------------------------------------------------------------------------------------------------

## 💻 七、全屏封面式（Hero Section）参考结构

``` jsx
import { useNavigate } from "react-router-dom";

export default function Hero() {
  const navigate = useNavigate();

  return (
    <div className="h-screen flex flex-col justify-center items-center bg-gradient-to-br from-[#6A5ACD] to-[#FF69B4] text-white">
      <div className="backdrop-blur-2xl bg-white/10 border border-white/30 rounded-3xl p-10 text-center shadow-2xl">
        <h1 className="text-4xl font-bold mb-2">RicerChen’s Online World</h1>
        <p className="text-white/80 mb-6">Explore My Thoughts</p>
        <button
          onClick={() => navigate("/blog")}
          className="px-6 py-3 bg-white/20 hover:bg-white/30 rounded-xl transition backdrop-blur-md"
        >
          Enter Blog
        </button>
      </div>
    </div>
  );
}
```

特点： - 暮光渐变背景\
- 中心毛玻璃卡片\
- 动态按钮（hover 发光）\
- 点击跳转到 `/blog`

## 🌈 八、延伸优化方向

  优化项        描述
  ------------- ---------------------------------------------
  ✨ 动效       使用 Framer Motion 添加淡入、缩放或浮动动画
  🧭 导航       透明导航栏，悬浮在背景上
  📱 响应式     确保手机端自动居中且内容比例不失真
  🔮 动态背景   使用 CSS 动画让渐变慢速流动，提升氛围感

## 🧩 九、推荐学习资源

-   [MDN:
    backdrop-filter](https://developer.mozilla.org/en-US/docs/Web/CSS/backdrop-filter)\
-   [Tailwind Backdrop
    Utilities](https://tailwindcss.com/docs/backdrop-blur)\
-   [ui.glass](https://ui.glass/) --- 在线生成玻璃风格样式\
-   [Dribbble: Glassmorphism
    UI](https://dribbble.com/tags/glassmorphism) --- 视觉灵感来源

## 🪶 十、学习感想

> 今天学习了 Glassmorphism 的设计思路与实现方式。\
> 我发现这种毛玻璃风格与我的博客主题"RicerChen's Online
> World"非常契合。\
> 它既有未来感，也有温柔的暮光氛围，让整个界面更具层次与质感。\
> 下一步，我准备把博客首页改造成全屏封面式，做成一个沉浸式的入口页面
> ✨。
