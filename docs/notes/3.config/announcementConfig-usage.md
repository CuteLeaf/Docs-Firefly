---
title: 公告配置
createTime: 2025/01/27 18:38:13
permalink: /config/announcementConfig-usage/
---
# 公告配置

## 概述

公告配置用于在网站顶部显示重要通知、更新信息或欢迎消息。

## 文件位置

```
src/config/announcementConfig.ts
```

## 基础配置

### 启用公告功能

```typescript
export const announcementConfig: AnnouncementConfig = {
  title: "公告", // 公告标题
  content: "欢迎来到我的博客！这是一则示例公告。", // 公告内容
  closable: true, // 允许用户关闭公告
  link: {
    enable: true, // 启用链接
    text: "了解更多", // 链接文本
    url: "/about/", // 链接 URL
    external: false, // 内部链接
  },
};
```

## 配置选项详解

### 基础设置

| 选项 | 类型 | 说明 | 默认值 |
|------|------|------|--------|
| `title` | `string` | 公告标题 | `"公告"` |
| `content` | `string` | 公告内容 | `"欢迎来到我的博客！这是一则示例公告。"` |
| `closable` | `boolean` | 是否可关闭 | `true` |

### 链接设置

| 选项 | 类型 | 说明 | 默认值 |
|------|------|------|--------|
| `link.enable` | `boolean` | 是否启用链接 | `true` |
| `link.text` | `string` | 链接文本 | `"了解更多"` |
| `link.url` | `string` | 链接地址 | `"/about/"` |
| `link.external` | `boolean` | 是否外部链接 | `false` |

## 使用场景

### 1. 欢迎消息

```typescript
export const announcementConfig: AnnouncementConfig = {
  title: "欢迎",
  content: "欢迎来到我的个人博客！这里分享技术文章和生活感悟。",
  closable: true,
  link: {
    enable: true,
    text: "了解我",
    url: "/about/",
    external: false,
  },
};
```

### 2. 更新通知

```typescript
export const announcementConfig: AnnouncementConfig = {
  title: "更新通知",
  content: "网站已更新到 v2.0 版本，新增了多项功能！",
  closable: true,
  link: {
    enable: true,
    text: "查看更新日志",
    url: "/changelog/",
    external: false,
  },
};
```

### 3. 重要提醒

```typescript
export const announcementConfig: AnnouncementConfig = {
  title: "重要提醒",
  content: "网站将于今晚 22:00-24:00 进行维护，期间可能无法访问。",
  closable: false, // 重要提醒不可关闭
  link: {
    enable: false, // 不需要链接
    text: "",
    url: "",
    external: false,
  },
};
```

### 4. 外部链接

```typescript
export const announcementConfig: AnnouncementConfig = {
  title: "新项目发布",
  content: "我的新项目已经发布到 GitHub！",
  closable: true,
  link: {
    enable: true,
    text: "查看项目",
    url: "https://github.com/username/project",
    external: true, // 外部链接
  },
};
```

## 样式自定义

公告组件支持通过 CSS 自定义样式：

```css
/* 公告容器 */
.announcement-container {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  padding: 1rem;
  border-radius: 8px;
  margin-bottom: 1rem;
}

/* 公告标题 */
.announcement-title {
  font-weight: bold;
  font-size: 1.1rem;
  margin-bottom: 0.5rem;
}

/* 公告内容 */
.announcement-content {
  line-height: 1.6;
  margin-bottom: 1rem;
}

/* 关闭按钮 */
.announcement-close {
  position: absolute;
  top: 0.5rem;
  right: 0.5rem;
  background: none;
  border: none;
  color: white;
  cursor: pointer;
  font-size: 1.2rem;
}

/* 链接样式 */
.announcement-link {
  color: #ffd700;
  text-decoration: underline;
  font-weight: 500;
}
```

## 响应式设计

公告组件在不同设备上会自动适配：

- **桌面端**：完整显示所有内容
- **平板端**：调整字体大小和间距
- **移动端**：优化布局，确保可读性

## 注意事项

1. **内容长度**：建议公告内容不要过长，保持简洁明了
2. **关闭状态**：用户关闭公告后，状态会保存在本地存储中
3. **链接安全**：外部链接会自动添加 `rel="noopener"` 属性
4. **无障碍访问**：公告组件支持键盘导航和屏幕阅读器

## 常见问题

**Q: 如何禁用公告功能？**
A: 在侧边栏配置中将公告组件设置为禁用状态

**Q: 公告内容支持 Markdown 吗？**
A: 目前不支持 Markdown，只支持纯文本

**Q: 如何让公告不可关闭？**
A: 将 `closable` 设置为 `false`

**Q: 如何添加多个公告？**
A: 目前只支持单个公告，如需多个公告需要修改源码

**Q: 公告在哪些页面显示？**
A: 公告会在所有页面的顶部显示（除了特殊页面如 404 页面）
