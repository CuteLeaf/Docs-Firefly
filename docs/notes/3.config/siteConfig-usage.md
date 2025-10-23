---
title: 站点配置
createTime: 2025/01/27 18:38:13
permalink: /config/siteConfig-usage/
---
# 站点配置

## 概述

站点配置是 Firefly 的核心配置文件，包含网站的基本信息、主题设置、功能开关等所有基础配置。

## 文件位置

```
src/config/siteConfig.ts
```

## 基础配置

### 网站基本信息

```typescript
export const siteConfig: SiteConfig = {
  title: "Firefly", // 网站标题
  subtitle: "Demo site", // 网站副标题
  description: "Firefly 是一款基于 Astro 框架开发的清新美观且现代化个人博客主题...", // 网站描述
  keywords: [ // SEO关键词
    "Firefly",
    "Fuwari", 
    "Astro",
    "ACGN",
    "博客",
    "技术博客",
    "静态博客",
  ],
  lang: "zh_CN", // 网站语言
};
```

## 配置选项详解

### 基础信息

| 选项 | 类型 | 说明 | 必填 |
|------|------|------|------|
| `title` | `string` | 网站标题 | 是 |
| `subtitle` | `string` | 网站副标题 | 是 |
| `description` | `string` | 网站描述（SEO用） | 否 |
| `keywords` | `string[]` | SEO关键词数组 | 否 |
| `lang` | `string` | 网站语言代码 | 是 |

### 支持的语言

| 语言代码 | 语言名称 | 说明 |
|----------|----------|------|
| `zh_CN` | 简体中文 | 默认语言 |
| `zh_TW` | 繁体中文 | 台湾地区 |
| `en` | 英文 | 国际通用 |
| `ja` | 日文 | 日本地区 |
| `ko` | 韩文 | 韩国地区 |
| `es` | 西班牙文 | 西班牙语地区 |
| `th` | 泰文 | 泰国地区 |
| `vi` | 越南文 | 越南地区 |
| `tr` | 土耳其文 | 土耳其地区 |
| `id` | 印尼文 | 印尼地区 |

## 主题颜色配置

### 主题色设置

```typescript
themeColor: {
  hue: 155, // 主题色相 (0-360)
  fixed: false, // 是否固定主题色
  defaultMode: "system", // 默认模式
}
```

### 色相值参考

| 颜色 | 色相值 | 说明 |
|------|--------|------|
| 红色 | 0 | 热情、活力 |
| 橙色 | 30 | 温暖、友好 |
| 黄色 | 60 | 明亮、乐观 |
| 绿色 | 120 | 自然、清新 |
| 青色 | 180 | 冷静、专业 |
| 蓝色 | 240 | 稳重、可信 |
| 紫色 | 300 | 神秘、创意 |
| 粉色 | 330 | 温柔、浪漫 |

### 默认模式选项

| 模式 | 说明 | 适用场景 |
|------|------|----------|
| `"light"` | 浅色模式 | 日间使用 |
| `"dark"` | 深色模式 | 夜间使用 |
| `"system"` | 跟随系统 | 自动切换 |

## 网站图标配置

### Favicon 设置

```typescript
favicon: [
  {
    src: "/assets/images/favicon.ico", // 图标文件路径
    theme: "light", // 主题类型
    sizes: "32x32", // 图标大小
  },
  {
    src: "/assets/images/favicon-dark.ico",
    theme: "dark",
    sizes: "32x32",
  },
]
```

### 支持的图标格式

- **ICO**：传统格式，兼容性好
- **PNG**：现代格式，支持透明
- **SVG**：矢量格式，可缩放
- **WebP**：现代格式，文件小

### 图标尺寸建议

| 尺寸 | 用途 | 说明 |
|------|------|------|
| 16x16 | 浏览器标签 | 最小尺寸 |
| 32x32 | 浏览器标签 | 标准尺寸 |
| 48x48 | 书签 | 中等尺寸 |
| 64x64 | 桌面快捷方式 | 较大尺寸 |
| 128x128 | 移动设备 | 高分辨率 |
| 192x192 | PWA | 应用图标 |
| 512x512 | PWA | 启动画面 |

## Logo 配置

### Logo 类型

#### 1. Astro 图标库

```typescript
logoIcon: {
  type: "icon",
  value: "material-symbols:home-pin-outline" // 图标名称
}
```

#### 2. 本地图片

```typescript
logoIcon: {
  type: "image",
  value: "/assets/images/logo.webp", // 图片路径
  alt: "Firefly Logo" // 替代文本
}
```

#### 3. 网络图片

```typescript
logoIcon: {
  type: "image",
  value: "https://example.com/logo.png", // 图片URL
  alt: "Firefly Logo"
}
```

### 常用图标示例

```typescript
// 首页图标
logoIcon: {
  type: "icon",
  value: "material-symbols:home-pin-outline"
}

// 代码图标
logoIcon: {
  type: "icon", 
  value: "material-symbols:code"
}

// 博客图标
logoIcon: {
  type: "icon",
  value: "material-symbols:article"
}

// 自定义图片
logoIcon: {
  type: "image",
  value: "/assets/images/logo.svg",
  alt: "我的博客"
}
```

## 背景壁纸配置

### 基础配置

```typescript
backgroundWallpaper: {
  enable: true, // 启用背景壁纸
  mode: "banner", // 壁纸模式
  src: {
    desktop: "/assets/images/d1.webp", // 桌面背景
    mobile: "/assets/images/m1.webp", // 移动背景
  },
  position: "10% 20%", // 图片位置
}
```

### 壁纸模式

| 模式 | 说明 | 使用场景 |
|------|------|----------|
| `"banner"` | Banner壁纸模式 | 主页横幅 |
| `"overlay"` | 全屏透明覆盖 | 背景装饰 |

### 图片位置配置

```typescript
// 常用位置值
position: "center"           // 居中
position: "top"              // 顶部居中
position: "bottom"           // 底部居中
position: "left"             // 左侧居中
position: "right"            // 右侧居中
position: "10% 20%"          // 自定义位置
position: "left top"         // 左上角
position: "right bottom"     // 右下角
```

## 功能配置

### 目录功能

```typescript
toc: {
  enable: true, // 启用目录
  depth: 3, // 目录深度 (1-6)
}
```

### 文章列表布局配置

```typescript
postListLayout: {
  defaultMode: "list", // 默认布局模式："list" 列表模式，"grid" 网格模式
  allowSwitch: true, // 是否允许用户切换布局
}
```

#### 布局模式说明

| 模式 | 说明 | 特点 |
|------|------|------|
| `"list"` | 列表模式 | 单列布局，显示文章封面，适合详细阅读 |
| `"grid"` | 网格模式 | 双列布局，无封面，适合快速浏览 |

#### 响应式行为

- 屏幕宽度 < 1200px 时自动切换为列表模式
- 布局切换按钮在小屏幕时自动隐藏
- 用户偏好会保存到 localStorage

### 分页配置

```typescript
pagination: {
  postsPerPage: 8, // 每页显示的文章数量
}
```

### 文章编辑时间

```typescript
showLastModified: true, // 显示上次编辑时间
```

### OpenGraph图片

```typescript
generateOgImages: false, // 生成OG图片（影响构建时间）
```

### 追番配置

```typescript
bangumi: {
  userId: "1163581", // Bangumi用户ID
}
```

## 页面开关配置

### 页面功能开关

```typescript
pages: {
  anime: true, // 追番页面开关
  projects: true, // 项目展示页面开关
  timeline: true, // 时间线页面开关
  skills: true, // 技能页面开关
}
```

## 完整配置示例

### 技术博客配置

```typescript
export const siteConfig: SiteConfig = {
  title: "张三的技术博客",
  subtitle: "分享技术，记录成长",
  description: "专注于前端开发、Node.js 和云原生技术的个人技术博客",
  keywords: ["前端", "JavaScript", "React", "Node.js", "技术博客"],
  lang: "zh_CN",
  
  themeColor: {
    hue: 200, // 蓝色主题
    fixed: false,
    defaultMode: "system",
  },
  
  favicon: [
    {
      src: "/assets/images/favicon.ico",
      theme: "light",
      sizes: "32x32",
    },
  ],
  
  logoIcon: {
    type: "icon",
    value: "material-symbols:code",
  },
  
  backgroundWallpaper: {
    enable: true,
    mode: "banner",
    src: {
      desktop: "/assets/images/tech-bg.webp",
      mobile: "/assets/images/tech-bg-mobile.webp",
    },
    position: "center",
  },
  
  toc: {
    enable: true,
    depth: 3,
  },
  
  postListLayout: {
    defaultMode: "list",
    allowSwitch: true,
  },
  
  pagination: {
    postsPerPage: 8,
  },
  
  showLastModified: true,
  generateOgImages: true,
  
  pages: {
    anime: false, // 不显示追番页面
    projects: true,
    timeline: true,
    skills: true,
  },
};
```

### 个人网站配置

```typescript
export const siteConfig: SiteConfig = {
  title: "李四的个人网站",
  subtitle: "设计师 & 开发者",
  description: "UI/UX 设计师，全栈开发者，分享设计心得和技术经验",
  keywords: ["设计", "UI", "UX", "前端", "全栈"],
  lang: "zh_CN",
  
  themeColor: {
    hue: 300, // 紫色主题
    fixed: false,
    defaultMode: "light",
  },
  
  favicon: [
    {
      src: "/assets/images/favicon.png",
      theme: "light",
      sizes: "32x32",
    },
  ],
  
  logoIcon: {
    type: "image",
    value: "/assets/images/logo.svg",
    alt: "李四的Logo",
  },
  
  backgroundWallpaper: {
    enable: true,
    mode: "overlay",
    src: "/assets/images/pattern.webp",
    position: "center",
  },
  
  toc: {
    enable: true,
    depth: 2,
  },
  
  postListLayout: {
    defaultMode: "grid",
    allowSwitch: true,
  },
  
  pagination: {
    postsPerPage: 6,
  },
  
  showLastModified: false,
  generateOgImages: false,
  
  pages: {
    anime: true,
    projects: true,
    timeline: true,
    skills: false, // 不显示技能页面
  },
};
```

## 注意事项

1. **SEO优化**：合理设置标题、描述和关键词
2. **性能考虑**：大图片会影响加载速度
3. **响应式设计**：确保在不同设备上正常显示
4. **语言支持**：选择正确的语言代码

## 常见问题

**Q: 如何更换网站标题？**
A: 修改 `title` 和 `subtitle` 字段

**Q: 如何设置主题颜色？**
A: 修改 `themeColor.hue` 的值（0-360）

**Q: 如何更换Logo？**
A: 修改 `logoIcon` 配置，支持图标和图片两种方式

**Q: 如何禁用某些页面？**
A: 在 `pages` 配置中将对应选项设为 `false`

**Q: 如何设置多语言？**
A: 修改 `lang` 字段，并配置对应的翻译文件

**Q: 如何优化SEO？**
A: 合理设置 `description` 和 `keywords` 字段

**Q: 如何设置文章列表布局？**
A: 修改 `postListLayout.defaultMode` 为 `"list"` 或 `"grid"`，设置 `allowSwitch` 控制是否允许用户切换

**Q: 如何调整每页显示的文章数量？**
A: 修改 `pagination.postsPerPage` 的值

**Q: 布局切换按钮在哪里？**
A: 在导航栏右侧，屏幕宽度大于1200px时显示

**Q: 为什么小屏幕上看不到布局切换按钮？**
A: 小屏幕（<1200px）会自动使用列表模式，因此隐藏切换按钮
