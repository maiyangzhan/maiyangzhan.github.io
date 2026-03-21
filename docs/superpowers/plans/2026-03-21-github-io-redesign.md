# GitHub IO 网站重构实施计划

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** 将 Luka Mai 的个人网站重构为科技感深色主题，提升视觉冲击力

**Architecture:** 渐进式增强 - 保持现有 HTML 结构，换肤 + 动画 + 更好布局。使用 Bootstrap 5.3 dark theme + 共享 CSS 变量实现统一风格。

**Tech Stack:** HTML5, CSS3, Vanilla JS, Bootstrap 5.3 (dark), Bootstrap Icons

---

## 文件结构

```
/ (项目根目录)
├── index.html              # 首页 - 完全重构
├── blogs.html              # 博客列表 - 完全重构
├── about_me.html           # 关于页 - 样式微调
├── blogs/
│   ├── openclaw-macos-deploy.html
│   ├── tmux install without root.html
│   ├── neovim install.html
│   └── linux terminal clash.html
└── docs/superpowers/specs/2026-03-21-github-io-redesign.md  # 设计规范
```

---

## 任务列表

### Task 1: 重构 index.html - 首页

**Files:**
- Modify: `index.html` (完全重写)

- [ ] **Step 1: 重写 index.html**
  - 新导航栏：Logo + 页面链接 + 当前页高亮
  - Hero 区：渐变头像光晕 + 渐变文字标题 + 数据统计 + CTA 按钮
  - 关于预览区：渐变分隔线 + 技能徽章
  - 保留打字机效果 JS

- [ ] **Step 2: 本地预览测试**
  - 用浏览器打开 index.html 检查布局

- [ ] **Step 3: 提交**
  ```bash
  git add index.html
  git commit -m "feat: 重构首页 - 科技感深色主题 Hero 区"
  ```

---

### Task 2: 重构 blogs.html - 博客列表页

**Files:**
- Modify: `blogs.html` (完全重写)

- [ ] **Step 1: 重写 blogs.html**
  - 新导航栏（与 index.html 一致）
  - 英雄区：标题 + 副标题 + 统计数据
  - 博客卡片列表（4篇博客）
  - 博客卡片样式：悬停动效 + 左侧渐变色条
  - 页脚：版权信息

- [ ] **Step 2: 本地预览测试**
  - 检查博客卡片悬停效果
  - 检查响应式布局

- [ ] **Step 3: 提交**
  ```bash
  git add blogs.html
  git commit -m "feat: 重构博客列表页 - 统一卡片样式和导航"
  ```

---

### Task 3: 统一博客文章页样式

**Files:**
- Modify: `blogs/openclaw-macos-deploy.html`
- Modify: `blogs/tmux install without root.html`
- Modify: `blogs/neovim install.html`
- Modify: `blogs/linux terminal clash.html`

- [ ] **Step 1: 更新 openclaw-macos-deploy.html**
  - 统一导航栏样式
  - 统一代码块样式
  - 检查阅读进度条、目录导航功能正常

- [ ] **Step 2: 更新其他 3 篇博客文章**
  - 确保导航栏、页脚样式与 blogs.html 一致

- [ ] **Step 3: 提交**
  ```bash
  git add blogs/
  git commit -m "style: 统一博客文章页样式 - 科技感深色主题"
  ```

---

### Task 4: 检查 about_me.html 样式一致性

**Files:**
- Modify: `about_me.html`

- [ ] **Step 1: 检查并更新 about_me.html**
  - 导航栏样式与其他页面一致
  - 时间线样式保持
  - 技能徽章使用统一渐变边框

- [ ] **Step 2: 提交**
  ```bash
  git add about_me.html
  git commit -m "style: 优化关于页面样式一致性"
  ```

---

### Task 5: 最终检查与推送

- [ ] **Step 1: 全局检查**
  - 所有页面导航栏一致
  - 所有页面深色主题一致
  - 所有页面响应式正常
  - 所有交互动效正常

- [ ] **Step 2: 推送到 GitHub**
  ```bash
  git push
  ```

- [ ] **Step 3: 线上验证**
  - 访问 https://maiyangzhan.github.io 检查效果

---

## 验收标准

- [ ] 首页首屏有视觉冲击力（渐变头像 + 渐变标题 + CTA）
- [ ] 导航栏在所有页面保持一致
- [ ] 博客卡片悬停有动效（上移 + 阴影）
- [ ] 所有页面使用统一深色主题
- [ ] 移动端布局正常
- [ ] 网站成功部署到 GitHub Pages
