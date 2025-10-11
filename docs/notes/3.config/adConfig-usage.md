---
title: 广告配置
createTime: 2025/10/11 18:38:13
permalink: /config/adConfig-usage/
---
# 广告配置

## 概述

`adConfig.ts` 文件用于配置网站中的广告组件，支持纯图片广告和完整内容广告两种类型。

## 文件位置

```
src/config/adConfig.ts
```

## 配置结构

### AdConfig 类型定义

```typescript
interface AdConfig {
  title?: string;           // 广告标题
  content?: string;         // 广告内容描述
  image?: {                 // 图片配置
    src: string;           // 图片路径
    alt: string;           // 图片描述
    link?: string;         // 图片链接
    external?: boolean;    // 是否外部链接
  };
  link?: {                 // 按钮链接配置
    text: string;          // 按钮文字
    url: string;           // 链接地址
    external?: boolean;    // 是否外部链接
  };
  closable: boolean;       // 是否可关闭
  displayCount: number;    // 显示次数（-1为无限）
  padding?: {              // 内边距配置
    all?: string;          // 统一内边距
    top?: string;          // 顶部内边距
    right?: string;        // 右侧内边距
    bottom?: string;       // 底部内边距
    left?: string;         // 左侧内边距
  };
}
```

## 配置示例

### 1. 纯图片广告（无边距）

```typescript
export const adConfig1: AdConfig = {
  image: {
    src: "/assets/images/d1.webp",
    alt: "广告横幅",
    link: "#",
    external: true,
  },
  closable: true,
  displayCount: -1,
  padding: {
    all: "0", // 零边距，图片占满整个组件
  },
};
```

**特点：**
- 只显示图片，无文字内容
- 零边距设计，图片占满整个组件
- 支持点击跳转
- 可关闭

### 2. 完整内容广告

```typescript
export const adConfig2: AdConfig = {
  title: "支持博主",
  content: "如果您觉得本站内容对您有帮助，欢迎支持我们的创作！",
  image: {
    src: "/assets/images/d2.webp",
    alt: "支持博主",
    link: "about/",
    external: false,
  },
  link: {
    text: "支持一下",
    url: "about/",
    external: false,
  },
  closable: true,
  displayCount: -1,
  padding: {
    // 使用默认边距
  },
};
```

**特点：**
- 包含标题、内容、图片和按钮
- 支持内部和外部链接
- 可自定义内边距
- 可关闭

## 配置选项详解

### 图片配置 (image)

| 属性 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `src` | string | 是 | 图片文件路径，支持相对路径和绝对路径 |
| `alt` | string | 是 | 图片的替代文本，用于无障碍访问 |
| `link` | string | 否 | 点击图片时的跳转链接 |
| `external` | boolean | 否 | 是否为外部链接，影响链接打开方式 |

### 链接配置 (link)

| 属性 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `text` | string | 是 | 按钮显示的文字 |
| `url` | string | 是 | 跳转的URL地址 |
| `external` | boolean | 否 | 是否为外部链接 |

### 内边距配置 (padding)

支持以下配置方式：

```typescript
// 方式1：统一内边距
padding: {
  all: "1rem"
}

// 方式2：分别设置各边
padding: {
  top: "0",
  right: "1rem", 
  bottom: "1rem",
  left: "1rem"
}

// 方式3：混合使用
padding: {
  all: "1rem",
  top: "0"  // 顶部会覆盖all设置
}
```

### 显示控制

| 属性 | 类型 | 说明 |
|------|------|------|
| `closable` | boolean | 是否显示关闭按钮 |
| `displayCount` | number | 显示次数，-1表示无限显示 |

## 在侧边栏中使用

广告配置需要在 `sidebarConfig.ts` 中启用：

```typescript
{
  type: "advertisement",
  enable: true,  // 启用广告组件
  order: 6,      // 显示顺序
  position: "sticky",
  configId: "ad1", // 对应 adConfig1
}
```

## 图片路径规范

### 推荐路径格式

```typescript
// 本地图片（推荐）
src: "/assets/images/ad-banner.webp"

// 外部图片
src: "https://example.com/banner.jpg"
```

### 支持的图片格式

- `.webp` (推荐，文件小)
- `.jpg` / `.jpeg`
- `.png`
- `.svg`

## 最佳实践

### 1. 图片优化

```typescript
// 使用WebP格式，文件更小
image: {
  src: "/assets/images/banner.webp",
  alt: "广告描述"
}
```

### 2. 响应式设计

```typescript
// 为不同设备准备不同尺寸的图片
image: {
  src: "/assets/images/banner-desktop.webp", // 桌面版
  // 移动版在CSS中通过媒体查询处理
}
```

### 3. 无障碍访问

```typescript
// 提供有意义的alt文本
image: {
  src: "/assets/images/support-banner.webp",
  alt: "支持博主创作，点击了解更多"
}
```

### 4. 链接安全

```typescript
// 外部链接设置external为true
link: {
  text: "访问官网",
  url: "https://example.com",
  external: true  // 会在新标签页打开
}
```

## 常见问题

### Q: 如何禁用某个广告？

A: 在 `sidebarConfig.ts` 中将对应组件的 `enable` 设为 `false`：

```typescript
{
  type: "advertisement",
  enable: false,  // 禁用广告
  configId: "ad1",
}
```

### Q: 如何修改广告显示顺序？

A: 调整 `sidebarConfig.ts` 中组件的 `order` 值，数字越小越靠前。

### Q: 广告图片不显示怎么办？

A: 检查图片路径是否正确，确保图片文件存在于 `public` 目录中。

## 注意事项

1. 图片文件应放在 `public/assets/images/` 目录下
2. 外部链接建议设置 `external: true`
3. 广告内容应符合网站主题和用户需求
4. 定期更新广告内容以保持新鲜感
