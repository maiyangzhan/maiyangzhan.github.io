# GitHub IO 网站重构设计规范

## 概述

对 Luka Mai 的个人网站进行渐进式视觉重构，采用**科技感深色主题**，提升整体视觉冲击力和用户体验。

**设计风格：** 科技感深色主题 · 渐变光效 · 现代排版

---

## 1. 设计系统

### 色彩方案
| 用途 | 色值 |
|------|------|
| 背景主色 | `#0a0a1a` → `#1a1a3a` (渐变) |
| 主题蓝 | `#0d6efd` |
| 主题紫 | `#6610f2` |
| 成功绿 | `#10b981` |
| 警告橙 | `#f59e0b` |
| 文字主色 | `#ffffff` |
| 文字次要 | `rgba(255,255,255,0.6)` |
| 边框色 | `rgba(255,255,255,0.1)` |

### 字体
- 标题：系统字体栈 `-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto`
- 正文：`system-ui` 默认
- 代码：`Monaco, 'Menlo', monospace`

### 间距
- 页面最大宽度：`900px`
- section 间距：`60px`
- 卡片圆角：`16px`
- 按钮圆角：`8px`

### 动效
- 过渡时长：`0.3s`
- 缓动函数：`cubic-bezier(0.4, 0, 0.2, 1)`
- 悬停阴影：`0 8px 30px rgba(13,110,253,0.2)`

---

## 2. 页面结构

### 2.1 导航栏 (Navbar)
- **位置：** 粘性顶部
- **内容：** Logo（渐变方块 + 名字）+ 页面链接
- **状态：**
  - 当前页链接：`#0d6efd` 高亮
  - 悬停：`opacity: 0.8`
- **样式：** 半透明背景 + 底部边框

### 2.2 首页 (index.html)
**首屏区域 (Hero)**
- 头像：圆形 + 渐变光晕阴影 `box-shadow: 0 0 60px rgba(13,110,253,0.4)`
- 名字：渐变文字 `background: linear-gradient(135deg, #0d6efd, #a855f7)`
- 副标题：打字机效果（保留原有）
- 数据统计：文章数 + 主研领域
- CTA 按钮：渐变背景 + 阴影

**关于预览区**
- 渐变分隔线
- 个人简介文字
- 技能徽章网格

### 2.3 博客列表页 (blogs.html)
**英雄区**
- 标题 + 副标题
- 统计数据（文章数、主要标签）

**博客卡片**
- 背景：`var(--bs-tertiary-bg)`
- 左侧渐变色条（悬停显示）
- 悬停：上移 5px + 阴影光效
- 内容：图标 + 标题 + 描述（2行截断）+ 元信息（日期/阅读时间/标签）

### 2.4 关于页面 (about_me.html)
保留现有结构，优化样式一致性：
- 时间线样式保持
- 技能徽章使用统一渐变边框

### 2.5 博客文章页
保持现有功能（阅读进度条、目录导航、返回顶部），统一样式细节

---

## 3. 组件规范

### 3.1 技能徽章 (Skill Tag)
```css
background: rgba(color, 0.2);
color: color;
border: 1px solid rgba(color, 0.3);
border-radius: 20px;
padding: 8px 16px;
```
不同技能使用不同主题色：
- AI Chips → `#0d6efd`
- SRAM Computing → `#6610f2`
- Python → `#10b981`
- Verilog → `#f59e0b`

### 3.2 博客卡片
```css
background: var(--bs-tertiary-bg);
border: 1px solid var(--bs-border-color);
border-radius: 16px;
transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
```
悬停态：
- `transform: translateY(-5px)`
- `box-shadow: 0 8px 30px rgba(13,110,253,0.2)`
- 左侧色条 `opacity: 1`

### 3.3 渐变文字
```css
background: linear-gradient(135deg, #0d6efd, #a855f7);
-webkit-background-clip: text;
-webkit-text-fill-color: transparent;
```

### 3.4 CTA 按钮
```css
background: linear-gradient(135deg, #0d6efd, #6610f2);
color: white;
border: none;
padding: 14px 32px;
border-radius: 8px;
box-shadow: 0 4px 20px rgba(13,110,253,0.4);
```

---

## 4. 技术实现

### 4.1 框架
- 保持纯 HTML + CSS + Vanilla JS
- 使用 Bootstrap 5.3 (dark theme)
- 使用 Bootstrap Icons

### 4.2 CSS 架构
- 所有页面共享 `style` 标签（简单有效）
- CSS 变量：`--primary-color`, `--accent-color`
- 响应式：使用 Bootstrap grid

### 4.3 动效
- CSS `transition` 实现悬停效果
- `transform: translateY()` 实现卡片悬停
- `box-shadow` 配合渐变实现光效

---

## 5. 实施步骤

1. **创建共享 CSS 变量文件**（可选，未来升级用）
2. **重构 index.html** - 新导航 + Hero 区
3. **重构 blogs.html** - 新布局 + 卡片样式
4. **统一博客文章页样式**
5. **检查 about_me.html 样式一致性**
6. **测试所有页面响应式**
7. **Git 提交并推送**

---

## 6. 成功标准

- [ ] 首页首屏有视觉冲击力
- [ ] 导航清晰，当前页高亮正确
- [ ] 博客卡片悬停有动效反馈
- [ ] 所有页面使用统一色彩系统
- [ ] 深色主题一致，无突兀的亮色
- [ ] 移动端布局正常
