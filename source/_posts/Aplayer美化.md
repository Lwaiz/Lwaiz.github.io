---
title: APlayer 美化指南：打造现代化毛玻璃音乐播放器
date: 2026-05-13 12:06:14
cover: /img/background/bg4.png
tags: [Hexo , Butterfly , Aplayer , 博客美化]
categories: 设计美化
description: Hexo + Butterfly博客，使用Aplayer播放器实现网页播放器，支持导入歌单，美化毛玻璃特效，自动隐藏呼出
---

# APlayer 美化指南：打造现代化毛玻璃音乐播放器

## 前言

博客中的音乐播放器，其实是非常容易被忽略的一个组件。

默认的播放器虽然功能完整，但在视觉效果上通常存在一些问题：

- UI 风格偏朴素
- 与博客主题不统一
- 深色模式适配一般
- 固定播放器交互生硬
- 歌单缺少层次感

于是我决定对Aplayer播放器的显示效果进行一次彻底重构。

最终实现了：

- 毛玻璃（Glassmorphism）效果
- 深浅色双模式适配
- 当前播放高亮
- 自定义滚动条
- 自动隐藏播放器
- 圆角与现代化 UI
- 更舒服的交互动画

本文将完整分享整个美化过程。

---

# 最终效果

本文最终实现：

- 半透明毛玻璃播放器
- 自动跟随博客深色模式
- 鼠标悬停展开播放器
- 当前播放歌曲高亮
- 更现代的播放器布局

适用于：

- Hexo
- Butterfly
- APlayer
- MetingJS

---

# 什么是 APlayer

APlayer 是一个非常流行的 HTML5 音乐播放器。

特点：

- 颜值高
- 支持歌词
- 支持歌单
- 支持固定播放器
- 支持网易云 / QQ 音乐等平台

通常会搭配：

- MetingJS

一起使用。

官方地址：

- https://github.com/DIYgod/APlayer
- https://github.com/metowolf/MetingJS

---

# 基础引入

## 引入 APlayer

```html
inject:
  head:
    - <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/aplayer@1.10.1/dist/APlayer.min.css">
    - <link rel="stylesheet" href="/css/aplayer.css">
  bottom:
    - <script src="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.js"></script>
    - <script src="https://cdn.jsdelivr.net/npm/meting@2/dist/Meting.min.js"></script>
    - <meting-js
        server="netease"
        type="playlist"
        id="964806107"
        fixed="true"
        autoplay="false"
        loop="all"
        lrcFolded="true">
      </meting-js>
    - <script>var observer=new MutationObserver(function(e){var t=document.querySelector(".aplayer-icon-lrc");t&&(setTimeout(function(){t.click()},1),observer.disconnect())});observer.observe(document.body,{childList:true,subtree:true});</script>
    - <script src="https://cdn.jsdelivr.net/npm/dayjs@1.11.7/dayjs.min.js"></script>
    - <script src="https://cdn.jsdelivr.net/npm/dayjs@1.11.7/plugin/duration.min.js"></script>
    - <script src="/scripts/realtime.js"></script>

```

其中，```/css/aplayer.css``` 是自定义的播放器css文件。

---

## 添加播放器

```html
<meting-js
  server="netease"
  type="playlist"
  id="123456"
  fixed="true"
  autoplay="false"
  loop="all"
  order="random"
  preload="auto"
  list-folded="true">
</meting-js>
```

---

# 毛玻璃效果实现

这是整个播放器美化中最核心的一部分。

## 核心代码

```css
.aplayer {
  background: rgba(255, 255, 255, 0.25) !important;
  position: relative;
  border-radius: 11px 11px 0 0 !important;
}

.aplayer-list,
.aplayer-info {
  backdrop-filter: blur(25px);
  border: none !important;
}
```

---

## 原理解析

毛玻璃效果主要由两部分组成：

### 1. 半透明背景

```css
background: rgba(255,255,255,0.25);
```

这里的：

- `rgba`
- 最后的 `0.25`

表示透明度。

---

### 2. 背景模糊

```css
backdrop-filter: blur(25px);
```

这是现代 CSS 中实现 Glassmorphism 的关键。

它会：

- 模糊后方内容
- 保留透明感
- 提升层次感

也是现在很多：

- macOS
- iOS
- Windows 11

UI 的核心设计语言。

---

# 圆角与布局优化

默认播放器的边角比较生硬。

所以这里统一增加圆角。

## 核心代码

```css
.aplayer.aplayer-fixed .aplayer-list {
  border-radius: 10px 10px 0 0 !important;
}

.aplayer.aplayer-fixed .aplayer-miniswitcher {
  border-radius: 0 6px 6px 0 !important;
}
```

---

## 效果提升

圆角的好处：

- UI 更现代
- 更符合 Butterfly 风格
- 减少“方块感”
- 与毛玻璃更搭配

---

# 自定义滚动条

歌单默认滚动条比较丑。

这里我们进行统一美化。

## 核心代码

```css
.aplayer .aplayer-list ol::-webkit-scrollbar {
  width: 5px;
}

.aplayer .aplayer-list ol::-webkit-scrollbar-thumb {
  border-radius: 3px;
  background-color: #1993de;
}
```

---

## 效果说明

这里主要使用：

```css
::-webkit-scrollbar
```

系列伪元素。

实现：

- 更细的滚动条
- 圆角
- hover 动画
- 自定义颜色

整体观感会舒服很多。

---

# 歌单高亮优化

这是整个播放器里我最喜欢的一部分。

## 默认问题

原版播放器：

- 当前播放不明显
- hover 没有层次感
- 歌单像普通列表

所以这里进行了重构。

---

## hover 效果

```css
.aplayer .aplayer-list ol li:hover {
  background: rgba(0, 0, 0, 0.1) !important;
}
```

---

## 当前播放高亮

```css
.aplayer .aplayer-list ol li.aplayer-list-light {
  background: rgba(159, 158, 158, 0.4) !important;
  backdrop-filter: blur(30px) !important;
  border-radius: 6px !important;
}
```

---

## 当前播放指示条

```css
.aplayer-list-cur {
  background-color: #006aec !important;
  width: 3.5px !important;
}
```

---

## 为什么这样设计

这样处理后：

- 当前播放会非常醒目
- 层次感更强
- 有类似 Apple Music 的感觉
- 歌单不会显得“死板”

---

# 字体与文字优化

默认字体其实并不统一。

这里统一了：

- 歌名
- 歌手
- 标题
- 作者

## 核心代码

```css
.aplayer-title {
  font-family: "微软雅黑", "苹方", sans-serif !important;
  font-size: 14px !important;
  color: #343232 !important;
}
```

---

# 深色模式适配

这是整个美化里非常重要的一部分。

因为很多博客都有夜间模式。

---

## 核心思路

Butterfly 会自动添加：

```html
data-theme="dark"
```

因此我们可以这样写：

```css
[data-theme="dark"] .aplayer {
  background: rgba(22, 22, 22, 0.6) !important;
}
```

---

# 深色模式完整适配

我主要适配了：

- 背景
- 图标
- hover
- 当前播放
- 标题
- 歌单文字

---

## 图标颜色

```css
[data-theme="dark"] .aplayer .aplayer-info .aplayer-controller .aplayer-icon path {
  fill: #d4d4d4;
}
```

---

## 当前播放颜色

```css
[data-theme="dark"] .aplayer .aplayer-list ol li.aplayer-list-light {
  background: #564e55 !important;
}
```

---

# 自动隐藏播放器

这是整个播放器最实用的功能之一。

---

## 最终效果

播放器：

- 默认隐藏
- 鼠标靠近自动展开
- 不占页面空间
- 更优雅

---

## 核心代码

```css
.aplayer.aplayer-fixed.aplayer-narrow .aplayer-body {
  left: -66px !important;
}

.aplayer.aplayer-fixed.aplayer-narrow .aplayer-body:hover {
  left: 0 !important;
}
```

---

## 原理

通过：

```css
left: -66px;
```

让播放器默认隐藏。

再通过：

```css
:hover
```

恢复位置。

实现：

- 自动隐藏
- 悬停展开

这种交互方式非常适合侧边固定播放器。

---

# 如何在 Hexo Butterfly 中使用

## 创建 CSS 文件

例如：

```bash
/source/css/aplayer.css
```

将完整 CSS 放入其中。

---

## Butterfly 引入方式

修改主题配置：

```yaml
inject:
  head:
  bottom:
    - /css/aplayer.css
```

---

# 完整 CSS

将完整 CSS 粘贴到：

```bash
/source/css/aplayer.css
```

即可。

---

# 可以继续优化的方向

目前这套播放器已经足够日常使用。

但还可以继续升级。

---

## 1. 页面跳转不断播

可以通过：

- PJAX
- 全局单例播放器

实现。

这样博客切页时音乐不会中断。

---

## 2. 播放器拖拽

可以实现：

- 任意拖动
- 记忆位置
- 移动端适配

---

## 3. 动态渐变背景

例如：

```css
background: linear-gradient(...)
```

配合动画实现流光效果。

---

## 4. 音频频谱动画

可以加入：

- Canvas
- Web Audio API

实现动态频谱。

---

# 总结

这次美化主要目标是：

> 让播放器真正融入博客 UI。

而不仅仅只是：

> “页面里多了个播放器”。

最终实现了：

- 现代化毛玻璃
- 深色模式适配
- 当前播放高亮
- 自动隐藏交互
- 更统一的 UI 风格

整体体验提升还是非常明显的。

---

# 参考

- https://github.com/DIYgod/APlayer
- https://github.com/metowolf/MetingJS

---

如果这篇文章对你有帮助，欢迎收藏或者交流讨论。